---
layout: single
title: Personalizando Termux
excerpt: "¿Te gustaría aprender a personalizelar tu term, para sistemas operativos tipo unix?ux para un entorno mas agradable, y facil de usarlo, haremos uso la Shell Oh-My-Zsh,  cual es un potente interprete de comandos, toma asiento que te lo explico."
date: 2021-09-11
classes: wide
header:
  teaser: /assets/images/personalizando-termux/t1.jpg
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - Termux
  - Android
  - Linux
tags:  
  - zsh
  - linux
  - bash
---
Termux es, en definitiva, un emulador de terminal para nuestro Android que nos permitirá , por medio de una shell, la ejecución de comandos Linux.

![](/assets/images/personalizando-termux/t1.jpg) 

## Dar Permisos para Uso de la SDcard

```
termux-setup-storage
```

## Actualizamos las dependencias de Termux

Actualizamos e instalamos los paquetes disponibles para termux.
```
apt update -y
apt upgrade -y
```

## Instalamos Ruby

El lenguaje Ruby se utiliza principalmente en el desarrollo de aplicaciones web, pero también se puede utilizar para desarrollar otro tipo de aplicaciones de software, Este lenguaje está disponible en plataformas como Windows, Linux y muchas otras.

```
apt install ruby -y
gem install lolcat --(le da color a cualquier cosa del terminal)
apt-get install cowsay figlet fortune -y
```
Vamos a editar el archivo motd, que se encuentra en la ruta ../usr/etc, pademos hacer uso de editor de texto vim o nano (sino lo tienes instalado puedes instalarlo con apt install nano vim).

```
cd ../usr/etc
mv motd motd-bk (no lo elimino, por si queremos recuperarlo)
```

En la misma carpeta editamos el archivo bash.basrc (usare el editor de texto vim)

![](/assets/images/personalizando-termux/t2.jpg)

y como resultado obtendremos, un terminal mas personalizado

![](/assets/images/personalizando-termux/t3.jpg)

...Pero podemos hacer aun mas amigable nuestro terminal. Vamos a instalar la shell zsh

```bash
apt install zsh -y
apt install git -y (para poder clonar los scripts a usar del zsh)
apt install curl (para las peticiones del prgrama)
```

Volvemos a HOME, y nos clonamos el script para instalar el zsh.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

Vamos a editar el archivo ~/.zshrc, hare uso de vim. buscamos la linea donde dice plugins=(git )

![](/assets/images/personalizando-termux/t4.jpg)

y pegamos la siguiente linea.

```bash
zsh-autosuggestions zsh-syntax-highlighting
```
![](/assets/images/personalizando-termux/t5.jpg)

Listo!! ya casi finalizamos.

![](/assets/images/personalizando-termux/t6.jpg)

l abrir nueva ventana de termux, podemos ver que la terminal nos indica con rojo si escribimos un comando que no existe, y tiene un historial de los ultimos comandos utilizados.

Tambien puedes verlo en mi canal [__Youtube__](#)

¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)