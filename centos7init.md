修改主机名
```
hostnamectl set-hostname <hostname>
```

修改ip
```
vi /etc/sysconfig/network-scripts/ifcfg-enp0s3

service network restart
```

停防火墙
```
systemctl stop firewalld && systemctl disable firewalld
```

禁用SELINUX
```
setenforce 0
sed -i "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config
```

禁用UseDNS
```
sed -i "s/#UseDNS yes/UseDNS no/g" /etc/ssh/sshd_config
```

时间同步
```
systemctl enable chronyd && systemctl start chronyd && chronyc sources
```

yum 加速
```
curl -o /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

yum clean all && yum makecache fast
```

安装常用工具
```
yum install -y wget net-tools
```


