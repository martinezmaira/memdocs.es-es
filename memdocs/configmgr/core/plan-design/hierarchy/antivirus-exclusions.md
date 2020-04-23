---
title: Exclusiones del antivirus
titleSuffix: Configuration Manager
description: Aprenda sobre las exclusiones del antivirus recomendadas que se pueden usar para solucionar posibles problemas.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703743"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Exclusiones del antivirus recomendadas para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo contiene recomendaciones que pueden ayudar a los administradores a determinar la causa de la posible inestabilidad de un equipo donde se ejecuta una versión compatible de los servidores de sitios, sistemas de sitios y clientes de Configuration Manager cuando se usa en combinación con software antivirus.

> [!IMPORTANT]
>
> - Se recomienda aplicar temporalmente estos procedimientos para evaluar un sistema. Si el rendimiento o la estabilidad del sistema se mejoran con las recomendaciones que se realizan en este artículo, póngase en contacto con el proveedor de software antivirus para que le proporcione indicaciones o una versión actualizada del software antivirus.
> - Este artículo contiene información que muestra cómo ayudar a reducir la configuración de seguridad o cómo desactivar temporalmente las características de seguridad en un equipo. Puede realizar estos cambios para comprender la naturaleza de un problema específico. Sin embargo, antes de realizarlos, se recomienda evaluar los riesgos asociados a la implementación de esta solución temporal en su entorno concreto.

## <a name="possible-symptoms"></a>Posibles síntomas 

La protección antivirus en tiempo real puede ocasionar muchos problemas en los servidores de sitios, sistemas de sitios y clientes de Configuration Manager.

A continuación se muestra una lista no exhaustiva de los posibles síntomas:

- Los componentes del sistema de sitio remoto no están instalados. SiteComp.log, Distmgr.log, hman.log u otros archivos de registro de Configuration Manager pueden contener errores, como es el caso del error 80070005.
- No se puede instalar el cliente de Configuration Manager mediante la inserción del cliente.
- La información del inventario de cliente es inexacta, no se encuentra o no está actualizada.
- Los trabajos pendientes tienen lugar en las carpetas *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes.
- El centro de software no se ha rellenado con el software implementado en los sistemas cliente o no se inicia. Además, el archivo CCMRepair.log puede contener errores como los de este ejemplo:

  > Error de comprobación de la base de datos con el resultado: 0x80004005, pero la base de datos: C:\Windows\CCM\filename.sdf se podía abrir; se omitirá la reparación de la base de datos.

- No se puede instalar el software que está implementado en los clientes.
- Los datos de cumplimiento de las implementaciones de software son inexactos.

## <a name="exclusions"></a>Exclusiones

Para evitar estos problemas, se recomienda agregar las siguientes exclusiones de protección en tiempo real:

### <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

|  |  |
| - | - |
|*Carpeta de instalación de Configuration Manager*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*Carpeta de instalación de MP*  |%ProgramFiles%\SMS_CCM  |  
|*Carpeta de instalación del cliente*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Exclusiones de carpetas para servidores de sitios

- *Carpeta de instalación de Configuration Manager*\Inboxes
- *Carpeta de instalación de Configuration Manager*\Logs
- *Carpeta de instalación de Configuration Manager*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>Exclusiones de carpetas para sistemas de sitios

- Puntos de administración
  - *Carpeta de instalación de MP*\ServiceData
  - Cualquiera de las siguientes:
    - *Carpeta de instalación de Configuration Manager*\MP\OUTBOXES
    - *Unidad de instalación*\SMS\MP\OUTBOXES
- Puntos de distribución
  - *Carpeta de instalación del cliente*\ServiceData
  - *ContentLib_Drive*\SMS_DP$
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- Servidores de bases de datos del sitio
  - [Cómo elegir el software antivirus que se ejecutará en los equipos con SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Exclusiones de carpetas para clientes

- *Carpeta de instalación del cliente*\\\*.sdf
- *Carpeta de instalación del cliente*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Carpeta de instalación del cliente*\Logs

### <a name="file-exclusions-for-mps"></a>Exclusiones de archivos para los MP

- POL00000.pol in
  - *Carpeta de instalación de MP*\PolReqStaging

### <a name="process-exclusions"></a>Exclusiones de procesos

Las exclusiones de procesos solo son necesarias si los programas antivirus agresivos consideran que los archivos de programa de Configuration Manager (archivos .exe) son procesos de alto riesgo.

- *Carpeta de instalación de Configuration Manager*\bin\64\Smsexec.exe
- Elija uno de los siguientes procesos:
  - *Carpeta de instalación del cliente*\Ccmexec.exe
  - *Carpeta de instalación de MP*\Ccmexec.exe
- *Carpeta de instalación del cliente*\CmRcService.exe (lado cliente)
- *Carpeta de instalación de Configuration Manager*\bin\64\Sitecomp.exe
- *Carpeta de instalación de Configuration Manager*\bin\64\Smswriter.exe
- *Carpeta de instalación de Configuration Manager*\bin\64\Smssqlbkup.exe o SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *Carpeta de instalación de Configuration Manager*\bin\64\Cmupdate.exe
- *Carpeta de instalación del cliente*\Ccmrepair.exe (lado cliente)
- %*windir*%\CCMSetup\Ccmsetup.exe (lado cliente)

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las exclusiones del antivirus, consulte los artículos siguientes:

[Exclusiones del antivirus de la rama actual de Configuration Manager: blog de ingenieros de campo de System Center Premier](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[Actualización de exclusiones del antivirus de System Center 2012 Configuration Manager con más información sobre las imágenes OSD y de arranque](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[Cómo elegir el software antivirus que se ejecutará en los equipos con SQL Server](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Recomendaciones de detección de virus para equipos empresariales que ejecutan versiones de Windows admitidas actualmente](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
