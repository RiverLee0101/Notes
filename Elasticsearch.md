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

## 1.5 ES和MySQL的比较

|         Elasticsearch         |         MySQL         |
| :---------------------------: | :-------------------: |
|         Index（索引）         |  Database（数据库）   |
|         Type（类型）          |      Table（表）      |
|       Document（文档）        |       Row（行）       |
|         Field（字段）         |     Column（列）      |
|        Mapping（映射）        |    Schema（方案）     |
| Everything indexed by default |     Index（索引）     |
|   Query DSL（查询专用语言）   | SQL（结构化查询语言） |



# 2. 安装elasticsearch和插件

## 2.1 安装elasticsearch(2.1.1)

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

## 2.2 安装es-head插件(2.1.1)

- 通过plugin安装：D:\Program Files\elasticsearch-2.1.1\bin>plugin install mobz/elasticsearch-head

  > 如果出现错误提示：ERROR: failed to download out of all possible locations..., use --verbose to get
  >  detailed information，即换下面的zip安装方式

- zip包安装：

  - https://github.com/mobz/elasticsearch-head下载zip 解压

  - 建立elasticsearch-2.1.1\plugins\head文件夹

  - 将解压后的elasticsearch-head-master文件夹下的文件copy到head

  - 运行es：D:\Program Files\elasticsearch-2.1.1\bin>elasticsearch

  - 浏览器打开：http://localhost:9200/_plugin/head/

    ![es-1.png](https://github.com/RiverLee0101/Notes/blob/master/images/es-1.png?raw=true)

## 2.3 安装elasticsearch(5.6.5)

- 下载elasticsearch 5.6.5：<https://www.elastic.co/cn/downloads/past-releases/elasticsearch-5-6-5>

- 解压至：D:\Program Files\elasticsearch-5.6.5

- 启动：**D:\Program Files\elasticsearch-5.6.5\bin>elasticsearch**

- 在浏览器中打开：localhost:9200 出现以下界面：

  ```json
  {
    "name" : "HRqnul0",
    "cluster_name" : "elasticsearch",
    "cluster_uuid" : "f06S9157ROSQzm51OQq3gg",
    "version" : {
      "number" : "5.6.5",
      "build_hash" : "6a37571",
      "build_date" : "2017-12-04T07:50:10.466Z",
      "build_snapshot" : false,
      "lucene_version" : "6.6.1"
    },
    "tagline" : "You Know, for Search"
  }
  ```

## 2.4 安装es-head插件(5.6.5)

> 注：es5以上版本安装 es-head 需要安装 node 和 grunt

- 安装node：**https://nodejs.org/en/download/**，双击安装

- 命令行进入：`cd C:\Program Files\nodejs`，`node -v`查看版本

- 安装grunt：`npm install -g grunt-cli`，重新打开CMD，输入 `grunt -version` 出现版本号则安装成功

- 进入：D:\Program Files\elasticsearch-5.6.5/config，打开elasticsearch.yml文件，在末尾添加：

  ```
  http.cors.enabled: true 
  http.cors.allow-origin: "*"
  node.master: true
  node.data: true
  ```

- 然后去掉 network.host: 192.168.0.1的注释并改为network.host: 0.0.0.0，再去掉cluster.name；node.name；http.port 的注释

- 下载head：https://github.com/mobz/elasticsearch-head

- 解压head得到 elasticsearch-head-master文件夹，把解压后的文件夹放至：D:\Program Files\elasticsearch-5.6.5\elasticsearch-head-master

- 进入该文件夹，修改 Gruntfile.js，在connect-server-options 加上hostname:'*'

  ![img](https://images2018.cnblogs.com/blog/986140/201802/986140-20180227095130174-1314908435.png)

- 进入：cd D:\Program Files\elasticsearch-5.6.5\elasticsearch-head-master，在此文件夹下执行：`npm install`

- 然后执行：`grunt server` 运行head插件，成功如下（不成功重新安装grunt）：

  ![1560504831307](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1560504831307.png)

- 浏览器访问：localhost:9100，成功如下：

  ![1560504936220](C:\Users\11101453\AppData\Roaming\Typora\typora-user-images\1560504936220.png)

  > - 浏览器中的：localhost：9100 为head的端口
  > - 下面的：http://localhost:9200/ 为es服务端口

## 2.5 启动es程序和head插件

- 调出CMD
- 进入es并运行：cd D:\Program Files\elasticsearch-5.6.5\bin>elasticsearch
- 进入head运行：cd D:\Program Files\elasticsearch-5.6.5\elasticsearch-head-master>grunt server
- 浏览器中输入：localhost:9100 打开head管理界面



# 3. Elasticsearch的CURD

## 3.1 新增数据

### 3.1.1 插入一个文档

- 向my_index索引库的my_type写入id为1的文档，如果my_index，my_type不存在，会默认创建，写入的数据为json格式：

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
  

### 3.1.2 从文件插入文档

- 将包含json数据的文件：walking.json 放在某个易找到的文件夹中

- 进入上面的文件夹，执行：

  ```
  curl -XPUT "http://localhost:9200/music/lyrics/1" -d @walking.json
  ```

  意思就是将 walking.json 写入索引 music 的 lyrics 类型中，并为该文档分配id=1

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



# 4. Document APIs

- <https://juejin.im/post/5b3ac6db6fb9a024fc284e60#heading-25>

## 4.1 注意事项

- 使用 Elasticsearch 的 java API，经验证，需满足以下要求：

  - JDK版本：1.8
  - Elasticsearch 版本：5.6.5
  - transport 版本：5.6.5

- 需引入的maven依赖：

  ```xml
  <dependency>
     <groupId>org.elasticsearch</groupId>
     <artifactId>elasticsearch</artifactId>
     <version>5.6.5</version>
  </dependency>
  <dependency>
     <groupId>org.elasticsearch.client</groupId>
     <artifactId>transport</artifactId>
     <version>5.6.5</version>
  </dependency>
  
  <!--spring整合es-->
  <dependency>
     <groupId>org.springframework.data</groupId>
     <artifactId>spring-data-elasticsearch</artifactId>
     <version>2.0.4.RELEASE</version>
  </dependency>
  ```

  

## 4.2 Index API

### 4.2.1 简介

- Index API 允许我们储存一个 json 格式的文档，使得数据可以被搜索到。文档通过 **index、type、id** 唯一确定。id 可以自己提供一个ID，也可以使用 Index API为我们生成一个。
- 有四种不同的方式来**产生json格式的文档**（document）：
  - 手动方式，使用原生的 byte[] 或者 String
  - 使用Map方式，会自动转换成与之等价的json
  - 使用第三方库来生成序列化 beans，如 JackJSON、FastJSON 等
  - 使用内置的帮助类 XContentFactory.jsonBuilder()

### 4.2.2 相关代码

```java
package com.ssm.daoTest;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.elasticsearch.action.index.IndexResponse;
import org.elasticsearch.client.transport.TransportClient;
import org.elasticsearch.common.settings.Settings;
import org.elasticsearch.common.transport.InetSocketTransportAddress;
import org.elasticsearch.common.xcontent.XContentBuilder;
import org.elasticsearch.common.xcontent.XContentFactory;
import org.elasticsearch.transport.client.PreBuiltTransportClient;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

import java.io.IOException;
import java.io.Serializable;
import java.net.InetAddress;
import java.net.UnknownHostException;
import java.util.HashMap;
import java.util.Map;

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration({"classpath:spring-mybatis.xml","classpath:spring-mvc.xml"})
public class ElasticsearchIndexAPITest {

    private TransportClient client=null;
    public static final String INDEX = "fendo";
    public static final String TYPE = "fendodate";
    @SuppressWarnings("unchecked")
    @Before
    public void getClient() throws Exception{
        //  1.设置连接的集群名称
        Settings settings = Settings.builder().put("cluster.name","my-application").build();
        //  2.连接集群
        client = new PreBuiltTransportClient(settings);
        client.addTransportAddress(new InetSocketTransportAddress(InetAddress.getByName("localhost"),9300));
        //  3.打印集群名称
        System.out.println(client.toString());
    }

    /*
    * 1.手动方式
    */
    @Test
    public void JsonDocument() throws UnknownHostException {
        String json = "{"+
                "\"user\":\"deepredapple\"," +
                "\"postDate\":\"2018-01-30\"," +
                "\"message\":\"trying out Elasticsearch\"" +
                "}";
        IndexResponse indexResponse = client.prepareIndex("fendo","fendodate").setSource(json).get();
        System.out.println(indexResponse.getResult());
    }
    /*
    * 2.Map 方式
    */
    @Test
    public void MapDocument(){
        Map<String, Object> json = new HashMap<String, Object>();
        json.put("user","jack");
        json.put("postDate", "2018-06-28");
        json.put("message", "trying out Elasticsearch");
        IndexResponse indexResponse = client.prepareIndex("fendo","fendodate").setSource(json).get();
        System.out.println(indexResponse.getResult());
    }
    /*
    * 3.序列化方式
    */
    @Test
    public void JACKSONDocument() throws JsonProcessingException {
        Blog blog = new Blog();
        blog.setUser("John");
        blog.setPostDate("2018-06-29");
        blog.setMessage("try out ElasticSearch");
        ObjectMapper mapper = new ObjectMapper();
        byte[] bytes = mapper.writeValueAsBytes(blog);
        IndexResponse response = client.prepareIndex("fendo","fendodate").setSource(bytes).get();
        System.out.println(response.getResult());
    }
    public class Blog implements Serializable {
        String user;
        String postDate;
        String message;
        public void setUser(String user){
            this.user = user;
        }
        public void setPostDate(String postDate){
            this.postDate = postDate;
        }
        public void setMessage(String message){
            this.message = message;
        }
        public String getUser(){return user;}
        public String getPostDate(){return postDate;}
        public String getMessage(){return message;}
    }
    /*
    * 4.XContentBuilder帮助类方式
    */
    @Test
    public void XContentBuilderDocument() throws IOException{
        XContentBuilder builder = XContentFactory.jsonBuilder().startObject()
                .field("user", "xcontentdocument")
                .field("postDate", "2018-06-30")
                .field("message", "this is ElasticSearch").endObject();
        IndexResponse response = client.prepareIndex(INDEX, TYPE).setSource(builder).get();
        System.out.println(response.getResult());
    }
}

```



## 4.3 Get API

- get API 可以通过id查看文档

- 代码：

  ```java
  @Test
      public void testGetApi(){
          // setOperationThreaded设置为true是在不同的线程里执行此操作
          GetResponse getResponse = client.prepareGet(INDEX, TYPE, "AWtWCcuelpooUlTSGlyc").setOperationThreaded(false).get();
          Map<String, Object> map = getResponse.getSource();
          Set<String> keySet = map.keySet();
          for(String key : keySet){
              Object o = map.get(key);
              System.out.println(o.toString());
          }
      }
  ```



## 4.4 Delete API

- 根据id删除

- 代码：

  ```java
  @Test
      public void testDeleteApi(){
          GetResponse getResponse = client.prepareGet(INDEX, TYPE, "AWtWCcuelpooUlTSGlyc").setOperationThreaded(false).get();
          System.out.println(getResponse.getSource());
          DeleteResponse deleteResponse = client.prepareDelete(INDEX, TYPE, "AWtWCcuelpooUlTSGlyc").get();
          System.out.println(deleteResponse.getResult());
      }
  ```



## 4.5 Delete By Query API

- 通过查询条件删除

- 代码：

  ```java
   @Test
      public void deleteByQuery(){
          BulkByScrollResponse response = DeleteByQueryAction.INSTANCE.newRequestBuilder(client)
                  .filter(QueryBuilders.matchQuery("user", "jack"))
                  .source(INDEX).get();
          long deleted = response.getDeleted(); // 删除文档数量
          System.out.println(deleted);
      }
  ```

  > 参数说明 QueryBuilders.matchQuery("user", "hhh") 的参数为字段和查询条件，source(INDEX)参数为索引名。



## 4.6 异步回调

- 当执行的删除的时间过长时，可以使用异步回调的方式执行删除操作，执行的结果在回调里面获取

- 代码：

  ```java
  @Test
      public void deleteByQueryAsync(){
          for(int i=1300;i<3000;i++){
              DeleteByQueryAction.INSTANCE.newRequestBuilder(client)
                      .filter(QueryBuilders.matchQuery("user", "hhh " + i))
                      .source(INDEX)
                      .execute(new ActionListener<BulkByScrollResponse>() {
                          @Override
                          public void onResponse(BulkByScrollResponse response) {
                              long deleted = response.getDeleted();
                              System.out.println("删除的文档数量为="+deleted);
                          }
  
                          @Override
                          public void onFailure(Exception e) {
                              System.out.println("Failure");
                          }
                      });
          }
  
      }
  ```
  - 当程序停止时，在ElasticSearch的控制台依旧在执行删除操作，异步的执行操作。



## 4.7 Update API

- 更新文档
- 主要有两种方法进行更新操作：
  - 创建UpdateRequest，通过client发送
  - 使用prepareUpdate()方法

### 4.7.1 使用UpdateRequest

```java
@Test
    public void testUpdateApi() throws IOException, ExecutionException, InterruptedException{
        UpdateRequest updateRequest = new UpdateRequest();
        updateRequest.index(INDEX);
        updateRequest.type(TYPE);
        updateRequest.id("AWtVzvtT8K4paE07nMyu");
        updateRequest.doc(jsonBuilder().startObject().field("user","Jack Huang").endObject());
        client.update(updateRequest).get();
    }
```

### 4.7.2 使用prepareUpdate()

```java
@Test
    public void testUpdatePrepareUpdate() throws IOException {
        //client.prepareUpdate(INDEX, TYPE, "AWtVzvtT8K4paE07nMyu").setScript(new Script("ctx._source.user = \"DeepRedApple\"")).get();
        client.prepareUpdate(INDEX, TYPE, "AWtVzvtT8K4paE07nMyu").setDoc(jsonBuilder().startObject().field("user", "DeepRedApple update").endObject()).get();
    }
```

### 4.7.3 Update By Script

- 使用脚本更新文档，直接执行脚本里面的数据执行更新操作

```java
@Test
    public void testUpdateByScript() throws ExecutionException, InterruptedException {
        UpdateRequest updateRequest = new UpdateRequest(INDEX, TYPE, "AWRFvLSTro3r8sDxIpia")
                .script(new Script("ctx._source.user = \"LZH\""));
        client.update(updateRequest).get();
    }
```

### 4.7.4 Upsert

- 更新文档，如果存在文档就更新，不存在就插入

```java
@Test
    public void testUpsert() throws IOException,ExecutionException,InterruptedException{
        IndexRequest indexRequest = new IndexRequest(INDEX, TYPE, "AWtVzvtT8K4paE07nMyu")
                .source(jsonBuilder()
                        .startObject()
                        .field("user", "hhh")
                        .field("postDate", "2018-02-14")
                        .field("message", "ElasticSearch")
                        .endObject());
        UpdateRequest updateRequest = new UpdateRequest(INDEX, TYPE, "AWtVzvtT8K4paE07nMyu")
                .doc(jsonBuilder()
                        .startObject()
                        .field("user", "LZH")
                        .endObject())
                .upsert(indexRequest); //如果不存在，就增加indexRequest
        client.update(updateRequest).get();
    }
```



## 4.8 Multi Get API

- 通过id一次获取多个文档

- 代码：

```java
@Test
    public void testMultiGetApi(){
        MultiGetResponse responses = client.prepareMultiGet()
                .add(INDEX, TYPE, "AWtVzvtT8K4paE07nMyu")
                .add(INDEX, TYPE, "AWtZ8o3gb2ILFvpwEaj6","AWtVJr9zTE5BzRZT3zd9")
                .add("blog","blog","AWtZ9T9qb2ILFvpwEaj7")
                .get();
        for(MultiGetItemResponse itemResponse : responses){
            GetResponse response = itemResponse.getResponse();
            if(response.isExists()){
                String source = response.getSourceAsString();
                JSONObject jsonObject = JSONObject.fromObject(source);
                Set<String> sets = jsonObject.keySet();
                for(String str : sets){
                    System.out.println("key -> " + str);
                    System.out.println("value -> "+jsonObject.get(str));
                    System.out.println("===============");
                }

            }
        }
    }
```



## 4.9 Bulk API

- Bulk API 可以实现批量插入
- 代码：

```java
@Test
    public void testBulkApi() throws IOException{
        BulkRequestBuilder requestBuilder = client.prepareBulk();
        requestBuilder.add(client.prepareIndex(INDEX, TYPE, "1")
                .setSource(jsonBuilder()
                        .startObject()
                        .field("user", "张三")
                        .field("postDate", "2018-05-01")
                        .field("message", "zhangSan message")
                        .endObject()
                )
        );
        requestBuilder.add(client.prepareIndex(INDEX, TYPE, "2")
                .setSource(jsonBuilder()
                        .startObject()
                        .field("user", "李四")
                        .field("postDate", "2016-09-10")
                        .field("message", "Lisi message")
                        .endObject()
                )
        );
        BulkResponse bulkResponse = requestBuilder.get();
        if(bulkResponse.hasFailures()){
            System.out.println("error!");
        }
    }
```



## 4.10 Useing Bulk Processor

- 使用Bulk Processor, Bulk Processor提供了一个简单的接口，在给定的大小的数量上定时批量自动请求



# 5. Search API

- 搜索API可以支持搜索查询，返回查询匹配的结果，它可以搜索一个index/type或者多个index/type，可以使用Query Java API作为查询条件
- Java 默认提供QUERY_AND_FETCH 和 DFS_QUERY_AND_FETCH 两种search Types，但是这两种模式应该由系统选择，而不是用户手动指定
- 示例代码：

```java
@Test
    public void testSearchApi(){
        SearchResponse response = client.prepareSearch(INDEX).setTypes(TYPE).setQuery(QueryBuilders.matchQuery("user","lijiang")).get();
        SearchHit[] hits = response.getHits().getHits();
        for(int i=0; i<hits.length;i++){
            String json = hits[i].getSourceAsString();
            JSONObject object = JSONObject.fromObject(json);
            Set<String> strings = object.keySet();
            for(String str : strings){
                System.out.println(object.get(str));
            }
        }
    }
```



## 5.1 Using scrolls in Java

- 一般的搜索请求都是返回一页的数据，无论多大的数据量都会返回给用户，Scrolls API可以允许我们检索大量的数据（甚至是全部数据）。Scroll API允许我们做一个初始阶段搜索页并且持续批量从ElasticSearch里面拉取结果直到结果没有剩下。Scroll API的创建并不是为了实时的用户响应，而是为了处理大量的数据。

