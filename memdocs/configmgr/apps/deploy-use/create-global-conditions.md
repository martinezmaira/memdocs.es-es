---
title: Creación de condiciones globales
titleSuffix: Configuration Manager
description: Cree condiciones globales para especificar cómo se proporciona y se implementa una aplicación en los dispositivos cliente.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689543"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Creación de condiciones globales en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En Configuration Manager, las condiciones globales son reglas que representan condiciones técnicas o empresariales que puede usar para especificar cómo se proporciona y se implementa una aplicación en dispositivos cliente. El acceso a las condiciones globales se realiza desde la página **Requisitos** del Asistente para crear tipos de implementación.  

> [!NOTE]  
>  Solo puede modificar las condiciones globales desde el sitio donde se crearon.  

 Use los procedimientos siguientes para crear condiciones globales de Configuration Manager.  

## <a name="provide-basic-information-about-the-global-condition"></a>Proporcione información básica sobre la condición global  
 Se dispone de varios tipos de condiciones globales. Cada tipo de condición global tiene asociado sus propias opciones. Cuando selecciona un tipo de condición global específica, Configuration Manager muestra las opciones que se aplican a la selección.  

1.  En la consola de Configuration Manager, pulse **Biblioteca de software** > **Administración de aplicaciones** > **Condiciones globales**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, pulse **Crear condición global**.  

4.  En el cuadro de diálogo **Crear condición global** , proporcione un nombre y una descripción opcional para la condición global.  

5.  En la lista desplegable **Tipo de dispositivo**, elija si la condición global es para un equipo **Windows** o un dispositivo **Windows Mobile**.  

6.  En la lista desplegable **Tipo de condición** , elija una de las siguientes opciones:  

    -   **Valor** : esta opción comprueba la existencia de uno o más elementos en los dispositivos cliente. Por ejemplo, puede comprobar la existencia de un archivo, carpeta o clave del Registro en un dispositivo cliente.  

    -   **Expresión**: esta opción le permite configurar reglas más complejas para comprobar si se cumple la condición en los dispositivos cliente. Por ejemplo, puede comprobar si la memoria física de un equipo está entre 2 GB y 4 GB, o si un dispositivo móvil usa entrada de pantalla táctil.  

## <a name="set-up-rules-for-the-global-condition"></a>Configurar reglas para la condición global  
 El procedimiento para definir las reglas de una condición global varía en función de si configura un valor o una expresión. Use el procedimiento aplicable que se explica a continuación para configurar un valor o una expresión para la condición global.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Para configurar un valor para la condición global  

1. En la lista desplegable **Tipo de condición** , elija **Valor**.  

