# VM Boot Failures

## VM starts then drops straight to pause state

There are two primary reasons this will occur:

* Disk space
* incorrect Libvirt type

Run the command below to determine if you have a disk space issue:
```bash
[root@compute-001 ~]# df -kh
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        40G   16G   25G  38% /
devtmpfs         16G     0   16G   0% /dev
tmpfs            16G  4.0K   16G   1% /dev/shm
tmpfs            16G  420K   16G   1% /run
tmpfs            16G     0   16G   0% /sys/fs/cgroup
tmpfs           3.2G     0  3.2G   0% /run/user/0
```


This error can also occur if you are using nested virtualisation or running your hypervisor on a non KVM based system

```bash

```