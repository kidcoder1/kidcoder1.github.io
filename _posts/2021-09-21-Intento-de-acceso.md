---
layout: single
title: Intento de acceso a un socket no permitido por sus permisos de acceso
excerpt: "Si al ejecutar scripts de python o aplicaciones como ngrok, genera un error de tipo Intento de acceso a un socket no permitido por sus permisos de acceso, vamos a ver como se soluciona."
date: 2021-09-21
classes: wide
header:
  teaser: /assets/images/post_intento-de-acceso/img1.jpg
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - hackthebox
  - windows
tags:  
  - Kali
  - Windows
  - Pentest
---

Si al ejecutar scripts de python o aplicaciones como ngrok, genera un error de tipo Intento de acceso a un socket no permitido por sus permisos de acceso, vamos a ver como se soluciona.

![](/assets/images/post_intento-de-acceso/img1.jpg)

## Error N° 1 
**al ejecutar  >>python -m http.server**

```bash
C:\Users\Kidcode1\Downloads\imagines>python -m http.server 8080
Traceback (most recent call last):
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\runpy.py", line 193, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\runpy.py", line 86, in _run_code
    exec(code, run_globals)
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\http\server.py", line 1283, in <module>
    test(HandlerClass=handler_class, port=args.port, bind=args.bind)
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\http\server.py", line 1248, in test
    with ServerClass(addr, HandlerClass) as httpd:
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\socketserver.py", line 452, in __init__
    self.server_bind()
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\http\server.py", line 137, in server_bind
    socketserver.TCPServer.server_bind(self)
  File "C:\Users\Kidcode1\AppData\Local\Programs\Python\Python38\lib\socketserver.py", line 466, in server_bind
    self.socket.bind(self.server_address)
OSError: [WinError 10013] Intento de acceso a un socket no permitido por sus permisos de acceso
```
## Error N°
**Al ejecutar ngrok**

~~~bash
C:\Users\Kidcode1\Downloads\imagines>ngrok.exe http 8088
listen tcp 127.0.0.1:4049: bind: An attempt was made to access a socket in a way forbidden by its access permissions.
~~~

---

****Estos errores persisten en todos los puertos, no solo en 8000 u 8080 o 443*

Buscando por san gogle encontre, esto de debia a una variedad de causas, y en mi caso es que estaba ocuado tdos los puertos. lo explica en este [__post__](https://ardalis.com/attempt-made-to-access-socket/) mas detalladamente.

Con el siguiente comando se puede ver que puertos estan ocupados.

~~~
**netsh interface ipv4 show excludedportrange protocol=tcp**
~~~

```bash
C:\Users\Kidcode1\Downloads\imagines>netsh interface ipv4 show excludedportrange protocol=tcp

Protocolo tcp Intervalos de exclusión de puertos

Puerto de inicio    Puerto final
----------          --------
      1635        1734
      1735        1834
      1835        1934
      1935        2034
      2035        2134
      2135        2234
      2235        2334
      2384        2483
      2484        2583
      2825        2924
      3025        3124
      3125        3224
      3225        3324
      3325        3424
      3425        3524
      3525        3624
      3725        3824
      3925        4024
      4025        4124
      4125        4224
      4225        4324
      4325        4424
      4425        4524
      4725        4824
      4925        5024
      5025        5124
      5125        5224
      5225        5324
      5325        5424
      5425        5524
      5825        5924
      6025        6124
      6125        6224
      6225        6324
      6325        6424
      6425        6524
      6525        6624
      7025        7124
      7225        7324
      7325        7424
      7425        7524
      7525        7624
      7625        7724
      7725        7824
      7826        7925
      7926        8025
      8026        8125
      8126        8225
      8308        8407
* - Administered port exclusions.
```
Pero como puedo liberar todos esos puertos, con el siguiente comando dejamos libres todos esos puertos.

~~~
net stop winnat
~~~

![](/assets/images/post_intento-de-acceso/img2.jpg)

> Kidcode
