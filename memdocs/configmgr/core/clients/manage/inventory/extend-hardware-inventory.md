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
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695423"
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

|Método|Más información|  
|------------|----------------------|  
|Habilitar o deshabilitar las clases existentes de inventario|Habilite o deshabilite las clases de inventario predeterminadas o cree una configuración de cliente personalizada que le permita recopilar diferentes clases de inventario de hardware de recopilaciones de clientes especificadas. Vea el procedimiento [Cómo habilitar o deshabilitar clases de inventario existentes](#BKMK_Enable) de este artículo.|  
|Agregue una nueva clase de inventario|Agregue una nueva clase de inventario del espacio de nombres WMI de otro dispositivo. Vea el procedimiento [Cómo agregar una clase de inventario nueva](#BKMK_Add) de este artículo.|  
|Importar y exportar las clases de inventario de hardware|Importe y exporte archivos Managed Object Format (MOF) que contengan clases de inventario de la consola de Configuration Manager. Vea los procedimientos [Cómo importar clases de inventario de hardware](#BKMK_Import) y [Cómo exportar clases de inventario de hardware](#BKMK_Export) de este artículo.|  
|Crear archivos NOIDMIF|Use archivos NOIDMIF para recopilar información sobre los dispositivos cliente que Configuration Manager no puede inventariar. Por ejemplo, podría desea recopilar información número de dispositivos activos que sólo existe como una etiqueta en el dispositivo. Inventario NOIDMIF se asocia automáticamente con el dispositivo de cliente que se recopilaron de. Vea [Cómo crear los archivos NOIDMIF](#BKMK_NOIDMIF) en este artículo.|  
|Crear archivos IDMIF|Use archivos IDMIF para recopilar información sobre los activos de la organización que no están asociados con un cliente de Configuration Manager, por ejemplo, proyectores, fotocopiadoras e impresoras de red. Vea [Cómo crear los archivos IDMIF](#BKMK_IDMIF) en este artículo.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimientos para ampliar el inventario de hardware  
Estos procedimientos le ayudan a configurar la configuración predeterminada para el inventario de hardware y se aplican a todos los clientes en la jerarquía. Si quiere que esta configuración solo se aplique a algunos clientes, cree una configuración de dispositivo cliente personalizada y asígnela a una recopilación de clientes determinados. Vea [Cómo establecer la configuración del cliente](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Cómo habilitar o deshabilitar clases de inventario existentes  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

6.  En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  

7.  En el **clases de inventario de Hardware** diálogo cuadro, active o desactive las clases y propiedades de clase para recopilar el inventario de hardware. Puede expandir las clases para activar o desactivar las propiedades individuales dentro de esa clase. Utilice la **Buscar clases de inventario** campo para buscar clases individuales.  

    > [!IMPORTANT]  
    >  Cuando se agregan clases nuevas al inventario de hardware de Configuration Manager, aumentará el tamaño del archivo de inventario que se recopila y envía al servidor de sitio. Esto podría afectar negativamente al rendimiento de la red y el sitio de Configuration Manager. Habilitar sólo las clases de inventario que se van a recopilar.  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Cómo agregar una clase de inventario nueva  

Solo se pueden agregar clases de inventario desde el servidor de nivel superior en la jerarquía modificando la configuración predeterminada del cliente. Esta opción no está disponible al crear la configuración de dispositivo personalizado.

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

2. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

3. En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

4. En la lista **Configuración de dispositivo**, pulse **Establecer clases**.  

5. En el cuadro de diálogo **Clases de inventario de hardware**, pulse **Agregar**.  

6. En el **Agregar clase de inventario de Hardware** cuadro de diálogo, haga clic en **Conectar**.  

7. En el **Conectar a Windows Management Instrumentation (WMI)** cuadro de diálogo, especifique el nombre del equipo desde el que se recuperarán las clases WMI y el espacio de nombres WMI para recuperar las clases. Si desea recuperar todas las clases debajo del espacio de nombres WMI que especificó, haga clic en **recursiva**. Si el equipo a que se conecta no es el equipo local, proporcione las credenciales de inicio de sesión de una cuenta que tenga permiso para obtener acceso a WMI en el equipo remoto.  

8. Pulse **Conectar**.  

9. En el cuadro de diálogo **Agregar clase de inventario de hardware**, en la lista **Clases de inventario**, seleccione las clases WMI que quiera agregar al inventario de hardware de Configuration Manager.  

10. Si quiere modificar la información sobre la clase WMI seleccionada, seleccione **Editar**, y en el cuadro de diálogo **Calificadores de clase**, proporcione la siguiente información:  

    - **Nombre para mostrar**: este nombre se mostrará en el Explorador de recursos.  

    - **Propiedades**: especifique las unidades en las que se mostrará cada una de las propiedades de la clase WMI.  

      También puede designar propiedades como una propiedad de clave para ayudar a identificar de forma única cada instancia de la clase. Si se ha definido ninguna clave para la clase y se informa de varias instancias de la clase de cliente, se almacena sólo la instancia más reciente que se encuentra en la base de datos.  

      Cuando haya terminado de configurar las propiedades, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Calificadores de clase** y los demás cuadros de diálogo abiertos. 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Cómo importar clases de inventario de hardware  

Sólo puede importar las clases de inventario cuando se modifica la configuración predeterminada del cliente. Pero se puede usar la configuración de cliente personalizada para importar información que no incluya un cambio de esquema, como el cambio de la propiedad de una clase existente de **True** a **False**.  

1.  En la consola de Configuration Manager, elija **Administración** >  **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

6.  En la lista **Configuración de dispositivo**, pulse **Establecer clases**.  

7.  En el cuadro de diálogo **Clases de inventario de hardware**, pulse **Importar**.  

8.  En el cuadro de diálogo **Importar**, seleccione el archivo Managed Object Format (MOF) que quiere importar y, después, pulse **Aceptar**. Revise los elementos que se van a importar y, después, haga clic en **Importar**.  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Cómo exportar clases de inventario de hardware  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Configuración de cliente predeterminada**, pulse **Inventario de hardware**.  

6.  En la lista **Configuración de dispositivo**, pulse **Establecer clases**.  

7.  En el cuadro de diálogo **Clases de inventario de hardware**, pulse **Exportar**.  

    > [!NOTE]  
    >  Cuando se exportan las clases, se exportan todas las clases actualmente seleccionadas.  

8.  En el cuadro de diálogo **Exportar**, especifique el archivo Managed Object Format (MOF) en el que quiere exportar las clases y, luego, pulse **Guardar**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a> Configurar el inventario de hardware para recopilar cadenas de más de 255 caracteres
A partir de Configuration Manager 1802, se puede especificar la longitud de las cadenas de modo que tengan más de 255 caracteres para las propiedades del inventario de hardware. Este cambio se aplica únicamente a las clases recién agregadas y a las propiedades de inventario del hardware que no son claves. <!-- 1357389 -->

1. En el área de trabajo **Administración**, haga clic en **Configuración de cliente**, resalte una configuración de dispositivo cliente para modificar, haga clic con el botón derecho y, después, seleccione **Propiedades**.

2. Seleccione **Inventario de hardware**, después **Establecer clases** y haga clic en **Agregar**.

3. Haga clic en el botón **Conectar**.

4. Rellene **Nombre de equipo** y **Espacio de nombres WMI**, y seleccione **Recurrente** si es necesario. Proporcione las credenciales si es necesario para conectarse. Haga clic en **Conectar** para ver las clases del espacio de nombres.

5. Seleccione una clase nueva y después haga clic en **Editar**.

6. Cambie la **Longitud** de la propiedad que sea una cadena, que no sea la clave, para que sea mayor de 255. Haga clic en **Aceptar**. 

7. Asegúrese de que esté seleccionada la propiedad modificada para **Agregar clase de inventario de hardware** y haga clic en **Aceptar**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Cómo usar archivos de información de administración (archivos MIF) para ampliar el inventario de hardware  
 Use archivos MIF para ampliar la información de inventario de hardware que Configuration Manager ha recopilado de los clientes. Durante el inventario de hardware, la información almacenada en los archivos MIF se agrega al informe de inventario de cliente y almacenada en la base de datos del sitio, donde puede usar los datos de la misma forma que utilice datos de inventario de cliente predeterminada. Hay dos tipos de archivos MIF, NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Para poder agregar información de archivos MIF a la base de datos de Configuration Manager, primero debe crear o importar la información de clase para ellos. Para obtener más información, vea las secciones [Cómo agregar una clase de inventario nueva](#BKMK_Add) y [Cómo importar clases de inventario de hardware](#BKMK_Import) de este artículo.  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Cómo crear archivos NOIDMIF  
 Los archivos NOIDMIF se pueden usar para agregar información a un inventario de hardware de cliente que normalmente Configuration Manager no puede recopilar y está asociado a un dispositivo de cliente concreto. Por ejemplo, muchas empresas etiquetan a cada equipo de la organización con un número de activo y, después, catalogan estos números de forma manual. Cuando se crea un archivo NOIDMIF, esta información puede agregarse a la base de datos de Configuration Manager y se usa para consultas e informes. Para obtener información sobre la creación de archivos NOIDMIF, consulte la documentación del SDK de Configuration Manager.  

> [!IMPORTANT]  
>  Cuando se crea un archivo NOIDMIF, se debe guardar en un formato codificado de ANSI. Configuration Manager no puede leer los archivos NOIDMIF guardados en un formato con codificación UTF-8.  

 Después de crear un archivo NOIDMIF, almacénelo en la carpeta _%Windir%_ **\CCM\Inventory\Noidmifs** de cada cliente. Configuration Manager recopila información de los archivos NODMIF en esta carpeta durante el siguiente ciclo de inventario de hardware programado.  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> Cómo crear archivos IDMIF  
 Los archivos IDMIF se pueden usar para agregar información sobre activos que Configuration Manager no podría inventariar normalmente, y que no están asociados a un dispositivo cliente determinado, a la base de datos de Configuration Manager. Por ejemplo, se podría usar IDMIFS para recopilar información sobre proyectores, reproductores de DVD, fotocopiadoras u otros equipos que no tienen un cliente de Configuration Manager. Para obtener información sobre la creación de archivos IDMIF, consulte la documentación del SDK de Configuration Manager.  

 Después de crear un archivo IDMIF, almacénelo en la carpeta _%Windir%_ **\CCM\Inventory\Idmifs** de equipos cliente. Configuration Manager recopila información de este archivo durante el siguiente ciclo de inventario de hardware programado. Debe declarar clases nuevas para la información contenida en el archivo agregando o importarlos.  

> [!NOTE]
> Los archivos MIF podrían contener grandes cantidades de datos y la recopilación de estos datos podría afectar negativamente al rendimiento del sitio. Habilite la recopilación de archivos MIF solo cuando sea necesario y configure la opción **Tamaño de archivo MIF personalizado máximo (KB)** en la configuración del inventario de hardware. Para obtener más información, vea [Introducción al inventario de hardware](introduction-to-hardware-inventory.md).
