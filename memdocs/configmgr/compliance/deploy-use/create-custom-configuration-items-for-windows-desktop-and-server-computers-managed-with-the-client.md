---
title: Creación de elementos de configuración personalizados
titleSuffix: Configuration Manager
description: Administración de la configuración de equipos y servidores de Windows con un elemento de configuración predeterminado para escritorios y servidores de Windows
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 24637862326b029f974843c18ccba835ee5501ba
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240429"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Creación de elementos de configuración personalizados para equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


Use el elemento de configuración de **escritorios y servidores de Windows personalizados** de Configuration Manager para administrar la configuración de equipos y servidores de Windows administrados por el cliente de Configuration Manager.  



## <a name="start-the-wizard"></a>Inicio del asistente

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione el nodo **Elementos de configuración**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear elemento de configuración**.  

3. En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  

4. En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Windows Desktops and Servers (custom)** .  

    > [!TIP]  
    > Si quiere proporcionar la configuración del método de detección que compruebe la existencia de una aplicación, seleccione **This configuration file contains application settings**.  

5. Para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager, seleccione **Categorías** para crear y asignar categorías.  



## <a name="detection-methods"></a>Métodos de detección  

Use este procedimiento para proporcionar información de método de detección para el elemento de configuración.  

> [!NOTE]  
> Esta información solo se aplica si selecciona **Este elemento de configuración contiene la configuración de la aplicación** en la página **General** del asistente.  

Un método de detección de Configuration Manager contiene reglas que se usan para detectar si una aplicación ya está instalada en un equipo. Esta detección se produce antes de que el cliente evalúe si cumple las normas para el elemento de configuración. Para detectar si una aplicación está instalada, puede detectar la presencia de un archivo de Windows Installer para la aplicación, utilice una secuencia de comandos personalizada o seleccione **suponer siempre se instala la aplicación** para evaluar el elemento de configuración para el cumplimiento, independientemente de si se instaló la aplicación.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detectar la instalación de una aplicación mediante el archivo de Windows Installer  

1. En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione la opción **Usar la detección de Windows Installer**.  

2. Seleccione **Abrir**, busque el archivo de Windows Installer (.msi) que quiere detectar y, a continuación, seleccione en **Abrir**.  

3. El campo **Versión** se rellena automáticamente con el número de versión del archivo de Windows Installer. Si el valor mostrado es incorrecto, escriba aquí un nuevo número de versión.  

4. Si quiere detectar todos los perfiles de usuario del equipo, seleccione **Esta aplicación se instala para uno o más usuarios**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detectar una aplicación y un tipo de implementación específicos  

1. En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione **Detectar una aplicación y un tipo de implementación específicos**. Elija **Seleccionar**.   

2. En el cuadro de diálogo **Especificar aplicación** , seleccione la aplicación y un tipo de implementación asociada quiere detectar.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detectar la instalación de una aplicación mediante un script personalizado  

1. En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione la opción **Usar un script personalizado para detectar la aplicación**.  

2. En la lista, seleccione el idioma del script. Elija uno de los formatos siguientes:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > A partir de la versión 1810, cuando un script de Windows PowerShell se ejecuta como un método de detección, el cliente de Configuration Manager llama a PowerShell con el parámetro `-NoProfile`. Esta opción inicia PowerShell sin perfiles. Un perfil de PowerShell es un script que se ejecuta cuando se inicia PowerShell. <!--3607762-->  

3. Seleccione **Abrir**, vaya al script que quiere usar y, a continuación, seleccione **Abrir**.  



## <a name="specify-supported-platforms"></a>Especificar plataformas admitidas  

En la página **Plataformas admitidas** del **Asistente para crear un elemento de configuración**, seleccione las versiones de Windows en las que quiere que se evalúe el cumplimiento del elemento de configuración o elija **Seleccionar todo**.

También puede **especificar la versión de Windows manualmente**. Seleccione **Agregar** y especifique cada parte del número de compilación de Windows.

