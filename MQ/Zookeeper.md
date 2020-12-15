## 1. 创建目录

```shell
mkdir -p /usr/local/src/zookeeper
cd /usr/local/src/zookeeper
```

## 2. 下载解压

```shell
wget https://archive.apache.org/dist/zookeeper/zookeeper-3.4.9/zookeeper-3.4.9.tar.gz
tar -zxvf zookeeper-3.4.9.tar.gz
cd zookeeper-3.4.9
mkdir data
mkdir logs
```

## 3. 修改配置文件

```shell
cd conf
cp zoo_sample.cfg zoo.cfg
```

修改zoo.cfg

```shell
# 数据文件夹
dataDir=/usr/local/services/zookeeper/zookeeper-3.4.9/data
# 日志文件夹
dataLogDir=/usr/local/services/zookeeper/zookeeper-3.4.9/logs
```

## 4. 启动ZK

```shell
cd ../bin
./zkServer.sh start
```

## 5. 查看状态

```shell
./zkServer.sh status
```

