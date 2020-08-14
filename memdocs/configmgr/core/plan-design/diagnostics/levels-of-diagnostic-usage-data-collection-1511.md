---
title: Datos de diagnóstico de 1511
titleSuffix: Configuration Manager
description: Obtenga información sobre los niveles de datos de diagnóstico y uso que se recopilan en la versión 1511 de Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94166557b07050706401c122b835579762bfa982
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128838"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-configuration-manager"></a>Niveles de recopilación de datos de uso de diagnóstico de la versión 1511 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La versión 1511 de Configuration Manager recopila tres niveles de datos de diagnóstico y de uso: **Básico**, **Mejorado** y **Completo**. De forma predeterminada, esta característica se establece en el nivel Mejorado. Las secciones siguientes proporcionan detalles adicionales sobre los datos que recopila cada nivel.  

> [!IMPORTANT]  
>  Configuration Manager no recopila códigos de sitio, nombres de sitios, direcciones IP, nombres de usuario o equipo, direcciones físicas o direcciones de correo electrónico en los niveles Básico o Mejorado. Cualquier recopilación de esta información en el nivel Completo no tiene ninguna finalidad, es decir, potencialmente se incluye en la información avanzada de diagnóstico como archivos de registro o instantáneas de memoria. Microsoft no usará esta información para identificarle, para ponerse en contacto con usted ni para el desarrollo de publicidad.  

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Cómo cambiar el nivel  
 Los administradores que tienen un ámbito administrativo basado en roles que incluye los permisos **Modificar** en la clase de objeto **Sitio** pueden cambiar el nivel de datos recopilados en la configuración de datos de diagnóstico y uso de la consola de Configuration Manager.

 Para ello, en la consola, vaya a la pestaña Backstage (la pestaña superior izquierda con la flecha desplegable), seleccione **Datos de uso** y, después, seleccione el nivel de datos que quiere usar.  


##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivel 1: Básico  
 El nivel Básico incluye datos sobre la jerarquía, datos que son necesarios para ayudar a mejorar su experiencia de instalación o actualización, y datos que ayudan a determinar las actualizaciones de Configuration Manager que son aplicables a la jerarquía.  

 A partir de la versión 1511 de Configuration Manager, este nivel incluye lo siguiente:  


-   Información sobre la instalación
    - Compilación, tipo de instalación, paquetes de idioma y características que ha habilitado

    - Errores y estado de implementación del paquete de actualización  

-   Métricas de rendimiento de la base de datos (información del procesamiento de replicación, los principales procedimientos almacenados de SQL Server mediante el uso de procesador y disco)  

-   Configuración básica de la base de datos (procesadores, configuración de clúster y configuración de vistas distribuidas)  

-   Esquema de base de datos de Configuration Manager (hash de todas las definiciones de objeto)  

-   Recuento de versiones de cliente de Configuration Manager y versiones de sistema operativo  

-   Recuento de sistemas operativos de los dispositivos administrados y las directivas establecidas por Exchange Connector  

-   Recuento de idiomas de cliente y configuraciones regionales

-   Recuento de dispositivos Windows 10 por ramificación y compilación  

-   Datos básicos de la jerarquía del sitio de Configuration Manager (lista de sitios, tipo, versión, estado, número de cliente y zona horaria)  

-   Información básica del servidor de sistema de sitio (roles de sistema de sitio usados, estado de SSL y de Internet, sistema operativo, procesadores y máquina física o virtual)  

-   Estadísticas básicas de detección de usuarios (recuento de detección de usuarios y tamaños de grupo mínimo, máximo y promedio)  

-   Información básica de Endpoint Protection (versiones de cliente antimalware)  

-   Recuentos básicos de aplicación y tipo de implementación (aplicaciones totales, aplicaciones totales con varios tipos de implementación, aplicaciones totales con dependencias, aplicaciones totales reemplazadas y recuento de tecnologías de implementación en uso)  

-   Recuentos (imágenes) de implementación básica de sistema operativo (OSD)  

-   Tipos de puntos de distribución y puntos de administración e información básica de configuración (protegida, preconfigurada, PXE, multidifusión, estado de SSL, puntos de distribución de extracción o del mismo nivel, MDM habilitado, SSL habilitado, etc.)  

-   Estadísticas de telemetría (cuando se ejecutan, tiempo de ejecución y errores)  

