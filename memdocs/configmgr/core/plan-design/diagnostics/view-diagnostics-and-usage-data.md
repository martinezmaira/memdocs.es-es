---
title: Visualización de datos de diagnóstico
titleSuffix: Configuration Manager
description: Vea datos de diagnóstico y de uso para confirmar que la jerarquía de Configuration Manager no contiene información confidencial.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a11b5779eca41ed25a8e53e555f91b596452e51b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128576"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Procedimientos para ver diagnósticos y datos de uso para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede ver datos de diagnóstico y de uso de la jerarquía de Configuration Manager para confirmar que no se incluye información confidencial o de identificación. El sitio resume y almacena sus datos de diagnóstico en la tabla **TEL_TelemetryResults** de la base de datos del sitio. Da formato a los datos para que se puedan usar mediante programación y sean eficaces.

La información de este artículo ofrece una vista de los datos exactos que se envían a Microsoft. No está diseñado para usarse con otros propósitos, como el análisis de datos.  

## <a name="view-data-in-database"></a>Visualización de datos en la base de datos

Use el comando de SQL siguiente para ver el contenido de esta tabla y mostrar los datos exactos que se envían:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Exportación de los datos

Cuando el punto de conexión de servicio está en modo sin conexión, use la herramienta de conexión de servicio para exportar los datos actuales a un archivo de valores separados por comas (CSV). Ejecute la herramienta de conexión de servicio en el punto de conexión de servicio con el parámetro **-Export**.

Para obtener más información, vea [Uso de la herramienta de conexión de servicio](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a> Valores hash unidireccionales

Algunos datos consisten en cadenas de caracteres alfanuméricos aleatorios. Configuration Manager usa el algoritmo SHA-256 para crear valores hash unidireccionales. Este proceso garantiza que Microsoft no recopile datos potencialmente confidenciales. Los datos con código hash todavía se pueden usar con fines de correlación y comparación.

Por ejemplo, en lugar de recopilar los nombres de tablas en la base de datos del sitio, captura el hash unidireccional de cada nombre de tabla. Este comportamiento garantiza que los nombres de tabla personalizados no sean visibles. Después, Microsoft realiza el mismo proceso de hash unidireccional de los nombres de tabla SQL predeterminados. La comparación de los resultados de las dos consultas determina la desviación del esquema de la base de datos con respecto al valor predeterminado del producto. Después, esta información se usa para mejorar las actualizaciones que requieren cambios en el esquema SQL.  

Cuando se visualizan los datos sin procesar, aparece un valor con código hash común en cada fila de datos. Este código hash es el identificador de la jerarquía. Se usa para poner en correlación los datos con la misma jerarquía sin identificar el cliente o el origen.

### <a name="how-the-one-way-hash-works"></a>Cómo funciona el código hash unidireccional

1. Ejecute la consulta SQL siguiente en SQL Management Studio en la base de datos de Configuration Manager para obtener el identificador de la jerarquía:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Use el script de Windows PowerShell siguiente para establecer el código hash unidireccional del identificador de la jerarquía.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Compare la salida del script con el GUID de los datos sin procesar. En este proceso se muestra cómo se ocultan los datos.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Niveles de datos de uso y diagnóstico](levels-overview.md)
