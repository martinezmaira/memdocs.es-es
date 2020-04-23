---
title: Crear una secuencia de tareas para capturar un sistema operativo
titleSuffix: Configuration Manager
description: Una secuencia de tareas de generación y captura crea un equipo de referencia que puede incluir controladores concretos y actualizaciones de software junto con el sistema operativo.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707393"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Crear una secuencia de tareas para capturar un sistema operativo

*Se aplica a: Configuration Manager (rama actual)*

Al usar una secuencia de tareas para implementar un sistema operativo en un equipo en Configuration Manager, el equipo instala la imagen de sistema operativo que especifique en la secuencia de tareas. Puede personalizar la imagen de sistema operativo para que incluya controladores, aplicaciones y actualizaciones de software específicos. En primer lugar, use una secuencia de tareas de generación y captura para crear un equipo de referencia. Después, capture la imagen de sistema operativo de ese equipo de referencia. Si ya tiene un equipo de referencia disponible para capturar, cree una secuencia de tareas personalizada para capturar el sistema operativo.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a> Acerca de la secuencia de tareas de generación y captura

La secuencia de tareas de generación y captura:

- Crea particiones y formatea el equipo de referencia
- Instala el sistema operativo
- Instala el cliente de Configuration Manager
- Instala aplicaciones
- Aplica actualizaciones de software
- Captura el sistema operativo del equipo de referencia

Los paquetes asociados a la secuencia de tareas, como las aplicaciones, deben estar disponibles en los puntos de distribución antes de implementar la secuencia de tareas de generación y captura.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a> Requisitos

Antes de crear una secuencia de tareas para instalar un sistema operativo, asegúrese de que se han implementado los siguientes componentes:  

### <a name="required"></a>Requerido

- [Imagen de arranque](../get-started/manage-boot-images.md)

