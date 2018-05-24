title: 【原创】Tomcat8 安装和配置、优化
date: 2017-05-16 18:58:35
tags:
- Tomcat
- Tomcat优化
categories: IT

---
﻿
# Tomcat 8 安装和配置、优化
## 1. Tomcat 8 安装目标
  - 安装h环境：rebhat 6.1 (linux通用)
  - 安装目录：`/opt/extra/apache-tomcat-8.5.31`
  - java目录：`/opt/java/jdk1.8.0_91`
  - 启动方式：`service tomcat8 start`
  - 配置：
     - 更新端口，可以增加数据源，配置系统服务，安全考虑
## 2. Tomcat 8 安装
### 2.1. 安装来源以及简介
  - 官网：<http://tomcat.apache.org/>
  - Tomcat 8 官网下载：<http://tomcat.apache.org/download-80.cgi>
  - 此时（20180524） Tomcat 8 最新版本为：`apache-tomcat-8.5.31.zip`
### 2.2. 安装目录
  - 我个人习惯 `/opt` 目录下创建一个目录 `software` 用来存放各种软件安装包；在 `/opt` 目录下创建一个 `apps` 用来存放各种解压后的软件包，下面的讲解也都是基于此习惯。不过下面是公司的按照我会按照`opt/extra/`来。
     - 压缩包解压：`unzip apache-tomcat-8.5.31.zip`
     -  移到解压出来文件夹到 /usr 下：`mv apache-tomcat-8.5.31/ /opt/extra/`
### 2.3. 更改端口（可跳过，根据需要修改）
  - 1) 编辑tomcat配置文件
     - 编辑tomcat配置文件`$tomcat_home/conf/server.xml` ，此处为：`/opt/extra/apache-tomcat-8.5.31/conf/server.xml`
  - 2) 更改服务关闭端口
   ``` xml
           <Server port="8205" shutdown="SHUTDOWN">
   ```
  - 3) 更改HTTP端口
   ``` xml
           <Connector port="8280" protocol="HTTP/1.1"
                  connectionTimeout="20000"
                  redirectPort="8643" />
   ```
  - 4) 更改AJP端口
   ``` xml
           <Connector port="8209" protocol="AJP/1.3" redirectPort="8643" />
   ```
### 2.4. 配置数据源（可跳过，根据需要修改）
  - 1) 更新端口
   ``` xml
    <Resource name="test/b2c" auth="Container" driverClassName="oracle.jdbc.driver.OracleDriver" defaultAutoCommit="true"
                 maxActive="20" maxWait="10000" initialSize="10" maxTotal="20" maxIdle="10"
                 username="test_app_1" password="**********" type="javax.sql.DataSource"
                 url="jdbc:oracle:thin:@(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=xxx.xxx.xx1)(PORT=1521))(ADDRESS=(PROTOCOL=TCP)(HOST=xxx.xxx.xx2)(PORT=1521))(LOAD_BALANCE=on)(FAILOVER=on))(CONNECT_DATA=(SERVICE_NAME=service.xxxx.com)(FAILOVER_MODE=(TYPE=SELECT)(METHOD=BASIC))))" 
                 validationQuery="SELECT sysdate FROM dual" testOnBorrow="true"/>
   ```
### 2.5. 配置启动脚本服务（官方推荐在$CATALINA_BASE/bin/setenv.sh）
  - 1) 为避免环境冲突，配置变量。编辑`vim /opt/extra/apache-tomcat-8.5.31/bin/setenv.sh`  然后保存 (可选, 官方recommended这种。 或者在catalina.sh在配置文件的可编辑内容最上面添加)
    ``` ini
    JRE_HOME=/opt/java/jdk1.8.0_91
    CATALINA_PID="$CATALINA_BASE/tomcat.pid"
    # CATALINA_PID=`cd ../;pwd`/tomcat.pid  #或者这种方式 # 可以不用   JAVA_HOME=/opt/java/jdk1.8.0_91
    ```

  - 2) 常用命令
      - 启动 
          - `/opt/extra/apache-tomcat-8.5.31/catalina.sh start  `
          - `sh /opt/extra/apache-tomcat-8.5.31/bin/startup.sh`  ； 可以边启动边查看日志 ;`sh  /opt/extra/apache-tomcat-8.5.31/bin/startup.sh; tail -200f /usr/program/tomcat8/logs/catalina.out` 
      - 关闭 `sh  /opt/extra/apache-tomcat-8.5.31/bin/shutdown.sh`  或者   `cat /opt/extra/apache-tomcat-8.5.31/tomcat.pid | xargs kill -9` 或者  /opt/extra/apache-tomcat-8.5.31/bin/catalina.sh stop

      - 查看服务 `ps aux|grep tomcat|grep -v grep`
### 2.6. 配置系统服务
  - 1)  配置JSVC服务启动方式 （为什么要用，查看附录说明）
    ``` shell
          cd /opt/tomcat/apache-tomcat-7.0.52/bin
          tar xvfz commons-daemon-native.tar.gz
          cd commons-daemon-1.0.15-native-src/unix
          ./configure --with-java=/opt/java/java-7-oracle
    ```

# 附录
## 解答环境
  - export 在子shell，父shell中的变量传递
      - 子 shell 对父 shell 里 export 出来的变量进行修改并不能影响到父 shell
      - 子 shell 只是在“导出变量列表“里对该变量进行了一个拷贝。但反过来，父shell再次更改此变量时，子 shell 再去读时，读到的是新值，而不是原来的值。
  - 为什么要用jsvc
     - Jsvc is a set of libraries and applications for making Java applications run on UNIX more easily. Jsvc allows the application (e.g. Tomcat) to perform some privileged operations as root (e.g. bindto a port < 1024), and then switch identity to a non-privileged user. 
     - 使用jsvc管理Tomcat的运行，相比使用其他方式最大的优势是可以使Tomcat以root身份做一些非root身份做不了的事，例如绑定端口到小与1024的端口，例如80。 
     - 通常为了安全考虑，linux服务器上运行Tomcat程序的进程其身份均不为root，这为Tomcat的正常使用带来了一些限制，使用jsvc恰好可以弥补这些限制带来的不足。

## 资料
- <http://tomcat.apache.org/tomcat-8.5-doc/setup.html>
- <http://tomcat.apache.org/tomcat-8.5-doc/RUNNING.txt>
- <http://tomcat.apache.org/tomcat-8.5-doc/BUILDING.txt>
- <http://commons.apache.org/proper/commons-daemon/jsvc.html> 
- <https://youmeek.gitbooks.io/linux-tutorial/content/markdown-file/Tomcat-Install-And-Settings.html >
- <http://www.jikexueyuan.com/course/2064_3.html?ss=1>
- <http://www.jikexueyuan.com/course/2064_3.html?ss=1>
- <http://www.wellho.net/mouth/2163_CATALINA-OPTS-v-JAVA-OPTS-What-is-the-difference-.html>
- <http://blog.csdn.net/sunlovefly2012/article/details/47395165>
- <http://blog.csdn.net/lifetragedy/article/details/7708724>
- <http://ihuangweiwei.iteye.com/blog/1233941>
- <http://www.cnblogs.com/ggjucheng/archive/2013/04/16/3024731.html>
- <http://www.apelearn.com/study_v2/chapter23.html>
- <http://blog.csdn.net/hanzheng260561728/article/details/51236131>
- <http://blog.csdn.net/attagain/article/details/38639007>