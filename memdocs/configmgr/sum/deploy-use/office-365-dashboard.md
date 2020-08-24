---
title: Panel de administración de clientes de Office 365
titleSuffix: Configuration Manager
description: Revisión de la información de los clientes de Aplicaciones de Microsoft 365 en el panel de administración de clientes de Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: bae995b0704e2b2774d5f002cbf907777a3edcf0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697048"
---
# <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365

*Se aplica a: Configuration Manager (rama actual)*

> [!Note]
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.

A partir de la versión 1802 de Configuration Manager, puede revisar la información de los clientes de Aplicaciones de Microsoft 365 en el panel de administración de clientes de Office 365. En el panel de administración de clientes de Office 365 se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico. <!--1357281 -->

## <a name="prerequisites"></a>Requisitos previos

### <a name="enable-hardware-inventory"></a>Habilitación del inventario de hardware

Los datos que se muestran en el panel de administración de clientes de Office 365 proceden de inventario de hardware. Habilite el inventario de hardware y seleccione la clase de inventario de hardware **Configuraciones de Office 365 ProPlus** antes de que los datos aparezcan en el panel.
 
1. Habilite el inventario de hardware, si aún no está habilitado. Para obtener más información, consulte [Configurar el inventario de hardware](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. En la consola de Configuration Manager, navegue a **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  
3. En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
4. En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  
5. En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  
6. En el cuadro de diálogo **Clases de inventario de hardware**, seleccione **Configuración de Office 365 ProPlus**.  
7. Haga clic en **Aceptar** para guardar los cambios y cerrar la **clases de inventario de Hardware** cuadro de diálogo.

El panel de administración de clientes de Office 365 comenzará a mostrar los datos a medida que se informe del inventario de hardware.

### <a name="connectivity-for-top-level-site-server"></a>Conectividad para el servidor de sitio de nivel superior

*(Introducido en la versión 1906 como requisito previo)*

El servidor de sitio de nivel superior necesita acceso al siguiente punto de conexión para descargar el archivo de preparación:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> No se requiere conectividad a Internet para los dispositivos cliente en ninguno de estos escenarios.

### <a name="enable-data-collection-for-microsoft-365-apps"></a>Habilitación de la recopilación de datos para Aplicaciones de Microsoft 365

*(Introducido en la versión 1910 como requisito previo)*

A partir de la versión 1910, deberá habilitar la recopilación de datos para Aplicaciones de Microsoft 365 para rellenar la información en el **Panel de estado y piloto de Office 365 ProPlus**. Los datos se almacenan en la base de datos de sitio de Configuration Manager y no se envían a Microsoft.

Estos datos son diferentes de los datos de diagnóstico, que se describen en [Datos de diagnóstico enviados desde Aplicaciones de Microsoft 365 a Microsoft](/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft).

Puede habilitar la recopilación de datos usando una directiva de grupo o editando el registro.

#### <a name="enable-data-collection-from-group-policy"></a>Habilitación de la recopilación de datos de una directiva de grupo

1. Descargue los [archivos de plantillas administrativas más recientes desde el Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=49030).
2. Habilite la configuración de directiva **Activar la recopilación de datos de telemetría** en `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard`.
    - Alternativamente, puede aplicar la configuración de directiva con el [servicio de directivas de la nube de Office](/DeployOffice/overview-office-cloud-policy-service).
    - La configuración de directiva también se usa en el panel de telemetría de Office, que no es necesario implementar para esta recopilación de datos.

#### <a name="enable-data-collection-from-the-registry"></a>Habilitación de la recopilación de datos del registro

El siguiente comando es un ejemplo de cómo habilitar la recopilación de datos en el registro:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visualización del panel de administración de clientes de Office 365

Para ver el panel de administración de clientes de Office 365 en la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**. En la parte superior del panel, use la opción desplegable **Colección** para filtrar los datos del panel por miembros de una colección determinada. A partir de la versión 1802 de Configuration Manager, en el panel de administración se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico.

El panel de administración de clientes de Office 365 proporciona una serie de gráficos con la siguiente información:

- Número de clientes de Aplicaciones de Microsoft 365
- Versiones de clientes de Aplicaciones de Microsoft 365
- Idiomas de clientes de Aplicaciones de Microsoft 365
- Canales de clientes de Aplicaciones de Microsoft 365. Para más información, vea [Información general sobre los canales de actualización de Aplicaciones de Microsoft 365](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-microsoft-365-apps-readiness"></a><a name="bkmk_o365_readiness"></a> Integración de la preparación de Aplicaciones de Microsoft 365
<!--3735402-->
A partir de la versión 1902 de Configuration Manager, se puede usar el panel para identificar los dispositivos con una confianza alta de que estén listos para actualizar a Aplicaciones de Microsoft 365. Esta integración proporciona conclusiones sobre los posibles problemas de compatibilidad con los complementos y las macros usados en su entorno. Después, use Configuration Manager para implementar Aplicaciones de Microsoft 365 en los dispositivos que estén listos.

El panel de administración de clientes de Office365 incluye un nuevo icono, **Office 365 ProPlus Upgrade Readiness**. Este icono es un gráfico de barras de los dispositivos con los siguientes estados:
- No evaluado
- Preparado para la actualización
- Necesita revisión

Seleccione un estado para obtener los detalles en una lista de dispositivos. En este informe de preparación se muestran más detalles sobre los dispositivos. Se incluyen columnas para el estado de compatibilidad de los complementos y las macros.

### <a name="prerequisites-for-microsoft-365-apps-readiness-integration"></a>Requisitos previos para la integración de la preparación de Aplicaciones de Microsoft 365

- Habilite el inventario de hardware en la configuración de cliente. Para más información, consulte la sección [Requisitos previos](#prerequisites).  

- El dispositivo necesita disponer de conectividad a la red de entrega de contenido (CDN) de Office para poder descargar el archivo de preparación de un complemento. Para obtener más información, vea [Redes de entrega de contenido](/office365/enterprise/content-delivery-networks). Si el dispositivo no puede descargar el archivo, el estado de los complementos será *Necesita revisión*.  

    > [!Note]  
    > No se envía ningún dato a Microsoft en relación con esta característica.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a> Preparación de la macro detallada

De manera predeterminada, el agente de detección busca en la lista de archivos usados más recientemente (MRU por sus siglas en inglés) de cada dispositivo. Cuenta los archivos de la lista que admiten macros. Estos archivos pueden ser de los siguientes tipos:
- Formatos de archivos de Office habilitados para macros, como libros habilitados para macros de Excel (.xlsm) o documentos habilitados para macros de Word (.docm).  
- Formatos de Office más antiguos que no indican si hay contenido de macro, como un libro de Excel 97-2003 (.xls).

Si necesita información más detallada sobre la compatibilidad con macros, implemente **Readiness Toolkit for Office** para analizar el código de los archivos de macro. Comprueba si hay cualquier posible problema de compatibilidad. Por ejemplo, que un archivo use una función que pueda cambiar en una versión más reciente de Office. Después de ejecutar Readiness Toolkit for Office y seleccionar la opción **Complementos instalados y documentos de Office usados recientemente en este equipo**, o usar la marca `-mru` en la línea de comandos, el agente de inventario de hardware de Configuration Manager puede seleccionar los resultados. Estos datos adicionales permiten mejorar el cálculo de la preparación del dispositivo. Para más información, vea [Uso de Readiness Toolkit para evaluar la compatibilidad de aplicaciones para Aplicaciones de Microsoft 365](https://aka.ms/readinesstoolkit).

Tenga en cuenta que no es necesario que Readiness Toolkit esté instalado en todos los dispositivos de destino para poder realizar el análisis. Puede usar la opción de línea de comandos de ejemplo siguiente para examinar cada dispositivo deseado.  La marca de salida es necesaria, pero los archivos no se usarán para generar los resultados en el panel, por lo que se puede seleccionar cualquier ubicación válida.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Para obtener más información, vea [Obtener información de preparación para varios usuarios en una empresa](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="microsoft-365-apps-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a> Panel de preparación de Aplicaciones de Microsoft 365

*(Se introdujo en la versión 1906)*

<!--4021125-->
Para ayudar a determinar qué dispositivos están listos para actualizar a Aplicaciones de Microsoft 365, hay un panel de preparación a partir de la versión 1906. Incluye el icono de **Upgrade Readiness para Office 365 ProPlus** que se publicó en la versión 1902 de la rama actual de Configuration Manager. Los siguientes iconos nuevos de este panel le ayudan a evaluar la preparación de las macros y los complementos:

- Implementación
- Preparación de los dispositivos
- Preparación de complementos
- Instrucciones de compatibilidad de complementos
- Complementos principales por número de versión
- Número de dispositivos que tienen macros
- Preparación de las macros
- Avisos de macros

El siguiente vídeo es una sesión de Ignite 2019, que incluye más información:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Prácticas recomendadas para la evaluación de compatibilidad y actualizaciones de Microsoft Office 365 ProPlus con Office Readiness en Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-microsoft-365-apps-upgrade-readiness-dashboard"></a>Uso del panel de Upgrade Readiness para Aplicaciones de Microsoft 365

Después de comprobar que cumple con los [requisitos previos](#prerequisites), utilice las siguientes instrucciones para usar el panel:
 
1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y expanda **Administración de clientes de Office 365**.
1. Seleccione el nodo **Upgrade Readiness para Aplicaciones de Microsoft 365**.
1. Cambie la **arquitectura de Office de colección** y **destino** para cambiar la información retransmitida en el panel.

[![Panel de Upgrade Readiness para Aplicaciones de Microsoft 365](./media/4021125-office-365-upgrade-readiness-dashboard.png)](./media/4021125-office-365-upgrade-readiness-dashboard.png#lightbox)

[![Complementos del panel de Upgrade Readiness para Aplicaciones de Microsoft 365](./media/4021125-office-365-to-add-ins.png)](./media/4021125-office-365-to-add-ins.png#lightbox)

[![Advertencias de macros del panel de Upgrade Readiness para Aplicaciones de Microsoft 365](./media/4021125-office-365-macro-advisories.png)](./media/4021125-office-365-macro-advisories.png#lightbox)

### <a name="device-readiness-information"></a>Información de preparación de los dispositivos

Cuando se haya evaluado el complemento y el inventario de macros en cada dispositivo, los dispositivos se agrupan de acuerdo con la información. Es probable que los dispositivos cuyo estado aparece como **Listo para actualizar** no tengan ningún problema de compatibilidad.

Al seleccionar la categoría **Listo para actualizar** en el gráfico se muestran más detalles sobre los dispositivos en la recopilación de restricción. Puede revisar la lista de dispositivos, hacer selecciones según sus requisitos empresariales y crear una nueva recopilación de dispositivos a partir de la selección. Use la nueva colección para implementar Aplicaciones de Microsoft 365 con Configuration Manager.

Los dispositivos que pueden estar en riesgo de incidencias de compatibilidad se marcan como **Necesita revisión**. Es posible que estos dispositivos requieran realizar alguna acción antes de actualizarlos a Aplicaciones de Microsoft 365. Por ejemplo, puede actualizar los complementos críticos a una versión más reciente.

### <a name="add-in-information"></a>Información de complementos

 En cada dispositivo se recopila un inventario de todos los complementos instalados. Después, el inventario se compara con la información que Microsoft tiene sobre el rendimiento del complemento en Aplicaciones de Microsoft 365. Si se encuentra un complemento que es probable que cause problemas después de la actualización, todos los dispositivos con el complemento se marcan para su revisión.

### <a name="macro-information"></a>Información de macros

Configuration Manager examina los archivos usados más recientemente en cada dispositivo. Cuenta los archivos de esta lista que admiten macros, incluidos los tipos siguientes:

- Formatos de archivo de Office habilitados para macros.
- Formatos de Office anteriores, que no indican si hay contenido de macros.

Este informe se puede usar para identificar los dispositivos que han usado recientemente archivos que podrían contener macros. Después, puede implementarse **Readiness Toolkit for Office** mediante Configuration Manager para examinar los dispositivos en los que se necesita información más detallada y comprobar si hay algún problema de compatibilidad potencial. Por ejemplo, si un archivo usa una función que cambió en una versión más reciente de Aplicaciones de Microsoft 365.

Para obtener más información sobre cómo llevar a cabo el examen, vea [Preparación de la macro detallada](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a> Piloto y panel de estado de Office 365 ProPlus
<!--4488272, 4488301-->
*(Se incluyó en la versión 1910)*

A partir de la versión 1910, el **Piloto y panel de estado de Office 365 ProPlus** lo ayuda a planear, probar y realizar la implementación de Aplicaciones de Microsoft 365. El panel proporciona información sobre el estado de los dispositivos con Aplicaciones de Microsoft 365 para ayudar a identificar posibles problemas que puedan afectar a los planes de implementación. En el **Panel de estado y piloto de Office 365 ProPlus** se proporciona una recomendación para dispositivos piloto basada en el inventario de complementos. Los iconos siguientes están en el panel:

- Generación del piloto
- Dispositivos piloto recomendados
- Implementación del piloto
- Dispositivos que envían datos de mantenimiento
- Dispositivos que no cumplen los objetivos de mantenimiento
- Complementos que no cumplen los objetivos de mantenimiento
- Macros que no cumplen los objetivos de mantenimiento

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Uso del piloto y el panel de estado de Office 365 ProPlus

Después de comprobar que cumple con los [requisitos previos](#prerequisites), utilice las siguientes instrucciones para usar el panel:

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y expanda **Administración de clientes de Office 365**.
1. Seleccione el nodo **Piloto y panel de estado de Office 365 ProPlus**.

![Panel de estado y piloto de Office 365 ProPlus](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Generación del piloto

Genere una recomendación piloto a partir de una recopilación de restricción al hacer clic en un botón. En cuanto se inicia la acción, una tarea en segundo plano comienza a calcular la recopilación piloto. La recopilación de restricción debe contener al menos un dispositivo con una versión de Office que no sea ProPlus.

### <a name="recommended-pilot-devices"></a>Dispositivos piloto recomendados

**Los dispositivos piloto recomendados** son un conjunto mínimo de dispositivos que representan todos los complementos instalados en la recopilación de restricción que se ha usado al generar el piloto. Explore en profundidad para obtener una lista de estos dispositivos. Después, use los detalles para excluir los dispositivos del piloto, si es necesario. Si todos los complementos ya están en los dispositivos con Aplicaciones de Microsoft 365, los dispositivos con esos complementos no se incluirán en el cálculo. Esto también significa que es posible que no obtenga ningún resultado en la recopilación piloto, ya que todos los complementos se han detectado en dispositivos en los que están instaladas las Aplicaciones de Microsoft 365.

### <a name="deploy-pilot"></a>Implementación del piloto

Cuando acepte los dispositivos piloto, implemente Aplicaciones de Microsoft 365 en la recopilación piloto mediante el asistente para la implementación por fases. Los administradores pueden definir el piloto y limitar la recopilación en el asistente para administrar las implementaciones.

### <a name="health-data"></a>Datos de mantenimiento

Una vez instaladas las Aplicaciones de Microsoft 365, habilite los datos de mantenimiento en los dispositivos piloto. Los datos de mantenimiento proporcionan información sobre los complementos y macros que no cumplen los objetivos de mantenimiento. El gráfico **Dispositivos listos para implementar** identifica los dispositivos no piloto listos para la implementación mediante el uso de la información de mantenimiento. Obtenga un recuento de los dispositivos que envían datos de mantenimiento desde el gráfico **Dispositivos que envían datos de mantenimiento**.

### <a name="devices-not-meeting-health-goals"></a>Dispositivos que no cumplen los objetivos de mantenimiento

Este icono resume los dispositivos que tienen problemas con complementos, macros o ambos.

### <a name="add-ins-not-meeting-health-goals"></a>Complementos que no cumplen los objetivos de mantenimiento

- Errores de descarga: no se pudo iniciar el complemento.
- Bloqueos: error en el complemento mientras se estaba ejecutando.
- Error: el complemento informó un error.
- Varios problemas: el complemento tiene más de uno de los problemas anteriores.

### <a name="macros-not-meeting-health-goals"></a>Macros que no cumplen los objetivos de mantenimiento

- Errores de descarga: no se pudo cargar el documento.
- Errores en tiempo de ejecución: se produjo un error mientras se ejecutaba la macro. Estos errores pueden depender de las entradas, por lo que puede que no se produzcan siempre.
- Errores de compilación: la macro no se compiló correctamente, por lo que no intentará ejecutarse.
- Varios problemas: la macro tiene más de uno de los problemas anteriores.

> [!NOTE]
> El inventario de macros se rellena con datos de Readiness Toolkit for Office y archivos de datos usados recientemente. El estado de las macros se rellena con los datos de estado. Debido a los diferentes orígenes de datos, es posible que el estado de mantenimiento de las macros sea **Necesita revisión** cuando el inventario de macros sea **No examinado**. <!--5922845-->

### <a name="known-issues"></a>Problemas conocidos

Hay un problema conocido con el icono de **Implementar piloto**. En este momento no se puede usar para realizar la implementación en un piloto. La solución alternativa es el flujo de trabajo existente para implementar una aplicación mediante el Asistente para la implementación por fases. <!--5525871-->

## <a name="next-steps"></a>Pasos siguientes

[Administración de actualizaciones de Aplicaciones de Microsoft 365 con Configuration Manager](manage-office-365-proplus-updates.md)