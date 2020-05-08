---
title: Creación de consultas
titleSuffix: Configuration Manager
description: Descubra cómo crear e importar consultas en Configuration Manager. Incluye ejemplos de consultas y sugerencias.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f815394414167ad4f887c5970538eab22c931a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906158"
---
# <a name="create-queries-in-configuration-manager"></a>Creación de consultas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se describe cómo crear e importar consultas en Configuration Manager.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a> Creación de una consulta  
 Use este procedimiento para crear una consulta en Configuration Manager.  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión**, seleccione **Consultas**. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear consulta**.  

3.  En la pestaña **General** del **Asistente para crear consultas**, especifique un nombre único y un comentario opcional para la consulta.  

4.  Si quiere importar una consulta existente para usar como base para la nueva consulta, elija **Importar instrucción de consulta**. En el cuadro de diálogo **Examinar consulta**, seleccione una consulta que quiera importar y, luego, elija **Aceptar**.  

5.  En la lista **Tipo de objeto**, seleccione el tipo de objeto que quiere que devuelva la consulta. En la tabla siguiente se describen algunos ejemplos de los tipos de objetos que puede buscar:  

    |Tipo de objeto|Descripción|  
    |-----------------|-----------------|  
    |**Recurso del sistema**|Use esta opción para buscar los atributos típicos del sistema, como el nombre NetBIOS de un dispositivo, la versión del cliente, la dirección IP del cliente y la información de Active Directory Domain Services.|  
    |**Recurso de usuario**|Use esta opción para buscar información habitual del usuario, como nombres de usuarios, nombres de grupos de usuarios y nombres de grupos de seguridad.|  
    |**Implementación**|Use esta opción para buscar los atributos típicos de una implementación, como el nombre de la implementación, la programación y la recopilación en la que se implementó.|  

6.  Seleccione **Editar instrucción de consulta** para abrir el cuadro de diálogo **Propiedades de instrucción** de &lt;nombre de consulta\>.  

