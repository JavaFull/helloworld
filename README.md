# 零、helloworld
导航项目

# 一、学习原则

## 1、数量or质量？

质量

## 2、28原则

技术太多，不管是深度还是广度，新技术层出不穷，人的精力是有限的，不可能所有都学。

> 技术的多样性、深度、广度和人的精力的有限性是一对矛盾，所以要有重点有目标的去学

要学底层本质，这门技术，用了什么算法，底层用了操作系统的什么机制，或者和操作系统、网络的一些通用原理有什么关联性？

对于新技术，多去**类比**计算机基础和现实世界的事物、事件。

抓住主要矛盾，**学最赚钱的，最能锻炼能力**的技术。

理论和实际结合，脱离实际的理论没有任何价值，要相辅相成。

## 3、确认边界

如果研究问题，需要确认问题边界。

如果做需求，需要确认需求边界。

如果写一道算法题，需要先处理算法的输入边界。

做一件事情，要确认要做的事情的边界。

## 4、不要完美主义

人性的弱点之一就是，经常会陷入完美主义的陷阱。

比如制定一个目标，没有达到，可能从心理上，是一种刺激。

但其实，**目标**是需要经常调整的，达不到，不要放弃，要不断调整，比如目标顺延，目标取消，目标合并，目标修改的更具体。

成功没有固定的模式，如果有，就是在不断的变化、纠正去往成功路线，去往终点，需要不断试错。

**技术选型**中，合格的架构师需要做到的是能够tradeoff，在各种策略中找到一个平衡。找平衡的过程就是一个不断纠正姿态的过程。

没有哪一个方案一定是好的、对的，这个方案只能在一定的上下文中发挥他的作用。

所以要针对不同的上下文环境，做出不同的反应，使用不同的方案。

也可以联想到架构的三原则之一，演进（其他两个是简单、合适）原则，架构不是一蹴而就，无中生有，是不断演进的。

# 二、学习内容

## [Java知识体系思维导图](https://www.processon.com/mindmap/6321d7011e085373dc7a5ef2)

