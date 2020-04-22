---
title: Datos de diagnóstico de 1702
titleSuffix: Configuration Manager
description: Obtenga información sobre los niveles de datos de diagnóstico y uso que se recopilan en la versión 1702 de Configuration Manager.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d43ab033-2902-4681-8716-b4b17a6df372
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 155d62b3b8876f3bdf7dab218451c38e7cca6aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81698133"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1702-of-configuration-manager"></a>Niveles de recopilación de datos de uso de diagnóstico de la versión 1702 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La versión 1702 de Configuration Manager recopila tres niveles de datos de diagnóstico y de uso: **Básico**, **Mejorado** y **Completo**. De forma predeterminada, esta característica se establece en el nivel Mejorado. En las secciones siguientes se proporcionan detalles adicionales sobre los datos que recopila cada nivel.

Los cambios respecto de versiones anteriores se indican mediante la nota ***[Nuevo]***, ***[Actualizado]***, ***[Quitado]*** o ***[Movido]***.


> [!IMPORTANT]
>  Configuration Manager no recopila códigos de sitio, nombres de sitios, direcciones IP, nombres de usuario o equipo, direcciones físicas o direcciones de correo electrónico en los niveles Básico o Mejorado. Cualquier recopilación de esta información en el nivel Completo no tiene ninguna finalidad, es decir, potencialmente se incluye en la información avanzada de diagnóstico como archivos de registro o instantáneas de memoria. Microsoft no usará esta información para identificarle, para ponerse en contacto con usted ni para el desarrollo de publicidad.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Cómo cambiar el nivel
 Los administradores que tienen un ámbito administrativo basado en roles que incluye los permisos **Modificar** en la clase de objeto **Sitio** pueden cambiar el nivel de datos recopilados en la configuración de datos de diagnóstico y uso de la consola de Configuration Manager.

Cambie el nivel de recopilación de datos desde la consola; para ello, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**. Abra **Configuración de jerarquía** y, después, seleccione el nivel de datos que quiere usar.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivel 1: Básico
El nivel Básico incluye datos sobre la jerarquía, datos que son necesarios para ayudar a mejorar su experiencia de instalación o actualización, y datos que ayudan a determinar las actualizaciones de Configuration Manager que son aplicables a la jerarquía.

En el caso de la versión 1702 de Configuration Manager, este nivel incluye lo siguiente:

- Consola de administración:
   - Estadísticas sobre las conexiones de consola (versión de sistema operativo, idioma, SKU y arquitectura; memoria del sistema, número de procesadores lógicos, identificador de sitio de conexión, versiones instaladas de .NET y paquetes de idioma de la consola)

- Recuentos básicos de aplicación y tipo de implementación (aplicaciones totales, aplicaciones totales con varios tipos de implementación, aplicaciones totales con dependencias, aplicaciones totales reemplazadas y recuento de tecnologías de implementación en uso)

- Datos básicos de la jerarquía del sitio de Configuration Manager (lista de sitios, tipo, versión, estado, número de cliente y zona horaria)

- Configuración básica de la base de datos (procesadores, configuración de clúster y configuración de vistas distribuidas)

- ***[Actualizado]*** Estadísticas básicas de detección (recuento de detección y tamaños de grupo mínimo/máximo/medio) incluidas cuando el sitio se ejecuta completamente con los servicios de Azure Active Directory.

- Información básica de Endpoint Protection (versiones de cliente antimalware)

- Recuentos (imágenes) de implementación básica de sistema operativo (OSD)

- Información básica del servidor de sistema de sitio (roles de sistema de sitio usados, estado de SSL y de Internet, sistema operativo, procesadores y máquina física o virtual)

- Esquema de base de datos de Configuration Manager (hash de todas las definiciones de objeto)

- Nivel configurado de telemetría, modo (en línea o sin conexión) y configuración de actualización rápida

- Recuento de idiomas de cliente y configuraciones regionales

- Recuento de versiones de cliente de Configuration Manager y versiones de sistema operativo

