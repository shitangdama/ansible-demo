https://www.cnblogs.com/yanjieli/p/10969299.html

https://github.com/svensp/cloud_hosts/tree/master/roles/etcd

https://www.bilibili.com/video/BV19p4y1t7ZB?p=13

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