---
layout: single
title: Uso de Sudo en Windows
excerpt: "Uso de gsudo o simplemente sudo es una experiencia de usuario similar a la del sudo original de Unix/Linux. Le permite ejecutar un comando (o reiniciar su shell actual) con permisos elevados. Aparecerá una ventana emergente de UAC cada vez ello pudiendo cambiar para ver menos la cache de gsudo. "
date: 2025-02-08
classes: wide
header:
  teaser: /assets/images/sudo-windows/000.jpg
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - windows
  - custom
tags:  
  - windows
  - custom
---

## Usando sudo en windows

Es similar a usar el comando runas /user:admin en Windows. Ambos comandos permiten ejecutar un proceso con privilegios de administrador.

- El comando sudo permite a los usuarios ejecutar comandos que normalmente requieren privilegios de superusuario. 

- El comando runas permite ejecutar programas como cualquier usuario, incluido el administrador. 

 Indicar que este comando ya viene por defecto en windows 11, solo necesita activarlo en las confiduraciones de windows. para los que aun vivimos con la windows 10 que se va, pero seguiremos usandola un rato mas.

 la forma de usarla es muy facil.

 ```zsh
 sudogsudo { ScriptBlock }
 ```
![](/assets\images\sudo-windows/001.jpg)

 al anteponer sudo a un comando a ejecutar nos saltara el UAC de windows, damos el permiso y ya ejecutaremos con privilegios de adminstrdor.

![](/assets\images\sudo-windows/003.jpg)
 
 Tambien podemos personalizar el gsudo o sudo a nuestro gusto.

![](/assets\images\sudo-windows/004.jpg)

## Instalacion.

POdemos usar algunos de los administrador de paquetes que tenemos instalado.

- Usando la cuchara: **scoop install gsudo**
- Uso de WinGet: **winget install gerardog.gsudo**
- Uso de chocolate: **choco install gsudo**

Para mas informacion visitemos la pagina del creador en Github.
[ __Gerardog
Gerardo Grignoli__ ](https://github.com/gerardog/gsudo.git)


¡Eso es todo nos vemos en Youtube!


Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)