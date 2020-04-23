---
title: Administrar controladores
titleSuffix: Configuration Manager
description: Use el catálogo de controladores de Configuration Manager para importar controladores de dispositivos, controladores de grupo en paquetes y distribuir esos paquetes a puntos de distribución.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708903"
---
# <a name="manage-drivers-in-configuration-manager"></a>Administración de controladores en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager proporciona un catálogo de controladores que puede usar para administrar los controladores de dispositivos Windows en su entorno de Configuration Manager. Use el catálogo de controladores para importar controladores de dispositivos en Configuration Manager, agruparlos en paquetes y distribuir esos paquetes a puntos de distribución. Los controladores de dispositivos se pueden usar cuando se instala un sistema operativo completo en el equipo de destino y cuando se usa Windows PE en una imagen de arranque. Los controladores de dispositivos de Windows están compuestos por un archivo de información de instalación (INF) y los archivos adicionales necesarios para admitir el dispositivo. Cuando se implementa un sistema operativo, Configuration Manager obtiene la información de hardware y plataforma para el dispositivo mediante el archivo INF. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a> Categorías de controladores

Cuando importa controladores de dispositivos, puede asignarlos a una categoría. Las categorías de controladores de dispositivos permiten agrupar controladores de dispositivos de uso similar en el catálogo de controladores. Por ejemplo, configure todos los controladores de dispositivos adaptadores de red en una determinada categoría. A continuación, cuando se crea una secuencia de tareas que incluye el paso [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers), especifique una categoría específica de controladores de dispositivos. Configuration Manager examina el hardware y selecciona los controladores aplicables de dicha categoría en la fase del sistema que va a usar el programa de instalación de Windows.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> Paquetes de controladores

Agrupe controladores de dispositivos similares en paquetes para facilitar las implementaciones de sistema operativo. Por ejemplo, cree un paquete de controladores para cada fabricante de equipos de la red. Puede crear un paquete de controladores al importar controladores en el catálogo de controladores directamente en el nodo **Paquetes de controladores**. Después de crear un paquete de controladores, distribúyalo a puntos de distribución. Luego, los equipos cliente de Configuration Manager pueden instalar los controladores según se requiera. 

Tenga en cuenta lo siguiente:  

- Cuando crea un paquete de controladores, la ubicación de origen del paquete debe apuntar a un recurso compartido de red vacío que ningún otro paquete de controladores esté utilizando. El proveedor de SMS debe tener permisos de **control total** en esa ubicación.  

- Al agregar controladores de dispositivos a un paquete de controladores, Configuration Manager lo copia en la ubicación de origen del paquete. Puede agregar a un paquete de controladores solo los controladores de dispositivos que haya importado y habilitado en el catálogo de controladores.  

- Puede copiar un subconjunto de controladores de dispositivos de un paquete de controladores existente. En primer lugar, cree un nuevo paquete de controladores. A continuación, agregue el subconjunto de controladores de dispositivo al nuevo paquete y, a continuación, distribuya el nuevo paquete a un punto de distribución.  

- Cuando use secuencias de tareas para instalar controladores, cree paquetes de controladores que contengan menos de 500 controladores de dispositivos.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a> Crear un paquete de controladores  

> [!IMPORTANT]  
> Para crear un paquete de controladores, debe tener una carpeta de red vacía que no use otro paquete de controladores. En la mayoría de los casos, cree una nueva carpeta antes de iniciar este procedimiento.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Sistemas operativos** y, a continuación, seleccione el nodo **Paquetes de controladores**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear paquete de controladores**.  

3. Especifique un **Nombre** descriptivo para el paquete de controladores.  

4. Escriba un **Comentario** opcional para el paquete de controladores. Use esta descripción para proporcionar información sobre el contenido o el propósito del paquete de controladores.  

5. En el cuadro **Ruta de acceso** , especifique una carpeta de origen vacía para el paquete de controladores. Cada paquete de controladores debe utilizar una carpeta única. Esta ruta de acceso se requiere como una ubicación de red.  

   > [!IMPORTANT]  
   > La cuenta de servidor de sitio debe tener permisos de **Control total** en la carpeta de origen especificada.  

El nuevo paquete de controladores no contiene ningún controlador. El siguiente paso agrega controladores al paquete.  

Si el nodo **Paquetes de controladores** contiene varios paquetes, puede agregar carpetas al nodo para separar los paquetes en grupos lógicos.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Acciones adicionales para paquetes de controladores  

Se pueden realizar otras acciones para administrar paquetes de controladores cuando se seleccione uno o varios paquetes de controladores del nodo **Paquetes de controladores**. 