围绕Java
## Java集合、算法、排序、查找、字符串匹配（数据结构和算法）
- [leetcode top 101](https://uploadfiles.nowcoder.com/bm/top101.html)
- [尚硅谷Java数据结构和算法](https://www.bilibili.com/video/BV1E4411H73v/?vd_source=d4842a1fb1b7f14826addcf047c30414)
## Java IO 、操作系统IO（操作系统）
- [零拷贝原理](https://juejin.cn/post/7043948967729561607)
## Java高性能网络编程、计算机网络、Netty等
- [尚硅谷Nginx](https://www.bilibili.com/video/BV1yS4y1N76R/?spm_id_from=333.999.0.0&vd_source=d4842a1fb1b7f14826addcf047c30414)
- Netty
  - [sofa-bolt](https://www.sofastack.tech/projects/sofa-bolt/overview/)
## Java多线程编程
- [多线程50问](https://juejin.cn/post/7134480865089814565)
## 关系型数据库
- [21个MySQL表设计的经验准则](https://juejin.cn/post/7147135702604447758)
- [MySQL13连问](https://mp.weixin.qq.com/s?__biz=MzkzNTEwOTAxMA==&mid=2247484479&idx=1&sn=97358231f0f7086f0056fc5bb4e8afff&chksm=c2b24cc2f5c5c5d4935a4a0c0c8adb912a08e3aa7d7ac06f62dad5826e4093b732e4e3ff73b4&token=1786594806&lang=zh_CN&scene=21#wechat_redirect)
## Java技术栈
- JVM
  - [JVM调优](https://mp.weixin.qq.com/s/RWVV80vLYmQKRmObIcHPTg)
- [Java全栈技术](https://pdai.tech/)
- [陌溪的学习笔记](http://note.moguit.cn/#/)
- [Java技术驿站](https://www.cmsblogs.com/)
- [芋道源码](https://www.iocoder.cn/)
- [spring-boot-bulking](https://github.com/aalansehaiyang/spring-boot-bulking)
- [spring-boot](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=Mzg2NzYyNjQzNg==&action=getalbum&album_id=1874600102896467974#wechat_redirect)
- Mybatis
## 微服务技术栈
- [RuoYi-Cloud](https://github.com/yangzongzhuan/RuoYi-Cloud)([国内站点](https://gitee.com/y_project/RuoYi-Cloud))
- Spring Cloud Gateway
- Ribbon负载均衡
- Open Feign生命式HTTP调用客户端
- Sentinel熔断、限流、降级
- Nacos注册中心/配置中心
- [Spring Cloud进阶](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzU3MDAzNDg1MA==&action=getalbum&album_id=2042874937312346114&scene=173&from_msgid=2247517680&from_itemidx=1&count=3&nolastread=1#wechat_redirect)
## 分布式架构技术
- [左耳听风，分布式系统技术栈](https://time.geekbang.org/column/article/1512)
- [软件架构设计](https://weread.qq.com/web/bookDetail/ac4325c071848780ac4f8d8)
- [sofastack](https://www.sofastack.tech/projects/)
- [Spring Cloud Alibaba]()
- 分布式缓存
  - [数据库缓存一致性讨论](https://juejin.cn/post/7030591648421806110)
- 分布式消息队列
  - [尚硅谷Kafka3.x](https://www.bilibili.com/video/BV1vr4y1677k/?p=18&spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=d4842a1fb1b7f14826addcf047c30414)
- 分布式全文搜索引擎
  - [尚硅谷Elasticsearch7.x](https://www.bilibili.com/video/BV1hh411D7sb/?spm_id_from=333.999.0.0&vd_source=d4842a1fb1b7f14826addcf047c30414)
- [分布式锁](https://juejin.cn/post/7084023049942466574)
- 分布式任务调度
- RPC
  - Dubbo
  - gRPC
- 分布式协调服务Zookeeper
- 分布式数据一致性协议
  - paxos
  - zab
  - raft
    - [sofa-jraft](https://www.sofastack.tech/projects/sofa-jraft/overview/)
- Seata分布式事务
- 分布式链路跟踪
- 其他
  - 租约机制（防止脑裂，死锁、长时间系统占用、错误异常情况）
    - 超时机制
    - 重试机制
  - 分片机制
    - 哈希
    - 一致性哈希
  - 副本机制
    - 数据服务冗余（有状态服务）
    - 业务/计算服务冗余（无状态服务）
    - 主从副本选举
  - 主从复制
  - 主从架构
  - 请求转发，重定向
  - Write Ahead基于内存的顺序写


## 方案设计
- [架构师之路](https://www.w3cschool.cn/architectroad/)
- [电商技术](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=Mzg2NzYyNjQzNg==&action=getalbum&album_id=1874603714678751240#wechat_redirect)
- [架构设计](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=Mzg2NzYyNjQzNg==&action=getalbum&album_id=1874615391855968264&scene=173&from_msgid=2247484799&from_itemidx=1&count=3&nolastread=1#wechat_redirect)
- [架构设计](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzIxMDAwMDAxMw==&action=getalbum&album_id=1760198867930660865&scene=173&from_msgid=2650731378&from_itemidx=1&count=3&nolastread=1#wechat_redirect)
- [聊聊幂等设计](https://mp.weixin.qq.com/s/SDTabW5nl31r2lFCJ9_Dlw)
- [左耳听风，幂等设计](https://time.geekbang.org/column/article/4050)
- 设计原则、设计模式
  
## 大数据技术
- Flink
  - [尚硅谷大数据之Flink实时数仓3.0](https://www.bilibili.com/video/BV1TG411a7nL/?spm_id_from=333.999.0.0&vd_source=d4842a1fb1b7f14826addcf047c30414)
  - [尚硅谷Flink1.13](https://www.bilibili.com/video/BV133411s7Sa/?spm_id_from=333.999.0.0&vd_source=d4842a1fb1b7f14826addcf047c30414)
- HBase
- Clickhouse
- Pulsar
- Vector

## 面试
- [我想进大厂](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=Mzg2NzYyNjQzNg==&action=getalbum&album_id=1911852085562703875&scene=126#wechat_redirect)
- [大厂面试重点](https://mp.weixin.qq.com/s/AFoxufhKBkL6S5pgWE2ISQ)
- [重点知识点串讲‼️](https://lagou.feishu.cn/base/bascnjvTR7K2iVIKZ0FG0JuVcZc?table=tblNgqOOasDAvNM5&view=vew8bMFTac)
- [32个Java面试必考点](https://kaiwu.lagou.com/course/courseInfo.htm?courseId=1#/detail/pc?id=3)
- [架构设计面试](https://kaiwu.lagou.com/course/courseInfo.htm?courseId=592#/content)
- [对线面试官](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzU4NzA3MTc5Mg==&action=getalbum&album_id=1657204970858872832&scene=173&from_msgid=2247484705&from_itemidx=1&count=3&nolastread=1#wechat_redirect)
- [面经](https://mp.weixin.qq.com/s/rQhS49RKvDkWc5wrz23kTw)
- [消息队列10连问](https://juejin.cn/post/7067322260511522823)
- [腾讯云后端15连问](https://juejin.cn/post/7075132492168036388)
- [小厂后端10连问](https://juejin.cn/post/7079569282887057439)
- [oppo后端16连问](https://juejin.cn/post/7087729302103392264)
- [Java面试题汇总](https://mp.weixin.qq.com/s/SARLx_J5oK6nYbby5YBxAg)

## 业务架构设计
- DDD领域驱动设计

## 技术管理

## 其他
  - 系统监控
  - 自动化测试
  - CI/CD，自动化构建、打包、部署

# 谁在招聘
  - https://github.com/ruanyf/weekly/issues/2666