- Recuento de sistemas operativos de los dispositivos administrados y las directivas establecidas por Exchange Connector

- Recuento de dispositivos Windows 10 por ramificación y compilación

- Métricas de rendimiento de la base de datos (información del procesamiento de replicación, los principales procedimientos almacenados de SQL Server mediante el uso de procesador y disco)

- Tipos de puntos de distribución y puntos de administración e información básica de configuración (protegida, preconfigurada, PXE, multidifusión, estado de SSL, puntos de distribución de extracción o del mismo nivel, MDM habilitado, SSL habilitado, etc.)

- Información sobre la instalación:
     - Compilación, tipo de instalación, paquetes de idioma, características que ha habilitado   

     - Uso de versión preliminar, tipo de medio de instalación, tipo de rama

     - Fecha de expiración de Software Assurance      

     - Estado y errores de la implementación del paquete de actualización, progreso de la descarga y errores de requisitos previos 

     - Uso del anillo rápido de actualización

     - Versión del script posterior a la actualización

- Versión de SQL, nivel de Service Pack, edición, identificador de intercalación y juego de caracteres     
- Estadísticas de telemetría (cuando se ejecutan, tiempo de ejecución, errores)

- Uso de la detección de redes (habilitada o deshabilitada)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivel 2: Mejorado
El nivel Mejorado es el valor predeterminado después de que finalice la instalación. Este nivel incluye datos que se han recopilado en el nivel Básico, datos específicos de característica (frecuencia y duración de uso), configuración de cliente de Configuration Manager (nombre de componente, estado y determinadas opciones como intervalos de sondeo) e información básica sobre las actualizaciones de software.

Se recomienda este nivel porque proporciona a Microsoft los datos mínimos que se necesitan para realizar mejoras útiles en versiones futuras de productos y servicios. En este nivel no se recopilan nombres de objetos (sitios, usuarios, equipos u objetos), detalles de objetos relacionados con la seguridad o vulnerabilidades como recuentos de sistemas que necesitan actualizaciones de software.

En el caso de la versión 1702 de Configuration Manager, este nivel incluye lo siguiente:

- **Administración de aplicaciones:**  

   - Requisitos de la aplicación (cantidad de condiciones integradas a las que se hace referencia por la tecnología de implementación)

   - Sustitución de aplicación, profundidad máxima de cadena

   - Estadísticas de aprobación de aplicaciones y frecuencia de uso

   - ***[Actualizado]*** Información sobre la implementación de aplicaciones (instalación o desinstalación, necesita aprobación, interacción de usuario habilitada o deshabilitada, dependencia, sustitución y recuento de uso de la característica de comportamiento de instalación)  

   - Estadísticas de tamaño y la complejidad de directivas de aplicación

   - Estadísticas de solicitudes de aplicación disponibles

   - ***[Nuevo]*** Información de configuración básica para los paquetes y programas (opciones de implementación y marcas de programa)

   - Información básica de uso o destino para tipos de implementación que se usan en la organización (usuario frente a dispositivo de destino, necesario frente a disponible y aplicaciones universales)

   - Estadísticas de grupo de límites (cuántas rápidas, cuántas lentas y cantidad por grupo)

   - Recuentos de entornos de App-V y propiedades de implementación

   - Recuento de aplicabilidad de aplicación por sistema operativo  

   - ***[Nuevo]*** Número de aplicaciones a las que la secuencia de tareas hace referencia

   - Número de paquetes por tipo  

   - Recuento de implementaciones de paquete o programa  

   - Recuento de licencias de aplicación con licencia de Windows 10  

   - Recuento de las aplicaciones de la Tienda Windows para empresas y estadísticas de sincronización (incluidos los tipos resumidos de aplicaciones, el estado de la aplicación con licencia y el número de aplicaciones con licencia en línea y sin conexión)  

   - Duración y el tipo de ventana de mantenimiento  

   - Número mínimo y máximo y promedio de implementaciones de aplicaciones por usuario o dispositivo por período de tiempo

   - ***[Nuevo]*** Códigos de error de instalación de aplicación más comunes según la tecnología de implementación

   - Recuentos y opciones de configuración de MSI

   - ***[Nuevo]*** Estadísticas sobre la interacción del usuario final con la notificación para las implementaciones de software necesario   

   - Uso del Acceso universal a datos (UDA), cómo se ha creado




