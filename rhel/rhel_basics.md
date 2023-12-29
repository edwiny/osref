# RHEL Basics


## Different product types

* RHEL AS - Advanced server
* RHEL ES - entry server
* RHEL WS - Enterprise linux work station
* RHEL Desktop 

## Versions

* 2007 - RHEL 5  - kernel 2.6.18-8
* 2011 - RHEL 6  - kernel 2.6.32
* 2014 - RHEL 7  - kernel 3.10
* 2019 - RHEL 8  - kernel 4.18
* 2022 - RHEL 9  - kernel 5.14.0


## Redhat products

* Openshift - Kubernetes containerisation platform


Common sys admin tasks to research:
* Security patching
* Package managemenent
* Backups
* Troubleshooting
* Database
* Containers 
* Virtualisation


NOTE: this info is for RHEL7!!!




## Inspecting the version

```
cat /etc/redhat-release
Red Hat Enterprise Linux Server release 7.9 (Maipo)
```

```
$ cat /etc/redhat-release
Red Hat Enterprise Linux Server release 7.9 (Maipo)
[ec2-user@ip-172-31-33-73 ~]$ cat /etc/os-release
NAME="Red Hat Enterprise Linux Server"
VERSION="7.9 (Maipo)"
ID="rhel"
ID_LIKE="fedora"
VARIANT="Server"
VARIANT_ID="server"
VERSION_ID="7.9"
PRETTY_NAME="Red Hat Enterprise Linux Server 7.9 (Maipo)"
...
```

```
$ hostnamectl
   Static hostname: ip-172-31-33-73.ap-southeast-2.compute.internal
         Icon name: computer-vm
           Chassis: vm
        Machine ID: ec2055a2d1b6e3c673a526ea011367f8
           Boot ID: 08892d664c104554a3972c531054af2e
    Virtualization: kvm
  Operating System: Red Hat Enterprise Linux Server 7.9 (Maipo)
       CPE OS Name: cpe:/o:redhat:enterprise_linux:7.9:GA:server
            Kernel: Linux 3.10.0-1160.15.2.el7.x86_64
      Architecture: x86-64
```


```
$ sudo yum install redhat-lsb-core
...
$ lsb_release -a
LSB Version:	:core-4.1-amd64:core-4.1-noarch
Distributor ID:	RedHatEnterpriseServer
Description:	Red Hat Enterprise Linux Server release 7.9 (Maipo)
Release:	7.9
Codename:	Maipo
```



## Networking

RHEL uses NetworkManager to manage configuration for network interfaces

Show all connections

```
$ nmcli con show

 ```

Ncurses ui for managing connections

```
nmtui
```


## Package management


See which repos are available, enabled

```
subscription-manager repos --list
yum repolist
```

Search for package in repo:

```
yum search <string>
```

Listing installed packages

```
yum list installed
```



## init.d / service management


Prior to RHEL7 used SysV style init.d + rc.N style.

With RHEL7 introduced the concept of service "units" and migration to systemd style.
In systemd, positive and negative dependencies between services exist. Starting particular service may require starting one or more other services (positive dependency) or stopping one or more services (negative dependency). 

The SysV style "runlevels" are replaced by systemd "target units." They group together other systemd units through a chain of dependencies.


startup scripts are symlinks in:

`/etc/systemd/system` pointing to `/usr/lib/systemd/system/name.<service>`




```
systemctl start name.service
systemctl reload name.service
systemctl status name.service
systemctl is-active name.service
systemctl list-units --type service --all
systemctl enable name.service
```

Boot/shutdown commands are also handled by systemctl:
```
systemctl halt
systemctl poweroff
systemctl reboot
systemctl suspend
systemctl hibernate
```

## User management

```
sudo useradd <username>
sudo passwd <username>
```



## Disk managmeent


Use `lsblk` to inspect disks;

```
$ lsblk
NAME        MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
nvme0n1     259:1    0  10G  0 disk
├─nvme0n1p1 259:2    0   1M  0 part
└─nvme0n1p2 259:3    0  10G  0 part /
nvme1n1     259:0    0   5G  0 disk
```

Use lvm to manage storage devices better.

* 'groups' are collections of physical disks / partitions
* 'volumes' are created on top of the groups, and is a subset of the groups

Making multiple disks appear as one volume:

```
# prepare disks
sudo pvcreate /dev/sdX1 /dev/sdY1
sudo vgcreate my_volume_group /dev/sdX1 /dev/sdY1
sudo lvcreate --type striped --size <size> --stripes <stripe_count> --name my_striped_volume my_volume_group
sudo mkfs.ext4 /dev/my_volume_group/my_striped_volume
sudo mount /dev/my_volume_group/my_striped_volume /mnt/my_mount_point
```

To resize a volume:

```
# check free space
sudo vgdisplay my_volume_group
# resize the "device"
sudo lvresize -L +10G /dev/my_volume_group/my_logical_volume
# resize the filesystem
sudo resize2fs /dev/my_volume_group/my_logical_volume

```



## Virtualisation on RHEL

### KVM

* Type 1 hypervisor (direct hardware access for guest os)
* Requires hardware features  Intel VT-x and AMD-V

Tools:
* libvirt - api for virtualisation and provides cmd line utils
* virt-manager is graphical user interface for managing vms




