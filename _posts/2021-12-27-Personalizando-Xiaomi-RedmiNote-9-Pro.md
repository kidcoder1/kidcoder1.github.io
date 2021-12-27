---
layout: single
title: Personalizando Redmi 9 Pro
excerpt: "En este apartado estaremos personalizando el Xiaomi RedmiNote 9 Pro nombre en clave (joyeuse), con android 11, con la version de MIUI Global 12.5.2, vamos a desbloquear el bootloader, vamos a instalar (flashear) el recovery con el OrangeFox, Instalaremos las ROM desde el fastboot y recovery, y finalmente estaremos ganando acceso root con Magisk v23.0"
date: 2021-12-27
classes: wide
header:
  teaser: /assets/images/xiaomi-tools/xi-1.jpg
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
## Que es Bootloader

el Bootloader o gestor de arranque  realiza varias comprobaciones antes de iniciar el sistema operativo, cuando inicias un ordenador o smartphone, arrancará en primer lugar para ver que todo está en su sitio, que los componentes del sistema operativo son los que se supone que deberían ser, y que todo puede iniciarse de forma correcta. Y a continuación, hace de guía para que el sistema operativo sepa qué pasos tiene que dar durante el proceso de inicio.

## Desbloqueando el bootloader

Para desbloquear el bootloader necesitaremos una PC con Winows, un programa [Mi-Unlock](https://en.miui.com/unlock/download_en.html), cable USB y guardar todos los datos que se encuetra en el telefono ya que durante el proceso se borraran todos los datos.

## Activar el modo desarrollador 

vamos a ajustes del telefono, acerca del telefono, todas las especificaciones y en version Miui precionamos varias veces hasta que salga un mensaje que indica que y eres desarrollador.

![](/assets/images/xiaomi-tools/xi-3.jfif)


Nuevamente vamos hasta ajustes de telefono, ajustes adicionales, opciones de desarrollador, y activamos al opcion desboqueo OEM y  depuracion USB.

![](/assets/images/xiaomi-tools/xi-4.jfif) 

Instalamos el programa Mi-Unlock, conectamos nuestro telefono en modo fastboot.

Para iniciar el telefono en fastboot, le damos en reiniciar y precionamos el boton volumen menos hasta que aparezca el logo de android.

![](/assets/images/xiaomi-tools/xi-6.jpg)

Una vez conectado el telefono a la PC, precioamos en refresh (F5) del Mi-unlock, si vemos la serie del telefono, todo esta bien, solo queda precionar en Unlock(F6), y como muestra el mensaje esperar 168 horas para volver hacer el mismo paso.

![](/assets/images/xiaomi-tools/xi-7.jpg)

se recomienda, no usar la aplicacion Limpiador durante los 7 dias, para no borrar la cache o temporales de conteo, ni insistir antes de que se cumpla las 168 horas o se empezara a contar desde cero otra vez.

![](/assets/images/xiaomi-tools/xi-8.jfif)

```
Pasado los 168 ya podremos desbloquear, los mismos pasos anteriores.
```

![](/assets/images/xiaomi-tools/xi-8.jpg)


Listo!! ya tenemos desbloqueado el xioami.

# Instalar (Flashear) Recovery

Ya teniendo desbloqueado el bootloader, y habilitado la depuracion USB.

- Vamos a descargar el recovery [OrangeFox-miatoll-stable](https://github.com/kidcoder1/xiaomi-tools/raw/master/OrangeFox-miatoll-stable%40R11.1_2.zip).

- Tambien descargamos [ADB Tools](https://dl.google.com/android/repository/platform-tools-latest-windows.zip) o desde la pagina [Oficial android MTK](https://androidmtk.com/download-minimal-adb-and-fastboot-tool)

- Otra herramienta que automatiza todo el proceso de instalacion de recovery, descargar ROMs y hacer root es [XiaoMiTool](https://www.xiaomitool.com/V2/).

## Flashear la recovery con ADB Tools

Para los que ya estan familiarizados con  las herramientas ADB, vamos a descomprimir la ADB Tools, y guardar la recovery.img en la misma carpeta.

![](/assets/images/xiaomi-tools/xi-9.jpg)

Pero si no queremos complicarnos la vida descargamos la XiaoMiTool y la instalamos como cualquier otro programa. Iniciamos el programa y automtimente descargara los drivers necesarios para que funcione sin problemas (si nos pregunta por nuestra region elegimos **Global**). 

Elegimos la primera opcion, "Dispositivo funcionando normalmente, quiero modificarlo", 

![](/assets/images/xiaomi-tools/xi-10.jpg)

Precionamos en seleccionar, y automaticamente reiniciara nuestro dispositivo en modo fastboot. 

![](/assets/images/xiaomi-tools/xi-11.jpg)

Para este caso no encuentra la recovery apropiada, pero recuerda nosotros vamos a instalar la **OrangeFox-miatoll-stable@R11.1_2** el cual ya tenemos descargada. por lo que elegimos recuperacion personalizada. [OrangeFox Web Offical](https://orangefox.download/es-ES)

![](/assets/images/xiaomi-tools/xi-12.jpg)

Nos pide que presionemos y seleccionamos el archivo recovery en el recuadro, como anteriormente guardamos la recovery en la carpeta del ADB-Tools, seleccionamos el recovery.img y presionamos continuar.

![](/assets/images/xiaomi-tools/xi-13.jpg)

Saldra una advertencia indicando que se perdera los datos que se encuentra en sdcard (ya les digo no se pierde ningun dato), como ya salvamos nuestros datos precionamos en continuar y saldra la pantalla que toda la instalacion se ha completado exitosamente, el telefono reiniciara en modo recovery. 

![](/assets/images/xiaomi-tools/xi-14.jpg)

Para los siguientes veces que queramos iniciar el recovery boton apagar (lector de huellas), reiniciar dispositivo y precionamos boton volumen mas (+), hasta ver la pantalla de recovery.

![](/assets/images/xiaomi-tools/xi-15.jpg)

# Ganando acceso root al xiaomi

Para ganar acceso root, necesitaremos iniciar nuestro en modo recovery, reiniciar y mantener precioando boton volumen mas (+).

- Descargamos el magisk para este caso he usado la version 23. [Magisk Github](https://github.com/topjohnwu/Magisk/releases), vamos a necesitar el .zip pero solo vemos el .apk, facil hay que cambiarlo la extension.

- Tambien necesitaremos el safety-fix-v2.1.1.zip [here](https://github.com/kidcoder1/xiaomi-tools/raw/master/safetynet-fix-v2.1.1.zip)

![](/assets/images/xiaomi-tools/xi-16.jfif)

Desde el recovery seleccionamos magisk-v23.0.zip, arrastramos el pestillo para que se flashee con el magisk.

![](/assets/images/xiaomi-tools/xi-17.jfif)

Reiniciamos el telefono, e instalamos magisk-v23.0.apk,
desde la aplicacion de magisk ingresamos a los modulos e instalamos los siguientes archivos.

![](/assets/images/xiaomi-tools/xi-18.jfif)

Instalar en el siguiente orden.

- Busybox_for_android_NDK.1.34.1.zip
- Riru-v26.1.3.r513.zip

- Safetynet-fix-v2.1.1.zip  

Este ultimo, ya tenemos descargado y seleccionamos instalar desde almacenamiento.

Finalmente, vamos a ajustes y activamos la opcion MagiskHide.

![](/assets/images/xiaomi-tools/xi-19.jfif)

Eso es todo. y para instalar las rom de xiaomi podemos usar el programa.

- [XiaoMiFlash](https://www.xiaomiflash.com/)
- [Xiaomi Stock Rom RedmiNote 9 Pro](https://xiaomistockrom.com/xiaomi-redmi-note-9-pro) 
- [Redmi Note 9 Pro Global](https://xiaomifirmwareupdater.com/miui/joyeuse/stable/V12.5.2.0.RJZMIXM/)
- [xiaomi.ue](https://xiaomi.eu/community/threads/twrp-orangefox-pitchblack-recovery-for-redmi-note-9-pro-joyeuse.56896/), este se instala desde el recovery.

Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)