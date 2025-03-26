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
```
sudo nano /etc/netplan/00-installer-config.yaml
```
![Imagen](source/netplan.png)
