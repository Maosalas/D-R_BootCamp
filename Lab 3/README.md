# Variables de entorno

:heavy_check_mark: Visualizar las variables de entorno

```
 $ printenv
 COLORFGBG=15;0
COLORTERM=truecolor
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
DESKTOP_SESSION=lightdm-xsession
DISPLAY=:0.0
GDMSESSION=lightdm-xsession
GDM_LANG=en_US.utf8
HOME=/home/mauricio
LANG=en_US.UTF-8
LANGUAGE=
LOGNAME=mauricio
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games
PWD=/home/mauricio
QT_ACCESSIBILITY=1
QT_AUTO_SCREEN_SCALE_FACTOR=0
QT_QPA_PLATFORMTHEME=qt5ct
SESSION_MANAGER=local/mao:@/tmp/.ICE-unix/839,unix/mao:/tmp/.ICE-unix/839
SHELL=/usr/bin/zsh
SSH_AGENT_PID=882
SSH_AUTH_SOCK=/tmp/ssh-aMLN7gVDZeeV/agent.839
TERM=xterm-256color
USER=mauricio
WINDOWID=0
XAUTHORITY=/home/mauricio/.Xauthority
XDG_CONFIG_DIRS=/etc/xdg
XDG_CURRENT_DESKTOP=XFCE
XDG_DATA_DIRS=/usr/share/xfce4:/usr/local/share/:/usr/share/:/usr/share
XDG_GREETER_DATA_DIR=/var/lib/lightdm/data/mauricio
XDG_MENU_PREFIX=xfce-
XDG_RUNTIME_DIR=/run/user/1000
XDG_SEAT=seat0
XDG_SEAT_PATH=/org/freedesktop/DisplayManager/Seat0
XDG_SESSION_CLASS=user
XDG_SESSION_DESKTOP=lightdm-xsession
XDG_SESSION_ID=2
XDG_SESSION_PATH=/org/freedesktop/DisplayManager/Session0
XDG_SESSION_TYPE=x11
XDG_VTNR=7
_JAVA_OPTIONS=-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
SHLVL=1
OLDPWD=/home/mauricio
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
LESS_TERMCAP_mb=
LESS_TERMCAP_md=                                                                                                                                  
LESS_TERMCAP_me=                                                                                                                                  
LESS_TERMCAP_so=
LESS_TERMCAP_se=                                                                                                                                  
LESS_TERMCAP_us=
LESS_TERMCAP_ue=                                                                                                                                  
_=/usr/bin/printenv
```

:heavy_check_mark: Filtrar por BASH_ALIASES

```
$ printenv | grep BASH_ALIASES

```

:heavy_check_mark: Incluir el path de masscan como variable de entorno

```
$ MAS_VAR='/home/mauricio/Desktop/Masscan_D-R/masscan/bin/masscan'
$ set | grep MAS_VAR
$ MAS_VAR='/home/mauricio/Desktop/Masscan_D-R/masscan/bin/masscan'
$ export MAS_VAR
$ printenv | grep MAS_VAR
$ MAS_VAR='/home/mauricio/Desktop/Masscan_D-R/masscan/bin/masscan'
```
:heavy_check_mark: Incluir una variable de entorno permanente

```
$ sudo nano /etc/enviroment
$ MAS_VAR=SYSADMIT
```

:heavy_check_mark: Cambiar el prompt del shell por "World Best Hacker"

> Primero creamos un backup del archivo ~/.bashrc

``
$ cp ~/.bashrc ~/.bashrc.bak
```

> Despues abrimos el archivo para modificarlo

```
$ sudo nano ~/.bashrc
$ PS1='World Best Hacker> '
```



# Bash Sript

:heavy_check_mark: Realiza un script que permita tomar los puertos a escanear

```
$ touch puertos.txt
$ nano puertos.txt
$ cat puertos.txt | sed -e "s/:/ /" | while read ip port
    do
    nmap -sS $ip -p $port -oN 'Nmap'$port -T4   
    done

