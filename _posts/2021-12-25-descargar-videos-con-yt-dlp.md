---
layout: single
title: Descargar Videos con yt-dlp (Youtube-dl is deprecated)
excerpt: "Vamos a configurar yt-dlp en termux para descargar videos de youtube y otras platafoms de videos permitidos por esta herramienta. Debido a que youtube-dl esta obsoleto y no descarga a la velocidad normal por un concepto llamado Bandwidth throttling o el estrangulamiento del ancho de banda"
date: 2021-12-25
classes: wide
header:
  teaser: /assets/images/yt-dlp-videos/yt-1.png
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - Android
  - termux
  - scripts
tags:  
  - Android
  - Termux
  - Scripts
---
Vamos a configurar yt-dlp en termux para descargar videos de youtube y otras platafoms de videos permitidos por esta herramienta. Debido a que youtube-dl esta obsoleto y no descarga a la velocidad normal por un concepto llamado [__Bandwidth throttling__](https://en.wikipedia.org/wiki/Bandwidth_throttling) El estrangulamiento del ancho de banda consiste en la limitación de la velocidad de comunicación de los datos entrantes y / o en la limitación de la velocidad de los datos salientes en un nodo de red o en un dispositivo de red.

## Yt-dlp

yt-dlp es una fork de ‎‎youtube-dl‎‎ basada en el ahora inactivo ‎‎youtube-dlc.‎‎ El enfoque principal de este proyecto es agregar nuevas características y parches, al tiempo que se mantiene al día con el proyecto original. [ver](https://github.com/yt-dlp/yt-dlp)

![](/assets/images/yt-dlp-videos/yt-2.jpg) 

Los pasos para realizar la instalacion, son sencillamente faciles.

```bash
pkg update
pkg install python
pkg install ffmpeg
pkg install yt-dlp
```

Si ya tenemos instalados y deseamos actualizarlo usaremos los siguentes comandos.

```bash
python3 -m pip install --upgrade yt-dlp
python3 -m pip install -U yt-dlp
```
Ahora solo queda usar el comando yt-dlp y  pegar la URL del video que queramos descargar.

```bash
Usage: yt-dlp [OPTIONS] URL [URL...]
```
![](/assets/images/yt-dlp-videos/yt-3.jpg)

Pero muy aburrido, vamos a crearnos un script que al darle en compartir video nos permita descargar el video y ademas escoger la calidad del mismo.

```bash
  mkdir -p ~/.config/yt-dlp
  # Aqui pondremos la calidad y el tipo de extension que queremos descargar por default.
```
**config**

```bash
  #Le decimos que queremos descargar en mp4, en 1080p.
  -f bestvideo[height<=1080][ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best -o /data/data/com.termux/files/home/storage/shared/YouTube/%(title)s-%(uploader)s.%(ext)s --no-mtime --sponsorblock-remove all
```
**Creamos una carpeta en nuestra sdcard donde se descargara los videos**

```bash
mkdir -p ~/storage/shared/YouTube 
```
---

## Termux Url Opener

‎Finalmente crearemos un script que reciba la url (primer argumento)‎ cuando demos compartir con termux desde la aplicacion de youtube.

**termux-url-opener**

le damos permisos de ejecusion de archivos.

- chmod +x termux-url-opener

```bash
#!/bin/bash
url=$1
echo  "---——------------------------------------"
echo "script Edited by kidcode1"
echo "For audio only press 1"
echo "For video 360p press 2"
echo "For video 480p press 3"
echo "For video 720p press 4"
echo "For video 1080p press 5"
read option
command="-f mp4 -o /data/data/com.termux/files/home/storage/shared/YouTube/%(title)s-%(uploader)s.%(ext)s --no-mtime --sponsorblock-remove all"
comand5="-f bestvideo[height<=1080][ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best -o /data/data/com.termux/files/home/storage/shared/YouTube/%(title)s-%(uploader)s.%(ext)s --no-mtime --sponsorblock-remove all"
if [ "$option" -eq "1" ]; then
    echo "-f 133+140/296+140  $command" > $HOME/.config/yt-dlp/config
    yt-dlp $url
elif [ "$option" -eq "2" ]; then
    echo "-f 134+140/296+140 $command" > $HOME/.config/yt-dlp/config
    yt-dlp $url
elif [ "$option" -eq "3" ]; then
    echo "-f 135+140/297+140 $command" > $HOME/.config/yt-dlp/config
    yt-dlp $url
elif [ "$option" -eq "4" ]; then
    echo "-f 136+140/298+140 $command" > $HOME/.config/yt-dlp/config
    yt-dlp $url
elif [ "$option" -eq "5" ]; then
    echo "$comand5" > $HOME/.config/yt-dlp/config
    yt-dlp $url
fi
```

***Ahora ya podemos descargar el video pero antes escoger con que calidad de video deseamos descargar***

aun podemos mejorarlo, pero por el momento va bien.

![](/assets/images/yt-dlp-videos/yt-4.jpg)

Esperar a que finalice y disfrutar del video.

Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)