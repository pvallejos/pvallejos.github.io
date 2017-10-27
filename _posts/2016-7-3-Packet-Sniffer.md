---
layout: post
title: Packet Sniffer
category: RaspberryPi
---

Packet Sniffer with Raspberry Pi

![_config.yml]({{ site.baseurl }}/images/23573368.png)

# Materiales
* Raspberry Pi
* Raspbian (ultima version)
* usb to ethernet adapter
* Cable ethernet
* Memoria disponible
* Corriente (De preferencia bateria externa)


# Configuracion
Creamos un archivo en Shell. Este script lo que hace es eliminar las direcciones ip de las interfaces `eth0` y `eth1`, para luego habilitar una interfaz nueva llamada `bridge0`, el cual usaremos para interceptar el trafico. podremos guardarlo con el nombre `analyzer_conf.sh` para luego ejecutarlo usando `sudo ./analyzer_conf.sh`

```
ifconfig eth0 0.0.0.0
ifconfig eth1 0.0.0.0
brctl addbr bridge0
brctl addif bridge0 eth0
brctl addif bridge0 eth1
ifconfig bridge0 up
```


# Intercepcion
Podremos ocupar cualquier sniffer, solo necesitas tener la interfaz en modo promiscuo, recomiendo estos:

* tcpdump
* netsniff-ng
* tshark
* bettercap

Ejemplo:

```
sudo tcpdump -i bridge0 -w captured.pcap
```


# Ejecutar al inicio
Si queremos que empiece a capturar desde que se enciende la Raspberry, necesitamos crear un script juntando las configuraciones de las interfaces y el sniffer en un solo archivo:

```python
#!/usr/bin/python
import os

# Config
os.system("ifconfig eth0 0.0.0.0")
os.system("ifconfig eth1 0.0.0.0")
os.system("brctl addbr bridge0")
os.system("brctl addif bridge0 eth0")
os.system("brctl addif bridge0 eth1")
os.system("ifconfig bridge0 up")

# Sniffer
a=0
while True:
	if os.path.exists("/home/pi/captured"+str(a)+".pcap"):
		a=a+1
	else:
		os.system("tcpdump -i bridge0 -w /home/pi/captured"+str(a)".pcap")
```

Luego, lo guardamos en la carpeta `/etc/init.d` con el nombre `start_sniffer.py`. Adicionalmente tendremos que agregarle permisos de ejecucion usando:

```
sudo chmod +x /etc/init.d/start_sniffer.py
```

Despues de agregarle los permisos de ejecucion, editaremos el siguiente archivo `/etc/rc.local`

```bash
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

# Print the IP address
_IP=$(hostname -I) || true
if [ "$_IP" ]; then
  printf "My IP address is %s\n" "$_IP"
fi

python /etc/init.d/start_sniffer.py # Agregando esta linea

exit 0
```

### Finalizando
Ahora está todo listo para usar la Raspberry Pi como Packet Analyzer. Solo queda hacer un `reboot` para que se apliquen las nuevas configuraciones
