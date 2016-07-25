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
