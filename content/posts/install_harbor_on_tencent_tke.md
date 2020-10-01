---
title: "在腾讯云TKE,上安装Harbor"
date: 2020-10-01T15:30:08+08:00
draft: true
toc: true
---

## 安装 NFS 服务器

```bash
yum -y install nfs-utils
mkdir /nfsroot
ip //TODO get ip use shell script
echo '/nfsroot 172.16.0.12/20(ro,no_root_squash,no_subtree_check)' > /etc/exports
exportfs -r
systemctl enable nfs
systemctl start nfs
showmount -e
/nfsroot 172.16.0.12/20
```

## 创建 PV PVC

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:  # PV建立不要加名称空间，因为PV属于集群级别的
  name: nfs-pv001  # PV名称
  labels: # 这些labels可以不定义
    name: nfs-pv001
    storetype: nfs
spec:  # 这里的spec和volumes里面的一样
  storageClassName: normal
  accessModes:  # 设置访问模型
    - ReadWriteMany
    - ReadWriteOnce
    - ReadOnlyMany
  capacity: # 设置存储空间大小
    storage: 500Mi
  persistentVolumeReclaimPolicy: Retain # 回收策略
  nfs:
    path: /work/volumes/v1
    server: stroagesrv01.contoso.com
```