- **Cliente:**  

   - Versión de cliente de la Tecnología de administración activa (AMT)

   - Antigüedad del BIOS en años

   - Actualización automática de cliente: la configuración de implementación incluido el piloto de cliente y el uso de exclusión (cliente de interoperabilidad extendida)

   - Configuración del tamaño de la caché de cliente

   - Errores de descarga de implementación de cliente

   - Resumen de problemas principales y estadísticas de estado de cliente

   - Estado de acción de operación de notificación de cliente (cantidad de ejecución de cada uno, número máximo de clientes de destino y tasa de éxito en promedio)
   - Recuento de instalaciones de cliente de cada tipo de ubicación de origen  

   - Recuento de errores de instalación de cliente  

   - ***[Nuevo]*** Recuento de dispositivos virtualizados por Hyper-V o Azure  

   - Acciones de recuento de Centro de Software   

   - ***[Nuevo]*** Recuento de dispositivos habilitados para UEFI

   - Métodos de implementación usados para el cliente y número de clientes por método de implementación

   - Lista o recuento de agentes de cliente habilitados  

   - Antigüedad del sistema operativo en meses

   - Número de clases de inventario de hardware, reglas de inventario de software y reglas de recopilación de archivos

   - ***[Nuevo]***  Estadísticas de atestación de estado de dispositivo, incluidos los códigos de errores más comunes, el número de servidores locales y los recuentos de dispositivos en varios estados.



- **Cloud Services:**

  - Estadísticas de uso y configuración de Cloud Management Gateway

  - ***[Nuevo]*** Recuento de clientes unidos a servicios de Azure Active Directory

  - Recuento de recopilaciones sincronizadas con Operations Management Suite

  - Recuento de conectores de Upgrade Analytics

  - Si el conector en la nube de Operations Management Suite está habilitado




- **Recopilaciones:**

    - Uso de identificador de recopilación (que no se ejecuta sin los identificadores)

    - Estadísticas de evaluación de la recopilación (tiempo de consulta, cantidades asignadas frente a cantidades sin asignar, recuentos por tipo, sustitución de identificador y uso de reglas)

    - Recopilaciones sin una implementación




- **Configuración de cumplimiento:**  

    - Información básica de línea de base de configuración (recuento, número de implementaciones y número de referencias)  

    - Recuento de elementos de configuración por tipo o  

    - Recuento de implementaciones que hacen referencia a valores integrados (capturando ahora la configuración de corrección)  

    - Recuento de reglas e implementaciones creadas para la configuración personalizada (capturando ahora la configuración de corrección)  
    -  Recuento de Protocolo de inscripción de certificados simple (SCEP), VPN, Wi-Fi, certificado (.pfx) y plantillas de directiva de cumplimiento implementadas

    - Recuento de certificado SCEP, VPN, Wi-Fi, certificado (.pfx) e implementaciones de directiva de cumplimiento por plataforma

    - Directiva de Passport for Work (creación, implementación)



- **Contenido:**  

    - Información de grupo de límites (recuento de límites y sistemas de sitio que se han asignado a cada grupo de límites)  

    - Relaciones de grupo de límites y configuración de reserva

    - Estadísticas de descarga del contenido de cliente

    - Recuento de límites por tipo  

    - Recuento de clientes de almacenamiento en caché del mismo nivel y estadísticas de uso

    - Información de configuración del administrador de distribuciones (subprocesos, intervalo de reintentos, número de reintentos y configuración de punto de distribución de extracción)  

    - Información de configuración de punto de distribución (uso de BranchCache y supervisión de punto de distribución)

    - Información de grupo de puntos de distribución (recuento de paquetes y puntos de distribución que se han asignado a cada grupo de puntos de distribución)  



