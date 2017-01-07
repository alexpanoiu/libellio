# libellio

> [Libellus continens] Bruti senis oscitationes de capsa miseri libellionis emptu[s] plus minus asse Gaiano.

> (P. Papinius Statius, Silvae, 4.9 "Hendecasyllabi iocosi ad Plotium Grypum")

- [Latin text](http://www.perseus.tufts.edu/hopper/text?doc=Stat.%20Silv.%204.9.21&lang=original) at [Perseus](http://www.perseus.tufts.edu/hopper/) Digital Library
- [Translation](https://books.google.ro/books?id=8XVhb9IAJloC&pg=PA146) by Betty Rose Nagle at [https://books.google.com/](Google Books)

## System information

```
$ uname -smorv
Linux 4.4.0-57-generic #78-Ubuntu SMP Fri Dec 9 23:46:51 UTC 2016 i686 GNU/Linux

$ lsb_release -cidr
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.1 LTS
Release:        16.04
Codename:       xenial

$ df -h /
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       9.3G  1.2G  7.6G  14% /

$ free -m
              total        used        free      shared  buff/cache   available
Mem:            492          57         167           2         267         405
Swap:           510           0         510
```

## Locales

```
$ sudo dpkg-reconfigure locales

$ sudo localedef --delete-from-archive en_AG en_IN en_NG en_ZM

$ locale -a | column
C               en_CA.utf8      en_NG.utf8      en_ZM.utf8      fr_LU.utf8
C.UTF-8         en_DK.utf8      en_NZ.utf8      en_ZW.utf8      ro_RO.utf8
POSIX           en_GB.utf8      en_PH.utf8      fr_BE.utf8
en_AG.utf8      en_HK.utf8      en_SG.utf8      fr_CA.utf8
en_AU.utf8      en_IE.utf8      en_US.utf8      fr_CH.utf8
en_BW.utf8      en_IN.utf8      en_ZA.utf8      fr_FR.utf8
```

## Install software

```
sudo apt-get -y install build-essential
sudo apt-get -y install language-pack-fr manpages-fr{,-dev,-extra}
sudo apt-get -y install aptitude aptitude-doc-en
sudo apt-get -y install exfat-fuse exfat-utils
sudo apt-get -y install sshfs
sudo apt-get -y install cifs-utils
sudo apt-get -y install fonttools inxi lynx mc smartmontools tidy
sudo apt-get -y install openssh-server samba
sudo apt-get -y install apache2 apache2-doc libapache2-mod-fastcgi
sudo apt-get -y install php-fpm php-gd php-xml
```

```
$ ls /etc/rc3.d/*{apache,php,samba}* | cat
/etc/rc3.d/K01apache-htcacheclean
/etc/rc3.d/S01php7.0-fpm
/etc/rc3.d/S01samba-ad-dc
/etc/rc3.d/S02apache2

$ sudo systemctl status samba-ad-dc apache2 php7.0-fpm |& cut -c 1-$COLUMNS
● samba-ad-dc.service - LSB: start Samba daemons for the AD DC
   Loaded: loaded (/etc/init.d/samba-ad-dc; bad; vendor preset: enabled)
   Active: active (exited) since Sun 2017-01-08 00:13:07 EET; 6min ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0
   Memory: 0B
      CPU: 0

Jan 08 00:13:07 libellio systemd[1]: Starting LSB: start Samba daemons for the A
Jan 08 00:13:07 libellio systemd[1]: Started LSB: start Samba daemons for the AD

● apache2.service - LSB: Apache2 web server
   Loaded: loaded (/etc/init.d/apache2; bad; vendor preset: enabled)
  Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
   Active: active (running) since Sun 2017-01-08 00:13:18 EET; 6min ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 56
   Memory: 2.1M
      CPU: 270ms
   CGroup: /system.slice/apache2.service
           ├─23706 /usr/sbin/apache2 -k start
           ├─23709 /usr/sbin/fcgi-pm -k start
           ├─23710 /usr/sbin/apache2 -k start
           └─23711 /usr/sbin/apache2 -k start

Jan 08 00:13:17 libellio systemd[1]: Stopped LSB: Apache2 web server.
Jan 08 00:13:17 libellio systemd[1]: Starting LSB: Apache2 web server...
Jan 08 00:13:17 libellio apache2[23689]:  * Starting Apache httpd web server apa
Jan 08 00:13:17 libellio apache2[23689]: AH00558: apache2: Could not reliably de
Jan 08 00:13:18 libellio apache2[23689]:  *
Jan 08 00:13:18 libellio systemd[1]: Started LSB: Apache2 web server.

● php7.0-fpm.service - The PHP 7.0 FastCGI Process Manager
   Loaded: loaded (/lib/systemd/system/php7.0-fpm.service; enabled; vendor prese
   Active: active (running) since Sun 2017-01-08 00:13:33 EET; 6min ago
  Process: 32288 ExecStartPre=/usr/lib/php/php7.0-fpm-checkconf (code=exited, st
 Main PID: 32297 (php-fpm7.0)
   Status: "Processes active: 0, idle: 2, Requests: 0, slow: 0, Traffic: 0req/se
    Tasks: 3
   Memory: 12.9M
      CPU: 65ms
   CGroup: /system.slice/php7.0-fpm.service
           ├─32297 php-fpm: master process (/etc/php/7.0/fpm/php-fpm.conf)
           ├─32300 php-fpm: pool www
           └─32301 php-fpm: pool www

Jan 08 00:13:33 libellio systemd[1]: Stopped The PHP 7.0 FastCGI Process Manager
Jan 08 00:13:33 libellio systemd[1]: Starting The PHP 7.0 FastCGI Process Manage
Jan 08 00:13:33 libellio systemd[1]: Started The PHP 7.0 FastCGI Process Manager

$ sudo systemctl stop samba-ad-dc apache2 php7.0-fpm

$ sudo systemctl disable samba-ad-dc apache2 php7.0-fpm |& cut -c 1-$COLUMNS
samba-ad-dc.service is not a native service, redirecting to systemd-sysv-install
Executing /lib/systemd/systemd-sysv-install disable samba-ad-dc
insserv: warning: current start runlevel(s) (empty) of script `samba-ad-dc' over
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `samba-ad-d
apache2.service is not a native service, redirecting to systemd-sysv-install
Executing /lib/systemd/systemd-sysv-install disable apache2
insserv: warning: current start runlevel(s) (empty) of script `apache2' override
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `apache2' o
Synchronizing state of php7.0-fpm.service with SysV init with /lib/systemd/syste
Executing /lib/systemd/systemd-sysv-install disable php7.0-fpm
insserv: warning: current start runlevel(s) (empty) of script `php7.0-fpm' overr
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `php7.0-fpm

$ ls /etc/rc3.d/*{apache,php,samba}* | cat
/etc/rc3.d/K01apache-htcacheclean
/etc/rc3.d/K01apache2
/etc/rc3.d/K01php7.0-fpm
/etc/rc3.d/K01samba-ad-dc
```

```
$ df -h /
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       9.3G  1.8G  7.1G  20% /

$ sudo apt-get clean; sudo apt-get update >/dev/null
$ df -h /
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       9.3G  1.7G  7.2G  19% /
```

## Detailed system info

```
$ inxi -c0 -v5
System:    Host: libellio Kernel: 4.4.0-57-generic i686 (32 bit gcc: 5.4.0)
           Console: tty 0 Distro: Ubuntu 16.04 xenial
Machine:   System: VMware product: VMware Virtual Platform
           Mobo: Intel model: 440BX Desktop Reference Platform
           Bios: Phoenix v: 6.00 date: 07/02/2015
CPU:       Single core Intel Core i7-4700MQ (-UP-) cache: 6144 KB
           flags: (lm nx pae sse sse2 sse3 sse4_1 sse4_2 ssse3) bmips: 4789 speed: 2394 MHz (max)
Memory:    No dmidecode memory data: try newer kernel.
Graphics:  Card: VMware SVGA II Adapter bus-ID: 00:0f.0
           Display Server: N/A driver: N/A
           tty size: 80x43 Advanced Data: N/A out of X
Audio:     Card Ensoniq ES1371 / Creative Labs CT2518/ES1373
           driver: snd_ens1371 port: 2000 bus-ID: 02:01.0
           Sound: Advanced Linux Sound Architecture v: k4.4.0-57-generic
Network:   Card: VMware VMXNET3 Ethernet Controller
           driver: vmxnet3 v: 1.4.7.0-k port: 5000 bus-ID: 0b:00.0
           IF: ens192 state: up speed: 10000 Mbps duplex: full
           mac: 00:50:56:09:f0:11
Drives:    HDD Total Size: 10.7GB (20.8% used)
           ID-1: /dev/sda model: VMware_Virtual_S size: 10.7GB temp: 0C
           Optical: No optical drives detected.
Partition: ID-1: / size: 9.3G used: 1.7G (19%) fs: ext4 dev: /dev/sda2
           label: LIBELLIO-SYSTEM uuid: afcea285-63f2-40fb-8dbc-ce144642cc14
           ID-2: swap-1 size: 0.54GB used: 0.00GB (0%) fs: swap dev: /dev/sda1
           label: LIBELLIO-SWAP uuid: f7a387a8-9a0b-4379-abc3-87735ad645a8
RAID:      No RAID devices: /proc/mdstat, md_mod kernel module present
Sensors:   System Temperatures: cpu: 100.0C mobo: N/A
           Fan Speeds (in rpm): cpu: N/A
Info:      Processes: 178 Uptime: 6 min Memory: 93.5/492.9MB
           Init: systemd runlevel: 5 Gcc sys: 5.4.0
           Client: Shell (bash 4.3.461) inxi: 2.2.35
```
