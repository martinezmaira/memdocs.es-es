---
title: Datos de diagnóstico y uso en la versión 1906
titleSuffix: Configuration Manager
description: Obtenga más información sobre los datos específicos de cada nivel que recopila Configuration Manager en la versión 1906.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 370fc61f-2d8a-45b4-adc7-7b5d5ede2bf4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae606018baf159fe753645a380593506773c7a39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703863"
---
# <a name="diagnostic-and-usage-data-for-version-1906"></a>Datos de diagnóstico y uso en la versión 1906

*Se aplica a: Configuration Manager (rama actual)*

En las secciones siguientes se proporcionan detalles adicionales sobre los datos que se recopilan en cada nivel. Para obtener más información sobre los niveles y cómo cambiarlos, vea [Niveles de datos de diagnóstico y uso](levels-overview.md).

Los cambios respecto de versiones anteriores se indican mediante la nota ***[Nuevo]***, ***[Actualizado]***, ***[Quitado]*** o ***[Movido]***.

> [!IMPORTANT]
> Configuration Manager no recopila códigos de sitio, nombres de sitios, direcciones IP, nombres de usuario o equipo, direcciones físicas o direcciones de correo electrónico en los niveles Básico o Mejorado. Cualquier recopilación de esta información en el nivel Completo no tiene ninguna finalidad. Se incluye potencialmente en la información de diagnóstico avanzada como archivos de registro o instantáneas de memoria. Microsoft no usa esta información para identificarle, para ponerse en contacto con usted ni para el desarrollo de publicidad.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivel 1: Básico

En el caso de la versión 1906 de Configuration Manager, este nivel incluye los datos siguientes:

- ***[Actualizado]*** Estadísticas sobre las conexiones de la consola de Configuration Manager: versión de SO, idioma, SKU y arquitectura; memoria del sistema, número de procesadores lógicos, identificador de sitio de conexión, versiones instaladas de .NET, paquetes de idioma de la consola y nivel de autenticación compatible.

- Recuentos básicos de aplicación y tipo de implementación: aplicaciones totales, aplicaciones totales con varios tipos de implementación, aplicaciones totales con dependencias, aplicaciones totales reemplazadas y recuento de tecnologías de implementación en uso.

- Datos básicos de la jerarquía del sitio de Configuration Manager: lista de sitios, tipo, versión, estado, número de cliente y zona horaria.

- Configuración básica de la base de datos: procesadores, tamaño de la memoria, opciones de la memoria, configuración de la base de datos de Configuration Manager, tamaño de la base de datos de Configuration Manager, configuración del clúster, configuración de vistas distribuidas y versión de seguimiento de cambios  

- Estadísticas básicas de detección: recuento de detección y tamaños de grupo mínimo/máximo/medio, y cuándo se ejecuta completamente el sitio con los servicios de Azure Active Directory.

- Información básica de Endpoint Protection sobre las versiones de cliente antimalware.

- Recuentos de implementación del sistema operativo básico de imágenes.

- Información básica del servidor de sistema de sitio: roles de sistema de sitio usados, estado de SSL y de Internet, sistema operativo, procesadores, máquina física o virtual, y uso de alta disponibilidad de servidor de sitio.

- Esquema de base de datos de Configuration Manager (hash de todas las definiciones de objeto)

- Nivel configurado de datos de diagnóstico y utilización, modo en línea o sin conexión y configuración de actualización rápida

- Recuento de idiomas de cliente y configuraciones regionales

- Recuento de versiones de cliente de Configuration Manager y versiones de sistema operativo u Office.

- Recuento de sistemas operativos de los dispositivos administrados y las directivas establecidas por Exchange Connector

- Recuento de dispositivos de Windows 10 por rama, compilación y bosque único de Active Directory  

- Recuento de clientes de Windows 10 que usan Windows Update for Business  

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

- Estadísticas de datos de diagnóstico y utilización: cuándo se ejecutan, runtime, errores  

- Si la detección de redes está habilitada o deshabilitada.  

