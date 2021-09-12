---
layout: single
title: Cheat Sheet Termux
date: 2021-09-11
classes: wide
header:
  teaser: /assets/images/slae32.png
categories:
  - android
  - termux
tags:
  - bash
  - zsh
---

Veremos los comandos mas utlizados en termux, de forma mas constante.

> Desde mi punto de vista - kidcode1.

## 1: Termux extra keys

La solución a este problema solo es escribir esto en la terminal.

```bash
mkdir $HOME/.termux/ ;echo "extra-keys = [['ESC','/','-','HOME','UP','END','PGUP'],['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN']]" >> $HOME/.termux/termux.properties
```

ya queda reiniciar termux, ya tienes teclas de acceso rapido, que te ayudaran a agilizar tus trabajos.

## 2: CONFIGURANDO TERMUX CON UNA SOLA INSTRUCCION

Bueno amigos aquí les pondré de una forma breve que comando en termux usaran para dejar instalados todos los paquetes necesarios para el uso básico de esta gran utilería que es TERMUX.

```bash
----------------
$  apt install util-linux coreutils vim python python2 ruby perl clang curl wget make openssl php zip unzip tar htop bison findutils git apr apr-util libtool pkg-config tmux termux-tools ncurses-utils ncurses postgresql termux-elf-cleaner openssl-tool
-----------------
```

Con esta instrucción y parametros estoy indicando a TERMUX  que instale los paquetes

1. util linux
2. python
3. python2
4. Ruby
5. Perl
6. clang
7. curl
8. php
9. zip  unzip
  

y muchas mas.... con esto nos evitamos estar instalando una a una......  ;)

## 3. Crear servidor ngrok

primero debes crear un servidor local, con -t apunta la ubicacion donde se encuentra tu ptoyecto (carpeta)
```
php -S 192.168.1.68:4433 -t $PREFIX/var/service/php > /dev/null 2>&
```

luego conecta el ngrok con el mismo puerto del servidor local.

```
./ngrok http 4433
```

## 4. Cambiar banner de termux

```
 ################################### ..IMAGE TO ASCII CONVERT.. Link : 
 
 https://linksad.net/RKA3 
 
 ################################### 

 # ASCII Website ................................. 
 
  https://www.asciiworld.com )
  
  ===================================( Crazy-Banner #####################################
 
https://github.com/Bhai4You/Crazy-Banner.git

```
> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)