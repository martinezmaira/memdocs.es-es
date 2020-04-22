---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697933"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a> Informes de inventario de hardware

<!--5468413-->
Si intenta ejecutar un informe que se basa en el inventario de hardware, se devuelve un error. Por ejemplo, un informe de BitLocker devuelve un error similar al siguiente mensaje:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

También puede ver el siguiente error en el archivo **dataldr.log**:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Los paneles de la consola que se basan en el inventario de hardware también pueden verse afectados.

Este problema se debe a un cambio de esquema de la base de datos en tablas de inventario de hardware específicas.

#### <a name="workaround"></a>Solución alternativa

La solución consiste en quitar el atributo existente de la base de datos. Después, el componente de sitio del cargador de datos puede crear un nuevo atributo. Ejecute el siguiente script de SQL en el servidor de base de datos del sitio para corregir el esquema de la tabla:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
