---
title: Datos de uso y diagnóstico para la versión 1802
titleSuffix: Configuration Manager
description: Obtenga información sobre los niveles de diagnóstico y datos de uso recopilados en la versión 1802.
ms.date: 05/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 29dd51b8-6576-4010-81ba-3129ed2c3421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bae73e89852efbc8e85ba4df7e98eb0452d6b754
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128736"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1802-of-configuration-manager"></a>Niveles de recopilación de datos de uso de diagnóstico de la versión 1802 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La versión 1802 de Configuration Manager recopila tres niveles de datos de diagnóstico y uso: **Básico**, **Mejorado** y **Completo**. De forma predeterminada, esta característica se establece en el nivel Mejorado. En las secciones siguientes se proporcionan detalles adicionales sobre los datos que se recopilan en cada nivel.

Los cambios respecto de versiones anteriores se indican mediante la nota ***[Nuevo]***, ***[Actualizado]***, ***[Quitado]*** o ***[Movido]***.


> [!IMPORTANT]
>  Configuration Manager no recopila códigos de sitio, nombres de sitios, direcciones IP, nombres de usuario o equipo, direcciones físicas o direcciones de correo electrónico en los niveles Básico o Mejorado. Cualquier recopilación de esta información en el nivel Completo no tiene ninguna finalidad. Se incluye potencialmente en la información de diagnóstico avanzada como archivos de registro o instantáneas de memoria. Microsoft no usa esta información para identificarle, para ponerse en contacto con usted ni para el desarrollo de publicidad.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Cómo cambiar el nivel
 Los administradores que tienen un ámbito administrativo basado en roles que incluye los permisos **Modificar** en la clase de objeto **Sitio** pueden cambiar el nivel de datos recopilados en la configuración de datos de diagnóstico y uso de la consola de Configuration Manager.

Cambie el nivel de recopilación de datos desde la consola; para ello, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**. Abra **Configuración de jerarquía** y, después, seleccione el nivel de datos que quiere usar.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivel 1: Básico
El nivel Básico incluye datos sobre la jerarquía, datos que son necesarios para ayudar a mejorar su experiencia de instalación o actualización, y datos que ayudan a determinar las actualizaciones de Configuration Manager que son aplicables a la jerarquía.

Para la versión 1802 de Configuration Manager, este nivel incluye los datos siguientes:

- Estadísticas sobre las conexiones de la consola de Configuration Manager: versión de SO, idioma, SKU y arquitectura; memoria del sistema, número de procesadores lógicos, identificador de sitio de conexión, versiones instaladas de .NET y paquetes de idioma de la consola

- Recuentos básicos de aplicación y tipo de implementación: aplicaciones totales, aplicaciones totales con varios tipos de implementación, aplicaciones totales con dependencias, aplicaciones totales reemplazadas y recuento de tecnologías de implementación en uso.

- Datos básicos de la jerarquía del sitio de Configuration Manager: lista de sitios, tipo, versión, estado, número de cliente y zona horaria.

- Configuración básica de la base de datos: procesadores, configuración de clúster y configuración de vistas distribuidas.

- Estadísticas básicas de detección: recuento de detección y tamaños de grupo mínimo/máximo/medio, y cuándo se ejecuta completamente el sitio con los servicios de Azure Active Directory.

- Información básica de Endpoint Protection sobre las versiones de cliente antimalware.

- Recuentos de implementación del sistema operativo básico de imágenes.

- Información básica del servidor de sistema de sitio: roles de sistema de sitio usados, estado de SSL y de Internet, sistema operativo, procesadores, máquina física o virtual, y uso de alta disponibilidad de servidor de sitio.

- Esquema de base de datos de Configuration Manager (hash de todas las definiciones de objeto)

- Nivel configurado de telemetría, modo en línea o sin conexión, y configuración de actualización rápida.

- Recuento de idiomas de cliente y configuraciones regionales

- Recuento de versiones de cliente de Configuration Manager y versiones de sistema operativo u Office.

- Recuento de sistemas operativos de los dispositivos administrados y las directivas establecidas por Exchange Connector

- Recuento de dispositivos Windows 10 por ramificación y compilación

- ***[Movido]*** Recuento de clientes de Windows 10 que usan Windows Update for Business.  

- Métricas de rendimiento de la base de datos: información del procesamiento de replicación, los principales procedimientos almacenados de SQL Server por procesador y uso de disco.

