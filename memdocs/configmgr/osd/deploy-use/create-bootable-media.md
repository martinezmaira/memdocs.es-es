---
title: Crear medios de arranque
titleSuffix: Configuration Manager
description: Use los medios de arranque de Configuration Manager para instalar una nueva versión de Windows o reemplazar un equipo.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c570fc2844093b190e388727dd3799bcbcdb92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694903"
---
# <a name="create-bootable-media"></a>Crear medios de arranque

*Se aplica a: Configuration Manager (rama actual)*

Los medios de arranque de Configuration Manager contienen la imagen de arranque, comandos de preinicio y archivos asociados opcionales y archivos de Configuration Manager. Use los medios preconfigurados para los siguientes escenarios de implementación del sistema operativo:  

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

- [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)  


## <a name="usage"></a>Uso

Al arrancar en medios de arranque, se produce el siguiente proceso:

1. Se inicia el equipo de destino
1. Se conecta a la red
1. Recupera el siguiente contenido del sitio:
    - La secuencia de tareas especificada
    - Imagen del sistema operativo
    - Cualquier otro contenido necesario

Dado que la secuencia de tareas no está en el medio, puede cambiar la secuencia de tareas o el contenido sin tener que volver a crear el medio.

Los paquetes en el medio de arranque no están cifrados. Para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados, adopte las medidas de seguridad adecuadas. Por ejemplo, agregue una contraseña al medio.

## <a name="prerequisites"></a>Requisitos previos

Antes de crear medios de arranque con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:

### <a name="boot-image"></a>Imagen de arranque

Tenga en cuenta los siguientes puntos sobre la imagen de arranque que usará en la secuencia de tareas para implementar el sistema operativo:

- La arquitectura de la imagen de arranque debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.
- Asegúrese de que la imagen de arranque contenga los controladores de almacenamiento y red necesarios para aprovisionar el equipo de destino.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creación de una secuencia de tareas para implementar un sistema operativo

