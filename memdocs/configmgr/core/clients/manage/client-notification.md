---
title: Notificación de cliente
titleSuffix: Configuration Manager
description: Administra clientes al tomar medidas inmediatas desde la consola central de Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a00f77a5a902728a7c41905314511cffcfa81a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694963"
---
# <a name="client-notification-in-configuration-manager"></a>Notificación de cliente de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para tomar medidas inmediatas en clientes remotos, envíe una acción de notificación de cliente desde la consola de Configuration Manager. Tome estas medidas en un dispositivo individual o en una colección de dispositivos.

## <a name="actions"></a>Acciones

Las siguientes acciones están en la cinta, en el grupo Dispositivo o Colección de la pestaña Inicio.

### <a name="install-client"></a>Instalar cliente

Se abre el **Asistente para la instalación de cliente**. Este asistente usa la instalación de inserción de cliente para instalar un cliente de Configuration Manager. Para obtener más información, vea [Instalación de inserción de cliente](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

#### <a name="permissions---install-client"></a>Permisos: instalar cliente

Esta acción requiere los permisos **Modificar recurso** y **Leer** en el objeto **Colección**.

Los siguientes roles integrados tienen estos permisos de forma predeterminada:

- Administrador de aplicaciones  
- Administrador total  
- Administrador de infraestructuras  
- Administrador de operaciones  
- Administrador de implementaciones del sistema operativo  

Agregue estos permisos a los roles personalizados que necesitan insertar el cliente.

### <a name="run-script"></a>Ejecutar script

Se abre el Asistente para **ejecutar script** para ejecutar un script de PowerShell en todos los clientes de la recopilación. Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

#### <a name="permissions---run-script"></a>Permisos: ejecutar script

Esta acción requiere el permiso **Ejecutar script** en el objeto **Colección**.

Los siguientes roles integrados tienen este permiso de forma predeterminada:

- Administrador total  
- Administrador de infraestructuras  
- Administrador de operaciones  

Agregue este permiso a cualquier rol personalizado que deba ejecutar scripts.

### <a name="start-cmpivot"></a>Iniciar CMPivot

Inicia **CMPivot**, que ejecuta consultas en tiempo real en los dispositivos de destino. Para obtener más información, vea [CMPivot](../../servers/manage/cmpivot.md).

#### <a name="permissions---start-cmpivot"></a>Permisos: iniciar CMPivot

Esta acción requiere los mismos permisos que la acción [Ejecutar script](#run-script).

A partir de la versión 1906, puede usar el permiso **Ejecutar CMPivot** en el objeto **Collection**.

## <a name="client-notification"></a>Notificación de cliente

Las siguientes acciones están en el menú **Notificación de cliente**, en la cinta, en el grupo Dispositivo o Colección de la pestaña Inicio.

En la versión 1806 o anterior, la opción **Notificación de cliente** solo está disponible en el nodo Colección de dispositivos o cuando veía la pertenencia de una colección de dispositivos. A partir de la versión 1810, puede iniciar una **Notificación de cliente** directamente desde el nodo **Dispositivos**. Ya no es requisito estar dentro de la vista de la pertenencia a una colección. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Permisos: notificación de cliente

<!--SCCMDocs-pr issue #2972-->
A partir de la versión 1810, las acciones de notificación de cliente requieren el permiso **Notificar al recurso** en el objeto Colección. Este permiso se aplica a todas las acciones del menú **Notificación de cliente**.

Los siguientes roles integrados tienen este permiso de forma predeterminada:

- Administrador total  
- Administrador de operaciones  

Agregue este permiso a cualquier rol personalizado que deba usar acciones de notificación de cliente.

### <a name="download-computer-policy"></a>Descargar directiva de equipo

Actualiza la directiva de dispositivo. Para obtener más información, vea [Iniciar la recuperación de directivas para un cliente de Configuration Manager](manage-clients.md#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Descargar directiva de usuario

Actualiza la directiva de usuario.  

### <a name="collect-discovery-data"></a>Recopilar datos de detección

Desencadena clientes para enviar un registro de datos de detección (DDR). Para obtener más información, vea [Heartbeat Discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat) (Detección de latidos).  

### <a name="collect-software-inventory"></a>Recopilar inventario de software

Desencadena clientes para ejecutar un ciclo de inventario de software. Para obtener más información, vea [Introducción al inventario de software](inventory/introduction-to-software-inventory.md).  

### <a name="collect-hardware-inventory"></a>Recopilar información de inventario de hardware

Desencadena clientes para ejecutar un ciclo de inventario de hardware. Para obtener más información, vea [Introducción al inventario de hardware](inventory/introduction-to-hardware-inventory.md).  

### <a name="evaluate-application-deployments"></a>Evaluar implementaciones de aplicaciones

Desencadena clientes para ejecutar un ciclo de evaluación de implementación de aplicaciones. Para obtener más información, vea [Programar la reevaluación para implementaciones](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Evaluar implementaciones de actualizaciones de software

Desencadena clientes para ejecutar un ciclo de evaluación de implementación de actualizaciones de software. Para obtener más información, vea [Introducción a las actualizaciones de software](../../../sum/understand/software-updates-introduction.md).  

### <a name="switch-to-the-next-software-update-point"></a>Cambiar al siguiente punto de actualización de software

Desencadena clientes para cambiar al siguiente punto de actualización de software disponible. Para obtener más información, vea [Cambio de punto de actualización de software](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching).  

### <a name="evaluate-device-health-attestation"></a>Evaluar Atestación de estado de dispositivo

Desencadena clientes de Windows 10 para comprobar y enviar su estado de dispositivo más reciente. Para más información, vea [Atestación de estado](../../servers/manage/health-attestation.md).  

### <a name="wake-up"></a>Reactivar

A partir de la versión 1810, desencadena la reactivación de los dispositivos configurados para admitir Wake-on-LAN mediante otros dispositivos de la misma subred para enviar el paquete Wake-on-LAN. Para obtener más información, vea [Cómo configurar Wake on LAN](../deploy/configure-wake-on-lan.md).

### <a name="restart"></a>Reiniciar

Desencadena los dispositivos seleccionados para que se reinicien. Para más información, vea [Reinicio de clientes](manage-clients.md#restart-clients).

## <a name="client-diagnostics"></a>Diagnósticos del cliente
<!--4433455-->

A partir de la versión 1910, hay nuevas acciones de dispositivo de **Diagnósticos del cliente** en la consola de Configuration Manager. Se han agregado las siguientes acciones:

- **Habilitación del registro detallado**: cambie el nivel de registro global del componente CCM a detallado y habilite el registro de depuración.
- **Deshabilitación del registro detallado**: cambie el nivel de registro global a predeterminado y deshabilite el registro de depuración.
- **Recopilar registros de cliente** (a partir de la versión 2002): Se envía un mensaje de notificación a los clientes seleccionados para recopilar los registros de CCM. Los registros se devuelven mediante la recopilación de archivos de inventario de software. <!--4226618-->
   - El límite de tamaño de los registros de cliente comprimidos es de 100 MB. <!--6366098-->
   - Use el [Explorador de recursos](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) para administrar y ver estos archivos.

   [![Recopilación de registros de cliente desde la consola](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - Estas acciones solo cambian el nivel de detalle del registro, no el tamaño ni el historial. Un registro más detallado puede generar más contenido de registro.
> - El rol de punto de administración también usa el componente CCM. Si el dispositivo de destino también es un punto de administración, esta acción también se aplica a ese rol.

Para obtener más información sobre esta configuración, consulte [Acerca de los archivos de registro](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client).

Realice un seguimiento del estado de la tarea en el elemento **diagnostics.log** del cliente. Al recopilar registros de cliente, se registra información adicional en **MP_SinvCollFile. log**, en el punto de administración, y **sinvproc.log**, en el servidor de sitio.

### <a name="prerequisites---client-diagnostics"></a>Requisitos previos: diagnósticos del cliente

- Actualice el cliente de destino a la versión más reciente.

- El usuario administrativo de Configuration Manager necesita el permiso **Notificar el recurso**.

  Los siguientes roles integrados tienen este permiso de forma predeterminada:

  - Administrador total  
  - Administrador de infraestructuras  

  Agregue este permiso a cualquier rol personalizado que deba usar acciones de notificación de cliente.


## <a name="endpoint-protection"></a>Endpoint Protection

Las siguientes acciones están en el menú **Endpoint Protection**. Este menú se encuentra en la cinta, en el grupo Colección de la pestaña Inicio. Cuando se seleccionan uno o más dispositivos, estas acciones pasan a la pestaña **Objeto seleccionado** de la cinta.

Para obtener más información, vea [Endpoint Protection en Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).

### <a name="permissions---endpoint-protection"></a>Permisos: Endpoint Protection

Esta acción requiere el permiso **Aplicar seguridad** en el objeto **Colección**.

Los siguientes roles integrados tienen este permiso de forma predeterminada:

- Administrador total  
- Endpoint Protection Manager  
- Administrador de operaciones  

Agregue este permiso a cualquier rol personalizado que deba desencadenar acciones de Endpoint Protection.

### <a name="full-scan"></a>Examen completo

Desencadena Endpoint Protection o Windows Defender para ejecutar un examen antimalware *completo*.  

### <a name="quick-scan"></a>Examen rápido

Desencadena Endpoint Protection o Windows Defender para ejecutar un examen antimalware *rápido*.  

### <a name="download-definition"></a>Descargar definición

Desencadena Endpoint Protection o Windows Defender para descargar las últimas definiciones de antimalware.  

## <a name="see-also"></a>Vea también

- [Cómo administrar clientes](manage-clients.md)
- [Cómo administrar recopilaciones](collections/manage-collections.md)
