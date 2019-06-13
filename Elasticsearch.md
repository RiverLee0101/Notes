# 1. Elasticsearch 简介

## 1.1 Elasticsearch是什么？

- **Elasticsearch** 是一个基于**Apache Lucene** 的开源分布式全文检索和分析引擎。可以近实时的**储存**，**搜索**和**分析**海量数据，为需要复杂搜索功能的应用程序提供底层的引擎和技术。

## 1.2 基本概念

- Node：每一个es实例为一个节点，节点类型包括主节点，数据节点，协调节点。从集群内部来说，集群是有主节点，主节点通过选举产生，从集群外部来说es是去中心化，没中心节点，外部与集群所有节点通信都是等价的。
- Cluster
- Document
- Field
- Type
- Index
- Shard
- Replica
- Mapping
- Tokenizer
- Token Filters
- Analyzer
- Term

## 1.3 使用场景

- 假如你有一个网上商店需要给你的用户提供商品搜索，你可以使用es来储存你的商品信息，然后提供搜素、建议功能。
- 你要收集日志或事物数据，并且你想分析和挖掘此数据以查找趋势，统计信息，摘要或异常。在这种情况下，你可以使用**Logstash**来收集，聚合和解析数据，然后将数据提供给Elasticsearch。一旦数据在ES中，你可以运行搜索和聚合来挖掘你感兴趣的任何信息。
- 你有希望**快速调查、分析、可视化**和**询问大量数据**的特殊问题（数百万或数十亿条记录）。在这种情况下，你可以使用ES储存数据，然后使用 **Kibana** 构建自定义仪表板，以便可视化对你重要的数据的方面。此外，你可以使用**ES聚合功能**对你的数据执行复杂的智能查询。

## 1.4 Elastic Stack(ELK)

- Elasticsearch, Logstash, Kibana 三者取首字母简称ELK，在es5.0后加上改名为Elastic Stack，并添加了新成员beats。
- **Logstash** 是动态数据收集管道，拥有可扩展的插件生态系统，能够与Elasticsearch产生强大的协同作用。
- **Kibana** 能够给以图表的形式呈现数据，并且具有可扩展的用户界面。
- **Beats** 是轻量型采集器的平台，从数据来源服务器向Logstash和Elasticsearch发送数据。



# 2. 安装elasticsearch和插件

## 2.1 安装elasticsearch

- 首先电脑需安装 java7 update 55 及以上

- 通过wget下载并解压（下载的文件位于：C:\Users\11101453）：

  ```
  wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.1.1/elasticsearch-2.1.1.tar.gz && tar -xzvf elasticsearch-2.1.1.tar.gz
  ```

- 将解压后的elasticsearch-2.1.1文件夹移至：D:\Program Files\elasticsearch-2.1.1

- 启动：**D:\Program Files\elasticsearch-2.1.1\bin>elasticsearch**

- 在浏览器中打开：localhost:9200 出现以下界面：

  ```json
  {
    "name" : "Tantra",
    "cluster_name" : "elasticsearch",
    "version" : {
      "number" : "2.1.1",
      "build_hash" : "40e2c53a6b6c2972b3d13846e450e66f4375bd71",
      "build_timestamp" : "2015-12-15T13:05:55Z",
      "build_snapshot" : false,
      "lucene_version" : "5.3.1"
    },
    "tagline" : "You Know, for Search"
  }
  ```

## 2.2 安装elasticsearch-head插件

- 通过plugin安装：D:\Program Files\elasticsearch-2.1.1\bin>plugin install mobz/elasticsearch-head

  > 如果出现错误提示：ERROR: failed to download out of all possible locations..., use --verbose to get
  >  detailed information，即换下面的zip安装方式

- zip包安装：

  - https://github.com/mobz/elasticsearch-head下载zip 解压

  - 建立elasticsearch-2.1.1\plugins\head文件

  - 将解压后的elasticsearch-head-master文件夹下的文件copy到head

  - 运行es：D:\Program Files\elasticsearch-2.1.1\bin>elasticsearch

  - 浏览器打开：http://localhost:9200/_plugin/head/

    ![1560413442895](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1560413442895.png)



# 3. ES的CURD

## 3.1 新增数据

