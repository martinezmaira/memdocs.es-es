---
title: Modo de aprovisionamiento
titleSuffix: Configuration Manager
description: Obtenga información sobre el modo de aprovisionamiento de cliente durante la secuencia de tareas de Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 815b32ecf7e9cd315c2365cb5ed73004b2a48718
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708653"
---
# <a name="provisioning-mode"></a>Modo de aprovisionamiento

*Se aplica a: Configuration Manager (rama actual)*

Durante una secuencia de tareas de implementación de sistema operativo, Configuration Manager cambia el cliente al modo de aprovisionamiento. (Una secuencia de tareas de implementación de sistema operativo incluye la actualización local a Windows 10). En este estado, el cliente no procesa la directiva desde el sitio. Este comportamiento permite que la secuencia de tareas se ejecute sin riesgo de implementaciones adicionales que se ejecutan en el cliente. Cuando la secuencia de tareas se completa, ya sea de forma correcta o con errores controlados, finaliza el modo de aprovisionamiento de cliente.

Si se produce un error inesperado en la secuencia de tareas, el cliente puede quedarse en modo de aprovisionamiento. Por ejemplo, si el dispositivo se reinicia en medio del procesamiento de una secuencia de tareas y no se puede recuperar. Un administrador debe identificar y corregir manualmente los clientes que tienen este estado.


## <a name="manually-remove-provisioning-mode"></a>Eliminación manual del modo de aprovisionamiento

Si un cliente se deja en el modo de aprovisionamiento, siga este proceso manual para restaurarlo a su funcionamiento normal.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Entre otros, uno de los cambios que realiza este método WMI consiste en establecer un valor del Registro. El simple hecho de cambiar el valor del Registro no quita al cliente por completo del modo de aprovisionamiento. Si edita manualmente el Registro, el cliente podría mostrar comportamientos inesperados.  


## <a name="client-provisioning-mode-timeout"></a>Tiempo de espera del modo de aprovisionamiento de cliente

A partir de la versión 1902, la secuencia de tareas establece una marca de tiempo cuando coloca el cliente en modo de aprovisionamiento. Cada 60 minutos, un cliente en modo de aprovisionamiento comprueba la duración del tiempo transcurrido desde la marca de tiempo. Si ha estado en modo de aprovisionamiento durante más de 48 horas, el cliente sale del modo de aprovisionamiento automáticamente y reinicia el proceso.

48 horas es el valor predeterminado de tiempo de espera del modo de aprovisionamiento. Puede ajustar este temporizador en un dispositivo estableciendo el valor **ProvisioningMaxMinutes** en la siguiente clave del Registro: `HKLM\Software\Microsoft\CCM\CcmExec`. Si este valor no existe o es `0`, el cliente usa el valor predeterminado de 48 horas.

La marca de tiempo **ProvisioningEnabledTime** se encuentra en la siguiente clave del Registro: `HKLM\Software\Microsoft\CCM\CcmExec`. El valor de la marca de tiempo es la última vez que el equipo haya entrado en modo de aprovisionamiento. El formato es época (marca de tiempo de UNIX) y está en UTC.

Esta marca de tiempo también se restablece en la hora actual cuando se coloca manualmente el equipo en modo de aprovisionamiento mediante el comando siguiente:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Diagramas de flujo del proceso

En estos diagramas se muestra el flujo del proceso para la secuencia de tareas y el cliente.

### <a name="task-sequence"></a>Secuencia de tareas

En el diagrama siguiente se muestra la manera en que la secuencia de tareas establece el modo de aprovisionamiento:

![Diagrama de flujo de una secuencia de tareas que establece el modo de aprovisionamiento](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Corrección de cliente

En el diagrama siguiente se muestra la manera en que el cliente sale del modo de aprovisionamiento:

![Diagrama de flujo de un cliente que sale del modo de aprovisionamiento](media/3197824-client-flow.png)


## <a name="see-also"></a>Vea también

[Instalar Windows y Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Actualizar el sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS)
