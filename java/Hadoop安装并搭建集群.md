# Hadoop安装并搭建集群

#### 环境

> jdk1.7, cenos6.7, hadoop2.6.1

先确认是否已安装java

```shell
# 出现版本提示信息则代表安装，否则需要先安装java
java -version
```



#### 安装

- 下载Hadoop

- 将压缩包放入虚拟机中的`/root`目录，或者自己选择

- 创建目录并解压文件

  ```shell
  # 创建目录
  mkdir /root/hadoop
  # 解压
  tar -zxvf hadoop-2.6.1.tar.gz
  ```

- 