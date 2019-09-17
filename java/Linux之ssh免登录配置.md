# Linux之ssh免登录配置

#### 用处

在操作集群时避免重复输入密码，方便管理



- 生成公钥、私钥对多台机器需要每个机器都生成一次

```shell
ssh-keygen
```

全部直接回车即可，执行成功后会在`~/.ssh`目录下生成对应的公钥私钥文件

- 将公钥发送给需要免登录的机器，需要免登录的机器都要相互发送公钥

  ```shell
  scp ~/.ssh/id_rsa.pub <用户名>@<ip>:~/
  ```

- 将收到的公钥追加到自己的`~/.ssh/authorized_keys`文件，如果不存在文件则创建即可并修改权限`chmod 600 authorized_keys `

```shell
 cat id_rsa.pub >> ~/.ssh/authorized_keys 
```

