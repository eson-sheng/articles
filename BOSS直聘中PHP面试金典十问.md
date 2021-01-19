# BOSS直聘中PHP面试金典十问

## 1.什么是缓存穿透？
缓存穿透是指查询一个一定不存在的数据，由于缓存是不命中时被动写的，并且出于容错考虑，如果从存储层查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到存储层去查询，失去了缓存的意义。在流量大时，可能DB就挂掉了，要是有人利用不存在的key频繁攻击我们的应用，这就是漏洞。
解决办法：
**查询条件增加过滤，布置缓存空数据（不管查询是否有结果集，都缓存起来）。**

## 2.什么是缓存击穿？
缓存击穿是一些设置了过期时间的缓存数据正好过期了，然后有大量请求来访问这个数据成为了热点数据。这个时候，大并发的请求可能会瞬间把后端DB压垮。
解决办法：
**设置key不存在时候用的互斥锁等待重新点燃缓存数据。举例：**
```java
public String get(key) {
  String value = redis.get(key);
  if (value == null) { //代表缓存值过期
    //设置3min的超时，防止del操作失败的时候，下次缓存过期一直不能load db
    // 将key的值设为value,当且仅当key不存在的时候,成功返回1,不成功返回0
    if (redis.setnx(key_mutex, 1, 3 * 60) == 1) {  //代表设置成功
      value = db.get(key);
      redis.set(key, value, expire_secs);
      redis.del(key_mutex);
    } else {  //这个时候代表同时候的其他线程已经load db并回设到缓存了，这时候重试获取缓存值即可
      sleep(50);
      get(key);  //重试
    }
  } else {
    return value;
  }
}
```

## 3.epoll与select有什么区别？
- epoll 和 select 都是 I/O 多路复用的技术，都可以实现同时监听多个 I/O 事件的状态。
- epoll 相比 select 效率更高，主要是基于其操作系统支持的I/O事件通知机制，而 select 是基于轮询机制。

## 4.单机redis与集群redis？
集群高可用和易扩展，同时增加了运维成本。另外，memcahce使用多线程，主线程listen，多个worker子线程执行读写，可能会出现锁冲突。redis是单线程的，这样虽然不用考虑锁对插入修改数据造成的时间的影响，但是无法利用多核提高整体的吞吐量，只能选择多开redis来解决。

## 5.为什么memcache只支持kv，而redis支持类型多？
> memcache是缓存的存储，而redis更像是缓存数据库

- 从数据结构上来说，redis在kv模式上，支持5中数据结构，String、list、hash、set、zset，并支持很多相关的计算，比如排序、阻塞等，而memcache只支持kv简单存储。所以当你的缓存中不只需要存储kv模型的数据时，redis丰富的数据操作空间，绝对是非常好的选择，另外说一句，利用redis可以高效的实现类似于单集群下的阻塞队列、锁及线程通信等功能。
- 从可靠性的角度来说，redis支持持久化，有快照和AOF两种方式，而memcache是纯的内存存储，不支持持久化的。
- 从内存管理方面来说，redis也有自己的内存机制，redis采用申请内存的方式，会把带过期时间的数据存放到一起，redis理论上能够存储比物理内存更多的数据，当数据超量时，会引发swap，把冷数据刷到磁盘上。而memcache把所有的数据存储在物理内存里。memcache使用预分配池管理，会提前把内存分为多个slab，slab又分成多个不等大小的chunk，chunk从最小的开始，根据增长因子增长内存大小。redis更适合做数据存储，memcache更适合做缓存，memcache在存储速度方面也会比redis这种申请内存的方式来的快。
- 从数据一致性来说，memcache提供了cas命令，可以保证多个并发访问操作同一份数据的一致性问题。 redis是串行操作，所以不用考虑数据一致性的问题。
- 从IO角度来说，选用的I/O多路复用模型，虽然单线程不用考虑锁等问题，但是还要执行kv数据之外的一些排序、聚合功能，复杂度比较高。memcache也选用非阻塞的I/O多路复用模型，速度更快一些。
- 从线程角度来说，memcahce使用多线程，主线程listen，多个worker子线程执行读写，可能会出现锁冲突。redis是单线程的，这样虽然不用考虑锁对插入修改数据造成的时间的影响，但是无法利用多核提高整体的吞吐量，只能选择多开redis来解决。
从集群方面来说，redis天然支持高可用集群，支持主从，而memcache需要自己实现类似一致性hash的负载均衡算法才能解决集群的问题，扩展性比较低。

## 6.redis数据过期策略是什么？
- 定时过期：每个设置过期时间的key都需要创建一个定时器，到过期时间就会立即清除。该策略可以立即清除过期的数据，对内存很友好；但是会占用大量的CPU资源去处理过期的数据，从而影响缓存的响应时间和吞吐量。
- 惰性过期：只有当访问一个key时，才会判断该key是否已过期，过期则清除。该策略可以最大化地节省CPU资源，却对内存非常不友好。极端情况可能出现大量的过期key没有再次被访问，从而不会被清除，占用大量内存。
- 定期过期：每隔一定的时间，会扫描一定数量的数据库的expires字典中一定数量的key，并清除其中已过期的key。该策略是前两者的一个折中方案。通过调整定时扫描的时间间隔和每次扫描的限定耗时，可以在不同情况下使得CPU和内存资源达到最优的平衡效果。
(expires字典会保存所有设置了过期时间的key的过期时间数据，其中，key是指向键空间中的某个键的指针，value是该键的毫秒精度的UNIX时间戳表示的过期时间。键空间是指该Redis集群中保存的所有键。)

## 7.如何快速定位php程序运行慢的地方？
[xdebug](https://pecl.php.net/package/xdebug) [xhprof](https://pecl.php.net/package/xhprof)

## 8.一个事务里面如果嵌套一个curl操作，会发生什么？
- curl 如果产生 Fatal error，程序不往下执行，事务交由自动处理程序处理（通常是自动回滚）；
- curl不产生致命错误，将不影响事务的处理；
- 如果在事务中必须使用curl的化，最好设置curl的超时时间,以便主动控制事务回滚。

## 9.cgi和fastcgi的关系？
## 10.php-fpm和fastcgi的关系？
CGI：是 Web Server 与 Web Application 之间数据交换的一种协议。
FastCGI：同 CGI，是一种通信协议，但比 CGI 在效率上做了一些优化。同样，SCGI 协议与 FastCGI 类似。
PHP-CGI：是 PHP （Web Application）对 Web Server 提供的 CGI 协议的接口程序。
PHP-FPM：是 PHP（Web Application）对 Web Server 提供的 FastCGI 协议的接口程序，额外还提供了相对智能一些任务管理。

------

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~

[hermit auto='1' loop='0' unexpand='1' fullheight='0']remote#:24[/hermit]