- Tipos de puntos de distribución y puntos de administración, e información básica de configuración: protegida, preconfigurada, PXE, multidifusión, estado de SSL, puntos de distribución de extracción o del mismo nivel, MDM habilitado, SSL habilitado.

- Lista de extensiones con hash de asistentes y páginas de propiedades de consola

- Información sobre la instalación:
     - Compilación, tipo de instalación, paquetes de idioma, características que ha habilitado   

     - Uso de versión preliminar, tipo de medio de instalación, tipo de rama

     - Fecha de expiración de Software Assurance      

     - Estado y errores de la implementación del paquete de actualización, progreso de la descarga y errores de requisitos previos 

     - Uso del anillo rápido de actualización

     - Versión del script posterior a la actualización

- Versión de SQL, nivel de Service Pack, edición, identificador de intercalación y juego de caracteres     

- Estadísticas de telemetría: cuándo se ejecutan, tiempo de ejecución, errores.

- Si la detección de redes está habilitada o deshabilitada.

- ***[Movido]*** Recuento de clientes unidos a Azure Active Directory.

- ***[Nuevo]*** Recuento de las implementaciones por fases creadas por tipo.

- ***[Nuevo]*** Recuento de clientes de interoperabilidad extendida.

- ***[Nuevo]*** Lista con hash de propiedades de inventario de hardware de más de 255 caracteres.



##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivel 2: Mejorado
El nivel Mejorado es el valor predeterminado después de que finalice la instalación. Este nivel incluye datos que se han recopilado en el nivel Básico, datos específicos de característica (frecuencia y duración de uso), configuración de cliente de Configuration Manager (nombre de componente, estado y determinadas opciones como intervalos de sondeo) e información básica sobre las actualizaciones de software.

Se recomienda este nivel porque proporciona a Microsoft los datos mínimos que se necesitan para realizar mejoras útiles en versiones futuras de productos y servicios. En este nivel no se recopilan nombres de objetos (sitios, usuarios, equipos u objetos), detalles de objetos relacionados con la seguridad o vulnerabilidades como recuentos de sistemas que necesitan actualizaciones de software.

Para la versión 1802 de Configuration Manager, este nivel incluye los datos siguientes:

### <a name="application-management"></a>Administración de aplicaciones  

- Requisitos de la aplicación: recuento de condiciones integradas a las que se hace referencia por la tecnología de implementación.

- Sustitución de aplicación, profundidad máxima de cadena

- Estadísticas de aprobación de aplicaciones y frecuencia de uso

- Estadísticas de tamaño del contenido de la aplicación

- Información sobre la implementación de aplicaciones: uso de instalación o desinstalación, necesita aprobación, interacción del usuario habilitada o deshabilitada, dependencia, sustitución y recuento de uso de la característica de comportamiento de instalación.  

- Estadísticas de tamaño y la complejidad de directivas de aplicación

- Estadísticas de solicitudes de aplicación disponibles

- Información de configuración básica para los paquetes y programas: opciones de implementación y marcas de programa.

- Información básica de uso o destino para tipos de implementación: usuario frente a dispositivo de destino, necesario frente a disponible y aplicaciones universales.

- Recuentos de entornos de App-V y propiedades de implementación

- Recuento de aplicabilidad de aplicación por sistema operativo.  

- Número de aplicaciones a las que la secuencia de tareas hace referencia

- Recuento de personalizaciones de marca distintivas de catálogo de aplicaciones

- Recuento de aplicaciones de Office 365 creadas con el panel

- Número de paquetes por tipo  

- Recuento de implementaciones de paquete o programa  

- Recuento de licencias de aplicación con licencia de Windows 10  

- Recuento de tipos de implementación de Windows Installer por configuración de contenido de desinstalación

- Recuento de las aplicaciones de Microsoft Store para Empresas y estadísticas de sincronización: tipos resumidos de aplicaciones, estado de la aplicación con licencia y número de aplicaciones con licencia en línea y sin conexión.  

- Duración y el tipo de ventana de mantenimiento  

- Número mínimo y máximo y promedio de implementaciones de aplicaciones por usuario o dispositivo por período de tiempo

- Códigos de error de instalación de aplicación más comunes según la tecnología de implementación

- Recuentos y opciones de configuración de MSI

