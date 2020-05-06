---
title: Registros de eventos de los clientes
titleSuffix: Configuration Manager
description: Referencia técnica de las posibles entradas del cliente de BitLocker (MBAM) en el registro de eventos de Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705973"
---
# <a name="client-event-logs"></a>Registros de eventos de los clientes

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Si ha implementado una directiva de administración de BitLocker en un cliente de Configuration Manager, use el Visor de eventos de Windows para ver los registros de eventos del cliente de BitLocker. Vaya a **Registros de aplicaciones y servicios**, **Microsoft**, **Windows**, **MBAM** para consultar los registros de eventos de [Administración](#admin) y [Operativos](#operational).

## <a name="admin"></a>Administración

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Error al aplicar las directivas de MBAM.

#### <a name="error-code--2144272219"></a>Código de error: -2144272219

Detalles: El cifrado de unidad BitLocker únicamente admite el cifrado solo en espacio utilizado en el almacenamiento aprovisionado fino.

Este error se produce si intenta usar BitLocker para cifrar una máquina virtual que ejecuta Windows 10, versión 1803 o anteriores. Las versiones anteriores de Windows 10 no admiten el cifrado de disco completo. Las directivas de administración de BitLocker aplican el cifrado de disco completo.

#### <a name="error-code--2147024774"></a>Código de error: -2147024774

Detalles: El área de datos que se pasa a una llamada del sistema es demasiado pequeña.

Para resolver este problema, reinicie el equipo.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Error al enviar datos de estado de cifrado.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Falta el volumen del sistema. Se necesita el volumen del sistema para cifrar la unidad del sistema operativo.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

Falta el hardware de TPM. Se necesita TPM para cifrar la unidad del sistema operativo con algún protector TPM.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

El equipo está exento de cifrado. Estado del hardware de la máquina: exento

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

El equipo está exento de cifrado. Estado del hardware de la máquina: Unknown

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Error de comprobación de exención de hardware.

### <a name="13-userisexempted"></a>13: UserIsExempted

El usuario está exento de cifrado.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

El usuario ha solicitado una exención.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Error de comprobación de exención de usuario.

### <a name="16-userpostponed"></a>16: UserPostponed

El usuario ha aplazado el proceso de cifrado.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

Error de inicialización de TPM. El usuario ha rechazado los cambios en el BIOS.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

No se puede conectar con el Servicio de recuperación y hardware de MBAM.

#### <a name="error-code--2147024809"></a>Código de error: -2147024809

Detalles: El parámetro es incorrecto.

Este error se produce si el sitio web no es HTTPS o si el cliente no tiene un certificado PKI.

### <a name="20-policymismatch"></a>20: PolicyMismatch

La directiva de administración de BitLocker está en conflicto o dañada.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Se ha detectado un conflicto de directivas de cifrado del volumen del sistema operativo. Compruebe las directivas de BitLocker relacionadas con los protectores de la unidad del sistema operativo.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Se ha detectado un conflicto de directivas de cifrado del volumen de la unidad de datos fija. Compruebe las directivas de BitLocker relacionadas con los protectores de la unidad de datos fija.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Se ha producido un error durante el cifrado. Se necesita un protector de Agente de recuperación de datos (DRA) en modo FIPS para equipos que ejecuten versiones de Windows anteriores a la 8.1.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

No se pudo restablecer el bloqueo de TPM.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

No se pudo recuperar el valor OwnerAuth de TPM de los servicios MBAM.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

No se pudo actualizar la ruta de búsqueda de DLL para el proveedor de WMI.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

El agente se detiene. Se agotó el tiempo de espera de la instancia del proveedor de WMI de MBAM.

## <a name="operational"></a>Operativo

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

Las directivas de administración de BitLocker se aplicaron correctamente.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

Los datos de estado de cifrado se han enviado correctamente.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Conexión establecida correctamente con el Servicio de recuperación y hardware de MBAM.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

Se ha custodiado el valor OwnerAuth de TPM.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

Se ha custodiado la clave de recuperación de BitLocker del volumen.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

Se ha actualizado la clave de recuperación de BitLocker del volumen.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

Se ha establecido la fecha de aplicación de la directiva del volumen.

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

Se ha borrado la fecha de aplicación de la directiva del volumen.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

Se restableció correctamente el bloqueo de TPM.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

Se recuperó correctamente el valor OwnerAuth de TPM de los servicios MBAM.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

Se montó la unidad extraíble.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

Se desmontó la unidad extraíble.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

El error al conectar con el servicio de recuperación y hardware de MBAM impidió que las directivas de administración de BitLocker se aplicaran correctamente al volumen.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

El estado de volumen bloqueado impidió que las directivas de administración de BitLocker se aplicaran correctamente al volumen.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

El error al conectar con el servicio de cumplimiento y estado de MBAM impidió la transferencia de datos de estado de cifrado.

## <a name="see-also"></a>Vea también

Para obtener más información sobre el uso de estos registros, vea [Registros de eventos de BitLocker](about-event-logs.md).

Para obtener más información acerca de la solución de problemas, vea [Solución de problemas de BitLocker](troubleshoot.md).
