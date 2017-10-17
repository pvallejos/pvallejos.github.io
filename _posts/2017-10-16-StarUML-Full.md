---
layout: post
title: StarUML Full
---

Install and crack StarUML 2 in Ubuntu 16.04

# Instalacion
```
wget https://launchpad.net/ubuntu/+archive/primary/+files/libgcrypt11_1.5.3-2ubuntu4.2_amd64.deb
sudo dpkg -i libgcrypt11_1.5.3-2ubuntu4.2_amd64.deb
wget http://staruml.io/download/release/v2.8.0/StarUML-v2.8.0-64-bit.deb
sudo dpkg -i StarUML-v2.8.0-64-bit.deb
```

# Crackeando StarUML 2
Para poder tener StarUML 2 registrado necesitamos editar el siguiente archivo:

En la carpeta de instalación:

    Mac OS: /Applications/StarUML.app/Contents/www/license/node/
    Linux: /opt/staruml/www/license/node/
    Microsoft: C:\Program Files (x86)\StarUML\www\license\node

buscar el archivo: `LicenseManagerDomain.js` y reemplazar la función:

```javascript
function validate(PK, name, product, licenseKey) {
        return{
           name: "Vay3t Arch",
           product: "StarUML",
           licenseType: "vip",
           quantity: "vay3t.github.io",
           licenseKey: "Licencia full starUML 2"
        };
    }
```

### Nota
En linux necesitas usar `sudo` para poder editar el archivo. Los campos más importantes son `name` y `licenseKey`. Esos campos puedes rellenarlos como tu quieras. No es necesario que diga `Vay3t Arch` ni tampoco `Licencia full starUML 2`.

### Activando StarUML
Para terminar abrir el programa, cerrar la ventana de registro, ir a `help -> Enter License` e ingresar el `name` que pusiste, en este caso `Vay3t Arch` y en `licenseKey` poner `Licencia full starUML 2`. 
