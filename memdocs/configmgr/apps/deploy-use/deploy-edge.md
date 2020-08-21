---
title: Implementación y actualización de Microsoft Edge, versión 77 y posteriores
titleSuffix: Configuration Manager
description: Implementación y actualización de Microsoft Edge, versión 77 y versiones posteriores con Configuration Manager
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc10f262e4639ffdd8513bece662116f5ed39516
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695381"
---
# <a name="microsoft-edge-management"></a>Administración de Microsoft Edge

*Se aplica a: Configuration Manager (rama actual)*

La nueva versión de Microsoft Edge está lista para empresas. A partir de la versión 1910 de Configuration Manager, ahora puede implementar [Microsoft Edge, versión 77 y posteriores](/deployedge/) para los usuarios. Se usa un script de PowerShell para instalar la compilación de Edge seleccionada. El script también desactiva las actualizaciones automáticas para Edge de modo que se puedan administrar con Configuration Manager.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a> Implementación de Microsoft Edge
<!--4561024-->
Los administradores pueden elegir el canal de la versión beta, de desarrollo o estable, junto con una versión del cliente de Microsoft Edge que se va a implementar. Cada versión incorpora aprendizajes y mejoras de nuestros clientes y de la comunidad.

### <a name="prerequisites-for-deploying"></a>Requisitos previos para la implementación

Clientes con una implementación de Microsoft Edge:

- No se puede establecer la [Directiva de ejecución](/powershell/module/microsoft.powershell.core/about/about_execution_policies) de PowerShell en Restringida.
  - PowerShell se ejecuta para realizar la instalación.

- El instalador de Microsoft Edge y [CMPivot](../../core/servers/manage/cmpivot.md) se firman con el certificado **Firma de código de Microsoft**. Si el certificado no aparece en el almacén **Editores de confianza**, deberá agregarlo. De lo contrario, el instalador de Microsoft Edge y CMPivot no se ejecutarán cuando la directiva de ejecución de PowerShell esté establecida en **AllSigned**. <!--7585106-->

El dispositivo que ejecuta la consola de Configuration Manager necesita acceso a los puntos de conexión siguientes:

|Ubicación|Use|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Información sobre las versiones de Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Contenido de las versiones de Microsoft Edge|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a> Comprobación de las directivas de actualización de Microsoft Edge

#### <a name="configuration-manager-version-1910"></a>Configuration Manager, versión 1910

En la versión 1910, cuando se implementa Microsoft Edge, el script de instalación desactiva las actualizaciones automáticas de Microsoft Edge para que se puedan administrar con Configuration Manager. Puede cambiar este comportamiento mediante la directiva de grupo. Para obtener más información, vea [Planear tu implementación de Microsoft Edge](/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) y [Directivas de actualización de Microsoft Edge](/DeployEdge/microsoft-edge-update-policies).

#### <a name="configuration-manager-version-2002-and-later"></a>Versión 2002 y posteriores de Configuration Manager
<!--4561024-->
A partir de la versión 2002 puede crear una aplicación de Microsoft Edge que esté configurada para recibir actualizaciones automáticas en lugar de deshabilitar las actualizaciones automáticas. Este cambio le permite elegir administrar las actualizaciones de Microsoft Edge con Configuration Manager o permitir que Microsoft Edge se actualice automáticamente. Al crear la aplicación, elige la opción para **permitir que Microsoft Edge actualice automáticamente la versión del cliente en el dispositivo del usuario final** en la página de **configuración de Microsoft Edge**. Si ha usado la directiva de grupo para cambiar este comportamiento, la directiva de grupo sobrescribirá la configuración efectuada por Configuration Manager durante la instalación de Microsoft Edge.

