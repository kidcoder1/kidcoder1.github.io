---
layout: single
title: Como acceder a nuestro localhost desde cualquier lugar
excerpt: "Veremos como podemos acceder a nuestro localhost desde cualquier parte utilizando [__ngrok__](https://ngrok.com/), y [__localhost.run__](http://localhost.run/), y todo lo haremos de windows, utilizando xamp para nuestro servidor web localhost"
date: 2021-09-21
classes: wide
header:
  teaser: /assets/images/acceder-a-locolhost/img1.jfif
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - Windows
  - Xamp
  - Web
tags:  
  - Windows
  - Xamp
  - Web
---
Veremos como podemos acceder a nuestro localhost desde cualquier parte utilizando [__ngrok__](https://ngrok.com/), y [__localhost.run__](http://localhost.run/), y todo lo haremos de windows, utilizando xamp para nuestro servidor web localhost.

## Ngrok

ngrok nos permite exponer a internet una URL generada dinámicamente, la cual apunta a un servicio web que se está ejecutando en nuestra máquina local

![](/assets/images/acceder-a-locolhost/img2.jpg) 

Una vez iniciado session en la pagina de [__ngrok__](https://ngrok.com/), ponemos nuestro token que copiamos de la pagina de **ngrok** y podemos ver nuestro archivo de configuracion en formato yaml con el token que pusimos.

```
ngrok.exe authtoken <YOUR_AUTHTOKEN>
```
![](/assets/images/acceder-a-locolhost/img3.jpg)

Ya podemos ejecutar ngrok con todas las opciones.

```bash
EXAMPLES:
    ngrok http 80                    # secure public URL for port 80 web server
    ngrok http -subdomain=baz 8080   # port 8080 available at baz.ngrok.io
    ngrok http foo.dev:80            # tunnel to host:port instead of localhost
    ngrok http https://localhost     # expose a local https server
    ngrok tcp 22                     # tunnel arbitrary TCP traffic to port 22
    ngrok tls -hostname=foo.com 443  # TLS traffic for foo.com to port 443
    ngrok start foo bar baz          # start tunnels from the configuration file

VERSION:
   2.3.40
```
---

## Localhost.run

‎El reenvío de puertos o asignación de puertos es una aplicación de traducción de direcciones de red que redirige una solicitud de comunicación de una combinación de dirección y número de puerto a otra mientras los paquetes atraviesan una puerta de enlace de red, como un enrutador o firewall.‎

Localhost.run ‎se puede utilizar sin registrarse sólo tiene que llamar a un simple comando en su terminal‎.

```bash
ssh -R 80:localhost:80 localhost.run
```
Esperen pero ssh no viene por defecto en windows, eso vamos a solucioanrlo instalando  **openssh** y lo vamos hacer de una forma sencilla de la siguiente manera, la mejor manera con **chocolatey**.

## Instalando Cholatey

Vamos a instalar desde powershell con privilegios de administrador [__pasos a seguir__](https://chocolatey.org/install), chocolatey es un instalador de paquetes de linea de comandos paa windows como apt, pkg o dpkg de ubuntu. 

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
![](/assets/images/acceder-a-locolhost/img4.jpg)

Ahora ya podemos ejecutar **chocolatey desde cmd.exe como desde powershell.exe, y vamos a instalar openss.

![](/assets/images/acceder-a-locolhost/img5.jpg)

Ahora ya podemos ejecutar ssh como en una terminal de Linux.

![](/assets/images/acceder-a-locolhost/img6.jpg)

---
## Instalando XAMPP

XAMPP es un paquete de software libre, que consiste principalmente en el sistema de gestión de bases de datos MySQL, el servidor web Apache y los intérpretes para lenguajes de script PHP y Perl.

![](/assets/images/acceder-a-locolhost/img7.jpg)

Al momento de instalar surgieron 03 errores faciles de resolver, ya que como cualquiera que hace pruebas tenemos muchas aplicaciones instaladas, y ellos ya pueden estar usando los puertos por defecto que utiliza xamp.

- Puerto 80 en uso (Tengo instalado MS SQL Server), SQL Server Reporting Service (MSSQLSERVER), usa por defecto el puerto 80, asi que si lo detenemos no afecta el funcioanmiento de del servidor de SQL. 
- El puerto 443 ya esta siendo usado. (Tengo instalado VMWare), solucion cambias el puerto en VMWARE o en la configuracion de Xamp [__Solucion__](https://stackoverflow.com/questions/21182512/how-to-stop-vmware-port-error-of-443-on-xampp-control-panel-v3-2-1).
- cannot create file c xampp xampp control ini acceso denegado. [__Solucion__](https://www.youtube.com/watch?v=6iTX06Kdt4U)

----
## Ahoara que ya tenemos instalado todas las herramientas podemos ver nuestro pagina que tenemos en localhost en cualquier parte.

![](/assets/images/acceder-a-locolhost/img8.jpg)

Ya tenemos panel de xamp ejecutandose en localhost, correctamente.

![](/assets/images/acceder-a-locolhost/img9.jpg)

Podemos ejecutar grok o localhost.run desde la terminal de cmd en el puerto 80 recuerda xamp esta ejecutandose en el puerto 80. veamos 

```bash
- **para ngrok**
- ngrok.exe http 80

- y para localhost.run
- ssh -R 80:localhost:80 localhost.run
```

![](/assets/images/acceder-a-locolhost/img10.jpg)

ahora ya tenemos los dos enlaces tanto de ngrok como localhost.run

```html
http://76e97b51e33843.localhost.run/dashboard/

http://5774-190-236-0-251.ngrok.io/dashboard/
```
vamos a ver como se ve en un navegador.

![](/assets/images/acceder-a-locolhost/img11.jpg)

![](/assets/images/acceder-a-locolhost/img12.jpg)




Tambien puedes verlo en mi canal [ __Youtube__ ](#)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)