- Recuento de clientes unidos a Azure Active Directory  

- Recuento de implementaciones por fases creadas por tipo  

- Recuento de clientes de interoperabilidad extendida  

- Lista con hash de propiedades de inventario de hardware de más de 255 caracteres  

- Recuento de clientes mediante el método de inscripción de administración conjunta.  

- Estadísticas de error de la inscripción de administración conjunta.  

- Recuento de clientes por antigüedad del sistema operativo Windows, hasta el intervalo de tres meses más cercano  

- 10 principales nombres de procesador usados en clientes y servidores  

- Recuento y tasas de procesamiento de objetos clave de Configuration Manager: registros de detección de datos (DDR), mensajes de estado, inventario de hardware, inventario de software y número total de archivos en las bandejas de entrada  

- Información de rendimiento del procesador y el disco del servidor de sitio  

- Información de uso de memoria y tiempo de actividad de los procesos de servidor de sitio de Configuration Manager  

- Recuento de bloqueos de los procesos de servidor de sitio de Configuration Manager y, si está disponible, el identificador de firma digital de Watson  

- Lista con hash de principales consultas SQL por recuento de bloqueos y uso de memoria  

- Estadísticas acumuladas de uso de administración conjunta: número de clientes inscritos alguna vez, número de clientes inscritos, número de clientes con inscripción pendiente, clientes que reciben la directiva, estados de las cargas de trabajo, tamaños de las recopilaciones de piloto/exclusión y errores de inscripción  

- Existencia de las extensiones del lado servidor de administración y supervisión de Microsoft BitLocker (MBAM)  

- Recuento de aplicaciones clasificadas y sin clasificar de Asset Intelligence

- ***[Nuevo]*** Estado del servicio de administración

- ***[Nuevo]*** Hash de los atributos de sitio clave (identificador del sitio, identificador del agente de SQL y la clave de intercambio de sitio)

## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivel 2: Mejorado

En el caso de la versión 1906 de Configuration Manager, este nivel incluye los datos siguientes:

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

- Recuento de aplicaciones a las que se hace referencia en una secuencia de tareas  

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

- Estadísticas acumuladas de afinidad entre usuario y dispositivo  

- Número máximo y promedio de usuarios primarios por dispositivo  

- Uso de la condición global de aplicación por tipo  

- Configuración de la personalización del Centro de software  

- Preparación y recuentos del Administrador de conversión de paquetes  

- Recuento de los métodos de detección de aplicaciones por tipo  

- Recuento de errores de cumplimiento de la aplicación  

- Propiedades del instalador MSI  

- Estadísticas de solicitudes de instalación de usuarios  

- Estadísticas acumuladas sobre el uso de la característica de aprobación de correo electrónico  

- Recuento de archivos, tamaño del contenido, recuento de servicios y recuento de acciones personalizadas de MSI del catálogo de aplicaciones  

- Recuento de dispositivos por estado de disponibilidad de Office ProPlus.

- ***[Nuevo]*** Estadísticas acumuladas sobre el uso de los grupos de aplicaciones

- ***[Nuevo]*** Estadísticas acumuladas sobre los complementos de Office, el uso de Office Readiness Toolkit y los recuentos de clientes con Office 365 ProPlus

### <a name="client"></a>Cliente  

- Versión de cliente de la Tecnología de administración activa (AMT)  

- Antigüedad del BIOS en años  

- Recuento de dispositivos con Arranque seguro habilitado  

- Recuento de dispositivos por estado de TPM  

- Actualización automática de cliente: la configuración de implementación incluido el piloto de cliente y el uso de exclusión (cliente de interoperabilidad extendida)  

- Configuración del tamaño de la caché de cliente  

- Errores de descarga de implementación de cliente  

- Resumen de problemas principales y estadísticas de estado de cliente por versión de cliente, componente, SO y carga de trabajo  

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

- Recuento de dispositivos por explorador predeterminado  

- Recuento de certificados de autenticación de servidor generados por Configuration Manager  

- Recuento de dispositivos de Microsoft Surface por modelo  

