---
title: Uso de Asset Intelligence
titleSuffix: Configuration Manager
description: Realice tareas comunes de Asset Intelligence en Configuration Manager.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1e272e8e71ceaa15c712cb3a53d9db835747d327
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695073"
---
# <a name="how-to-use-asset-intelligence-in-configuration-manager"></a>Cómo usar Asset Intelligence en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este tema contiene información para ayudarle a administrar las tareas típicas de Asset Intelligence en la jerarquía de Configuration Manager:  

##  <a name="view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Ver información de Asset Intelligence  
 Puede ver información de Asset Intelligence en la página principal de **Asset Intelligence** y en los informes de Asset Intelligence.  

###  <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Página principal de Asset Intelligence  
 En la página principal de **Asset Intelligence** se muestra un panel de resumen para obtener información sobre el catálogo Asset Intelligence. En la página principal, puede ver información sobre la sincronización del catálogo y el estado de software inventariado. La página principal de **Asset Intelligence** se divide en las siguientes secciones:  

- **Sincronización del catálogo**: ofrece información sobre si Asset Intelligence está habilitada, el estado actual del punto de sincronización de Asset Intelligence, la programación de sincronización, si se importó el informe de licencia del cliente, cuándo se actualizó por última vez el estado y la hora de la siguiente actualización programada, y el número de cambios que se han producido después de que se instalara el sistema de sitio del punto de sincronización de Asset Intelligence.  

  > [!NOTE]  
  >  La sección de sincronización del catálogo Asset Intelligence de la página principal de **Asset Intelligence** aparece únicamente si se ha instalado un rol de sistema de sitio del punto de sincronización de Asset Intelligence.  

- **Estado de software inventariado**: ofrece el recuento y porcentaje de software inventariado, categorías de software y familias de software que identifica Microsoft o un usuario administrativo, están pendientes de identificación en línea, o no tienen identificación y no están pendientes de ella. En la información que se representa en formato de tabla se muestra el recuento de cada uno, mientras que en la información del gráfico se muestra el porcentaje.  

  Use el procedimiento siguiente para ver información de Asset Intelligence en la página principal de **Asset Intelligence** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Cómo ver información de Asset Intelligence en la página principal de Asset Intelligence  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**. Se muestran los informes de Asset Intelligence.  

