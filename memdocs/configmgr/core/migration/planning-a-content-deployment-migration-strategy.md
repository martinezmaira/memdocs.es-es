---
title: Migración de contenido
titleSuffix: Configuration Manager
description: Use puntos de distribución para administrar contenido mientras migra datos a una jerarquía de destino de la rama actual de Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: afb39af5087daaca3b2bb6eb15f33d81d959beec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702873"
---
# <a name="plan-a-content-deployment-migration-strategy-in-configuration-manager"></a>Planear una estrategia de migración de implementación de contenido en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Mientras migra datos activamente a una jerarquía de destino de la rama actual de Configuration Manager, los clientes de Configuration Manager en ambas jerarquías, la de origen y la de destino, pueden mantener el acceso al contenido que implemente en la jerarquía de origen. También puede usar la migración para actualizar o reasignar los puntos de distribución de la jerarquía de origen para que se conviertan en puntos de distribución en la jerarquía de destino. Cuando comparte y actualiza o reasigna puntos de distribución, esta estrategia puede ayudarle a evitar tener que volver a implementar contenido en los servidores nuevos de la jerarquía de destino para los clientes que migre.  

Aunque se puede volver a crear y distribuir contenido en la jerarquía de destino, también se pueden utilizar las siguientes opciones para administrar este contenido:  

-   Comparta los puntos de distribución de la jerarquía de origen con los clientes de la jerarquía de destino.  

-   Actualice puntos de distribución de Configuration Manager 2007 independientes o sitios secundarios de Configuration Manager 2007 en la jerarquía de origen para que sean puntos de distribución en la jerarquía de destino.  

-   Reasigne puntos de distribución de una jerarquía de origen de Configuration Manager a un sitio en la jerarquía de destino.  

