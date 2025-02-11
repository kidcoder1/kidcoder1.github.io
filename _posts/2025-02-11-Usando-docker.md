---
layout: single
title: Usando Docker y sus Comandos
excerpt: "En el mundo del desarrollo de software, la portabilidad y consistencia son claves. Imagina poder ejecutar tu aplicación en cualquier entorno sin preocuparte por las diferencias de configuración entre las máquinas. Aquí es donde Docker entra en juego. Con Docker, puedes crear, probar y desplegar aplicaciones en contenedores ligeros, aislados y autónomos"
date: 2025-02-11
classes: wide
header:
  teaser: /assets/images/usando-dockers/000.jpg
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

Docker es una plataforma de contenedores que permite empaquetar, distribuir y ejecutar aplicaciones de manera ligera y aislada. Utiliza tecnología de contenedores para crear entornos virtuales independientes que incluyen todo lo necesario para ejecutar una aplicación: código, dependencias y configuraciones. Esto asegura que la aplicación se ejecute de manera consistente sin importar el entorno. Docker facilita el desarrollo, la prueba y el despliegue de aplicaciones, optimizando el uso de recursos y mejorando la portabilidad, lo que lo convierte en una herramienta esencial para los desarrolladores modernos

En este artículo, exploraremos qué es Docker, cómo funciona y por qué se ha convertido en una herramienta esencial para los desarrolladores modernos. Desde sus beneficios de eficiencia y facilidad de uso hasta la forma en que resuelve problemas comunes de compatibilidad entre entornos.

## Instalando Docker

Siempre debemos asegurarnos de que tenemos todo actualizado antes de comenzar con la instalación de cualquier software extra en nuestro sistema operativo.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$
kali@kali:~$ sudo apt install -y docker.io
```

## Matando los procesos docker

```bash
kali@kali:~$ pkill docker
```

## Docker Daemon

Cuando ejecutas dockerd, se inicia el demonio Docker, que escucha las solicitudes del cliente Docker (por ejemplo, a través de la línea de comandos con docker) y las procesa. Es el componente central que orquesta todas las acciones y asegura que los contenedores se ejecuten correctamente y se mantengan aislados entre sí. 

El siguiente comando se utiliza para ejecutar el demonio de Docker (dockerd) en segundo plano y redirigir tanto la salida estándar como los errores a /dev/null, que es un dispositivo que descarta cualquier dato que se le envíe

````bash
kali@kali:~$ dockerd > /dev/null 2>&1 &
````

- Verifica si Docker ya está en ejecución con el siguiente comando

```bash
kali@kali:~$ ps aux | grep dockerd
```

- Si encuentras un proceso de Docker en ejecución, puedes detenerlo con.

```bash
kali@kali sudo systemctl stop docker
```

- O, si no está controlado por systemctl, intenta matar el proceso manualmente usando el PID (en este caso 125153).

```bash
kali@kali sudo kill 125153
```

- Si Docker se cerró incorrectamente o no se detuvo de manera adecuada, el archivo /var/run/docker.pid puede seguir existiendo y hacer que el daemon no pueda arrancar. Si estás seguro de que no hay procesos de Docker en ejecución, puedes eliminar el archivo docker.pid manualmente:

```bash
kali@kali:~$ sudo rm /var/run/docker.pid
````

- El comando disown % se usa en sistemas Unix/Linux dentro de un shell (como Bash) para desasociar un trabajo en segundo plano de la sesión actual del terminal.

```bash
kali@kali:~$ disown %
```

-  listar todas las imágenes de Docker en tu sistema. Este comando lista las imágenes de Docker que están disponibles en tu máquina local. Muestra información sobre cada imagen, como su ID, nombre, etiqueta, fecha de creación y tamaño. La opción -a (o --all) indica que se deben listar todas las imágenes, incluyendo las imágenes intermedias que no están siendo usadas por contenedores. Si no usas -a, solo se mostrarían las imágenes que tienen al menos un contenedor asociado.

```bash
kali@kali:~$ docker images -a
```

- creando un archivo docker file

  - touch dockerfile
  - FROM ubuntu:18.04 --> construimos la imagen de ubuntu

- Le indicamos que construya la imagen y lo llame ubuntu
```bash
kali@kali:~$ docker bulid . -t ubuntu 
```

- si vemos con docker images, vemos que se ha creado una imagen.