###  <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Informes de Asset Intelligence  
 Hay más de 60 informes de Asset Intelligence que muestran la información que ha recopilado Asset Intelligence. Muchos de estos informes vinculan a otros más específicos en los que puede consultar información general y profundizar para obtener información más detallada. Los informes de Asset Intelligence se encuentran en la consola de Configuration Manager, en el área de trabajo **Supervisión**, en el nodo **Informes**. Los informes ofrecen información sobre el hardware, la administración de licencias y el software. Para obtener más información sobre los informes en Configuration Manager, consulte [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  La precisión del número de títulos de software instalados y la información de licencias que se muestran en los informes de Asset Intelligence puede variar del número real de títulos de software instalados o licencias en uso en el entorno, debido a las limitaciones y dependencias complejas que forman parte del inventario de la información de licencia de software de los títulos de software instalados en los entornos empresariales. Los informes de Asset Intelligence no deben utilizarse como el único origen para determinar la compatibilidad de las licencias de software adquiridas.  

 Use el procedimiento siguiente para ver información de Asset Intelligence mediante los informes de Asset Intelligence.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Cómo ver información de Asset Intelligence mediante los informes de Asset Intelligence  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , expanda **Generación de informes**, luego expanda **Informes**y después haga clic en **Asset Intelligence**. Se muestran los informes de Asset Intelligence.  

    > [!WARNING]  
    >  Si no existe ninguna carpeta de informes en el nodo **Informes** , compruebe que ha configurado la creación de informes. Para obtener más información, vea [Configuración de informes](../../../../core/servers/manage/configuring-reporting.md).  

3.  Seleccione el informe de Asset Intelligence que quiera ejecutar y, en la pestaña **Inicio** , en el grupo **Grupo de informes** , haga clic en **Ejecutar**.  

##  <a name="synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a> Sincronizar el catálogo Asset Intelligence  
 Puede sincronizar el catálogo Asset Intelligence local con System Center Online para recuperar la categorización de títulos de software más reciente. Cuando solicita manualmente la sincronización del catálogo con System Center Online, el proceso de sincronización podría tardar 15 minutos o más. Configuration Manager actualiza el valor **Última actualización correcta** en la página principal de **Asset Intelligence** con la hora actual para cuando la sincronización finalice correctamente.  

> [!NOTE]  
>  Antes de utilizar los procedimientos, debe instalarse un rol de sistema de sitio del punto de sincronización de Asset Intelligence. Para más información sobre cómo instalar un punto de sincronización de Asset Intelligence, vea [Configurar Asset Intelligence en Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Utilice el procedimiento siguiente para crear una programación de sincronización para el catálogo Asset Intelligence.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Cómo crear una programación de sincronización para el catálogo Asset Intelligence  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**.  

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Sincronizar**y luego en **Programar sincronización**.  

4. En el cuadro de diálogo **Programación de puntos de sincronización de Asset Intelligence** , seleccione **Habilitar sincronización según una programación**y después configure una programación simple o personalizada.  

5. Haga clic en **Aceptar** para guardar los cambios.  

   > [!NOTE]  
   >  Para obtener información sobre la programación de sincronización, incluida la próxima sincronización programada, consulte el nodo **Asset Intelligence** en el área de trabajo **Activos y compatibilidad** en el sitio de nivel superior de la jerarquía.  

   Utilice el procedimiento siguiente para sincronizar manualmente el catálogo Asset Intelligence.  

> [!WARNING]  
>  System Center Online solo acepta una solicitud de sincronización manual en un período de 12 horas.  

###  <a name="to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> Cómo sincronizar manualmente el catálogo Asset Intelligence  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Sincronizar**, luego en **Sincronizar catálogo Asset Intelligence**y después en **Aceptar**.  

##  <a name="customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a> Personalizar el catálogo Asset Intelligence  
 La información de categorización del catálogo Asset Intelligence recibida de System Center Online se almacena en la base de datos del sitio con permisos de solo lectura y no se puede modificar ni eliminar. Sin embargo, puede crear, modificar y eliminar categorías de software personalizado, familias de software, etiquetas de software e información de catálogo de los requisitos de hardware. Después puede usar datos de categorización personalizada en lugar de la información que facilita System Center Online para la información de títulos de software existente o definida por el usuario. Al cambiar o agregar información de categorización, la información del catálogo se considera definida por el usuario. La información de categorización definida por el usuario se almacena en tablas de base de datos distintas a las de la información del catálogo validada.  

###  <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorías de software  
 Las categorías de software de Asset Intelligence se usan para categorizar en líneas generales los títulos de software inventariado y también como agrupaciones de alto nivel de familias de software más específicas. Por ejemplo, una categoría de software podría ser empresas de energía, y una familia de software dentro de esa categoría de software podría ser petróleo y gas o hidroeléctrica. Existen muchas categorías de software predefinidas en el catálogo Asset Intelligence y se pueden crear categorías adicionales definidas por el usuario para concretar aún más el software inventariado. El estado de validación de todas las categorías de software predefinido es siempre **Validado**, mientras que el de la información de categorías de software personalizado que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**.  

 Use el procedimiento siguiente para crear una categoría de software definida por el usuario.  

##### <a name="to-create-a-user-defined-software-category"></a>Cómo crear una categoría de software definida por el usuario  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Catálogo**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear categoría de software**.  

4.  En la página **General** , escriba un nombre para la nueva categoría de software y, de forma opcional, una descripción.  

    > [!NOTE]  
    >  El estado de validación de todas las nuevas categorías de software personalizado siempre se establece como **Definido por el usuario**.  

     Haga clic en **Siguiente**.  

5.  En la página **Resumen** , revise la configuración y después haga clic en **Siguiente**.  

6.  En la página **Finalización** , haga clic en **Cerrar** para salir del asistente.  

###  <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Familias de software  
 Las familias de software de Asset Intelligence se usan para definir aún más los títulos de software inventariado dentro de las categorías de software. Por ejemplo, una categoría de software podría ser empresas de energía, y una familia de software dentro de esa categoría de software podría ser petróleo y gas o hidroeléctrica. Existen muchas familias de software predefinidas en el catálogo Asset Intelligence y se pueden crear familias adicionales definidas por el usuario para concretar el software inventariado. El estado de validación de todas las familias de software predefinido es siempre **Validado**, mientras que el de la información de familias de software personalizado que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**.  

 Use el procedimiento siguiente para crear una familia de software definida por el usuario.  

##### <a name="to-create-a-user-defined-software-family"></a>Cómo crear una familia de software definida por el usuario  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Catálogo**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear familia de software**.  

4.  En la página **General** , escriba un nombre para la nueva familia de software y, de forma opcional, una descripción.  

    > [!NOTE]  
    >  El estado de validación de todas las nuevas familias de software personalizado siempre se establece como **Definido por el usuario**.  

5.  En la página **Resumen** , revise la configuración y después haga clic en **Siguiente**.  

6.  En la página **Finalización** , haga clic en **Cerrar** para salir del asistente.  

###  <a name="software-labels"></a><a name="BKMK_SoftwareLabels"></a> Etiquetas de software  
 Las etiquetas de software personalizado de Asset Intelligence le permiten crear filtros que puede utilizar para agrupar los títulos de software y verlos mediante informes de Asset Intelligence. Por ejemplo, puede crear una etiqueta de software denominada shareware, asociarla a un número de aplicaciones y, después, ejecutar un informe que muestre todos los títulos con la etiqueta de software shareware. El estado de validación de todas las etiquetas de software personalizado que agregue al catálogo Asset Intelligence es **Definido por el usuario** .  

 Use el procedimiento siguiente para crear una etiqueta personalizada definida por el usuario.  

##### <a name="to-create-a-user-defined-software-label"></a>Cómo crear una etiqueta de software definida por el usuario  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Catálogo**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear etiqueta de software**.  

4.  En la página **General** , escriba un nombre para la nueva familia de software y, de forma opcional, una descripción.  

    > [!NOTE]  
    >  El estado de validación de todas las nuevas etiquetas de software personalizado siempre se establece como **Definido por el usuario**.  

5.  En la página **Resumen** , revise la configuración y después haga clic en **Siguiente**.  

6.  En la página **Finalización** , haga clic en **Cerrar** para salir del asistente.  

###  <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  
 La información de requisitos de hardware puede ayudarle a comprobar que los equipos cumplan los requisitos de hardware de los títulos de software antes de que se destinen a implementaciones de software. Muchos de los requisitos de hardware están predefinidos en el catálogo Asset Intelligence, y puede crear nueva información de requisitos de hardware definida por el usuario para cumplir requisitos personalizados. El estado de validación de todos los requisitos de hardware predefinidos siempre es **Validado**, mientras que el de la información de los requisitos de hardware que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**.  

> [!IMPORTANT]  
>  Los requisitos de hardware que se muestran en la consola de Configuration Manager se recuperan desde el catálogo Asset Intelligence en el equipo local y no se basan en información de títulos de software inventariado de clientes System Center 2012 Configuration Manager. La información de requisitos de hardware no se actualiza como parte del proceso de sincronización con System Center Online. Puede crear requisitos de hardware definidos por el usuario para software inventariado que no tenga requisitos de hardware asociados.  

 Use el procedimiento siguiente para crear un requisito de hardware definido por el usuario.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Cómo crear un requisito de hardware definido por el usuario  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Requisitos de hardware**.  

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear requisitos de hardware**.  

4. En la página **General** , escriba la siguiente información:  

   1. **Título de software**: especifica el título de software con el que están asociados los requisitos de hardware. El título de software no puede figurar ya en el catálogo Asset Intelligence.  

   2. **Estado de validación**: enumera el estado de validación como **Definido por el usuario** para los requisitos de hardware. Esta configuración no se puede modificar.  

   3. **CPU mínima (MHz)** : especifica la velocidad del procesador mínima, en megahercios (MHz), que requiere el título de software.  

   4. **RAM mínima (KB)** : especifica la memoria RAM mínima, en kilobytes (KB), que requiere el título de software.  

   5. **Espacio en disco mínimo (KB)** : especifica el espacio disponible en disco mínimo, en KB, que requiere el título de software.  

   6. **Tamaño del disco mínimo (KB)** : especifica el tamaño del disco duro mínimo, en KB, que requiere el título de software.  

      Haga clic en **Siguiente**.  

5. En la página **Resumen** , revise la configuración y después haga clic en **Siguiente**.  

6. En la página **Finalización** , haga clic en **Cerrar** para salir del asistente.  

###  <a name="modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a> Modificar la información de categorización del software inventariado  
 El software predefinido en el catálogo Asset Intelligence se configura con información de categorización determinada, como el nombre de producto, el proveedor, la categoría de software y la familia de software. Cuando la información de categorización predefinida no cumple sus requisitos, puede modificar la información en las propiedades del título de software. Cuando se modifica la información de categorización de software predefinido, el estado de validación del software cambia de **Validado** a **Definido por el usuario**.  

> [!IMPORTANT]  
>  La información de categorización solo puede modificarse en el sitio de nivel superior.  

 Use el procedimiento siguiente para modificar la información de categorización del software inventariado.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Cómo modificar las categorizaciones de los títulos de software  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Software inventariado**.  

3. Seleccione uno o varios títulos de software para los que quiera modificar las categorizaciones.  

4. En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5. En la pestaña **General** , puede modificar la información de categorización siguiente:  

   -   **Nombre de producto**: especifica el nombre del título de software inventariado.  

   -   **Proveedor**: especifica el nombre del proveedor que ha desarrollado el título de software inventariado.  

   -   **Categoría**: especifica la categoría de software que está asignada actualmente al título de software inventariado.  

   -   **Familia**: especifica la familia de software que está asignada actualmente al título de software inventariado.  

6. Haga clic en **Aceptar** para guardar los cambios.  

   Use el procedimiento siguiente para revertir el software a la información de categorización original.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Revertir la información de categorización a la configuración original del software  
 Configuration Manager almacena la información de categorización obtenida de System Center Online en la base de datos. La información no se puede eliminar. Después de modificar la información, puede revertir la información de categorización de nuevo a la categorización de System Center Online. El software inventariado que no está en el catálogo Asset Intelligence también se puede revertir a la configuración original.  

 Use el procedimiento siguiente para revertir la información de categorización a la configuración original.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Cómo revertir la información de categorización a la configuración original  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Software inventariado**.  

3.  Seleccione uno o varios títulos de software que quiera revertir a la configuración original. Solo se puede revertir el software que tenga un estado **Definido por el usuario** .  

    > [!TIP]  
    >  Haga clic en la columna **Estado** para ordenar por el estado de validación. La ordenación permite ver todo el software por estado de validación y seleccionar rápidamente varios elementos para revertir a la configuración original.  

4.  En la pestaña **Inicio** , en el grupo **Producto** , haga clic en **Revertir**.  

5.  Haga clic en **Sí** para revertir el software a la información de categorización original.  

6.  Cuando se revierte la información de categorización de software que se encuentre en el catálogo Asset Intelligence, el estado de validación cambia de **Definido por el usuario** a **Validado**. Cuando se revierte software que no está en el catálogo, el estado de validación cambia de **Definido por el usuario** a **Sin categoría**.  

##  <a name="request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a> Solicitar una actualización del catálogo para títulos de software sin categoría  
 Información de títulos de software sin categorizar puede enviarse a System Center Online de investigación y la categorización. Después de enviar un título de software sin categoría y cuando haya al menos 4 solicitudes de categorización de clientes para el mismo título de software, los investigadores identifican, categorizan y ponen la información de categorización del título a disposición de todos los clientes que usen el servicio System Center Online. Microsoft da máxima prioridad a los títulos de software que tengan la mayoría de solicitudes de categorización. El software personalizado y las aplicaciones de línea de negocio no suelen recibir una categoría y, como práctica recomendada, no se deberían enviar estos títulos de software a Microsoft para su categorización.  

 Cuando se envía información de títulos de software a System Center Online para su categorización, se aplican las condiciones siguientes:  

-   Solo se transmite la información básica del título de software a System Center Online y se puede revisar la información del título de software que se va a categorizar antes de su envío.  

-   Nunca se transmite la información de licencia del software.  

-   Cualquier título de software que se cargue estará disponible públicamente como parte del catálogo de System Center Online y otros clientes podrán descargarlo.  

-   El origen del título de software no se almacena en el catálogo de System Center Online. Sin embargo, los títulos de aplicaciones que contengan información confidencial o de propiedad no se deben enviar para su categorización en System Center Online.  

> [!NOTE]  
>  Para más información sobre la información de privacidad de Asset Intelligence, vea [Seguridad y privacidad de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Utilice el procedimiento siguiente para solicitar una categorización de un título de software del catálogo Asset Intelligence desde System Center Online.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Cómo solicitar una actualización del catálogo para títulos de software sin categoría  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Software inventariado**.  

3.  Seleccione uno o varios nombres de producto que se enviarán a System Center Online para su categorización. Solo se pueden enviar títulos de software inventariado sin categoría a System Center Online para su investigación y categorización. Si un administrador ha categorizado un título de software inventariado que ha resultado en un estado definido por el usuario, debe hacer clic con el botón derecho en el título de software inventariado y, después, hacer clic en **Revertir** para revertir el título de software al estado **Sin categoría** antes de poderlo enviar a System Center Online para su categorización.  

    > [!NOTE]  
    >  Configuration Manager puede procesar a la vez hasta 2000 títulos de software con el fin de clasificarlos. Si selecciona un número mayor, solo se procesarán los primeros 2000. El resto de títulos de software para clasificar se debe seleccionar en lotes de menos de 2000.  

    > [!TIP]  
    >  Haga clic en la columna **Estado** para ordenar por el estado de validación. Esto le permite ver todos los nombres de producto sin categorizar y seleccionar rápidamente varios elementos a fin de enviarlos para su categorización.  

4.  En la pestaña **Inicio** , en el grupo **Producto** , haga clic en **Solicitar actualización de catálogo**.  

5.  Revise el mensaje de privacidad de envío de categorización de System Center Online. Haga clic en **Detalles** para ver la información que se enviará a System Center Online.  

6.  Seleccione **He leído y comprendido este mensaje**y luego haga clic en **Aceptar** para permitir que los títulos de software seleccionados se envíen para su categorización.  

7.  Compruebe que el estado de los nombres de producto de software inventariados enviados a System Center Online para su categorización ha cambiado de **Sin categoría** a **Pendiente**.  

    > [!NOTE]  
    >  El software que se envía a System Center Online para su categorización y tiene un estado de validación **Pendiente** en un sitio de administración central se sigue mostrando con un estado de validación **Sin categoría** en los sitios primarios secundarios.  

##  <a name="resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a> Resolver conflictos de detalles de software  
 Tras la categorización de software recién actualizado detalles se han recibido de System Center Online que entran en conflicto con la información de detalles de software existente, puede elegir cómo resolver el conflicto. El software que tiene un conflicto actual tiene un estado de validación de **Actualizable**. Después de resolver un conflicto de detalles de software, se conserva la información de categorización de software en el catálogo Asset Intelligence según la configuración que especifique. Un conflicto de detalles de software no se producirá de nuevo con el mismo valor de categorización de software, a menos que el valor de System Center Online cambie después de que se haya resuelto el conflicto.  

 Utilice el procedimiento siguiente para resolver un conflicto de detalles de software.  

#### <a name="to-resolve-a-software-details-conflict"></a>Cómo resolver conflictos de detalles de software  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Asset Intelligence**y luego en **Software inventariado**.  

3. Revise la columna **Estado** en busca de títulos de software con el estado **Actualizable** .  

4. Seleccione el título de software para el que tiene que resolver un conflicto y después, en la pestaña **Inicio** , en el grupo **Producto** , haga clic en **Resolver conflicto**.  

5. Revisa la información siguiente:  

   -   **Valor local**: especifica la información de categorización de software existente en el catálogo Asset Intelligence que está en conflicto con los detalles más recientes de categorización de software de System Center Online.  

   -   **Valor descargado**: especifica la nueva información de categorización de software de System Center Online para la información de categorización de software del catálogo Asset Intelligence que está en conflicto.  

6. Seleccione una de las siguientes opciones para resolver el conflicto de detalles de software:  

   - **No cambiar el valor de la información de catálogo editado localmente**: resuelve el conflicto de detalles de software manteniendo la información de categorización de software del catálogo Asset Intelligence existente. Cuando se selecciona esta opción, el estado del título de software cambia de **Actualizable** a **Definido por el usuario**.  

   - **Sobrescribir el valor de la información de catálogo editado localmente con el valor descargado de System Center Online**: resuelve el conflicto de detalles de software sobrescribiendo la información de categorización de software del catálogo Asset Intelligence existente con la nueva información obtenida desde System Center Online. Cuando se selecciona esta opción, el estado del título de software cambia de **Actualizable** a **Validado**.  

     Haga clic en **Aceptar** para guardar la resolución de conflictos.  