##  <a name="share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Compartir puntos de distribución entre jerarquías de origen y de destino  
Durante la migración, puede compartir los puntos de distribución de una jerarquía de origen con la jerarquía de destino. Puede usar puntos de distribución compartidos para que el contenido que migró de una jerarquía de origen esté disponible inmediatamente para los clientes en la jerarquía de destino sin tener que recrear el contenido y, a continuación, distribuirlo en los nuevos puntos de distribución de la jerarquía de destino. Cuando los clientes de la jerarquía de destino solicitan contenido implementado en puntos de distribución compartidos, los puntos de distribución compartidos pueden ofrecerse a los clientes como ubicaciones de contenido válidas.  

 Además de ser una ubicación de contenido válida para clientes en la jerarquía de destino mientras la migración desde la jerarquía de origen está activa, es posible actualizar o reasignar un punto de distribución a la jerarquía de destino. Puede actualizar puntos de distribución compartidos de Configuration Manager 2007 y reasignar los puntos de distribución compartidos de System Center 2012 Configuration Manager. Al actualizar o volver a asignar un punto de distribución compartido, este se quita de la jerarquía de origen y se convierte en un punto de distribución en la jerarquía de destino. Después de actualizar o volver a asignar un punto de distribución compartido, puede seguir usando el punto de distribución en la jerarquía de destino una vez finalizada la migración desde la jerarquía de origen. Para más información sobre cómo actualizar un punto de distribución compartido, vea [Planear actualizar los puntos de distribución compartidos de Configuration Manager 2007](#Planning_to_Upgrade_DPs). Para más información sobre cómo reasignar un punto de distribución compartido, vea [Planear la reasignación de puntos de distribución de Configuration Manager](#BKMK_ReassignDistPoint).  

 Puede elegir compartir puntos de distribución desde cualquier sitio de origen en la jerarquía de origen. Cuando comparte puntos de distribución para un sitio de origen, los sitios secundarios se comparten en todos los puntos de distribución certificados en ese sitio primario y en cada uno de los sitios secundarios. Para ser un punto de distribución compartido, el servidor de sistema de sitio que hospeda el punto de distribución debe configurarse con un nombre de dominio completo (FQDN). No se tienen en cuenta los puntos de distribución configurados con un nombre NetBIOS.  

> [!TIP]  
>  Configuration Manager 2007 no requiere que se configure un FQDN para servidores de sistema de sitio.  

Utilice la siguiente información para ayudarle a planear puntos de distribución compartidos:  

-   Los puntos de distribución que comparte deben cumplir los requisitos previos para los puntos de distribución compartidos. Para más información sobre estos requisitos previos, vea la sección [Configuraciones necesarias para la migración](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) en [Requisitos previos para la migración](../../core/migration/prerequisites-for-migration.md).  

-   La acción del punto de distribución compartido es una configuración de todo el sitio que comparte todos los puntos de distribución certificados en un sitio de origen y en cualquier sitio secundario directo. No puede seleccionar puntos de distribución individuales para compartir cuando se habilita el uso compartido de puntos de distribución.  

-   Los clientes de la jerarquía de destino pueden recibir información de ubicación de contenido para los paquetes que se distribuyen en los puntos de distribución que se comparten desde la jerarquía de origen. Para los puntos de distribución de una jerarquía de origen de Configuration Manager 2007, esto incluye puntos de distribución de sucursal, puntos de distribución en recursos compartidos del servidor y puntos de distribución estándar.  

    > [!WARNING]  
    >  Si cambia la jerarquía de origen, los puntos de distribución compartidos de la jerarquía de origen original ya no estarán disponibles y no se podrán ofrecer como ubicaciones de contenido a los clientes de la jerarquía de destino. Si vuelve a configurar la migración para que use la jerarquía de origen original, se restaurarán los puntos de distribución compartidos previamente como servidores de ubicación de contenido válidos.  

-   Cuando migre un paquete hospedado en un punto de distribución compartido, la versión del paquete debe seguir siendo la misma en las jerarquías de origen y de destino. Cuando la versión de un paquete no sea la misma en la jerarquía de origen y de destino, los clientes de la jerarquía de destino no podrán recuperar el contenido del punto de distribución compartido. Por lo tanto, si actualiza un paquete en la jerarquía de destino, debe volver a migrar los datos del paquete antes de que los clientes de la jerarquía de destino puedan recuperar ese contenido de un punto de distribución compartido.  

    > [!NOTE]  
    >  Cuando vea detalles de un paquete hospedado en un punto de distribución compartido, el número de paquetes que se muestran como **Paquetes migrados hospedados** en la pestaña **Puntos de distribución compartidos** del sitio de origen no se actualiza hasta que finalice el siguiente ciclo de recopilación de datos.  

-   Puede ver puntos de distribución compartidos y sus propiedades en el nodo **Jerarquía de orígenes** del área de trabajo **Administración** en la consola de Configuration Manager que se conecte a la jerarquía de destino.  

-   No puede utilizar un punto de distribución compartido de una jerarquía de origen de Configuration Manager 2007 para hospedar paquetes de Microsoft Application Virtualization (App-V). Los paquetes de App-V deben migrar y convertirse para que los usen los clientes en la jerarquía de destino. Pero puede usar un punto de distribución compartido de una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager para hospedar los paquetes de App-V para los clientes en una jerarquía de destino.  

-   Cuando comparta un punto de distribución protegido desde una jerarquía de origen de Configuration Manager 2007, la jerarquía de destino creará un grupo de límites que incluirá las ubicaciones de red protegidas de ese punto de distribución. No puede cambiar este grupo de límites en la jerarquía de destino. Pero puede cambiar la información de los límites protegidos para el punto de distribución en la jerarquía de origen de Configuration Manager 2007. Ese cambio se verá reflejado en la jerarquía de destino cuando finalice el siguiente ciclo de recopilación de datos.  

    > [!NOTE]  
    >  System Center 2012 Configuration Manager y la rama actual de Configuration Manager usan el concepto de puntos de distribución preferidos en lugar de puntos de distribución protegidos. Esta condición solo se aplica a los puntos de distribución compartidos desde sitios de origen de Configuration Manager 2007.  

Los puntos de distribución elegibles no están visibles en la consola de Configuration Manager antes de compartir puntos de distribución desde un sitio de origen. Después de compartir los puntos de distribución, solo se enumerarán los puntos de distribución que se compartan correctamente.  

Después de compartir los puntos de distribución, puede cambiar la configuración de cualquier punto de distribución compartido en la jerarquía de origen. Los cambios realizados en la configuración de un punto de distribución se reflejan en la jerarquía de destino después del siguiente ciclo de recopilación de datos. Los puntos de distribución actualizados para ser susceptibles de compartirse se comparten automáticamente, mientras que los que ya no son susceptibles dejan de compartirse. Por ejemplo, es posible que tenga un punto de distribución que no esté configurado con un FQDN de intranet y que no se compartiera inicialmente con la jerarquía de destino. Después de configurar el FQDN de ese punto de distribución, el siguiente ciclo de recopilación de datos identifica esta configuración y, después, el punto de distribución se comparte con la jerarquía de destino.  

##  <a name="plan-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a> Planear actualizar los puntos de distribución compartidos de Configuration Manager 2007  
Cuando realiza la migración de una jerarquía de origen de Configuration Manager 2007, puede actualizar un punto de distribución compartido para que sea un punto de distribución de la rama actual de Configuration Manager. Puede actualizar los puntos de distribución en sitios primarios y sitios secundarios. El proceso de actualización quita el punto de distribución de la jerarquía de Configuration Manager 2007 y lo convierte en un servidor de sistema de sitio en la jerarquía de destino. Este proceso también copia el contenido existente que se encuentra en el punto de distribución en una nueva ubicación del equipo del punto de distribución. A continuación, el proceso de actualización modifica la copia del contenido para crear el almacén de instancia única para usar con la implementación de contenido en la jerarquía de destino. Por lo tanto, cuando actualice un punto de distribución, no tendrá que redistribuir el contenido migrado hospedado en el punto de distribución de Configuration Manager 2007.  

Después de que Configuration Manager convierta el contenido en un almacén de instancia única, Configuration Manager elimina el contenido de origen original en el equipo del punto de distribución para liberar espacio en disco. Configuration Manager no usa la ubicación original del contenido de origen.  

No todos los puntos de distribución de Configuration Manager 2007 que puede compartir son aptos para su actualización a la rama actual de Configuration Manager. Para poder actualizarse, un punto de distribución de Configuration Manager 2007 debe cumplir una serie de condiciones. Estas condiciones incluyen el servidor de sistema de sitio en el que se instala el punto de distribución y el tipo de punto de distribución de Configuration Manager 2007 que se instala. Por ejemplo, no puede actualizar ningún tipo de punto de distribución instalado en el equipo del servidor de sitio en un sitio primario, pero puede actualizar un punto de distribución estándar instalado en el equipo del servidor de sitio en un sitio secundario.  

> [!NOTE]  
>  Solo puede actualizar aquellos puntos de distribución compartidos de Configuration Manager 2007 que estén en un equipo que ejecute una versión de sistema operativo compatible con los puntos de distribución en la jerarquía de destino. Por ejemplo, aunque pueda compartir un punto de distribución de Configuration Manager 2007 en un equipo que ejecute Windows Vista, este punto de distribución compartido no se puede actualizar porque la rama actual de Configuration Manager no admite el uso de ese sistema operativo como punto de distribución.  

La tabla siguiente enumera las ubicaciones compatibles de cada tipo de punto de distribución de Configuration Manager 2007 que puede actualizar.  

|Tipo de punto de distribución|Punto de distribución en un equipo de sistema de sitio que no sea el servidor de sitio|Punto de distribución en un equipo de sistema de sitio que no sea el servidor de sitio y que hospede otros roles de sistema de sitio|Punto de distribución en un servidor de sitio secundario|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Punto de distribución estándar|Sí|No|Sí|  
|Punto de distribución en recursos compartidos del servidor<sup>1</sup>|Sí|No|No|  
|Punto de distribución de sucursal|Sí|No|No|  

 <sup>1</sup> La rama actual de Configuration Manager no admite recursos compartidos de servidor para sistemas de sitio, pero admite la actualización de un punto de distribución de Configuration Manager 2007 que se encuentre en un recurso compartido de servidor. Cuando actualice un punto de distribución de Configuration Manager 2007 que no esté en un recurso compartido de servidor, el tipo de punto de distribución se convertirá automáticamente en un servidor y deberá seleccionar la unidad del equipo del punto de distribución que contendrá el almacén de contenido de instancia única.  

> [!WARNING]  
>  Antes de actualizar un punto de distribución de sucursal, desinstale el software de cliente de Configuration Manager 2007. Cuando actualice un punto de distribución de sucursal que tenga instalado el software de cliente de Configuration Manager 2007, se quitará el contenido previamente implementado en el equipo y se producirá un error en la actualización del punto de distribución.  

Para identificar puntos de distribución aptos para su actualización en la consola de Configuration Manager en el nodo **Jerarquía de orígenes**, seleccione un sitio de origen y, después, seleccione la pestaña **Puntos de distribución compartidos**. Los puntos de distribución elegibles muestran **Sí** en la columna **Apto para actualización** .  

Cuando se actualiza un punto de distribución instalado en un servidor de sitio secundario de Configuration Manager 2007, el sitio secundario se desinstala de la jerarquía de origen. Aunque este escenario se denomine una actualización de sitio secundario, solo se aplica al rol de sistema de sitio del punto de distribución. El resultado es que el sitio secundario no se actualiza, sino que se desinstala. Esto deja un punto de distribución de la jerarquía de destino en el equipo en el que estaba el servidor del sitio secundario. Si planea actualizar el punto de distribución en un sitio secundario, vea [Planear la actualización de sitios secundarios de Configuration Manager 2007](#BKMK_UpgradeSS) en este tema.  

###  <a name="distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Proceso de actualización de puntos de distribución  
Puede usar la consola de Configuration Manager para actualizar puntos de distribución de Configuration Manager 2007 que ha compartido con la jerarquía de destino. Al actualizar un punto de distribución compartido, el punto de distribución se desinstala del sitio de Configuration Manager 2007. Después, se instala como un punto de distribución que se adjunta a un sitio primario o secundario que especifique en la jerarquía de destino. El proceso de actualización crea una copia del contenido migrado que se almacena en el punto de distribución y, a continuación, convierte esta copia en el almacén de contenido de instancia única. Cuando Configuration Manager convierte un paquete en el almacén de contenido de instancia única, elimina ese paquete del recurso compartido SMSPKG en el equipo del punto de distribución a menos que el paquete tenga uno o más anuncios establecidos en **Ejecutar programa desde el punto de distribución**.  

Para actualizar el punto de distribución, Configuration Manager usa la **Cuenta de acceso del sitio de origen** configurada para recopilar datos del proveedor de SMS del sitio de origen. Aunque esta cuenta requiere solo el permiso **Leer** para que los objetos de sitio recopilen datos del sitio de origen, también debe tener el permiso **Eliminar** y **Modificar** en la clase **Sitio** para quitar correctamente el punto de distribución del sitio de Configuration Manager 2007 durante la actualización.  

> [!NOTE]  
>  Configuration Manager puede convertir el contenido en el almacén de instancia única de un solo punto de distribución a la vez. Cuando configura varias actualizaciones de puntos de distribución, los puntos de distribución se ponen en cola para la actualización y se procesan de uno en uno.  

Antes de actualizar un punto de distribución compartido, asegúrese de que se migra todo el contenido implementado en el punto de distribución. El contenido que no se migra antes de actualizar el punto de distribución no está disponible en la jerarquía de destino después de la actualización. Al actualizar un punto de distribución, el contenido de los paquetes migrados se convierte en un formato compatible con el almacenamiento de instancia única de la jerarquía de destino.  

Para actualizar un punto de distribución desde la consola de Configuration Manager, el servidor de sistema de sitio de Configuration Manager 2007 debe cumplir las condiciones siguientes:  

-   La configuración y la ubicación del punto de distribución deben poder actualizarse.  

-   El equipo del punto de distribución debe tener espacio en disco suficiente para que el contenido se convierta del formato de almacenamiento de contenido de Configuration Manager 2007 al formato de almacén de instancia única. Esta conversión requiere un espacio disponible en disco igual al tamaño del paquete más grande almacenado en el punto de distribución.  

-   El equipo del punto de distribución debe ejecutar una versión de sistema operativo que se admita como punto de distribución en la jerarquía de destino.  

    > [!NOTE]  
    >  Cuando Configuration Manager comprueba la idoneidad de un punto de distribución para su actualización, no valida la versión del sistema operativo del equipo del punto de distribución.  

Para actualizar un punto de distribución, en el área de trabajo **Administración**, expanda **Migración**, expanda el nodo **Jerarquía de orígenes** y después seleccione el sitio que contiene el punto de distribución que quiere actualizar. A continuación, en el panel de detalles, en la pestaña **Puntos de distribución compartidos** , seleccione el punto de distribución que desea actualizar.  

Puede confirmar que el punto de distribución está listo para su actualización viendo el estado en la columna **Apto para reasignación** .  Luego, en la cinta de la consola de Configuration Manager, en la pestaña **Puntos de distribución**, en el grupo **Punto de distribución**, seleccione **Reasignar**. Se abrirá a un asistente que se puede usar para completar la actualización del punto de distribución.  

Cuando actualice un punto de distribución compartido, debe asignar el punto de distribución a un sitio primario o secundario de su elección en la jerarquía de destino. Una vez actualizado el punto de distribución, el punto de distribución se administra como un punto de distribución de la jerarquía de destino, como cualquier otro punto de distribución.  

Para supervisar el progreso de la actualización de un punto de distribución en la consola de Configuration Manager, seleccione el nodo **Migración de punto de distribución** en el nodo **Migración** del área de trabajo **Administración**. También puede ver la información en el **Migmctrl.log** del servidor de sitio de administración central de la jerarquía de destino, o en el **distmgr.log** del servidor de sitio de la jerarquía de destino que administra el punto de distribución actualizado.  

> [!NOTE]  
>  Al actualizar un punto de distribución en la jerarquía de destino, se quita el rol de sistema de sitio del punto de distribución del sitio de origen de Configuration Manager 2007. Sin embargo, los paquetes que se enviaron al punto de distribución no se actualizan en la jerarquía de Configuration Manager 2007. En la consola de Configuration Manager 2007, los paquetes que se habían enviado al punto de distribución continúan apareciendo en el equipo del sistema de sitio como un punto de distribución del **Tipo** **Desconocido**. Las actualizaciones posteriores del paquete en Configuration Manager 2007 provocan errores en los informes del administrador de distribución en el registro distmgr.log del sitio al intentar actualizar el paquete en el sistema de sitio desconocido.  

Si decide no actualizar un punto de distribución compartido, aún puede instalar un punto de distribución de la jerarquía de destino en un punto de distribución anterior de Configuration Manager 2007. Antes de instalar el punto de distribución, debe desinstalar primero todos los roles de sistema de sitio de Configuration Manager 2007 del equipo del punto de distribución. Esto incluye el sitio de Configuration Manager 2007 en caso de que sea el equipo del servidor de sitio. Cuando se desinstala un punto de distribución de Configuration Manager 2007, no se elimina del equipo el contenido que se implementó en el punto de distribución.  

###  <a name="plan-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a> Planear la actualización de sitios secundarios de Configuration Manager 2007  
 Cuando usa la migración para actualizar un punto de distribución compartido hospedado en un servidor de sitio secundario de Configuration Manager 2007, Configuration Manager actualiza el rol de sistema de sitio del punto de distribución para que sea un punto de distribución en la jerarquía de destino. También desinstala el sitio secundario de la jerarquía de origen. El resultado es un punto de distribución de la rama actual de Configuration Manager, pero no un sitio secundario.  

 Para que un punto de distribución del equipo del servidor de sitio pueda actualizarse, Configuration Manager debe ser capaz de desinstalar el sitio secundario y cada uno de los roles de sistema de sitio de ese equipo. Por lo general, un punto de distribución compartido de un recurso compartido de servidor de Configuration Manager 2007 es apto para la actualización. Sin embargo, cuando existe un recurso compartido de servidor en el servidor de sitio secundario, el sitio secundario y los puntos de distribución compartidos de ese equipo no son aptos para la actualización. El motivo de esto es que el recurso compartido del servidor se trata como un objeto de sistema de sitio adicional cuando el proceso intenta desinstalar el sitio secundario, y este proceso no puede desinstalar este objeto. En este escenario, puede habilitar un punto de distribución estándar en el servidor de sitio secundario y, a continuación, redistribuir el contenido a ese punto de distribución estándar. Este proceso no usa ancho de banda de red y, una vez completado, es posible desinstalar el punto de distribución del recurso compartido del servidor, quitar el recurso compartido del servidor y, después, actualizar el punto de distribución y el sitio secundario.  

 Antes de actualizar un punto de distribución compartido, revise la configuración del punto de distribución en Configuration Manager 2007 para evitar la actualización de un punto de distribución en un sitio secundario que aún quiere usar con Configuration Manager 2007. Esto es recomendable porque una vez actualizado un punto de distribución compartido en un servidor de sitio secundario, el servidor de sistema de sitio se quita de la jerarquía de Configuration Manager 2007 y deja de estar disponible para su uso con esa jerarquía. Cuando se quita el sitio secundario, el resto de puntos de distribución en el sitio secundario son huérfanos. Esto significa que se convierten en no administrados por Configuration Manager 2007 y ya no son compartidos ni aptos para su actualización.  

> [!WARNING]  
>  Cuando ve puntos de distribución compartidos en la consola de Configuration Manager, no hay ninguna indicación visible de que un punto de distribución compartido esté en un servidor de sistema de sitio remoto o en el servidor de sitio secundario.  

 Cuando tenga un sitio secundario en una ubicación de red remota que se usa principalmente para controlar la implementación de contenido en esa ubicación remota, es aconsejable actualizar los sitios secundarios que tengan un punto de distribución compartido. Como puede configurar el control de ancho de banda de red al distribuir contenido en un punto de distribución de la rama actual de Configuration Manager, a menudo es posible actualizar un sitio secundario a un punto de distribución, configurar el punto de distribución para el control de ancho de banda de red y evitar instalar un sitio secundario en esa ubicación de red en la jerarquía de destino.  

 El proceso para actualizar un punto de distribución compartido en un servidor de sitio secundario es el mismo que cualquier otra actualización de punto de distribución compartido. El contenido se copia y se convierte en el almacén de instancia única que usa la jerarquía de destino. Pero cuando actualiza un punto de distribución compartido que está en un servidor de sitio secundario, el proceso de actualización también desinstala el punto de administración, si está presente y, después, desinstala el sitio secundario del servidor. El resultado es que el sitio secundario se quita de la jerarquía de Configuration Manager 2007. Para desinstalar el sitio secundario, Configuration Manager usa la cuenta que está configurada para recopilar datos del sitio de origen.  

 Durante la actualización, se produce un retraso entre el momento en que se desinstala el sitio secundario de Configuration Manager 2007 y el momento en que comienza la instalación del punto de distribución en la jerarquía de destino. El ciclo de recopilación de datos determina este retraso de hasta cuatro horas. El retraso pretende proporcionar tiempo para que se desinstale el sitio secundario antes de que comience la instalación del nuevo punto de distribución.  

 Para más información sobre cómo actualizar un punto de distribución compartido, vea [Planear actualizar los puntos de distribución compartidos de Configuration Manager 2007](#Planning_to_Upgrade_DPs).  

##  <a name="plan-to-reassign-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a> Planear la reasignación de puntos de distribución de Configuration Manager  
 Al migrar desde una versión compatible de System Center 2012 Configuration Manager a una jerarquía de la misma versión, es posible reasignar un punto de distribución compartido desde la jerarquía de origen a un sitio en la jerarquía de destino. Esto es similar al concepto de actualización de un punto de distribución de Configuration Manager 2007 a un punto de distribución en la jerarquía de destino. Puede reasignar los puntos de distribución desde sitios primarios y sitios secundarios. Esta acción de reasignar un punto de distribución lo quita de la jerarquía de origen y hace que el equipo, y su punto de distribución, se conviertan en un servidor de sistema de sitio seleccionado en la jerarquía de destino.  

 Cuando reasigne un punto de distribución, no tendrá que redistribuir el contenido migrado hospedado en el punto de distribución del sitio de origen. Además, al contrario de lo que ocurre en la actualización de un punto de distribución de Configuration Manager 2007, la reasignación de un punto de distribución no requiere espacio adicional en disco en el equipo del punto de distribución. Esto se debe a que desde System Center 2012 Configuration Manager, los puntos de distribución usan el formato de almacén de instancia única para el contenido. El contenido en el equipo de punto de distribución no necesita convertirse cuando el punto de distribución se reasigna entre jerarquías.  

 Para que un punto de distribución de System Center 2012 Configuration Manager sea apto para la reasignación, debe cumplir los siguientes criterios:  

-   Un punto de distribución compartido debe instalarse en un equipo que no sea el servidor del sitio.  

-   Un punto de distribución compartido no puede compartir ubicación con otros roles de sistema de sitio adicionales.  

Para identificar puntos de distribución aptos para su reasignación en la consola de Configuration Manager en el nodo **Jerarquía de orígenes**, seleccione un sitio de origen y, después, seleccione la pestaña **Puntos de distribución compartidos**. Los puntos de distribución aptos muestran **Sí** en la columna **Apto para reasignación** (esta columna se llamaba **Apto para actualización** antes de System Center 2012 R2 Configuration Manager).  

###  <a name="distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Proceso de reasignación de puntos de distribución  
 Puede usar la consola de Configuration Manager para reasignar puntos de distribución que ha compartido de una jerarquía de origen activa. Al reasignar un punto de distribución compartido, el punto de distribución se desinstala de su sitio de origen y, después, se instala como un punto de distribución que se adjunta a un sitio primario o secundario que se especifica en la jerarquía de destino.  

 Para reasignar el punto de distribución, la jerarquía de destino usa la cuenta de acceso del sitio de origen que está configurada para recopilar datos del proveedor de SMS del sitio de origen. Para más información sobre los permisos necesarios y requisitos previos adicionales, vea [Requisitos previos para la migración](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar varios puntos de distribución compartidos al mismo tiempo
A partir de la versión 1610, puede usar **Reasignar punto de distribución** para que Configuration Manager procese en paralelo la reasignación de un máximo de 50 puntos de distribución compartidos al mismo tiempo. Esto incluye los puntos de distribución compartidos de sitios de origen compatibles que ejecutan:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- Administrador de configuración de System Center 2012 R2
- Configuration Manager (rama actual)

Cuando se reasignan puntos de distribución, todos ellos deben poder actualizarse o reasignarse. El nombre de la acción y el proceso implicados, (ya sea actualización o reasignación), depende de la versión de Configuration Manager que ejecute el sitio de origen. Los resultados para las dos acciones son los mismos: el punto de distribución se asigna a uno de los sitios de Rama actual con su contenido local.

Antes de la versión 1610, Configuration Manager solo podía procesar un punto de distribución de cada vez. Ahora puede reasignar tantos puntos de distribución como quiera, pero tenga en cuenta las observaciones siguientes:  
- Aunque no es posible seleccionar varios puntos de distribución para su reasignación, cuando se ha puesto en cola más de uno, Configuration Manager los procesará en paralelo en lugar de esperar a que se termine uno para iniciar el siguiente.  
- De forma predeterminada, se procesa en paralelo un máximo de 50 puntos de distribución a la vez. Una vez terminada la reasignación del primer punto de distribución, Configuration Manager empieza a procesar el número 51, y así sucesivamente.  
- Cuando se usa el SDK de Configuration Manager, es posible cambiar la propiedad **SharedDPImportThreadLimit** para ajustar el número de puntos de distribución reasignados que Configuration Manager puede procesar en paralelo.


##  <a name="assign-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a> Asignar la propiedad del contenido durante la migración de contenido  
 Cuando migra contenido para las implementaciones, debe asignar el objeto de contenido a un sitio en la jerarquía de destino. Este sitio, a continuación, se convierte en el propietario de ese contenido en la jerarquía de destino. Aunque el sitio de nivel superior de la jerarquía de destino es el sitio que migra los metadatos del contenido, es el sitio asignado el que usa los archivos de origen originales del contenido en la red.  

 Para minimizar el ancho de banda de red usado al migrar contenido, considere la posibilidad de transferir la propiedad del contenido de un sitio en la jerarquía de destino cercano en la red a la ubicación del contenido en la jerarquía de origen. Dado que la información sobre el contenido en la jerarquía de destino se comparte de forma global, estará disponible en cada sitio.  

 Aunque la información sobre el contenido se comparte en todos los sitios mediante la replicación de base de datos, cualquier contenido que asigne a un sitio primario y que luego implemente en puntos de distribución en otros sitios primarios se transfiere mediante la replicación basada en archivos. Esta transferencia se dirige al sitio de administración central y, a continuación, al sitio primario adicional. Puede reducir las transferencias de datos en redes de ancho de banda bajo si centraliza paquetes que planee distribuir en varios sitios primarios antes o durante la migración cuando asigne un sitio como propietario de contenido.
