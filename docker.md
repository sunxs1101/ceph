##使用docker镜像和仓库
 - sudo docker images列出镜像，镜像保存在仓库中，仓库存在Registry中，默认的Registry是由docker公司运营的公共Registry服务，即Docker Hub。
 
用docker run从镜像启动一个容器时，如果该镜像不在本地，Docker会先从Docker Hub下载该镜像，下载latest的。
  - 查找镜像sudo docker search puppet
  
 