##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivel 2: Mejorado  
El nivel Mejorado es el valor predeterminado después de que finalice la instalación. Este nivel incluye datos que se han recopilado en el nivel Básico, datos específicos de característica (frecuencia y duración de uso), configuración de cliente de Configuration Manager (nombre de componente, estado y determinadas opciones como intervalos de sondeo) e información básica sobre las actualizaciones de software.  

Se recomienda este nivel porque proporciona a Microsoft los datos mínimos que se necesitan para realizar mejoras útiles en versiones futuras de productos y servicios. En este nivel no se recopilan nombres de objetos (sitios, usuarios, equipos u objetos), detalles sobre objetos relacionados con la seguridad o vulnerabilidades como recuentos de sistemas que necesitan actualizaciones de software.  

A partir de la versión 1511 de Configuration Manager, este nivel incluye lo siguiente:  

-   **Administración de aplicaciones:**  

    -   Información básica de uso o destino para tipos de implementación que se usan en la organización (usuario frente a dispositivo de destino y necesario frente a disponible)  

    -   Información sobre la implementación de aplicaciones (instalación o desinstalación, necesita aprobación e interacción de usuario habilitada o deshabilitada)  

    -   Estadísticas de solicitudes de aplicación disponibles  

    -   Número de paquetes por tipo  

    -   Recuento de aplicabilidad de aplicación por sistema operativo  

    -   Recuento de implementaciones de paquete o programa  

    -   Recuentos de entornos de App-V y propiedades de implementación  

    -   Recuento de licencias de aplicación con licencia de Windows 10  

    -   Número mínimo y máximo y promedio de implementaciones de aplicaciones por usuario o dispositivo  

    -   Duración y el tipo de ventana de mantenimiento  

-   **Cliente:**  

    -   Lista o recuento de agentes de cliente habilitados  

    -   Recuento de instalaciones de cliente de cada tipo de ubicación de origen  

    -   Recuento de errores de instalación de cliente  

-   **Configuración de cumplimiento:**  

    -   Recuento de elementos de configuración por tipo o  

    -   Información básica de línea de base de configuración (recuento, número de implementaciones y número de referencias)  

    -   Recuento de las implementaciones que hacen referencia a valores integrados (no se captura el valor de configuración)  

    -   Recuento de reglas e implementaciones que se han creado para la configuración personalizada  

    -   Recuento de plantillas implementadas del Protocolo de inscripción de certificados simple  

-   **Contenido:**  

    -   Recuento de límites por tipo  

    -   Información de grupo de límites (recuento de límites y sistemas de sitio que se han asignado a cada grupo de límites)  

    -   Información de grupo de puntos de distribución (recuento de paquetes y puntos de distribución que se han asignado a cada grupo de puntos de distribución)  

    -   Información de configuración de punto de distribución (uso de BranchCache y supervisión de punto de distribución)  

    -   Información de configuración del administrador de distribuciones (subprocesos, intervalo de reintentos, número de reintentos y configuración de punto de distribución de extracción)  

-   **Endpoint Protection:**  

    -   Uso de la directiva de Firewall de Windows y de antimalware de Endpoint Protection (número de directivas únicas asignadas al grupo)<br /><br />Esto no incluye ninguna información sobre la configuración que se incluye en la directiva.  

    -   Errores de implementación de Endpoint Protection (recuento de códigos de error de implementación de directivas de Endpoint Protection)  

    -   Recuento de recopilaciones que se han seleccionado para que aparezcan en el panel de Endpoint Protection  

    -   Recuento de alertas que se han configurado para la característica de Endpoint Protection  

-   **Administración de aplicaciones móviles (MAM)**  

    -   Recuento de aplicaciones Office con MAM habilitado, aplicaciones de línea de negocio y directivas por sistema operativo  

    -   Recuento de implementaciones de directiva de aplicación MAM  

    -   Recuento de reglas que se han creado por la configuración de MAM  

-   **Administración de dispositivos móviles (MDM)**  

    -   Recuento de acciones de dispositivo móvil emitidas: bloquear, restablecer PIN, borrar y retirar comandos

    -   Recuento de dispositivos móviles que se administran por Configuration Manager y Microsoft Intune, así como la forma en que se inscribieron (masiva o basada en el usuario)  

    -   Duración de la comprobación de estadísticas y programación de sondeo de dispositivos móviles  

    -   Recuento de directivas de dispositivos móviles  

    -   Recuento de usuarios que tienen varios dispositivos móviles inscritos  

