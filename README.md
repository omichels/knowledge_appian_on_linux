## Installation of Appian on Red Hat 9.x

the intention of this document to do it quick, not safe and correct, just 
quick and very very dirty

## minimal configuration

12 CPU cores, 64 GB RAM, 500 GB free diskspace on /home


## disable SELINUX

get rid of SELINUX, it's only a hassle. system calls will just be ignored
and you will wander, why nginx didn't bind to a port



## extend diskspace

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

```
vgs
vgdisplay
sudo xfs_growfs /home
```
