# ceph架构

![](http://www.ibm.com/developerworks/cn/linux/l-ceph/figure1.gif)

参考：http://www.ibm.com/developerworks/cn/cloud/library/cl-openstackceph/
与任何经典的分布式文件系统中一样，放入集群中的文件是条带化的，依据一种称为Ceph Controlled Replication Under
Scalable Hashing(CRUSH)的伪随机的数据分布算法放入集群节点中。


![](http://docs.ceph.com/docs/master/_images/ditaa-cffd08dd3e192a5f1d724ad7930cb04200b9b425.png)