2. En la lista desplegable **Tipo de configuración** , elija el elemento que se va a utilizar como condición para la comprobación de requisitos. Los siguientes tipos de configuración están disponibles.  

   - **Consulta de Active Directory**  

     -   **Prefijo LDAP** : especifique un prefijo LDAP válido para que la consulta de los Servicios de dominio de Active Directory evalúe el cumplimiento en equipos de cliente. Puede usar **LDAP://** o **GC://** .  

     -   **Nombre distintivo (DN)** : especifique el nombre distintivo del objeto de Active Directory Domain Services cuyo cumplimiento se evaluará en equipos cliente.  

     -   **Filtro de búsqueda** : especifique un filtro LDAP opcional para refinar los resultados de la consulta de Servicios de dominio de Active Directory y evaluar el cumplimiento en equipos de cliente.  

     -   **Ámbito de búsqueda** : especifique el ámbito de búsqueda en Servicios de dominio de Active Directory:  

         -   **Base**: consulta solo el objeto especificado.  

         -   **Un nivel**: esta opción no se usa en esta versión de Configuration Manager.  

         -   **Subárbol**: consulta el objeto especificado y su subárbol completo en el directorio.  

     -   **Propiedad** : especifica la propiedad del objeto de Servicios de dominio de Active Directory que se utilizará para evaluar el cumplimiento en equipos de cliente.  

     -   **Consulta**: muestra la consulta LDAP que se ha creado a partir de las entradas de **Prefijo LDAP**, **Nombre distintivo (DN)** , **Filtro de búsqueda**, si se especifica, y **Propiedad**. Esta consulta se utilizará para evaluar el cumplimiento en los equipos de cliente.  

   - **Ensamblaje**  

     -   **Nombre de ensamblado** : especifica el nombre del objeto de ensamblado que se busca. El nombre no puede ser el mismo que el de otro objeto de ensamblado del mismo tipo y, además, debe estar registrado en la caché global de ensamblados. El nombre de ensamblado puede tener un máximo de 256 caracteres.  

     > [!NOTE]  
     >  Un ensamblado es un fragmento de código que se puede compartir entre aplicaciones. Los ensamblados pueden tener la extensión de nombre de archivo .dll o .exe. La caché global de ensamblados es una carpeta con el nombre *%systemroot%\assembly* en los equipos clientes en la que se almacenan todos los ensamblados compartidos.  

   - **Sistema de archivos**  

     - **Tipo**: en la lista desplegable, seleccione si quiere buscar un **Archivo** o una **Carpeta**.  

     - **Ruta de acceso** : especifique la ruta a la carpeta o el archivo especificado en los equipos de cliente. Puede especificar las variables de entorno del sistema y la variable de entorno *% USERPROFILE %* en la ruta.  

       > [!NOTE]  
       >  Si utiliza la variable de entorno *%USERPROFILE%* en los campos **Ruta de acceso** o **Nombre de archivo o carpeta** , la búsqueda se realizará en todos los perfiles de usuario del equipo cliente. Se podrían detectar así varias instancias del archivo o la carpeta.  

     - **Nombre de archivo o carpeta** : especifique el nombre del objeto de archivo o de carpeta que se buscará. Puede especificar las variables de entorno del sistema y la variable de entorno *% USERPROFILE %* en el nombre de archivo o de carpeta. También puede usar los caracteres comodín * y ? en el nombre de archivo.  

       > [!NOTE]  
       >  Si especifica un nombre de archivo o carpeta y utiliza comodines, podría generarse una gran cantidad de resultados. Esto podría tener como consecuencia un uso intensivo de los recursos del equipo cliente y un tráfico de red elevado cuando se notifiquen los resultados a Configuration Manager.  

     - **Incluir subcarpetas** : habilite esta opción si desea buscar en las subcarpetas de la ruta especificada.  

     - **Este archivo o esta carpeta están asociados con una aplicación de 64 bits**: elija si se debe buscar en la ubicación del archivo de sistema de 64 bits ( *%windir%* \system32), además de en la ubicación del archivo de sistema de 32 bits ( *%windir%* \syswow64) en clientes de Configuration Manager que ejecutan una versión de 64 bits de Windows.  

       > [!NOTE]  
       >  Si el mismo archivo o carpeta existe en ubicaciones de archivo de sistema de 64 y 32 bits en el mismo equipo de 64 bits, la condición global detectará varios archivos.  

       El tipo de configuración **Sistema de archivos** no admite la especificación de una ruta de acceso UNC a un recurso compartido de red en el campo **Ruta de acceso** .  

   - **Metabase de IIS**  

     -   **Ruta de acceso de metabase** : especifique una ruta válida a la metabase de IIS.  

     -   **Id. de propiedad** : especifique la propiedad numérica de la configuración de la metabase de IIS.  

   - **Clave del Registro**  

     -   **Subárbol**: en la lista desplegable, seleccione el subárbol del Registro en el que quiere realizar la búsqueda.  

     -   **Clave** : especifique el nombre de la clave del Registro que desea buscar. El formato utilizado debe ser *clave\subclave*.  

     -   **Esta clave del Registro está asociada con una aplicación de 64 bits** : especifica si se deben buscar claves del Registro de 64 bits, además de claves del Registro de 32 bits, en clientes que ejecutan una versión de 64 bits de Windows.  

         > [!NOTE]  
         >  Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detectará ambas claves del Registro.  

   - **Valor del Registro**  

     -   **Subárbol** : en la lista desplegable, seleccione el subárbol del Registro en el que desea realizar la búsqueda.  

     -   **Clave** : especifique el nombre de la clave del Registro que desea buscar. El formato utilizado debe ser *clave\subclave*.  

     -   **Valor** : especifique el valor que debe estar incluido en la clave del Registro especificada.  

     -   **Esta clave del Registro está asociada con una aplicación de 64 bits** : especifica si se deben buscar claves del Registro de 64 bits, además de claves del Registro de 32 bits, en clientes que ejecutan una versión de 64 bits de Windows.  

         > [!NOTE]  
         >  Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detectará ambas claves del Registro.  

   - **Script**  

     -   **Script de detección**: pulse **Agregar** para especificar o buscar el script que se va a usar. Puede usar scripts de Windows PowerShell, VBScript o JScript.  

     -   **Ejecutar scripts mediante las credenciales de usuario del usuario que inició sesión**: si habilita esta opción, el script se ejecutará en los equipos cliente mediante las credenciales del usuario que ha iniciado sesión.  

         > [!NOTE]  
         >  El valor que devuelve el script se utilizará para evaluar el cumplimiento de la condición global. Por ejemplo, si usa VBScript, podría usar el comando **WScript.Echo Result** para devolver el valor de la variable Resultado a la condición global.  
         >   
         >  Si el script devuelve varios valores, dichos valores deben encontrarse en una sola línea y estar separados por un punto y coma. Si cada valor aparece en una línea independiente, la evaluación no se podrá realizar.  

   - **Consulta SQL**  

     -   **Instancia de SQL Server** : elija si desea que la consulta SQL se ejecute en la instancia predeterminada, en todas las instancias, o en un nombre de instancia de base de datos determinado.  

         > [!NOTE]  
         >  El nombre de instancia debe hacer referencia a una instancia local de SQL Server. Para hacer referencia a una instancia en clúster de SQL, debería utilizar una configuración de script.  

     -   **Base de datos** : especifique el nombre de la base de datos de Microsoft SQL Server para la que se ejecutará la consulta SQL.  

     -   **Columna** : especifica el nombre de columna que devuelve la instrucción Transact-SQL que se utiliza para evaluar el cumplimiento de la condición global.  

     -   **Instrucción Transact-SQL** : especifique la consulta SQL completa que se utilizará para la condición global. También puede pulsar **Abrir** para abrir una consulta SQL existente.  

   - **Consulta WQL**  

     -   **Espacio de nombres** : especifique el espacio de nombres de WMI que se utilizará para crear una consulta WQL cuyo cumplimiento se evaluará en equipos cliente. El valor predeterminado es Root\cimv2.  

     -   **Clase** : especifique la clase de WMI que se utilizará para crear una consulta WQL cuyo cumplimiento se evaluará en equipos cliente.  

     -   **Propiedad** : especifique la propiedad de WMI que se utilizará para crear una consulta WQL cuyo cumplimiento se evaluará en equipos cliente.  

     -   **Cláusula WHERE de consulta WQL** : puede utilizar el elemento **Cláusula WHERE de consulta WQL** para especificar una cláusula WHERE que se aplicará a la propiedad, clase y espacio de nombres especificados en los equipos cliente.  

   - **Consulta XPath**  

     -   **Ruta** : especifique la ruta de acceso al archivo XML en los equipos cliente que se usarán para evaluar el cumplimiento. Configuration Manager admite el uso de todas las variables de entorno de sistema de Windows y la variable de usuario *%USERPROFILE%* en el nombre de ruta de acceso.  

     -   **Nombre de archivo XML**: especifique el nombre de archivo que contiene la consulta XML que se usará para evaluar el cumplimiento en equipos cliente.  

     -   **Incluir subcarpetas** : habilite esta opción si desea buscar en las subcarpetas de la ruta especificada.  

     -   **Este archivo está asociado con una aplicación de 64 bits**: elija si se debe buscar en la ubicación del archivo de sistema de 64 bits ( *%windir%* \system32), además de en la ubicación del archivo de sistema de 32 bits ( *%windir%* \syswow64) en clientes de Configuration Manager que ejecutan una versión de 64 bits de Windows.  

     -   **Consulta XPath** : especifique una consulta de lenguaje de rutas XML (XPath) válida y completa para evaluar el cumplimiento en los equipos cliente.  

     -   **Espacios de nombres** : abre el cuadro de diálogo **Espacio de nombres XML** para identificar los prefijos y espacios de nombres que se utilizan durante la consulta XPath.  

