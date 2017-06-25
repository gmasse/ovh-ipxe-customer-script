# iPXE customer script (BETA)

Booting your server with your own iPXE script allows cool things like:
 - running diskless bare-metal system like CoreOS, SmartOS, ...
 - recovering with your own Rescue system or bare-metal restore tools (like Acronis and Idera)
 - launching Standard installer like ESXi, [Linux](https://gist.github.com/gmasse/008445b0a3d328cedd6a#linux-vnc-installer), Solaris, ...


How?
Using directly the RESTful API [EU](https://api.ovh.com/)|[CA](https://ca.api.ovh.com) or the API console [EU](https://api.ovh.com/console/)|[CA](https://ca.api.ovh.com/console/).

It's also working for Kimsufi [EU](https://eu.api.kimsufi.com)|[CA](https://ca.api.kimsufi.com) and SoYouStart [EU](https://eu.api.soyoustart.com)|[CA](https://ca.api.soyoustart.com).


#### 1. Upload your custom iPXE script
CoreOS example (https://coreos.com/docs/running-coreos/bare-metal/booting-with-ipxe/)

```http
POST /1.0/me/ipxeScript HTTP/1.1

{
  "description": "CoreOS stable",
  "name": "coreos",
  "script": "#!ipxe\n\nset base-url http://stable.release.core-os.net/amd64-usr/current\nkernel ${base-url}/coreos_production_pxe.vmlinuz sshkey=\"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAYQC2PxAKTLdczK9+RNsGGPsz0eC2pBlydBEcrbI7LSfiN7Bo5hQQVjki+Xpnp8EEYKpzu6eakL8MJj3E28wT/vNklT1KyMZrXnVhtsmOtBKKG/++odpaavdW2/AU0l7RZiE= coreos pxe demo\"\ninitrd ${base-url}/coreos_production_pxe_image.cpio.gz\nboot"
}
```
```http
HTTP/1.1 200 OK
```

#### 2. Request your custom bootId

```http
GET /1.0/dedicated/server/ns320309.ip-46-105-117.eu/boot?bootType=ipxeCustomerScript HTTP/1.1
```
```http
HTTP/1.1 200 OK

[
  38
]
```

#### 3. Configure your server to boot on your iPXE script

```http
PUT /1.0/dedicated/server/ns320309.ip-46-105-117.eu HTTP/1.1

{
  "bootId": 38
}
```
```http
HTTP/1.1 200 OK
```

#### 4. Reboot your server!
