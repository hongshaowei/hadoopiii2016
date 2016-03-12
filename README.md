# Big Data之處理與分析實務班
==========================

## Slides

- https://www.slideshare.net/secret/jAXKRnPCrknokG


## Centos 6.6 檔案下載

- https://drive.google.com/a/largitdata.com/file/d/0BwcmldsH2om-T3dQS2V3QklmNHM/view?usp=sharing

## 安裝步驟
---------------------------------------

### prepare machine
- ifconfig
- su - 
- ssh-keygen
- cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
- ssh localhost

### setup hostname
- gedit /etc/hosts
- hostname master
- hostname -f

### setup ntp
- chkconfig ntpd on
- service ntpd start

### Java Download
- http://192.168.39.54/dl/jdk-7u79-linux-x64.rpm
- rpm –ivh jdk-7u79-linux-x64.rpm

### 於安裝主機上建立軟連結
- ln -s /usr/java/jdk1.7.0_79 /usr/java/java

### 於安裝主機設定環境變數
- vi /etc/profile 

```
export JAVA_HOME=/usr/java/java
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib/rt.jar
export PATH=$PATH:$JAVA_HOME/bin
```


### 立即更新
- source /etc/profile

### 檢查 Java 版本
- java -version


### 於安裝主機關閉防火牆
- chkconfig iptables off
- service iptables stop

### 於安裝主機設定SELlinux
- vi /etc/selinux/config 將 SELINUX=disabled
- setenforce 0

### HDP建議關閉 Transparent Huge Pages，於安裝主機上執行
- echo never > /sys/kernel/mm/redhat_transparent_hugepage/enabled
- echo never > /sys/kernel/mm/redhat_transparent_hugepage/defrag

### 確定登入帳號為 root 在 master 上執行 (需要網路環境好的環境下)
- cd /tmp
- wget -nv http://public-repo-1.hortonworks.com/ambari/centos6/2.x/updates/2.2.0.0/ambari.repo -O /etc/yum.repos.d/ambari.repo 
- yum repolist
- yum install ambari-server

### 替代方案
- http://192.168.39.54/dl/ambari-server-2.2.0.0-1310.x86_64.rpm
- yum localinstall ambari-server-2.2.0.0-1310.x86_64.rpm

### 設定 Ambari
- ambari-server setup

### 安裝 Ambari
- ambari-server start

## Java WordCount 操作範例
- https://www.youtube.com/watch?v=h0mFQkqNo5g