- 向my_index索引库的my_type写入id为1的数据，如果my_index，my_type不存在，会默认创建，写入的数据为json格式：

  ```json
  curl -XPUT "localhost:9200/my_index/my_type/1" -d
  "{
  	"name":"jack",
  	"age":16,
  	"sex":false
  }"
  ```

  ```json
  http://localhost:9200/my_index/my_type/1/
  										PUT
  {
  	"name":"jack",
  	"age":16,
  	"sex":false
  }
  ```

## 3.2 查询数据

- 查询 name 为 jack 的数据：

  - 参数通过 **REST request URI** 方式

  ```json
  curl "http://localhost:9200/my_index/_search?q=name:jack"
  ```

  ```JSON
  http://localhost:9200/my_index/
  _search?q=name:jack			GET
  {}
  ```

  - 参数通过 **REST request body** 方式

  ```json
  curl -XPOST "http:localhost:9200/my_index/_search" -d
  "{
  	"query":{"term":{"name":"jack"}}
  }"
  ```

  ```json
  http://localhost:9200/my_index/
  _search						POST
  {
  	"query":{
  		"term":{
  			"name":"jack"
  		}
  	}
  }
  ```

## 3.3 更新数据

### 3.3.1 更新字段

- 更新部分字段，例如将 _id=1 的数据的 name 改为 jhon

  ```json
  curl -XPOST "http://localhost:9200/my_index/my_type/1/_update" -d
  "{
  	"doc":{"name":"jack"}
  }"
  ```

  ```json
  http://localhost:9200/my_index/my_type/1/_update/
  											POST
  {
  	"doc":{
  		"name":"jack"
  	}
  }
  ```

### 3.3.2 脚本更新

> 注意：无论是从性能还是安全方面考虑，能不用脚本尽量不用脚本。
>
> 无论是覆盖写入，还是更新操作（哪怕更新一个字段），es底层Lucene是先删除整条旧数据，再添加索引整条新数据，所以更新操作对es来说开销很大，es不太适合更新频率很大的应用场景。

### 3.3.3 Upserts

- 更新插入操作，id为1的文档如果已经存在，将执行script做更新操作，如果不存在将把upset 元素作为新文档做插入操作。

  ```json
  curl -XPOST "http://localhost:9200/my_index/my_type/1/_update" -d
  "{
  	"script":{
  		"inline":"ctx._source.age += count",
  		"params":{
  			"count":4
  		}
  	},
  	"upsert":{
  		"age":1,
  		"name":"jack"
  	}
  }"
  ```

  设置doc_as_upsert为true，不用指定upsert值，使用doc作为upsert值：

  ```json
  curl -XPOST "http://localhost:9200/my_index/my_type/1/_update" -d
  "{
  	"doc":{
  		"name":"jack"
  	},
  	"doc_as_upsert":true
  }"
  ```

## 3.4 获取数据

- 直接通过GET访问 index+type+唯一主键_id即可得到数据

  ```json
  curl http://localhost:9200/my_index/my_type/1
  ```

  ```JSON
  http://localhost:9200/my_index/my_type/1/
  										GET
  {}
  ```

## 3.5 删除数据

- 将请求方法换为DELETE即可

  ```
  curl -XDELETE "http://localhost:9200/my_index/my_type/1"
  ```

## 3.6 批量操作

- 批量操作支持批量执行index，create，delete，update操作，index和create操作必须下一行为source数据源，delete操作不需要source数据源，update需要在下一行指定部分文档，upsert和script及其选项

- 将所有命令放在command文本文件中：

  ```txt
  {"index":{"_index":"test","_type":"type1","_id:"1"}}
  {"field1":"value1"}
  {"create":{"_index":"test","_type":"type1","_id":"2"}}
  {"field1":"value2"}
  {"create":{"_index":"test","_type":"type1","_id":"3"}}
  {"field1":"value3"}
  {"delete":{"_index":"test","_type":"type1","_id":"3"}}
  {"update":{"_index":"test","_type":"type1","_id":"1"}}
  {"doc":{"field1":"value10","field2":"value2"}}
  
  curl -s -XPOST "http://localhost:9200/_bulk" --data-binary "@command"; echo
  ```

  

