# Práctica 9: SERVIDORES (HTTP Y SAMBA)

**ESCUELA POLITÉCNICA NACIONAL**  
**Facultad de Ingeniería de Sistemas**  
**Carrera de Ciencia de Datos e Inteligencia Artificial**  

**Asignatura:** Sistemas Operativos  
**Semestre:** 2026-A  
 **Información del Grupo**  
**Docente:** Ing. Diana Martínez, PhD.  
**Integrantes:** Karely Bombón, Jhoan Sasnalema, Jhon Tiupul, Fidel Quilumba 
**Paralelo:** GR2CD 
**Fecha:** 7 de julio de 2026.  

---

## ÍNDICE DE CONTENIDOS


1. [OBJETIVOS](#1-objetivos)
2. [MARCO TEÓRICO](#2-marco-teórico)
3. [DESARROLLO Y PROCEDIMIENTO](#3-desarrollo-y-procedimiento)
    - 3.1. [Procedimiento: Parte 1 - Servidor Web Apache](#31-procedimiento-parte-1---servidor-web-apache)
    - 3.2. [Procedimiento: Parte 2 - Servidor SAMBA](#32-procedimiento-parte-2---servidor-samba)
    - 3.3. [Verificación de Funcionamiento de Red](#33-verificación-de-funcionamiento-de-red)
    - 3.4. [Conexión Remota desde Windows](#34-conexión-remota-desde-windows)
4. [INFORME](#4-informe)
5. [CONCLUSIONES Y RECOMENDACIONES](#5-conclusiones-y-recomendaciones)

---

## 1. OBJETIVOS
**Crear, configurar y desplegar servidores HTTP en un entorno Linux (Ubuntu) utilizando el software Apache2, con la finalidad de comprender el ciclo de peticiones de red y la gestión de recursos web compartidos bajo protocolos estándar de comunicación.**
**Implementar servidores Samba dentro de sistemas operativos tipo Unix/Linux para establecer canales interactivos de transferencia de datos en red, permitiendo la interoperabilidad nativa y el intercambio seguro de archivos con plataformas Windows.**

---

## 2. MARCO TEÓRICO

La arquitectura cliente-servidor representa uno de los modelos de diseño más eficientes en las redes de comunicación modernas, permitiendo la distribución centralizada o distribuida de recursos dentro de un sistema operativo en red. Entre las aplicaciones más comunes de este entorno se destaca la implementación de servidores HTTP y de almacenamiento compartido, los cuales resuelven problemas críticos de disponibilidad y transferencia de datos.

Apache HTTP Server, o comúnmente denominado Apache, es un software de servidor web multiplataforma, de código abierto y completamente gratuito, desarrollado bajo el respaldo de la Apache Software Foundation. Este entorno se destaca por su versatilidad, escalabilidad y facilidad de configuración, posibilitando el alojamiento y entrega eficiente de sitios web mediante canales basados en los protocolos de red estándar HTTP y HTTPS. En sistemas derivados de Red Hat como RHEL 8 o CentOS 8, el demonio de este servicio opera bajo el nombre de `httpd`, mientras que en distribuciones de la familia Debian, como Ubuntu, se implementa y administra de forma predeterminada mediante el paquete conocido como `apache2`.

Por otra parte, la interoperabilidad de datos en redes con sistemas heterogéneos requiere el uso de herramientas capaces de unificar protocolos dispares entre arquitecturas de software disímiles. Samba surge como una solución libre y robusta que emula el protocolo de compartición de archivos e impresión de Microsoft Windows, históricamente conocido como SMB (Server Message Block) y renombrado en sus fases evolutivas como CIFS (Common Internet File System). Mediante el uso de Samba, las computadoras que ejecutan sistemas de tipo UNIX o Linux adquieren la capacidad técnica de integrarse de manera transparente en la infraestructura de red de Windows, actuando activamente como servidores de almacenamiento dedicados o interactuando en calidad de clientes autorizados dentro del dominio de red local.

---

## 3. PROCEDIMIENTO

### Servidor web

#### 1. Instalación de httpd

Instalación de Apache2 y configuración inicial del Firewall (UFW):

```bash
sudo apt install apache2
sudo ufw status
sudo ufw allow 'Apache'

sudo systemctl status apache2
<img width="460" height="394" alt="image" src="https://github.com/user-attachments/assets/99229f8b-cc05-4982-92e6-123d91378185" />


#### 2. Dirigirse hacia el navegador y colocar localhost

Ingresar a la parte del navegador para ver el apartado del localhost en Firefox:

<img width="659" height="404" alt="image" src="https://github.com/user-attachments/assets/195ff0fd-6bd3-4c12-aff5-d482cd480d31" />

