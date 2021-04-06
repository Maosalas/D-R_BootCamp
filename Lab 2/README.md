# Laboratorio 2

## Redes

:heavy_check_mark: Identificar ip del equipo, mascarade red y gateway

```
$ ifconfig
```
Resultado

* 192.168.240.128
* 255.255.255.0
* 192.168.240.25

:heavy_check_mark: Cambio de ip provisional

```
$ sudo ifconfig 192.168.240.129 netmask 255.255.255.0
```
Resultado

> Al reiniciar no se mantuvo la nueva ip

:heavy_check_mark: Ip de manera estatica
> Se utilizó Vi

```
$ vi /etc/network/interfaces
```

```
  iface eth0 inet static
  address <ip>/24
  gateway <ip>
```

```
$ service networking restart
```

:heavy_check_mark: Ver los puertos abiertos

```
$ netstat -lntu
```
>Resultado

```
$ tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN 
```

:heavy_check_mark: Ip por dhcp

```
$ echo “iface eth0 inet dhcp” >>/etc/network/interfaces
$ ifconfig eth0 up
```

:heavy_check_mark: Instalar ssh

```
$ sudo apt-get install ssh
$ sudo service ssh start
```
>Habilita ssh remoto
```
$ sudo update-rc.d -f ssh remove
```
>Agregar los defaults
```
$ sudo update-rc.d -f ssh defaults
```
>Cambiamos el puerto para mayor seguridad y le cambiamos el ListenAdress a 0.0.0.0
```
$ nano /etc/ssh/sshd_config
# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

Include /etc/ssh/sshd_config.d/*.conf

Port 10101
#AddressFamily any
ListenAddress 0.0.0.0
#ListenAddress ::

#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key
#HostKey /etc/ssh/ssh_host_ed25519_key
```

>Y tambien habilitamos el PermitRootLogin
```
Authentication:

#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

```

:heavy_check_mark: Uso de dig

```
$ apt-get install dnsutils
```
>Para encontrar todos los registros de google
```
$ dig google.com any
```
Resultados
```
google.com.             299     IN      A       172.217.193.100
google.com.             299     IN      A       172.217.193.138
google.com.             299     IN      A       172.217.193.113
google.com.             299     IN      A       172.217.193.101
google.com.             299     IN      A       172.217.193.102
google.com.             299     IN      A       172.217.193.139
google.com.             299     IN      AAAA    2607:f8b0:400c:c03::8a
google.com.             299     IN      AAAA    2607:f8b0:400c:c03::66
google.com.             299     IN      AAAA    2607:f8b0:400c:c03::65
google.com.             299     IN      AAAA    2607:f8b0:400c:c03::71
google.com.             3599    IN      TXT     "v=spf1 include:_spf.google.com ~all"
google.com.             3599    IN      TXT     "google-site-verification=wD8N7i1JTNTkezJ49swvWW48f8_9xveREV4oB-0Hf5o"
google.com.             3599    IN      TXT     "globalsign-smime-dv=CDYX+XFHUw2wml6/Gb8+59BsH31KzUr6c1l2BPvqKX8="
google.com.             599     IN      MX      20 alt1.aspmx.l.google.com.
google.com.             21599   IN      NS      ns4.google.com.
google.com.             21599   IN      NS      ns1.google.com.
google.com.             599     IN      MX      30 alt2.aspmx.l.google.com.
google.com.             599     IN      MX      50 alt4.aspmx.l.google.com.
google.com.             3599    IN      TXT     "apple-domain-verification=30afIBcvSuDV2PLX"
google.com.             21599   IN      CAA     0 issue "pki.goog"
google.com.             599     IN      MX      40 alt3.aspmx.l.google.com.
google.com.             3599    IN      TXT     "docusign=05958488-4752-4ef2-95eb-aa7ba8a3bd0e"
google.com.             3599    IN      TXT     "facebook-domain-verification=22rm551cu4k0ab0bxsw536tlds4h95"
google.com.             21599   IN      NS      ns2.google.com.
google.com.             59      IN      SOA     ns1.google.com. dns-admin.google.com. 366769421 900 900 1800 60
google.com.             3599    IN      TXT     "docusign=1b0a6754-49b1-4db5-8540-d2c12664b289"
google.com.             21599   IN      NS      ns3.google.com.
google.com.             599     IN      MX      10 aspmx.l.google.com.
```
>Los registros que mas se ven son de tipo AAAA