- [Imagen del sistema operativo](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Necesario (si se usa)

- [Paquetes de controladores](../get-started/manage-drivers.md) que contengan los controladores de Windows necesarios para admitir el hardware en el equipo de referencia. Para más información sobre los pasos de la secuencia de tareas para administrar controladores, vea [Use task sequences to install device drivers (Usar secuencias de tareas para instalar controladores de dispositivos)](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Actualizaciones de software](../../sum/get-started/synchronize-software-updates.md)

- [Aplicaciones](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Crear una secuencia de tareas de generación y captura

Use el siguiente procedimiento a fin de emplear una secuencia de tareas para crear un equipo de referencia y capturar el sistema operativo.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

1. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

1. En la página **Crear una nueva secuencia de tareas** , seleccione **Generar y capturar una imagen de sistema operativo de referencia**.  

1. En la página **Información de secuencia de tareas**, especifique la siguiente configuración:  

    - **Nombre de la secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    - **Descripción**: Especifique una descripción opcional para la secuencia de tareas. Por ejemplo, describa el sistema operativo que crea la secuencia de tareas.

    - **Imagen de arranque**: Especifique la imagen de arranque que se va a usar con esta secuencia de tareas.  

        > [!IMPORTANT]  
        > La arquitectura de la imagen de arranque debe ser compatible con la arquitectura de hardware del equipo de destino.  

1. En la página **Instalar Windows**, especifique la siguiente configuración:  

    - **Paquete de imagen**: Especifique el paquete de imágenes del sistema operativo, que contiene los archivos necesarios para instalar el sistema operativo.  

    - **Índice de imagen**: Especifique el índice del sistema operativo que se va a instalar en la imagen. Si la imagen del sistema operativo contiene varias versiones, seleccione la que quiere instalar.  

    - **Clave de producto**: Si es necesario, especifique la clave de producto del sistema operativo Windows que se va a instalar. Puede especificar claves de licencia por volumen codificadas y claves de producto estándar. Si usa una clave de producto no codificada, separe cada grupo de cinco caracteres con un guion (`-`). Por ejemplo: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Modo de licencia de servidor**: si es necesario, especifique que la licencia de servidor es **Por puesto**, **Por servidor**, o bien que no se especifica ninguna licencia. Si la licencia de servidor es **Por servidor**, especifique también el número máximo de conexiones de servidor.  

    - Especifique cómo se debe configurar la cuenta de administrador del sistema operativo implementado:  

        - **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas**: Cree una contraseña aleatoria para la cuenta de administrador local. Deshabilite la cuenta cuando se haya configurado Windows.

        - **Habilitar la cuenta y especificar la contraseña de administrador local**: Use la misma contraseña para la cuenta de administrador local en todos los equipos en los que implemente este sistema operativo.

1. En la página **Configurar red**, especifique la siguiente configuración:

    - **Unirse a un grupo de trabajo**: especifique si quiere agregar el equipo de destino a un grupo de trabajo cuando se implemente el sistema operativo.  

    - **Unirse a un dominio**: especifique si quiere agregar el equipo de destino a un dominio cuando se implemente el sistema operativo. En **Dominio**, especifique el nombre del dominio.  

        > [!IMPORTANT]  
        > Puede examinar para localizar los dominios del bosque local. Especifique el nombre de dominio para un bosque remoto.

        También puede especificar una unidad organizativa (OU). Este valor es opcional y especifica el nombre distintivo LDAP X.500 de la unidad organizativa en la que se va a crear la cuenta de equipo, si aún no existe.  

    - **Cuenta**: especifique el nombre de usuario y la contraseña de la cuenta que tenga permisos para unirse al dominio especificado. Por ejemplo, `domain\user` o `%variable%`.  

        > [!IMPORTANT]  
        > Si planea migrar la configuración del dominio o la configuración del grupo de trabajo durante la implementación, asegúrese de introducir aquí las credenciales de dominio adecuadas.  

1. En la página **Instalar Configuration Manager**, especifique el paquete de cliente de Configuration Manager. Este paquete contiene los archivos de código fuente necesarios para instalar el cliente de Configuration Manager. Especifique también las propiedades adicionales necesarias para instalar el cliente.  

    Para obtener más información, vea [Información sobre las propiedades de instalación de clientes](../../core/clients/deploy/about-client-installation-properties.md).

1. En la página **Incluir actualizaciones**, especifique si desea instalar las actualizaciones de software necesarias, todas las actualizaciones de software o ninguna. Si especifica que se instalen las actualizaciones de software, Configuration Manager instala solo las que se destinan a las colecciones a las que pertenece el equipo de destino.  

1. En la página **Instalar aplicaciones**, especifique las aplicaciones que desee instalar en el equipo de destino. Si especifica varias aplicaciones, también puede especificar que la secuencia de tareas continúe si se produce un error en la instalación de una aplicación específica.  

    > [!NOTE]
    > Luego se muestra la página **Preparación del sistema** en el asistente, pero ya no se usa. Seleccione **Siguiente** para continuar.

1. En la página **Propiedades de imagen**, especifique los valores siguientes para la imagen de sistema operativo:

    - **Creado por**: Especifique el nombre del usuario que se debe anotar como creador de la imagen del sistema operativo.  

    - **Versión**: Especifique el número de versión asociado a la imagen de sistema operativo. No es necesario que este atributo sea la versión del sistema operativo, ya que el sitio almacena ese valor por separado.

    - **Descripción**: Especifique la descripción de la imagen del sistema operativo.  

1. En la página **Capturar imagen**, especifique la siguiente configuración:

    - **Ruta de acceso**: Especifique una carpeta de red compartida donde Configuration Manager deba almacenar el archivo de imagen de salida (.wim). Este archivo contiene la imagen de sistema operativo que se basa en la configuración que especifique en este asistente. Si especifica una carpeta que contenga un archivo .WIM, se sobrescribirá.  

    - **Cuenta**: especifique la cuenta de Windows que tenga permisos para el recurso compartido de red donde se almacena la imagen.  

1. Complete el asistente.  

Para agregar pasos adicionales a la secuencia de tareas, selecciónela y elija **Editar**. Para obtener más información sobre cómo editar una secuencia de tareas, vea [Uso del editor de secuencias de tareas](../understand/task-sequence-editor.md).  

Implemente la secuencia de tareas en un equipo de referencia según una de las maneras siguientes:  

- Si el equipo de referencia ya es un cliente de Configuration Manager, implemente la secuencia de tareas de generación y captura en una colección que contenga el equipo de referencia. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

- Si el equipo de referencia no es un cliente de Configuration Manager o si quiere ejecutar manualmente la secuencia de tareas en el equipo de referencia, use el **Asistente para crear medio de secuencia de tareas** para crear un medio de arranque. Para obtener más información, consulte [Crear medios de arranque](create-bootable-media.md).  

Después de capturar la imagen, puede implementarla en otros equipos. Para obtener más información sobre cómo implementar la imagen capturada de sistema operativo, vea [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a> Capturar desde un equipo de referencia existente

Si ya tiene un equipo de referencia listo para capturar, cree una secuencia de tareas que solo capture el sistema operativo del equipo de referencia. Use el paso de la secuencia de tareas **Capturar imagen de sistema operativo** para capturar una o más imágenes de un equipo de referencia y almacenarlas en un archivo de imagen (.wim) en el recurso compartido de red especificado. Inicie el equipo de referencia en Windows PE con una imagen de arranque. La secuencia de tareas captura cada unidad de disco duro del equipo de referencia como una imagen independiente en el archivo .wim. Si el equipo al que se hace referencia tiene varias unidades, el archivo .wim resultante contiene una imagen independiente para cada volumen. Solo captura los volúmenes con formato NTFS o FAT32. Omite los volúmenes con otros formatos o los volúmenes USB.  

Use el procedimiento siguiente para capturar una imagen de sistema operativo de un equipo de referencia existente:

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear secuencia de tareas**. Esta acción inicia el Asistente para crear secuencia de tareas.  

1. En la página **Crear una nueva secuencia de tareas** , seleccione **Crear una nueva secuencia de tareas personalizada**.  

1. En la página **Información de secuencia de tareas**, especifique un nombre para la secuencia de tareas. Si lo desea, agregue una descripción para la secuencia de tareas.  

1. Especifique una imagen de arranque para la secuencia de tareas. Configuration Manager usa esta imagen de arranque para iniciar el equipo de referencia con Windows PE. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

1. Complete el asistente.  

1. En el nodo **Secuencias de tareas**, seleccione la nueva secuencia de tareas. En la pestaña **Inicio** de la cinta, en el grupo **Secuencia de tareas**, seleccione **Editar**. Esta acción abre el editor de secuencia de tareas.  

1. Si el cliente de Configuration Manager está instalado en el equipo de referencia:

    Vaya al menú **Agregar**, seleccione **Imágenes** y, a continuación, elija [Preparar el cliente de Configuration Manager para la captura](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Este paso generaliza el cliente de Configuration Manager en el equipo de referencia.

    > [!Note]  
    > La secuencia de tareas no admite la desinstalación del cliente de Configuration Manager.

1. Vaya al menú **Agregar**, seleccione **Imágenes** y elija [Preparar Windows para la captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Este paso ejecuta Sysprep y luego reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas. Para que esta acción se lleve a cabo correctamente, no debe unir el equipo de referencia a un dominio.

1. Vaya al menú **Agregar**, seleccione **Imágenes** y elija [Capturar imagen de sistema operativo](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage). Este paso solo se ejecuta desde Windows PE para capturar las unidades de disco duro del equipo de referencia. Configure las siguientes opciones:

    - **Nombre** y **Descripción**: opcionalmente, puede cambiar el nombre del paso de la secuencia de tareas y proporcionar una descripción.  

    - **Destino**: especifique una carpeta de red compartida donde se guardará el archivo .WIM. Este archivo contiene la imagen de sistema operativo basada en la configuración que especifique en este asistente. Si especifica una carpeta que contenga un archivo .WIM, se sobrescribirá.  

    - **Descripción**, **Versión** y **Creado por**: opcionalmente, proporcione detalles sobre la imagen que se va a capturar.  

    - **Cuenta de captura de imagen del sistema operativo**: especifique la cuenta de Windows que tenga permisos en el recurso compartido de red que haya especificado. Seleccione **Establecer** para especificar el nombre de esa cuenta de Windows.  

Seleccione **Aceptar** para guardar los cambios y cerrar el editor de secuencia de tareas.  

Implemente la secuencia de tareas en un equipo de referencia según una de las maneras siguientes:  

- Si el equipo de referencia ya es un cliente de Configuration Manager, implemente la secuencia de tareas de captura en una colección que contenga el equipo de referencia. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

- Si el equipo de referencia no es un cliente de Configuration Manager o si quiere ejecutar manualmente la secuencia de tareas en el equipo de referencia, use el **Asistente para crear medio de secuencia de tareas** para crear un medio de captura. Para obtener más información, consulte [Create capture media](create-capture-media.md) (Crear medios de captura).  

Después de capturar la imagen, puede implementarla en otros equipos. Para obtener más información sobre cómo implementar la imagen capturada de sistema operativo, vea [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a> Secuencia de tareas de ejemplo

Use la tabla siguiente como guía para crear una secuencia de tareas que genere y capture una imagen de sistema operativo. La tabla ayuda a decidir la secuencia general de los pasos de la secuencia de tareas y cómo organizar y estructurar esos pasos en grupos lógicos. La secuencia de tareas que cree puede variar con respecto a este ejemplo. Puede contener más o menos pasos y grupos.

> [!NOTE]  
> Siempre use el Asistente para crear secuencia de tareas para crear este tipo de secuencia de tareas.
>
> El asistente agrega pasos a la secuencia de tareas con nombres un poco diferentes a los que vería si agregara los mismos pasos manualmente.

### <a name="group-build-the-reference-machine"></a>Grupo: Generar el equipo de referencia

Este grupo contiene las acciones necesarias para generar un equipo de referencia.

|Paso de secuencia de tareas|Descripción|  
|-------------------------------|---------------|  
|**Reiniciar en Windows PE**|Reinicie el equipo de destino en la imagen de arranque asignada a la secuencia de tareas. Este paso muestra un mensaje al usuario que indica que el equipo se va a reiniciar para que pueda continuar la instalación.<br /><br />Este paso usa la variable de la secuencia de tareas `_SMSTSInWinPE` de solo lectura. Si el valor asociado es igual a `false`, el paso de la secuencia de tareas continúa.|
|**Disco de partición 0 - BIOS**|Cree particiones y formatee el disco duro del equipo de destino en modo BIOS. El número de disco predeterminado es `0`.<br /><br />Este paso usa varias variables de la secuencia de tareas de solo lectura. Por ejemplo, solo se ejecuta si la memoria caché del cliente de Configuration Manager no existe y no se ejecuta si el equipo está configurado para UEFI.|
|**Disco de partición 0 - UEFI**|Cree particiones y formatee el disco duro del equipo de destino en modo UEFI. El número de disco predeterminado es `0`.<br /><br />Este paso usa varias variables de la secuencia de tareas de solo lectura. Por ejemplo, solo se ejecuta si la memoria caché del cliente de Configuration Manager no existe y solo se ejecuta si el equipo está configurado para UEFI.|
|**Aplicar el sistema operativo**|Instale la imagen de sistema operativo especificada en el equipo de destino. Este paso primero elimina todos los archivos del volumen, salvo los archivos de control específicos de Configuration Manager. A continuación, aplica todas las imágenes de volumen incluidas en el archivo WIM al volumen de disco secuencial correspondiente en el equipo de destino.|
|**Aplicar configuraciones de Windows**|Configure las opciones de Windows para el equipo de destino.|
|**Aplicar configuración de red**|Especifique la información de configuración del grupo de trabajo o la red para el equipo de destino.|
|**Aplicar controladores del dispositivo**|Haga coincidir e instale controladores como parte de esta implementación del sistema operativo. Para obtener más información, consulte [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />Este paso usa la variable de la secuencia de tareas `_SMSTSMediaType` de solo lectura. Si el valor asociado no es igual a `FullMedia`, este paso no se ejecutará.|
|**Instalar Windows y Configuration Manager**|Instale el software cliente de Configuration Manager. Configuration Manager instala y registra el GUID del cliente de Configuration Manager. Incluya las **propiedades de instalación** necesarias.|
|**Instalar actualizaciones**|Especifique cómo se deben instalar las actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso. En ese momento, la evaluación es similar a cualquier otro cliente administrado por Configuration Manager. Para obtener más información, consulte [Instalar actualizaciones de software](../understand/install-software-updates.md).<br /><br />Este paso usa la variable de la secuencia de tareas `_SMSTSMediaType` de solo lectura. Si el valor asociado no es igual a `FullMedia`, este paso no se ejecutará.|
|**Instalar aplicaciones**|Especifica las aplicaciones que se deben instalar en el equipo de referencia.|

### <a name="group-capture-the-reference-machine"></a>Grupo: Capturar el equipo de referencia

Este grupo contiene los pasos necesarios para preparar y capturar un equipo de referencia.

|Paso de secuencia de tareas|Descripción|  
|-------------------------------|---------------|  
|**Preparar cliente de Configuration Manager**|Generalice el cliente de Configuration Manager en el equipo de referencia.|
|**Preparar sistema operativo**|Ejecuta Sysprep para generalizar Windows. Luego reinicia el equipo en la imagen de arranque de Windows PE especificada para la secuencia de tareas.|
|**Capturar el equipo de referencia**|Captura la imagen en el recurso compartido de red especificado y en el archivo .WIM.|

> [!IMPORTANT]
> Después de capturar una imagen desde un equipo de referencia, no capture otra imagen de sistema operativo desde ese equipo. Durante la configuración inicial se crean entradas del registro. Cree un nuevo equipo de referencia cada vez que capture una imagen del sistema operativo. Si tiene previsto usar el mismo equipo de referencia para crear futuras imágenes del sistema operativo, primero debe desinstalar y volver a instalar el cliente de Configuration Manager.

## <a name="next-steps"></a>Pasos siguientes

[Métodos para implementar sistemas operativos de empresa](methods-to-deploy-enterprise-operating-systems.md)