- Recuento de errores de comprobación de mantenimiento de cliente por tipo de problema

### <a name="cloud-services"></a>Cloud Services  

- Estadísticas de detección de Azure Active Directory  

- Configuración y estadísticas de uso de Cloud Management Gateway: recuentos de regiones y entornos, y estadísticas de autenticación y autorización.  

- Recuento de servicios y aplicaciones de Azure Active Directory conectados a Configuration Manager  

- Recuento de recopilaciones sincronizadas con Azure Log Analytics  

- Recuento de conectores de Upgrade Analytics  

- Si el conector en la nube de Azure Log Analytics está habilitado  

- Recuento de puntos de distribución de incorporación de cambios con un punto de distribución en la nube como ubicación de origen  

### <a name="cmpivot"></a>CMPivot

- Estadísticas de uso de CMPivot  

- Recuento de consultas de CMPivot guardadas  

- Recuento de consultas por tipo de entidad  

### <a name="co-management"></a>Administración conjunta  

- Programación de inscripción y estadísticas históricas.  

- Recuento de clientes aptos para la administración conjunta.  

- Inquilino de Microsoft Intune asociado.  

### <a name="collections"></a>Recopilaciones  

- Uso de identificador de recopilación (que no se ejecuta sin los identificadores)  

- Estadísticas de evaluación de la recopilación: tiempo de consulta, cantidades asignadas frente a cantidades sin asignar, recuentos por tipo, sustitución de identificador y uso de reglas.  

- Recopilaciones sin una implementación  

- ***[Nuevo]*** Recuento de recopilaciones sincronizadas con Azure Active Directory

### <a name="compliance-settings"></a>Configuración de cumplimiento  

- Información básica de línea de base de configuración: recuento, número de implementaciones y número de referencias.  

- Estadísticas de error de directivas de cumplimiento  

- Recuento de elementos de configuración por tipo o  

- Recuento de implementaciones que hacen referencia a valores integrados, incluida la configuración de corrección.  

- Recuento de reglas e implementaciones creadas para la configuración personalizada, incluida la configuración de corrección.  

- Recuento de plantillas de Protocolo de inscripción de certificados simple (SCEP), VPN, Wi-Fi, certificado (.pfx) y de directiva de cumplimiento implementadas.  

- Recuento de implementaciones de certificado SCEP, VPN, Wi-Fi, certificado (.pfx) y de directiva de cumplimiento por plataforma  

- Directiva de Windows Hello para empresas (creada, implementada).  

- Recuento de directivas del explorador Microsoft Edge implementadas  

- Recuento de directivas de OneDrive (creadas, implementadas)

### <a name="content"></a>Content  

- Estadísticas de grupo de límites: cuántas rápidas, cuántas lentas, recuento por grupo y relaciones de reserva  

- Información de grupo de límites: recuento de límites y sistemas de sitio que se han asignado a cada grupo de límites.  

- Relaciones de grupo de límites y configuración de reserva  

- Estadísticas de descarga del contenido de cliente  

- Recuento de límites por tipo  

- Recuento de clientes de caché del mismo nivel, estadísticas de uso y estadísticas de descargas parciales  

- Información de configuración del administrador de distribuciones: subprocesos, intervalo de reintentos, número de reintentos y configuración del punto de distribución de extracción.  

- Información de configuración del punto de distribución: uso de BranchCache y supervisión de punto de distribución.  

- Información de grupo de puntos de distribución: recuento de paquetes y puntos de distribución que se han asignado a cada grupo de puntos de distribución.  

- Tipo de biblioteca de contenido, ya sea local o remoto  

- Recuento de grupos de límites por configuración  

### <a name="endpoint-protection"></a>Endpoint Protection  

- Directivas de Advanced Threat Protection (ATP) de Microsoft Defender, anteriormente conocido como ATP de Windows Defender: recuento de directivas y si estas están implementadas.

- Recuento de alertas que se han configurado para la característica de Endpoint Protection  

- Recuento de recopilaciones que se han seleccionado para que aparezcan en el panel de Endpoint Protection  

