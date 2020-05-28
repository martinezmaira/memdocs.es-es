---
title: Ampliación del inventario de hardware
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo ampliar el inventario de hardware en Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427736"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Cómo ampliar el inventario de hardware en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

El inventario de hardware lee información de equipos Windows mediante Instrumental de administración de Windows (WMI). WMI es la implementación de Microsoft de Web-Based Enterprise Management (WBEM), un estándar de la industria para acceder a información de administración en una empresa. En versiones anteriores de Configuration Manager, se ampliaba el inventario de hardware modificando el archivo sms_def.mof del servidor de sitio. Este archivo contenía una lista de clases WMI que el inventario de hardware podía leer. Al editar este archivo, se podían habilitar y deshabilitar las clases existentes y también crear clases de inventario.  

El archivo Configuration.mof se usa para definir las clases de datos que se deben inventariar mediante el inventario de hardware en el cliente y no se ha cambiado desde Configuration Manager 2012. Puede crear clases de datos para inventariar clases de datos de repositorios WMI existentes o personalizadas, o claves del Registro que estén en los sistemas cliente.  

 El archivo Configuration.mof también define y registra los proveedores WMI que tienen acceso a información del dispositivo durante el inventario de hardware. Registrar proveedores define el tipo de proveedor que se usará y las clases que admite el proveedor.  

 Cuando los clientes de Configuration Manager solicitan la directiva, se adjunta Configuration.mof al cuerpo de la directiva. Este archivo, a continuación, se descarga y se compilan los clientes. Al agregar, modificar o eliminar clases de datos en el archivo Configuration.mof, los clientes compilación automáticamente estos cambios realizados en las clases de datos relacionadas con el inventario. No es necesario hacer nada más para inventariar clases de datos nuevas o modificadas en los clientes de Configuration Manager. Este archivo se encuentra en **<Ubicación de instalación de CM\>\Inboxes\clifiles.src\hinv\\** en los servidores del sitio principal.  

 En Configuration Manager, ya no es necesario editar el archivo sms_def.mof como en Configuration Manager 2007. En su lugar, puede habilitar y deshabilitar clases WMI y agregar nuevas clases que el inventario de hardware deba recopilar mediante la configuración del cliente. Configuration Manager proporciona los siguientes métodos para ampliar el inventario de hardware.  

> [!NOTE]  
>  Si ha cambiado manualmente el archivo Configuration.mof para agregar clases de inventario personalizadas, estos cambios se sobrescribirán cuando actualice a la versión 1602. Para seguir usando las clases personalizadas después de actualizar, debe agregarlas a la sección "Added extensions" del archivo Configuration.mof después de actualizar a 1602.  
> Pero no se debe modificar todo lo anterior a esta sección, ya que estas secciones se reservan para que Configuration Manager las modifique. Encontrará una copia de seguridad del archivo Configuration.mof personalizado en:  
> **<Directorio de instalación de CM\>\data\hinvarchive\\** .  

## <a name="methods"></a>Métodos

### <a name="enable-or-disable"></a>Habilitar o deshabilitar

