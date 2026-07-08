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
    - 3.1. [Servidor Web](#31-servidor-web)
    - 3.2. [Servidor de Archivos](#32-servidor-de-archivos)
4. [CONCLUSIONES Y RECOMENDACIONES](#5-conclusiones-y-recomendaciones)
5. [Referencias](#5-referencias)
6. [Uso de IA](#6-uso-de-ia)

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

---
### 3.1.Servidor web

#### 1. Instalación de httpd

Instalación de Apache2 y configuración inicial del Firewall (UFW):

```bash
sudo apt install apache2
sudo ufw status
sudo ufw allow 'Apache'

sudo systemctl status apache2
```
<img width="460" height="394" alt="image" src="https://github.com/user-attachments/assets/193a9e03-d67d-4946-bd03-8a0c3a4be1fa" />

#### 2. Dirigirse hacia el navegador y colocar localhost

Ingresar al navegador y escribir **localhost** en la barra de direcciones para comprobar que Apache está funcionando correctamente.

<img width="659" height="404" alt="image" src="https://github.com/user-attachments/assets/7444fdba-db9c-4551-9671-69807db6a784" />

#### 3. Descargar la página web y colocarla como `index.html`

Descargar la página web desde Internet y guardarla como **index.html** dentro del directorio **/var/www/html**, que es el directorio principal de Apache.

```bash
cd /var/www/html
sudo wget https://www.metropolitan-touring.com/galapagos/
sudo mv index.html index.html.bk
sudo mv index.html.1 index.html
```
<img width="638" height="218" alt="image" src="https://github.com/user-attachments/assets/4765e565-f2fa-46fc-819b-6e3eb0b82be0" />

#### 4. Verificar la página web en el navegador

Abrir el navegador e ingresar **localhost** en la barra de direcciones para comprobar que la nueva página web se muestra correctamente.

```text
http://localhost
```
<img width="886" height="498" alt="image" src="https://github.com/user-attachments/assets/9074092b-586e-4ffb-b5bc-0e76b858dfb2" />

#### 5. Acceder al servidor web desde la máquina física Windows

Desde la máquina física con Windows, abrir un navegador web e ingresar la dirección IP del servidor para verificar que el sitio web sea accesible desde otro equipo.

---

## 3.2.Servidor de archivos

#### 1. Instalación de Samba

Instalar el servicio **Samba** y verificar que el servicio **nmbd** se encuentre en ejecución.

Antes de instalar el paquete Samba, se actualizó el índice de paquetes del sistema con el comando sudo apt-get update, con el fin de asegurar que se descargue la versión más reciente disponible en los repositorios de Ubuntu. 

```bash
sudo apt-get update
sudo apt-get install samba
sudo systemctl status nmbd
```
<img width="875" height="492" alt="image" src="https://github.com/user-attachments/assets/b69e101b-ab00-4ce3-94e2-bc90dc201f62" />

A continuación, se instaló el paquete samba mediante sudo apt-get install samba. Durante la instalación se descargaron e instalaron las dependencias necesarias para el funcionamiento del servicio.

<img width="875" height="467" alt="image" src="https://github.com/user-attachments/assets/966e7f07-f522-4cc3-a332-41f2805d1ab3" />

Finalizada la instalación, se verificó que el daemon nmbd se encontrara activo con el comando sudo systemctl status nmbd. La salida confirma el estado active (running) del servicio, lo que indica que Samba quedó correctamente instalado y en ejecución.

<img width="875" height="464" alt="image" src="https://github.com/user-attachments/assets/4a105a74-63ed-4f54-aec4-7d637d43ef19" />


#### 2. Configuración de Samba

Crear el directorio compartido, abrir el archivo de configuración de Samba y agregar la configuración correspondiente al final del archivo.

```bash
sudo mkdir /samba
sudo vi /etc/samba/smb.conf
```

Se creó el directorio /samba, que sirve como base para el recurso compartido, mediante sudo mkdir /samba
<img width="451" height="95" alt="image" src="https://github.com/user-attachments/assets/f14d864b-b2fe-4090-8b16-3fc2b33c4012" />

Posteriormente se editó el archivo de configuración /etc/samba/smb.conf con sudo vi /etc/samba/smb.conf, agregando al final del fichero el bloque correspondiente al nuevo recurso compartido [samba-share], especificando el comentario, la ruta (path = /samba), permisos de escritura (read only = no) y visibilidad del recurso (browsable = yes).
<img width="875" height="331" alt="image" src="https://github.com/user-attachments/assets/496f885d-af47-4651-8033-789808b75aba" />

Después de configurar el archivo smb.conf, se creó el usuario del sistema samba (sudo useradd samba) y se estableció su contraseña de acceso a Samba con sudo smbpasswd -a samba. Luego se creó el subdirectorio /samba/public, se ajustó su propietario a nobody:nogroup, se otorgaron permisos de lectura/escritura/ejecución completos (chmod 0777) y se asignó el grupo sambashare. Finalmente se reinició el servicio con sudo systemctl restart smbd.service y se deshabilitó temporalmente el firewall con sudo ufw disable para permitir el acceso desde la red.
<img width="777" height="531" alt="image" src="https://github.com/user-attachments/assets/9d6ca6aa-e297-44fb-ae66-acb55120381f" />

#### 3. Verificar el funcionamiento

Acceder al apartado **Red** desde la máquina cliente, localizar el recurso compartido de Samba e ingresar el usuario y la contraseña configurados para comprobar que el acceso funciona correctamente.

```text
Usuario: <usuario_samba>
Contraseña: <contraseña_samba>
```

Desde el explorador de archivos (Nautilus) de la propia máquina virtual se accedió a la red local y se seleccionó el recurso compartido samba-share. El sistema solicitó las credenciales de autenticación, indicándose el usuario samba y la contraseña configurada previamente con smbpasswd, confirmando así que el recurso quedó correctamente publicado .
<img width="750" height="494" alt="image" src="https://github.com/user-attachments/assets/a66aa957-954d-49d4-a37b-bd776547ae1f" />

#### 4. Conectarse remotamente al recurso compartido

Desde la máquina con Windows, acceder al recurso compartido de Samba utilizando la dirección IP de la máquina virtual. Ingresar el usuario y la contraseña configurados, verificar el acceso y comprobar el intercambio de archivos entre ambos sistemas.

```text
\\192.168.56.101
```

- Ingresar el **usuario** y la **contraseña** de Samba.
  <img width="750" height="478" alt="image" src="https://github.com/user-attachments/assets/acaf12b9-aaae-442e-acd2-e3959fc4631c" />

- Copiar un archivo desde Windows hacia la carpeta compartida de la máquina virtual Ubuntu y verificar que se haya guardado correctamente.
  <img width="750" height="473" alt="image" src="https://github.com/user-attachments/assets/b436e4da-c71b-49f0-a130-3601f7fed45f" />

- Copiar un archivo en la carpeta compartida de Ubuntu (**public**) y comprobar que sea visible desde Windows.
  <img width="875" height="464" alt="image" src="https://github.com/user-attachments/assets/84391be5-d443-40d3-b838-7e9d4864378c" />

#### 5. Prueba de transferencia de archivos

Para comprobar la transferencia de archivos en el sentido Ubuntu → Windows, se creó un documento de texto (Practica 9 Samba.odt) directamente en la máquina virtual, guardándolo dentro de la carpeta compartida /samba/public mediante LibreOffice Writer.
<img width="875" height="464" alt="image" src="https://github.com/user-attachments/assets/454d0156-6bcf-4661-929a-85ec396a0e11" />

Al revisar la carpeta public del recurso samba-share desde el explorador de Windows, el archivo creado en la máquina virtual apareció disponible de forma inmediata, confirmando la correcta sincronización del recurso compartido.
<img width="750" height="478" alt="image" src="https://github.com/user-attachments/assets/6efdd272-b18b-4829-a105-500cf6edb5ef" />

Para comprobar la transferencia en el sentido inverso (Windows → Ubuntu), se copió el archivo Prac9SO_2026A.pdf desde el equipo físico hacia la misma carpeta compartida public.
<img width="750" height="478" alt="image" src="https://github.com/user-attachments/assets/ff6359d9-1c90-43fe-9539-66cd95e911e3" />

Finalmente, desde el gestor de archivos de la máquina virtual Ubuntu se verificó que el archivo PDF copiado desde Windows se encontraba disponible dentro de /samba/public, junto con el archivo creado previamente en la propia máquina virtual, confirmando la transferencia de archivos en ambos sentidos.
<img width="875" height="464" alt="image" src="https://github.com/user-attachments/assets/ea7b136b-e607-48db-9ce3-1b407c790875" />


## 4. Conclusiones y Recomendaciones

•	Samba permitió establecer una interoperabilidad efectiva entre el servidor GNU/Linux (Ubuntu Server) y el cliente Windows, cumpliendo su función principal de compartir archivos entre sistemas operativos distintos mediante el protocolo SMB.
•	La correcta configuración del archivo smb.conf, junto con los permisos del sistema de archivos (chown, chmod, chgrp) y la creación de un usuario Samba independiente, resultó indispensable para que el recurso compartido fuera accesible tanto en lectura como en escritura.
•	Se recomienda, para entornos reales, evitar deshabilitar el firewall por completo y en su lugar habilitar de forma selectiva los puertos requeridos por Samba, tal como se describió en la sección 4, con el fin de mantener un nivel adecuado de seguridad en el servidor.
•	La prueba de transferencia bidireccional de archivos confirmó el correcto funcionamiento del recurso compartido, validando tanto la configuración del servidor como la conectividad de red entre la máquina virtual y la máquina física.

## 5. Referencias
Martínez, D. (2026). Guía de Laboratorio: Servidores. Laboratorio de Sistemas Operativos, Facultad de Ingeniería en Sistemas, Escuela Politécnica Nacional. Recuperado de: https://aulasvirtuales.epn.edu.ec/pluginfile.php/16233892/mod_resource/content/6/Prac9SO_2026A.pdf

## 6. Uso de IA
Declaración de porcentaje de uso de IA: Se declara formalmente que en la elaboración de este informe de laboratorio se utilizó Inteligencia Artificial (modelo Gemini) en un estimado del 8%. La asistencia de la IA se limitó estrictamente a la estructuración del documento, corrección de estilo, ortografía y apoyo en la redacción formal del análisis teórico.

















