---
title: Administración de la sincronización de actualizaciones de software
titleSuffix: Configuration Manager
description: Siga estos pasos para programar la sincronización de actualizaciones de software, iniciar la sincronización de actualizaciones de software de forma manual y supervisar la sincronización de actualizaciones de software.
ms.date: 05/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d36c6a02868b8ccde9538a286135b2ad1ce08f43
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83269055"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a> Sincronizar actualizaciones de software

*Se aplica a: Configuration Manager (rama actual)*

 La sincronización de las actualizaciones de software en Configuration Manager es el proceso de recuperación de los metadatos de actualización de software que cumplen los criterios que configure. Esto incluye productos, clasificaciones e idiomas específicos. Normalmente, el punto de actualización de software en el sitio de administración central o en un sitio primario independiente recupera los metadatos de Microsoft Update. Después, el sitio de nivel superior enviará una solicitud de sincronización a otros sitios. Cuando un sitio recibe una solicitud de sincronización desde el sitio primario, el punto de actualización de software del sitio recupera metadatos de las actualizaciones de software desde su [origen de la sincronización](../plan-design/plan-for-software-updates.md#BKMK_SyncSource) del canal de subida. Para obtener más información sobre la sincronización de actualizaciones de software, consulte [Sincronización de las actualizaciones de software](../understand/software-updates-introduction.md#BKMK_Synchronization).

La sincronización de la actualización de software se configura para que se ejecute según una programación en las propiedades del punto de actualización de software en el sitio de nivel superior. Después de configurar la programación de la sincronización, normalmente no cambiará la programación como parte de las operaciones normales. Pero puede iniciar manualmente la sincronización de la actualización de software cuando sea necesario.

  > [!NOTE]  
  >  Los puntos de actualización de software deben estar conectados a su origen de la sincronización del canal de subida para sincronizar las actualizaciones de software. Cuando se desconecta un punto de actualización de software de su origen de la sincronización del canal de subida, puede utilizar el método de exportación e importación para sincronizar las actualizaciones de software. Para obtener más información, consulte [Sincronizar actualizaciones de software desde un punto de actualización de software desconectado](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Programar la sincronización de las actualizaciones de software
Cuando configura una programación de sincronización de actualizaciones de software, el punto de actualización de software de nivel superior inicia la sincronización con Microsoft Update en la fecha y hora programadas. La programación personalizada permite sincronizar las actualizaciones de software en un momento en que la demanda del servidor Windows Server Update Services (WSUS), el servidor de sitio y la red sea baja. Por ejemplo, puede establecer la programación de modo que las actualizaciones de software se sincronicen una vez a la semana a las 2:00 a. m. Durante la sincronización programada, todos los cambios en los metadatos de las actualizaciones de software desde la última sincronización programada se insertan en la base de datos del sitio. Esto incluye nuevos metadatos de actualizaciones de software o metadatos que se modificaron, se eliminaron o expiraron.

Use los procedimientos siguientes en el sitio de nivel superior para programar la sincronización de las actualizaciones de software.  

#### <a name="to-schedule-software-updates-synchronization"></a>Para programar la sincronización de las actualizaciones de software  

  1.  En la consola de Configuration Manager, haga clic en **Administración**.  

  2.  En el área de trabajo Administración, expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

  3.  En el panel de resultados, haga clic en el sitio de administración central o el sitio primario independiente.  

  4.  En la pestaña **Inicio** , en el grupo **Configuración** , expanda **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**.  

  5.  En el cuadro de diálogo Propiedades de componente de punto de actualización de software, seleccione **Habilitar sincronización según una programación**y, a continuación, especifique la programación de la sincronización.  

## <a name="manually-start-software-updates-synchronization"></a>Iniciar de forma manual la sincronización de las actualizaciones de software
Puede iniciar de forma manual la sincronización de actualizaciones de software en el sitio de nivel superior en la consola de Configuration Manager desde el nodo **Todas las actualizaciones de software** del área de trabajo **Biblioteca de software**.  

Use los procedimientos siguientes en el sitio de nivel superior para iniciar de forma manual la sincronización de las actualizaciones de software.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Para iniciar de forma manual la sincronización de las actualizaciones de software  

1. En la consola de Configuration Manager que está conectada al sitio de administración central o al sitio primario independiente, haga clic en **Biblioteca de software**.  

2. En el área de trabajo Biblioteca de software, expanda **Actualizaciones de software** y haga clic en **Todas las actualizaciones de software** o en **Grupos de actualizaciones de software**.  

3. En la pestaña **Inicio**, en el grupo **Todas las actualizaciones de software**, haga clic en **Sincronizar actualizaciones de software**. Haga clic en **Sí** en el cuadro de diálogo para confirmar que desea iniciar el proceso de sincronización.  

   Después de iniciar el proceso de sincronización en el punto de actualización de software, puede supervisar el proceso de sincronización desde la consola de Configuration Manager para todos los puntos de actualización de software de la jerarquía. Utilice el siguiente procedimiento para supervisar el proceso de sincronización de las actualizaciones de software.  


## <a name="monitor-software-updates-synchronization"></a>Supervisar la sincronización de las actualizaciones de software
Después de iniciar el proceso de sincronización, puede usar la consola de Configuration Manager para supervisar el proceso de todos los puntos de actualización de software de la jerarquía. Utilice el siguiente procedimiento para supervisar el proceso de sincronización de la actualización de software. Para obtener más información sobre cómo supervisar las actualizaciones de software, incluido el proceso de sincronización, consulte [Supervisar actualizaciones de software](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para supervisar el proceso de sincronización de las actualizaciones de software  

1. En la consola de Configuration Manager, haga clic en **Supervisión**.  

2. En el área de trabajo **Supervisión** , haga clic en **Estado de sincronización de punto de actualización de software**.  

   Los puntos de actualización de software de la jerarquía de Configuration Manager se muestran en el panel de resultados. Desde esta vista, puede supervisar el estado de la sincronización de todos los puntos de actualización de software. Para obtener más información detallada sobre el proceso de sincronización, revise el archivo wsyncmgr.log, que se encuentra en <*RutaInstalaciónConfigurationManager*>\Logs en cada servidor de sitio.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importación de actualizaciones desde el catálogo de Microsoft Update

En el punto de actualización de software de nivel superior se usa WSUS para obtener información sobre las actualizaciones de software de Microsoft en Configuration Manager. En ocasiones, es posible que necesite una actualización que no se sincroniza de forma automática en WSUS para los productos y las clasificaciones seleccionados, pero que está disponible en el [catálogo de Microsoft Update](https://catalog.update.microsoft.com). Las actualizaciones que no se sincronizan de forma automática en WSUS normalmente están diseñadas para resolver problemas muy específicos. Normalmente, si una actualización está disponible en el catálogo, puede importarla a WSUS. Después, puede sincronizarla en Configuration Manager e implementarla como cualquier otra actualización.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Para importar una actualización desde el catálogo de Microsoft Update

1. Abra la consola de administración de WSUS y conéctela al servidor WSUS de nivel superior de la jerarquía.
   - Si Internet Explorer no es el explorador web predeterminado del equipo, establézcalo temporalmente como el predeterminado.
2. Haga clic en **Actualizaciones** o en el nombre del servidor WSUS. 
3. En el panel **Acciones**, haga clic en **Importar actualizaciones...** , lo que abrirá una ventana del explorador con el [catálogo de Microsoft Update](https://catalog.update.microsoft.com).
   ![Selección de Importar actualizaciones en la consola de WSUS](media/wsus-console-import-updates.png)
4. Si se le solicita, instale el control ActiveX del catálogo de Microsoft Update. El control se debe instalar para importar las actualizaciones en WSUS. 
5. En la ventana del explorador, busque la actualización que quiera. Haga clic en el botón **Agregar*** para agregarla a la cesta.
6. Haga clic en **Ver cesta**. Asegúrese de que está seleccionada la opción **Importar directamente en Windows Server Update Services**. Después, haga clic en **Importar**.
    ![Importación de la actualización desde el catálogo a WSUS](./media/import-catalog-update-into-wsus.png)
7. Una vez completada la importación, haga clic en **Cerrar** en la ventana del explorador.
     - Si es necesario, restablezca el explorador predeterminado.
8. Sincronice el punto de actualización de software de Configuration Manager.


## <a name="next-steps"></a>Pasos siguientes
Después de sincronizar las actualizaciones de software por primera vez o después de que haya clasificaciones o productos nuevos, debe [configurar los productos y clasificaciones nuevos](configure-classifications-and-products.md) para sincronizar las actualizaciones de software con los nuevos criterios.

Después de sincronizar las actualizaciones de software con los criterios que necesite, [administre la configuración de las actualizaciones de software](manage-settings-for-software-updates.md).  
