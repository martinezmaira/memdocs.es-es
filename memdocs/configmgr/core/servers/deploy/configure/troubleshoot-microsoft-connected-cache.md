---
title: Solución de problemas de la caché de conexión
titleSuffix: Configuration Manager
description: Detalles técnicos de la caché de conexión de Microsoft que ayudan a solucionar problemas.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5be6158a2ed7d79af2bee72c81a462e4d83b68e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700873"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Solución de problemas de la caché de conexión de Microsoft en Configuration Manager

En este artículo encontrará detalles técnicos sobre la caché de conexión de Microsoft en Configuration Manager. Úselo como ayuda para solucionar problemas que pueda tener en el entorno. Para más información sobre cómo funciona esta caché y cómo usarla, vea [Caché de conexión de Microsoft en Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> A partir de la versión 1910, esta característica se llama **caché con conexión de Microsoft**. Antes se conocía como “caché en la red de Optimización de distribución (DOINC)”.

## <a name="verify"></a>Comprobar

Cuando se instala correctamente el servidor de caché de optimización de distribución y se configuran los clientes de forma correcta, estos descargan del servidor de caché instalado en el punto de distribución en lugar de hacerlo desde Internet.

Compruebe este comportamiento [en un cliente](#bkmk_verify-client) o [en el servidor](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a> Comprobación en un cliente

1. En un cliente que ejecute Windows 10, versión 1809 o posterior, descargue contenido administrado en la nube. Para más información sobre los tipos de contenido que la caché de conexión admite, vea [Comprobación de la caché de conexión](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Abra PowerShell y ejecute el comando siguiente: `Get-DeliveryOptimizationStatus`

Por ejemplo:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Observe que el atributo `BytesFromCacheServer` no es cero.

Si el cliente no está configurado correctamente o el servidor de caché no está instalado correctamente, el cliente de optimización de distribución recurre al origen en la nube original. Después, el atributo BytesFromCacheServer será cero.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a> Comprobación en el servidor

En primer lugar, compruebe que las propiedades del Registro están configuradas correctamente: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`. Por ejemplo, la ubicación de la caché de unidad es `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`, donde `PrimaryDrivesInput` puede ser varias unidades, por ejemplo `C,D,E`.

Después, use el método siguiente para simular una solicitud de descarga de cliente en el servidor con los encabezados obligatorios.

1. Abra una ventana de PowerShell de 64 bits como administrador.
2. Ejecute el comando siguiente y reemplace el nombre o la dirección IP del servidor por `<DoincServer>`:

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

El resultado es similar al ejemplo siguiente:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Los atributos siguientes indican que la operación se ha realizado correctamente:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Archivos de registro

- Registro de instalación de ARR: `%temp%\arr_setup.log`

- Registro de instalación del servidor de caché de optimización de distribución: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` en el punto de distribución y `DistMgr.log` en el servidor de sitio

- Registros operativos de IIS: De forma predeterminada, `%SystemDrive%\inetpub\logs\LogFiles`

- Registro operativo del servidor de caché de optimización de distribución: `C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Entre otros usos, este registro puede ayudarle a identificar problemas de conectividad con la nube de Microsoft.

## <a name="setup-error-codes"></a>Códigos de error de configuración

Cuando Configuration Manager instala el componente de caché de conexión en el punto de distribución, en la tabla siguiente se enumeran los posibles códigos de error que se pueden producir:

| Código de error | Descripción del error |
|------------|-------------------|
| 0x00000000 | Correcto |
| 0x00000BC2 | Correcto, reinicio necesario |
| 0x00000643 | Error de instalación genérico |
| 0x00D00001 | La configuración de la caché de conexión solo se puede ejecutar si se ha instalado Internet Information Services (IIS). |
| 0x00D00002 | La configuración de la caché de conexión solo se puede ejecutar si existe un "sitio web predeterminado" en el servidor. |
| 0x00D00003 | No se puede instalar la caché de conexión si el Enrutamiento de solicitud de aplicaciones (ARR) ya está instalado. |
| 0x00D00004 | La configuración de la caché de conexión solo se puede ejecutar si Enrutamiento de solicitud de aplicaciones (ARR) se ha instalado con el script install.ps1. |
| 0x00D00005 | La configuración de la caché de conexión requiere una sesión de PowerShell que se ejecute como administrador. |
| 0x00D00006 | La configuración de la caché de conexión solo se puede ejecutar desde un entorno de PowerShell de 64 bits. |
| 0x00D00007 | La configuración de la caché de conexión solo se puede ejecutar en Windows Server. |
| 0x00D00008 | Error: El número de unidades de caché especificadas debe coincidir con el número de porcentajes de tamaño de la unidad de caché especificados |
| 0x00D00009 | Error: Se debe proporcionar un identificador de nodo de caché válido |
| 0x00D0000A | Error: Se debe proporcionar un conjunto de unidades de caché válido |
| 0x00D0000B | Error: Se debe proporcionar un conjunto de porcentaje de tamaño de unidad de caché válido |
| 0x00D0000C | Error: Se debe proporcionar un porcentaje de tamaño de unidad de caché válido o un tamaño de unidad de caché en GB |
| 0x00D0000D | Error: No se puede proporcionar un porcentaje de tamaño de unidad de caché válido y un tamaño de unidad de caché en GB |
| 0x00D0000E | Error: El número de unidades de caché especificadas debe coincidir con el número de tamaño de la unidad de caché en GB especificado |
| 0x00D0000F | Error: No se ha podido realizar una copia de seguridad del archivo applicationhost.config de $AppHostConfig en $AppHostConfigDestinationName |
| 0x00D00010 | Error: No se ha podido realizar una copia de seguridad del archivo web.config del sitio web predeterminado de $WebsiteConfigFilePath en $WebConfigDestinationName |
| 0x00D00011 | Error: Se ha producido una excepción en SetupARRWebFarm.ps1 |
| 0x00D00012 | Error: Se ha producido una excepción en SetupARRWebFarmRewriteRules.ps1 |
| 0x00D00013 | Error: Se ha producido una excepción en SetupARRWebFarmProperties.ps1 |
| 0x00D00014 | Error: Se ha producido una excepción en SetupAllowableServerVariables.ps1 |
| 0x00D00015 | Error: Se ha producido una excepción en SetupFirewallRules.ps1 |
| 0x00D00016 | Error: Se ha producido una excepción en SetupAppPoolProperties.ps1 |
| 0x00D00017 | Error: Se ha producido una excepción en SetupARROutboundRules.ps1 |
| 0x00D00018 | Error: Se ha producido una excepción en SetupARRDiskCache.ps1 |
| 0x00D00019 | Error: Se ha producido una excepción en SetupARRProperties.ps1 |
| 0x00D0001A | Error: Se ha producido una excepción en SetupARRHealthProbes.ps1 |
| 0x00D0001B | Error: Se ha producido una excepción en VerifyIISSItesStarted.ps1 |
| 0x00D0001C | Error: Se ha producido una excepción en SetDrivesToHealthy.ps1 |
| 0x00D0001D | Error: Se ha producido una excepción en VerifyCacheNodeSetup.ps1 |
| 0x00D0001E | No se puede instalar la caché de conexión si el sitio web predeterminado no está en el puerto 80. |
| 0x00D0001F | Error: La asignación de unidad de caché en porcentaje no puede ser superior a 100 |
| 0x00D00020 | Error: La asignación de la unidad de caché en GB no puede superar el espacio libre de la unidad |
| 0x00D00021 | Error: La asignación de unidad de caché en porcentaje debe ser superior a 0 |
| 0x00D00022 | Error: La asignación de la unidad de caché en GB debe ser mayor que 0 |
| 0x00D00023 | Error: Se ha producido una excepción en RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Error: Se ha producido una excepción en RegisterScheduledTask_Maintenance |
| 0x00D00025 | Error: Se ha producido una excepción al configurar las reglas de reescritura para la granja HTTPS: $FarmName |
| 0x00D00026 | Error: Se ha producido una excepción al configurar las reglas de reescritura para la granja HTTP: $FarmName |
| 0x00D00027 | No se puede instalar la caché de conexión porque no se ha podido instalar el software dependiente "Enrutamiento de solicitud de aplicaciones (ARR)". Vea el archivo de registro ubicado en %temp%\arr_setup.log |

## <a name="iis-configurations"></a>Configuraciones de IIS

La instalación del servidor de caché de optimización de distribución realiza varias modificaciones en la configuración de IIS en el punto de distribución.

### <a name="application-request-routing"></a>Enrutamiento de solicitudes de aplicación

El servidor de caché de optimización de distribución instala y configura el [Enrutamiento de solicitud de aplicaciones (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) de IIS. Para evitar posibles conflictos, este componente no debe estar ya instalado en el punto de distribución.

### <a name="allowed-server-variables"></a>Variables de servidor permitidas

Después de instalar el servidor de caché de optimización de distribución, el sitio web predeterminado tiene las siguientes variables de servidor *locales*:

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>Reglas de reescritura

El servidor de caché de optimización de distribución agrega las reglas de reescritura siguientes:

#### <a name="inbound-rewrite-rules"></a>Reglas de reescritura de entrada

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Reglas de reescritura de salida

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Administración de recursos del servidor

El espacio en disco necesario para cada servidor de caché de optimización de distribución puede variar en función de los requisitos de actualización de la organización. 100 GB deben ser espacio suficiente para almacenar en caché el contenido siguiente:

- Una actualización de características
- De dos a tres meses de actualizaciones de calidad y de Office
- Aplicaciones de Microsoft Intune y aplicaciones de Bandeja de entrada de Windows

El servidor de caché de optimización de distribución no debe consumir mucho tiempo de procesador o memoria del sistema. Después de instalar el servidor de caché de optimización de distribución, si observa un consumo significativo de recursos de memoria o de procesos, analice los archivos de registro de IIS y ARR.

Si los archivos de registro de IIS y ARR ocupan demasiado espacio en el servidor, puede usar varios métodos para administrar esos archivos. Para más información, vea [Administración del almacenamiento de archivos de registro de IIS](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Vea también

[Caché de conexión de Microsoft en Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
