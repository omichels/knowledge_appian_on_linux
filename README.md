## Installation of Appian on Red Hat 9.x

the intention of this document to do it quick, not safe and correct, just 
quick and very very dirty

## Minimal configuration

12 CPU cores, 64 GB RAM, 500 GB free diskspace on /home


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


