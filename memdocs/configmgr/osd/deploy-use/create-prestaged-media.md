---
title: Crear medios preconfigurados
titleSuffix: Configuration Manager
description: Use medios preconfigurados en Configuration Manager para simplificar la implementación de Windows en varios escenarios.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82bb02d8154939b4b0e0ee89bcc6637e9393acff
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125226"
---
# <a name="create-prestaged-media"></a>Crear medios preconfigurados

*Se aplica a: Configuration Manager (rama actual)*

Los medios preconfigurados en Configuration Manager son un archivo de imagen de Windows (WIM). Se pueden instalar en un equipo sin sistema operativo por el fabricante o en su centro de almacenamiento provisional que no está conectado al entorno de producción de Configuration Manager. Los medios preconfigurados contienen la imagen de arranque que se usa para iniciar el equipo de destino y la imagen del sistema operativo que se aplica al equipo de destino. También puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiere incluir como parte de los medios preconfigurados. La secuencia de tareas que implementa el sistema operativo no se incluye en los medios. Los medios preconfigurados se aplican a la unidad de disco duro de un nuevo equipo antes de enviar el equipo al usuario final.

Use los medios preconfigurados para los siguientes escenarios de implementación del sistema operativo:  

- [Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

- [Deploy Windows to Go](deploy-windows-to-go.md) (Implementación de Windows to Go)  


## <a name="usage"></a>Uso

Cuando el equipo se inicia por primera vez después de haber aplicado los medios preconfigurados, el equipo se inicia en Windows PE. Se conecta a un punto de administración para encontrar la secuencia de tareas que completa el proceso de implementación del sistema operativo. Al implementar una secuencia de tareas que usa medios preconfigurados, el cliente comprueba primero que el contenido de la caché de secuencia de tareas local sea válido. Si el contenido no se encuentra o se ha revisado, el cliente lo descarga desde un punto de distribución o un homólogo.  


## <a name="prerequisites"></a>Requisitos previos

Antes de crear medios preconfigurados con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:

### <a name="boot-image"></a>Imagen de arranque

Tenga en cuenta los siguientes puntos sobre la imagen de arranque que usará en la secuencia de tareas para implementar el sistema operativo:

- La arquitectura de la imagen de arranque debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.
- Asegúrese de que la imagen de arranque contenga los controladores de almacenamiento y red necesarios para aprovisionar el equipo de destino.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creación de una secuencia de tareas para implementar un sistema operativo

Como parte de los medios preconfigurados, especifique la secuencia de tareas para implementar el sistema operativo. Para más información, consulte [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo el contenido asociado con la secuencia de tareas

Distribuya todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Este contenido incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila el contenido del punto de distribución al crear los medios preconfigurados.

Su cuenta de usuario necesita al menos acceso de **Lectura** a la biblioteca de contenido en ese punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Unidad de disco duro del equipo de destino

La unidad de disco duro del equipo de destino debe estar formateada antes de aplicarle los medios preconfigurados. Si la unidad de disco duro no está formateada cuando se apliquen los medios, la secuencia de tareas que implementa el sistema operativo producirá un error al intentar iniciar el equipo de destino.

> [!NOTE]  
> El Asistente para crear medio de secuencia de tareas establece la siguiente condición de variable de secuencia de tareas en el medio: **_SMSTSMediaType = OEMMedia**. Puede usar esta misma condición en la secuencia de tareas.  


## <a name="process"></a>Proceso

 > [!NOTE]  
 > En el caso de los entornos de PKI, puesto que la entidad de certificación raíz se especifica en el sitio principal, asegúrese de que los medios preconfigurados se crean en el sitio primario. El sitio de CAS no tiene la información de la entidad de certificación raíz para crear correctamente los medios preconfigurados.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear medio de secuencia de tareas**. Esta acción inicia el Asistente para crear medio de secuencia de tareas.  

3. En la página **Seleccionar tipo de medio**, especifique las siguientes opciones:  

    - Seleccione **Medio preconfigurado**.  

    - Opcionalmente, si quiere permitir solo que el sistema operativo se implemente sin requerir intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**.  

        > [!IMPORTANT]  
        > Cuando se selecciona esta opción, no se solicita al usuario que proporcione información de configuración de red ni que realice secuencias de tareas opcionales. Si se configura el medio para la protección con contraseña, se seguirá solicitando una contraseña al usuario.  

4. En la página **Administración de medio**, especifique una de las siguientes opciones:  

    - **Medio dinámico**: permite que un punto de administración redirija el medio a otro punto de administración, según la ubicación del cliente en los límites del sitio.  

    - **Medio basado en sitio**: el medio solo se pone en contacto con el punto de administración especificado.  

5. En la página **Propiedades de medio**, especifique la siguiente información:  

    - **Creado por**: especifique la persona que creó el medio.  

    - **Versión**: especifique el número de versión del medio.  

    - **Comentario**: escriba una descripción única del uso del medio.  

    - **Archivo multimedia**: especifique el nombre y la ruta de acceso de los archivos de salida. El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: `\\servername\folder\outputfile.wim`  

    - **Carpeta de almacenamiento provisional**:<!--1359388-->: el proceso de creación de medios puede requerir una gran cantidad de espacio en disco temporal. De forma predeterminada, esta ubicación es similar a la siguiente ruta de acceso: `%UserProfile%\AppData\Local\Temp`. A partir de la versión 1902, para ofrecer mayor flexibilidad con respecto al almacenamiento de estos archivos temporales, cambie este valor a otra unidad y ruta de acceso.  

6. En la página **Seguridad**, especifique las siguientes opciones:  

    - **Habilitar compatibilidad de equipos desconocida**: permite que el medio implemente un sistema operativo en un equipo que no esté administrado por Configuration Manager. No hay ningún registro de estos equipos en la base de datos de Configuration Manager. Para obtener más información, consulte [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos).  

    - **Proteger medio con contraseña:** : escriba una contraseña segura para ayudar a proteger el medio frente al acceso no autorizado. Cuando se especifica una contraseña, el usuario debe proporcionar esa contraseña para utilizar el medio preconfigurado.  

        > [!IMPORTANT]  
        > Por motivos de seguridad, asigne siempre una contraseña para ayudar a proteger el medio preconfigurado.  
 
    - Para las comunicaciones HTTP, seleccione **Crear certificado autofirmado de medio**. A continuación, especifique la fecha de inicio y expiración del certificado.  
    
        > [!NOTE] 
        > Si selecciona esta opción, los puntos de administración de HTTPS no estarán disponibles para su selección en la página **Imagen de arranque** de este asistente.

    - Para comunicaciones HTTPS, seleccione **Importar certificado PKI**. A continuación, especifique el certificado que desea importar y su contraseña.  

        Para más información sobre este certificado de cliente que se usa para imágenes de arranque, consulte [Requisitos de certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Afinidad entre usuario y dispositivo**: para admitir la administración centrada en el usuario en Configuration Manager, especifique cómo quiere que el medio asocie los usuarios con el equipo de destino. Para más información sobre cómo la implementación del sistema operativo admite la afinidad entre usuario y dispositivo, consulte [Asociación de usuario a un equipo de destino](../get-started/associate-users-with-a-destination-computer.md).  

        - **Permitir afinidad de dispositivo de usuario con autoaprobación**: el medio asocia automáticamente los usuarios al equipo de destino. Esta funcionalidad se basa en las acciones de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino cuando implementa el sistema operativo en el equipo de destino.  

        - **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador**: el medio asocia los usuarios al equipo de destino después de conceder la aprobación. Esta funcionalidad se basa en el ámbito de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino, pero espera la aprobación del usuario administrativo antes de implementar el sistema operativo.  

        - **No permitir afinidad de dispositivo de usuario**: el medio no asocia los usuarios con el equipo de destino. En este escenario, la secuencia de tareas no asocia los usuarios con el equipo de destino cuando se implementa el sistema operativo.  

7. En la página **Secuencia de tareas**, seleccione la secuencia de tareas que se ejecuta en el equipo de destino. Compruebe la lista de contenido al que hace referencia la secuencia de tareas.  

    - **Detectar dependencias de aplicación asociadas y agregarlas a este medio**: también agrega contenido a los medios para las dependencias de la aplicación.  

        > [!TIP]  
        > Si no ve las dependencias de aplicación esperadas, anule la selección y, a continuación, vuelva a seleccionar esta opción para actualizar la lista.  

8. En la página **Imagen de arranque**, especifique las opciones siguientes:  

    > [!IMPORTANT]  
    > La arquitectura de la imagen de arranque que se distribuye debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.  

    - **Imagen de arranque**: seleccione la imagen de arranque para iniciar el equipo de destino.  

    - **Punto de distribución**: seleccione el punto de distribución que tiene la imagen de arranque. El asistente recupera la imagen de arranque desde el punto de distribución y la escribe en el medio.  

        > [!NOTE]  
        > Su cuenta de usuario necesita al menos permisos de **Lectura** para la biblioteca de contenido en el punto de distribución.  

    - **Punto de administración**: solo para *medios basados en sitio*, seleccione un punto de administración desde un sitio primario.  

    - **Puntos de administración asociados**: solo para *medios dinámicos*, seleccione los puntos de administración de sitio primario para usar y un orden de prioridad para la comunicación inicial.  

        > [!NOTE]  
        > Los puntos de administración habilitados para HTTPS solo se mostrarán cuando se especifique un certificado PKI en la página **Seguridad** de este asistente.  

9. En la página **Imágenes**, especifique las siguientes opciones:  

    - **Paquete de imagen**: Especifique la imagen que debe usarse. Para más información, vea [Administrar imágenes de SO](../get-started/manage-operating-system-images.md).  

    - **Índice de imagen**: si el paquete contiene varias imágenes del sistema operativo, especifique el índice de la imagen que se implementará.  

    - **Punto de distribución**: especifique el punto de distribución que tiene el paquete de la imagen del sistema operativo. El asistente obtiene la imagen del sistema operativo del punto de distribución y la escribe en el medio.  

10. En la página **Seleccionar aplicación**, seleccione aplicaciones adicionales para agregar al archivo de medios preconfigurados.  

11. En la página **Seleccionar paquete**, seleccione paquetes adicionales para agregar al archivo de medios preconfigurados.  

12. En **Seleccionar el paquete de controladores**, seleccione los paquetes de controladores adicionales para agregar al archivo de medios preconfigurados.  

13. En la página **Puntos de distribución**, seleccione uno o varios puntos de distribución de los que obtener el contenido.  

    Configuration Manager solo muestra los puntos de distribución que incluyen el contenido. Antes de continuar, distribuya todo el contenido asociado a la secuencia de tareas en al menos un punto de distribución. Después de distribuir el contenido, actualice la lista de puntos de distribución. Quite los puntos de distribución ya haya seleccionado en esta página, vaya a la página anterior y después regrese a la página **Puntos de distribución**. O bien, reinicie al asistente. Para obtener más información, consulte [Distribuir contenido al que hace referencia una secuencia de tareas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) y [Administración del contenido y de la infraestructura de contenido](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. En la página **Personalización**, especifique las siguientes opciones:  

    - Agregue las variables que usa la secuencia de tareas.  

    - **Habilitar comando de preinicio**: Especifique los comandos de preinicio que desee ejecutar antes de que se ejecute la secuencia de tareas. Los comandos de preinicio son un script o un ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas. Para obtener más información, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

        > [!TIP]  
        > Durante la creación de medios, la secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro **CreateTSMedia.log** en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

        Si el comando de preinicio necesita contenido, seleccione la opción **Incluir archivos para el comando de preinicio**.  

15. Complete el asistente.  


## <a name="next-steps"></a>Pasos siguientes

[Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
