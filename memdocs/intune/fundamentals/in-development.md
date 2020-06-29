---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 107ac1e2aef18bcb72a6fe1f94eade23c3f85319
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216525"
---
# <a name="in-development-for-microsoft-intune"></a>En desarrollo para Microsoft Intune

Para ayudarle con la preparación y planeación, en esta página se enumeran las actualizaciones y características de la interfaz de usuario de Intune que están en desarrollo, pero que aún no se han publicado. Además de la información de esta página: 

- Si prevemos que tendrá que tomar medidas antes de realizar un cambio, haremos una publicación complementaria en el Centro de mensajes de Office.
- Cuando una característica entra en producción, ya sea una versión preliminar o disponible con carácter general, la descripción de la característica pasa de esta página a [Novedades](whats-new.md).
- Esta página y la página [Novedades](whats-new.md) se actualizan periódicamente. Compruebe si hay actualizaciones adicionales.
- Consulte el [plan de desarrollo de Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) para conocer los plazos de tiempo y los productos estratégicos.

> [!NOTE]
> Esta página refleja las expectativas actuales sobre las funciones de Intune en una versión futura. Las fechas y las características individuales pueden cambiar. En esta página no se describen todas las características en desarrollo.

**Fuente RSS**: para recibir notificaciones cuando esta página se actualice, copie y pegue la dirección URL siguiente en el lector de fuentes: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Este artículo se actualizó por última vez en la fecha que aparece bajo el título anterior.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
<!--## App management-->


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Establecimiento del estado de cumplimiento de dispositivos desde partners de MDM de terceros<!-- 6361689   -->
Los clientes de Microsoft 365 que posean soluciones de MDM de terceros podrán aplicar directivas de acceso condicional para aplicaciones de Microsoft 365 en iOS y Android a través de la integración con el servicio de cumplimiento de dispositivos de Microsoft Intune. Un proveedor de MDM de terceros aprovechará el servicio Cumplimiento de dispositivos de Intune para enviar datos de cumplimiento de dispositivos a Intune. Después, Intune evaluará para determinar si el dispositivo es de confianza y establecerá los atributos de acceso condicional en Azure AD.  A los clientes se les pedirá que establezcan directivas de acceso condicional de Azure AD desde el centro de administración de Microsoft Endpoint Manager o desde el portal de Azure AD.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nueva configuración de VPN para dispositivos Windows 10 y versiones más recientes<!-- 6602122  -->
Cuando se crea un perfil de VPN mediante el tipo de conexión de IKEv2, hay nuevas opciones que puede configurar(**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10 y posteriores** como plataforma > **VPN** para el perfil > **VPN base**):

- **Túnel de dispositivos**: Permite que los dispositivos se conecten automáticamente a VPN sin necesidad de interacción del usuario, incluido el inicio de sesión del usuario. Esta característica requiere que se habilite **Always On** y que se usen **certificados de máquina** como método de autenticación.
- Configuración de Cryptography Suite: Configure los algoritmos que se usan para proteger las asociaciones de seguridad IKE y secundarias, que permiten hacer coincidir la configuración de cliente y servidor.

Para ver las opciones que puede configurar, vaya a [Configuración de dispositivos con Windows 10 y Windows Holographic para agregar conexiones VPN mediante Intune](../configuration/vpn-settings-windows-10.md).

Se aplica a:
- Windows 10 y versiones posteriores


<!-- ***********************************************-->
<!--## Device enrollment-->



<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics incluirá registros de detalles del dispositivo<!--6014987  -->
Habrá disponibles registros detallados del dispositivo de Intune en **Informes** > **Log Analytics**. Puede correlacionar los detalles del dispositivo para compilar consultas personalizadas y libros de Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Asociación de inquilinos: escala de tiempo del dispositivo en el centro de administración<!--7220536, CM7141381 -->
Cuando Configuration Manager sincroniza un dispositivo con Microsoft Endpoint Manager de Microsoft a través de una asociación de inquilinos, podrá ver una escala de tiempo de eventos. Esta escala de tiempo muestra la actividad pasada en el dispositivo que puede ayudarle a solucionar problemas. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Asociación de inquilinos: instalación de una aplicación desde el centro de administración<!-- 7220536, CM6024389 -->
Ahora podrá iniciar la instalación de una aplicación en tiempo real para un dispositivo asociado al inquilino desde el centro de administración de Microsoft Endpoint Management. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Asociación de inquilinos: CMPivot desde el centro de administración<!--7220536, CM6024392 -->
Podrá incorporar la eficacia de [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, puedan iniciar consultas en tiempo real desde la nube en un dispositivo individual administrado por ConfigMgr y devolver los resultados al centro de administración. Esto proporciona todas las ventajas tradicionales de CMPivot, permitiendo a los administradores de TI y a otros roles designados evaluar rápidamente el estado de los dispositivos en su entorno y tomar medidas. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Asociación de inquilinos: ejecución de scripts desde el centro de administración<!--7220536, CM6234688 -->
Podrá incorporar la eficacia de la característica [Ejecutar scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) local de Configuration Manager al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, ejecuten scripts de PowerShell desde la nube en un dispositivo administrado de Configuration Manager individual. Esto proporciona todas las ventajas tradicionales de los scripts de PowerShell que ya se han definido y aprobado por el administrador de Configuration Manager en este nuevo entorno. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nueva lógica de combinación para dispositivos Windows 10<!--179048-->
En la actualidad, si un cliente restablece la imagen inicial de un dispositivo y luego lo vuelve a inscribir, aparecerán varios registros para el dispositivo en la consola de administración de Microsoft Endpoint Manager. La nueva lógica de combinación está en desarrollo para combinar estos registros duplicados para dispositivos Windows 10.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Plantilla de informe de cumplimiento de Power BI V2.0<!-- 636958  -->
Los administradores podrán actualizar la versión de la plantilla de informe de cumplimiento de Power BI de V1.0 a V2.0. En V2.0 se incluirá un diseño mejorado, así como cambios en los cálculos y datos que se muestran como parte de la plantilla. Para obtener información relacionada, vea [Conexión con el almacenamiento de datos con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.