- **Endpoint Protection:**  

   - Directivas de protección contra amenazas avanzada (ATP) (recuento de directivas y si las directivas se implementan)

   - Recuento de alertas que se han configurado para la característica de Endpoint Protection  

   - Recuento de recopilaciones que se han seleccionado para que aparezcan en el panel de Endpoint Protection  

   - Errores de implementación de Endpoint Protection (recuento de códigos de error de implementación de directivas de Endpoint Protection)  

   - Uso de la directiva de Firewall de Windows y de antimalware de Endpoint Protection (número de directivas únicas asignadas al grupo)<br /><br /> Esto no incluye ninguna información sobre la configuración incluida en la directiva.  



- **Migración:**

  - Recuento de objetos migrados (uso del Asistente para migración)



- **Administración de dispositivos móviles (MDM)**  

    - Recuento de acciones de dispositivo móvil: comandos bloquear, restablecer PIN, borrar, retirar y sincronizar ahora

    - Recuento de directivas de dispositivos móviles  

    - Recuento de dispositivos móviles que se administran por Configuration Manager y Microsoft Intune, así como la forma en que se inscribieron (masiva, basada en el usuario)  

    - Recuento de usuarios que tienen varios dispositivos móviles inscritos  

    - Duración de la comprobación de estadísticas y programación de sondeo de dispositivos móviles  




- **Solución de problemas de Microsoft Intune:**

    - Recuento y tamaño de los mensajes de acciones de dispositivo (borrar, retirar, bloquear), telemetría y de datos que se replican en Microsoft Intune

    - Recuento y tamaño de los mensajes de estado, condición, inventario, RDR, DDR, UDX, estado de inquilino, POL, LOG, certificado, CRP, resincronización, CFD, RDO, BEX, ISM y de cumplimiento que se han descargado de Microsoft Intune

    - Estadísticas de sincronización de usuario completas y diferenciales para Microsoft Intune



- **Administración local de dispositivos móviles (MDM):**  

    - Recuento de perfiles y paquetes de inscripción masiva de Windows 10  

    - Estadísticas de implementaciones correctas o con errores para las implementaciones locales de aplicaciones MDM  




- **Implementación de sistema operativo:**  

    - Recuento de imágenes de arranque, controladores, paquetes de controladores, puntos de distribución habilitados para multidifusión, puntos de distribución habilitados para PXE y secuencias de tareas  

    - Recuento de directivas de actualización de edición

    - Recuentos de uso de paso de secuencia de tareas



- **Actualizaciones de sitios:**

    - Versiones de revisiones instaladas de Configuration Manager



- **Actualizaciones de software:**  

    - Diferencias disponibles y de fecha límite que se han usado en reglas de implementación automática  

    - Número promedio y máximo de las asignaciones por actualización  

    - Evaluación de actualizaciones de cliente y programaciones de búsquedas  

    - Clasificaciones que se sincronizan por punto de actualización de software

    - Estadísticas de aplicación de revisiones de clúster  

    - Configuración de las actualizaciones rápidas de Windows 10

    - Configuraciones que se usan para planes de mantenimiento activos de Windows 10  

    - Recuento de actualizaciones implementadas de Office 365  

    - Recuento de grupos de actualizaciones y asignaciones  

    - Recuento de paquetes de actualización y el número mínimo, máximo y promedio de puntos de distribución de destino con paquetes  

    - Recuento de actualizaciones que se crean e implementan con System Center Updates Publisher  

    - Recuento de clientes de Windows 10 que usan Windows Update for Business  

    - Número de reglas de implementación automática que están asociadas a la sincronización  

    - Número de reglas de implementación automática que crean actualizaciones nuevas o agregan otras a un grupo existente  

    - Número de reglas de implementación automática que tienen varias implementaciones  
    - Número de grupos de actualizaciones y número mínimo, máximo y promedio de actualizaciones por grupo  

    - Número de actualizaciones y porcentaje de las actualizaciones que se han implementado, caducado, sustituido, descargado y que contienen términos de licencia  

    - Estadísticas de equilibrio de carga de punto de actualización de software

    - Programación de la sincronización del punto de actualización de software  

    - Número total o promedio de recopilaciones que tienen implementaciones de actualización de software y el número máximo o promedio de actualizaciones implementadas  

    - Códigos de error de búsqueda de actualizaciones y recuento de máquinas  

    - Versiones de contenido del panel de Windows 10  



