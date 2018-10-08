# `MySQL`不一样的`UPDATE`更新操作  
> 一条MySQL语句搞定 - “有就更新，没则新增”数据的操作。  

在这个世界上，有很多很多的业务场景需要数据库的支持和操作。这期就讲讲站内通讯系统的一个需求，一起来看看吧！

```sql
	INSERT INTO message_global
		( message_text_id, rec_id, status )
	VALUES 
		( :m,:n,:t )
	ON DUPLICATE KEY UPDATE
		message_text_id = :m ,
		rec_id = :n ,
		status = :t
```

这个`SQL`语句的意思是：新建一条数据，如果有就触发唯一索引执行更新数据操作，没有就新建一条数据。

表设计需求是为了缓解数据量一下更新太多对数据库造成冲击，所以用户每查看一次消息就更新一条数据状态而设计的，表结构如下：

```sql
-- 系统消息表建立
DROP TABLE IF EXISTS `message_global`;
CREATE TABLE IF NOT EXISTS `message_global`(
    `id` INT UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'ID',
    `message_text_id` INT UNSIGNED NOT NULL COMMENT '消息ID',
    `rec_id` INT UNSIGNED NOT NULL COMMENT '接收者ID',
    `time` TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `status` TINYINT(1) NOT NULL DEFAULT '1' COMMENT '状态(单选):0=删除,1=未读,2=已读',
    PRIMARY KEY(`id`),
    UNIQUE KEY `id` (`id`),
    UNIQUE KEY `mr_id` (`message_text_id`, `rec_id`),
    KEY `message_text_id` (`message_text_id`),
    KEY `rec_id` (`rec_id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='系统消息管理表';
```

其中这句```UNIQUE KEY `mr_id` (`message_text_id`, `rec_id`),```是组合唯一索引，所以新建相同的数据就会触发组合唯一索引，达到修改这条数据的作用。

这样一条`SQL`语句就达到了 “有就更新，没则新增”数据的操作，好神奇啊是不是？赶快收藏吧！

Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:8[/hermit]
