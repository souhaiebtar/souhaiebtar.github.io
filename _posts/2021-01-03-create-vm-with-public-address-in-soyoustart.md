---
layout: post
date: 2021-01-03 20:51:09
title: Create vm with public address in soyoustart
description: >-
  create vm with public address in soyoustart
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  create vm with public address in soyoustart
introduction: "how to create a vm with public address in soyoustart"
---

## Requirements
  * a server from soyoustart (it already come with public address ip 300.165.252.73, fake address for sake of example)
  * a failover ip associated with a mac address (it can be created on the UI, in our case the ip address p is 53.35.201.103 and MAC @ is 02:00:00:7b:22:80)

# How to proceed

in my case i choose to install ubuntu 20.04 on my server, i tried to install vmwareEsx and proxmox to try them but it wasn't a success because of the limitation of the UI provided to manage my server.

1. Install kvm
```BASH
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst
```

2. Give permission
```BASH
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
```

3. Allow forwarding
```BASH
sysctl -w net.ipv4.conf.all.forwarding=1
```

than now i will proceed with the exact step i used to get a vm with a public ip

```BASH
sudo su -
curl -fLO https://releases.ubuntu.com/16.04/ubuntu-16.04.7-server-amd64.iso
```

Create a  vm with a bridged network with eno1(the network interface that have access to internet) with the mac address that we got

```BASH
sudo virt-install \
--virt-type=kvm \
--name=ubuntu16 \
--ram=2048 \
--vcpus=2 \
--os-variant=ubuntu16.04 \
--virt-type=kvm \
--hvm \
--cdrom=/var/lib/libvirt/boot/ubuntu-16.04.7-server-amd64.iso \
--network type=direct,mac=02:00:00:7b:22:80,source=eno1,source_mode=bridge,model=rtl8139,address.type=pci,address.domain=0,address.bus=0,address.slot=9,address.function=0 \
--graphics vnc \
--disk path=/var/lib/libvirt/images/ubuntu16.qcow2,size=40,bus=virtio,format=qcow2
```


as we created the vm with option --graphics vnc, now we will finish the install after connecting using vnc

we run the next command to get the port used by vnc
```BASH
virsh dumpxml ubuntu16 | grep vnc
```

RESULT
```
<graphics type='vnc' port='5900' autoport='yes' listen='127.0.0.1'>
```


in this example the port used is 5900

know we will try to reverse proxy using ssh to the server (the public ip of our server that we got 37.23.43.22) to be able to open vnc to finish the install of our vm, open a new terminal

```BASH
ssh ubuntu@37.23.43.22 -L 5900:127.0.0.1:5900
```

now on your laptop, open your vnc client (in my case on macOS i simply opened `VNC Viewer`) and put localhost:5900 as address and proceed to the install when it come to network config just skip it for now, we will make config manually after)

after the install finish, connect again using your vnc client, now we will configure the network config

i started by running `ip -c a` to check the name address of the network interface, in my case it was `ens9`

i edited `/etc/network/interfaces` by adding the next block in the end

```
auto ens9
iface ens9 inet static
address 53.35.201.103
netmask 255.255.255.255
dns-nameservers 8.8.8.8
broadcast 53.35.201.103
post-up route add 300.165.252.73 dev ens9
post-up route add default gw 300.165.252.73
post-down route del default gw 300.165.252.73
post-down route del 300.165.252.73 dev ens9
```

and i started the machine `shutdown -r now`

after i restarted i installed nginx on the vm and i put the vm address in the browser to check if the page is showing and it does,

thanks goes to
[1]: https://lodge.glasgownet.com/tech/linux-kvm-vms-on-debian-soyoustart-hosts/
[2]: https://binaryimpulse.com/2014/08/ovh-ip-failover-vm-configuration/