3. En la lista desplegable **Tipo de datos** , elija el formato de los datos que devolverá la condición antes de que se utilicen para los requisitos de comprobación.  

   > [!NOTE]  
   >  La lista desplegable **Tipo de datos** no se muestra para todos los tipos de configuración.  

4. Configure más detalles de esta configuración debajo de la lista desplegable **Tipo de configuración**. Los elementos que se pueden configurar variarán en función del tipo de configuración que ha seleccionado.  

5. Pulse **Aceptar** para guardar la regla y cerrar el cuadro de diálogo **Crear condición global**.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Configurar una expresión para la condición global  

1.  En la lista desplegable **Tipo de condición** , elija **Expresión**.  

2.  Pulse **Agregar cláusula** para abrir el cuadro de diálogo **Agregar cláusula**.  

3.  En la lista desplegable **Seleccionar categoría** , seleccione si esta expresión es para un dispositivo o un usuario. También puede seleccionar **Personalizada** para utilizar una condición global configurada previamente.  

4.  En la lista desplegable **Seleccionar una condición** , seleccione la condición que se va a utilizar para evaluar si el usuario o el dispositivo cumple los requisitos de la regla. El contenido de esta lista variará según la categoría seleccionada.  

5.  En la lista desplegable **Elegir operador** , elija el operador que se utilizará para comparar la condición seleccionada con el valor especificado para evaluar si el usuario o el dispositivo cumple los requisitos de la regla. Los operadores disponibles variarán según la condición seleccionada.  

6.  En el campo **Valor** , especifique los valores que se utilizarán con la condición y el operador seleccionados para evaluar si el usuario o el dispositivo cumple los requisitos de la regla. Los valores disponibles variarán según la condición seleccionada y el operador seleccionado.  

7.  Pulse **Aceptar** para guardar la expresión y para cerrar el cuadro de diálogo **Agregar cláusula**.  

8.  Cuando termine de agregar cláusulas a la condición global, pulse **Aceptar** para cerrar el cuadro de diálogo **Crear condición global** y para guardar la condición global.  