- **Datos de SQL o de rendimiento:**  

    - ***[Nuevo]*** Configuración y duración del resumen de sitio

    - Recuento de tablas de base de datos más grandes  

    - Estadísticas operativas de detección (recuento de objetos detectados)

    - Tipos de detección, habilitados y programación (completa, incremental)

    - Estado de mantenimiento, uso e información de réplica de SQL AlwaysOn

    - Problemas de rendimiento del seguimiento de cambios de SQL, período de retención y estado de limpieza automática

    - Período de retención de seguimiento de cambios de SQL

    - ***[Nuevo]*** Estado y estadísticas de rendimiento de mensajes de estado, incluidos los tipos de mensajes más caros y más comunes



- **Varios**

    - ***[Nuevo]*** Configuración del Punto de servicio de Almacenamiento de datos, incluidos el programa de sincronización y el tiempo promedio

    - Recuento de sitios con Wake On Lan (WOL)

    - Informes de uso y estadísticas de rendimiento  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivel 3: Completo
El nivel Completo incluye todos los datos de los niveles Básico y Mejorado. También incluye información adicional sobre Endpoint Protection, porcentajes de cumplimiento de actualización e información de actualización de software.  Este nivel también puede incluir información avanzada de diagnóstico como archivos del sistema e instantáneas de memoria que pueden incluir información personal que existía en los archivos de registro o de memoria en el momento de la captura.

En el caso de la versión 1702 de Configuration Manager, este nivel incluye lo siguiente:

- Información de la programación de evaluación de reglas de implementación automática

- Resumen de estado de ATP

- Evaluación de recopilación y estadísticas de actualización

- Configuración de cumplimiento: SCEP, VPN, Wi-Fi y detalles de configuración de plantilla de directiva de cumplimiento Recuento de grupos que tienen actualizaciones de software caducadas

- Módulo de configuración de DCM para el uso de Configuration Manager

- Errores de instalación de implementación de cliente detallados
- Resumen de estado de Endpoint Protection (incluido el recuento de clientes protegidos, en peligro, desconocidos y no admitidos)

- Configuración de directivas de Endpoint Protection

- ***[Nuevo]*** Lista de procesos configurados con el comportamiento de la instalación de aplicaciones

- Número mínimo, máximo y promedio de horas desde la última búsqueda de actualizaciones de software

- Número mínimo, máximo y promedio de clientes inactivos en recopilaciones de implementación de actualizaciones de software

- Número mínimo, máximo y promedio de actualizaciones de software por paquete

- Código de producto de MSI (aplicaciones comunes que los clientes implementan)

- Cumplimiento general de las implementaciones de actualizaciones de software.

- Recuentos y códigos de error de implementación de actualizaciones de software

- Información de implementación de actualización de software (porcentaje de implementaciones de destino con cliente frente a hora UTC, necesaria frente a opcional frente a silenciosa y supresión de reinicio)

- Productos de actualización de software sincronizados por punto de actualización de software

- Porcentajes de éxito de búsqueda de actualizaciones de software

- Primeras 50 CPU en el entorno

- Tipo de directivas de acceso condicional de EAS (bloquear o cuarentena) para dispositivos que administra Intune

- Detalles de la aplicación de la Tienda Windows para empresas (lista no agregada de aplicaciones sincronizadas, incluido AppID, el estado en línea o sin conexión y el recuento total de licencias adquiridas)
