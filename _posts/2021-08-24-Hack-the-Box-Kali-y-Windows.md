---
layout: single
title: Kali Linux y Windows
excerpt: "Si alguna pensaste usar Burp Suite u otras tools desde Windows sin salir de kali, mientras hacias una maquina de Hack the Box, y no pudiste por que HTB solo permite usar la VPN en una sola terminal con tu suario, la solucion seria usar Kali en modo enrutdor de tal manera que puedas hacer ping desde windows como si estuvieras en Kali, claro usando la VPN desde kali, de esa manera podemos usar las tools de nuestra preferencia en windows sin problemas."
date: 2021-08-24
classes: wide
header:
  teaser: /assets/images/kali-windows/kali-windows.png
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

Si alguna pensaste usar Burp Suite u otras tools desde Windows sin salir de kali, mientras hacias una maquina de Hack the Box, y no pudiste por que HTB solo permite usar la VPN en una sola terminal con tu suario, la solucion seria usar Kali en modo enrutdor de tal manera que puedas hacer ping desde windows como si estuvieras en Kali, claro usando la VPN desde kali, de esa manera podemos usar las tools de nuestra preferencia en windows sin problemas.

<img src="/assets/images/kali-windows/kali-windows.png" alt="BurpSuite" width="1200" height="640"/>

## codigo
**Borramos si tenemos alguna configuracion anterior**

```
iptables --flush
iptables --table nat --flush
iptables --delete-chain
iptables --table nat --delete-chain
```
## kali
**Agregamos las siguientes entradas en nuestra kali, para que se comporte como un enrutador**

~~~
 iptables --table nat --append POSTROUTING --out-interface tun0 -j MASQUERADE
 echo 1 > /proc/sys/net/ipv4/ip_forward
~~~
## Windows
****Agregamos las siguientes entradas en windows para que se enrute correctamente**

~~~
route add 10.10.10.0 mask 255.255.255.0 192.168.18.128
~~~

y ya podemos usar windows como si estuvieramos en kali linux, podemos hacer ping desde windows

![](/assets/images/kali-windows/cmd.jpg)

o talvez usar Burp Suite 

<img src="/assets/images/kali-windows/burpsuite1.png" alt="BurpSuite" width="400" height="650"/>

<!---![](/assets/images/kali-windows/burpsuite1.png)-->

> Kidcode
