---
layout: single
title: Configuracion Personalizada del Simbolo del Sistema Windows
excerpt: "Ya en un apartado aprendimos a configurar powershell haciendo uso de Oh-My-Posh, hoy vamos a configurar para el terminal en cmd.exe al estilo de los que usan linux con personalizaciones de shell como ***Oh-My-ZSH*** u ***Oh-My-Fish***, que nos permite hacer que nuestra día a día sea un poco más amigable en ese lugar donde pasamos tanto tiempo conectados ejecutando nuestros comandos favoritos"
date: 2023-02-19
classes: wide
header:
  teaser: /assets/images/personalizando-cmd/cmd0.jpg
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - windows
  - scripts
  - custom
tags:  
  - windows
  - script
  - custom
---
## Configuracion Personalizada del Simbolo del Sistema Windows

En este apartado aprenderemos a configurar el simbolo cmd.exe de windows, para convertirlo semenjante al terminal en linux al estilo oh-my-zsh o oh-my-fish, configuraremos el prompt con autocompletado, resaltado sintactico, resaltado de errores. 

Para hacer uso de los comandos de Linux instalaremos el programa cygwin, y para emular los efectod de szh haremos uso de un repositorio en github de clink, indicar que esto va actualizandose constantemente.

## Binarios de Linux
 
  vamos a descargar los binarios que se usan en linux de la pagina [cygwin](https://www.cygwin.com/setup-x86_64.exe)

  ![](/assets/images/personalizando-cmd/cmd1.png)

  luego vamos de descargar el programa vamos a instalarlo, todo por default, todo siguiente.

  ![](/assets/images/personalizando-cmd/cmd2.jpeg)

  Al instalarlo nos creara una carpeta llamada cygwin64 en la raiz del disco C:/

![](/assets/images/personalizando-cmd/cmd3.jpeg)

En la siguinte opcion escogemos la opcion full, para que nos descargue todos los binarios usados en linux.

![](/assets/images/personalizando-cmd/cmd4.jpeg)

Esperamos a que se descargue todo de internet.

![](/assets/images/personalizando-cmd/cmd5.jpeg)

Finalmente creara un acceso directo para abrir su propio terminal de Cywin, porsupuesto que no usaremos esa, vamos hacer uso de la nativa que viene con windows o puedes optar por windows terminal descargado de microsoft store

![](/assets/images/personalizando-cmd/cmd6.jpeg)

Ahora nos dirigimos a la raiz del disco C:/ para localizar la carpeta Cygwin64 y en la carpeta bin estan los binarios que usaremos.

![](/assets/images/personalizando-cmd/cmd7.jpeg)

Pero para usar los binarios necesitamos agregar a nuestra Path. Vamos a inicio y editar variables de entorno.

![](/assets/images/personalizando-cmd/cmd8.jpeg)

En la opcion path vamo agregar una entrada mas, que apunte a nuestro binario.

![](/assets/images/personalizando-cmd/cmd9.jpeg)

Como se puede observar en esta imagen.

![](/assets/images/personalizando-cmd/cmd10.jpeg)

En este punto ya podremos usar los comandos de linux, como el ***ls*** o ***grep***, pero nuestra terminal sigue manteniendo las letras blancas con fondo negro.

Para solucionarlo vamos a crearnos un script en .bat, que lo guardaremos donde estan los binarios de Linux, en C:/Cywin64/bin con el nombre aliases.bat 

```ruby
#aliases.bat
@ECHO OFF
doskey ls=ls --color $*
```
Y a este archivo se ejecutara como una tarea programada cada dez que abramos la terminal para ello lo llamaremos desde el registro de windows en la siguiente ruta. La entrada sera de tipo REG_SZ llamado AutoRun.

En informacion de valor escribimos.

```java
cls && aliases.bat
```
![](/assets/images/personalizando-cmd/cmd11.jpeg)

Ahora si la hace ls ya tenemos algo mas parecido a la terminal de linux en nuestra cmd.exe con los colores

![](/assets/images/personalizando-cmd/cmd12.jpeg)

Pero si nos acercamos un poco mas a Linux, pedemos moficicar muestra prompt clasica [Custom prompt](https://github.com/jersonmartinez/Curso_Administracion_Windows_Consola/blob/master/10.
%20Gesti%C3%B3n%20del%20PROMPT.md)

- Podemos usar los siguientes comandos.

```bash
> setx prompt ░▒▓$S$T$H$H$H$S▓▒░$S░▒▓$S$P$S▓▒░$S   ----> esto establece tu prompt

> PROMPT "$_$e[0;1;44mN$e[1;30;47mI$e[0;1;44mC$E[35;40m $d$s$t$h$h$h$h$h$h$_$E[1;33;40m$p$_$E[0;0m~$g$s"

> echo %prompt%  -----> esto es para ver valor de la prompt actual
```
Ahora esta un poco mas personalizado

![](/assets/images/personalizando-cmd/cmd13.jpeg)

## Configurando CLINK

Clink combina el shell cmd.exe nativo de Windows con las potentes funciones de edición de línea de comandos de la biblioteca GNU Readline, que proporciona completas funciones de finalización, historial y edición de línea. Readline es mejor conocido por su uso en el shell Bash de Unix, el shell estándar para Mac OS X y muchas distribuciones de Linux. [Clink](https://github.com/chrisant996/clink).

vamos a descargar y extraerlo. [descargar](https://github.com/chrisant996/clink/releases/download/v1.4.19/clink.1.4.19.57e404.zip)

![](/assets/images/personalizando-cmd/cmd14.jpeg)

Vamos a utilizar estos binarios,para ello e ir mas ordenado, he creado una carpeta en la raiz del disco y movido la carpeta alli.

![](/assets/images/personalizando-cmd/cmd15.jpeg)

Luego procedo a gregar esta ruta a mi PATH para llamarlos desde cualquier lugar de la consola, para no olvidarme cree un especie de alias, una copia de clink_x64 con el nombre linux, esto para llamarlo mas facilmente

![](/assets/images/personalizando-cmd/cmd16.jpeg)

A partir desde este momento solo queda configurar clink para que se inicie automaticamente y configurarlo a nuestro gusto.

- para activar clink automaticamente al iniciar cmd.exe

```ruby
C:\Users\Kidcode1>linux autorun install
```
- luego activamos el autostart a true

```ruby
C:\Users\Kidcode1>linux set clink.autostart true
```

- pero no me gusta ver el banner de clink y lo ponemos en off
  
```ruby
C:\Users\Kidcode1>linux set clink.logo none
```
- para activar el autosuggest le indicamos con el comando

```ruby
C:\Users\Kidcode1>linux set autosuggest.enable true
```
- para aplica color cuando el comando es un ejecutable

```ruby
C:\Users\Kidcode1>linux set color.executable sgr 38;5;32
```
- para aplicar color cuando el comando no es reconocido

```ruby
C:\Users\Kidcode1>linux set color.unrecognized sgr 38;5;203
```
![](/assets/images/personalizando-cmd/cmd17.jpg)


Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)