- Recuento de clientes de destino, implementaciones y directivas de Protección contra vulnerabilidades de seguridad de Windows Defender.  

- Errores de implementación de Endpoint Protection, recuento de códigos de error de implementación de directivas de Endpoint Protection.  

- Uso de la directiva de Firewall de Windows y de antimalware de Endpoint Protection (número de directivas únicas asignadas al grupo). Estos datos no incluyen ninguna información sobre la configuración incluida en la directiva.  

### <a name="migration"></a>Migración  

- Recuento de objetos migrados (uso del Asistente para migración)  

### <a name="mobile-device-management-mdm"></a>Administración de dispositivos móviles (MDM)  

- Recuento de acciones de dispositivo móvil: comandos bloquear, restablecer PIN, borrar, retirar y sincronizar ahora.  

- Recuento de directivas de dispositivos móviles  

- Recuento de dispositivos móviles administrados por Configuration Manager y Microsoft Intune, así como la forma en que se han inscrito (masiva, según el usuario)  

- Recuento de usuarios que tienen varios dispositivos móviles inscritos  

- Duración de la comprobación de estadísticas y programación de sondeo de dispositivos móviles  

### <a name="microsoft-intune-troubleshooting"></a>Solución de problemas de Microsoft Intune  

- Recuento y tamaño de acciones de dispositivo (borrar, retirar, bloquear), datos de utilización y mensajes de datos que se replican en Microsoft Intune  

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

- Recuento de tareas de mantenimiento de imágenes  

- Recuento de máquinas importadas  

- ***[Nuevo]*** Recuento de los identificadores de hardware duplicados (dirección MAC y GUID de SMBIOS) excluidos del registro de cliente y PXE

- ***[Nuevo]*** Recuento de secuencias de tareas por tipo (secuencia de tareas genérica o implementación del SO)

- ***[Nuevo]*** Recuento de paquetes con configuración del contenido de la caché previa

### <a name="site-updates"></a>Actualizaciones de sitios  

- Versiones de revisiones instaladas de Configuration Manager  

### <a name="software-updates"></a>Actualizaciones de software  

- Diferencias disponibles y de fecha límite que se han usado en reglas de implementación automática  

- Número promedio y máximo de las asignaciones por actualización  

- Evaluación de actualizaciones de cliente y programaciones de búsquedas  

- Clasificaciones sincronizadas por el punto de actualización de software  

- Estadísticas de aplicación de revisiones de clúster  

- Configuración de las actualizaciones rápidas de Windows 10  

- Configuraciones que se usan para planes de mantenimiento activos de Windows 10  

- Recuento de actualizaciones implementadas de Office 365  

- Recuento de controladores de Microsoft Surface sincronizados  

- Recuento de grupos de actualizaciones y asignaciones  

- Recuento de paquetes de actualización y el número mínimo, máximo y promedio de puntos de distribución de destino con paquetes  

- Recuento de actualizaciones que se crean e implementan con System Center Updates Publisher  

- Recuento de directivas de Windows Update para empresas creadas e implementadas  

- Estadísticas acumuladas de configuraciones de Windows Update para empresas  

- Número de reglas de implementación automática que están asociadas a la sincronización  

- Número de reglas de implementación automática que crean actualizaciones nuevas o agregan otras a un grupo existente  

- Número de reglas de implementación automática que tienen varias implementaciones  

- Número de grupos de actualizaciones y número mínimo, máximo y promedio de actualizaciones por grupo  

- Número de actualizaciones y porcentaje de las actualizaciones que se han implementado, caducado, sustituido, descargado y que contienen términos de licencia  

- Estadísticas de equilibrio de carga del punto de actualización de software  

- Programación de la sincronización del punto de actualización de software  

- Número total o promedio de recopilaciones que tienen implementaciones de actualización de software y el número máximo o promedio de actualizaciones implementadas  

- Códigos de error de búsqueda de actualizaciones y recuento de máquinas  

- Versiones de contenido del panel de Windows 10  

