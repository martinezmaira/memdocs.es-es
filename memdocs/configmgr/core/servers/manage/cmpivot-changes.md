---
title: Cambios de CMPivot
titleSuffix: Configuration Manager
description: Obtenga información sobre los cambios realizados en CMPivot entre versiones de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 20b23cec74ae3d201bc81fe1834e87e7eb8fcc13
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129614"
---
# <a name="changes-to-cmpivot"></a>Cambios de CMPivot

Use la siguiente información para conocer los cambios realizados en [CMPivot](cmpivot.md) entre versiones de Configuration Manager:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a> Cambios de CMPivot para la versión 2006
<!--6518631-->

A partir de la versión 2006, se han realizado las mejoras siguientes para CMPivot:

- Convergencia de [CMPivot independiente](cmpivot.md#bkmk_standalone) y CMPivot iniciado desde la consola de administración. Al iniciar CMPivot desde la consola de administración, se usa la misma tecnología subyacente que para CMPivot independiente para proporcionar una paridad de escenario.

- Mejoras en la navegación con el teclado en CMPivot.

- Puede ejecutar CMPivot desde un dispositivo individual o varios dispositivos desde el nodo de dispositivos sin necesidad de seleccionar una colección de dispositivos. Esta mejora facilita a los usuarios (por ejemplo, los trabajadores del departamento de soporte técnico) la creación de consultas de CMPivot para dispositivos específicos fuera de una colección creada previamente.
   - Seleccione un dispositivo individual o varios dispositivos en una colección de dispositivos o seleccione **Iniciar CMPivot**.

- Al devolver los dispositivos dentro de una vista de lista de consultas, puede seleccionar **Dinámica del dispositivo** en uno o varios dispositivos y, a continuación, dinamizar y consultar solo esos dispositivos para profundizar más. Este cambio le permite profundizar sin consultar el conjunto de dispositivos más grande de la colección original. Se reemplazó **Dinámica del dispositivo** por **Dinámica para**.
   - Dentro de una operación de CMPivot existente, seleccione un dispositivo individual o varios dispositivos en la salida. Haga clic con el botón derecho y dinamice con la opción **Dinámica del dispositivo**. Esta acción inicia una instancia de CMPivot independiente limitada solo a los dispositivos seleccionados. Esto facilita la dinamización y la consulta de los dispositivos deseados exclusivamente, sin tener que crear una recopilación para ellos.

- Al ejecutar CMPivot para un dispositivo individual, el nombre del dispositivo se muestra en la parte superior de la ventana. En el caso de varios dispositivos, el número de dispositivos seleccionados aparece en la parte superior de la ventana.
- La opción **Crear colección** de la pestaña Resumen de consulta se quitó porque CMPivot ya no necesita realizar consultas en una colección. Realice una **Dinámica del dispositivo** para abrir una instancia nueva de CMPivot limitada solo a los dispositivos que desea consultar. **Crear colección** sigue estando disponible en el menú principal.

![Dinamización de dispositivos para varios dispositivos con CMPivot](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a> Cambios de CMPivot para la versión 2002
<!--5870934-->
Se ha facilitado la navegación por las entidades CMPivot. A partir de la versión 2002 de Configuration Manager, puede buscar entidades de CMPivot. También se han agregado nuevos iconos para que pueda diferenciar fácilmente las entidades y los tipos de objeto de entidad.

![Búsqueda de entidades CMPivot](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a> Cambios de CMPivot para la versión 1910
<!--5410930, 3197353-->
A partir de la versión 1910, CMPivot se ha optimizado notablemente para reducir el tráfico de red y la carga en los servidores. Además, se han agregado varias entidades y mejoras de entidad para ayudar en la solución de problemas y las búsquedas. Se han incluido los siguientes cambios relativos a CMPivot en la versión 1910:

- [Optimizaciones del motor de CMPivot](#bkmk_optimization)
- Otras entidades y mejoras de entidades:
  - Registros de eventos de Windows ([WinEvent](#bkmk_WinEvent))
  - Contenido de archivo ([FileContent](#bkmk_File))
  - Dlls cargados por procesos ([ProcessModule](#bkmk_ProcessModule))
  - Información de Azure Active Directory ([AADStatus](#bkmk_AadStatus))
  - Estado de protección de punto de conexión ([EPStatus](#bkmk_EPStatus))
- [Evaluación de una consulta de dispositivo local con CMPivot independiente](#bkmk_local-eval)
- [Otras mejoras de CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> Optimizaciones del motor de CMPivot
<!--3197353-->
Para reducir el tráfico de red y la carga en los servidores, CMPivot se ha optimizado en 1910. Ahora, muchas de las operaciones de consulta se realizan directamente en el cliente en lugar de en los servidores. Este cambio también se traduce en que algunas operaciones de CMPivot devuelven datos mínimos de la primera consulta. Si decide explorar los datos para obtener más información, puede que se ejecute una nueva consulta para capturar más datos del cliente. Por ejemplo, antes, cuando se ejecutaba una consulta de tipo "recuento resumido", se devolvía al servidor un conjunto de datos grande.  Al obtenerse un conjunto de datos grande, existía la posibilidad de explorar los datos inmediatamente, cuando muchas veces solo se necesitaba el recuento resumido. En 1910, cuando se elige profundizar en un cliente específico, se lleva a cabo otra colección de los datos para devolver los datos adicionales solicitados. Este cambio mejora el rendimiento y la escalabilidad de las consultas en un gran número de clientes. <!--3197353, 5458337-->

#### <a name="examples"></a>Ejemplos

Las optimizaciones de CMPivot reducen drásticamente la carga de CPU del servidor y de la red necesaria para ejecutar consultas de CMPivot. Con estas optimizaciones, ahora se pueden examinar los gigabytes de datos de cliente en tiempo real. Las siguientes consultas ilustran estas optimizaciones:

- Búsqueda de errores de autenticación en todos los registros de eventos de todos los clientes de la empresa.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Búsqueda de un archivo por hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<logname>,[\<timespan>])

Esta entidad se usa para obtener eventos de los registros de eventos y de los archivos de registro de seguimiento de eventos. La entidad obtiene datos de los registros de eventos que genera la tecnología de registros de eventos de Windows. La entidad también obtiene eventos en archivos de registro generados por Seguimiento de eventos para Windows (ETW). De manera predeterminada, WinEvent examina los eventos que se produjeron dentro de las últimas 24 horas. Sin embargo, el valor predeterminado de 24 horas se puede reemplazar si se incluye un intervalo de tiempo.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<filename>)

FileContent se usa para obtener el contenido de un archivo de texto.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<processname>)  

Esta entidad se usa para enumerar los módulos (dlls) que carga un proceso determinado. ProcessModule es útil al buscar malware que se oculta en procesos legítimos.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

Esta entidad se puede usar para obtener la información de identidad de Azure Active Directory actual de un dispositivo.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus se usa para obtener el estado del software antimalware instalado en el equipo.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> Evaluación de una consulta de dispositivo local con la versión independiente de CMPivot
<!--3197353-->
Al usar CMPivot fuera de la consola de Configuration Manager, puede consultar solo el dispositivo local sin necesidad de la infraestructura de Configuration Manager. Ahora puede usar las consultas de Azure Log Analytics de CMPivot para ver rápidamente información de WMI en el dispositivo local. Esto también permite validar y perfeccionar las consultas de CMPivot antes de ejecutarlas en un entorno más grande. CMPivot independiente solo está disponible en inglés. Para más información sobre CMPivot independiente, vea [CMPivot independiente](#bkmk_standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Problemas conocidos de la evaluación de consultas de dispositivos locales

 - Si consulta en **Este equipo** una entidad WMI a la que no se tiene acceso (como una clase WMI bloqueada), es posible que vea un bloqueo en CMPivot. Ejecute CMPivot con una cuenta con privilegios elevados para consultar esas entidades. <!--5753242-->
- Si consulta entidades que no son de WMI en **Este equipo**, verá un mensaje **Espacio de nombres no válido** o una excepción ambigua.
- Ejecute la versión independiente de CMPivot desde el acceso directo del menú Inicio, no directamente desde la ruta de acceso del archivo ejecutable. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> Otras mejoras

- Se pueden realizar consultas de tipo de expresión regular con el nuevo operador `like`. Por ejemplo:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- Actualizamos las entidades **CcmLog()** y **EventLog()** para examinar de manera predeterminada solo los mensajes en las últimas 24 horas. Este comportamiento se puede reemplazar si se indica un intervalo de tiempo opcional. Por ejemplo, con la siguiente consulta se examinarán los eventos de la última hora:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- La entidad **File()** se actualizó para recopilar información sobre los archivos ocultos y los archivos del sistema e incluir el hash de MD5. Si bien un hash de MD5 no es tan preciso como el hash de SHA256, tiende a ser un hash que se informa de manera habitual en la mayoría de los boletines sobre malware.  

- Puede agregar comentarios en las consultas.<!-- 5431463 --> Este comportamiento es útil cuando se comparten consultas. Por ejemplo:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot se conecta automáticamente al último sitio.<!-- 5420395 --> Después de iniciar CMPivot, puede conectarse a un sitio nuevo si es necesario.

- En el menú **Exportar**, seleccione la opción nueva para **Query link to clipboard** (Vínculo de consulta en el Portapapeles).<!-- 5431577 --> Esta acción copia un vínculo en el Portapapeles que puede compartir con otros usuarios. Por ejemplo:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Este vínculo abre CMPivot independiente con la consulta siguiente:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > Para que este vínculo funcione, [instale CMPivot independiente](#bkmk_standalone).

- En los resultados de la consulta, si el dispositivo está inscrito en Protección contra amenazas avanzada (ATP) de Microsoft Defender, haga clic con el botón derecho en el dispositivo para iniciar el portal en línea del **Centro de seguridad de Microsoft Defender**.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Problemas conocidos de CMPivot en la versión 1910

- Es posible que no se muestre el banner de máximo de resultados cuando se alcance el límite. <!--5431427-->
  - Cada cliente está limitado a 128 KB de datos por consulta.
  - Los resultados se pueden truncar si los resultados de la consulta superan los 128 KB.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a> Cambios de CMPivot para la versión 1906

A partir de la versión 1906, estos elementos se agregaron a CMPivot:

- [Combinaciones, operadores adicionales y agregadores](#bkmk_cmpivot_joins).
- [Permisos de CMPivot agregados al rol Administrador de seguridad](#bkmk_cmpivot_secadmin1906).
- [CMPivot independiente](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> Adición de combinaciones, operadores adicionales y agregadores en CMPivot
<!--4054074-->
Ahora tiene más operadores aritméticos, agregadores y la posibilidad de agregar combinaciones de consulta como el uso conjunto de Registro y Archivo. Se han agregado los elementos siguientes:

#### <a name="table-operators"></a>Operadores de tabla

|Operadores de tabla| Descripción|
|-----|-----|
| [join](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Combina las filas de dos tablas para formar una nueva tabla mediante la coincidencia de fila para el mismo dispositivo|
|render|Representa los resultados como salida gráfica|

El operador render ya existe en CMPivot. Se ha agregado compatibilidad con varias series y la instrucción **with**. Para más información, vea la sección de [ejemplos](#bkmk_cmpivot_examples1906) y el artículo sobre el [operador join](https://docs.microsoft.com/azure/kusto/query/joinoperator) de Kusto.

#### <a name="limitations-for-joins"></a>Limitaciones para las combinaciones

1. La columna de combinación siempre se realiza de forma implícita en el campo **Dispositivo**.
1. Puede usar un máximo de 5 combinaciones por consulta.
1. Puede usar un máximo de 64 columnas combinadas.

#### <a name="scalar-operators"></a>Operadores escalares

|Operador| Descripción|Ejemplo|
|-----|-----|-----|
| + | Agregar| `2 + 1, now() + 1d`|
| - |  Restar| `2 - 1, now() - 1d`|
| * | Multiplicar| `2 * 2`|
| / | Dividir | `2 / 1`|
| % | Módulo | `2 % 1`

#### <a name="aggregation-functions"></a>Funciones de agregación

|Función| Descripción|
|-----|-----|
| percentile()| Devuelve una estimación para el percentil más próximo a la clasificación especificada de la población definida por la expresión|
| sumif() | Devuelve una suma de Expresión para la que Predicado se evalúa como true|

#### <a name="scalar-functions"></a>Funciones escalares

|Función| Descripción|
|-----|-----|
| case()| Evalúa una lista de predicados y devuelve la primera expresión de resultado cuyo predicado se cumpla |
| iff() | Evalúa el primer argumento y devuelve el valor del segundo o tercer argumento en función de si el predicado se ha evaluado como true (el segundo) o false (el tercero)|
 | indexof() | La función notifica el índice de base cero de la primera repetición de una cadena especificada dentro de la cadena de entrada|
| strcat() | Concatena entre 1 y 64 argumentos |
| strlen()| Devuelve la longitud, en caracteres, de la cadena de entrada|
| substring() | Extrae una subcadena de una cadena de origen desde un índice hasta el final de la cadena |
| tostring() | Convierte la entrada en una operación de cadena |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> Ejemplos

- Mostrar el dispositivo, el fabricante, el modelo y la versión del SO:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Mostrar el gráfico de tiempos de arranque para un dispositivo:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Gráfico de barras apiladas en el que se muestran los tiempos de arranque para un dispositivo en ms](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> Permisos de CMPivot agregados al rol Administrador de seguridad
<!--4683130-->

A partir de la versión 1906, se agregaron los permisos siguientes al rol **Administrador de seguridad** integrado de Configuration Manager:

 - **Lectura** en script SMS
 - **Ejecutar CMPivot** en Colección
 - **Lectura** en Informe de inventario

>[!NOTE]
> **Ejecutar scripts** es un superconjunto del permiso **Ejecutar CMPivot**.

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot independiente

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a> Cambios de CMPivot para la versión 1902
<!--3610960-->
A partir de Configuration Manager versión 1902, puede ejecutar CMPivot desde el sitio de administración central (CAS) en una jerarquía. El sitio primario sigue controlando la comunicación con el cliente. Al ejecutar CMPivot desde el sitio de administración central, se comunica con el sitio primario a través del canal de suscripción de mensajes de alta velocidad. Esta comunicación no depende de la replicación SQL estándar entre sitios.

Para ejecutar CMPivot en el sitio CAS, se requieren permisos adicionales cuando SQL o el proveedor no están en el mismo equipo o en el caso de la configuración Always On de SQL. Con estas configuraciones remotas, tiene un "escenario de salto doble" para CMPivot.

Para que CMPivot funcione en el servidor de CAS con dicho "escenario de salto doble", puede definir una delegación restringida. Lea el artículo [Información general de la delegación restringida de Kerberos](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) para entender las implicaciones de seguridad de esta configuración. Kerberos debe trabajar a través de todos los saltos entre los equipos.<!--5746133--> Si tiene más de una configuración remota, como el proveedor de SMS o SQL junto con el CAS o no, o varios bosques de confianza, es posible que necesite una combinación de opciones de permisos. A continuación se muestran los pasos que podría tener que seguir:

### <a name="cas-has-a-remote-sql-server"></a>El CAS tiene un servidor SQL remoto

1. Vaya al servidor SQL Server de cada sitio principal.
   1. Agregue el servidor SQL Server remoto del CAS y el servidor de sitio del CAS al grupo [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess).
   ![Grupo Configmgr_DviewAccess en el servidor SQL Server de un sitio principal](media/cmpivot-dviewaccess-group.png)
1. Vaya a Usuarios y equipos de Active Directory.
   1. Para cada servidor de sitio principal, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server del CAS con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
   1. Para el sitio del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.

   ![Ejemplo de delegación de AD de CMPivot para saltos dobles](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>El CAS tiene un proveedor remoto

1. Vaya al servidor SQL Server de cada sitio principal.
   1. Agregue la cuenta del equipo del proveedor del CAS y el servidor de sitio del CAS al grupo [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess).
1. Vaya a Usuarios y equipos de Active Directory.
   1. Seleccione el equipo del proveedor del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
   1. Seleccione el servidor de sitio del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
1. Reinicie el equipo del proveedor remoto del CAS.

### <a name="sql-always-on"></a>Always On de SQL

1. Vaya al servidor SQL Server de cada sitio principal.
   1. Agregue el servidor de sitio del CAS al grupo [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess).
1. Vaya a Usuarios y equipos de Active Directory.
   1. Para cada servidor de sitio principal, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue las cuentas de servicio del servidor SQL Server del CAS para los nodos de SQL con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
   1. Seleccione el servidor de sitio del CAS, haga clic con el botón derecho y seleccione **Propiedades**.
      1. En la pestaña Delegación, seleccione la tercera opción: **Confiar en este equipo para la delegación solo a los servicios especificados**. 
      1. Seleccione **Usar solamente Kerberos**.
      1. Agregue el servicio de SQL Server de cada sitio principal con el puerto y la instancia.
      1. Asegúrese de que estos cambios se ajustan a la directiva de seguridad de su empresa.
1. Asegúrese de que el [SPN se publique](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) para el nombre del cliente de escucha de SQL del CAS y para cada nombre del cliente de escucha de SQL principal.
1. Reinicie los servidores principales de SQL Server.
1. Reinicie el servidor de sitio del CAS y los servidores SQL Server del CAS.


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a> Cambios de CMPivot para la versión 1810
<!--1359068, 3607759-->

A partir de la versión 1810 de Configuration Manager, CMPivot incluye las mejoras siguientes:

- [Utilidad y rendimiento de CMPivot](#bkmk_cmpivot-perf)
- [Funciones escalares](#bkmk_cmpivot-functions)  
- [Visualizaciones de representación](#bkmk_cmpivot-charts)  
- [Inventario de hardware](#bkmk_cmpivot-hinv)  
- [Operadores escalares](#bkmk_cmpivot-operators)  
- [Resumen de consulta](#bkmk_cmpivot-summary)  
- [Mensajes de estado de auditoría](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> Utilidad y rendimiento de CMPivot

- CMPivot devolverá hasta 100 000 celdas, en lugar de 20 000 filas.
  - Si la entidad tiene 5 propiedades, lo que significa 5 columnas, se mostrarán hasta 20 000 filas.
  - Para una entidad con 10 propiedades, se mostrarán hasta 10 000 filas.
  - El total de los datos que se muestran es menor o igual que 100 000 celdas.
- En la pestaña Resumen de la consulta, seleccione el número de dispositivos con errores o sin conexión y, a continuación, seleccione la opción **Crear colección**. Esta opción hace que sea más fácil establecer el destino de dichos dispositivos con una implementación de la corrección.
   - Esta opción se quitó en la versión 2006, ya que CMPivot ya no necesita realizar consultas en una colección.
- Para guardar las consultas **favoritas**, haga clic en el icono de carpeta.
   ![Ejemplo de cómo guardar una consulta favorita en CMPivot](media/cmpivot-favorite.png)

- Los clientes actualizados a la versión 1810 devuelven resultados inferiores a 80 KB al sitio a través de un canal de comunicación rápido.
  - Este cambio aumenta el rendimiento de la visualización de resultados del script o la consulta.
  - Si el resultado del script o la consulta es mayor que 80 KB, el cliente envía los datos a través de un mensaje de estado.
  - Si el cliente no se actualiza a la versión de cliente 1810, sigue usando los mensajes de estado.

- Al iniciar CMPivot, puede que vea un error parecido a este:  **No se puede usar CMPivot en este momento debido a una versión de script incompatible. Este problema puede deberse a que la jerarquía está en proceso de actualizar un sitio. Espere a que se complete la actualización y vuelva a intentarlo.**

  - Si ve este mensaje, podría significar que:
    - El ámbito de seguridad no está configurado correctamente.
    - Hay problemas con el proceso de actualización.
    - El script de CMPivot subyacente es incompatible.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> Funciones escalares
CMPivot admite estas funciones escalares:
- **ago()** : resta el intervalo de tiempo dado de la hora UTC actual.  
- **datetime_diff()** : calcula la diferencia de calendario entre dos valores de fecha y hora.  
- **now()** : devuelve la hora de reloj UTC actual.  
- **bin()** : redondea valores a la baja a un número entero múltiplo del tamaño de una ubicación determinada.  

> [!Note]  
> El tipo de datos de fecha y hora representa un instante de tiempo, normalmente expresado como una fecha y hora del día. Los valores de tiempo se miden en unidades de 1 segundo. Siempre es un valor de fecha y hora en la zona horaria UTC. Siempre expresa literales de fecha y hora en formato ISO 8601, como por ejemplo, `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Ejemplos
- `datetime(2015-12-31 23:59:59.9)`: literal de fecha y hora específicas.   
- `now()`: hora actual.  
- `ago(1d)`: hora actual menos un día.  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> Visualizaciones de representación

CMPivot ahora incluye compatibilidad básica para el [operador de representación](https://docs.microsoft.com/azure/kusto/query/renderoperator) de KQL. Esta compatibilidad incluye estos tipos:  
- **barchart**: la primera columna es el eje X y puede ser texto, fecha y hora o un valor numérico. La segunda columna debe ser numérica y se muestra como una banda horizontal.  
- **columnchart**: como barchart, con bandas verticales en lugar de bandas horizontales.  
- **piechart**: la primera columna es el eje de color y la segunda columna es numérica.  
- **timechart**: gráfico de líneas. La primera columna es el eje x y debe ser la fecha y hora. La segunda columna es el eje y.  

#### <a name="example-bar-chart"></a>Ejemplo: gráfico de barras
En esta consulta se representan las aplicaciones más usadas recientemente como un gráfico de barras:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Ejemplo de visualización de gráfico de barras de CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Ejemplo: gráfico de tiempo
Para representar gráficos de tiempo, use el nuevo operador **bin()** para agrupar eventos en el tiempo. En esta consulta se muestra cuándo se han iniciado los dispositivos en los últimos siete días:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Ejemplo de visualización de gráfico de tiempo de CMPivot](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Ejemplo: gráfico circular
En esta consulta se muestran todas las versiones de sistema operativo en un gráfico circular:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Ejemplo de visualización de gráfico circular de CMPivot](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> Inventario de hardware
Use CMPivot para consultar cualquier clase de inventario de hardware. Estas clases incluyen cualquier extensión personalizada que realice en el inventario de hardware. CMPivot devuelve inmediatamente los resultados almacenados en caché desde el último examen de inventario de hardware almacenado en la base de datos del sitio. Al mismo tiempo, actualiza los resultados si es necesario con datos dinámicos de cualquier cliente en línea.

La saturación de color de los datos en la tabla de resultados o el gráfico indica si los datos se han transmitido en directo o se han almacenado en caché. Por ejemplo, el azul oscuro indica que los datos son en tiempo real desde un cliente en línea. El azul claro indica que los datos están almacenados en caché.

#### <a name="example"></a>Ejemplo

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Ejemplo de consulta de inventario de CMPivot con visualización de gráfico de columnas](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Limitaciones
- No se admiten estas entidades de inventario de hardware:  
    - Propiedades de la matriz, como por ejemplo, la dirección IP  
    - Real32/Real64 <!--example?-->  
    - Propiedades de objetos incrustados <!--example?-->  
- Los nombres de entidad de inventario deben empezar con un carácter
- No se pueden sobrescribir las entidades integradas mediante la creación de una entidad de inventario con el mismo nombre  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> Operadores escalares
CMPivot incluye estos operadores escalares:  

> [!Note]  
> - LHS: cadena a la izquierda del operador  
> - RHS: cadena a la derecha del operador  


|Operador|Descripción|Ejemplo (da como resultado true)|
|--------|-----------|---------------------|
|==|Igual a|`"aBc" == "aBc"`|
|!=|No es igual a|`"abc" != "ABC"`|
|like|LHS contiene una coincidencia para RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS no contiene ninguna coincidencia para RHS|`"Fabrikam" !like "%xyz%"`|
|contiene|RHS ocurre como una subsecuencia de LHS|`"FabriKam" contains "BRik"`|
|!contains|RHS no se produce en LHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS es una subsecuencia inicial de LHS|`"Fabrikam" startswith "fab"`|
|!startswith|RHS no es una subsecuencia inicial de LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS es una subsecuencia de cierre de LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS no es una subsecuencia de cierre de LHS|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> Resumen de consulta

Seleccione la pestaña **Resumen de consulta** en la parte inferior de la ventana de CMPivot. Con este estado es más fácil identificar los clientes que están sin conexión o solucionar los errores que puedan producirse. Seleccione un valor en la columna Recuento para abrir una lista de dispositivos específicos con ese estado. 

Por ejemplo, seleccione el número de dispositivos con un estado de error. Vea el mensaje de error específico y exporte una lista de estos dispositivos. Si el error indica que no se reconoce un cmdlet específico, cree una colección de la lista de dispositivos exportados para implementar una actualización de Windows PowerShell.  

### <a name="cmpivot-audit-status-messages"></a>Mensajes de estado de auditoría de CMPivot

A partir de la versión 1810, al ejecutar CMPivot, se crea un mensaje de estado de auditoría con el **MessageID 40805**. Para ver los mensajes de estado, vaya a **Supervisión** > **Estado del sistema** > **Consultas de mensaje de estado**. Puede ejecutar **Todos los mensajes de estado de auditoría de un usuario específico** o **All Audit status Messages for a Specific Site** (Todos los mensajes de estado de auditoria de un sitio específico), o bien crear su propia consulta de mensaje de estado.

Se usa el formato siguiente para el mensaje:

MessageID 40805: El usuario &lt;nombre de usuario> ejecutó el script &lt;GUID de script> con el hash &lt;hash de script> en la colección &lt;id. de colección>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 es el GUID de script para CMPivot.
- El hash de script puede verse en el archivo scripts.log del cliente.
- También puede ver el hash almacenado en la puntuación del script de cliente. El nombre de archivo del cliente es &lt;GUID de script>_&lt;hash de script>.
    - Ejemplo de nombre de archivo: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Ejemplo de mensaje de estado de auditoría de CMPivot](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Pasos siguientes
 
[Solución de problemas de CMPivot](cmpivot-tsg.md)