| Registro | Definicion |
| --- | --- |
| A | Hace referencia a la direccion ipv4 de un servidor web. |
| AAAA | Referencia a la direccion ipv6 de un host. |
| CAA| Posibles autoridades de sertificacion CA para un dominio.|
| SOA| Hace referencia al comienzo de autoridad, es uno de los mas importantes ya que guarda informacion esenciual como la fecga de la ultima actualizacion del dominio.|
| TXT| Referencia a un texto, esto permite que los admin insertent texto en los registros dns.|
| MX|Lista de servidor de intercambio de correo que se utiliza para este dominio. |
| NS| A los servidores de nombres es el autorizado par el dominio.|

:heavy_check_mark: Conectarse mediante iwconfig
> Escaneamos las redes
```
$ iwlist wlan0 scan
Cell 01 - Address: FE:EC:DA:2C:2D:78
                    ESSID:"Blippy"
                    Protocol:IEEE 802.11bgn
                    Mode:Master
                    Frequency:2.437 GHz (Channel 6)
                    Encryption key:on
                    Bit Rates:300 Mb/s
                    Extra:rsn_ie=30140100000fac040100000fac040100000fac020c00
                    IE: IEEE 802.11i/WPA2 Version 1
                        Group Cipher : CCMP
                        Pairwise Ciphers (1) : CCMP
                        Authentication Suites (1) : PSK
                    Quality=100/100  Signal level=100/100  

```
> Conectamos a nuestra red que queremos
```
$ iwconfig wlan0 essid Blippy key 01
```

# Manejo de paquetes
:heavy_check_mark: Actualizar los sources de kali

```
$ apt-get update
```
:heavy_check_mark: Instalar snort
```
$ apt-get install snort
```
* Install sin el manejador de paquetes
```
  $ git clone https://github.com/robertdavidgraham/masscan
  $ cd masscan
  $ make
  $ make install
```
:heavy_check_mark: Desinstalar snort
```
$ sudo apt-get remove --purge snort
```
# Manejo de permisos
:heavy_check_mark: Crear un nuevo grupo de usuarios
```
$ addgroup estudiantes
$ adduser -g estudiantes MauricioCR
```
:heavy_check_mark: Crear archivo en /tmp
```
$ cd /tmp
$ touch archivoTemp.txt
```
## Umask (user mask o máscara de usuario).

Es un comando para entornos POSIX que determina los permisos predeterminados que se establecen cuando creamos un archivo o directorio (carpeta).

También hace referencia a la función que establece la máscara (mask), y a la máscara en sí; normalmente se conoce como la máscara de creación del modo de archivo.