- Estadísticas sobre la interacción del usuario final con la notificación para las implementaciones de software necesario   

- Uso del Acceso universal a datos, cómo se ha creado.

- ***[Nuevo]*** Estadísticas acumuladas de afinidad de dispositivo de usuario. 

- ***[Nuevo]*** Máximo y promedio de usuarios primarios por dispositivo.


### <a name="client"></a>Cliente  

- Versión de cliente de la Tecnología de administración activa (AMT)

- Antigüedad del BIOS en años

- Recuento de dispositivos con Arranque seguro habilitado

- Recuento de dispositivos por estado de TPM

- Actualización automática de cliente: la configuración de implementación incluido el piloto de cliente y el uso de exclusión (cliente de interoperabilidad extendida)

- Configuración del tamaño de la caché de cliente

- Errores de descarga de implementación de cliente

- Resumen de problemas principales y estadísticas de estado de cliente

- Estado de acción de operación de notificación de cliente: cantidad de ejecución de cada uno, número máximo de clientes de destino y tasa media de éxito.

- Recuento de instalaciones de cliente de cada tipo de ubicación de origen  

- Recuento de errores de instalación de cliente  

- Recuento de dispositivos virtualizados por Hyper-V o Azure  

- Acciones de recuento de Centro de Software   

- Recuento de dispositivos habilitados para UEFI

- Métodos de implementación usados para el cliente y número de clientes por método de implementación

- Lista o recuento de agentes de cliente habilitados  

- Antigüedad del SO en meses

- Número de clases de inventario de hardware, reglas de inventario de software y reglas de recopilación de archivos

- Estadísticas de atestación de estado de dispositivo: códigos de error más comunes, número de servidores locales y recuentos de dispositivos en varios estados.

- ***[Nuevo]*** Recuento de dispositivos por explorador predeterminado.


### <a name="cloud-services"></a>Cloud Services  

- Estadísticas de detección de Azure Active Directory

- Configuración y estadísticas de uso de Cloud Management Gateway: recuentos de regiones y entornos, y estadísticas de autenticación y autorización.

- Recuento de servicios y aplicaciones de Azure Active Directory conectados a Configuration Manager

- Recuento de recopilaciones sincronizadas con Azure Log Analytics

- Recuento de conectores de Upgrade Analytics

- Si el conector en la nube de Azure Log Analytics está habilitado


### <a name="co-management"></a>Administración conjunta  
- Estadísticas acumuladas de uso de la administración conjunta: número de clientes inscritos, clientes que reciben la directiva, estados de las cargas de trabajo, tamaños de las recopilaciones de piloto/exclusión y errores de inscripción.  

- Recuento de clientes mediante el método de inscripción de administración conjunta.  

- Estadísticas de error de la inscripción de administración conjunta.  

- Programación de inscripción y estadísticas históricas.  

- Recuento de clientes aptos para la administración conjunta.  

- Inquilino de Microsoft Intune asociado.


### <a name="collections"></a>Recopilaciones  

- Uso de identificador de recopilación (que no se ejecuta sin los identificadores)

- Estadísticas de evaluación de la recopilación: tiempo de consulta, cantidades asignadas frente a cantidades sin asignar, recuentos por tipo, sustitución de identificador y uso de reglas.

- Recopilaciones sin una implementación


### <a name="compliance-settings"></a>Configuración de cumplimiento  

- Información básica de línea de base de configuración: recuento, número de implementaciones y número de referencias.

- Estadísticas de error de directivas de cumplimiento

- Recuento de elementos de configuración por tipo o  

- Recuento de implementaciones que hacen referencia a valores integrados, incluida la configuración de corrección.  

- Recuento de reglas e implementaciones creadas para la configuración personalizada, incluida la configuración de corrección.  

- Recuento de plantillas de Protocolo de inscripción de certificados simple (SCEP), VPN, Wi-Fi, certificado (.pfx) y de directiva de cumplimiento implementadas.

- Recuento de implementaciones de certificado SCEP, VPN, Wi-Fi, certificado (.pfx) y de directiva de cumplimiento por plataforma.

- Directiva de Windows Hello para empresas (creada, implementada).


### <a name="content"></a>Content  

- ***[Actualizado]*** Estadísticas de grupo de límites: cuántas rápidas, cuántas lentas, cantidad por grupo y relaciones de reserva.

- Información de grupo de límites: recuento de límites y sistemas de sitio que se han asignado a cada grupo de límites.  

