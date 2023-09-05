# 如何解决k8s集群calico节点一直处于 0/1 running的情况

这里专指使用：https://github.com/easzlab/kubeasz  安装的k8s集群，

怎么安装这里略过，已经很傻瓜式操作。

但是当使用它通过ezctl add node的操作的时候，会发现，节点成功添加了，但是对应添加的calico pod，却变为了0/1 running，始终起不来，这里记录一下原因和解决办法。

## 一、原因

> calico要通过解析hosts文件，来确定节点的ip地址，kubeasz脚本ezctl add node，如果不指定node name，那么默认名称是default，这点可以通过kubectl get -A nodes确认

那么calico的节点名是什么呢？因为calico也是kubeasz ezctl对应命令装上的，所以也是这个node name，要检查可以前往：https://docs.tigera.io/calico/latest/reference/configure-calico-node

calico查找节点文件名的顺序如下

![image](https://github.com/sherry0429/sherry0429.github.io/assets/11309831/354149bc-1193-44de-b583-6edab669d718)

经过查故障节点的/var/lib/calico/nodename也可以发现，该nodename和预期不一致


## 二、解决办法

1. 在所有步骤之前，先编辑各个节点的/etc/hosts文件，给每个节点各自的hostname，比如test.server1/test.server2

2. 使用ezctl add-node的时候，指定/etc/hosts中记录的名称
```shell
ezctl add-node cluster01 1.1.1.1 k8s_nodename=clickhouse.zk    # k8s_ndoename非常重要！一定要给，并且不能和其他节点重复，最好就是节点的host英文字符串
```

3. calico pod启动后可以检测/var/lib/calico/nodename文件，存在于etc/hosts文件中，则说明正常
