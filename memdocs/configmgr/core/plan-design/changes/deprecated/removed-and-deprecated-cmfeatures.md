---
title: Características en desuso
titleSuffix: Configuration Manager
description: Obtenga información sobre las características que Configuration Manager ya no admite.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 29b5dd8fdceb803de77aff9adbd0614d1e201b18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694266"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Características en desuso y eliminadas de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo enumera las características que están en desuso o no reciben soporte técnico de Configuration Manager. Las características en desuso se van a quitar en una futura actualización. Estos cambios futuros podrían afectar al uso de Configuration Manager.  

Esta información está sujeta a cambios en futuras versiones. Podría no incluir todas las características de Configuration Manager en desuso.

## <a name="deprecated-features"></a>Características en desuso

Las siguientes características están en desuso. Ahora todavía puede usarlas, pero Microsoft planea finalizar la compatibilidad en el futuro.

|Característica|Primer anuncio del desuso|Soporte técnico&nbsp;eliminado|
|-----------|---|--------------|
|Ha cambiado la implementación para compartir contenido de Azure. Use una puerta de enlace de administración en la nube habilitada para contenido. No podrá crear un punto de distribución en la nube tradicional en el futuro.|Febrero de 2019|Por determinar<sup>[Nota 1](#bkmk_note1)</sup>|
|Implementación del servicio clásico en Azure para la puerta de enlace de administración y el punto de distribución en la nube. Para obtener más información, vea [Planificación de Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|Noviembre de 2018|Por determinar<sup>[Nota 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Nota 1: Soporte eliminado Por determinar

Se debe determinar el período de tiempo específico (TBD). Microsoft recomienda que cambie al nuevo proceso o característica, pero puede continuar usando el proceso o la característica en desuso en el futuro próximo.

## <a name="unsupported-and-removed-features"></a>Características no admitidas y eliminadas

Ya no se admiten las características siguientes. En algunos casos, ya no están en el producto.

|Característica|Primer anuncio del desuso|Soporte técnico&nbsp;eliminado|  
|-----------|---|--------------|  
| Opción de Análisis de escritorio para **Ver datos recientes** para la inscripción de dispositivos y las actualizaciones de seguridad.<!-- 7080949 --> Para más información, consulte [Latencia de datos](../../../../desktop-analytics/troubleshooting.md#data-latency).|Mayo de 2020|Julio de 2020|
| Integración de Windows Analytics y Upgrade Readiness. Para más información, consulte [KB 4521815: Windows Analytics se retirará el 31 de enero de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14 de octubre de 2019 | 31 de enero de 2020 |
| Evaluación de la atestación de estado de dispositivo para las directivas de cumplimiento de acceso condicional <!--1235616 aka 3608202--> Para obtener más información, vea [¿Qué ha ocurrido con la MDM híbrida?](../../../../mdm/understand/what-happened-to-hybrid.md)| 3 de julio de 2019 | Versión 1910 |
| La aplicación Portal de empresa para Configuration Manager | 21 de mayo de 2019 | Versión 1910 |
| El catálogo de aplicaciones que incluye los dos roles de sistema de sitio: el punto de sitios web del catálogo de aplicaciones y el punto de servicios web. Para más información, vea [Eliminación del catálogo de aplicaciones](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21 de mayo de 2019 | Versión 1910 |
|Autenticación basada en certificados con configuración de Windows Hello para empresas en Configuration Manager<br>Para más información, vea [Configuración de Windows Hello para empresas](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|Diciembre de 2017|Versión 1910|
|System Center Endpoint Protection para Mac y Linux<br>Para obtener más información, vea la [entrada del blog de fin del soporte técnico](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|Octubre de 2018|31 de diciembre de 2018|
|Acceso condicional local<br>Para obtener más información, vea [¿Qué ha ocurrido con la MDM híbrida?](../../../../mdm/understand/what-happened-to-hybrid.md)|30 de enero de 2019|1 de septiembre de 2019|
|Administración híbrida de dispositivos móviles (MDM)<br>Para obtener más información, vea [¿Qué ha ocurrido con la MDM híbrida?](../../../../mdm/understand/what-happened-to-hybrid.md)<br><br>A partir de la versión de servicio 1902 de Intune, prevista para finales de febrero de 2019, los nuevos clientes no pueden crear una conexión híbrida.<!--Intune feature 2683117-->|14 de agosto de 2018|1 de septiembre de 2019|
|Extensiones de Security Content Automation Protocol (SCAP). <!--3607889--><br>La versión anterior con certificado aún está disponible en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=48741).|Septiembre de 2018|Versión 1810|
|La **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite. Los usuarios deben utilizar el nuevo Centro de software. Para obtener más información, consulte [Configurar el centro de software](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11 de agosto de 2017| Versión 1806|
|La versión anterior del Centro de software.<br><br>Para obtener más información sobre el nuevo Centro de software, vea [Planear y configurar la administración de aplicaciones](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|13 de diciembre de 2016|Versión 1802|
|Administración de discos duros virtuales (VHD) con Configuration Manager. <br><br>Este desuso incluye la eliminación de opciones para crear un nuevo VHD o administrar un VHD con una secuencia de tareas, y la eliminación del nodo de discos duros virtuales de la consola de Configuration Manager. <br><br>Los VHD existentes no se eliminan, pero ya no son accesibles desde la consola de Configuration Manager.  |6 de enero de 2017 |Versión 1710|
|Secuencias de tareas: <br /> - Convertir el disco en dinámico <br /> - Instalar herramientas de implementación |18 de noviembre de 2016|Versión 1710|
|Herramienta de evaluación de actualizaciones<br><br>La Herramienta de evaluación de actualizaciones depende de Configuration Manager y del kit de herramientas de compatibilidad de aplicaciones (ACT) 6.x. La versión final de ACT se ha entregado en Windows 10 v1511 ADK. Como no hay más actualizaciones para ACT, se interrumpe el soporte para la Herramienta de evaluación de actualizaciones. El aviso de desuso se agregó a la [página de descarga de UAT](https://www.microsoft.com/software-download/windows10) el 12 de septiembre de 2016. | 12 de septiembre de 2016  | 11 de julio de 2017 |
|Puntos de actualización de software con un clúster de equilibrio de carga de red (NLB) | 27 de febrero de 2016 | Versión 1702 |
|Secuencias de tareas: <br /> - OSDPreserveDriveLetter  <br /><br /> Ahora, durante una implementación del sistema operativo, el programa de instalación de Windows determina, de forma predeterminada, cuál es la mejor letra de unidad (normalmente C:). Si quiere especificar otra unidad, puede cambiar la ubicación en el paso de secuencia de tareas Aplicar el sistema operativo. Vaya a la opción de configuración **Seleccionar la ubicación en la que desea aplicar este sistema operativo**. Seleccione **Letra de unidad lógica específica** y elija la unidad que desee utilizar. |20 de junio de 2016 |Versión 1606 |
|Protección de acceso a redes (NAP): como aparece en System Center 2012 Configuration Manager|10 de julio de 2015|Versión 1511|  
|Administración fuera de banda: como aparece en System Center 2012 Configuration Manager|16 de octubre de 2015|Versión 1511|

### <a name="features-removed-in-version-1511"></a>Características eliminadas de la versión 1511

Las secciones siguientes incluyen detalles adicionales de las características eliminadas con la versión 1511:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Administración fuera de banda  

Con Configuration Manager, se ha quitado la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager.  

- Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). El complemento permite el acceso a las funciones más recientes para administrar AMT, a la vez que elimina las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios.  

- La administración fuera de banda en System Center 2012 Configuration Manager no se ve afectada por este cambio.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Protección de acceso a redes

Configuration Manager ha eliminado la compatibilidad con Protección de acceso a redes. La característica quedó en desuso en Windows Server 2012 R2 y se eliminó en Windows 10.  

Para alternativas de protección de acceso a redes, consulte la sección *Funcionalidad en desuso* de [Información general sobre servicios de acceso y directivas de redes](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)).

## <a name="see-also"></a>Vea también

- [Elementos eliminados y en desuso](removed-and-deprecated.md)
- [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle)
- [Compatibilidad con versiones de la rama actual de Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)