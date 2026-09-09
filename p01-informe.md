# Shell Survival Kit

Tiene como objetivo responder 6 preguntas puntuales que sirven para dejar como documentación el estado actual del servidor.

### 1. ¿Qué máquina es ésta y que SO corre?

Comando `hostnamectl`

```
Static hostname:  srv1
Icon name:        computer-vm
Chassis:          vm 🖴
Machine ID:       baec3fa12ebd4dd380f6cf24404ca096
Boot ID:          f0133422da434d1ab4a57a0585a37b3d
Virtualization:   oracle
Operating System: Debian GNU/Linux 12 (bookworm)
Kernel:           Linux 6.1.0-52-amd64
Architecture:     x86-64
Hardware Vendor:  innotek GmbH
Hardware Model:   VirtualBox
Firmware Version: VirtualBox
```

### 2. ¿Que direcciones de red tiene?

Comando `ip address`

```
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
```

Este comando permite listar las interfaces de red del dispositivo, permitiendo visualizar además las direcciones MAC y las IP asociadas a una interfaz. Lista otra información util, pero para este caso solo nos importa esto.

### 3. ¿Cuánto disco hay y cuánto queda libre?

Comando `df` (Disk free)

```
S.ficheros	bloques de 1K	Usados	Disponibles	Uso%	Montado en
udev		987944		0	987944		0%	/dev
tmpfs		201448		556	200892		1%	/run
/dev/sda1	19480400	1936276	16529240	11%	/
tmpfs		1007232	0	1007232	0%	/dev/shm
tmpfs		5120		0	5120		0%	/run/lock
tmpfs		201444		0	201444		0%	/run/user/1000
```

### 4. ¿Cuánta memoria?

Comando `free -h`

```
		total	usado	libre	compartido	búf/caché	disponible
Mem:		1,9Gi	216Mi	1,7Gi	560Ki		96Mi		1,7Gi
Inter:		974Mi	0B	974Mi
```

### 5. ¿Qué Servicios están corriendo?

```
  UNIT                       LOAD    ACTIVE  SUB      DESCRIPTION
  cron.service               loaded  active  running  Regular background program processing daemon
  dbus.service               loaded  active  running  D-Bus System Message Bus
  getty@tty1.service         loaded  active  running  Getty on tty1
  ssh.service                loaded  active  running  OpenBSD Secure Shell server
  systemd-journald.service   loaded  active  running  Journal Service
  systemd-logind.service     loaded  active  running  User Login Management
  systemd-timesyncd.service  loaded  active  running  Network Time Synchronization
  systemd-udevd.service      loaded  active  running  Rule-based Manager for Device Events and Files
  user@1000.service          loaded  active  running  User Manager for UID 1000
  wpa_supplicant.service     loaded  active  running  WPA supplicant
```

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.
10 loaded units listed.

### 6. ¿Quién entró últimamente?

```
sysadmin	pts/0		10.0.2.2		Wed Sep  9 12:44   still logged in
reboot		system boot	6.1.0-52-amd64		Wed Sep  9 12:43   still running
sysadmin	pts/0		10.0.2.2		Sun Sep  6 15:11 - crash          (2+21:31)
sysadmin	pts/0		10.0.2.2		Sun Sep  6 14:57 - 15:11          (00:14)
reboot		system boot	6.1.0-52-amd64		Sun Sep  6 14:56   still running
sysadmin	pts/0		192.168.100.100		Sun Sep  6 13:06 - crash          (01:50)
sysadmin	tty1				Sun Sep  6 13:03 - crash          (01:53)
reboot		system boot	6.1.0-52-amd64		Sun Sep  6 13:03   still running
sysadmin	tty1				Thu Sep  3 19:22 - crash          (2+17:40)
reboot		system boot	6.1.0-52-amd64		Thu Sep  3 19:22   still running
sysadmin	tty1				Thu Sep  3 19:20 - crash          (00:01)
reboot		system boot	6.1.0-52-amd64		Thu Sep  3 19:20   still running
sysadmin	tty1				Thu Sep  3 19:16 - down           (00:03)
reboot		system boot	6.1.0-52-amd64		Thu Sep  3 19:16 - 19:20          (00:04)
sysadmin	tty1				Thu Sep  3 18:38 - crash          (00:37)
reboot		system boot	6.1.0-52-amd64		Thu Sep  3 18:38 - 19:20          (00:41)
reboot		system boot	6.1.0-52-amd64		Wed Aug 26 20:38 - 19:20         (7+22:42)
sysadmin	tty2				Wed Aug 26 20:12 - crash          (00:25)
sysadmin	tty1				Wed Aug 26 20:10 - crash          (00:27)
reboot		system boot	6.1.0-52-amd64		Wed Aug 26 20:10 - 19:20         (7+23:10)

wtmp empieza Wed Aug 26 20:10:16 2026
```

### 7. ¿Existe /etc/ssh/sshd_config? Y de las entradas que están directamente dentro de /etc (sin entrar en subdirectorios), ¿cuál se modificó más recientemente?

Si existe ssh_config.d y se puede comprobar facilmente hciendo cd hacia la carpeta ssh y comprobando con el comando ls el listado de archivos y directorios.

Y de las entradas de /etc la ultima que se modificó fue

```
-rw-r--r-- 1 root root      20 sep  9 12:43 resolv.conf
```

### 8. ¿Qué registró el sistema sobre los últimos accesos por SSH? Mostrá los últimos diez eventos del servicio y explicá qué dice cada tipo de línea.

Comando `journalctl _SYSTEMD_UNIT=ssh.service | grep "Accepted" | tail -n 10`

```
sep 06 13:06:31 srv1 sshd[618]: Accepted password for sysadmin from 192.168.100.100 port 55032 ssh2
sep 06 14:57:33 srv1 sshd[581]: Accepted password for sysadmin from 10.0.2.2 port 57916 ssh2
sep 06 15:11:55 srv1 sshd[680]: Accepted password for sysadmin from 10.0.2.2 port 40934 ssh2
sep 09 12:44:31 srv1 sshd[581]: Accepted password for sysadmin from 10.0.2.2 port 56484 ssh2
```
