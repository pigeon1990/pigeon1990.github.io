---
title: "Note"
date: 2020-10-01T15:39:29+08:00
draft: true
---

```
ip rule add from $(ip route get 1 | grep -Po '(?<=src )(\S+)') table 128
ip rule add from 111.230.175.235 table 128
ip route add table 128 to $(ip route get 1 | grep -Po '(?<=src )(\S+)')/32 dev $(ip -4 route ls | grep default | grep -Po '(?<=dev )(\S+)')
ip route add table 128 default via $(ip -4 route ls | grep default | grep -Po '(?<=via )(\S+)')


rm -rf /etc/yum.repos.d/* && rpm -Uvh --force http://mirror.centos.org/centos/7/os/x86_64/Packages/centos-release-7-8.2003.0.el7.centos.x86_64.rpm && yum clean all && yum makecache

curl https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh > shadowsocks-libev.sh && chmod +x shadowsocks-libev.sh

expressvpn preferences set network_lock off
expressvpn preferences set force_vpn_dns false
```

