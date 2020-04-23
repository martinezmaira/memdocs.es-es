---
title: Implementación de contenido
titleSuffix: Configuration Manager
description: Después de instalar puntos de distribución para Configuration Manager, siga los pasos que se indican a continuación para empezar a implementar contenido en ellos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7478eff1a14eeffd4d12b1539df7c5573c6a7cb6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707263"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Implementar y administrar contenido en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de instalar puntos de distribución para Configuration Manager, puede empezar a implementar contenido en ellos. Normalmente, el contenido se transfiere a los puntos de distribución a través de la red, pero existen otras opciones para llevar el contenido a los puntos de distribución. Después de que se haya transferido el contenido a un punto de distribución, puede actualizar, redistribuir, quitar y validar ese contenido en los puntos de distribución.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a> Distribuir contenido  
Normalmente, se distribuye contenido en puntos de distribución para que esté disponible en los equipos cliente. (La excepción es el uso de la distribución de contenido a petición para una implementación específica).  Al distribuir contenido, Configuration Manager almacena archivos de contenido en un paquete y, después, distribuye el paquete al punto de distribución. Entre los diversos tipos de contenido que se pueden distribuir se incluyen los siguientes:  

- Tipos de implementación de aplicaciones  

- Paquetes  

- Paquetes de implementación  

- Paquetes de controladores  

- Imágenes de sistema operativo  

- Instaladores de sistema operativo  

- Imágenes de arranque  

- Secuencias de tareas  

Cuando crea un paquete que contiene archivos de origen como, por ejemplo, tipos de implementación de aplicaciones o paquetes de implementación, el sitio en el que se crea el paquete se convierte en el propietario del sitio del origen de contenido del paquete. Configuration Manager copia los archivos de origen desde la ruta de acceso del archivo de origen especificada para el objeto a la biblioteca de contenido en el servidor de sitio al que pertenece el origen de contenido del paquete.  Después, Configuration Manager replica la información en los sitios adicionales. (Consulte [The content library](../../../../core/plan-design/hierarchy/the-content-library.md) (La biblioteca de contenido) para obtener más información sobre este tema).  

Utilice el siguiente procedimiento para distribuir contenido en puntos de distribución.  

#### <a name="to-distribute-content-on-distribution-points"></a>Para distribuir contenido en puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los siguientes pasos para el tipo de contenido que desea distribuir:  

    - **Aplicaciones**: expanda **Administración de aplicaciones** > **Aplicaciones** y, después, seleccione las aplicaciones que quiera distribuir.  

    - **Paquetes**: expanda **Administración de aplicaciones** >  **Paquetes** y, después, seleccione los paquetes que quiera distribuir.  

    - **Paquetes de implementación**: expanda **Actualizaciones de software** >  **Paquetes de implementación** y, después, seleccione los paquetes de implementación que quiera distribuir.  

    - **Paquetes de controladores**: expanda **Sistemas operativos** >  **Paquetes de controladores** y, después, seleccione los paquetes de controladores que quiera distribuir.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos** >   **Imágenes de sistema operativo** y, después, seleccione las imágenes de sistema operativo que quiera distribuir.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos** > **Instaladores de sistema operativo** y, después, seleccione los instaladores de sistema operativo que quiera distribuir.  

    - **Imágenes de arranque**: expanda **Sistemas operativos** >  **Imágenes de arranque** y, después, seleccione las imágenes de arranque que quiera distribuir.  

    - **Secuencias de tareas**: expanda **Sistemas operativos** >  **Secuencias de tareas** y, después, seleccione la secuencia de tareas que quiera distribuir. Aunque las secuencias de tareas no incluyen contenido, tienen las dependencias de contenido asociadas que se distribuyen.  

      > [!NOTE]  
      > Si modifica la secuencia de tareas, deberá redistribuir el contenido.  

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Distribuir contenido**. Se abre el Asistente para distribuir contenido.  

4.  En la página **General**, compruebe que el contenido que aparece es el contenido que quiere distribuir, elija si quiere que Configuration Manager detecte las dependencias de contenido asociadas al contenido seleccionado y agregue las dependencias a la distribución. Después, haga clic en **Siguiente**.  

    > [!NOTE]  
    > Puede configurar la opción **Detectar dependencias de contenido asociadas y agregarlas a esta distribución** solo para el tipo de contenido de aplicación. Configuration Manager configura automáticamente esta opción para las secuencias de tareas, y no se puede modificar.  

5.  En la pestaña **Contenido** , si se muestra, compruebe que el contenido que aparece es el contenido que desea distribuir y, a continuación, haga clic en **Siguiente**.  

    > [!NOTE]  
    > La página **Contenido** se muestra solo cuando la opción **Detectar dependencias de contenido asociadas y agregarlas a esta distribución** está seleccionada en la página **General** del asistente.  

