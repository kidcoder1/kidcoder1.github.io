---
layout: single
title: Restablecer Password de Root en Maquinas Virtuales Linux
excerpt: "Alguna vez te ha pasado que estas trabajando con maquinas virtules, y se te olvida la contraseña para ingresar a la maquina, aprenderremos a restablecer la contraseña de root a travez de una shell con Grub.
restablecer la password de root, dejarla en blanco o cualquier otra acción privilegiada como acceder a los volúmenes del sistema para realizar un volcado o copia de los ficheros /etc/passwd y /etc/shadow con el fin de realizar un cracking de contraseñas por fuerza bruta a sus hashe. "
date: 2025-02-08
classes: wide
header:
  teaser: /assets/images/change-passwd-linux/000.jpg
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - Linux
  - custom
tags: 
  - Linux
  - custom
---
Simplemente es una funcionalidad estándar del kernel de Linux que permite a los administradores de sistemas entrar en un modo a una consola interactiva para poder recuperar un sistema de ficheros dañado o una contraseña olvidada.

En el momento que inicia una maquina se despliega el menu del Grub.

![](/assets/images/change-passwd-linux/001.jpg)

Presionando la tecla "e" podemos editar Grub. Localizamos un línea similar a "linux /boot/vmlinuz-VERSION-generic root=UUID=IDENTIFICADOR ro single disc_ucode_ldr" modificamos ro (solo lectura) por rw (lectura y escritura) y añadimos al final "init=/bin/bash".

![](/assets/images/change-passwd-linux/002.jpg)

Luego de realizar los cambios deberia quedar de la siguiente manera.

![](/assets/images/change-passwd-linux/003.jpg)

 Finalmente guardamos y salimos con "Ctrl-x". Esto reiniciará el sistema y nos levantará una shell privilegiada en un contexto de root.

```bash
init=/bin/bash: Indica al kernel de Linux que ejecute /bin/bash como init, en lugar de ejecutar init como sistema.
```
Después de reiniciar se levantará una terminal en un contexto de root. Podremos restablecer la password y establecer una nueva con el comando passwd o realizar cualquier acción privilegiada.

![](/assets/images/change-passwd-linux/004.jpg)

Y ya esta la proxima vez que iniciamos Linux los loguearemos con nuestra passwd que cambiamos.

## ¿Cómo evitar y protegerse de esta técnica?

Establecer una password en el Grub es la opción más sencilla y segura. Creamos una password tipo PBKDF2 (Password-Based Key Derivation Function 2) que caracteriza por reducir ataques de fuerza bruta. 

Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)