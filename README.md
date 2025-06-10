## Installation of Appian on Red Hat 9.x

the intention of this document to do it quick, not safe and correct, just 
quick and very very dirty

## Minimal configuration

12 CPU cores, 64 GB RAM, 500 GB free diskspace on /home
Do not use Red-Hat Linux, use a decent linux which is not made for security-paranoia nerds


## Disable SELINUX

get rid of SELINUX, it's only a hassle. system calls will just be ignored
and you will wonder, why nginx didn't bind to a port

```
vi /etc/selinux/config
```

uncomment everything, leave only this line, after that reboot.

```
SELINUX=disabled
```


## Extend diskspace

### identify the new disk (after reboot)
```
lsblk
```

### create a physical volume on the disk
```
pvcreate /dev/sdX1 (X1 may be a, b, c, whatever)
```
### extend the volumegroup
```
vgextend <vg_name> /dev/sdX1
```

### verify

```
vgs
vgdisplay
```

### grow the filesystem
```
xfs_growfs /home
```

### prepare virtual memory, elasticsearch may complain about 'max virtual memory areas vm.max_map_count is too low'

```
sysctl -w vm.max_map_count=262144
```

### Useradd appian

Install in /home/appian, su - appian

verify the following tools:
- which java
- which jps (part of openjdk-devel)
- logrotate

### prepare virtual memory, elasticsearch may complain about 'max virtual memory areas vm.max_map_count is too low'

```
sysctl -w vm.max_map_count=262144
```


### Install NGINX as a TLS-reverse proxy

```
yum install nginx
```


### verify that nginx listens on port 443

```
netstat -tunlp | grep 443
```