7.  En la pestaña **General** del cuadro de diálogo **Propiedades de instrucción** de &lt;nombre de la consulta\>, especifique los atributos que devuelve esta consulta y cómo se van a mostrar. Seleccione el icono **Nuevo** para agregar un nuevo atributo. También puede seleccionar **Mostrar idioma de consulta** para escribir o editar la consulta directamente en el lenguaje de consulta de WMI (WQL). Para ver ejemplos de consultas de WMI, consulte la sección [Example WQL queries](#BKMK_Example) en este artículo.  

    > [!TIP]  
    > Puede usar la siguiente documentación de referencia para que le ayude a construir sus propias consultas WQL:  
    >   
    > -   [WQL (SQL para WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [Cláusula WHERE](https://docs.microsoft.com/windows/win32/wmisdk/where-clause)  
    > -   [Operadores WQL](https://docs.microsoft.com/windows/win32/wmisdk/wql-operators)  

8.  En la pestaña **Criterios** del cuadro de diálogo **Propiedades de instrucción** de &lt;nombre de consulta\>, especifique los criterios que se usan para refinar los resultados de la consulta. Por ejemplo, podría devolver solo los recursos que tienen un código de sitio de **XYZ**. Puede configurar varios criterios para una consulta.  

    > [!IMPORTANT]  
    > Si crea una consulta que no contiene ningún criterio, devolverá todos los dispositivos en la recopilación **Todos los sistemas** .  

9. En la pestaña **Combinaciones** del cuadro de diálogo **Propiedades de instrucción** de &lt;nombre de consulta\>, puede combinar datos de dos atributos diferentes en los resultados de la consulta. Aunque Configuration Manager crea automáticamente combinaciones de consulta cuando se eligen atributos diferentes para el resultado de la consulta, la pestaña **Combinaciones** proporciona opciones más avanzadas. Configuration Manager admite estas clases de atributos:  

    |Tipo de combinación|Descripción|  
    |---------------|-----------------|  
    |Interna|Muestra solo los resultados coincidentes. Se usa siempre con las combinaciones que se crean automáticamente.|  
    |Izquierda|Muestra todos los resultados para el atributo base y solo los resultados coincidentes para el atributo de combinación.|  
    |Derecha|Muestra todos los resultados del atributo de combinación y solo los resultados coincidentes del atributo base.|  
    |Full|Muestra todos los resultados del atributo base y del atributo de combinación.|  

     Para más información sobre cómo usar operaciones de combinación, consulte la documentación de SQL Server.  

10. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades de instrucción** de &lt;nombre de consulta\>.  

11. En la pestaña **General** del **Asistente para crear consultas**, especifique que los resultados de la consulta no se limitan a los miembros de una recopilación, que se limitan a los miembros de una recopilación especificada o que aparece una solicitud de una recopilación cada vez que se ejecuta la consulta.  

12. Complete el asistente para crear la consulta. La nueva consulta se muestra en el nodo **Consultas** del área de trabajo **Supervisión**.  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a> Importación de una consulta  
 Use este procedimiento para importar una consulta en Configuration Manager. Para más información sobre cómo exportar consultas, vea [Cómo administrar consultas](../../../core/servers/manage/manage-queries.md).  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión**, seleccione **Consultas**. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Importar objetos**.  

3.  En la página **Nombre de archivo MOF** del **Asistente para importar objetos**, elija **Examinar** para seleccionar el archivo Managed Object Format (MOF) que contiene la consulta que quiere importar.  

4.  Revise la información sobre la consulta que quiere importar y, luego, siga los pasos del asistente. La nueva consulta se muestra en el nodo **Consultas** del área de trabajo **Supervisión**.  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Esta sección contiene consultas de WMI de ejemplo que puede usar en su jerarquía o modificarlas para otros fines. Para usar estas consultas, seleccione **Mostrar idioma de consulta** en el cuadro de diálogo **Propiedades de instrucción de consulta**. A continuación, copie y pegue la consulta en el campo **Instrucción de consulta**.  

> [!TIP]  
> Use el carácter comodín `%` para indicar cualquier cadena de caracteres. Por ejemplo, `%Visio%` devuelve Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-10"></a>Equipos que ejecutan Windows 10

Use la siguiente consulta para devolver la versión del sistema operativo y el nombre NetBIOS de todos los equipos que ejecutan Windows 7.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Equipos con un paquete de software específico instalado  

Use la siguiente consulta para devolver el nombre NetBIOS y el nombre del paquete de software de todos los equipos que tienen instalado un paquete de software específico. En este ejemplo se devuelven todos los equipos que tienen instalada una versión de Microsoft Visio. Reemplace `Microsoft%Visio%` por el paquete de software que quiere consultar.  

> [!TIP]  
> Esta consulta busca el paquete de software con los nombres que se muestran en la lista de programas del Panel de Control de Windows.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Equipos que están en una unidad organizativa específica de Active Directory Domain Services

Use la siguiente consulta para devolver el nombre NetBIOS y el nombre de unidad organizativa de todos los equipos de una unidad organizativa. Reemplace el texto `OU Name` por el nombre de la unidad organizativa que quiere consultar.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Equipos con un nombre NetBIOS específico

Use la siguiente consulta para devolver el nombre NetBIOS de todos los equipos que empiecen por una cadena de caracteres específica. En este ejemplo, la consulta devuelve todos los equipos con un nombre NetBIOS que empiece por `ABC`.  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Dispositivos de un tipo específico

Los tipos de dispositivos se almacenan en la base de datos de Configuration Manager en la clase de recurso **sms_r_system** y el nombre de atributo **AgentEdition**. Use esta consulta para recuperar solo los dispositivos que coinciden con la edición de agente del tipo de dispositivo que especifique:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Use uno de estos valores para &lt;Id. de dispositivo\>:  

|Tipo de dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Equipo portátil o de escritorio de Windows|0|  
|Dispositivo basado en ARM de Windows (que ejecuta Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Equipo Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Sistema Intel en un chip|12|  
|Servidores Unix y Linux|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Los valores que no se enumeran en esta tabla están asociados a dispositivos que ya no se admiten.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Por ejemplo, si quiere devolver solo los equipos Mac, use esta consulta:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Pasos siguientes

[Cómo administrar consultas](manage-queries.md)
