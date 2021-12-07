# elasticsearch

## 文档
官网 : [https://www.elastic.co/cn/elasticsearch/](https://www.elastic.co/cn/elasticsearch/)


## open jdk
网站 [https://openjdk.java.net/](https://openjdk.java.net/)

安装

```
wget https://download.java.net/java/GA/jdk17.0.1/2a2082e5a09d4267845be086888add4f/12/GPL/openjdk-17.0.1_linux-x64_bin.tar.gz

tar -zvxf openjdk-17.0.1_linux-x64_bin.tar.gz 

sudo  mv jdk-17.0.1 /usr/lib/jvm/

sudo vim /etc/profile

export JAVA_HOME=/usr/lib/jvm/  ## 这里要注意目录要换成自己解压的jdk 目录
export JRE_HOME=${JAVA_HOME}/jre  
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
export PATH=${JAVA_HOME}/bin:$PATH
source /etc/profile

```

查看当前版本

```
java --version
```

## elasticsearch

### 安装

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.15.2-linux-x86_64.tar.gz

tar -zvxf elasticsearch-7.15.2-linux-x86_64.tar.gz 

```

### 运行

```
cd elasticsearch-7.15.2/

./bin/elasticsearch
```

### 设置外网访问

```
vim  elasticsearch.yml 

修改为 => network.host: 0.0.0.0
```

启动加参数,单节点启动

 ```
  ./bin/elasticsearch -E "discovery.type=single-node"
 ```



## 图形化界面  kibana

### 下载页面
[https://www.elastic.co/cn/downloads/kibana](https://www.elastic.co/cn/downloads/kibana)

### 安装

```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.15.2-linux-x86_64.tar.gz

tar -zvxf kibana-7.15.2-linux-x86_64.tar.gz 
```

### 设置外网访问

```
vim config/kibana.yml 

修改为 => server.host: "0.0.0.0"
```


### 运行

```
./bin/kibana
```

### 工具
[http://115.159.195.129:5601/app/dev_tools#/console](http://115.159.195.129:5601/app/dev_tools#/console)