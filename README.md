

### 如何通过ssh工具链连接内外网？[holer]
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
