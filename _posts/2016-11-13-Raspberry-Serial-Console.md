---
layout: post
title: Raspberry Serial Console
categories: RaspberryPi
---

Raspberry Pi serial console connection with TTL2USB cable

![_config.yml]({{ site.baseurl }}/images/raspberrypittl.png)

# Materiales

* Raspberry pi
* Raspbian
* Cable TTL2USB

# Habilitando conexion por TTL
Para poder conectarse de forma fisica a la terminal de Raspbian tenemos que habilitar el uart en la Raspbian, desde SSH o escritorio

```
sudo su
echo "enable_uart=1" >> /boot/config.txt
```

# Conectando a Raspbian
Ya teniendo habilitado el uart desde Raspbian ahora toca conectar a los pines adecuados como sale en la imagen inicial, instalar y conectarse usando screen desde el dispositivo donde esté conectada la Raspberry pi

### Instalando screen
```
sudo apt-get install screen
```

### Conectando a Raspbian
```
sudo screen /dev/ttyUSB0 115200
```

mas informacion: [https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all){:target="_blank"}


