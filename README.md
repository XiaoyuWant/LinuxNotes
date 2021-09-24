# NOTE
---

## ⚪ HPC 基本用法

1. 注册https://nic.csu.edu.cn/info/1144/1766.htm

2. 使用ssh登录节点 `ssh -p 8220 name@hpclogin1.csu.edu.cn`

3. HPC作业系统分为`登录节点`和`运算节点`，所有的文件和环境都可以被两者访问

4. 在登录节点安装环境等，因为一旦进入GPU节点就无法联网

5. 申请使用GPU：这些参数在HPC文档可以找到

    `sbatch your_task.sh` 指申请任务以sh脚本形式

   `-J 任务名` `-o -e 输出文件` `-N 节点` `-n 核心数` `-exclusive独占模式` `-p -q GPU节点类型` `--gres=gpu:2 GPU数目 `

   后面的是你的任务，如`python your_task.py`

    ```shell
    #!/bin/sh
    #SBATCH -J loop
    #SBATCH -o loop.log
    #SBATCH -e loop.err
    #SBATCH -N 1 -n 10 --exclusive -p gpu2Q -q gpuq --gres=gpu:2
    python your_task.py
    wait
    ```

6. 查看 `squeue`     取消`scancel NAME_ID`
7. 申请到GPU之后，进入GPU节点`ssh gpu206` 任务会在后台运行，也可以在这个节点上同时进行其他计算

---

## ⚪ 配置环境

1. 安装 `anadonda3`

2. 新建环境 `envname` 

3. `conda install pytorch torvision cudatoolkit=10.0 -c pytorch` 10.0表示cuda的运行时版本

4. 如果启动时没有conda环境

   ```shell
   export PATH=~/anaconda3/bin/:$PATH
   conda init 
   ```

5. `conda install PKGNAME` 安装一些包

6. 

---

## ⚪ 常用Linux指令

| 命令       | 参数                  |                              |
| ---------- | --------------------- | ---------------------------- |
| `ls` `ll`  |                       | 列出文件名                   |
| `cp `      | `-r`递归              | 复制文件、文件夹             |
| `mkdir`    |                       | 新建文件夹                   |
| `touch`    |                       | 新建文件                     |
| `vim` `vi` |                       | 编辑器                       |
| `scp`      | `-P`目标端口 `-r`递归 | 从本电脑复制文件到另一台电脑 |
|            |                       |                              |

---

## ⚪ SSH工具链连接内外网
**1. [ Holer ]**
```shell
# 在服务器端的配置

# 安装java
apt install openjdk-8-jdk

# 安装tomcat
mkdir tomcat
cd tomcat
wget https://mirror-hk.koddos.net/apache/tomcat/tomcat-8/v8.5.68/bin/apache-tomcat-8.5.68.tar.gz
vim apache-tomcat-8.5.68/bin/startup.sh
在倒数第二行加入
export TOMCAT_HOME=/root/***
启动tomcat
sh apache-tomcat-8.5.68/bin/startup.sh

# 安装holer
mkdir holer
wget https://github.91chifun.workers.dev/https://github.com//wisdom-projects/holer-client/releases/download/1.2/holer-linux-x86.tar.gz
tar -zxvf **
启动
sh startup.sh
第一次启动配置ssh的信息
HOLER_CLIENT-822404317F9D8ADD
holer.org

# 在客户端连接
ssh -p 65534 holer.org
```
**2. [ NPS ]**

[https://ehang-io.github.io/nps]

内网穿透，方便访问校内服务器。

**要求**：有自己的服务器，如阿里云

1. 服务端

   在config配置服务器IP、安装、启动。

   可在http://ip:8024管理：

   	- 新建客户端，在服务器端需要使用其中的字段
   	- 新建TCP连接，配置好端口，后续使用这个端口就可以转发目的地址

2. 客户端

   - 下载对应的client端，mac上是`darwin`

   - 根据服务器新建客户端的字段启动服务

3. 用户

   - 在任意设备连接公网服务器:端口即可连接
   
---

## ⚪ 文件相关

- 远程复制文件
```shell
scp -r -P {port} root@host:~/path/of/folder
```

- 快速在主机间传输文件
```shell
tar -c /path/to/dir | ssh remote_server 'tar -xvf - -C /absolute/path/to/remotedir'
```

- 复制前100个文件夹
``` shell
ls |head -n 100 |xargs -i cp -r {} ../food100
```
