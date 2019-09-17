# Linux 配置zookeeper集群

### 下载安装包

官网的历史版本地址：https://archive.apache.org/dist/zookeeper/  根据需要下载对应的版本，我使用的是3.4.10

### 将压缩包放入服务器

- 解压文件

```shell
tar -zxvf zookeeper-3.4.10.tar.gz
```

- 改名(可有可无，改了方便点)

```shell
mv zookeeper-3.4.10 zookeeper
```

- 修改配置文件

  ```shell
  # 进入conf目录
  cd zookeeper/conf
  # 复制一份配置文件
  cp zoo_sample.cfg zoo.cfg
  # 修改内容
  vi zoo.cfg
  ```

  >dataDir=/root/zookeeper/data # 数据存储路径，需要自己创建
  >
  >dataLogDir=/root/zookeeper/log # 日志存储路径，需要自己创建
  >
  >server.1=dfs01:2888:3888 #(主机名(ip):心跳端口:数据端口),这是三台主机的配置
  >
  >server.2=dfs02:2888:3888
  >
  >server.3=dfs03:2888:3888​                  

  ### ZooKeeper常见配置

  - tickTime:CS通信心跳数；以`毫秒`为单位，可以使用默认配置。

  - initLimit:LF初始通信时限；

  - syncLimit:LF同步通信时限；数值不宜过高。

  - dataDir:数据文件目录；

  - dataLogDir:日志文件目录；

  - clientPort:客户端连接端口；

  - server.N:服务器名称与地址（服务编号，服务地址，LF通信端口，选举端口）

    注意配置主机名时需要确保能够ping对应的主机，同时要在`/etc/hosts`文件中添加对应的主机名映射

  ```shell
  #/etc/hosts
  192.168.229.129 dfs01
  192.168.229.130 dfs02
  192.168.229.131 dfs03
  ```

  ```shell
  #分发给其他主机
  scp /etc/hosts <用户名>@<主机名/ip>:/etc/
  ```

- 在`zookeeper`目录下创建目录

  ```shell
  mkdir data;mkdir log
  ```

- 在`data`目录下添加`myid`文件

  ```shell
  # zookeeper目录下
  vi data/myid
  # 添加内容，内容为在conf/zoo.cfg中配置的主机对应的数字，如A主机为dfs02那么对应的则是2，每台主机需要单独配置
  1
  ```


- 添加至环境变量

  ```shell
  vi /etc/profile
  ```

  ```
  export ZOOKEEPER_HOME=/root/zookeeper/   # 自己的zookeeper路径
  export PATH=$ZOOKEEPER_HOME/bin:$PATH
  ```


- 启动

  ```shell
  zkServer.sh start
  ```

  提示以下信息代表启动成功

  ```
  ZooKeeper JMX enabled by default
  Using config: /root/zookeeper/bin/../conf/zoo.cfg
  Starting zookeeper ... STARTED
  ```

- 查看状态

  ```shell
  zkServer.sh status
  ```

  出现以下信息代表正常

  ```
  ZooKeeper JMX enabled by default
  Using config: /root/zookeeper/bin/../conf/zoo.cfg
  Mode: follower  # leader为领导
  ```

- 查看日志

  ```shell
  zkServer.sh start-foreground #出现短裤端口占用先别急，jps查看是否已经运行，如果已经运行则不用管
  ```
