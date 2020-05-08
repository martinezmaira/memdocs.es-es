---
title: Nueva versión 1802
titleSuffix: Configuration Manager
description: Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1802 de Configuration Manager.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e7bc30c4350d96654a0f6a6ae548d63c2928e791
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904656"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Novedades de la versión 1802 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1802 para la rama actual de Configuration Manager está disponible como una actualización en la consola. Aplique esta actualización en los sitios que ejecuten las versiones 1702, 1706 o 1710. <!-- baseline only statement: -->Al instalar un nuevo sitio, también está disponible como una versión de línea de base.

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para más información, vea [Resumen de cambios en la rama actual de Configuration Manager, versión 1802](https://support.microsoft.com/help/4101375).

Ahora también están disponibles las siguientes actualizaciones adicionales a esta versión:
- [Paquete acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>
> Más información acerca de:    
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)  
> - [Instalación de actualizaciones en los sitios](../../servers/manage/updates.md)  
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones de la versión 1802 de Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestructura del sitio

### <a name="reassign-distribution-point"></a>Reasignación del punto de distribución
<!-- 1306937 -->
Muchos clientes tienen grandes infraestructuras de Configuration Manager y reducen los sitios primarios o secundarios para simplificar su entorno. Tienen que conservar los puntos de distribución en las ubicaciones de las sucursales para entregar el contenido a los clientes administrados. Estos puntos de distribución a menudo contienen varios terabytes o más de contenido. Este contenido es costoso en términos de tiempo y ancho de banda de red para distribuirlo entre estos servidores remotos. Esta característica permite volver a asignar un punto de distribución a otro sitio primario sin redistribuir el contenido. Esta acción actualiza la asignación del sistema de sitio mientras se conserva todo el contenido en el servidor. Para obtener más información, vea[Reassign a distribution point](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign) (Reasignar un punto de distribución).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configuración de la optimización de distribución de Windows para usar grupos de límites de Configuration Manager
<!-- 1324696 -->
Los grupos de límites de Configuration Manager se usan para definir y regular la distribución de contenido a través de la red corporativa y en las oficinas remotas. La [optimización de distribución de Windows](/windows/deployment/update/waas-delivery-optimization) es una tecnología entre iguales basada en la nube para compartir contenido entre los dispositivos de Windows 10. A partir de esta versión, configure la optimización de distribución para usar los grupos de límites al compartir contenido entre iguales. Una nueva configuración de cliente aplica el identificador del grupo de límites como el identificador del grupo de optimización de distribución en el cliente. Cuando el cliente se comunica con el servicio en la nube de optimización de distribución, utiliza este identificador para buscar elementos del mismo nivel con el contenido deseado. Para obtener más información, consulte [Fundamental concepts for content management](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (Conceptos fundamentales de la administración de contenido).

### <a name="support-for-windows-10-arm64-devices"></a>Compatibilidad con dispositivos Windows 10 ARM64
<!-- 1353704 -->
A partir de esta versión, el cliente de Configuration Manager se admite en dispositivos Windows 10 ARM64. Las características de administración de cliente existentes deben funcionar con estos nuevos dispositivos. Por ejemplo, el inventario de hardware y software, las actualizaciones de software y la administración de aplicaciones. La implementación de sistema operativo no se admite actualmente. 

### <a name="improved-support-for-cng-certificates"></a>Mejora de la compatibilidad con certificados CNG
<!-- 1357314 -->
La versión 1710 de Configuration Manager (rama actual) admite [certificados Cryptography: Next Generation (CNG)](../network/cng-certificates-overview.md). En la versión 1710 se limita la compatibilidad a certificados cliente en determinados escenarios. 

A partir de esta versión, use certificados CNG para los siguientes roles de servidor habilitados para HTTPS:
- Punto de administración
- Punto de distribución
- Punto de actualización de software
- Punto de migración de estado  


### <a name="boundary-group-fallback-for-management-points"></a>Reserva de grupo de límites para puntos de administración
<!-- 1324594 -->
Configure las relaciones de reserva para los puntos de administración entre [grupos de límites](../../servers/deploy/configure/boundary-groups.md). Este comportamiento proporciona mayor control para los puntos de administración que utilizan los clientes. Para obtener más información, vea [Configuración de grupos de límites](../../servers/deploy/configure/boundary-groups.md#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Afinidad de sitio del punto de distribución en la nube
<!--503719-->
Esta característica beneficia a los clientes que tienen una jerarquía de varios sitios dispersa geográficamente con puntos de distribución en la nube. Antes, cuando un cliente basado en Internet buscaba contenido, la lista de puntos de distribución en la nube que recibía el cliente no tenía ningún orden. Este comportamiento podía hacer que los clientes basados en Internet recibiesen contenido de puntos de distribución en la nube geográficamente distantes. La descarga de contenido de un servidor distante suele ser más lenta que la de un servidor más cercano.
 
Con la afinidad de sitio del punto de distribución en la nube, un cliente basado en Internet recibe una lista ordenada. Esta lista da prioridad a los puntos de distribución en la nube del sitio asignado del cliente. Este comportamiento permite al administrador conservar la intención de su diseño en lo que respecta a las descargas de contenido de recursos del sitio.
 

## <a name="management-insights"></a>Información de administración
<!-- 1353967 -->
Información de administración de Configuration Manager proporciona información sobre el estado actual del entorno. La información se basa en el análisis de los datos de la base de datos del sitio. Esta información le ayuda a entender mejor el entorno y tomar medidas en consecuencia. Para obtener más información, vea [Management Insights](../../servers/manage/management-insights.md) (Información de administración).

En configuración Manager 1802, está disponible la información siguiente:
- Aplicaciones:
    - Aplicaciones sin implementaciones
- Servicios en la nube: <!--1356412-->
    - Evaluar la preparación de la administración conjunta 
    - Permitir que los dispositivos estén unidos a Azure Active Directory y sean híbridos
    - Modernizar la infraestructura de identidad y acceso
    -  Actualizar los clientes a Windows 10, versión 1709 o superior 
- Recopilaciones:
    - Recopilaciones vacías
- Administración simplificada:  <!--1355148-->
    - Versiones de cliente obsoletas  
- Centro de software: 
    - Dirigir a los usuarios al Centro de software en lugar de al Catálogo de aplicaciones  
    - Usar la nueva versión del Centro de software 
- Windows 10: <!--1357421-->
    - Configurar la telemetría de Windows y la clave de id. comercial 
    - Conexión de Configuration Manager con Upgrade Readiness 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Administración de cliente

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Compatibilidad con Cloud Management Gateway para Azure Resource Manager
<!-- 1324735 -->
Al crear una instancia de [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG), el asistente proporciona ahora la opción de crear una **implementación de Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) es una moderna plataforma para administrar todos los recursos de la solución como una única entidad, denominada [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Al implementar CMG con Azure Resource Manager, el sitio usa Azure Active Directory (Azure AD) para autenticar y crear los recursos necesarios en la nube. Esta implementación modernizada no requiere el certificado de administración de Azure clásico. Para obtener más información, vea [CMG topology design](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager) (Diseño de la topología de CMG).

> [!IMPORTANT]
> Esta función no habilita la compatibilidad de los proveedores de servicios en la nube (CSP) de Azure. La implementación de CMG con Azure Resource Manager sigue usando el servicio en la nube clásico, que no es compatible con los proveedores de servicios en la nube. Para obtener más información, vea [Servicios de Azure disponibles en el programa CSP de Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Mejoras en Cloud Management Gateway  

- A partir de esta versión, **Cloud Management Gateway** ya no es una característica de versión preliminar.  

- La documentación de las características se ha revisado y mejorado. Vea los siguientes artículos para más información:
    - [Planificación de Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Números de tamaño y escala de System Center Configuration Manager](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Seguridad y privacidad de la puerta de enlace de administración en la nube](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Preguntas más frecuentes sobre Cloud Management Gateway](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Certificados para la puerta de enlace de administración en la nube](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Configurar puerta de enlace de administración en la nube](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configurar el inventario de hardware para recopilar cadenas de más de 255 caracteres
<!-- 1357389 -->
Puede configurar la longitud de las cadenas de modo que tengan más de 255 caracteres para las propiedades del inventario de hardware. Este cambio se aplica únicamente a las clases recién agregadas y a las propiedades de inventario del hardware que no son claves. Para obtener más información, vea el artículo [Cómo ampliar el inventario de hardware](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255). 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Anuncio de desuso de la compatibilidad con clientes de Linux y UNIX
 <!--510139-->
Microsoft tiene la intención de dejar en desuso la compatibilidad con clientes de Linux y UNIX en Configuration Manager aproximadamente dentro de un año, de modo que los clientes no se incluirán en la versión 1902 en el calendario de principios de 2019. La versión Configuration Manager 1810, a finales del calendario de 2018, será la última que incluya los clientes de Linux y UNIX, y se admitirán para el ciclo de vida completo de Configuration Manager 1810. Después de Configuration Manager 1810, los clientes deben considerar la posibilidad de usar Microsoft Azure Management para administrar servidores Linux. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

### <a name="surface-device-dashboard"></a>Panel de dispositivos Surface
<!--1355788-->
El panel de dispositivos Surface proporciona información sobre los dispositivos Surface del entorno. En la consola, vaya a **Supervisión** > **Dispositivos Surface**. Puede ver estos elementos:
- El porcentaje de dispositivos Surface
- El porcentaje de modelos Surface
- Las primeras cinco versiones de firmware

Para obtener más información, vea el artículo [Surface dashboard](../../clients/manage/surface-device-dashboard.md) (Panel de Surface).

### <a name="change-in-the-configuration-manager-client-install"></a>Cambio en la instalación del cliente de Configuration Manager
<!--1356195-->
A partir de esta versión, Silverlight ya no se instala automáticamente en los dispositivos cliente. Para más información, vea [Requisitos previos para la implementación de clientes en equipos Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies).

## <a name="co-management"></a>Administración conjunta

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Transición de la carga de trabajo de Endpoint Protection a Intune mediante la administración conjunta
<!-- 1357365 -->
 La carga de trabajo de Endpoint Protection se puede pasar a Intune después de habilitar la administración conjunta. Para realizar la transición de la carga de trabajo de Endpoint Protection, vaya a la página de propiedades de la administración conjunta y mueva la barra deslizante de Configuration Manager a **Piloto** o **Todos**. Para ver detalles sobre las cargas de trabajo, consulte el artículo sobre las [cargas de trabajo de administración conjunta](../../../comanage/workloads.md). Para obtener más información sobre la administración conjunta, vea [Administración conjunta para dispositivos de Windows 10](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Panel de administración conjunta en Configuration Manager
<!--1356648-->
A partir de esta versión, puede ver un panel con información sobre la administración conjunta. El panel le ayudará a revisar las máquinas que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención. Para obtener más información, vea el artículo [Co-management dashboard](../../../comanage/how-to-monitor.md#co-management-dashboard) (Panel de administración conjunta). 


## <a name="compliance-settings"></a>Configuración de cumplimiento

### <a name="microsoft-edge-browser-policies"></a>Directivas del explorador Microsoft Edge
<!-- 1357310 -->
Para los clientes que usan el explorador web [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) en los clientes de Windows 10, cree una directiva de configuración de cumplimiento de Configuration Manager para configurar varias opciones de Microsoft Edge. Para obtener más información, vea [Create Microsoft Edge browser profile](../../../compliance/deploy-use/browser-profiles.md) (Crear el perfil del explorador Microsoft Edge). 



## <a name="application-management"></a>Administración de aplicaciones

### <a name="allow-user-interaction-when-installing-an-application"></a>Permitir la interacción del usuario al instalar una aplicación
<!-- 1356976 -->
Puede permitir que un usuario final interactúe con la instalación de una aplicación durante la ejecución de la secuencia de tareas. Por ejemplo, ejecute un proceso de instalación que solicite al usuario final diversas opciones. En algunos instaladores de aplicaciones no se pueden silenciar los mensajes, o bien el proceso de instalación puede requerir valores de configuración específicos que solo conoce el usuario. Esta característica permite controlar estos escenarios de instalación. Para obtener más información, vea [Especificar opciones de experiencia del usuario para el tipo de implementación](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>No actualizar automáticamente las aplicaciones reemplazadas
<!-- 1351266 -->
Configure una implementación de aplicación de modo que no actualice automáticamente las versiones reemplazadas. Ahora, al crear la implementación, en la página **Configuración de implementación** del **Asistente para implementar software**, para cada propósito de instalación **Disponible**, puede habilitar o deshabilitar la opción **Actualizar automáticamente cualquier versión reemplazada de esta aplicación**. Para obtener más información, vea [Especificar la configuración de implementación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Aprobación de solicitudes de aplicación para los usuarios por dispositivo
<!-- 1357015 -->
A partir de esta versión, cuando un usuario solicita una aplicación que requiere aprobación, el nombre de dispositivo específico ahora forma parte de la solicitud. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. Para obtener más información, vea [Especificar la configuración de implementación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

 > [!Note]  
 > Esta característica es opcional. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../servers/manage/install-in-console-updates.md#bkmk_options).  


### <a name="run-scripts-improvements"></a>Mejoras en Ejecutar scripts 
<!-- 1236459 -->
 A partir de esta versión, **Ejecutar scripts** ya no es una característica de versión preliminar. La salida del script ahora realiza la devolución con el formato JSON. Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md).


## <a name="operating-system-deployment"></a>Implementación de sistema operativo

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Secuencia de tareas de actualización en contexto de Windows 10 a través de Cloud Management Gateway
<!-- 1357149 -->
La [secuencia de tareas de actualización en contexto](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) de Windows 10 ahora admite la implementación en los clientes basados en Internet que se administran a través de [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md). Esta función permite a los usuarios remotos actualizar con mayor facilidad a Windows 10 sin necesidad de conectarse a la red corporativa. Para obtener más información, vea [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Mejoras en la secuencia de tareas de actualización en contexto de Windows 10
<!-- 1357425 -->
La plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 ahora incluye grupos adicionales con las acciones recomendadas que se agregarán antes y después del proceso de actualización. Estas acciones son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Para obtener más información, vea [Crear una secuencia de tareas para actualizar un sistema operativo](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Mejoras en la implementación de sistema operativo
Esta versión incluye las siguientes mejoras para la implementación del sistema operativo:
- En Windows PE, al iniciar cmtrace.exe, ya no se le solicita que elija si este programa se debe establecer como el visor predeterminado para los archivos de registro. <!-- SMS 500897 -->
- Agregue imágenes de arranque al paso de secuencia de tareas [Descargar contenido de paquete](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent).
- Mejoras en el paso [Ejecutar secuencia de tareas](../../../osd/understand/task-sequence-steps.md#child-task-sequence): <!-- 1261338 -->   
  - Compatibilidad con todos los escenarios de implementación de sistemas operativos desde el Centro de Software, el entorno PXE y soportes físicos.
  - Mejoras en las acciones de la consola como copiar, importar, exportar y advertir durante la eliminación de objetos.
  - Compatibilidad con el [Asistente para crear archivos de contenido preconfigurados](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).
  - Integración con Verificación de la implementación. Para obtener más información, vea [Implementaciones de secuencias de tareas de alto riesgo](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - El paso Ejecutar secuencia de tareas ahora puede usarse en los distintos niveles de secuencias de tareas, no solo en una relación de elementos primarios y secundarios. Las relaciones de varios niveles aumentan la complejidad, así que úselas con precaución. Estas relaciones se siguen comprobando para las referencias circulares.

### <a name="deployment-templates-for-task-sequences"></a>Plantillas de implementación para secuencias de tareas
<!-- 1357391 -->
El [Asistente para la implementación de secuencias de tareas](../../../osd/deploy-use/deploy-a-task-sequence.md) ahora puede crear una plantilla de implementación. La plantilla de implementación puede guardarse y aplicarse a una secuencia de tareas nueva o existente para crear una implementación. 

### <a name="phased-deployments-for-task-sequences"></a>Implementaciones por fases para secuencias de tareas
<!--1356837-->
 Las implementaciones por fases son una [característica de versión preliminar](../../servers/manage/pre-release-features.md). Las implementaciones por fases automatizan una implementación coordinada y secuencial de una secuencia de tareas en varias recopilaciones. Puede [crear implementaciones por fases](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) con el valor predeterminado de dos fases, o bien configurar manualmente varias fases. La implementación por fases de las secuencias de tareas no es compatible con la instalación de medios o PXE.




## <a name="software-center"></a>Centro de software

### <a name="install-multiple-applications-in-software-center"></a>Instalar varias aplicaciones en el Centro de software
<!-- 1357126 -->
Si un usuario final o técnico de escritorio necesita instalar varias aplicaciones en un dispositivo, ahora en el Centro de software se admite la instalación de varias aplicaciones seleccionadas. Este comportamiento permite que el usuario sea más eficaz, al no tener que esperar a que finalice una instalación antes de iniciar la siguiente. Para obtener más información, vea [Install multiple applications](../../understand/software-center.md#install-multiple-applications) (Instalar varias aplicaciones) en la nueva guía de usuario del Centro de software.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Uso del Centro de software para buscar e instalar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD
<!-- 1322613 -->
Si implementa aplicaciones como disponibles para los usuarios, ahora puede examinarlas e instalarlas a través del Centro de software en dispositivos de Azure Active Directory (Azure AD). Para obtener más información, vea cómo [implementar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Ocultar aplicaciones instaladas en el Centro de software
<!--1357592-->
Ahora, las aplicaciones instaladas se pueden ocultar en el Centro de software. Las aplicaciones que estén instaladas ya no aparecerán en la pestaña Aplicaciones cuando se habilite esta opción en la configuración del cliente. Esta opción se establece como valor predeterminado al instalar o actualizar a Configuration Manager 1802.  Las aplicaciones instaladas siguen estando disponibles para su revisión en la pestaña Estado de la instalación. Infórmese sobre cómo [ocultar aplicaciones instaladas en el Centro de software](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled).   

### <a name="hide-unapproved-applications-in-software-center"></a>Ocultar aplicaciones no aprobadas en el Centro de software
 <!--1355146-->
Cuando esta opción de la configuración del cliente está habilitada, las aplicaciones disponibles para los usuarios que necesiten aprobación se ocultan en el Centro de software.  Infórmese sobre cómo [ocultar aplicaciones no aprobadas en el Centro de software](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved).  

### <a name="software-center-shows-user-additional-compliance-information"></a>El Centro de software muestra información de cumplimiento adicional del usuario
<!-- 1235616 -->
 Al usar el estado Atestación de estado de dispositivo como regla de directiva de cumplimiento para el acceso condicional a los recursos de la empresa, el Centro de software ahora muestra al usuario la configuración de Atestación de estado de dispositivo que no es compatible.


 ## <a name="software-updates"></a>Actualizaciones de software 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Programe la evaluación de reglas de implementación automática para que se desplacen con respecto a un día base. 
<!--1357133-->
Las reglas de implementación automática se pueden programar para evaluar el desplazamiento con respecto a un día base. Es decir, si la revisión del martes en su caso cae en miércoles, se puede establecer la programación de evaluación para el segundo martes del mes con un desplazamiento de un día. Para obtener más información, vea [Implementar actualizaciones de software automáticamente](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Generación de informes

### <a name="report-for-default-browser-counts"></a>Informe sobre la cantidad de exploradores predeterminados
<!-- 1357830 -->
Ahora hay un nuevo informe para mostrar la cantidad de clientes con un explorador web específico como valor predeterminado de Windows. Vea el informe **Recuentos de exploradores predeterminados** en el grupo de informes **Software - Companies and Products** (Software: compañías y productos). Para obtener más información, vea [Lista de informes](../../servers/manage/list-of-reports.md#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Información de dispositivo Windows AutoPilot
<!-- 1351442 -->
Windows AutoPilot es una solución para la incorporación y configuración de nuevos dispositivos de Windows 10 de forma moderna. Para más información, consulte [Resumen de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Un método para registrar dispositivos existentes con Windows AutoPilot es cargar la información de dispositivo a Microsoft Store para Empresas y Educación. Esta información incluye el número de serie del dispositivo, el identificador de producto de Windows y un identificador de hardware. Use Configuration Manager para recopilar y notificar esta información del dispositivo con el nuevo informe, **Información del dispositivo de Windows AutoPilot**, en el nodo de informes **Hardware: general**. Para más información, consulte el artículo sobre la [preparación de dispositivos basados en Internet para la administración conjunta](../../../comanage/how-to-prepare-Win10.md#windows-autopilot).

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Informe sobre los detalles de mantenimiento de Windows 10 para una recopilación específica
<!--1357653-->
En el informe **Detalles de mantenimiento de Windows 10 para una colección específica** se muestra información general sobre el mantenimiento de Windows 10 para una recopilación específica. En este informe aparecen el identificador de recurso, el nombre de NetBIOS, el nombre del sistema operativo, la compilación, la rama de sistema operativo y el estado del servicio para dispositivos Windows 10. Para obtener más información, vea [Lista de informes](../../servers/manage/list-of-reports.md#operating-system).



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Proteger los dispositivos

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Mejoras en las directivas de Configuration Manager para Protección contra vulnerabilidades de seguridad de Windows Defender
<!-- 1356220 -->
Se han agregado nuevos parámetros de directivas para los componentes [Reducción de la superficie expuesta a ataques](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) y [Acceso controlado a carpetas](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) en Configuration Manager para [Protección contra vulnerabilidades de seguridad de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Nueva configuración de interacción de host para Protección de aplicaciones de Windows Defender
<!-- 1356256 -->
Para Windows 10 versión 1709 y dispositivos posteriores, hay dos nuevas opciones de interacción de host para [Protección de aplicaciones de Windows Defender](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS): 
- A los sitios web se les puede conceder acceso al procesador de gráficos virtuales del host. 
- Los archivos descargados en el contenedor se pueden conservar en el host. 




## <a name="configuration-manager-console"></a>Consola de Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Mejoras en la consola de Configuration Manager 
Esta versión incluye las mejoras siguientes en la consola de Configuration Manager.
- En las listas de dispositivos bajo Activos y compatibilidad, Dispositivos, ahora se muestra el usuario primario de forma predeterminada. En esta columna solo se muestra en el nodo dispositivos. También se puede agregar el último usuario que inició sesión como columna opcional.<!-- 1357280 --> Habilite la configuración de cliente de [afinidad entre usuario y dispositivo](../../clients/deploy/about-client-settings.md#user-and-device-affinity) para que el sitio asocie un usuario primario con un dispositivo.
- Si una recopilación es miembro de otra y se cambia de nombre, el nuevo nombre se actualiza en las reglas de pertenencia.<!--1357282--> 
- Cuando se usa el control remoto en un cliente con varios monitores en una escala de PPP distinta, el cursor del mouse ahora se asigna correctamente entre ellos. <!--433170-->
- En el [panel de administración de clientes de Office 365](../../../sum/deploy-use/office-365-dashboard.md) se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico. <!--1357281 --> 



## <a name="next-steps"></a>Pasos siguientes
Cuando esté listo para instalar esta versión, consulte el artículo sobre [actualizaciones de Configuration Manager](../../servers/manage/updates.md).