```bash
kali@kali:~$ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    ubuntu              18.04               4e5021d210f6        3 weeks ago         64.2MB
    ubuntu              latest              4e5021d210f6        3 weeks ago         64.2MB
````

- creamos y ejecutamos un contenedor a partir de la imagen de Docker Ubuntu, con ciertas opciones. 

  - docker run: Este es el comando base para crear y ejecutar un contenedor a partir de una imagen. Si la imagen no está presente localmente, Docker la descarga del registro de Docker (por defecto, Docker Hub).
  - docker run: Este es el comando base para crear y ejecutar un contenedor a partir de una imagen. Si la imagen no está presente localmente, Docker la descarga del registro de Docker (por defecto, Docker Hub).
  - -i: La opción -i habilita el modo interactivo, lo que significa que se mantiene la entrada estándar (stdin) abierta para el contenedor. Esto generalmente se usa para poder interactuar con el contenedor si se accede a él más tarde, aunque no se use directamente en este caso (ya que es en segundo plano).
  - -t: Esta opción asigna un pseudo-TTY (terminal) al contenedor. Se utiliza junto con -i para permitir la interacción del contenedor, especialmente si deseas ejecutar comandos interactivos dentro del contenedor.
  - --network bridge: Define que el contenedor usará la red bridge. Esto significa que el contenedor se conecta a una red interna proporcionada por Docker que permite la comunicación entre contenedores en esa red. La red "bridge" es la red predeterminada que Docker asigna a los contenedores cuando no se especifica una red personalizada.
  - --name aplication: Asigna un nombre personalizado al contenedor. En este caso, el contenedor se llamará aplication en lugar de usar el nombre predeterminado que Docker asigna a los contenedores (generalmente un nombre aleatorio).
  - ubuntu: Es el nombre de la imagen desde la cual se creará el contenedor. Si no tienes esta imagen en tu sistema, Docker la descargará automáticamente desde Docker Hub.

- listar los contenedores en ejecución en tu sistema. Muestra información sobre los contenedores que están actualmente activos (es decir, que están en estado "ejecutándose").

```bash
kali@kali:~$ docker ps
```
- con -a : Esto incluirá los contenedores que están detenidos o en cualquier otro estado.

- para ejecutar un comando dentro de un contenedor en ejecución. En este caso, el comando ejecutado es bash, lo que permite abrir una terminal interactiva dentro del contenedor llamado aplication. Vamos a desglosarlo

```bash
kali@kali:~$  docker exec -it aplication bash 
 ```

1.  docker exec: Este comando se utiliza para ejecutar un comando en un contenedor que ya está en ejecución. A diferencia de docker run, que se usa para iniciar un contenedor, docker exec te permite interactuar con un contenedor que ya está corriendo
2. -it: Son dos opciones combinadas, -i: Permite la entrada interactiva (stdin), lo que permite la interacción con el contenedor y -t: Asigna un pseudo-TTY (terminal) al contenedor lo que le permite mostrar una interfaz de línea de comandos interactiva.
3. aplication: Es el nombre del contenedor al que deseas acceder. En este caso, el contenedor se llama aplication. Puedes reemplazarlo con el ID del contenedor si prefieres usar el identificador.
4. bash: Este es el comando que se ejecutará dentro del contenedor. En este caso, se está invocando la shell de Bash dentro del contenedor, lo que te permitirá trabajar de manera interactiva.

- para salir o detener el contenedor usamos.

```bash
kali@kali:~$  exit
kali@kali:~$  docker stop aplication
```

- eliminamos cualquier proceso de docker uculto corriendo.

```bash
docker rm $(docker ps -a -q)
```

- Para eliminar todas las imágenes "colgantes" o "dangling" de Docker, es decir, aquellas imágenes que ya no están asociadas a ningún contenedor y que generalmente son versiones intermedias creadas durante el proceso de construcción de otras imágenes.

```bash
kali@kali:~$ docker rmi $(docker images --filter='dangling=true' -q)
```

- Para crear y ejecutar un contenedor a partir de la imagen Ubuntu, con varias configuraciones específicas. Vamos a desglosarlo paso a paso:
1.  docker run: Este comando crea y ejecuta un contenedor a partir de la imagen que se especifica.
2. -d: Esto indica que el contenedor debe ejecutarse en modo "detached" (en segundo plano).
3. -i: Esta opción habilita la entrada interactiva (stdin).
4. -t: Asigna un pseudo-TTY (terminal) al contenedor.
5. -p80:80: Esta opción mapea el puerto 80 de tu máquina local al puerto 80 del contenedor. Es decir, cualquier solicitud HTTP que llegue al puerto 80 de tu máquina (en este caso, a través de tu navegador o herramientas de red) será redirigida al puerto 80 del contenedor. Esto es útil si quieres ejecutar un servidor web (como Apache o Nginx) dentro del contenedor y acceder a él desde fuera.
6. --network bridge: Esta opción especifica que el contenedor debe conectarse a la red bridge, que es la red predeterminada de Docker para contenedores.
7. --name aplication: Esta opción le asigna un nombre personalizado al contenedor.
8. ubuntu: Es el nombre de la imagen de Docker a partir de la cual se creará el contenedor.



Tambien puedes verlo en mi canal [ __Youtube kidcoder1__ ](https://www.youtube.com/channel/UC1kIp8GaJLCzYJW_h_Raisw)

> ¿Te ha gustado este artículo? Si quieres, puedes ayudarme a escribir el siguiente artículo.  [__invitándonme a un rico café.__](#)