# Virtualisation

## Hypervisor


The software or firmware layer responsible for managing and allocating physical resources to virtual instances. It abstracts and isolates the guests from the physical hardware. 

Two types:
* Type 1: hyper visor has direct access to hardware (kvm is type 1 as it is a kernel module that turns the kernel into a hypervisor, however the kernel still run other processes too so it's actually a hybrid between type 1 and type 2)
* Type 2: hyper visor is a process and hw access goes via OS. E.g. virtualbox


## Paravirtualisation

* Guest OS is modified and aware of virtualisation and can coordinate with host to share resources better
* Examples: Xen and VMware's vSphere


## OS-level virtualisation

OS-level virtualization is an operating system virtualization paradigm in which the kernel allows the existence of multiple isolated user space instances, called containers (LXC, Solaris containers, AIX WPARs, HP-UX SRP Containers, Docker, Podman)


On Unix-like operating systems, this feature can be seen as an advanced implementation of the standard chroot mechanism, which changes the apparent root folder for the current running process and its children.

Relies on:
* Linux namespaces
  * partitions kernel resources such that one set of processes sees one set of resources while another set of processes sees a different set of resources. 
  * Resources may exist in multiple spaces
  * 8 different types: mnt, pid, net, ipc, utc, user, cgroup, time
* cgroups 
  * a Linux kernel feature that limits, accounts for, and isolates the resource usage (CPU, memory, disk I/O, etc.[1]) of a collection of processes. 


## Popular hypervisors

* Hyper-V - Runs on windows x86-64, can run guest os: windows + linux