- Relaciones de grupo de límites y configuración de reserva

- Estadísticas de descarga del contenido de cliente

- Recuento de límites por tipo  

- Recuento de clientes de caché del mismo nivel, estadísticas de uso y estadísticas de descargas parciales

- Información de configuración del administrador de distribuciones: subprocesos, intervalo de reintentos, número de reintentos y configuración del punto de distribución de extracción.  

- Información de configuración del punto de distribución: uso de BranchCache y supervisión de punto de distribución.

- Información de grupo de puntos de distribución: recuento de paquetes y puntos de distribución que se han asignado a cada grupo de puntos de distribución.  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Directivas de Advanced Threat Protection (ATP) de Microsoft Defender, anteriormente conocido como ATP de Windows Defender: recuento de directivas y si estas están implementadas.

- Recuento de alertas que se han configurado para la característica de Endpoint Protection  

- Recuento de recopilaciones que se han seleccionado para que aparezcan en el panel de Endpoint Protection  

- Recuento de clientes de destino, implementaciones y directivas de Protección contra vulnerabilidades de seguridad de Windows Defender.

- Errores de implementación de Endpoint Protection, recuento de códigos de error de implementación de directivas de Endpoint Protection.  

- Uso de la directiva de Firewall de Windows y de antimalware de Endpoint Protection (número de directivas únicas asignadas al grupo)<br /><br /> Estos datos no incluyen ninguna información sobre la configuración incluida en la directiva.  


### <a name="migration"></a>Migración  

- Recuento de objetos migrados (uso del Asistente para migración)


### <a name="mobile-device-management-mdm"></a>Administración de dispositivos móviles (MDM)  

- Recuento de acciones de dispositivo móvil: comandos bloquear, restablecer PIN, borrar, retirar y sincronizar ahora.

- Recuento de directivas de dispositivos móviles  

- Recuento de dispositivos móviles que se administran por Configuration Manager y Microsoft Intune, así como la forma en que se inscribieron (masiva, basada en el usuario)  

- Recuento de usuarios que tienen varios dispositivos móviles inscritos  

- Duración de la comprobación de estadísticas y programación de sondeo de dispositivos móviles  


### <a name="microsoft-intune-troubleshooting"></a>Solución de problemas de Microsoft Intune  

- Recuento y tamaño de los mensajes de acciones de dispositivo (borrar, retirar, bloquear), telemetría y de datos que se replican en Microsoft Intune

- Recuento y tamaño de los mensajes de estado, condición, inventario, RDR, DDR, UDX, estado de inquilino, POL, LOG, certificado, CRP, resincronización, CFD, RDO, BEX, ISM y de cumplimiento que se han descargado de Microsoft Intune

- Estadísticas de sincronización de usuario completas y diferenciales para Microsoft Intune


### <a name="on-premises-mobile-device-management-mdm"></a>Administración local de dispositivos móviles (MDM)  

- Recuento de perfiles y paquetes de inscripción masiva de Windows 10  

- Estadísticas de implementaciones correctas o con errores para las implementaciones locales de aplicaciones MDM  


### <a name="os-deployment"></a>Implementación del sistema operativo  

- Recuento de imágenes de arranque, controladores, paquetes de controladores, puntos de distribución habilitados para multidifusión, puntos de distribución habilitados para PXE y secuencias de tareas  

- Recuento de clientes de Configuration Manager por versiones de cliente

- Recuento de imágenes de arranque por versión de Windows PE

- Recuento de directivas de actualización de edición

- Recuento de identificadores de hardware que se excluyen del entorno PXE

- Recuento de implementación de sistema operativo por versión de SO

- Recuento de actualizaciones del sistema operativo en el tiempo

- Recuento de implementaciones de secuencias de tareas que usan la opción para descargar contenido previamente

- Recuentos de uso de paso de secuencia de tareas

- Versión de Windows ADK instalada


### <a name="site-updates"></a>Actualizaciones de sitios  

- Versiones de revisiones instaladas de Configuration Manager


### <a name="software-updates"></a>Actualizaciones de software  

- Diferencias disponibles y de fecha límite que se han usado en reglas de implementación automática  

- Número promedio y máximo de las asignaciones por actualización  

- Evaluación de actualizaciones de cliente y programaciones de búsquedas  

