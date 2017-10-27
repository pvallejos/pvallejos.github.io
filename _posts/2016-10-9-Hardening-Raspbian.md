---
layout: post
title: Hardening Raspbian
categories: RaspberryPi
---

Raspbian secure configs

# Password por defecto
Despues de instalar Raspbian la contraseña por defecto es 'raspberry'. para eso tendremos que cambiarlo usando:

```
passwd pi
```

# Cambiar hostname
```
sudo sh -c "echo nuevohostname > /etc/hostname"
sudo sed -i 's/raspberrypi/nuevohostname/' /etc/hosts
sudo reboot
```


# Actualizar
Antes que todo es recomendado actualizar el sistema a la ultima version, terminado esto reiniciar

```
sudo apt-get update
sudo apt-get dist-upgrade -y
sudo reboot
```

# Cambiando puerto SSH
Para poder cambiar el puerto SSH por defecto necesitamos editar el siguiente archivo:

```
sudo nano /etc/ssh/sshd_config
```

En la parte donde dice `port 22` cambiamos por algun numero entre 1 y 65535

```
# Package generated configuration file
# See the sshd_config(5) manpage for details

# What ports, IPs and protocols we listen for
Port 22
# Use these options to restrict which interfaces/protocols sshd will bind to
#ListenAddress ::
#ListenAddress 0.0.0.0
(...)
```

Terminado de cambiar las configuraciones se tiene que reiniciar el servicio SSH

```
sudo service ssh restart
```

# Bloqueando fuerza bruta
El ataque mas comun para poder acceder al SSH es usar fuerza bruta. Este tipo de ataques no es muy efectivo pero siempre hay un porcentaje de riesgo. Para evitar estos ataques necesitaremos instalar fail2ban

### Instalacion

```
sudo apt-get install fail2ban -y
```

### Configuracion

Las configuraciones por defecto de fail2ban es bloquear por 10 minutos el intento de acceso por SSH cuando se supera los 6 intentos errados. fail2ban tambien esta disponible para otros servicios donde se pueden habilitar o modificar:

```
sudo nano /etc/fail2ban/jail.conf
```

Los intentos de acceso quedaran guardados en: `/var/log/auth.log`

# Doble autentificacion SSH
A veces no basta solo usar una contraseña. Para eso ocuparemos el autenticador de Google, que lo instalaremos en el telefono: 
[https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2){:target="_blank"}


### Instalacion
Con las configuraciones iniciales en el APK ya hechas necesitamos instalarlo y configurarlo en raspbian

```
sudo apt-get install libpam-google-authenticator -y
```

### Configuracion

Luego de tenerlos insrtalado ejecutamos:

```
google-authenticator
```

```
Do you want authentication tokens to be time-based (y/n) y

[Saldra un codigo QR donde tendras que usar la aplicacion de google authenticator desde el telefono "Escanear codigo de barras"]

Do you want me to update your "/root/.google_authenticator" file (y/n) y

Do you want to disallow multiple uses of the same authentication token? This restricts you to one login about every 30s, but it increases your chances to notice or even prevent man-in-the-middle attacks (y/n) y

By default, tokens are good for 30 seconds. In order to compensate for possible time-skew between the client and the server, we allow an extra token before and after the current time. If you experience problems with poor time synchronization, you can increase the window from its default size of +-1min (window size of 3) to about +-4min (window size of 17 acceptable tokens). Do you want to do so? (y/n) y

If the computer that you are logging into isn't hardened against brute-force login attempts, you can enable rate-limiting for the authentication module. By default, this limits attackers to no more than 3 login attempts every 30s. Do you want to enable rate-limiting (y/n) y
```

Despues de instalar y configurar google-authenticator en Raspbian, ahora toca configurar el SSH para que pueda recivir el codigo de verificacion de google, editando este archivo `/etc/pam.d/sshd` y añadiendo la linea `auth       required     pam_google_authenticator.so` antes de `@include common-auth`

```
# PAM configuration for the Secure Shell service
auth       required     pam_google_authenticator.so

# Standard Un*x authentication.
@include common-auth

# Disallow non-root logins when /etc/nologin exists.
account    required     pam_nologin.so

# Uncomment and edit /etc/security/access.conf if you need to set complex
# access limits that are hard to express in sshd_config.
# account  required     pam_access.so
(...)
```

luego de esto ahora toca modificar el siguiente archivo `/etc/ssh/sshd_config` cambiando la linea `ChallengeResponseAuthentication no` por `ChallengeResponseAuthentication yes`

```
(...)
# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
ChallengeResponseAuthentication yes
(...)
```

Terminando de hacer todo esto, solo queda reiniciar el servicio de SSH

```
sudo service ssh restart
```

# Deshabilitando servicios en boot
Cuando uno instala algun servicio como por ejemplo dnsmasq o mysql en Raspbian, este queda iniciado por defecto en el boot, para poder deshabilitarlo se ocupa `sudo update-rc.d <nombre del servicio> disable`, aca unos ejemplos:

```
# Disable services in boot
sudo update-rc.d apache2 disable
sudo update-rc.d dnsmasq disable
sudo update-rc.d mysql disable
sudo update-rc.d postgresql disable
```

# Cambiando TTL
Para evitar el reconocimiento de un sistema operativo por medio del TTL es recomendado cambiarlo

```
sudo sh -c "echo 1 > /proc/sys/net/ipv4/ip_default_ttl"
```
