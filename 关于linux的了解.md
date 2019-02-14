# 为什么使用Linux系统而不是Windows系统
![linux-windows](https://blog.eson.site/wp-content/uploads/2019/02/linux-windows.png)

# 它是开源系统
每一位投身于Linux行业的技术人或者程序员只要听到开源项目就会由衷地感到自豪，这是一种从骨子里带有的独特情怀。开源的企业不单纯是为了利益，而是互相扶持，努力服务好更多的用户。开源软件最重要的特性有下面这些:

>**低风险**：使用闭源软件无疑把命运交付给他人，一旦封闭的源代码没有人来维护，你将进退维谷；而且相较于商业软件公司，开源社区很少存在倒闭的问题。
**高品质**：相较于闭源软件产品，开源项目通常是由开源社区来研发及维护的，参与编写、维护、测试的用户量众多，一般的bug还没有等爆发就已经被修补。
**低成本**：开源工作者都是在幕后默默且无偿地付出劳动成果，为美好的世界贡献一份力量，因此使用开源社区推动的软件项目可以节省大量的人力、物力和财力。
**更透明**：没有哪个笨蛋会把木马、后门等放到开放的源代码中，这样无疑是把自己的罪行暴露在阳光之下。

开放源代码，用户可利用源代码在其基础上修改和学习，但开源系统同样也有版权，同样也受法律保护。
下面介绍一下开源许可证：
![开源许可证](https://blog.eson.site/wp-content/uploads/2019/02/开源许可证.png)
世界上的开源许可证，大概有[上百种](http://www.gnu.org/licenses/license-list.html)。很少有人搞得清楚它们的区别。即使在最流行的六种，在这之中做选择，也很复杂。
 - [GPL](http://www.gnu.org/licenses/gpl.html)
 - [BSD](http://en.wikipedia.org/wiki/BSD_licenses)
 - [MIT](http://en.wikipedia.org/wiki/MIT_License)
 - [Mozilla](http://www.mozilla.org/MPL/)
 - [Apache](http://www.apache.org/licenses/LICENSE-2.0)
 - [LGPL](http://www.gnu.org/copyleft/lesser.html)

# 常见的Linux系统版本

### 红帽企业系统 - redhat
![redhat](https://blog.eson.site/wp-content/uploads/2019/02/redhat.png)
红帽企业系统（RedHatEnterpriseLinux,RHEL.）. 红帽公司是全球最大的开源技术厂商，RHEL是全世界内使用最广泛的Linux系统。RHEL系统具有极强的性能与稳定性，并且在全球范围内拥有完善的技术支持，也是红帽认证以及众多生产环境中使用的系统。对于商业模式的系统有些组件然而并不是完全免费的，正所谓软件给你服务需要充会员。

### 社区企业操作系统（Community Enterprise Operating System，CentOS）
![centos](https://blog.eson.site/wp-content/uploads/2019/02/centos.jpg)
通过把RHEL系统重新编译并发布给用户免费使用的Linux系统，具有广泛的使用人群。CentOS当前已被红帽公司“收编”。如果企业使用RedHat的付费服务，那么任何时候只要系统出了问题，用钱直接能召来厂家人员处理。而像Centos这类免费分发版本是完全没有人负责售后的。所以企业用户会一直采购RedHat这样的商品。而个人用户由于付不起或者没有必要支付费用，会一直下载并享受和RHEL一样的软件Centos。这个我觉得其实对双方都是良性的，如果centos出了bug，其实与RedHat的企业利益没有直接关系（但是有间接影响），RedHat不用赔偿商业用户一分钱，但是反手就能修复RHEL的Bug。

### Fedora
![fedora](https://blog.eson.site/wp-content/uploads/2019/02/fedora.png)
由红帽公司发布的桌面版系统套件（目前已经不限于桌面版）。用户可免费体验到最新的技术或工具，这些技术或工具在成熟后会被加入到RHEL系统中，因此Fedora也称为RHEL系统的“试验田”。运维人员如果想时刻保持自己的技术领先，就应该多关注此类Linux系统的发展变化及新特性，不断改变自己的学习方向。

### Debian
![debian](https://blog.eson.site/wp-content/uploads/2019/02/debian.png)
稳定性、安全性强，提供了免费的基础支持，可以良好地支持各种硬件架构，以及提供近十万种不同的开源软件，在国外拥有很高的认可度和使用率。

### Ubuntu
![ubuntu](https://blog.eson.site/wp-content/uploads/2019/02/ubuntu.png)
是一款派生自Debian的操作系统，对新款硬件具有极强的兼容能力。Ubuntu与Fedora都是极其出色的Linux桌面系统，而且Ubuntu也可用于服务器领域。

### Deepin
![deepin](https://blog.eson.site/wp-content/uploads/2019/02/deepin.jpeg)
国产操作系统典范：deepin操作系统 。Deepin是由武汉深之度科技有限公司开发的Linux发行版。Deepin 是一个基于 Linux 的操作系统，专注于使用者对日常办公、学习、生活和娱乐的操作体验的极致，适合笔记本、桌面计算机和一体机。Deepin是中国最活跃的 Linux 发行版，Deepin 为所有人提供稳定、高效的操作系统，强调安全、易用、美观。其口号为“免除新手痛苦，节约老手时间”。在社区的参与下，“让 Linux 更易用”也不断变成可以触摸的现实。

# 了解红帽认证
![certificate](https://blog.eson.site/wp-content/uploads/2019/02/certificate.png)
**红帽认证系统管理员**（Red Hat Certified System Administrator，RHCSA）属于Linux系统的初级认证，比较适合Linux爱好者。该认证要求考生对Linux系统有一定的了解，并且能够熟练使用Linux命令来完成以下任务：
- 管理文件、目录、文档以及命令行环境；
- 使用分区、LVM逻辑卷管理本地存储；
- 安装、更新、维护、配置系统与核心服务；
- 熟练创建、修改、删除用户与用户组，并使用LDAP进行集中目录身份认证；
- 熟练配置防火墙以及SELinux来保障系统安全。

**红帽认证工程师**（Red Hat Certified Engineer，RHCE）属于Linux系统的中级水平认证，难度相对RHCSA认证来讲更大，而且要求考生必须已获得RHCSA认证。该认证适合有基础的Linux运维管理员，主要考察对下列服务的管理与配置能力：
- 熟练配置防火墙规则链与SElinux安全上下文；
- 配置iSCSI（互联网小型计算机系统接口）服务；
- 编写Shell脚本来批量创建用户、自动完成系统的维护任务；
- 配置HTTP/HTTPS网络服务；
- 配置FTP服务；
- 配置NFS服务；
- 配置SMB服务；
- 配置SMTP服务；
- 配置SSH服务；
- 配置NTP服务。

**红帽认证架构师**（Red Hat Certified Architect，RHCA）属于Linux系统的最高级别认证，是公认的Linux操作系统顶级认证，目前中国仅有不到1000人（2017年更新数据）持有该认证。考生需要在获得RHCSA与RHCE认证后再完成5门课程的考试才能获得RHCA认证，因此难度最大，备考时间最长，费用也最高（考试费约在1.8万元～2.1万元人民币）。该认证考察的是考生对红帽卫星服务、红帽系统集群、红帽虚拟化、系统性能调优以及红帽云系统的安装搭建与维护能力。
>红帽RHEL 7版本的RHCA认证需要完成至少5门考试。这5门考试的时间不同，但均为210分合格（70%）。而且红帽公司非常注重RHCA架构师认证的实用性，所以课程总是在随行业趋势而不断调整。

下表为2017年最新版的考试课程。欲取得红帽RHCA认证，您必须通过以下任意5门认证考试。

| 考试代码 | 认证名称 |
| ------------ | ------------ |
| EX210  |  红帽 OpenStack 认证系统管理员考试  |
| EX220  |  红帽混合云管理专业技能证书考试  |
| EX236  |  红帽混合云存储专业技能证书考试  |
| EX248  |  红帽认证 JBoss 管理员考试  |
| EX280  |  红帽平台即服务专业技能证书考试  |
| EX318  |  红帽认证虚拟化管理员考试  |
| EX401  |  红帽部署和系统管理专业技能证书考试  |
| EX413  |  红帽服务器固化专业技能证书考试  |
| EX436  |  红帽集群和存储管理专业技能证书考试  |
| EX442  |  红帽性能调优专业技能证书考试  |

------

有一种想报名考试的冲动！好啦，今天情人节约会去了。
Thanks♪(･ω･)ﾉ 感谢你长得那么好看还来看我的博客！see you around ~
