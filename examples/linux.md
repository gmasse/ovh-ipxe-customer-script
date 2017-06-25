# iPXE scripts
These iPXE scripts can be used on OVH Dedicated Server with the [iPXE Customer Script feature](https://gist.github.com/gmasse/4b0c34be3d797cd729d2)

#### Linux VNC installer
##### Fedora 21
:warning: All VNC traffic between client and server is unencrypted after authentication. It means the password you will type during the installation process will be passed in clear.
```
#!ipxe
set base http://fedora.mirrors.ovh.net/linux/releases/21/Server/x86_64/os
kernel ${base}/images/pxeboot/vmlinuz repo=${base} inst.vnc inst.vncpassword=YOURNONSECUREPASSWD ifname=eth0:${netX/mac} ip=eth0:dhcp nameserver=213.186.33.99
initrd ${base}/images/pxeboot/initrd.img
boot
```

##### CentOS 7
:warning: All VNC traffic between client and server is unencrypted after authentication. It means the password you will type during the installation process will be passed in clear.
```
#!ipxe
set base http://mirror.ovh.net/ftp.centos.org/7/os/x86_64
kernel ${base}/images/pxeboot/vmlinuz repo=${base} inst.vnc inst.vncpassword=YOURNONSECUREPASSWD ifname=eth0:${netX/mac} ip=eth0:dhcp nameserver=213.186.33.99
initrd ${base}/images/pxeboot/initrd.img
boot
```
