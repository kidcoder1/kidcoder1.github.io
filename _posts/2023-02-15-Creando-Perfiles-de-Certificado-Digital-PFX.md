---
layout: single
title: Creacion de Perfiles de Certificado Digital PFX
excerpt: "En criptografía, PKCS #12 define un formato de archivo para almacenar muchos objetos criptográficos como un solo archivo. Suele utilizarse para agrupar una clave privada con su certificado X.509 o para agrupar a todos los miembros de una cadena de confianza. Un archivo PKCS #12 puede cifrarse y firmarse. [wikipedia](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiG_sPW5Jj9AhV3rJUCHU7hBSgQmhN6BAhYEAI&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FPKCS_12&usg=AOvVaw33lim6wQpG14wIzCWAuSR8)"
date: 2023-02-15
classes: wide
header:
  teaser: /assets/images/cert-pfx/pfx-1.jpg
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - windows
  - scripts
  - hardening
tags:  
  - windows
  - scriptd
  - hardening
---
## Crear Archivo de Certificado .PFX Usando OPENSSL

El formato PKCS #12 o PFX es un formato binario para almacenar el certificado del servidor, cualquier certificado intermedio y la clave privada en un solo archivo encriptable. Los archivos PFX generalmente se encuentran con las extensiones .pfx y .p12. Los archivos PFX se utilizan normalmente en maquinas Windows para importar y exportar certificados y claves privadas.

## Requisitos

- La clave privada original utilizada para el certificado
- Un archivo PEM (.pem, .crt, .cer) o PKCS #7/P7B (.p7b, .p7c)
- OpenSSL
  
[Fuente: Nodored](https://nodored.com/clientes/knowledgebase/330/Crear-un-archivo-de-certificado-.pfxor.p12-utilizando-OpenSSL.html)

## Vamos a preparar la maquina para ello 

Primero necesitamos instalar OPENSSL, para este punto voy a usar el gestor de paquetes Chocolatey, vamos a instalar usando powerhell como administrador.

```java
PS C:\Windows\system32\WindowsPowerShell\v1.0> powershell.exe -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))"
```
luego agregamos chocolatey a nuestra PATH, escribimos en inicio de windows variables de entorno o como estamos en la terminal de powershell usamos esta.

```java
PS C:\Windows\system32\WindowsPowerShell\v1.0> SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

![](/assets/images/cert-pfx/pfx-2.jpg)


ahora vamos a instalar openssh usando chocolatey, desde el terminal de powershell o cmd, recuerde como administrador.

```ruby
C:\OpenSSL>choco install openssl
```

![](/assets/images/cert-pfx/pfx-3.jpg) 

si el OPENSSL se ha instalado correctamente con choco. vamos a crearnos un directorio de trabajo, creare una carpeta llamada OPENSSL y dentro de ella nos creamos la siguiente estructura de carpetas para trabajar ordenadamente

```bash
C:\OpenSSL>md certs,crl,csr,newcerts,private
```
![](/assets/images/cert-pfx/pfx-4-1.jpg)

ahora vamos a buscar un archivo de configuracion, cuando instalaste openssl por defecto se ha creado en la siguiente ruta.

![](/assets/images/cert-pfx/pfx-4.jpg)

El archivo se llama openssl.cfg vamos a copiar a la carpeta de hemos creado llamado ***OpenSSL*** en la raiz. como se observa en la imagen.

![](/assets/images/cert-pfx/pfx-5.jpeg)

de hecho hay puntos que deberiamos configurar a nuestro gusto, pero para esta practica solo cambiaremos el lugar donde hemos creado nuestro carpeta de trabajo y la linea 83 debe quedar.

```bash
policy = policy_anything

```
![](/assets/images/cert-pfx/pfx-6.jpeg)

Despues vamos a crear un archivo de texto vacio llamado index.txt el cual se comportara como nuestra base de datos.

![](/assets/images/cert-pfx/pfx-7.jpeg)

Vamos a crear otro archivo sin extension dentro de la carpeta OpenSSL, llamado serial, el cual va actuar como nuestra version.

![](/assets/images/cert-pfx/pfx-8.jpeg)

Vamos a crear el certificado publico para nuestra CA y la llave privada asociada al certificado, es necesario ingresar los datos que consideremos necesarios y una contraseña para privadaCA.key (ejm. kidcode12345).

```bash
openssl req -config openssl.cnf -new -x509 -extensions v3_ca -keyout C:/OpenSSL/private/privadaCA.key -out C:/OpenSSL/certs/certificadoCA.crt
```
![](/assets/images/cert-pfx/pfx-9.jpeg)

Vamos a generar una llave privada para el usuario cliente (el servidor cliente debe generar su llave privada en la carpeta private, te solicitara que coloques una contraseña (ejm. kidcode2023).

```bash
openssl genrsa -aes128 -out C:/OpenSSL/private/privadaAngel.key 1024
```
Vamos a generar una solicitud de firma por parte del servidor cliente. el cliente debe generar una solicitud para que nuestra ropia ca/ (/OpenSSL) le emita el certificado publico firmado. recuerda poner su password de la llave privada cliente (kidcode2023), y completa los datos para el certificado.

```bash
openssl req -new -key C:/OpenSSL/private/privadaAngel.key -out C:/OpenSSL/csr/solicitudAngel.csr -config C:/OpenSSL/openssl.cnf
```
![](/assets/images/cert-pfx/pfx-10.jpeg)

Luego procedemos a firmar la solicitud generada por el usuario angel, te va pedir la password de la clave privada (kidcode12345), finalmente le damos si a las dos ultimas prguntas.
```bash
openssl ca -in C:/OpenSSL/csr/solicitudAngel.csr -out C:/OpenSSL/newcerts/certificadoAngel.crt -cert C:/OpenSSL/certs/certificadoCA.crt -keyfile C:/OpenSSL/private/privadaCA.key -config C:/OpenSSL/openssl.cnf
```
![](/assets/images/cert-pfx/pfx-11.jpeg)

finalmente vamos a convertir un archivo pem  y la clave privada a un archivo pfx, ponemos la password de la llave privada cliente (kidcode2023), y ponemos una nueva contraseña para el archivo pfx (pfx2023)

```ruby
openssl pkcs12 -export -out C:/OpenSSL/newcerts/angel.pfx -inkey C:/OpenSSL/private/privadaAngel.key -in C:/OpenSSL/newcerts/certificadoAngel.crt
```

![](/assets/images/cert-pfx/pfx-12.jpeg)

y ya esta tenemos nuestra certificado digital en la carpeta **newcert** con el nombre angel.pfx

![](/assets/images/cert-pfx/pfx-13.jpeg)

Tambien puedes verlo en mi canal [ __Youtube__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)