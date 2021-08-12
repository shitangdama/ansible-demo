https://www.cnblogs.com/yanjieli/p/10969299.html

https://github.com/svensp/cloud_hosts/tree/master/roles/etcd


参数对比

ExecStart=/usr/local/bin/etcd --name my-etcd-{{ ansible_hostname }} \
	--quota-backend-bytes {{ storage }} \ 后端大小超过给定配额时引发警报（0默认为低空间配额）。
    --data-dir /var/lib/etcd \
    --auto-compaction-retention {{ key_history }} \ 自动压缩模式 Interpret 'auto-compaction-retention' one of: 'periodic', 'revision'. 'periodic' for duration based retention, defaulting to hours if no time unit is provided (e.g. '5m'). 'revision' for revision number based retention.

    --listen-client-urls https://{{ ansible_default_ipv4.address }}:2379 \
    此成员的客户端URL的列表，以广播到集群的其余部分。这些URL可以包含域名。
默认值：“ http：// localhost：2379 ”
环境变量：ETCD_ADVERTISE_CLIENT_URLS
例如： “ http://example.com:2379，http://10.0.0.1:2379 ”
请注意，如果从群集成员中发布诸如http：// localhost：2379之类的URL，并且正在使用etcd的代理功能。这将导致循环，因为代理将向其转发请求，直到其资源（内存，文件描述符）最终耗尽为止。

    --advertise-client-urls https://{{ ansible_fqdn }}:2379 \
    

    --listen-peer-urls https://{{ ansible_default_ipv4.address }}:2380 \

    --initial-advertise-peer-urls https://{{ ansible_fqdn }}:2380 \

    --initial-cluster {% for host in groups[etcd_group] %}{% if not loop.first %},{% endif %}my-etcd-{{ hostvars[host].ansible_hostname }}=https://{{ hostvars[host].ansible_fqdn  }}:2380{% endfor %} \



https://blog.csdn.net/u011673554/article/details/48877985?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_title-12&spm=1001.2101.3001.4242


ansible -i


 ansible -i ./inventory remote -m ping -u root --ask-pass 

 ansible-playbook


 https://github.com/qist/k8s/blob/master/k8s-install.sh

 https://github.com/zhangguanzhang/consul-tls-ansible

 glusterfs

 https://kubernetes.io/zh/docs/concepts/storage/volumes/#nfs


 https://kubernetes.io/zh/docs/concepts/scheduling-eviction/pod-overhead/#%E9%AA%8C%E8%AF%81-pod-cgroup-%E9%99%90%E5%88%B6


 关于验证pod cgroup 限制


etcd的资源限制 怎么监控
 https://etcd.io/docs/v3.5/op-guide/hardware/#example-hardware-configurations


关于docker的控制 需要看线cri相关命令和代码
 https://kubernetes.io/zh/docs/tasks/administer-cluster/migrating-from-dockershim/check-if-dockershim-deprecation-affects-you/#role-of-dockershim



 Container命令ctr,crictl的用法

 https://blog.csdn.net/tongzidane/article/details/114587138

 Kubelet Eviction Policy 

 https://github.com/howieyuen/howieyuen.github.io/tree/31273576d6b34353b8c159207765c9be12bc3500/content/docs/kubernetes

 https://github.com/howieyuen/howieyuen.github.io/blob/31273576d6b34353b8c159207765c9be12bc3500/content/docs/kubernetes/kubelet/kubelet-eviction-manager.md



 kubelet-docker交互.md
 https://github.com/lx1036/code/blob/b026bbca968ff30db1249732f4d86c7b2527b97c/go/k8s/kubelet/docker/kubelet-docker%E4%BA%A4%E4%BA%92.md

kubelet 源码
 https://github.com/lx1036/code/blob/b026bbca968ff30db1249732f4d86c7b2527b97c/go/k8s/kubelet/kubelet%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90.md



 https://github.com/DarkForcesX/note/blob/ab57279a22bbc70bb2ab840dedf8cbc7d4481cac/00%E3%80%81k8sLink.md

 sgw组
 ecmp->dpvs->nginx


 https://xigang.github.io/2018/05/05/systemctl/