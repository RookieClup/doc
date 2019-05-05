# ElasticSearch 环境搭建

## elasticSearch 安装
1，基础环境：jdk1.8

2，es 下载地址:

wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.7.2.tar.gz
```所遇到的坑：
1，内存
由于ES是运行在JVM上，JVM本身除了分配的heap内存以外，还会用到一些堆外(off heap)内存。 在小内存的机器上跑ES，如果heap划分过多，累加上堆外内存后，总的JVM使用内存量可能超过物理内存限制。 如果swap又是关闭的情况下，就会被操作系统oom killer

解决方法： 修改ES中config目录下的jvm.options文件
vim jvm.options 将
 -Xms1g -Xmx1g 改为  -Xms512m -Xmx512m
2，注意：不要在root 目录下下载elastic ,用普通用户启动。
```


若为集群: 进入 ...\elasticsearch-5.6.0\config\elasticsearch.yml
配置如下集群信息：
```
cluster.name: my-application   # 集群名称
path.data: /path/to/data       # ES数据存储路径
path.logs: /path/to/logs       # ES日志存储路径
node.name: node-1              # 当前节点的名称
network.host: 192.168.0.1      # 配置当前结点绑定的IP地址，可设置为0.0.0.0
http.port: 9200                # 设置对外服务的HTTP端口，默认为9200
```

3,运行 ./bin/elasticsearch

访问：http://localhost:9200/?pretty

##ElasticSearch 可视化界面kibana

```
   下载并解压缩 Kibana: wget https://artifacts.elastic.co/downloads/kibana/kibana-6.7.2-linux-x86_64.tar.gz
   在编辑器中打开 config / kibana.yml。
   设置 elasticsearch.url 为您的Elasticsearch实例，如本地：elasticsearch.url: "http://localhost:9200"。
   运行 bin/kibana（或bin\kibana.bat在Windows上）。
   后台启动：nohup bin/kibana -d
   浏览器输入 http://localhost:5601。
   
```

`'注意'：这样其中之后只能本地访问，若要外网能够访问需要改配置文件，开放主机和端口。es:elasticSearch.yaml `