-   **Solución de problemas de Microsoft Intune:**  

    -   Recuento y tamaño de los mensajes de estado, condición, inventario, RDR, DDR, UDX, estado de inquilino, POL, LOG, certificado, CRP, resincronización, CFD, RDO, BEX, ISM y de cumplimiento que se han descargado de Microsoft Intune  

    -   Recuento y tamaño de los mensajes de acciones de dispositivo (borrar, retirar, bloquear), telemetría y de datos que se replican en Microsoft Intune  

    -   Estadísticas de sincronización de usuario completas y diferenciales para Microsoft Intune  

-   **Administración local de dispositivos móviles (MDM):**  

    -   Estadísticas de implementaciones correctas o con errores para las implementaciones locales de aplicaciones MDM  

    -   Recuento de perfiles y paquetes de inscripción masiva de Windows 10  

-   **Implementación de sistema operativo:**  

    -   Recuento de imágenes de arranque, controladores, paquetes de controladores, puntos de distribución habilitados para multidifusión, puntos de distribución habilitados para PXE y secuencias de tareas  

-   **Actualizaciones de software:**  

    -   Número total o promedio de recopilaciones que tienen implementaciones de actualización de software y el número máximo o promedio de actualizaciones implementadas  

    -   Número de reglas de implementación automática que están asociadas a la sincronización  

    -   Número de reglas de implementación automática que crean actualizaciones nuevas o agregan otras a un grupo existente  

    -   Diferencias disponibles y de fecha límite que se han usado en reglas de implementación automática  

    -   Número promedio y máximo de las asignaciones por actualización  

    -   Recuento de actualizaciones creadas e implementadas con System Center Updates Publisher  

    -   Recuento de grupos de actualizaciones y asignaciones  

    -   Recuento de paquetes de actualización y el número mínimo, máximo y promedio de puntos de distribución de destino con paquetes  

    -   Número de grupos de actualizaciones y número mínimo, máximo y promedio de actualizaciones por grupo  

    -   Número de actualizaciones y porcentaje de las actualizaciones que se han implementado, caducado, sustituido, descargado y que contienen términos de licencia  

    -   Códigos de error de búsqueda de actualizaciones y recuento de máquinas  

    -   Evaluación de actualizaciones de cliente y programaciones de búsquedas  

    -   Programación de la sincronización del punto de actualización de software  

    -   Número de reglas de implementación automática que tienen varias implementaciones  

    -   Configuraciones que se usan para planes de mantenimiento activos de Windows 10  

    -   Versiones de contenido del panel de Windows 10  

    -   Recuento de clientes de Windows 10 que usan Windows Update for Business  

    -   Estadísticas de aplicación de revisiones de clúster  

    -   Recuento de actualizaciones implementadas de Office 365  

-   **Datos de SQL o de rendimiento:**  

    -   Recuento de tablas de base de datos más grandes  

    -   Información de réplicas siempre activadas de SQL  

    -   Recuento de recopilaciones por tipo  

##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivel 3: Completo  
El nivel Completo incluye todos los datos de los niveles Básico y Mejorado. También incluye información adicional sobre Endpoint Protection, porcentajes de cumplimiento de actualización e información de actualización de software. Este nivel también puede incluir información avanzada de diagnóstico como archivos del sistema e instantáneas de memoria que pueden incluir información personal que existía en los archivos de registro o de memoria en el momento de la captura.  

A partir de la versión 1511 de Configuration Manager, este nivel incluye lo siguiente:  

-   Evaluación de recopilación y estadísticas de actualización  

-   Resumen de estado de Endpoint Protection (incluido el recuento de clientes protegidos, en peligro, desconocidos y no admitidos)  

-   Configuración de directivas de Endpoint Protection  

-   Información de implementación de actualización de software (porcentaje de implementaciones de destino con cliente frente a hora UTC, necesaria frente a opcional frente a silenciosa y supresión de reinicio)  

-   Cumplimiento general de las implementaciones de actualizaciones de software.  

-   Información de la programación de evaluación de reglas de implementación automática  

-   Número de clientes que tienen directivas de protección de acceso a la red  

-   Recuentos y códigos de error de implementación de actualizaciones de software  

-   Número mínimo, máximo y promedio de clientes inactivos en recopilaciones de implementación de actualizaciones de software  

-   Recuento de grupos que tienen actualizaciones de software caducadas  

-   Número mínimo, máximo y promedio de actualizaciones de software por paquete  

-   Porcentajes de éxito de búsqueda de actualizaciones de software  

-   Número mínimo, máximo y promedio de horas desde la última búsqueda de actualizaciones de software  