6.  En la página **Destino del contenido** , haga clic en **Agregar**, elija una de las siguientes opciones y, a continuación, siga el paso asociado:  

    - **Recopilaciones**: seleccione **Recopilaciones de usuarios** o **Recopilaciones de dispositivos**, haga clic en la recopilación asociada a uno o más grupos de puntos de distribución y, después, haga clic en **Aceptar**.  

        > [!NOTE]  
        > Se muestran solo las recopilaciones que están asociadas a un grupo de puntos de distribución. Para más información sobre cómo asociar recopilaciones a grupos de puntos de distribución, vea la sección [Administrar grupos de puntos de distribución](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) en el tema [Instalación y configuración de puntos de distribución de Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    - **Punto de distribución**: seleccione un punto de distribución existente y, después, haga clic en **Aceptar**. No se muestran los puntos de distribución que recibieron previamente el contenido.  

    - **Grupo de puntos de distribución**: seleccione un grupo de puntos de distribución existente y, después, haga clic en **Aceptar**. No se muestran los grupos de puntos de distribución que recibieron previamente el contenido.  

    Cuando termine de agregar los destinos del contenido, haga clic en **Siguiente**.  

7.  En la página **Resumen** , revise la configuración de la distribución antes de continuar. Para distribuir el contenido en los destinos seleccionados, haga clic en **Siguiente**.  

8.  En la página **Progreso** se muestra el progreso de la distribución.  

9. La página **Confirmación** muestra si el contenido se asignó correctamente a los puntos. Para supervisar la distribución de contenido, vea [Supervisar el contenido distribuido con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a> Usar contenido preconfigurado  
Se pueden preconfigurar los archivos de contenido para aplicaciones y tipos de paquetes:  

- En la consola de Configuration Manager, seleccione el contenido que necesite y, después, use el **Asistente para crear archivos de contenido preconfigurados** para crear un archivo de contenido preconfigurado comprimido que contenga los archivos y los metadatos asociados del contenido seleccionado.  

- A continuación puede importar manualmente el contenido en un servidor de sitio, un sitio secundario o un punto de distribución.  

- Cuando se importa el archivo de contenido preconfigurado en un servidor de sitio, los archivos de contenido se agregan a la biblioteca de contenido del servidor de sitio y, a continuación, se registran en la base de datos del servidor de sitio.  

- Cuando se importa el archivo de contenido preconfigurado en un punto de distribución, los archivos de contenido se agregan a la biblioteca de contenido del punto de distribución y se envía un mensaje de estado al servidor de sitio para notificar al sitio que el contenido está disponible en el punto de distribución.  

**Limitaciones y consideraciones para el contenido preconfigurado:**  

- **Cuando el punto de distribución se encuentra en el servidor de sitio**, no habilite el punto de distribución para contenido preconfigurado. En su lugar, use el procedimiento descrito en [How to prestage content on a distribution point on a site server](#bkmk_dpsiteserver) (Cómo preconfigurar el contenido en un punto de distribución de un servidor de sitio).  

- **Cuando el punto de distribución está configurado como un punto de distribución de extracción**, no habilite el punto de distribución para contenido preconfigurado. La configuración del contenido preconfigurado para un punto de distribución reemplaza la configuración de punto de distribución de extracción. Un punto de distribución de extracción que está configurado para contenido preconfigurado no extrae contenido del punto de distribución de origen y no recibe contenido del servidor de sitio.  

- **La biblioteca de contenido se debe crear en el punto de distribución para poder preconfigurar contenido para el punto de distribución**. Distribuya el contenido a través de la red al menos una vez antes de preconfigurar el contenido para el punto de distribución.  

- **Cuando se preconfigura contenido para un paquete con una ruta de origen de paquete larga** (por ejemplo, de más de 140 caracteres), es posible que la herramienta de línea de comandos de extracción de contenido no extraiga correctamente el contenido de ese paquete en la biblioteca de contenido.  

Para obtener información sobre cuándo se deben preconfigurar los archivos de contenido, consulte *Prestaged content* (Contenido preconfigurado) en el tema [Manage network bandwidth for content management](../../../plan-design/hierarchy/manage-network-bandwidth.md) (Administración del ancho de banda de red para la administración de contenido).  

Consulte las siguientes secciones para preconfigurar el contenido.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a> Paso 1: Crear un archivo de contenido preconfigurado  
Se puede crear un archivo de contenido preconfigurado comprimido que contenga los archivos y los metadatos asociados del contenido que se selecciona en la consola de Configuration Manager. Utilice el procedimiento siguiente para crear un archivo de contenido preconfigurado.  

##### <a name="to-create-a-prestaged-content-file"></a>Para crear un archivo de contenido preconfigurado  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los pasos siguientes para el tipo de contenido que desea preconfigurar:  

    - **Aplicaciones**: expanda **Administración de aplicaciones**, haga clic en **Aplicaciones** y, después, seleccione las aplicaciones que quiera preconfigurar.  

    - **Paquetes**: expanda **Administración de aplicaciones**, haga clic en **Paquetes** y, después, seleccione los paquetes que quiera preconfigurar.  

    - **Paquetes de controladores**: expanda **Sistemas operativos**, haga clic en **Paquetes de controladores** y, después, seleccione los paquetes de controladores que quiera preconfigurar.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos**, haga clic en **Imágenes de sistema operativo** y, después, seleccione las imágenes de sistema operativo que quiera preconfigurar.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos**, haga clic en **Instaladores de sistema operativo** y, después, seleccione los instaladores de sistema operativo que quiera preconfigurar.  

    - **Imágenes de arranque**: expanda **Sistemas operativos**, haga clic en **Imágenes de arranque** y, después, seleccione las imágenes de arranque que quiera preconfigurar.  

    - **Secuencias de tareas**: expanda **Sistemas operativos**, haga clic en **Secuencias de tareas** y, después, seleccione la secuencia de tareas que quiera preconfigurar.  

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Crear archivo de contenido preconfigurado**. Se abre el Asistente para crear archivos de contenido preconfigurados.  

    > [!NOTE]  
    > **Para aplicaciones**: en la pestaña **Inicio**, en el grupo **Aplicación**, haga clic en **Crear archivo de contenido preconfigurado**.  
    >   
    > **Para los paquetes:** en la pestaña **Inicio**, en el grupo &lt;*Nombre del paquete*>, haga clic en **Crear archivo de contenido preconfigurado**.  

4.  En la página **General** , haga clic en **Examinar**, elija la ubicación del archivo de contenido preconfigurado, especifique el nombre del archivo y, a continuación, haga clic en **Guardar**. Utilice este archivo de contenido preconfigurado en servidores de sitio primario, servidores de sitio secundario o puntos de distribución para importar el contenido y los metadatos.  

5.  Para las aplicaciones, seleccione **Exportar todas las dependencias** para que Configuration Manager detecte las dependencias asociadas a la aplicación y las agregue al archivo de contenido preconfigurado. De forma predeterminada, esta opción está seleccionada.  

6.  En **Comentarios del administrador**, si lo desea, escriba sus comentarios acerca del archivo de contenido preconfigurado y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Contenido** , compruebe que el contenido que aparece es el contenido que desea agregar al archivo de contenido preconfigurado y, a continuación, haga clic en **Siguiente**.  

8.  En la página **Ubicaciones de contenido** , especifique los puntos de distribución desde los que se van a recuperar los archivos de contenido para el archivo de contenido preconfigurado. Se puede seleccionar más de un punto de distribución para recuperar el contenido. Los puntos de distribución se enumeran en la sección Ubicaciones de contenido. En la columna **Contenido** se muestra cuántos de los paquetes o aplicaciones seleccionados están disponibles en cada punto de distribución. Configuration Manager empieza por el primer punto de distribución de la lista para recuperar el contenido seleccionado y, después, continúa con los demás elementos de la lista para recuperar el contenido restante necesario para el archivo de contenido preconfigurado. Haga clic en **Subir** o **Bajar** para cambiar el orden de prioridad de los puntos de distribución. Si los puntos de distribución de la lista no contienen todo el contenido seleccionado, es necesario agregar a la lista los puntos de distribución que contengan el contenido o salir del asistente, distribuir el contenido al menos a un punto de distribución y, a continuación, reiniciar el asistente.  

9. En la página **Resumen** , confirme los detalles. Puede volver a las páginas anteriores y realizar cambios. Haga clic en **Siguiente** para crear el archivo de contenido preconfigurado.  

10. En la página **Progreso** se muestra el contenido que se está agregando al archivo de contenido preconfigurado.  

11. En la página **Finalización** , compruebe que el archivo de contenido preconfigurado se creó correctamente y, a continuación, haga clic en **Cerrar**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a> Paso 2: Asignar el contenido a los puntos de distribución  
 Una vez preconfigurado el archivo de contenido, asigne el contenido a los puntos de distribución.  

> [!NOTE]  
> Si utiliza un archivo de contenido preconfigurado para recuperar la biblioteca de contenido de un servidor de sitio y no necesita preconfigurar los archivos de contenido de un punto de distribución, puede omitir este procedimiento.  

 Utilice el siguiente procedimiento para asignar el contenido del archivo de contenido preconfigurado a los puntos de distribución.  

> [!IMPORTANT]  
> Compruebe que los puntos de distribución que desea preconfigurar están configurados como puntos de distribución preconfigurados o que el contenido se distribuye a los puntos de distribución mediante la red.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Para asignar el contenido a los puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los pasos siguientes para el tipo de contenido seleccionado cuando creó el archivo de contenido preconfigurado:  

    - **Aplicaciones**: expanda **Administración de aplicaciones**, haga clic en **Aplicaciones** y, después, seleccione las aplicaciones preconfiguradas.  

    - **Paquetes**: expanda **Administración de aplicaciones**, haga clic en **Paquetes** y, después, seleccione los paquetes preconfigurados.  

    - **Paquetes de implementación**: expanda **Actualizaciones de software**, haga clic en **Paquetes de implementación** y, después, seleccione los paquetes de implementación preconfigurados.  

    - **Paquetes de controladores**: expanda **Sistemas operativos**, haga clic en **Paquetes de controladores** y, después, seleccione los paquetes de controladores preconfigurados.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos**, haga clic en **Imágenes de sistema operativo** y, después, seleccione las imágenes de sistema operativo preconfiguradas.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos**, haga clic en **Instaladores de sistema operativo** y, después, seleccione los instaladores de sistema operativo preconfigurados.  

    - **Imágenes de arranque**: expanda **Sistemas operativos**, haga clic en **Imágenes de arranque** y, después, seleccione las imágenes de arranque preconfiguradas.  

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Distribuir contenido**. Se abre el Asistente para distribuir contenido.  

4.  En la página **General**, compruebe que el contenido que aparece es el contenido preconfigurado, elija si quiere que Configuration Manager detecte las dependencias de contenido asociadas al contenido seleccionado y agregue las dependencias a la distribución. Después, haga clic en **Siguiente**.  

    > [!NOTE]  
    > Puede configurar la opción **Detectar dependencias de contenido asociadas y agregarlas a esta distribución** solo para el tipo de contenido de aplicación. Configuration Manager configura automáticamente esta opción para las secuencias de tareas, y no se puede modificar.  

5.  En la página **Contenido** , si se muestra, compruebe que el contenido que aparece es el contenido que desea distribuir y, a continuación, haga clic en **Siguiente**.  

    > [!NOTE]  
    > La página **Contenido** se muestra solo cuando la opción **Detectar dependencias de contenido asociadas y agregarlas a esta distribución** está seleccionada en la página **General** del asistente.  

6.  En la página **Destino del contenido** , haga clic en **Agregar**, elija una de las siguientes opciones que incluya los puntos de distribución a preconfigurar y, a continuación, siga el paso asociado:  

    - **Recopilaciones**: seleccione **Recopilaciones de usuarios** o **Recopilaciones de dispositivos**, haga clic en la recopilación asociada a uno o más grupos de puntos de distribución y, después, haga clic en **Aceptar**.  

      > [!NOTE]  
      > Se muestran solo las recopilaciones que están asociadas a un grupo de puntos de distribución.  Para más información, vea [Administrar grupos de puntos de distribución](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) en el tema [Instalación y configuración de puntos de distribución de Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    - **Punto de distribución**: seleccione un punto de distribución existente y, después, haga clic en **Aceptar**. No se muestran los puntos de distribución que recibieron previamente el contenido.  

    - **Grupo de puntos de distribución**: seleccione un grupo de puntos de distribución existente y, después, haga clic en **Aceptar**. No se muestran los grupos de puntos de distribución que recibieron previamente el contenido.  

    Cuando termine de agregar los destinos del contenido, haga clic en **Siguiente**.  

7.  En la página **Resumen** , revise la configuración de la distribución antes de continuar. Para distribuir el contenido en los destinos seleccionados, haga clic en **Siguiente**.  

8.  En la página **Progreso** se muestra el progreso de la distribución.  

9. La página **Confirmación** muestra si el contenido se asignó correctamente o no a los puntos de distribución. Para supervisar la distribución de contenido, vea [Supervisar el contenido distribuido con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a> Paso 3: Extraer el contenido del archivo de contenido preconfigurado  
Después de crear el archivo de contenido preconfigurado y asignar el contenido a puntos de distribución, puede extraer los archivos de contenido en la biblioteca de contenido de un servidor de sitio o punto de distribución. Normalmente, se copió el archivo de contenido preconfigurado en una unidad portátil, como una unidad USB, o se grabó el contenido en un medio, como un DVD, y está disponible en la ubicación del servidor de sitio o punto de distribución que necesita el contenido.  

Utilice el siguiente procedimiento para exportar manualmente los archivos de contenido desde el archivo de contenido preconfigurado mediante la herramienta de línea de comandos de extraer contenido.  

> [!IMPORTANT]  
> Al ejecutar la herramienta de línea de comandos de extraer contenido, la herramienta crea un archivo temporal mientras crea el archivo de contenido preconfigurado. A continuación, el archivo se copia en la carpeta de destino y se elimina el archivo temporal. Debe tener suficiente espacio en disco para este archivo temporal o se producirá un error en el proceso. El archivo temporal se crea en la siguiente ubicación:  
>   
> - El archivo temporal se crea en la misma carpeta que especificó como carpeta de destino para el archivo de contenido preconfigurado.  

> [!IMPORTANT]  
> El usuario que ejecuta la herramienta de línea de comandos de extracción de contenido debe tener derechos de **Administrador** en el equipo desde el que va a extraer el contenido preconfigurado.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Para extraer los archivos de contenido del archivo de contenido preconfigurado  

1.  Copie el archivo de contenido preconfigurado en el equipo desde el que desea extraer el contenido.  

2.  Copie la herramienta de línea de comandos de extracción de contenido desde &lt;*ruta de instalación de Configuration Manager*>\bin\\&lt;*plataforma*> en el equipo del que quiere extraer el archivo de contenido preconfigurado.  

3.  Abra el símbolo del sistema y desplácese hasta la ubicación de la carpeta de la herramienta de extraer contenido y el archivo de contenido preconfigurado.  

    > [!NOTE]  
    > Puede extraer uno o varios archivos de contenido preconfigurado en un servidor de sitio, un servidor de sitio secundario o un punto de distribución.  

4.  Escriba **extractcontent /P:** &lt;*PrestagedFileLocation*> **\\** &lt;*PrestagedFileName*>  **/S** para importar un solo archivo.  

    Escriba **extractcontent /P:** &lt;*PrestagedFileLocation*>  **/S** para importar todos los archivos preconfigurados en la carpeta especificada.  

    Por ejemplo, escriba **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S**, donde `D:\PrestagedFiles\` es la ubicación de archivo preconfigurado, `MyPrestagedFile.pkgx` es el nombre de archivo preconfigurado y `/S` indica a Configuration Manager que extraiga solamente los archivos de contenido posteriores a los que ya existen en el punto de distribución.  

    Cuando se extrae el archivo de contenido preconfigurado en un servidor de sitio, los archivos de contenido se agregan a la biblioteca de contenido del servidor de sitio y, a continuación, el contenido disponible se registra en la base de datos del servidor de sitio. Cuando se exporta el archivo de contenido preconfigurado en un punto de distribución, los archivos de contenido se agregan a la biblioteca de contenido del punto de distribución, el punto de distribución envía un mensaje de estado al servidor de sitio primario principal y, a continuación, el contenido disponible se registra en la base de datos del sitio.  

    > [!IMPORTANT]  
    > En el siguiente escenario, debe actualizar el contenido que extrajo de un archivo de contenido preconfigurado cuando el contenido se actualice a una nueva versión:  
    >   
    >  1.  Se crea un archivo de contenido preconfigurado para la versión 1 de un paquete.  
    >  2.  Se actualizan los archivos de origen para el paquete con la versión 2.  
    >  3.  Se extrae el archivo de contenido preconfigurado (versión 1 del paquete) en un punto de distribución.  
    >   
    > Configuration Manager no distribuye automáticamente la versión 2 del paquete en el punto de distribución. Debe crear un nuevo archivo de contenido preconfigurado que contenga la versión del nuevo archivo y, a continuación, extraer el contenido, actualizar el punto de distribución para distribuir los archivos cambiados o redistribuir todos los archivos en el paquete.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a> Preconfiguración del contenido en un punto de distribución de un servidor de sitio  
Al instalar un punto de distribución en un servidor de sitio, debe usar el procedimiento siguiente para preconfigurar correctamente el contenido. Esto se debe a que los archivos de contenido ya están en la biblioteca de contenido.  

Si el punto de distribución no está habilitado para contenido preconfigurado o no está ubicado en un servidor de sitio, consulte la sección [Usar contenido preconfigurado](#bkmk_prestage) de este tema.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Para preconfigurar el contenido en puntos de distribución ubicados en un servidor de sitio  

1.  Use los pasos siguientes para comprobar que el punto de distribución no esté habilitado para contenido preconfigurado.  

    1.  En la consola de Configuration Manager, haga clic en **Administración**.  

    2.  En el área de trabajo **Administración** , haga clic en **Puntos de distribución**y, a continuación, seleccione el punto de distribución ubicado en el servidor de sitio.  

    3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

    4.  En la pestaña **General** , compruebe que la casilla **Habilitar este punto de distribución para contenido preconfigurado** está desactivada.  

2.  Cree el archivo de contenido preconfigurado mediante el [paso 1: crear un archivo de contenido preconfigurado](#BKMK_CreatePrestagedContentFile) en este tema.  

3.  Asigne el contenido al punto de distribución mediante el [Paso 2: asignar el contenido a puntos de distribución](#BKMK_AssignContentToDistributionPoint) en este tema.  

4.  En el servidor de sitio, extraiga el contenido del archivo de contenido preconfigurado mediante el [Paso 3: extraer el contenido del archivo de contenido preconfigurado](#BKMK_ExportContentFromPrestagedContentFile) de este tema.  

    > [!NOTE]  
    > Si el punto de distribución se encuentra en un sitio secundario, espere como mínimo 10 minutos y, después, use una consola de Configuration Manager conectada al sitio primario principal para asignar el contenido al punto de distribución en el sitio secundario.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a> Administrar el contenido distribuido  
Dispone de las opciones siguientes para administrar el contenido:  
- [Actualizar contenido](#update-content)
- [Redistribuir contenido](#redistribute-content)
- [Quitar contenido](#remove-content)
- [Validar contenido](#validate-content)

### <a name="update-content"></a>Actualizar contenido
Cuando la ubicación del archivo de origen de una implementación se actualiza agregando archivos nuevos o reemplaza archivos existentes con una versión nueva, puede actualizar los archivos de contenido en los puntos de distribución mediante la acción **Actualizar puntos de distribución** o **Actualizar contenido**:  
- Los archivos de contenido se copian de la ruta de acceso del archivo de origen a la biblioteca de contenido en el sitio al que pertenece el origen de contenido del paquete.  
- La versión del paquete se incrementa.  
- Cada instancia de la biblioteca de contenido en los servidores de sitio y en los puntos de distribución se actualiza únicamente con los archivos que se cambiaron.  

> [!WARNING]  
> La versión del paquete para las aplicaciones siempre es 1. Cuando se actualiza el contenido para un tipo de implementación de aplicaciones, Configuration Manager crea un nuevo identificador de contenido para el tipo de implementación y el paquete hace referencia al nuevo identificador de contenido.  

#### <a name="to-update-content-on-distribution-points"></a>Para actualizar contenido en puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los siguientes pasos para el tipo de contenido que desea distribuir:  

    - **Aplicaciones**: expanda **Administración de aplicaciones** > **Aplicaciones** y, después, seleccione las aplicaciones que quiera distribuir. Haga clic en la pestaña **Tipos de implementación** y, a continuación, seleccione el tipo de implementación que desea actualizar.  

    - **Paquetes**: expanda **Administración de aplicaciones** > **Paquetes** y, después, seleccione los paquetes que quiera actualizar.  

    - **Paquetes de implementación**: expanda **Actualizaciones de software** > **Paquetes de implementación** y, después, seleccione los paquetes de implementación que quiera actualizar.  

    - **Paquetes de controladores**: expanda **Sistemas operativos** > **Paquetes de controladores** y, después, seleccione los paquetes de controladores que quiera actualizar.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos** > **Imágenes de sistema operativo** y, después, seleccione las imágenes de sistema operativo que quiera actualizar.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos** > **Instaladores de sistema operativo** y, después, seleccione los instaladores de sistema operativo que quiera actualizar.  

    - **Imágenes de arranque**: expanda **Sistemas operativos** >  **Imágenes de arranque** y, después, seleccione las imágenes de arranque que quiera actualizar.  

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Actualizar puntos de distribución**y, a continuación, haga clic en **Aceptar** para confirmar que desea actualizar el contenido.  

    > [!NOTE]  
    > Para actualizar el contenido para las aplicaciones, haga clic en la pestaña **Tipos de implementación** , haga clic con el botón secundario en el tipo de implementación, haga clic en **Actualizar contenido**y, a continuación, haga clic en **Aceptar** para confirmar que desea actualizar el contenido.  

    > [!NOTE]  
    > Cuando se actualiza contenido para imágenes de arranque, se abre el Asistente para administrar puntos de distribución. Revise la información de la página **Resumen** y, a continuación, complete el asistente para actualizar el contenido.  

### <a name="redistribute-content"></a>Redistribuir contenido
Puede redistribuir un paquete para copiar todos los archivos de contenido del paquete en puntos de distribución o grupos de puntos de distribución y así sobrescribir los archivos existentes.  

Use esta operación para reparar archivos de contenido del paquete o volver a enviar el contenido cuando se produce un error en la distribución inicial. Puede redistribuir un paquete desde:  

- Las propiedades del paquete  
- Las propiedades del punto de distribución  
- Las propiedades del grupo de puntos de distribución  


#### <a name="to-redistribute-content-from-package-properties"></a>Para redistribuir contenido de las propiedades del paquete  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los siguientes pasos para el tipo de contenido que desea distribuir:  

    - **Aplicaciones**: expanda **Administración de aplicaciones** >  **Aplicaciones** y, después, seleccione la aplicación que quiera redistribuir.  

    - **Paquetes**: expanda **Administración de aplicaciones** > **Paquetes** y, después, seleccione el paquete que quiera redistribuir.  

    - **Paquetes de implementación**: expanda **Actualizaciones de software** >  **Paquetes de implementación** y, después, seleccione el paquete de implementación que quiera redistribuir.  

    - **Paquetes de controladores**: expanda **Sistemas operativos** > **Paquetes de controladores** y, después, seleccione el paquete de controladores que quiera redistribuir.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos** > **Imágenes de sistema operativo** y, después, seleccione la imagen de sistema operativo que quiera redistribuir.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos** > **Instaladores de sistema operativo** y, después, seleccione el instalador de sistema operativo que quiera redistribuir.  

    - **Imágenes de arranque**: expanda **Sistemas operativos** >  **Imágenes de arranque** y, después, seleccione la imagen de arranque que quiera redistribuir.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Ubicaciones de contenido** , seleccione el punto de distribución o el grupo de puntos de distribución en el que desea redistribuir el contenido, haga clic en **Redistribuir**y, a continuación, haga clic en **Aceptar**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Para redistribuir contenido de las propiedades de punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Puntos de distribución**y, a continuación, seleccione el punto de distribución en el que desea redistribuir el contenido.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Contenido** , seleccione el contenido que desea redistribuir, haga clic en **Redistribuir**y, a continuación, haga clic en **Aceptar**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Para redistribuir contenido de las propiedades de grupo de puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Grupos de puntos de distribución**y, a continuación, seleccione el grupo de puntos de distribución en el que desea redistribuir el contenido.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Contenido** , seleccione el contenido que desea redistribuir, haga clic en **Redistribuir**y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    > El contenido del paquete se redistribuye a todos los puntos de distribución del grupo de puntos de distribución.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Usar el SDK para forzar la replicación de contenido
Puede usar el método de clase **RetryContentReplication** de Instrumental de administración de Windows (WMI) desde el SDK de Configuration Manager para obligar a que el administrador de distribución copie el contenido de la ubicación de origen en la biblioteca de contenido.  

Use este método únicamente para forzar la replicación cuando tenga que redistribuir contenido después de que se hayan producido problemas con la replicación normal de contenido (lo que suele confirmarse mediante el uso del nodo Supervisión de la consola).   

Para obtener más información sobre esta opción del SDK, consulte [RetryContentReplication Method in Class SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) (Método RetryContentReplication de la clase SMS_CM_UpdatePackages) en MSDN.Microsoft.com.

### <a name="remove-content"></a>Quitar contenido
Cuando ya no necesite el contenido en los puntos de distribución, puede quitar los archivos de contenido del punto de distribución.  

- Las propiedades del paquete  
- Las propiedades del punto de distribución  
- Las propiedades del grupo de puntos de distribución  

Sin embargo, cuando el contenido está asociado a otro paquete que se distribuyó al mismo punto de distribución, no se puede quitar el contenido.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Para quitar archivos de contenido de paquete de los puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los pasos siguientes para el tipo de contenido que desea eliminar:  

    - **Aplicaciones**: expanda **Administración de aplicaciones** > **Aplicaciones** y, después, seleccione la aplicación que quiera quitar.  

    - **Paquetes**: expanda **Administración de aplicaciones** > **Paquetes** y, después, seleccione el paquete que quiera quitar.  

    - **Paquetes de implementación**: expanda **Actualizaciones de software** > **Paquetes de implementación** y, después, seleccione el paquete de implementación que quiera quitar.  

    - **Paquetes de controladores**: expanda **Sistemas operativos** > **Paquetes de controladores** y, después, seleccione el paquete de controladores que quiera quitar.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos** > **Imágenes de sistema operativo** y, después, seleccione la imagen de sistema operativo que quiera quitar.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos** > **Instaladores de sistema operativo** y, después, seleccione el instalador de sistema operativo que quiera quitar.  

    - **Imágenes de arranque**: expanda **Sistemas operativos** > **Imágenes de arranque** y, después, seleccione la imagen de arranque que quiera quitar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Ubicaciones de contenido** , seleccione el punto de distribución o el grupo de puntos de distribución del que desea quitar el contenido, haga clic en **Quitar**y, a continuación, haga clic en **Aceptar**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Para quitar contenido de paquete de las propiedades de punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Puntos de distribución**y, a continuación, seleccione el punto de distribución del que desea eliminar el contenido.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Contenido** , seleccione el contenido que desea quitar, haga clic en **Quitar**y, a continuación, haga clic en **Aceptar**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Para quitar contenido de las propiedades de grupo de puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Grupos de puntos de distribución**y, a continuación, seleccione el grupo de puntos de distribución del que desea quitar contenido.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Contenido** , seleccione el contenido que desea quitar, haga clic en **Quitar**y, a continuación, haga clic en **Aceptar**.  


### <a name="validate-content"></a>Validar contenido
El proceso de validación de contenido comprueba la integridad de los archivos de contenido en puntos de distribución. Habilite la validación de contenido según una programación, o bien inicie manualmente la validación de contenido desde las propiedades de los paquetes y puntos de distribución.  

Cuando se inicia el proceso de validación del contenido, Configuration Manager comprueba los archivos de contenido en puntos de distribución y, si el hash de archivo es inesperado para los archivos del punto de distribución, Configuration Manager crea un mensaje de estado que puede revisar en el área de trabajo **Supervisión**.  

Para más información sobre la configuración de la programación de la validación de contenido, vea la sección [Configuraciones de punto de distribución](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) del tema [Instalación y configuración de puntos de distribución de Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Para iniciar la validación de todo el contenido en un punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Puntos de distribución**y, a continuación, seleccione el punto de distribución en el que desee validar el contenido.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En la pestaña **Contenido** , seleccione el paquete donde desee validar el contenido, haga clic en **Validar**, haga clic en **Aceptar**y, a continuación, haga clic en **Aceptar**de nuevo. Se iniciará el proceso de validación del contenido para el paquete en el punto de distribución.  

5.  Para ver los resultados del proceso de validación de contenido, en el área de trabajo **Supervisión** , expanda **Estado de distribución**y haga clic en el nodo **Estado de contenido** . Se muestra el contenido de cada tipo de paquete (por ejemplo, Aplicación, Paquete de actualización de software e Imagen de arranque). Para más información sobre cómo supervisar el estado del contenido, vea [Supervisar el contenido distribuido con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Para iniciar la validación del contenido de un paquete  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los pasos siguientes para el tipo de contenido que desea validar:  

    - **Aplicaciones**: expanda **Administración de aplicaciones** > **Aplicaciones** y, después, seleccione la aplicación que quiera validar.  

    - **Paquetes**: expanda **Administración de aplicaciones** > **Paquetes** y, después, seleccione el paquete que quiera validar.  

    - **Paquetes de implementación**: expanda **Actualizaciones de software** > **Paquetes de implementación** y, después, seleccione el paquete de implementación que quiera validar.  

    - **Paquetes de controladores**: expanda **Sistemas operativos** > **Paquetes de controladores** y, después, seleccione el paquete de controladores que quiera validar.  

    - **Imágenes de sistema operativo**: expanda **Sistemas operativos** > **Imágenes de sistema operativo** y, después, seleccione la imagen de sistema operativo que quiera validar.  

    - **Instaladores de sistema operativo**: expanda **Sistemas operativos** >  **Instaladores de sistema operativo** y, después, seleccione el instalador de sistema operativo que quiera validar.  

    - **Imágenes de arranque**: expanda **Sistemas operativos** > **Imágenes de arranque** y, después, seleccione la imagen de arranque que quiera preconfigurar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En la pestaña **Ubicaciones de contenido** , seleccione el punto de distribución o grupo de puntos de distribución donde desee validar el contenido, haga clic en **Validar**, haga clic en **Aceptar**y, a continuación, haga clic en **Aceptar**de nuevo. Se inicia el proceso de validación del contenido en el punto de distribución o grupo de puntos de distribución seleccionado.  

5.  Para ver los resultados del proceso de validación de contenido, en el área de trabajo **Supervisión** , expanda **Estado de distribución**y haga clic en el nodo **Estado de contenido** . Se muestra el contenido de cada tipo de paquete (por ejemplo, Aplicación, Paquete de actualización de software e Imagen de arranque). Para más información sobre cómo supervisar el estado del contenido, vea [Supervisar el contenido distribuido con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
