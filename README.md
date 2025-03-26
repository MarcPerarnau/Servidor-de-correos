# Configuración de un Servidor DHCP, DNS y Correo en Ubuntu
Este documento detalla los pasos necesarios para configurar un servidor con servicios de DHCP, DNS y correo en un entorno Ubuntu Server. El objetivo es proporcionar una infraestructura de red funcional con asignación de direcciones IP dinámicas, resolución de nombres de dominio y gestión de correos electrónicos.

## Requisitos Previos

- Antes de comenzar, asegúrese de cumplir con los siguientes requisitos:

- Ubuntu Server instalado y configurado con una IP fija dentro del rango de la red local.

- Acceso con privilegios de superusuario.

- Conexión a internet para la instalación de paquetes.

- Dominio local configurado para el servicio de DNS y correo.

## Servicios a Configurar

- Servidor DHCP: Asignar direcciones IP dinámicas a los clientes de la red.

- Servidor DNS: Resolver nombres de dominio dentro de la red local.

- Servidor de Correo: Configurar Postfix y Dovecot para el envío y recepción de correos.

# Instalación y Configuración

A continuación, se detallan los pasos para la instalación y configuración de cada servicio.

## Configuración de a IP fija

- Deberemos editar el archivo `/etc/netplan/00-installer-config.yaml`
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```
![Imagen](source/netplan.png)

- Dentro deberemos configurar lo siguiente. 
```bash
network:
  version: 2
  ethernets:
    enp0s3: # Cambiar por tu adaptador de red
      addresses:
         - Tu-IP/mascara
      routes:
        - to: default
          via: Tu-Gatawey
      nameservers:
        addresses: [ 1.1.1.1, Tu-IP ]
```
![Imagen](source/configuraciónIP.png)

Cuando todo este configurado salimos con `Ctrl` + `o` y `Ctrl` + `X`

- Una vez acabada la configuración de la IP fija ejecutaremos un `netplan apply` para confirmar la configuración exitosa. 

```bash
sudo netplan apply
```
![Imagen](source/netplanapply.png)

- Ejecutamos un `ip a` y confirmamos que ya tenemos assignada la IP de manera fija. 
```bash
ip a
```

![Imagen](source/ipa.png)

## Actualizaciones y instalaciones

- Primero de todo deberemos actualizar el equipo mediante la siguiente comanda. 
```bash
sudo apt update && sudo apt full-upgrade -y
```
![Imagen](source/actualización.png)

- Instalamos bind9 para el servidor de DNS y algunos de sus paquetes.
```bash
sudo apt install bind9 bind9-utils bind9-doc -y
```

![Imagen](source/bin9.png)

- Ahora deberemos instalar `isc-dhcp-server`
```bash
sudo apt install isc-dhcp-server -y
```

![Imagen](source/dhcp.png)

- Ahora procedemos a instalar `Postfix` `Dovecot` `Maildir` y `Mailutils`

```bash
sudo apt install postfix dovecot-imapd mailutils maildir-utils -y
```

![Imagen](source/postfix.png)

- Nos va a salir un pop-up deberemos escojer la opción `Sitio de Internet` y tendremos que añadir nuestro dominio.

![Imagen](source/dominio.png)