Como parte del medio de arranque, especifique la secuencia de tareas para implementar el sistema operativo. Para más información, consulte [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo el contenido asociado con la secuencia de tareas

Distribuya todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Este contenido incluye la imagen de arranque y otros archivos de preinicio asociados. El asistente recopila la información del punto de distribución al crear los medios de arranque.

Su cuenta de usuario necesita al menos acceso de **Lectura** a la biblioteca de contenido en ese punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar la unidad USB extraíble

Si usa una unidad USB extraíble, conéctela al equipo donde se ejecuta el Asistente para crear medio de secuencia de tareas. Windows debe identificar la unidad USB como un dispositivo extraíble. El asistente escribe directamente en la unidad extraíble cuando crea los medios.

### <a name="create-an-output-folder"></a>Crear una carpeta de salida

Antes de ejecutar el Asistente para crear medio de secuencia de tareas para crear medios para un conjunto de CD o DVD, cree una carpeta para los archivos de salida que se crean. Los medios que se crean para un conjunto de CD o DVD se escriben como un archivo .ISO directamente en la carpeta.


## <a name="process"></a>Proceso

 > [!NOTE]  
 > En el caso de los entornos de PKI, puesto que la entidad de certificación raíz se especifica en el sitio principal, asegúrese de que los medios de arranque se crean en el sitio primario. El sitio de CAS no tiene la información de la entidad de certificación raíz para crear correctamente los medios de arranque.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear medio de secuencia de tareas**. Esta acción inicia el Asistente para crear medio de secuencia de tareas.  

3. En la página **Seleccionar tipo de medio**, especifique las siguientes opciones:  

    - Seleccione **Medio de arranque**.  

    - Opcionalmente, si quiere permitir solo que el sistema operativo se implemente sin requerir intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**.  

        > [!IMPORTANT]  
        > Cuando se selecciona esta opción, no se solicita al usuario que proporcione información de configuración de red ni que realice secuencias de tareas opcionales. Si se configura el medio para la protección con contraseña, se seguirá solicitando una contraseña al usuario.  

4. En la página **Administración de medio**, especifique una de las siguientes opciones:  

    - **Medio dinámico**: permite que un punto de administración redirija el medio a otro punto de administración, según la ubicación del cliente en los límites del sitio.  

    - **Medio basado en sitio**: el medio solo se pone en contacto con el punto de administración especificado.  

5. En la página **Tipo de medios**, especifique si el medio es una **unidad USB extraíble** o un **conjunto de CD/DVD**. Luego, configure las siguientes opciones:  

    > [!IMPORTANT]  
    > Los medios usan un sistema de archivos FAT32. No puede crear medios en una unidad USB cuyo contenido incluya un archivo de más de 4 GB de tamaño.  

    - Si selecciona **Unidad USB extraíble**, especifique dónde quiere almacenar el contenido.  

        - **Formatear la unidad USB extraíble (FAT32) y hacerla de arranque** : de forma predeterminada, permita que Configuration Manager prepare la unidad USB. Muchos de los nuevos dispositivos UEFI requieren una partición FAT32 de arranque. Sin embargo, este formato también limita el tamaño de los archivos y la capacidad total de la unidad. Si ya ha formateado y configurado la unidad extraíble, deshabilite esta opción.

    - Si selecciona **Conjunto de CD/DVD**, especifique la capacidad del medio (**Tamaño de medio**) y el nombre y la ruta de acceso del archivo de salida (**Archivo multimedia**). El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: `\\servername\folder\outputfile.iso`  

        Si la capacidad del medio es demasiado pequeña para almacenar todo el contenido, crea varios archivos. A continuación, deberá almacenar el contenido en varios CD o DVD. Si se requieren varios archivos multimedia, Configuration Manager agrega un número de secuencia al nombre de cada archivo de salida que crea.  

        > [!IMPORTANT]  
        > Si selecciona una imagen .iso existente, el Asistente para crear medio de secuencia de tareas elimina la imagen de la unidad o el recurso compartido cuando pasa a la siguiente página del asistente. Se elimina la imagen existente incluso si, a continuación, se cancela al asistente.  

    - **Carpeta de almacenamiento provisional**:<!--1359388-->: el proceso de creación de medios puede requerir una gran cantidad de espacio en disco temporal. De forma predeterminada, esta ubicación es similar a la siguiente ruta de acceso: `%UserProfile%\AppData\Local\Temp`. A partir de la versión 1902, para ofrecer mayor flexibilidad con respecto al almacenamiento de estos archivos temporales, cambie este valor a otra unidad y ruta de acceso.  

    - **Etiqueta de medio**:<!--1359388-->: a partir de la versión 1902, agregue una etiqueta al medio de secuencia de tareas. Esta etiqueta ayuda a identificar mejor el medio después de crearlo. El valor predeterminado es `Configuration Manager`. Este campo de texto aparece en las siguientes ubicaciones:  

        - Si monta un archivo ISO, Windows muestra esta etiqueta como el nombre de la unidad montada  

        - Si aplica formato a una unidad USB, usa los primeros 11 caracteres de la etiqueta como nombre  

        - Configuration Manager escribe un archivo de texto denominado `MediaLabel.txt` en la raíz del medio. De forma predeterminada, el archivo incluye una sola línea de texto: `label=Configuration Manager`. Si personaliza la etiqueta del medio, esta línea usa la etiqueta personalizada en lugar del valor predeterminado.  

    - **Incluir archivo autorun.inf en el medio**:<!-- 4090666 -->: a partir de la versión 1906, Configuration Manager no agrega un archivo autorun.inf de forma predeterminada. Normalmente, los productos antimalware bloquean este archivo. Para obtener más información sobre la característica de ejecución automática de Windows, vea [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (Creación de una aplicación de CD-ROM con ejecución automática habilitada). Si todavía lo necesita en su escenario, seleccione esta opción para incluir el archivo.  

6. En la página **Seguridad**, especifique las siguientes opciones:  

    - **Habilitar compatibilidad de equipos desconocida**: permite que el medio implemente un sistema operativo en un equipo que no esté administrado por Configuration Manager. No hay ningún registro de estos equipos en la base de datos de Configuration Manager. Para obtener más información, consulte [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos).  

    - **Proteger medio con contraseña:** : escriba una contraseña segura para ayudar a proteger el medio frente al acceso no autorizado. Al especificar una contraseña, el usuario debe proporcionar dicha contraseña para poder utilizar el medio de arranque.  

        > [!IMPORTANT]  
        > Por seguridad, se recomienda siempre asignar una contraseña para ayudar a proteger los medios de arranque.  

    - Para las comunicaciones HTTP, seleccione **Crear certificado autofirmado de medio**. A continuación, especifique la fecha de inicio y expiración del certificado.  
    
      > [!NOTE]  
      > Si selecciona esta opción, los puntos de administración de HTTPS no estarán disponibles para su selección en la página **Imagen de arranque** de este asistente.

    - Para comunicaciones HTTPS, seleccione **Importar certificado PKI**. A continuación, especifique el certificado que desea importar y su contraseña.  

        Para más información sobre este certificado de cliente que se usa para imágenes de arranque, consulte [Requisitos de certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Afinidad entre usuario y dispositivo**: para admitir la administración centrada en el usuario en Configuration Manager, especifique cómo quiere que el medio asocie los usuarios con el equipo de destino. Para más información sobre cómo la implementación del sistema operativo admite la afinidad entre usuario y dispositivo, consulte [Asociación de usuario a un equipo de destino](../get-started/associate-users-with-a-destination-computer.md).  

        - **Permitir afinidad de dispositivo de usuario con autoaprobación**: el medio asocia automáticamente los usuarios al equipo de destino. Esta funcionalidad se basa en las acciones de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino cuando implementa el sistema operativo en el equipo de destino.  

        - **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador**: el medio asocia los usuarios al equipo de destino después de conceder la aprobación. Esta funcionalidad se basa en el ámbito de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino, pero espera la aprobación del usuario administrativo antes de implementar el sistema operativo.  

        - **No permitir afinidad de dispositivo de usuario**: el medio no asocia los usuarios con el equipo de destino. En este escenario, la secuencia de tareas no asocia los usuarios con el equipo de destino cuando se implementa el sistema operativo.  

7. En la página **Imagen de arranque**, especifique las opciones siguientes:  

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

8. En la página **Personalización**, especifique las siguientes opciones:  

    - Agregue las variables que usa la secuencia de tareas.  

    - **Habilitar comando de preinicio**: Especifique los comandos de preinicio que desee ejecutar antes de que se ejecute la secuencia de tareas. Los comandos de preinicio son un script o un ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas. Para obtener más información, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

        > [!TIP]  
        > Durante la creación de medios, la secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro **CreateTSMedia.log** en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

        Si el comando de preinicio necesita contenido, seleccione la opción **Incluir archivos para el comando de preinicio**.  

9. Complete el asistente.  


## <a name="alternate-method"></a>Método alternativo

Puede crear medios de arranque en una unidad USB extraíble cuando la unidad no está conectada al equipo que ejecuta la consola de Configuration Manager.

1. [Crear el medio de arranque de secuencia de tareas](#process). En la página **Tipo de medio**, seleccione **Conjunto de CD/DVD**. El asistente escribe los archivos de salida en la ubicación que especifique. Por ejemplo: `\\servername\folder\outputfile.iso`.  

2. Prepare la unidad USB extraíble. Debe ser una unidad de con formato, vacía y de arranque.

3. Monte la imagen ISO desde la ubicación del recurso compartido y transfiera los archivos desde la imagen ISO a la unidad USB.


## <a name="next-steps"></a>Pasos siguientes

[Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  
