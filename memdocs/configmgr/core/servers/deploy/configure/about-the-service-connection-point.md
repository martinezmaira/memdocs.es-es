---
title: Punto de conexión de servicio
titleSuffix: Configuration Manager
description: Obtenga información sobre este rol de sistema de sitio de Configuration Manager y comprenda y planee sus diversos usos.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704953"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Acerca del punto de conexión de servicio en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

El punto de conexión de servicio es un rol de sistema de sitio que proporciona varias funciones importantes para la jerarquía. Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus posibilidades de uso. La planificación del uso podría afectar su forma de configurar este rol de sistema de sitio:

- Descargar las actualizaciones que se aplican a su infraestructura de Configuration Manager: solo se ponen a disposición las actualizaciones apropiadas para la infraestructura, según los datos de uso que se carguen.

- Cargar datos de uso desde su infraestructura de Configuration Manager: puede controlar el nivel o la cantidad de detalle que se carga. Para obtener más información, vea [Configuración y niveles de datos de uso](../install/setup-reference.md#bkmk_usage).

- Implementar una instancia de [Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md) en Azure.

- Sincronizar aplicaciones desde [Microsoft Store para Empresas y Educación](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

- Detectar usuarios y grupos en [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc).

- Usar [Análisis de escritorio](../../../../desktop-analytics/overview.md) para obtener información sobre la preparación de aplicaciones y actualizaciones de Windows 10.

Cada jerarquía admite una única instancia de este rol. Solo se puede instalar en el sitio de nivel superior de la jerarquía, es decir, un sitio de administración central (CAS) o un sitio primario independiente. Si expande un sitio primario independiente a una jerarquía más grande, desinstale este rol del sitio primario y, después, instálelo en el CAS.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a> Modos de operación

El punto de conexión de servicio admite dos modos de funcionamiento:

- **En línea**: El punto de conexión de servicio comprueba si existen actualizaciones automáticamente cada 24 horas. Descarga automáticamente las nuevas actualizaciones disponibles para la infraestructura y la versión del producto actuales para que estén disponibles en la consola de Configuration Manager.

- **Sin conexión**: El punto de conexión de servicio no se conecta al servicio en la nube de Microsoft. Para importar manualmente las actualizaciones disponibles, puede usar la [herramienta de conexión de servicio](../../manage/use-the-service-connection-tool.md).

### <a name="change-mode"></a>Cambio de modo

Si cambia entre los modos con conexión o sin conexión después de instalar el punto de conexión de servicio, reinicie el subproceso **SMS_DMP_DOWNLOADER** del servicio SMS_Executive. Al reiniciar el subproceso, el cambio entra en vigor. Para reiniciar el subproceso, use el Administrador de servicios de Configuration Manager.

> [!TIP]
> También puede reiniciar el servicio SMS_Executive para Configuration Manager, con lo que se reinician la mayoría de componentes del sitio. Como alternativa, espere una tarea programada, como una copia de seguridad del sitio, que detenga y después reinicie el servicio SMS_Executive.

Para usar el Administrador de servicios de Configuration Manager para reiniciar el subproceso SMS_DMP_DOWNLOADER:

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y haga clic en el nodo **Estado del componente**. En la cinta de opciones, seleccione **Inicio** y, después, **Administrador de servicios de Configuration Manager**.

1. En el panel de navegación del administrador de servicios, expanda el sitio, expanda **Componentes** y, después, seleccione el componente que quiera reiniciar: **SMS_DMP_DOWNLOADER**.

1. Vaya al menú **Componente** y seleccione **Consulta**.

1. Confirme el estado actual del componente. Después, vaya al menú **Componente** y seleccione **Detener**.  

1. **Consulte** el componente de nuevo para confirmar que se ha detenido. Después, seleccione la acción **Iniciar componente** para reiniciarlo.

## <a name="remote-site-system-requirements"></a>Requisitos del sistema del sitio remoto

Al instalar el punto de conexión de servicio en un servidor de sistema de sitio alejado del servidor de sitio, configure los requisitos siguientes:

- La cuenta de equipo del servidor de sitio tiene que ser un administrador local del equipo que hospeda un punto de conexión de servicio remoto.

- Configure el servidor de sistema de sitio que hospeda el rol con una [cuenta de instalación de sistema de sitio](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). El administrador de distribución del servidor de sitio usa la cuenta de instalación de sistema de sitio para transferir las actualizaciones desde el punto de conexión de servicio.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a> Requisitos de acceso a Internet

Si la organización restringe la comunicación de red con Internet a través de un dispositivo proxy o firewall, necesita permitir que el punto de conexión de servicio acceda a los puntos de conexión de Internet.

Para más información, consulte los [requisitos de acceso a Internet](../../../plan-design/network/internet-endpoints.md#bkmk_scp).

## <a name="install"></a>Instalar

Cuando ejecute la **Instalación** para instalar el sitio de nivel superior de una jerarquía, puede instalar el punto de conexión de servicio.

Después de ejecutar la instalación, o si vuelve a instalar el rol, use el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio**. (Instale el punto de conexión de servicio solo en el sitio de nivel superior de la jerarquía). Para más información, consulte [Instalación de roles de sistema de sitio para System Center Configuration Manager](install-site-system-roles.md).

## <a name="move-the-role"></a><a name="bkmk_move"></a> Traslado del rol

<!-- SCCMDocs#922 -->
Hay varios escenarios en los que puede que necesite trasladar el punto de conexión de servicio a otro servidor:

- [Recuperación](../../manage/recover-sites.md)
- [Alta disponibilidad de servidor de sitio](site-server-high-availability.md)
- [Expansión de sitios](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Después de trasladar el punto de conexión de servicio, compruebe todas las funciones del sitio. Por ejemplo, quizá tenga que renovar la clave secreta para las conexiones a los inquilinos de Azure Active Directory (Azure AD). Para más información, vea [Renovar clave secreta](azure-services-wizard.md#bkmk_renew).

## <a name="log-files"></a>Archivos de registro

Para consultar información sobre las cargas en Microsoft, vea **Dmpuploader.log** en el servidor en que se ejecuta el punto de conexión de servicio. Para el progreso de descarga de las actualizaciones, vea **Dmpdownloader.log**. Para obtener la lista completa de registros relacionados con el punto de conexión de servicio, vea [Archivo de registro: Punto de conexión de servicio](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog).

## <a name="next-steps"></a>Pasos siguientes

Use los siguientes diagramas de flujo para comprender las entradas del registro de claves y el flujo de proceso. Este proceso incluye descargas de actualización y replicación de actualizaciones en otros sitios.

- [Diagrama de flujo: descargar actualizaciones](../../manage/download-updates-flowchart.md)

- [Diagrama de flujo: replicación de actualización](../../manage/update-replication-flowchart.md)
