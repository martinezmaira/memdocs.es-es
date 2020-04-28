---
title: Nueva versión 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1710 de Configuration Manager.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073626"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Novedades de la versión 1710 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1710 de la rama actual de Configuration Manager está disponible como actualización en consola en los sitios instalados previamente que ejecutan las versiones 1610, 1702 o 1706.

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para más información, vea [Resumen de cambios en la rama actual de Configuration Manager, versión 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Ahora también están disponibles las siguientes actualizaciones adicionales a esta versión:
- [Paquete acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Paquete acumulativo de actualizaciones 2 de la rama actual de Configuration Manager, versión 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>
> Más información acerca de:    
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)  
> - [Instalación de actualizaciones en los sitios](../../servers/manage/updates.md)  
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1710 de Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestructura del sitio

### <a name="updates-for-peer-cache-----sms500850---"></a>Actualizaciones de la caché del mismo nivel  <!-- sms500850 -->
A partir de esta versión, la caché del mismo nivel ya no es una característica de versión preliminar.  En esta versión no se presenta ningún otro cambio. Para obtener más información, vea [Caché del mismo nivel para clientes de Configuration Manager](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Compatibilidad de los puntos de distribución en la nube con la nube de Azure Government   <!-- sms491428 -->
Ahora puede usar [puntos de distribución en la nube](../hierarchy/use-a-cloud-based-distribution-point.md) en la nube de Azure Government.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revisión de unidad de inventario predeterminado <!-- sms503697 -->
Como en los dispositivos ahora se incluyen unidades de disco duro con tamaños en gigabytes (GB), terabytes (TB) y de mayor escala, en esta versión se cambia la unidad predeterminada (SMS_Units) que se usa en muchas vistas de megabytes (MB) a GB. Por ejemplo, el valor de v_gs_LogicalDisk.FreeSpace ahora indica unidades de GB.


<!-- ## Migration  -->


## <a name="client-management"></a>Administración de cliente

### <a name="co-management-for-windows-10-devices"></a>Administración conjunta para dispositivos de Windows 10    
<!-- 1350871 -->
Las actualizaciones anteriores de Windows 10 ya permiten unir un dispositivo Windows 10 a Active Directory (AD) local y en la nube al mismo tiempo (Azure AD híbrido). A partir de la versión 1710 de Configuration Manager, la administración conjunta aprovecha esta mejora y permite administrar dispositivos de la versión 1709 de Windows 10 (también conocida con el nombre Fall Creators Update) de forma simultánea mediante Intune y Configuration Manager. Se trata de una solución que sirve de puente entre la administración tradicional y moderna, y proporciona un camino para realizar la transición con un enfoque por fases. Para más información, consulte [Administración conjunta para dispositivos de Windows 10](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Reinicio de equipos desde la consola de Configuration Manager  <!-- 1356283 -->
A partir de esta versión, puede usar la consola de Configuration Manager para identificar los dispositivos de cliente que requieren un reinicio y, después, usar una acción de notificación de cliente para reiniciarlos.

Vea [Cómo administrar clientes](../../clients/manage/manage-clients.md#restart-clients).


<!-- ## Compliance settings -->


## <a name="application-management"></a>Administración de aplicaciones
### <a name="improvements-for-run-scripts------1236459---"></a>Mejoras en la funcionalidad de scripts de ejecución   <!-- 1236459 -->
Esta versión ofrece varias mejoras en la funcionalidad de **scripts de ejecución**, que permite implementar scripts de PowerShell para ejecutarlos en los dispositivos administrados. Esta característica se introdujo por primera vez en la versión 1706.

Estas son algunas de las mejoras:
- Uso de ámbitos de seguridad para ayudar a controlar quién puede usar la funcionalidad de scripts de ejecución
- Supervisión en tiempo real de los scripts que se ejecutan
- Los parámetros del script se muestran en el Asistente para crear scripts, admiten la validación y se identifican como obligatorios u opcionales.

Para obtener más información sobre el uso de la funcionalidad de scripts de ejecución, consulte [Creación y ejecución de scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Configuración de nueva directiva de administración de aplicaciones móviles
<!-- 1324760 -->
Las siguientes opciones se han agregado a la configuración de directiva de administración de aplicaciones móviles:
- **Deshabilitar sincronización de contactos**: impide que la aplicación guarde los datos en la aplicación de contactos nativa del dispositivo.
- **Deshabilitar la impresión**: impide que la aplicación imprima datos profesionales o educativos.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>El Centro de software ya no distorsiona los iconos que tienen un tamaño superior a 250 x 250  
<!-- 1356194 -->

Con esta versión, el Centro de software ya no distorsiona los iconos con un tamaño superior a 250 x 250. Esos iconos aparecían antes borrosos. Ahora puede configurar un icono con una dimensión de píxel de hasta 512 x 512 sin que se muestre distorsionado.

Para agregar un icono para su aplicación en el Centro de software, consulte el artículo sobre cómo [crear aplicaciones](../../../apps/deploy-use/create-applications.md).

## <a name="operating-system-deployment"></a>Implementación de sistema operativo
 > [!TIP]   
 > <!-- 1354281 -->
 > A partir de la versión 1709 (también conocida como "Fall Creators Update") de Windows 10, Windows Media incluye varias ediciones. Al configurar una secuencia de tareas para usar un paquete de actualizaciones del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición que se pueda usar con Configuration Manager](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Adición de secuencias de tareas secundarias a una secuencia de tareas
<!-- 1261338 -->

Puede agregar un nuevo paso de secuencia de tareas que ejecute otra secuencia de tareas, y que crea una relación de elementos primarios y secundarios entre las secuencias de tareas. De este modo, puede crear más secuencias de tareas modulares que puede volver a utilizar.  

Para obtener más información sobre la secuencia de tareas secundarias, lea la sección sobre [secuencias de tareas secundarias](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Personalización de Centro de software
<!-- 1351224 -->
Puede agregar elementos de personalización de marca de empresa y especificar la visibilidad de las pestañas en el Centro de software. Puede agregar el nombre de compañía específico del Centro de software, establecer un tema de color para la configuración de Centro de software, establecer un logotipo de empresa y establecer las pestañas visibles para los dispositivos del cliente.

Para obtener más información, consulte [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).

## <a name="software-updates"></a>Actualizaciones de software

### <a name="surface-driver-updates-----1098490---"></a>Actualizaciones de controladores de Surface  <!-- 1098490 -->
A partir de esta versión, la administración de actualizaciones de controladores de Surface ya no es una característica de versión preliminar.  


## <a name="reporting"></a>Generación de informes

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitación de los datos mejorados de Windows 10 al envío únicamente de datos pertinentes para el Estado de dispositivos de Windows Analytics
<!-- 1356148 -->

Ahora puede establecer el nivel de recopilación de datos de diagnóstico de Windows 10 en **Mejorado (limitado)** . Esta configuración le permite obtener información práctica sobre los dispositivos de su entorno sin que los dispositivos informen de todos los datos del nivel **Mejorado** con Windows 10, versión 1709 o una versión posterior.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Administración de dispositivos móviles

### <a name="actions-for-non-compliance"></a>Acciones de no cumplimiento 
<!--1321366 -->    
Ahora puede configurar una secuencia ordenada de acciones que se aplican a los dispositivos que no cumplen las normas. Por ejemplo, puede notificar a los usuarios de dispositivos no compatibles a través de correo electrónico o marcar los dispositivos como no compatibles.

### <a name="windows-10-arm64-device-support"></a>Compatibilidad con dispositivos Windows 10 (ARM64)
<!-- 1355000 -->

Cuando los dispositivos ARM64 que ejecutan Windows 10 estén disponibles, admitirán los escenarios híbridos de administración de dispositivos móviles (MDM).

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiencia mejorada del perfil VPN en la consola de Configuration Manager 
<!-- 1318232 -->

Con esta versión, hemos actualizado las páginas de propiedades y el Asistente para perfiles de VPN con el fin de mostrar una configuración más adecuada para la plataforma seleccionada:


- Cada plataforma tiene su propio flujo de trabajo, lo que significa que los nuevos perfiles VPN contienen únicamente la configuración compatible con la plataforma.
- La página **Plataformas admitidas** ahora aparece después de **General**.  Ahora se elige primero la plataforma antes de establecer los valores de propiedad.
- Cuando la plataforma se establece en **Android**, **Android for Work** o **Windows Phone 8.1**, la página **Plataformas admitidas** no es necesaria y no se muestra.
- El flujo de trabajo basado en el cliente de Configuration Manager se ha combinado con los flujos de trabajo de Windows 10 basados en el cliente de dispositivos móviles híbridos (MDM). Ambos admiten la misma configuración.
- Cada flujo de trabajo de la plataforma incluye únicamente las opciones adecuadas para ese flujo de trabajo.  Por ejemplo, el flujo de trabajo de Android contiene configuraciones adecuadas para Android; las configuraciones adecuadas para iOS o Windows 10 Mobile ya no aparecen en el flujo de trabajo de Android.
- La página VPN automática está obsoleta y se ha quitado.

Estos cambios se aplican a los nuevos perfiles VPN.  

Para minimizar el riesgo de compatibilidad, los perfiles VPN existentes no se modifican.  Al editar un perfil existente, la configuración aparece igual que cuando se creó el perfil.  

Para más información, vea [Perfiles de VPN en dispositivos móviles](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Compatibilidad limitada con certificados de Cryptography: Next Generation (CNG) <!-- 1356191 -->

Configuration Manager tiene compatibilidad limitada con Cryptography: Next Generation (CNG). Los clientes de Configuration Manager pueden usar un certificado de autenticación del cliente PKI con clave privada en el proveedor de almacenamiento de claves (KSP) de CNG. Gracias a la compatibilidad con KSP, los clientes de Configuration Manager admiten una clave privada basada en hardware, como el KSP de TPM para los certificados de autenticación de cliente PKI.

Para obtener más información, consulte [Introducción a los certificados CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Proteger los dispositivos

### <a name="create-and-deploy-exploit-guard-policies"></a>Creación e implementación de directivas de Protección contra vulnerabilidades de seguridad
<!-- 1355468 -->

También puede [crear e implementar directivas](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) que administren los cuatro componentes de Protección contra vulnerabilidades de seguridad de Windows Defender, incluida la reducción de la superficie de ataque, el acceso controlado a carpetas, la protección contra vulnerabilidades y la protección de red.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Creación e implementación de directivas de Protección de aplicaciones de Windows Defender
<!-- 1351960 -->

También puede [crear e implementar directivas de Protección de aplicaciones de Windows Defender](../../../protect/deploy-use/create-deploy-application-guard-policy.md) con Configuration Manager Endpoint Protection.

### <a name="device-guard-policy-changes"></a>Cambios en la directiva de Device Guard
<!-- 1355092 -->
Se han realizado los siguientes tres cambios en relación con las directivas de Device Guard:

- Las directivas de Device Guard se llaman ahora directivas de Windows Defender Application Control. Así, por ejemplo, el **Asistente para la creación de directivas de Device Guard** ahora se llama **Asistente para la creación de directivas de Windows Defender Application Control**.
- Los dispositivos que utilizan Windows Fall Creators Update, versión 1709, para Windows no necesitan reiniciarse para aplicar las directivas de Windows Defender Application Control. Reiniciar sigue siendo la opción predeterminada, pero puede [desactivar los reinicios](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
- Puede [establecer los dispositivos para que automáticamente ejecuten software](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) en el que confía Intelligent Security Graph.





## <a name="next-steps"></a>Pasos siguientes
Cuando esté listo para instalar esta versión, consulte el artículo sobre [actualizaciones de Configuration Manager](../../servers/manage/updates.md).
