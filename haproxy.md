创建haproxy配置文件
```
mkdir -p /etc/haproxy/
```

```
cat > /etc/haproxy/haproxy.cfg << EOF
global
    daemon
    maxconn 256
#    user        haproxy
#    group       haproxy
#    chroot      /var/lib/haproxy

defaults
    mode tcp
    timeout connect 5000ms
    timeout client 50000ms
    timeout server 50000ms

listen registry
    bind *:6000
    mode tcp
    balance roundrobin
    server registry 30.0.0.11:5000 check port 5000 inter 1000 rise 2 fall 2 maxconn 32
    
listen apiserver
    bind *:6443
    mode tcp
    balance roundrobin
    server apiserver01 30.0.0.21:6443 check port 6443 inter 1000 rise 2 fall 2 maxconn 32
    server apiserver02 30.0.0.22:6443 check port 6443 inter 1000 rise 2 fall 2 maxconn 32
    server apiserver03 30.0.0.23:6443 check port 6443 inter 1000 rise 2 fall 2 maxconn 32
    server apiserver04 30.0.0.24:6443 check port 6443 inter 1000 rise 2 fall 2 maxconn 32
    server apiserver05 30.0.0.25:6443 check port 6443 inter 1000 rise 2 fall 2 maxconn 32
EOF

```

进程方式安装 haproxy
```
yum install -y haproxy

systemctl enable haproxy && systemctl start haproxy
```