```

:heavy_check_mark: Scan a la direccion ip de Metasploitable y envia a una extension grep

```
$ nmap -sS 192.168.240.130 -p- -oG output -T4
```

> -oG salida grepeable, "Esta obsoleto"

:heavy_check_mark: Fuera del script filtre al puerto 80

```
$ cat output| grep 80/open > grepPort80.txt
```

:heavy_check_mark: Fuera del script cuente los puertos abiertos

```
$ awk '/^Host: / && /Ports: / { num=gsub("/open/", ""); print $2, "-", num }' < ./output

```

:heavy_check_mark: Comprime el archivo de salida en formato .tar.gz

```
$ tar -czvf grep.tar.gz ./

```

:heavy_check_mark: Incluye los 3 ultimos pasos dentro del script

```
$ cat puertos.txt | sed -e "s/:/ /" | while read ip port
    do
    nmap -sS $ip -p $port -oN 'Nmap'$port -T4   
    done

    nmap -sS 192.168.240.130 -p- -oG output -T4
    cat output| grep 80/open > grepPort80.txt
    tar -czvf scriptsOutputs.tar.gz ./ 

```

:heavy_check_mark: Descomprima el archivo 

```
$ tar -xzvf scriptsOutputs.tar.gz
```

# Storage and Device Management

:heavy_check_mark: Listar particiones

```
$ df -h  
```

:heavy_check_mark: Conectar una usb y montarla a un directorio

:heavy_check_mark: Crear el directorio para montar el usb
```
$ mkdir /media/usb
```
:heavy_check_mark: Identificar el nombre de la unidad
```
$ ls -l /dev/sd*
```

:heavy_check_mark: Montar la memorio usb
> Nota, si el usb esta en FAT
```
$ mount -t vfat /dev/sdb1 /media/usb
```

:heavy_check_mark: Montar la memorio usb
> Nota, si el usb esta en NTFS
```
$ mount -t ntfs-3g /dev/sdb1 /media/usb
```

:heavy_check_mark: Montar la memorio usb
> Nota, si el usb esta en NTFS
```
$ mount -t ntfs-3g /dev/sdb1 /media/usb
```

:heavy_check_mark: Montar la memorio usb
> Nota, si el usb esta en ext4
```
$ mount -t ext4 /dev/sdb1 /media/usb
```

:heavy_check_mark: Validamos el espacio disponible

```
$ df -h  
```

:heavy_check_mark: Desmontamos el USB

```
$ umount /media/usb 
```

# Logging

:heavy_check_mark: Que es rsyslog?

Se encarga de implementar el protocolo de syslog básico, lo extiende con filtrado basado en un contenido dado, con capacidades de filtrado enriquecido, opciones de configuración flexibles y agrega características como uso de TCP para el transporte.

:heavy_check_mark: Donde se encuentra el archivo de configuración de rsyslog?
```
$ /etc/rsyslog.conf
```

:heavy_check_mark: Que es logrotate?

Esta utilidad en linux nos permite rotar, comprimir y renovar los ficheros de log de forma automatizada.

:heavy_check_mark: Intenta hacer sudo con un usuario que no este en sudoers

>No se puede

:heavy_check_mark: Ingresa mal la contraseña de un user que este en sudoers

>Indica que la contraseña está mal ingresada


# Transferencia de archivos

:heavy_check_mark: Crea un archivo en kali

```
$ touch toMTSP.txt
```

:heavy_check_mark: Transfiere el archivo mediante scp a Metasploitable

```
$ scp ./toMTSP.txt msfadmin@192.168.240.130:/home/msfadmin
```
:heavy_check_mark: Transfiere el archivo mediante FTP a Metasploitable

```
$ ftp 192.168.240.130
$ msfadmin
$ msfadmin
$ put <nombreArchivo>
```

:heavy_check_mark: Transfiere el archivo mediante tFTP a Metasploitable
>No hay puerto de escucha