ansible file模块

path参数 ：必须参数，用于指定要操作的文件或目录，在之前版本的ansible中，使用dest参数或者name参数指定要操作的文件或目录，为了兼容之前的版本，使用dest或name也可以。

上传文件夹
∂∂

一些内置函数

这里 host 进行表名 
[host]
127.0.0.1 etcdname=etcd1

区分group_vars和host_vars的变量区别



ExecStart=/usr/local/bin/etcd --name my-etcd-{{ ansible_hostname }} \
        --data-dir /var/lib/etcd \
        --listen-client-urls http://{{ ansible_default_ipv4.address }}:2379 \
        --advertise-client-urls http://{{ ansible_fqdn }}:2379 \
        --listen-peer-urls http://{{ ansible_default_ipv4.address }}:2380 \
        --initial-advertise-peer-urls https://{{ ansible_fqdn }}:2380 \
        --initial-cluster {% for host in groups[etcd_group] %}{% if not loop.first %},{% endif %}my-etcd-{{ hostvars[host].ansible_hostname }}=http://{{ hostvars[host].ansible_fqdn  }}:2380{% endfor %}