[![Configuración de actualización automática de Microsoft Edge](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Creación de una implementación

Cree una aplicación de Microsoft Edge mediante la experiencia de aplicaciones integradas, que facilita la administración de Microsoft Edge:

1. En la consola, en **Biblioteca de software**, hay un nuevo nodo llamado **Administración de Microsoft Edge**.
1. Seleccione **Crear una aplicación de Microsoft Edge** desde la cinta o haciendo clic con el botón derecho en el nodo **Administración de Microsoft Edge**.

   ![Acción de clic con el botón secundario en el nodo de Administración de Microsoft Edge](./media/4561024-create-microsoft-edge-application.png)

1. En la página **Configuración de la aplicación** del asistente, especifique un nombre, una descripción y una ubicación para el contenido de la aplicación. Asegúrese de que la carpeta de ubicación de contenido que especifique esté vacía.
1. En la página **Configuración de Microsoft Edge**, seleccione:
   - Canal que se va a implementar
   - Versión que se va a implementar
   - Si quiere **permitir que Microsoft Edge actualice automáticamente la versión del cliente en el dispositivo del usuario final** (agregado en la versión 2002)
1. En la página **Implementación**, decida si quiere implementar la aplicación. Si selecciona **Sí**, puede especificar la configuración de implementación de la aplicación. Para más información sobre la configuración de implementación, consulte [Implementación de aplicaciones](deploy-applications.md#bkmk_deploy-general).
1. En **Centro de software** en el dispositivo del cliente, el usuario puede ver e instalar la aplicación.

   ![Página de Configuración de Microsoft Edge en el asistente para la implementación](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Archivos de registro para la implementación

|Ubicación|Registro|Use|
|---|---|---|
| Servidor de sitio|SMSProv.log|Muestra detalles si se produce un error en la creación de la aplicación o la implementación.|
| [Varía](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Muestra detalles si se produce un error en la descarga de contenido|
| Cliente|  AppEnforce.log|Muestra información sobre la instalación|

## <a name="update-microsoft-edge"></a>Actualización de Microsoft Edge
<!--4831871-->

A partir de la versión 1910 de Configuration Manager, verá un nodo denominado **Todas las actualizaciones de Microsoft Edge** en **Administración de Microsoft Edge**. Este nodo lo ayuda a administrar las actualizaciones de todos los canales de Microsoft Edge.<!--initial edge updates released Jan 15,2020-->

1. Para obtener actualizaciones de Microsoft Edge, asegúrese de que tiene la clasificación **Actualizaciones** y el producto **Microsoft Edge** [seleccionado para la sincronización](../../sum/get-started/configure-classifications-and-products.md).

   [![Selección de Microsoft Edge como producto en las propiedades del punto de actualización de software](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. En el área de trabajo **Biblioteca de software**, expanda **Administración de Microsoft Edge** y haga clic en el nodo **Todas las actualizaciones de Microsoft Edge**.

1. Si es necesario, haga clic en **Sincronizar actualizaciones de software** en la cinta de opciones para iniciar una sincronización. Para más información, vea [Sincronizar actualizaciones de software](../../sum/get-started/synchronize-software-updates.md).

   ![Nodo de todas las actualizaciones de Microsoft Edge](./media/4831871-all-microsoft-edge-updates.png)

1. Administre e implemente las actualizaciones de Microsoft Edge como cualquier otra actualización, por ejemplo, al agregarlas a la [regla de implementación automática](../../sum/deploy-use/automatically-deploy-software-updates.md). Entre las tareas de actualización comunes que puede realizar desde el nodo **Todas las actualizaciones de Microsoft Edge** se incluyen:

   - [Creación de una implementación por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Implementar actualizaciones de software manualmente](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Descargar actualizaciones de software](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Panel Administración de Microsoft Edge
<!--3871913-->
*(Introducido en la versión 2002)*

A partir de Configuration Manager 2002, el panel Administración de Microsoft Edge le proporciona información sobre el uso de Microsoft Edge y otros exploradores. En este panel, puede hacer lo siguiente:

- Ver cuántos dispositivos tienen instalado Microsoft Edge
- Vea cuántos clientes tienen instaladas versiones diferentes de Microsoft Edge.
   - Este gráfico no incluye el canal Canary.
- Ver los exploradores instalados en todos los dispositivos
- Ver el explorador preferido en cada dispositivo <!--5907383-->
   - Actualmente, para la versión 2002, este gráfico estará vacío.

### <a name="prerequisites-for-the-dashboard"></a>Requisitos previos del panel

Habilite las siguientes propiedades en las clases de [inventario de hardware](../../core/clients/manage/inventory/extend-hardware-inventory.md) que aparecen más abajo para el panel de administración de Microsoft Edge:

- **Software instalado: Asset Intelligence (SMS_InstalledSoftware)**
   - Código de software
   - Nombre de producto
   - Versión del producto

- **Explorador predeterminado (SMS_DefaultBrowser)**
   - Id. de programa del explorador

- **Uso del explorador (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>Ver el panel

En el área de trabajo **Biblioteca de software**, haga clic en **Administración de Microsoft Edge** para ver el panel. Haga clic en **Examinar** y seleccione otra colección para los datos del gráfico. De forma predeterminada, la lista desplegable incluye las cinco colecciones más grandes. Al seleccionar una colección que no está en la lista, la colección recién seleccionada pasa a ocupar la parte inferior de la lista desplegable.

[![Panel Administración de Microsoft Edge](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="known-issues"></a>Problemas conocidos

### <a name="hardware-inventory-may-fail-to-process"></a>Es posible que no se pueda procesar el inventario de hardware.
<!--7535675-->
Es posible que no se procese el inventario de hardware de los dispositivos. Pueden aparecer errores similares al siguiente en el archivo Dataldr.log:

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**Mitigación:** Para solucionar este problema, deshabilite la recopilación de la clase de inventario de hardware Uso del explorador (SMS_BrowerUsage).

## <a name="next-steps"></a>Pasos siguientes

[Supervisar aplicaciones](monitor-applications-from-the-console.md)

[Supervisar actualizaciones de software](../../sum/deploy-use/monitor-software-updates.md)

[Administración y supervisión de implementaciones por fases](../../osd/deploy-use/manage-monitor-phased-deployments.md)