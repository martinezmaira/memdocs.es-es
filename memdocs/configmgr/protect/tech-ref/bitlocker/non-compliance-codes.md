---
title: Códigos de no conformidad
titleSuffix: Configuration Manager
description: Referencia técnica de los posibles códigos de un cliente de Configuration Manager que no es compatible con la directiva de BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705963"
---
# <a name="non-compliance-codes"></a>Códigos de no conformidad

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

WMI en el cliente proporciona los siguientes códigos de no conformidad. Además, describe las razones por las que un dispositivo determinado se notifica como no conforme.

Existen varios métodos para visualizar WMI. Por ejemplo, utilice el siguiente comando de PowerShell:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Si el dispositivo es conforme, este comando no devuelve nada.
>
> También se puede comprobar el atributo `Compliant` de esta clase, que es `1` si el dispositivo es conforme.

|Código de no compatibilidad|Motivo de no compatibilidad|
|--- |--- |
|0|Intensidad de cifrado distinta de AES 256.|
|1|La directiva de BitLocker requiere que este volumen esté cifrado, pero no lo está.|
|2|La directiva de BitLocker requiere que este volumen *no* esté cifrado, pero lo está.|
|3|La directiva de BitLocker requiere que este volumen use un protector TPM, pero lo hace.|
|4|La directiva de BitLocker requiere que este volumen use un protector TPM y un PIN, pero lo hace.|
|5|La directiva de BitLocker no permite que las máquinas que no son TPM se notifiquen como conformes.|
|6|El volumen tiene un protector TPM, pero TPM no está visible.|
|7|La directiva de BitLocker requiere que este volumen use un protector de contraseña, pero no tiene ninguno.|
|8|La directiva de BitLocker requiere que este volumen *no* use un protector de contraseña, pero tiene uno.|
|9|La directiva de BitLocker requiere que este volumen use un protector de desbloqueo automático, pero no tiene ninguno.|
|10|La directiva de BitLocker requiere que este volumen *no* use un protector de desbloqueo automático, pero tiene uno.|
|11|BitLocker detecta un conflicto de directivas, lo que le impide notificar este volumen como conforme.|
|12|Se necesita un volumen del sistema para cifrar el volumen del sistema operativo, pero no está presente.|
|13|Se ha suspendido la protección para el volumen.|
|14|El protector de desbloqueo automático no es seguro, a menos que el volumen del sistema operativo esté cifrado.|
|15|La directiva requiere que la intensidad de cifrado mínima sea XTS-AES-128 bits, pero la intensidad de cifrado real es más débil.|
|16|La directiva requiere que la intensidad de cifrado mínima sea XTS-AES-256 bits, pero la intensidad de cifrado real es más débil.|
