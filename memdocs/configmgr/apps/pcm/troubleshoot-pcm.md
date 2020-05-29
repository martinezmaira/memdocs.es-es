---
title: Solución de problemas del Administrador de conversión de paquetes
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas con el Administrador de conversión de paquetes en Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877619"
---
# <a name="troubleshoot-package-conversion-manager"></a>Solución de problemas del Administrador de conversión de paquetes

*Se aplica a: Configuration Manager (rama actual)*

<!--1357861-->

Use la información de este artículo para facilitar la solución de problemas de uso del Administrador de conversión de paquetes.



## <a name="sms-provider"></a>Proveedor de SMS

El Administrador de conversión de paquetes utiliza el proveedor de SMS. Para más información, vea [Plan for the SMS Provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Planear el proveedor de SMS).

Si el proveedor de SMS no funciona correctamente, la consola de Configuration Manager, incluido el Administrador de conversión de paquetes, no funcionará.



## <a name="package-readiness"></a>Preparación del paquete

Antes de convertir un paquete en una aplicación, analice el paquete con la función **Analizar** del Administrador de conversión de paquetes. Después del análisis, agregue la columna **Preparación** en el nodo **Paquetes** de la consola de Configuration Manager. La lista de paquetes muestra uno de los siguientes estados de preparación del paquete analizado:

- **Automático**: el paquete se puede convertir directamente con la función **Convertir**.      

  > [!NOTE]  
  > Una conversión automática no convierte las consultas WQL en requisitos de la aplicación. Use el proceso **Corregir y convertir** para convertir estas consultas.  

- **Manual**: el paquete necesita algunas adiciones o cambios para poderlo convertir con la función **Corregir y convertir**.  

- **No aplicable**: el paquete no es adecuado para la conversión. Corrija cualquier problema con el paquete o siga implementándolo como un paquete.  

- **Error**: el paquete contiene errores. Corrija estos errores manualmente para poder analizarlo y convertirlo.  

En el panel de detalles del nodo **Paquetes** de la consola de Configuration Manager se muestran los problemas de preparación. Seleccione un paquete y después la pestaña **Resumen** del panel de detalles.



## <a name="log-files"></a>Archivos de registro

### <a name="enable-logging"></a>Habilitar registro

Al habilitar el registro para el Administrador de conversión de paquetes, se registran todas sus acciones, excepciones y errores.

Para habilitar el registro para este componente en Configuration Manager, modifique **Microsoft.ConfigurationManagement.exe.Config**. De forma predeterminada, este archivo de configuración se encuentra en la ruta de acceso siguiente:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> A partir de la versión 1910, esta ruta de acceso cambió para usar la carpeta `Microsoft Endpoint Manager`. Asegúrese de que no usa una versión anterior del archivo que pudiera existir en otra carpeta.

Inserte los siguientes elementos XML **switches** y **trace** en el elemento **system.diagnostics** después del último elemento **sources**:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Este ejemplo usa el archivo **PCMTrace.log**. Este registro se encuentra en el equipo que ejecuta la consola de Configuration Manager en la siguiente ruta de acceso:  
`%UserProfile%\AppData\Local\Temp`

Para cambiar el nivel de detalle, cambie la configuración del modificador trace **PcmLogging**. Establezca este valor en cuatro niveles de detalle, desde el menos detallado (`1`) hasta el más detallado (`4`).


### <a name="smsprovlog"></a>SMSProv.log

En algunas situaciones, la información relevante para solucionar problemas en el proceso de conversión de paquetes se encuentra en el archivo **SMSProv.log**. Este archivo captura información del proveedor de SMS de Configuration Manager.

De forma predeterminada, este archivo de registro se encuentra en el servidor de sitio de Configuration Manager en la siguiente ruta de acceso:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Si ve alguno de los siguientes mensajes de error, el archivo **SMSProv.log** puede contener información de solución de problemas pertinente:

- `The SMS Provider reported an error`

- `Generic Failure`

Normalmente, estos mensajes de error indican que se produjo un error en el servidor de sitio y que la información de error no se envió a la consola de Configuration Manager.

Para más información, vea [Referencia técnica de mensajes de error del Administrador de conversión de paquetes](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Cambiar atributos de paquete después del análisis

Una vez que se analiza un paquete y tiene un estado de preparación asignado de **automático** o **manual**, si se cambia cualquiera de los atributos pertinentes, el proceso de conversión puede producir un error.

Por ejemplo, analiza un paquete y su estado de preparación es **automático**. A continuación, agregue otro programa al paquete. La conversión del paquete puede presentar errores.

Si necesita realizar cambios en un paquete después del análisis, vuelva a ejecutar el análisis antes de la conversión. 



## <a name="see-also"></a>Vea también

[Referencia técnica de mensajes de error del Administrador de conversión de paquetes](error-messages.md)