- Clasificaciones que se sincronizan por punto de actualización de software

- Estadísticas de aplicación de revisiones de clúster  

- Configuración de las actualizaciones rápidas de Windows 10

- Configuraciones que se usan para planes de mantenimiento activos de Windows 10  

- Recuento de actualizaciones implementadas de Office 365  

- Recuento de controladores de Microsoft Surface sincronizados

- Recuento de grupos de actualizaciones y asignaciones  

- Recuento de paquetes de actualización y el número mínimo, máximo y promedio de puntos de distribución de destino con paquetes  

- Recuento de actualizaciones que se crean e implementan con System Center Updates Publisher  

- Recuento de directivas de Windows Update para empresas creadas e implementadas

- ***[Nuevo]*** Estadísticas acumuladas de configuraciones de Windows Update para empresas.

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


### <a name="sqlperformance-data"></a>Datos de SQL o de rendimiento  

- Configuración y duración del resumen de sitio

- Recuento de tablas de base de datos más grandes  

- Estadísticas operativas de detección (recuento de objetos detectados)

- Tipos de detección, habilitados y programación (completa, incremental)

- Estado de mantenimiento, uso e información de réplica de SQL AlwaysOn

- Problemas de rendimiento del seguimiento de cambios de SQL, período de retención y estado de limpieza automática

- Período de retención de seguimiento de cambios de SQL

- Estado y estadísticas de rendimiento de mensajes de estado, incluidos los tipos de mensajes más caros y más comunes


### <a name="miscellaneous"></a>Varios  

- Configuración del punto de servicio de almacenamiento de datos, incluidos la programación de sincronización y el tiempo promedio

- Recuento de scripts y estadísticas de ejecución

- Recuento de sitios con Wake On Lan (WOL)

- Informes de uso y estadísticas de rendimiento

- ***[Nuevo]*** Estadísticas de uso de implementaciones por fases.



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivel 3: Completo
El nivel Completo incluye todos los datos de los niveles Básico y Mejorado. También incluye información adicional sobre Endpoint Protection, porcentajes de cumplimiento de actualización e información de actualización de software. Este nivel también puede incluir información avanzada de diagnóstico como archivos del sistema e instantáneas de memoria que pueden incluir información personal que existía en los archivos de registro o de memoria en el momento de la captura.

Para la versión 1802 de Configuration Manager, este nivel incluye los datos siguientes:

- Información de la programación de evaluación de reglas de implementación automática

- Resumen de estado de ATP

- Evaluación de recopilación y estadísticas de actualización

- Estadísticas de cumplimiento y errores de las directivas de cumplimiento

- Configuración de cumplimiento: SCEP, VPN, Wi-Fi y detalles de configuración de plantilla de directiva de cumplimiento

- Módulo de configuración de DCM para el uso de Configuration Manager

- Errores de instalación de implementación de cliente detallados

- Resumen de estado de Endpoint Protection: incluido el recuento de clientes protegidos, en peligro, desconocidos y no admitidos.

- Configuración de directivas de Endpoint Protection

- Lista de procesos configurados con el comportamiento de la instalación de aplicaciones

- Número mínimo, máximo y promedio de horas desde la última búsqueda de actualizaciones de software

- Número mínimo, máximo y promedio de clientes inactivos en recopilaciones de implementación de actualizaciones de software

- Número mínimo, máximo y promedio de actualizaciones de software por paquete

- ***[Actualizado]*** Estadísticas de implementación de código de producto MSI. 

- Cumplimiento general de las implementaciones de actualizaciones de software.

- Recuento de grupos que tienen actualizaciones de software caducadas

- Recuentos y códigos de error de implementación de actualizaciones de software

- Información de implementación de actualización de software: porcentaje de implementaciones de destino con cliente frente a hora UTC, necesaria frente a opcional frente a silenciosa y supresión de reinicio.

- Productos de actualización de software sincronizados por punto de actualización de software

- Porcentajes de éxito de búsqueda de actualizaciones de software

- Primeras 50 CPU en el entorno

- Tipo de directivas de acceso condicional de Exchange Active Sync (EAS) (bloquear o cuarentena) para dispositivos que administra Microsoft Intune.

- Detalles de la aplicación de Microsoft Store para Empresas: lista no agregada de aplicaciones sincronizadas, incluido AppID, el estado en línea o sin conexión, y el recuento total de licencias compradas.
