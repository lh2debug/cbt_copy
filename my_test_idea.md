# my test idea



## 测试形态
S3
rados
RBD


### 区别

Cosbench (cosbench.py): 这个脚本可能是用来运行 Cosbench，这是一个用于云存储系统的基准测试工具。它可能包括对 Ceph 存储系统进行各种操作的测试，比如读写操作、对象大小、并发进程数等。

CephTestRados (cephtestrados.py): 这个脚本是用于运行 Ceph 自带的 ceph_test_rados 测试工具，它是一个用于测试 RADOS 层性能的基准测试工具。

Fio (fio.py): 这个脚本用于配置和运行 FIO（Flexible I/O Tester），这是一个非常灵活的 I/O 测试工具，可以用于测试不同的 I/O 模式、块大小、并发级别等。

KvmRbdFio (kvmrbdfio.py): 这个脚本可能是用于在 KVM 虚拟机环境中运行 RBD FIO 测试。它可能涉及到在虚拟机中使用 RBD 作为存储后端，并运行 FIO 测试。

Hsbench (hsbench.py): 这个脚本可能用于运行针对 Ceph S3 或 Swift 接口的基准测试，测试可能包括创建桶、上传和下载对象等操作。

Getput (getput.py): 这个脚本可能用于测试 Ceph 集群的 GET 和 PUT 操作的性能，通常用于对象存储的基准测试。

LibrbdFio (librbdfio.py): 这个脚本用于配置和运行针对 librbd（RBD 的客户端库）的 FIO 测试，这可能包括对 RBD 图像的直接 I/O 操作。

Radosbench (radosbench.py): 这个脚本用于运行 Ceph 自带的 radosbench 工具，它是用于测试 RADOS 存储性能的基准测试工具。

Nullbench (nullbench.py): 这个脚本可能用作一个空的基准测试，不进行任何实际的测试操作，可能用于测试框架的某些方面，而不需要执行实际的性能测试。

RbdFio (rbdfio.py): 这个脚本用于运行针对 RBD 的 FIO 测试，它可能包括创建 RBD 图像、挂载它们，然后运行 FIO 测试。

## 是否可以启动多客户端测试

可以


## 可以改测试参数吗

可以理解有的参数可设置，有的参数不可以设置，具体参考脚本参数

参数主要是和性能有关系，比如

  pool_profiles:
    replication:
      pg_size: 256
      pgp_size: 256
      replication: 1 
    ec21:
      pg_size: 2048 
      pgp_size: 2048
      replication: 'erasure'
      erasure_profile: 'ec21'


## 可以搞failover吗

通过阅读源码以及测试，已经确定没有办法做failover，像磁盘、网络、进程等的故障需要额外的工具去模拟



















