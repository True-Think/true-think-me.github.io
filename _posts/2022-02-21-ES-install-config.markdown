---
layout:     post
title:      "ES安装与配置"
subtitle:   " \"ES部署过程记录\""
date:       2022-02-21 17:45:00 +0800
author:     "True-Think"
header-img: "img/aurora-2020-02-21.jpg"
catalog: true
tags:
    - 技术
    - ES
    - ElasticSearch
---
> **Elasticsearch**是一个基于[Lucene](https://zh.wikipedia.org/wiki/Lucene)库的[搜索引擎](https://zh.wikipedia.org/wiki/%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E)。它提供了一个分布式、支持多租户的[全文搜索](https://zh.wikipedia.org/wiki/%E5%85%A8%E6%96%87%E6%AA%A2%E7%B4%A2)引擎，具有[HTTP](https://zh.wikipedia.org/wiki/HTTP)?Web接口和无模式[JSON](https://zh.wikipedia.org/wiki/JSON)文档。Elasticsearch是用[Java](https://zh.wikipedia.org/wiki/Java)开发的，并在[Apache许可证](https://zh.wikipedia.org/wiki/Apache%E8%AE%B8%E5%8F%AF%E8%AF%81)下作为开源软件发布。官方客户端在[Java](https://zh.wikipedia.org/wiki/Java)、[.NET](https://zh.wikipedia.org/wiki/.NET%E6%A1%86%E6%9E%B6)（[C#](https://zh.wikipedia.org/wiki/C%E2%99%AF)）、[PHP](https://zh.wikipedia.org/wiki/PHP)、[Python](https://zh.wikipedia.org/wiki/Python)、[Apache Groovy](https://zh.wikipedia.org/wiki/Groovy)、[Ruby](https://zh.wikipedia.org/wiki/Ruby)和许多其他语言中都是可用的。[[5]](https://zh.wikipedia.org/wiki/Elasticsearch#cite_note-offizsite-5)根据DB-Engines的排名显示，Elasticsearch是最受欢迎的企业搜索引擎，其次是[Apache Solr](https://zh.wikipedia.org/wiki/Apache_Solr)，也是基于Lucene。 --- 维基百科

Elasticsearch（以下简称ES）的安装步骤为：

 - 下载安装文件，完成解压；

- 放入安装目录，设置配置文件；

- 后台启动

其他：添加分词插件；用户权限

## 一、下载安装文件，完成解压

下载地址：

官网: https://www.elastic.co/cn/downloads/elasticsearch
或
中文社区：https://elasticsearch.cn/download/

如下载了版本7.3.2。主要关心的文件为
|目录	| 配置文件	| 描述 |
|---            |---                   |---      |
|bin	|–	|放置脚本文件，如启动脚本 elasticsearch, 插件安装脚本等。|
|config	|elasticserch.yml	|elasticsearch 配置文件，如集群配置、jvm 配置等。|
|jdk	|–	|java 运行环境 |
|data	|path.data	|数据持久化文件 |
|lib	|–	|依赖的相关类库 |
|logs	|path.log	|日志文件 |
|modules	|–	|包含的所有 ES 模块 |
|plugins	|–	|包含的所有已安装的插件 |
注：data和logs会占用较大的空间，需要选择足够空间的位置，尽量不要放在安装目录下

## 二、放入安装目录，设置配置文件
安装前确保JDK已安装，并设置JAVA_HOME的环境变量。 (Elasticsearch 7.0 开始，内置了 Java 环境)
> export JAVA_HOME=/usr/local/jdk1.8.0_181
export PATH=\$PATH:$JAVA_HOME/bin

放入安装目录后（如  /usr/local/elasticsearch/），开始编辑配置文件 config/elasticserch.yml  
> cluster.name: elasticsearch \# ES名称
node.name: node-1  \# 节点名称
\# data storage info
path.data: /data/to_path/es_data/data   \# 数据存储位置
path.logs: /data/to_path/es_data/logs \# 数据操作日志
bootstrap.memory_lock: false \#内存锁
discovery.seed_hosts: ["127.0.0.1"] \#  集群主机列表
cluster.initial_master_nodes: ["node-1"]  \# 初始化节点名称
http.port: 9200 \# http 访问接口
transport.tcp.port: 9300 \# tcp通信端口
\#gateway.recover_after_nodes: 3
network.host: 0.0.0.0  # 外部访问设置
\# head插件可访问es并且开启ES跨域
http.cors.enabled: true
http.cors.allow-origin: "*"

## 三、后台启动
进入bin/目录下
启动测试
> ./elasticsearch 

这时候可能会遇到一些问题，可以去[常见问题解答]和[参考]中寻找对应的问题。
然后关闭进程
>  ps -aux | grep elasticsearch
> kill -9 [pid]

后台启动
> ./elasticsearch -d

但可能会出现./elasticsearch正常启动，但./elasticsearch -d 则会报错，改成如下则成功
> ./elasticsearch d

## 四、其他
### 1、分词插件
1）进入 https://github.com/medcl/elasticsearch-analysis-ik/releases 选择**与安装ES版本对应的**ik插件
2）在plugins/下，新建ik/目录，将分词插件解压后放入该目录
### 2、es用户登录启动
> groupadd es  \# 创建组名
useradd es -g es  \# 创建用户并加入组
passwd es  \# 设置用户密码
chown –R es:es /usr/local/elasticsearch  \# es安装文件设置为es用户的权限
su – es  \# 切换es用户

然后后台启动es。
注意：数据和日志要给es读写权限，当然可以让这些文件开最高的读写权限，但劝你最好不要这样做，应用chown命令更改文件所有权。\[chmod 777 file]是对数据很不安全的命令，问题总结可以看看[这篇文章](https://zhuanlan.zhihu.com/p/255000117)。
> chown -R es:es  /data/to_path/es_data/data
chown -R es:es  /data/to_path/es_data/logs

### 3、浏览器插件
**方式一**：添加chrome的ElasticSearch Head插件，
进入后数据 http://xx.xx.xx.xx:9200/ 连接 （xx.xx.xx.xx为安装ES的主机IP）
效果图：
![image.png](https://upload-images.jianshu.io/upload_images/27635537-8b82299b7e444be7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注：firefox插件则可用Elasticvue

**方式二**：安装ElasticSearch Head插件在服务主机上。
具体可以参考[这篇文章](https://blog.csdn.net/wpc2018/article/details/121108389)。
效果图：
![image.png](https://upload-images.jianshu.io/upload_images/27635537-568a09e5071188c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4、常见问题解答
[这里](https://www.cnblogs.com/kelelipeng/p/12290256.html)有一些问题集锦，或许会遇到。

参考：
https://zh.wikipedia.org/wiki/Elasticsearch
https://zhuanlan.zhihu.com/p/255000117
https://blog.csdn.net/qq_45988496/article/details/116380830
https://www.cnblogs.com/kelelipeng/p/12290256.html
https://blog.csdn.net/qq_31674359/article/details/80671749
https://blog.csdn.net/lizz861109/article/details/112532473
https://blog.csdn.net/wpc2018/article/details/121108389