在使用kubeadm reset 重置kubernetes集群时，各node节点上的保存的原有配置信息会被删除掉。
但是创建的虚拟网卡还是会存在的，如flannel.1、cni0等。
建议重置集群后，一定要使用命令将其删除，否则会带来意外的故障。


  [root@docker2 ~]# ip link delete cni0
  [root@docker2 ~]# ip link delete flannel.1
  
  
我在创建nginx-ingress的时候，一直报错，重置集群后，重新添加还是报错。删除虚拟网卡后，在重新join集群，恢复正常。
