
# Shell Survival Kit

Tiene como objetivo responder 6 preguntas puntuales que sirven para dejar como documentación el estado actual del servidor.

### 1. ¿Qué máquina es ésta y que SO corre?

Comando `hostnamectl`

 Static hostname: srv1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: baec3fa12ebd4dd380f6cf24404ca096
         Boot ID: b36657a2f56d4cb18aa1eb32f696379d
  Virtualization: oracle
Operating System: Debian GNU/Linux 12 (bookworm)
          Kernel: Linux 6.1.0-52-amd64
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox

### 2. ¿Que direcciones de red tiene?

Comando `ip address`

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ee:cd:6e brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic enp0s3
       valid_lft 84518sec preferred_lft 84518sec
    inet6 fd17:625c:f037:2:a00:27ff:feee:cd6e/64 scope global dynamic mngtmpaddr 
       valid_lft 85953sec preferred_lft 13953sec
    inet6 fe80::a00:27ff:feee:cd6e/64 scope link 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:43:56:b3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.10/24 brd 192.168.100.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe43:56b3/64 scope link 
       valid_lft forever preferred_lft forever

Este comando permite listar las interfaces de red del dispositivo, permitiendo visualizar además las direcciones MAC y las IP asociadas a una interfaz. Lista otra información util, pero para este caso solo nos importa esto.

### 3. ¿Cuánto disco hay cuánto queda libre?  