- Recuento de suscripciones a catálogo de actualizaciones de software de terceros y uso  

- Recuento de actualizaciones de software implementadas con y sin contenido  

- Estadísticas acumuladas sobre el número de actualizaciones de UUP necesarias, implementadas, expiradas, sustituidas y descargadas  

- Uso de categorías de productos de UUP  

- Recuento de clientes que han implementado al menos una actualización de calidad de UUP o una actualización de características de UUP  

- Principales códigos de error de UUP y recuento de dispositivos afectados  

- ***[Nuevo]*** Lista de suscripciones a los catálogos de actualización de software de teceros

- ***[Nuevo]*** Uso de la configuración de mantenimiento de WSUS

### <a name="sqlperformance-data"></a>Datos de SQL o de rendimiento  

- Configuración y duración del resumen de sitio  

- Recuento de tablas de base de datos más grandes  

- Estadísticas operativas de detección (recuento de objetos detectados)  

- Tipos de detección, habilitados y programación (completa, incremental)  

- Estado de mantenimiento, uso e información de réplica de SQL AlwaysOn  

- Problemas de rendimiento del seguimiento de cambios de SQL, período de retención y estado de limpieza automática  

- Período de retención de seguimiento de cambios de SQL  

- Estado y estadísticas de rendimiento de mensajes de estado, incluidos los tipos de mensajes más caros y más comunes  

- Estadísticas de tráfico del punto de administración (número total de bytes enviados y recibidos por el punto de conexión)  

- Medidas del contador de rendimiento del punto de administración  

- ***[Nuevo]*** Estadísticas de rendimiento acumuladas de las llamadas hechas a los puntos de conexión del Centro de software en el punto de administración

### <a name="miscellaneous"></a>Varios  

- Configuración del punto de servicio de almacenamiento de datos, que incluye la programación de sincronización, el tiempo medio y el uso de característica de tablas personalizadas  

- Recuento de scripts y estadísticas de ejecución y edición  

- Recuento de sitios con Wake On Lan (WOL)  

- Informes de uso y estadísticas de rendimiento  

- Estadísticas de utilización de implementaciones por fases  

- Recuentos de elementos de conclusiones de administración y progreso  

- Recuento de bloqueos de los procesos únicos que no son de Configuration Manager en el servidor de sitio y, si está disponible, el identificador de firma digital de Watson  

- Estadísticas acumuladas sobre errores de inscripciones y uso de Análisis de escritorio

- Recuento de notificaciones de consola no críticos

- Estadísticas acumuladas de tiempo de arranque del sistema por SO, factor de forma y tipo de unidad

- ***[Nuevo]*** Estadísticas acumuladas sobre el uso de Análisis de escritorio

- ***[Nuevo]*** Estado y configuración de las tareas de mantenimiento de SQL

## <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivel 3: Completo

En el caso de la versión 1906 de Configuration Manager, este nivel incluye los datos siguientes:

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

- Estadísticas de implementación de código de producto MSI  

- Cumplimiento general de las implementaciones de actualizaciones de software.  

- Recuento de grupos que tienen actualizaciones de software caducadas  

- Recuentos y códigos de error de implementación de actualizaciones de software  

- Información de implementación de actualización de software: porcentaje de implementaciones de destino con cliente frente a hora UTC, necesaria frente a opcional frente a silenciosa y supresión de reinicio.  

- Productos de actualización de software sincronizados por punto de actualización de software  

- Porcentajes de éxito de búsqueda de actualizaciones de software  

- Primeras 50 CPU en el entorno  

- Tipo de directivas de acceso condicional de Exchange Active Sync (EAS) (bloquear o cuarentena) para dispositivos que administra Microsoft Intune.  

- Detalles de la aplicación de Microsoft Store para Empresas: lista no agregada de aplicaciones sincronizadas, incluido AppID, el estado en línea o sin conexión, y el recuento total de licencias compradas.  

- Recuento de clientes insertados con opción a no permitir retroceso a NTLM  

- ***[Nuevo]*** Lista de las extensiones de la consola de Configuration Manager