> [!NOTE]
> Al especificar Windows Server 2016, la selección de `All Windows Server 2016 and higher 64-bit)` también incluye Windows Server 2019. Para especificar solo Windows Server 2016, use la opción **Especificar la versión de Windows manualmente**. <!--5866480-->



##  <a name="configure-settings"></a>Configurar valores  

Use este procedimiento para configurar las opciones del elemento de configuración.  

Configuración representa el negocio o condiciones técnicas que se utilizan para evaluar el cumplimiento en dispositivos cliente. Puede configurar una nueva configuración o ir a una configuración existente en un equipo de referencia.  

1. En la página **Configuración** del **Asistente para crear un elemento de configuración**, seleccione **Nuevo**.  

2. En el **General** ficha de la **Crear configuración** diálogo cuadro, proporcione la siguiente información:  

    - **Nombre**: escriba un nombre único para la configuración. Puede utilizar un máximo de 256 caracteres.  

    - **Descripción**: especifique una descripción para la configuración. Puede utilizar un máximo de 256 caracteres.  

    - **Tipo de configuración**: en la lista, elija y configure uno de los siguientes tipos de configuración que se usará para esta configuración:  
        - [Consulta de Active Directory](#bkmk_adquery)
        - [Ensamblaje](#bkmk_assembly)
        - [Sistema de archivos](#bkmk_file)
        - [Metabase de IIS](#bkmk_iis)
        - [Clave del Registro](#bkmk_regkey)
        - [Valor del Registro](#bkmk_regval)
        - [Script](#bkmk_script)
        - [Consulta SQL](#bkmk_sql)
        - [Consulta WQL](#bkmk_wql)
        - [Consulta XPath](#bkmk_xpath)

    - **Tipo de datos**: Elija el formato en el que la condición devuelve los datos antes de que se usen para evaluar la configuración. La lista **Tipo de datos** no se muestra para todos los tipos de configuración.  

        > [!Tip]  
        > El tipo de datos **Punto flotante** admite solo tres dígitos después del separador decimal.  

3. Configurar detalles adicionales acerca de esta configuración en el **Establecer tipo** lista. Los elementos que se pueden configurar varían según el tipo de configuración seleccionada.  

4. Seleccione **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Crear configuración**.  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a> Consulta de Active Directory

- **Prefijo LDAP**: especifique un prefijo válido para que la consulta de Active Directory Domain Services evalúe el cumplimiento en los equipos cliente. Para realizar una búsqueda en el catálogo global, use `LDAP://` o `GC://`.  

- **Nombre distintivo (DN)** : especifique el nombre distintivo del objeto de Active Directory Domain Services cuyo cumplimiento se evaluará en los equipos cliente.  

- **Filtro de búsqueda**: especifique un filtro LDAP opcional para refinar los resultados de la consulta de Active Directory Domain Services y evaluar el cumplimiento en los equipos cliente. Para devolver todos los resultados de la consulta, escriba `(objectclass=*)`.  

- **Ámbito de búsqueda**: especifique el ámbito de búsqueda de Active Directory Domain Services.  

    - **Base**: consulta solo el objeto especificado.  

    - **Un nivel**: esta opción no se usa en esta versión de Configuration Manager.  

    - **Subárbol**: consulta el objeto especificado y su subárbol completo en el directorio.  

- **Propiedad**: Especifica la propiedad del objeto de Active Directory Domain Services que se usa para evaluar el cumplimiento en los equipos cliente.  

    Por ejemplo, si quiere consultar la propiedad de Active Directory que almacena el número de veces que un usuario escribe mal una contraseña, escriba `badPwdCount` en este campo.  

- **Consulta**: muestra la consulta que se creó a partir de las entradas de **Prefijo LDAP**, **Nombre distintivo (DN)** , **Filtro de búsqueda** (si se especificó) y **Propiedad**.  


### <a name="assembly"></a><a name="bkmk_assembly"></a> Ensamblaje

Un ensamblado es un fragmento de código que se puede compartir entre aplicaciones. Los ensamblados pueden tener la extensión de nombre de archivo .dll o .exe. La caché global de ensamblados es la carpeta `%SystemRoot%\Assembly` en los equipos cliente. En esta caché se almacenan todos los ensamblados compartidos de Windows.  

- **Nombre de ensamblado:** especifica el nombre del objeto de ensamblado que se quiere buscar. El nombre no puede ser el mismo que el de otros objetos de ensamblado del mismo tipo. Primero, regístrelo en la caché global de ensamblados. El nombre de ensamblado puede tener hasta 256 caracteres.  


### <a name="file-system"></a><a name="bkmk_file"></a> Sistema de archivos

- **Tipo**: En la lista, seleccione si quiere buscar un **archivo** o una **carpeta**.  

- **Ruta de acceso**: Especifique la ruta de acceso de la carpeta o archivo especificado en los equipos cliente. Puede especificar las variables de entorno del sistema y la variable de entorno `%USERPROFILE%` en la ruta de acceso.  

    > [!NOTE]  
    > Si usa la variable de entorno `%USERPROFILE%` en los cuadros **Ruta de acceso** o **Nombre de archivo o carpeta**, el cliente de Configuration Manager busca en todos los perfiles de usuario del equipo cliente. Este comportamiento podría permitirle encontrar varias instancias del archivo o la carpeta.  
    >   
    > Si la configuración de cumplimiento no tiene acceso a la ruta especificada, se genera un error de detección. Además, si el archivo que está buscando está actualmente en uso, se genera un error de detección.  

    > [!Tip]  
    > Seleccione **Examinar** para realizar la configuración a partir de los valores de un equipo de referencia.   

- **Nombre de archivo o carpeta**: especifique el nombre del archivo o carpeta para buscar. Puede especificar las variables de entorno del sistema y la variable de entorno `%USERPROFILE%` en el nombre de archivo o carpeta. También puede utilizar los caracteres comodín `*` y `?` en el nombre de archivo.  

    > [!NOTE]  
    > Si especifica un nombre de archivo o carpeta y utiliza comodines, esta combinación podría producir una gran cantidad de resultados. Esto podría tener también como resultado un uso intensivo de los recursos del equipo cliente y un tráfico de red elevado cuando se notifiquen los resultados a Configuration Manager.  

- **Incluir subcarpetas**: busque también en todas las subcarpetas de la ruta de acceso especificada.  

- **Este archivo o esta carpeta están asociados con una aplicación de 64 bits**: si se habilita, solo se busca en ubicaciones de archivos de 64 bits, como `%ProgramFiles%` en equipos de 64 bits. Si esta opción no está habilitada, se busca en ubicaciones de 64 bits y de 32 bits, como `%ProgramFiles(x86)%`.  

    > [!NOTE]  
    > Si el mismo archivo o carpeta existe en ubicaciones de archivo de sistema de 64 y 32 bits en el mismo equipo de 64 bits, la condición global detectará varios archivos.  

    El tipo de configuración **Sistema de archivos** no admite la especificación de una ruta de acceso UNC a un recurso compartido de red en el campo **Ruta de acceso**.  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a> Metabase de IIS

- **Ruta de acceso de metabase**: especifique una ruta válida a la metabase de Internet Information Services (IIS). Por ejemplo, `/LM/W3SVC/`.  

- **Id. de propiedad**: especifique la propiedad numérica de la configuración de la metabase de IIS.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a> Clave del Registro

- **Subárbol**: seleccione el subárbol del Registro en el que quiere realizar la búsqueda.

    > [!Tip]  
    > Seleccione **Examinar** para realizar la configuración a partir de los valores de un equipo de referencia. Para buscar una clave del Registro en un equipo remoto, habilite el servicio **Registro remoto** en el equipo remoto.  

- **Clave**: Especifique el nombre de la clave del Registro que desea buscar. Use el formato `key\subkey`.  

- **Esta clave del Registro está asociada con una aplicación de 64 bits**: busque claves del Registro de 64 bits además de las claves del Registro de 32 bits en los clientes que ejecutan una versión de Windows de 64 bits.  

    > [!NOTE]  
    > Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detecta ambas claves del Registro.  


### <a name="registry-value"></a><a name="bkmk_regval"></a> Valor del Registro

- **Subárbol**: seleccione el subárbol del Registro en el que se va a realizar la búsqueda.  

    > [!Tip]  
    > Seleccione **Examinar** para realizar la configuración a partir de los valores de un equipo de referencia. Para buscar un valor del Registro en un equipo remoto, habilite el servicio **Registro remoto** en el equipo remoto. También necesita permisos de administrador para acceder al equipo remoto.  

- **Clave**: especifique el nombre de la clave del Registro que se va a buscar. Use el formato `key\subkey`.  

- **Valor**: Especifique el valor que debe estar incluido en la clave del Registro especificada.  

- **Esta clave del Registro está asociada con una aplicación de 64 bits**: busque claves del Registro de 64 bits además de las claves del Registro de 32 bits en los clientes que ejecutan una versión de Windows de 64 bits.  

    > [!NOTE]  
    > Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detecta ambas claves del Registro.  


### <a name="script"></a><a name="bkmk_script"></a> Script

El valor que devuelve el script se usa para evaluar el cumplimiento de la condición global. Por ejemplo, si usa VBScript, se puede usar el comando **WScript.Echo Result** para devolver el valor de la variable *Result* a la condición global.  

- **Script de detección**: seleccione **Agregar script** y escriba o busque un script. Este script se usa para buscar el valor. Puede utilizar scripts de Windows PowerShell, VBScript o Microsoft JScript.  

- **Script de corrección (opcional)** : seleccione **Agregar script** y escriba o busque un script. Este script se usa para corregir valores de configuración no compatibles. Puede utilizar scripts de Windows PowerShell, VBScript o Microsoft JScript.  

- **Ejecutar scripts mediante las credenciales de usuario del usuario que inició sesión**: si habilita esta opción, el script se ejecuta en los equipos cliente que usan las credenciales del usuario que ha iniciado la sesión.  

> [!Note]  
> A partir de la versión 1810, cuando se usa Windows PowerShell como script de detección o corrección, el cliente de Configuration Manager llama a PowerShell con el parámetro `-NoProfile`. Esta opción inicia PowerShell sin perfiles. Un perfil de PowerShell es un script que se ejecuta cuando se inicia PowerShell. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a> Consulta SQL

- **Instancia de SQL Server**: elija si quiere que la consulta SQL se ejecute en la instancia predeterminada, en todas las instancias o en un nombre de instancia de base de datos determinado.  

    > [!NOTE]  
    > El nombre de instancia debe hacer referencia a una instancia local de SQL Server. Para hacer referencia a una instancia en clúster de SQL, debería utilizar una configuración de script.  

- **Base de datos**: especifique el nombre de la base de datos de Microsoft SQL Server en la que desea ejecutar la consulta SQL.  

- **Columna**: especifique el nombre de columna que devuelve la instrucción Transact-SQL que se usa para evaluar el cumplimiento de la condición global.  

- **Instrucción Transact-SQL**: especifique la consulta SQL completa que se va a utilizar para la condición global. Para usar una consulta SQL existente, seleccione **Abrir**.  

    > [!IMPORTANT]  
    > La configuración de consulta SQL no admite los comandos SQL que modifican la base de datos. Solo puede usar los comandos SQL que leen la información de la base de datos.  


### <a name="wql-query"></a><a name="bkmk_wql"></a> Consulta WQL

- **Espacio de nombres**: especifique el espacio de nombres WMI cuyo cumplimiento se evalúa en los equipos cliente. El valor predeterminado es `root\cimv2`.  

- **Clase**: especifique la clase WMI de destino en el espacio de nombres anterior.  

- **Propiedad**: especifique la propiedad WMI de destino en la clase anterior.  

- **Cláusula WHERE de consulta WQL**: especifique una cláusula completa para reducir los resultados. Por ejemplo, para consultar únicamente el servicio DHCP en la clase Win32_Service, la cláusula WHERE podría ser `Name = 'DHCP' and StartMode = 'Auto'`.   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a> Consulta XPath

- **Ruta de acceso**: especifique la ruta de acceso al archivo .xml en los equipos cliente que se usa para evaluar el cumplimiento. Configuration Manager admite el uso de todas las variables de entorno de sistema de Windows y la variable de usuario `%USERPROFILE%` en el nombre de ruta de acceso.  

- **Nombre de archivo XML**: especifique el nombre de archivo que contiene la consulta XML en la ruta de acceso anterior.  

- **Incluir subcarpetas**: habilite esta opción si desea buscar en las subcarpetas de la ruta especificada.  

- **Este archivo está asociado con una aplicación de 64 bits**: busque en la ubicación de archivos del sistema de 64 bits `%Windir%\System32`, además de en la ubicación de archivos del sistema de 32 bits `%Windir%\Syswow64`, en clientes de Configuration Manager que ejecutan una versión de Windows de 64 bits.  

- **Consulta XPath**: especifique una consulta de lenguaje de rutas XML (XPath) válida y completa.  

- **Espacios de nombres**: identifique los espacios de nombres y los prefijos que se van a usar durante la consulta XPath.  

Si se intenta detectar un archivo .xml cifrado, la configuración de cumplimiento encuentra el archivo, pero la consulta XPath no produce ningún resultado. El cliente de Configuration Manager no genera un error.  

Si la consulta XPath no es válida, la configuración se evalúa como no conforme en los equipos cliente.  



##  <a name="configure-compliance-rules"></a>Configurar reglas de cumplimiento  

Las reglas de cumplimiento especifican las condiciones que definen la conformidad de un elemento de configuración. Para poder evaluar el cumplimiento de una configuración, debe tener al menos una regla de cumplimiento. WMI, el registro y la configuración de la secuencia de comandos le permite corregir valores que se encuentran como no conforme. Puede crear nuevas reglas o busque una configuración existente en cualquier elemento de configuración para seleccionar las reglas en ella.  


### <a name="to-create-a-compliance-rule"></a>Para crear una regla de cumplimiento  

1. En la página **Reglas de cumplimiento** del **Asistente para crear un elemento de configuración**, seleccione **Nuevo**.  

2. En el cuadro de diálogo **Crear regla** , proporcione la siguiente información:  

    - **Nombre**: escriba un nombre para la regla de cumplimiento.  

    - **Descripción**: escriba una descripción para la regla de cumplimiento.  

    - **Configuración seleccionada**: seleccione **Examinar** para abrir el cuadro de diálogo **Seleccionar configuración**. Seleccione la configuración para la que quiere definir una regla o haga clic en **Nueva configuración**. Cuando termine, elija **Seleccionar**.  

        > [!Tip]  
        > Para ver información sobre la configuración seleccionada, seleccione **Propiedades**.  

    - **Tipo de regla**: seleccione el tipo de regla de cumplimiento que quiere usar:  

        - **Valor**: cree una regla que compare el valor devuelto por el elemento de configuración con un valor que especifique. Para obtener más información sobre la configuración adicional, consulte [Reglas de valor](#bkmk_value).  

        - **Existencial**: cree una regla que evalúe la configuración en función de si existe en un dispositivo cliente o de las veces que se encuentra. Para obtener más información sobre la configuración adicional, consulte [Reglas de existencial](#bkmk_exist).  

3. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Crear regla**.  




### <a name="value-rules"></a><a name="bkmk_value"></a> Reglas de valor  

- **Propiedad**: la propiedad del objeto que se va a comprobar varía en función del valor seleccionado. Las propiedades disponibles varían según el tipo de valor. 

- **La configuración debe cumplir la siguiente regla**: las reglas o permisos disponibles varían según el tipo de valor.

- **Corregir las reglas no compatibles cuando se admita**: Seleccione esta opción para que Configuration Manager corrija automáticamente las reglas no compatibles. Configuration Manager admite esta acción con los siguientes tipos de reglas:  

    - **Valor del Registro**: si no es compatible, el cliente establece el valor del Registro. Si no existe, el cliente crea el valor.  

    - **Script**: el cliente usa el script de corrección que se ha especificado con la configuración.  

    - **Consulta WQL**  

    > [!IMPORTANT]  
    > Solo puede corregir reglas no conformes cuando el operador de regla se establece en **es igual a**.  

- **Notificar la no conformidad si no se encuentra la instancia de esta configuración**: Si esta configuración no se encuentra en los equipos cliente, habilite esta opción para que el elemento de configuración informe del incumplimiento.  

- **Gravedad de la falta de cumplimiento de los informes**: especifique el nivel de gravedad que se indica en los informes de Configuration Manager si se produce un error en esta regla de cumplimiento. Están disponibles los siguientes niveles de gravedad:  
    - **Ninguno**  
    - **Información**  
    - **Advertencia**  
    - **Crítica**  
    - **Crítica con evento**: Los equipos que no respeten esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a> Reglas de existencial 

> [!NOTE]  
> Las opciones mostradas pueden variar según el tipo de configuración para la que configura una regla.  

- **La configuración debe existir en dispositivos cliente**  

- **La configuración no debe existir en dispositivos cliente.**  

- **La configuración ocurre el siguiente número de veces:**  

- **Gravedad de la falta de cumplimiento de los informes**: especifique el nivel de gravedad que se indica en los informes de Configuration Manager si se produce un error en esta regla de cumplimiento. Están disponibles los siguientes niveles de gravedad:  
    - **Ninguno**  
    - **Información**  
    - **Advertencia**  
    - **Crítica**  
    - **Crítica con evento**: Los equipos que no respeten esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a> Seguimiento de las correcciones de elementos de configuración
<!--4261411-->
*(Se incorporó en la versión 2002)*

A partir de Configuration Manager versión 2002, puede **realizar un seguimiento del historial de correcciones cuando se admita** en las reglas de cumplimiento de los elementos de configuración. Cuando se habilita esta opción, cualquier corrección que se produzca en el cliente para el elemento de configuración generará un mensaje de estado. El historial se almacena en la base de datos de Configuration Manager.

Cree informes personalizados para ver el historial de correcciones mediante la vista pública **v_CIRemediationHistory**. La columna `RemediationDate` es la hora, en UTC, a la que el cliente ejecutó la corrección. El valor `ResourceID` identifica el dispositivo. La creación de informes personalizados con la vista **v_CIRemediationHistory** le ayudará a:

- Identificar posibles problemas con los scripts de corrección
- Buscar tendencias en las correcciones, como un cliente que en ningún momento es compatible con los ciclos de evaluación.

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Habilitar la opción de seguimiento del historial de correcciones cuando se admita

- Para los nuevos elementos de configuración, agregue la opción **Track remediation history when supported** (Seguimiento del historial de correcciones cuando se admita) en la pestaña **Reglas de compatibilidad** cuando cree un valor en la página **Configuración** del asistente.
- Para los elementos de configuración existentes, agregue la opción **Track remediation history when supported** (Seguimiento del historial de correcciones cuando se admita) en la pestaña **Reglas de compatibilidad** en las **Propiedades** del elemento de configuración.
[ ![Seguimiento del historial de correcciones cuando se admita en la versión 2002](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Pasos siguientes

[Crear líneas base de configuración](create-configuration-baselines.md)
