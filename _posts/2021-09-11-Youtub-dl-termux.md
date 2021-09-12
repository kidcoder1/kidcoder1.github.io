---
layout: single
title: Instalando Youtube-dl en Termux
excerpt: "youtube-dl es un programa de línea de comandos para descargar vídeos o extraer audio de sitios de streaming tales como YouTube, Dailymotion o Vimeo. El programa está escrito en Python, por lo que es multiplataforma, pudiéndose ejecutar en cualquier sistema con Python"
date: 2021-09-11
classes: wide
header:
  teaser: /assets/images/post-youtube-dl-termux/you-dl.png
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - Termux
  - Android
  - Linux
tags:  
  - zsh
  - linux
  - python
---
Youtube-dl es un programa de línea de comandos para descargar vídeos o extraer audio de sitios de streaming tales como YouTube, Dailymotion o Vimeo. El programa está escrito en Python, por lo que es multiplataforma, pudiéndose ejecutar en cualquier sistema con Python.

![](/assets/images/post-youtube-dl-termux/y1.jfif) 

## Actualizamos e Instalamos las Dependencias de Termux - Instalamos python

```
apt update -y
apt upgrade -y
apt install python -y 
pip install youtube-dl
```

## Verificamos la version de Youtube-dl instalada

![](/assets/images/post-youtube-dl-termux/y2.jfif)

## Comandos u opciones para descargar

```bash
# Descarga Basica:
youtube-dl URL

# Descargar Lista en una carpeta, y ordenarlos:
youtube-dl -o '%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s' URL

# Download playlist starting from certain video:
youtube-dl --playlist-start 5 example.com/watch?v=id&list=listid
```

En este punto tendriamos que escribir youtube-dl URL, muy comlicado y perdida de tiempo, es mas facil poner compartir seleccionar termux.

![](/assets/images/post-youtube-dl-termux/y3.jfif)

## Aun falta agregar unos scripts

Si ponemos compartir con termux desde youtube (que es la forma mas facil de descargar cualquier video de youtube, por ejemplo), aun no funcionara por que no le indicamos a youtube-dl que url debe tomar como parametro y donde descargarlo y en que resolucion de video deseamos descargarlo.

![](/assets/images/post-youtube-dl-termux/y4.jfif)

Nos indica que debemos crear un script en la siguiente ruta $HOME/bin/termux-url-opener, entonces este script tendra el siguiente contenido (usare el editor de texto nano para escribir codigo)

```zsh
mkdir $HOME/bin
nano termux-url-opener
```
___

```bash
#!/bin/bash
# Copyright 2017 Gabi Tiplea

echo "Copyright 2017 Gabi Tiplea"
echo "For audio only press 1"
echo "For video 360p press 2"
echo "For video 480p press 3"
echo "For video 720p press 4"
echo "For video 1080p press 5"
read option
command='-no-mtime -o /data/data/com.termux/files/home/storage/shared/Youtube/%(title)s.%(ext)s -f'
if [ "$option" -eq "1" ]; then
    echo "$command 140" > $HOME/.config/youtube-dl/config
    youtube-dl $1
elif [ "$option" -eq "2" ]; then
    echo "$command \"best[height<=360]\"" > $HOME/.config/youtube-dl/config
    youtube-dl $1
elif [ "$option" -eq "3" ]; then
    echo "$command \"best[height<=480]\"" > $HOME/.config/youtube-dl/config
    youtube-dl $1
elif [ "$option" -eq "4" ]; then
    echo "$command \"best[height<=720]\"" > $HOME/.config/youtube-dl/config
    youtube-dl $1
elif [ "$option" -eq "5" ]; then
    echo "$command \"best[height<=1080]\"" > $HOME/.config/youtube-dl/config
    youtube-dl $1
fi
```
Aparte de ello para que funcione nuestro script, necesitamos crear otros lineas de codigo mas en la siguiente ruta.

~~~
mkdir $HOME/.config/youtube-dl
nano config 
~~~

```bash
-no-mtime -o /data/data/com.termux/files/home/storage/shared/Youtube/%(title)s.%(ext)s -f "best[height<=720]"
```

ahora al dar en compatir con termux, ya podemos descargar de forma facil y eligiendo la calidad de video que queramos descargar no solo de youtube, sino de cualquier pagina que tenga la opcion compartir.

![](/assets/images/post-youtube-dl-termux/y5.jfif)

Tambien puedes verlo en mi canal [ __Youtube__ ](#)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)