Habilite o deshabilite algunos de los atributos de una clase que ya existe en el cliente. Esta acción indica al agente de inventario de hardware que lo recopile en los clientes. Puede realizar esta acción en la configuración de cliente predeterminada o en la configuración de cliente de dispositivo personalizada. Para más información, consulte [Habilitar o deshabilitar las clases existentes de inventario](#BKMK_Enable).

### <a name="add"></a>Agregar

Si existe una clase WMI en el cliente que el sitio conoce, esta acción la incluye en el posible conjunto de clases de inventario de hardware. Puede agregar una nueva clase de inventario del espacio de nombres WMI de otro dispositivo. Esta acción solo está en la configuración de cliente predeterminada. Para más información, consulte [Adición de una nueva clase de inventario](#BKMK_Add).

### <a name="extend"></a>Extend

Agregue una nueva clase WMI al cliente. Para ampliar manualmente el inventario de hardware, edite configuration.mof en el sitio de primer nivel.<!-- SCCMDocs#1073 -->

Si la clase WMI todavía no existe en el cliente, debe ampliar el esquema WMI:

1. Edite el archivo configuration.mof en el sitio de primer nivel. Revise **dataldr.log** para ver que el sitio lo agrega.

1. Actualice la directiva en un cliente y espere a que la nueva clase se compile.

1. Utilice la configuración de cliente predeterminada para [Agregar](#add) la nueva clase al inventario de hardware. No tiene que habilitar esta clase en la configuración de cliente predeterminada. Puede luego habilitarla en una configuración de cliente de dispositivo personalizada.

### <a name="import-and-export"></a>Importación y exportación

Use la consola de Configuration Manager para importar y exportar archivos Managed Object Format (MOF) que contengan clases de inventario. Para más información, consulte [Importación de clases de inventario de hardware](#BKMK_Import) y [Exportación de clases de inventario de hardware](#BKMK_Export).

### <a name="create-noidmif-files"></a>Crear archivos NOIDMIF

Use archivos NOIDMIF para recopilar información sobre los dispositivos cliente que Configuration Manager no puede inventariar. Por ejemplo, recopile información del número de activo del dispositivo que solo existe como etiqueta en el dispositivo. Inventario NOIDMIF se asocia automáticamente con el dispositivo de cliente que se recopilaron de. Para más información, consulte [Crear archivos NOIDMIF](#BKMK_NOIDMIF).

### <a name="create-idmif-files"></a>Crear archivos IDMIF

Use archivos IDMIF para recopilar información sobre los activos de la organización que no están asociados a un cliente de Configuration Manager. Por ejemplo, proyectores, fotocopiadoras e impresoras de red. Para más información, consulte [Crear archivos IDMIF](#BKMK_IDMIF).

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimientos para ampliar el inventario de hardware

Estos procedimientos le ayudan a configurar la configuración predeterminada para el inventario de hardware y se aplican a todos los clientes en la jerarquía. Si quiere que esta configuración solo se aplique a algunos clientes, cree una configuración de dispositivo cliente personalizada y asígnela a una recopilación de clientes determinados. Para obtener más información, vea [Cómo configurar el cliente](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Habilitación o deshabilitación de clases de inventario existentes  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

1. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

1. En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

1. En la lista **Configuración de dispositivo**, seleccione **Establecer clases**.  

1. En el **clases de inventario de Hardware** diálogo cuadro, active o desactive las clases y propiedades de clase para recopilar el inventario de hardware. Puede expandir las clases para activar o desactivar las propiedades individuales dentro de esa clase. Utilice la **Buscar clases de inventario** campo para buscar clases individuales.  

    > [!IMPORTANT]  
    >  Cuando se agregan clases nuevas al inventario de hardware de Configuration Manager, aumentará el tamaño del archivo de inventario que se recopila y envía al servidor de sitio. Esto podría afectar negativamente al rendimiento de la red y el sitio de Configuration Manager. Habilitar sólo las clases de inventario que se van a recopilar.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Adición de una nueva clase de inventario  

Solo se pueden agregar clases de inventario desde el servidor de primer nivel de la jerarquía modificando la configuración predeterminada del cliente. Esta opción no está disponible al crear la configuración de dispositivo personalizada.

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

1. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

1. En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

1. En la lista **Configuración de dispositivo**, pulse **Establecer clases**.  

1. En el cuadro de diálogo **Clases de inventario de hardware**, pulse **Agregar**.  

1. En el cuadro de diálogo **Agregar clase de inventario de hardware**, seleccione **Conectar**.  

1. En el cuadro de diálogo **Conectar con Instrumental de administración de Windows (WMI)** , especifique el nombre del equipo desde el que se recuperarán las clases WMI y el espacio de nombres WMI que se usará para recuperar las clases. Si quiere recuperar todas las clases del espacio de nombres WMI que especificó, seleccione **Recursivo**. Si el equipo al que se conecta no es el equipo local, proporcione las credenciales de una cuenta que tenga permiso para acceder a WMI en el equipo remoto.

1. Pulse **Conectar**.  

1. En el cuadro de diálogo **Agregar clase de inventario de hardware**, en la lista **Clases de inventario**, seleccione las clases WMI que quiera agregar al inventario de hardware de Configuration Manager.  

1. Si quiere modificar la información sobre la clase WMI seleccionada, seleccione **Editar**, y en el cuadro de diálogo **Calificadores de clase**, proporcione la siguiente información:  

    - **Nombre para mostrar**: este nombre se mostrará en el Explorador de recursos.  

    - **Propiedades**: especifique las unidades en las que se mostrará cada una de las propiedades de la clase WMI.  

      También puede establecer propiedades como propiedad de clave para ayudar a identificar de forma única cada instancia de la clase. Si se ha definido ninguna clave para la clase y se informa de varias instancias de la clase de cliente, se almacena sólo la instancia más reciente que se encuentra en la base de datos.  

      Cuando haya terminado de configurar las propiedades, seleccione **Aceptar** para cerrar el cuadro de diálogo **Calificadores de clase** y los demás cuadros de diálogo abiertos.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Importación de clases de inventario de hardware

Sólo puede importar las clases de inventario cuando se modifica la configuración predeterminada del cliente. Pero se puede usar la configuración de cliente personalizada para importar información que no incluya un cambio de esquema, como el cambio de la propiedad de una clase existente de **True** a **False**.  

1. En la consola de Configuration Manager, elija **Administración** >  **Configuración de cliente** > **Configuración de cliente predeterminada**.

1. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

1. En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

1. En la lista **Configuración de dispositivo**, pulse **Establecer clases**.  

1. En el cuadro de diálogo **Clases de inventario de hardware**, pulse **Importar**.  

1. En el cuadro de diálogo **Importar**, seleccione el archivo Managed Object Format (MOF) que quiere importar y, después, pulse **Aceptar**. Revise los elementos que se van a importar y, después, seleccione **Importar**.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Exportación de clases de inventario de hardware  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

1. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

1. En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

1. En la lista **Configuración de dispositivo**, pulse **Establecer clases**.  

1. En el cuadro de diálogo **Clases de inventario de hardware**, pulse **Exportar**.  

    > [!NOTE]  
    > Cuando se exportan las clases, se exportan todas las clases actualmente seleccionadas.  

1. En el cuadro de diálogo **Exportar**, especifique el archivo Managed Object Format (MOF) en el que quiere exportar las clases y, luego, pulse **Guardar**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a> Configurar el inventario de hardware para recopilar cadenas de más de 255 caracteres

Puede especificar la longitud de las cadenas de modo que tengan más de 255 caracteres para las propiedades del inventario de hardware. Esta acción se aplica únicamente a las clases recién agregadas y a las propiedades de inventario del hardware que no son claves. <!-- 1357389 -->

1. En el área de trabajo **Administración**, seleccione **Configuración de cliente**. Elija una opción de dispositivo de cliente que quiera editar y luego seleccione **Propiedades**.

1. Seleccione **Inventario de hardware**, después **Establecer clases** y haga clic en **Agregar**.

1. Seleccione **Conectar**.

1. Rellene **Nombre de equipo** y **Espacio de nombres WMI**, y seleccione **Recurrente** si es necesario. Proporcione las credenciales si es necesario para conectarse. Seleccione **Conectar** para ver las clases del espacio de nombres.

1. Elija una nueva clase y después seleccione **Editar**.

1. Cambie la **Longitud** de la propiedad que sea una cadena, que no sea la clave, para que sea mayor de 255. Seleccione **Aceptar**.

1. Asegúrese de que esté seleccionada la propiedad modificada para **Agregar clase de inventario de hardware** y seleccione **Aceptar**.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>Uso de archivos MFI para ampliar el inventario de hardware

Use archivos MIF para ampliar la información de inventario de hardware que Configuration Manager ha recopilado de los clientes. Durante el inventario de hardware, la información almacenada en los archivos MIF se agrega al informe de inventario de cliente y almacenada en la base de datos del sitio, donde puede usar los datos de la misma forma que utilice datos de inventario de cliente predeterminada. Existen dos tipos de archivos MFI: NOIDMIF e IDMIF.

> [!IMPORTANT]  
> Para poder agregar información de archivos MIF a la base de datos de Configuration Manager, primero debe crear o importar la información de clase para ellos. Para obtener más información, vea las secciones [Cómo agregar una clase de inventario nueva](#BKMK_Add) y [Cómo importar clases de inventario de hardware](#BKMK_Import) de este artículo.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Creación de archivos NOIDMIF

Los archivos NOIDMIF se pueden usar para agregar información a un inventario de hardware de cliente que normalmente Configuration Manager no puede recopilar y está asociado a un dispositivo de cliente concreto. Por ejemplo, muchas empresas etiquetan a cada equipo de la organización con un número de activo y, después, catalogan estos números de forma manual. Cuando se crea un archivo NOIDMIF, esta información puede agregarse a la base de datos de Configuration Manager y se usa para consultas e informes. Para obtener información sobre la creación de archivos NOIDMIF, consulte la documentación del SDK de Configuration Manager.  

> [!IMPORTANT]  
> Cuando se crea un archivo NOIDMIF, se debe guardar en un formato codificado de ANSI. Configuration Manager no puede leer los archivos NOIDMIF guardados en un formato con codificación UTF-8.  

Después de crear un archivo NOIDMIF, almacénelo en la carpeta `%Windir%\CCM\Inventory\Noidmifs` de cada cliente. Configuration Manager recopila información de los archivos NODMIF en esta carpeta durante el siguiente ciclo de inventario de hardware programado.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a> Creación de archivos IDMIF

Los archivos IDMIF se pueden usar para agregar información sobre activos que Configuration Manager no podría inventariar normalmente, y que no están asociados a un dispositivo cliente determinado, a la base de datos de Configuration Manager. Por ejemplo, se podría usar IDMIFS para recopilar información sobre proyectores, reproductores de DVD, fotocopiadoras u otros equipos que no tienen un cliente de Configuration Manager. Para obtener información sobre la creación de archivos IDMIF, consulte la documentación del SDK de Configuration Manager.  

Después de crear un archivo IDMIF, almacénelo en la carpeta `%Windir%\CCM\Inventory\Idmifs` de los equipos cliente. Configuration Manager recopila información de este archivo durante el siguiente ciclo de inventario de hardware programado. Declare nuevas clases para la información contenida en el archivo agregándolas o importándolas.  

> [!NOTE]
> Los archivos MIF podrían contener grandes cantidades de datos y la recopilación de estos datos podría afectar negativamente al rendimiento del sitio. Habilite la recopilación de archivos MIF solo cuando sea necesario y configure la opción **Tamaño de archivo MIF personalizado máximo (KB)** en la configuración del inventario de hardware. Para obtener más información, vea [Introducción al inventario de hardware](introduction-to-hardware-inventory.md).
