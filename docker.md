## docker学习
 1. docker run [options] IMAGE [command]
``` 
docker run用来基于特定的镜像创建一个容器，如docker run ubuntu echo "hello world"
sudo docker run -i -t --name mytest ubuntu:latest /bin/bash
-i表示使用交互模式
-t表示分配一个伪终端
--name可以指定docker run命令启动容器的名词，无此选项，Docker将为容器随机分配一个名字
在镜像名后添加tag来区分同名的镜像，如ubuntu:14.04，默认选取tag为latest的镜像。
```
 2. docker ps
 3. docker commit

## docker部署
docker的设计理念是希望用户能够保证一个容器只运行一个进程，即只提供一种服务。
然而，单一容器是无法满足需求的，通常用户需要利用多个容器，分别提供不同的服务，并在不同容器间互连通信，最后形成一个docker集群。

docker run命令的--link选项建立容器间的互联关系。



##使用docker镜像和仓库
 - sudo docker images列出镜像，镜像保存在仓库中，仓库存在Registry中，默认的Registry是由docker公司运营的公共Registry服务，即Docker Hub。
 
用docker run从镜像启动一个容器时，如果该镜像不在本地，Docker会先从Docker Hub下载该镜像，下载latest的。
  - 查找镜像sudo docker search puppet
  
### 原来ubuntu 14.10 utopic不能安装docker的问题
docker不支持14.10utopic，一般安装utrusty。
在/etc/apt/source.list中做替换操作。
 1. sudo sh -c "echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
 2. whereis curl
 3. 1722  curl: /usr/bin/curl /usr/bin/X11/curl /usr/share/man/man1/curl.1.gz
 4. 1723  sudo apt-get -y install curl
 5. 1724  sudo apt-get -y install
 6. 1725  sudo apt-get -y install -f
 7. 1726  sudo apt-get -y install -f --force-yes
 8. 1727  curl -s https://get.docker.io/gpg | sudo apt-key add -
 9. 1728  uname -a
 10. 1729  sudo apt-get update
 11. 1730  ls -l /sys/class/misc/device-mapper
 12. 1731  whereis curl
 13. 1732  sudo apt-get -y install curl
 14. 1733  sudo apt-get install lxc-docker
 15. 1734  sudo apt-get -f install lxc-docker
 16. 1735  sudo apt-get -f install
 17. 1736  sudo apt-get -f install docker.io
 18. 1737  vi helloworld.cpp
 19. 1738  sudo apt-get -f install emacs24

http://mirrors.aliyun.com/help/ubuntu
