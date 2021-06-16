https://www.cnblogs.com/yanjieli/p/10969299.html

https://github.com/svensp/cloud_hosts/tree/master/roles/etcd

https://www.bilibili.com/video/BV19p4y1t7ZB?p=13

参数对比

ExecStart=/usr/local/bin/etcd --name my-etcd-{{ ansible_hostname }} \
	--quota-backend-bytes {{ storage }} \
    --data-dir /var/lib/etcd \
    --auto-compaction-retention {{ key_history }} \
    --listen-client-urls https://{{ ansible_default_ipv4.address }}:2379 \
    --advertise-client-urls https://{{ ansible_fqdn }}:2379 \
    --listen-peer-urls https://{{ ansible_default_ipv4.address }}:2380 \
    --initial-advertise-peer-urls https://{{ ansible_fqdn }}:2380 \
    --initial-cluster {% for host in groups[etcd_group] %}{% if not loop.first %},{% endif %}my-etcd-{{ hostvars[host].ansible_hostname }}=https://{{ hostvars[host].ansible_fqdn  }}:2380{% endfor %} \
    --initial-cluster-token my-etcd-token \
    --initial-cluster-state new \
	 --cert-file=/etc/etcd/client.cert.pem \
	 --key-file=/etc/etcd/client.key.pem \
	 --trusted-ca-file=/etc/etcd/client.cacert.pem \
	 --client-cert-auth=true \
	 --peer-cert-file=/etc/etcd/peer.cert.pem \
	 --peer-key-file=/etc/etcd/peer.key.pem \
	 --peer-client-cert-auth=true \
	 --peer-trusted-ca-file=/etc/etcd/peer.cacert.pem