#### <a name="create-prestage-content-file"></a>Crear archivo de contenido preconfigurado
Crea archivos que se pueden utilizar para importar manualmente contenido y sus metadatos asociados. Utilice el contenido preconfigurado si dispone de poco ancho de banda de red entre el servidor de sitio y los puntos de distribución donde se almacena el paquete de controladores.

#### <a name="delete"></a>Eliminar
Quita el paquete de controladores del nodo **Paquetes de controladores**.

#### <a name="distribute-content"></a>Distribuir contenido
Distribuye el paquete de controladores a puntos de distribución, grupos de puntos de distribución y grupos de puntos de distribución asociados a recopilaciones.

#### <a name="manage-access-accounts"></a>Administrar cuentas de acceso
Agrega, modifica o elimina cuentas de acceso para el paquete de controladores.

Para obtener más información sobre las cuentas de acceso de paquete, consulte [Referencia técnica para las cuentas que se usan en Configuration Manager](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Mover
Mueve el paquete de controladores a otra carpeta en el nodo **Paquetes de controladores**.

#### <a name="update-distribution-points"></a>Actualizar puntos de distribución
Actualiza el paquete de controladores de dispositivo en todos los puntos de distribución en los que se almacena el paquete. Esta acción copia solo el contenido que ha cambiado desde la última vez que se distribuyó.

#### <a name="properties"></a>Propiedades
Se abrirá el cuadro de diálogo **Propiedades**. Revise y cambie el contenido y las propiedades del controlador. Por ejemplo, cambie el nombre y la descripción del controlador, habilítelo o deshabilítelo y especifique en qué plataformas se puede ejecutar. 

<!--3607716, fka 1358270-->
A partir de la versión 1810, los paquetes de controladores tienen campos de metadatos para **Fabricante** y **Modelo**. Use estos campos para etiquetar los paquetes de controladores con información para ayudar en el mantenimiento general o para identificar controladores antiguos y duplicados que se pueden eliminar. En la pestaña **General**, seleccione un valor existente en las listas desplegables o escriba una cadena para crear una nueva entrada.

En el nodo **Paquetes de controladores**, estos campos se muestran en la lista como las columnas **Fabricante del controlador** y **Modelo del controlador**. También se pueden usar como criterios de búsqueda.

A partir de la versión 1906, use estos atributos para almacenar en caché previamente el contenido de un cliente. Para obtener más información, vea [Configuración del contenido de la caché previa](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Controladores de dispositivo

Puede instalar controladores en equipos de destino sin incluirlos en la imagen del sistema operativo que se implementa. Configuration Manager proporciona un catálogo de controladores con referencias a todos los controladores que se importan en Configuration Manager. El catálogo de controladores se encuentra en el área de trabajo **Biblioteca de software** y consta de dos nodos: **Controladores** y **Paquetes de controladores**. El nodo **Controladores** enumera todos los controladores que haya importado en el catálogo de controladores.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Importar controladores de dispositivos en el catálogo de controladores  

Para poder usar un controlador al implementar un sistema operativo, debe importarlo en el catálogo de controladores. Para administrarlos mejor, importe solo los controladores que va a instalar como parte de las implementaciones del sistema operativo. Guarde varias versiones de controladores en el catálogo de controladores para proporcionar una manera sencilla de actualizar los controladores existentes cuando se producen cambios en los requisitos de hardware en la red.  

Como parte del proceso de importación para el controlador de dispositivo, Configuration Manager lee las siguientes propiedades sobre el controlador:
- Provider
- Class
- Version
- Firma
- Hardware compatible
- Información de la plataforma admitida

De forma predeterminada, el controlador recibe el nombre del primer dispositivo de hardware al que presta servicio. Puede cambiar el nombre del controlador de dispositivo más adelante. La lista de plataformas compatibles se basa en la información del archivo INF del controlador. Como la exactitud de esta información puede variar, compruebe manualmente que el controlador es compatible después de importarlo en el catálogo.  

Después de importar controladores de dispositivos en el catálogo, agréguelos a los paquetes de controladores o a paquetes de imágenes de arranque.  

> [!IMPORTANT]  
> No puede importar controladores de dispositivos directamente en una subcarpeta del nodo **Controladores**. Para importar un controlador de dispositivo en una subcarpeta, primero importe el controlador de dispositivo en el nodo **Controladores** y, después, mueva el controlador a la subcarpeta.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Proceso de importación de controladores de dispositivos de Windows en el catálogo de controladores  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Sistemas operativos** y seleccione el nodo **Controladores**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Importar controlador** para iniciar el **Asistente para importar nuevo controlador**.  

3. En la página **Buscar controlador**, especifique las opciones siguientes:  

    - **Importar todos los controladores en la siguiente ruta de acceso de red (UNC)** : Para importar todos los controladores de dispositivo en una carpeta específica, especifique la ruta de acceso de red. Por ejemplo: `\\servername\share\folder`.  

        > [!NOTE]  
        > Si hay un gran número de subcarpetas y una gran cantidad de archivos INF del controlador, este proceso puede tardar tiempo.  

    - **Importar un controlador específico**: para importar un controlador específico desde una carpeta, especifique la ruta de acceso de red al archivo INF del controlador de dispositivo de Windows.  

    - **Especificar la opción para controladores duplicados**: seleccione cómo quiere que Configuration Manager administre las categorías de controladores cuando importe un controlador de dispositivo duplicado.  
        - **Importar el controlador y agregar una nueva categoría a las categorías existentes**  
        - **Importar el controlador y conservar las categorías existentes**  
        - **Importar el controlador y sobrescribir las categorías existentes**  
        - **No importar el controlador**  

    > [!IMPORTANT]  
    > Cuando se importan controladores, el servidor de sitio debe tener permiso de **lectura** en la carpeta o se producirá un error en la importación.  

4. En la página **Detalles del controlador**, especifique las opciones siguientes:  

    - **Ocultar los controladores que no sean de almacenamiento o red (para imágenes de arranque)** : Use esta opción para mostrar solo los controladores de almacenamiento y red. Esta opción también oculta otros controladores que no suelen ser necesarios para las imágenes de arranque, como un controlador de vídeo o de módem.  

    - **Ocultar los controladores que no estén firmados digitalmente**: Microsoft recomienda usar solo los controladores que estén firmados digitalmente.  

    - En la lista de controladores, seleccione los controladores que desee importar en el catálogo de controladores.  

    - **Habilitar estos controladores y permitir que los equipos los instalen**: seleccione esta opción para permitir que los equipos instalen los controladores de dispositivos. Esta opción está habilitada de forma predeterminada.  

        > [!IMPORTANT]  
        > Si un controlador de dispositivo causa un problema o desea suspender su instalación, deshabilítelo durante la importación. También puede deshabilitar los controladores después de importarlos.  

    - Para asignar controladores de dispositivos a una categoría administrativa con propósitos de filtrado, como las categorías de "Equipos de escritorio" o "Blocs de notas", haga clic en **Categorías**. Luego, seleccione una categoría existente o cree una nueva categoría. Use categorías para controlar qué controladores de dispositivos se aplican con el paso de la secuencia de tareas [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).  

5. En la página **Agregar controlador a paquetes**, elija si quiere agregar los controladores a un paquete.  

    - Seleccione los paquetes de controladores que se utilizan para distribuir los controladores de dispositivos.  

        Si es necesario, seleccione **Nuevo paquete** para crear un nuevo paquete de controladores. Cuando cree un nuevo paquete de controladores, proporcione un recurso compartido de red que no use ningún otro paquete de controladores.  

    - Si el paquete ya se distribuyó a los puntos de distribución, seleccione **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyan a los puntos de distribución. Si selecciona **No**, ejecute la acción **Actualizar punto de distribución** antes de usar la imagen de arranque. Si el paquete de controladores no se distribuyó nunca, debe usar la acción **Distribuir contenido** en el nodo **Paquetes de controladores**.  

6. En la página **Agregar controlador a imágenes de arranque**, elija si desea agregar los controladores de dispositivos a imágenes de arranque existentes.  

    > [!NOTE]  
    > Agregue solo controladores de almacenamiento y red a las imágenes de arranque.  

    - Seleccione **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyan a los puntos de distribución. Si selecciona **No**, ejecute la acción **Actualizar punto de distribución** antes de usar la imagen de arranque. Si el paquete de controladores no se distribuyó nunca, debe usar la acción **Distribuir contenido** en el nodo **Paquetes de controladores**.  

    - Configuration Manager le advierte si la arquitectura de uno o varios controladores no coincide con la arquitectura de las imágenes de arranque que seleccionó. Si no coinciden, seleccione **Aceptar**. Vuelva a la página **Detalles del controlador** para borrar los controladores que no coinciden con la arquitectura de la imagen de arranque seleccionada. Por ejemplo, si selecciona una imagen de arranque x64 y x86, todos los controladores deben admitir ambas arquitecturas. Si selecciona una imagen de arranque x64, todos los controladores deben admitir la arquitectura x64.  

        > [!NOTE]  
        > - La arquitectura se basa en la arquitectura que se indica en el archivo INF del fabricante.  
        > - Si un controlador indica que es compatible con ambas arquitecturas, puede importarlo en ambas imágenes de arranque.  

    - Configuration Manager le advierte si agrega controladores de dispositivo que no son controladores de red o de almacenamiento a una imagen de arranque. En la mayoría de los casos, no son necesarios para la imagen de arranque. Seleccione **Sí** para agregar los controladores a la imagen de arranque o **No** para volver atrás y modificar la selección de controladores.  

    - Configuration Manager le advierte si uno o varios de los controladores seleccionados no están firmados digitalmente de forma correcta. Seleccione **Sí** para continuar y seleccione **No** para volver atrás y cambiar la selección de controladores.  

7. Complete el asistente.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Administrar controladores de dispositivos en un paquete de controladores  

Utilice los procedimientos siguientes para modificar paquetes de controladores e imágenes de arranque. Para agregar o quitar un controlador, primero búsquelo en el nodo **Controladores**. A continuación, edite los paquetes o imágenes de arranque que están asociados al controlador seleccionado.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Sistemas operativos** y seleccione el nodo **Controladores**.  

2. Seleccione los controladores de dispositivos que desee agregar al paquete de controladores.  

3. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Controlador**, seleccione **Editar**y, a continuación, elija **Paquetes de controladores**.  

4. Para agregar un controlador de dispositivo, active la casilla de los paquetes de controladores a los que desee agregar el controlador de dispositivo. Para quitar un controlador de dispositivo, desactive la casilla de los paquetes de controladores de los que desee quitar el controlador de dispositivo.  

    Si está agregando controladores de dispositivos que están asociados con los paquetes de controladores, puede crear opcionalmente un nuevo paquete. Seleccione **Nuevo paquete**, con lo que se abre el cuadro de diálogo **Nuevo paquete de controladores**.  

5. Si el paquete ya se distribuyó a los puntos de distribución, seleccione **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyan a los puntos de distribución. Si selecciona **No**, ejecute la acción **Actualizar punto de distribución** antes de usar la imagen de arranque. Si el paquete de controladores no se distribuyó nunca, debe usar la acción **Distribuir contenido** en el nodo **Paquetes de controladores**. Para que los controladores estén disponibles, debe actualizar el paquete de controladores en los puntos de distribución.  

    Seleccione **Aceptar** cuando termine.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Administrar controladores de dispositivos en una imagen de arranque  

Puede agregar a imágenes de arranque los controladores de dispositivos de Windows que se han importado en el catálogo. Use las siguientes directrices al agregar controladores de dispositivos a una imagen de arranque:  

- Agregue solo controladores de almacenamiento y red a las imágenes de arranque. Normalmente no se requieren otros tipos de controladores en Windows PE. Los controladores que no son necesarios aumentan el tamaño de la imagen de arranque innecesariamente.  

- Agregue solo controladores de dispositivos para Windows 10 a una imagen de arranque. La versión requerida de Windows PE se basa en Windows 10.  

- Asegúrese de que usa el controlador de dispositivo correcto para la arquitectura de la imagen de arranque. No agregue un controlador de dispositivo x86 a una imagen de arranque x64.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Proceso para modificar los controladores de dispositivos asociados a una imagen de arranque  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Sistemas operativos** y seleccione el nodo **Controladores**.  

2. Seleccione los controladores de dispositivos que desee agregar al paquete de controladores.  

3. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Controlador**, seleccione **Editar** y, a continuación, elija **Imágenes de arranque**.  

4. Para agregar un controlador de dispositivo, active la casilla de la imagen de arranque a la que desee agregar el controlador de dispositivo. Para quitar un controlador de dispositivo, desactive la casilla de la imagen de arranque de la que desee quitar el controlador de dispositivo.  

5. Si no desea actualizar los puntos de distribución donde se almacena la imagen de arranque, desactive la casilla **Actualizar puntos de distribución cuando termine**. De forma predeterminada, los puntos de distribución se actualizan cuando se actualiza la imagen de arranque.  

    - Seleccione **Sí** en el cuadro de diálogo para actualizar las imágenes de arranque en los puntos de distribución. No puede utilizar controladores de dispositivos hasta que se distribuyan a los puntos de distribución. Si selecciona **No**, ejecute la acción **Actualizar punto de distribución** antes de usar la imagen de arranque. Si el paquete de controladores no se distribuyó nunca, debe usar la acción **Distribuir contenido** en el nodo **Paquetes de controladores**.  

    - Configuration Manager le advierte si la arquitectura de uno o varios controladores no coincide con la arquitectura de las imágenes de arranque que seleccionó. Si no coinciden, seleccione **Aceptar**. Vuelva a la página **Detalles del controlador** para borrar los controladores que no coinciden con la arquitectura de la imagen de arranque seleccionada. Por ejemplo, si selecciona una imagen de arranque x64 y x86, todos los controladores deben admitir ambas arquitecturas. Si selecciona una imagen de arranque x64, todos los controladores deben admitir la arquitectura x64.  

        > [!NOTE]
        > - La arquitectura se basa en la arquitectura que se indica en el archivo INF del fabricante.  
        > - Si un controlador indica que es compatible con ambas arquitecturas, puede importarlo en ambas imágenes de arranque.  

    - Configuration Manager le advierte si agrega controladores de dispositivo que no son controladores de red o de almacenamiento a una imagen de arranque. En la mayoría de los casos, no son necesarios para la imagen de arranque. Seleccione **Sí** para agregar los controladores a la imagen de arranque o **No** para volver atrás y modificar la selección de controladores.  

    - Configuration Manager le advierte si uno o varios de los controladores seleccionados no están firmados digitalmente de forma correcta. Seleccione **Sí** para continuar o seleccione **No** para volver atrás y cambiar la selección de controladores.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a> Acciones adicionales para controladores de dispositivos  

Puede realizar acciones adicionales para administrar los controladores cuando se seleccionan en el nodo **Controladores**.  

#### <a name="categorize"></a>Clasificar
Borra, administra o establece una categoría administrativa para los controladores seleccionados.

#### <a name="delete"></a>Eliminar
Quita el controlador del nodo **Controladores** y también quita el controlador de los puntos de distribución asociados.

#### <a name="disable"></a>Deshabilitar
Impide que el controlador se instale. Esta acción deshabilita temporalmente el controlador. La secuencia de tareas no puede instalar un controlador deshabilitado cuando se implementa un sistema operativo. 

> [!Note]  
> Esta acción solo impide que los controladores realicen la instalación mediante el paso de la secuencia de tareas **Aplicar controladores automáticamente**.

#### <a name="enable"></a>Habilitar
Permite a los equipos cliente de Configuration Manager y las secuencias de tareas instalar el controlador de dispositivo cuando se implementa el sistema operativo.

#### <a name="move"></a>Mover
Mueve el controlador de dispositivo a otra carpeta en el nodo **Controladores**.

#### <a name="properties"></a>Propiedades
Se abrirá el cuadro de diálogo **Propiedades**. Revise y cambie las propiedades del controlador. Por ejemplo, cambie su nombre y descripción, habilítelo o deshabilítelo y especifique en qué plataformas se puede ejecutar.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a> Usar secuencias de tareas para instalar controladores  

Use secuencias de tareas para automatizar la implementación del sistema operativo. Cada paso en la secuencia de tareas puede realizar una acción determinada como, por ejemplo, la instalación de un controlador. Puede usar estos dos pasos de secuencia de tareas para instalar controladores de dispositivos durante la implementación de un sistema operativo:  

- [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Este paso le permite encontrar controladores de dispositivos coincidentes e instalarlos como parte de la implementación de sistema operativo. Puede configurar el paso de la secuencia de tareas para instalar solo el controlador que mejor coincida con cada dispositivo de hardware detectado. Alternativamente, especifique que el paso instala todos los controladores compatibles con cada dispositivo de hardware detectado y permita que el programa de instalación de Windows elija el mejor controlador. Además, puede especificar una categoría de controladores para limitar los controladores que están disponibles en este paso.  

- [Aplicar paquete de controladores](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Este paso le permite poner todos los controladores de dispositivos en un determinado paquete de controladores a disposición del programa de instalación de Windows. El programa de instalación de Windows busca los controladores de dispositivos necesarios en los paquetes de controladores especificados. Al crear medios independientes, debe usar esta etapa para instalar controladores de dispositivos.  

Al usar estos pasos de la secuencia de tareas, también puede especificar cómo se instalan los controladores de dispositivos en el equipo en el que se implementa el sistema operativo. Para obtener más información, vea [Manage task sequences to automate tasks](../deploy-use/manage-task-sequences-to-automate-tasks.md) (Administración de secuencias de tareas para automatizar tareas).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a> Informes de controladores  

Puede usar varios informes en la categoría de informes **Administración de controladores** para obtener información general acerca de los controladores de dispositivos en el catálogo de controladores. Para obtener más información sobre cómo ejecutar informes, consulte [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).