# Process Management
:heavy_check_mark: Procesos de mi maquina
```
$ ps
PID TTY          TIME CMD
   4431 pts/0    00:00:00 sudo
   4432 pts/0    00:00:00 su
   4433 pts/0    00:00:00 zsh
   4705 pts/0    00:00:00 sudo
   4706 pts/0    00:00:00 ps
```
>Mostrar todos los procesos del sistema
```
$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  99792 10652 ?        Ss   10:57   0:01 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    10:57   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   10:57   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   10:57   0:00 [rcu_par_gp]
root           6  0.0  0.0      0     0 ?        I<   10:57   0:00 [kworker/0:0H-events_highpri]
root           9  0.0  0.0      0     0 ?        I<   10:57   0:00 [mm_percpu_wq]
root          10  0.0  0.0      0     0 ?        S    10:57   0:00 [rcu_tasks_rude_]
root          11  0.0  0.0      0     0 ?        S    10:57   0:00 [rcu_tasks_trace]
root          12  0.0  0.0      0     0 ?        S    10:57   0:00 [ksoftirqd/0]
root          13  0.0  0.0      0     0 ?        I    10:57   0:00 [rcu_sched]
root          14  0.0  0.0      0     0 ?        S    10:57   0:00 [migration/0]
root          15  0.0  0.0      0     0 ?        S    10:57   0:00 [cpuhp/0]
root          17  0.0  0.0      0     0 ?        S    10:57   0:00 [kdevtmpfs]
root          18  0.0  0.0      0     0 ?        I<   10:57   0:00 [netns]
root          19  0.0  0.0      0     0 ?        S    10:57   0:00 [kauditd]
root          20  0.0  0.0      0     0 ?        S    10:57   0:00 [khungtaskd]
root          21  0.0  0.0      0     0 ?        S    10:57   0:00 [oom_reaper]
root          22  0.0  0.0      0     0 ?        I<   10:57   0:00 [writeback]
root          23  0.0  0.0      0     0 ?        S    10:57   0:00 [kcompactd0]
root          24  0.0  0.0      0     0 ?        SN   10:57   0:00 [ksmd]
root          25  0.0  0.0      0     0 ?        SN   10:57   0:00 [khugepaged]
root          43  0.0  0.0      0     0 ?        I<   10:57   0:00 [kintegrityd]
root          44  0.0  0.0      0     0 ?        I<   10:57   0:00 [kblockd]
root          45  0.0  0.0      0     0 ?        I<   10:57   0:00 [blkcg_punt_bio]
root          46  0.0  0.0      0     0 ?        I<   10:57   0:00 [edac-poller]
root          47  0.0  0.0      0     0 ?        I<   10:57   0:00 [devfreq_wq]
root          48  0.0  0.0      0     0 ?        I<   10:57   0:00 [kworker/0:1H-kblockd]
root          49  0.0  0.0      0     0 ?        S    10:57   0:00 [kswapd0]
root          50  0.0  0.0      0     0 ?        I<   10:57   0:00 [kthrotld]
root          51  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/24-pciehp]
root          52  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/25-pciehp]
root          53  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/26-pciehp]
root          54  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/27-pciehp]
root          55  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/28-pciehp]
root          56  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/29-pciehp]
root          57  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/30-pciehp]
root          58  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/31-pciehp]
root          59  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/32-pciehp]
root          60  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/33-pciehp]
root          61  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/34-pciehp]
root          62  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/35-pciehp]
root          63  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/36-pciehp]
root          64  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/37-pciehp]
root          65  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/38-pciehp]
root          66  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/39-pciehp]
root          67  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/40-pciehp]
root          68  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/41-pciehp]
root          69  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/42-pciehp]
root          70  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/43-pciehp]
root          71  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/44-pciehp]
root          72  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/45-pciehp]
root          73  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/46-pciehp]
root          74  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/47-pciehp]
root          75  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/48-pciehp]
root          76  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/49-pciehp]
root          77  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/50-pciehp]
root          78  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/51-pciehp]
root          79  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/52-pciehp]
root          80  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/53-pciehp]
root          81  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/54-pciehp]
root          82  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/55-pciehp]
root          83  0.0  0.0      0     0 ?        I<   10:57   0:00 [acpi_thermal_pm]
root          84  0.0  0.0      0     0 ?        I<   10:57   0:00 [ipv6_addrconf]
root          95  0.0  0.0      0     0 ?        I<   10:57   0:00 [kstrp]
root          98  0.0  0.0      0     0 ?        I<   10:57   0:00 [zswap-shrink]
root          99  0.0  0.0      0     0 ?        I<   10:57   0:00 [kworker/u257:0-hci0]
root         145  0.0  0.0      0     0 ?        I<   10:57   0:00 [mpt_poll_0]
root         146  0.0  0.0      0     0 ?        I<   10:57   0:00 [ata_sff]
root         147  0.0  0.0      0     0 ?        I<   10:57   0:00 [mpt/0]
root         148  0.0  0.0      0     0 ?        S    10:57   0:00 [scsi_eh_0]
root         149  0.0  0.0      0     0 ?        I<   10:57   0:00 [scsi_tmf_0]
root         150  0.0  0.0      0     0 ?        S    10:57   0:00 [scsi_eh_1]
root         151  0.0  0.0      0     0 ?        S    10:57   0:00 [irq/16-vmwgfx]
root         152  0.0  0.0      0     0 ?        I<   10:57   0:00 [scsi_tmf_1]
root         154  0.0  0.0      0     0 ?        I<   10:57   0:00 [cryptd]
root         156  0.0  0.0      0     0 ?        I<   10:57   0:00 [ttm_swap]
root         158  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc0]
root         160  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc1]
root         162  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc2]
root         164  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc3]
root         166  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc4]
root         168  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc5]
root         170  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc6]
root         172  0.0  0.0      0     0 ?        S    10:57   0:00 [card0-crtc7]
root         214  0.0  0.0      0     0 ?        S    10:57   0:00 [scsi_eh_2]
root         215  0.0  0.0      0     0 ?        I<   10:57   0:00 [scsi_tmf_2]
root         259  0.0  0.0      0     0 ?        S    10:57   0:00 [jbd2/sda1-8]
root         260  0.0  0.0      0     0 ?        I<   10:57   0:00 [ext4-rsv-conver]
root         311  0.0  0.4  89440 34980 ?        Ss   10:57   0:00 /lib/systemd/systemd-journald
root         321  0.0  0.0      0     0 ?        I<   10:57   0:00 [rpciod]
root         322  0.0  0.0      0     0 ?        I<   10:57   0:00 [xprtiod]
root         329  0.0  0.0 150472   276 ?        Ssl  10:57   0:00 vmware-vmblock-fuse /run/vmblock-fuse -o rw,subtype=vmware-vmblock,default_perm
root         337  0.0  0.0  23200  6456 ?        Ss   10:57   0:00 /lib/systemd/systemd-udevd
root         456  0.0  0.0   8120  7528 ?        Ss   10:57   0:00 /usr/sbin/haveged --Foreground --verbose=1
root         463  0.0  0.0  88992  7312 ?        Ssl  10:57   0:04 /usr/bin/vmtoolsd
root         467  0.0  0.0   6684  2784 ?        Ss   10:57   0:00 /usr/sbin/cron -f
message+     468  0.0  0.0   9420  5424 ?        Ss   10:57   0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd
root         473  0.0  0.2 254760 17216 ?        Ssl  10:57   0:00 /usr/sbin/NetworkManager --no-daemon
root         479  0.0  0.1 235324  9484 ?        Ssl  10:57   0:00 /usr/libexec/polkitd --no-debug
root         484  0.0  0.0 220740  4608 ?        Ssl  10:57   0:00 /usr/sbin/rsyslogd -n -iNONE
root         498  0.0  0.0  13956  7040 ?        Ss   10:57   0:00 /lib/systemd/systemd-logind
root         530  0.0  0.1 314792 12724 ?        Ssl  10:57   0:00 /usr/sbin/ModemManager
root         536  0.0  0.0      0     0 ?        I<   10:57   0:00 [kworker/u257:2-hci0]
root         558  0.0  0.0 308352  7372 ?        SLsl 10:57   0:00 /usr/sbin/lightdm
root         567  0.1  1.4 660476 114184 tty7    Ssl+ 10:57   0:11 /usr/lib/xorg/Xorg :0 -seat seat0 -auth /var/run/lightdm/root/:0 -nolisten tcp 
root         569  0.0  0.0   5784  1672 tty1     Ss+  10:57   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
rtkit        672  0.0  0.0 153684  3056 ?        SNsl 10:57   0:00 /usr/libexec/rtkit-daemon
root         721  0.0  0.1 163604  8760 ?        Sl   10:59   0:00 lightdm --session-child 14 23
mauricio     726  0.0  0.1  15392  8912 ?        Ss   10:59   0:00 /lib/systemd/systemd --user
mauricio     727  0.0  0.0 101468  2844 ?        S    10:59   0:00 (sd-pam)
mauricio     746  0.0  0.3 634044 27324 ?        S<sl 10:59   0:00 /usr/bin/pulseaudio --daemonize=no --log-target=journal
mauricio     752  0.0  0.2 269496 24056 ?        Ssl  10:59   0:00 xfce4-session
mauricio     753  0.0  0.0   8564  5136 ?        Ss   10:59   0:01 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --system
mauricio     795  0.0  0.0   5964   468 ?        Ss   10:59   0:00 /usr/bin/ssh-agent x-session-manager
mauricio     805  0.0  0.0 307280  6712 ?        Ssl  10:59   0:00 /usr/libexec/at-spi-bus-launcher
mauricio     810  0.0  0.0   8160  4300 ?        S    10:59   0:00 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.co
mauricio     814  0.0  0.0 230000  5716 ?        Sl   10:59   0:00 /usr/lib/x86_64-linux-gnu/xfce4/xfconf/xfconfd
mauricio     820  0.0  0.0 165800  6596 ?        Sl   10:59   0:00 /usr/libexec/at-spi2-registryd --use-gnome-session
mauricio     830  0.0  0.0  81036  3504 ?        SLs  10:59   0:00 /usr/bin/gpg-agent --supervised
mauricio     832  0.0  0.9 683776 79928 ?        Sl   10:59   0:01 xfwm4
```
:heavy_check_mark: Filtrar proceso por msfconsole
```
$ ps aux | grep msfconsole
$ mauricio    4758 80.2  2.3 757776 191928 pts/2   Sl+  13:27   0:04 ruby /usr/bin/msfconsole
```
>PDI de 3898

:heavy_check_mark: Cambio de prioridad de proceso
```
$ renice -n 10 -p 3898
```
>Esta consumiendo 2.3MB

:heavy_check_mark: Terminar proceso
```
$ kill 3898
```
:heavy_check_mark: Cron Job
>5 4 * * sun /home/mauricio/desktop/script.sh

Los 5 asteriscos
De izquierda a derecha, los asteriscos representan:
Minutos: de 0 a 59.
Horas: de 0 a 23.
Día del mes: de 1 a 31.
Mes: de 1 a 12.
Día de la semana: de 0 a 6, siendo 0 el domingo.

:heavy_check_mark: Creacion de script calendarizado.

```
$ touch script.sh
$ nano script.sh
$ #!/bin/bash

# our comment is here

echo "The current directory is:"

pwd

echo "The user logged in is:"

whoami
```
> damos persmisos
``` 
$ chmod +x ./script.sh
```
``` 
$ crontab -e
5 4 * * sun /home/mauricio/desktop/script.sh
```
>4:05 los domingos