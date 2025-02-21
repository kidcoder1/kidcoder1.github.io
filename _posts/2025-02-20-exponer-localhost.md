---
layout: single
title: Exponer Localhost a Internet
excerpt: "Hoy veremos diferentes formas de exponer nuestro servidor local hacia internet. Basicamente son herramientas que permite conectar servidores locales a internet público. Es un proxy inverso que funciona en la mayoría de los sistemas operativos y con cualquier conexión a internet.
- Da nombres a los servidores locales 
- Hace que los servidores locales sean accesibles globalmente 
- Tunela protocolos como HTTPS o SSH a través de cortafuegos y NAT 
- Permite hacer visible un servidor HTTP en un dispositivo sin una dirección IP pública"
date: 2025-02-20
classes: wide
header:
  teaser: /assets/images/tuneling/000.png
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - windows
  - Linux
  - custom
tags:  
  - windows
  - Linux
  - custom
---

Aqui veremos diferentes formas de exponer nuestro servidor local a internet publico.

## NGROK

Ngrok es un servicio que nos permite crear nuestro servidor local en un subdominio para poder visualizarlo fuera de la LAN.

primero necesitaras crear una cuenta, es gratis (tambien hay una version de paga), desde podras generar tu token e cual te servira para poder usar ngrok.
   
  ![](/assets/images/tuneling/001.jpg)

## Instalacion 

Descargas el binario para tu sistema operativo, lo guardas en algun directorio, para mayor comodidad puedes agregarlo a tu PATH.

#### (Windows)

En windows puedes instalar con el comando choco (administrador de paquetes parecido a APT o PKG en linux), tambien ya vimos como instalarlo en windows, ya que no viene de forma nativa.

pagina de descarga : https://dashboard.ngrok.com/get-started/setup/windows

```bash
choco install ngrok
```
#### Iniciamos ngrok solo la primera vez

```bash
ngrok config add-authtoken $YOUR_AUTHTOKEN
```

Esto creara un archivo con las siguintes caracteristicas, ngrok.yml, donde tambien puedes personalizar a tu manera con mas detalles de tunneling.

```bash
agent:
	authtoken: <your-authtoken>
```
#### Publicamos

A partir de este momento ya podemos publicar nuestro localhost:8080 a internet

```bash
ngrok http http://localhost:8080
```

cree mi servdor local con python

```bash
python -m http.server 8000
```
Puedes ver toda la documentacion.

https://dashboard.ngrok.com/get-started/setup/windows


## BORE

Un túnel TCP moderno y simple en Rust que expone los puertos locales a un servidor remoto, evitando los firewalls de conexión NAT estándar. Eso es todo lo que hace: ni más ni menos. gracias a Erik Zhang 

Github: https://github.com/ekzhang/bore

![](/assets/images/tuneling/002.jpg)

#### Instalacion

En el github hay binarios para todas las plataformas, yo como utilizo windows voy poe exe. lo descargas desde su releases.

https://github.com/ekzhang/bore/releases/tag/v0.5.2

```bash
# binario para windows
wget https://github.com/ekzhang/bore/releases/download/v0.5.2/bore-v0.5.2-x86_64-pc-windows-msvc.zip
```

una vez descargado, lo extraigo del zip, si quiero puede agregarlo a mi PATH, y ejecutarlo. antes ya debemos tener nuestro servidor localhost, para las pruebas yo utilizo python -m http.server 8000, pero bien puedes usar XAMPP u otro similar

```bash
.\bore local 8000 --to bore.pub
```

![](/assets/images/tuneling/003.jpg)

El resultado en nuestro navegador desde internet publico

![](/assets/images/tuneling/004.jpg)

## Localtunnel Pinggy

Si buscas algo mas simple, y no quieres instalar nada en tu sistema, puedes usar este servicio, solo tienes que pegar este comando y redirigir tu puerto local hacia 443 por ejemplo.

Pagina: https://pinggy.io/blog/local_tunnel/

```bash
 $ ssh -p 443 -R0:localhost:8000 qr@a.pinggy.io
```
![](/assets/images/tuneling/005.jpg)

Redirigimos nuestro localhost al publico

![](/assets/images/tuneling/006.jpg)

Resultado nuestra pagina web en internet.

![](/assets/images/tuneling/007.jpg)

## localhost.run

Otro servicio parecido al anterior, sin necesidad de registrarse o instalar algo en el sistema.

Todo en un solo comando pasale tu puerto localhost y expongalo hacia internet.

Toda la documentacion en : https://localhost.run/

```bash
$ ssh -R 80:localhost:8000 localhost.run
```

listo !!

```bash
authenticated as anonymous user
8d9891ffd6ac33.lhr.life tunneled with tls termination, https://8d9891ffd6ac33.lhr.life
```
![](/assets/images/tuneling/008.jpg)

Nuestro tunneling funcionando.

![](/assets/images/tuneling/009.jpg)

Ademas te comparte un QR para que la envies, y la URL es dinamica va cambiando cada 15 minutos aproximado.

![](/assets/images/tuneling/010.jpg)

y tu que tunels conoces?...

Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)