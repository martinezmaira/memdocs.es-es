---
title: Referencia de la configuración de BitLocker
titleSuffix: Configuration Manager
description: Toda la configuración de administración de BitLocker disponible en Configuration Manager
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b52fe5a60899d7e871381d1a34a2360bbe68a36c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820483"
---
# <a name="bitlocker-settings-reference"></a>Referencia de la configuración de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!-- 5925683 -->

Las directivas de administración de BitLocker incluidas en Configuration Manager contienen los siguientes grupos de directivas:

- Configurar
- Unidad de sistema operativo
- Unidad fija
- Unidad extraíble
- Administración de cliente

En las secciones siguientes se describen y se sugieren opciones para la configuración de cada grupo.

> [!NOTE]
> Esta configuración se basa en la versión 2002 de Configuration Manager. La versión 1910 no incluye todas estas opciones.

## <a name="setup"></a>Configurar

Mediante las opciones de esta página se configuran las opciones de cifrado globales de BitLocker.

### <a name="drive-encryption-method-and-cipher-strength"></a>Método de cifrado de unidades e intensidad de cifrado

*Configuración sugerida*: **Habilitado** con el método de cifrado predeterminado o superior.

> [!NOTE]
> En la página de propiedades **Configuración** se incluyen dos grupos de opciones para diferentes versiones de Windows. En esta sección se describen ambos grupos.

#### <a name="windows-81-devices"></a>Dispositivos Windows 8.1

Para dispositivos Windows 8.1, habilite la opción **Método de cifrado de unidades e intensidad de cifrado** y seleccione uno de los métodos de cifrado siguientes:

- AES, 128 bits con difusor
- AES, 256 bits con difusor
- AES, 128 bits (valor predeterminado)
- AES de 256 bits

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMBLEncryptionMethodPolicy](/powershell/module/configurationmanager/new-cmblencryptionmethodpolicy?view=sccm-ps).

#### <a name="windows-10-devices"></a>Dispositivos Windows 10

En el caso de los dispositivos Windows 10, habilite la opción **Método de cifrado de unidades e intensidad de cifrado (Windows 10)** . A continuación, seleccione individualmente uno de los métodos de cifrado siguientes para las unidades de sistema operativo, las unidades de datos fijas y las unidades de datos extraíbles:

- AES-CBC, 128 bits
- AES-CBC, 256 bits
- XTS-AES, 128 bits (valor predeterminado)
- XTS-AES, 256 bits

> [!TIP]
> BitLocker usa el Estándar de cifrado avanzado (AES) como algoritmo de cifrado con longitudes de claves configurables de 128 o 256 bits. En los dispositivos Windows 10, el cifrado AES admite el encadenamiento de bloques de cifrado (CBC) o el robo de texto cifrado (XTS).
>
> Si necesita usar una unidad extraíble en dispositivos que no ejecutan Windows 10, use AES-CBC.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMBLEncryptionMethodWithXts](/powershell/module/configurationmanager/new-cmblencryptionmethodwithxts?view=sccm-ps).

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Notas de uso general del cifrado de unidades y su intensidad

- Si deshabilita o no establece esta configuración, BitLocker usará el método de cifrado predeterminado.

- Configuration Manager aplica esta configuración al activar BitLocker.

- Si la unidad ya está cifrada o está en proceso de estarlo, cualquier cambio en esta configuración de directiva no cambiará el cifrado de unidades en el dispositivo.

- Si usa el valor predeterminado, puede que el informe de cumplimiento del equipo de BitLocker muestre la intensidad de cifrado como **desconocida**. Para que esto no suceda, habilite esta configuración e indique un valor explícito para la intensidad de cifrado.

### <a name="prevent-memory-overwrite-on-restart"></a>Impedir la sobrescritura de memoria al reiniciar

*Configuración sugerida*: **No configurado**.

Configure esta directiva para mejorar el rendimiento de reinicio sin sobrescribir secretos de BitLocker en la memoria al reiniciar.

Si no se configura esta directiva, BitLocker quita sus secretos de la memoria cuando se reinicia el equipo.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMNoOverwritePolicy](/powershell/module/configurationmanager/new-cmnooverwritepolicy?view=sccm-ps).

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Validar el cumplimiento de reglas de uso de certificados de tarjetas inteligentes

*Configuración sugerida*: **No configurado**.

Configure esta directiva para utilizar la protección de BitLocker basada en certificados de tarjeta inteligente. A continuación, especifique el certificado **Identificador de objeto**.

Si no se configura esta directiva, BitLocker usa el identificador de objeto predeterminado `1.3.6.1.4.1.311.67.1.1` para especificar un certificado.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMScCompliancePolicy](/powershell/module/configurationmanager/new-cmsccompliancepolicy?view=sccm-ps).

### <a name="organization-unique-identifiers"></a>Identificadores únicos de la organización

*Configuración sugerida*: **No configurado**.

Configure esta directiva para utilizar un agente de recuperación de datos basado en certificados o el Lector de BitLocker To Go.

Si no se configura esta directiva, BitLocker no usa el campo de **Identificación**.

Si su organización requiere más medidas de seguridad, configure el campo **Identificación**. Establezca este campo en todos los dispositivos USB de destino y alinéelo con esta configuración.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMUidPolicy](/powershell/module/configurationmanager/new-cmuidpolicy?view=sccm-ps).

## <a name="os-drive"></a>Unidad de sistema operativo

Mediante las opciones de esta página se configuran las opciones de cifrado para la unidad en la que está instalado Windows.

### <a name="operating-system-drive-encryption-settings"></a>Configuración de cifrado de la unidad del sistema operativo

*Configuración sugerida*: **Habilitado**

si habilita esta opción, el usuario tiene que proteger la unidad del sistema operativo y BitLocker cifra la unidad. Si la deshabilita, el usuario no puede proteger la unidad. Si no configura esta directiva, no se requiere la protección de BitLocker en la unidad de sistema operativo.

> [!NOTE]
> Si la unidad ya está cifrada y deshabilita esta configuración, BitLocker descifra la unidad.  

Si tiene dispositivos sin un [Módulo de plataforma segura (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-top-node), use la opción **Permitir BitLocker sin un TPM compatible (requiere una contraseña)** . Esta configuración permite que BitLocker cifre la unidad de sistema operativo, incluso aunque el dispositivo no tenga un TPM. Si permite esta opción, Windows solicitará al usuario que especifique una contraseña de BitLocker.

En dispositivos con un TPM compatible, se pueden usar dos tipos de métodos de autenticación durante el inicio para ofrecer una protección adicional para los datos cifrados. Cuando se inicia el equipo, se puede utilizar únicamente el TPM para la autenticación o también se puede requerir la entrada de un número de identificación personal (PIN). Configure las siguientes opciones:

- **Select protector for operating system drive** (Seleccionar protector para la unidad del sistema operativo): configúrelo para usar un TPM y PIN, o simplemente el TPM.

- **Configurar longitud mínima de PIN para el inicio**: si necesita un PIN, este valor es la longitud más corta que el usuario puede especificar. El usuario escribe este PIN cuando arranca el equipo para desbloquear la unidad. De forma predeterminada, la longitud de PIN mínima es de `4`.

> [!TIP]
> Para una mayor seguridad, al habilitar dispositivos con el protector TPM + PIN, considere la posibilidad de *deshabilitar* la configuración de directiva de grupo siguiente en **Sistema** > **Administración de energía** > **Configuración de suspensión**:
>
> - Permitir estados de espera (S1-S3) mientras el equipo está en suspensión (conectado)
>
> - Permitir estados de espera (S1-S3) mientras el equipo está en suspensión (con batería)

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMBMSOSDEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsosdencryptionpolicy?view=sccm-ps).

### <a name="allow-enhanced-pins-for-startup"></a>Permitir PIN de inicio mejorados

*Configuración sugerida*: **No configurado**.

Configure BitLocker para usar PIN de inicio mejorados. Estos PIN permiten el uso de caracteres adicionales, como letras mayúsculas y minúsculas, símbolos, números y espacios. Esta configuración se aplica al activar BitLocker.

> [!IMPORTANT]
> No todos los equipos pueden admitir PIN mejorados en el entorno previo al arranque. Antes de habilitar su uso, evalúe si los dispositivos admiten esta característica.

Si habilita esta configuración, todos los PIN de inicio de BitLocker nuevos permitirán que el usuario cree PIN mejorados.

- **Requerir PIN solo de ASCII**: Ayude a que los PIN mejorados sean más compatibles con los equipos que limitan el tipo o el número de caracteres que se pueden especificar en el entorno previo al arranque.

Si deshabilita o no establece esta configuración de directiva, BitLocker no usará PIN mejorados.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMEnhancedPIN](/powershell/module/configurationmanager/new-cmenhancedpin?view=sccm-ps).

### <a name="operating-system-drive-password-policy"></a>Directiva de contraseñas de controlador de sistema operativo

*Configuración sugerida*: **No configurado**.

Use esta configuración para establecer las restricciones de las contraseñas con el fin de desbloquear las unidades de sistema operativo protegidas por BitLocker. Si permite protectores que no son TPM en unidades de sistema operativo, configure las opciones siguientes:

- **Configure la complejidad de las contraseñas para las unidades de sistema operativo**: Para requerir el cumplimiento de los requisitos de complejidad, seleccione **Requerir complejidad de la contraseña**.

- **Longitud mínima de la contraseña para unidades de sistema operativo**: De forma predeterminada, la longitud mínima es de `8`.

- **Requerir contraseñas solo de ASCII para unidades de sistema operativo extraíbles**

Si habilita esta configuración de directiva, los usuarios pueden configurar una contraseña que cumpla los requisitos que se hayan definido.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMOSPassphrase](/powershell/module/configurationmanager/new-cmospassphrase?view=sccm-ps).

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Notas de uso general de la directiva de contraseñas de unidades de sistema operativo

- Para que la configuración de los requisitos de complejidad sea eficaz, habilite también la configuración de directiva de grupo **Las contraseñas deben cumplir los requisitos de complejidad**, que se encuentra en **Configuración del equipo** > **Configuración de Windows** > **Configuración de seguridad** > **Directivas de cuenta** > **Directiva de contraseñas**.

- BitLocker aplica esta configuración al activarlo, no al desbloquear un volumen. BitLocker permite desbloquear una unidad con cualquiera de los protectores que están disponibles en la unidad.

- Si usa la directiva de grupo para habilitar los algoritmos compatibles con FIPS para el cifrado, el uso de hash y la firma, no puede permitir que las contraseñas actúen como un protector de BitLocker.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Restablecer los datos de validación de plataforma tras la recuperación de BitLocker

*Configuración sugerida*: **No configurado**.

Controle si Windows actualiza los datos de validación de plataforma cuando se inicia después de la recuperación de BitLocker.

Si habilita o no establece esta configuración, Windows actualizará los datos de validación de plataforma en esta situación.

Si deshabilita esta configuración de directiva, Windows no actualizará los datos de validación de plataforma en esta situación.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMTpmAutoResealPolicy](/powershell/module/configurationmanager/new-cmtpmautoresealpolicy?view=sccm-ps).

### <a name="pre-boot-recovery-message-and-url"></a>URL y mensaje de recuperación previos al arranque

*Configuración sugerida*: **No configurado**.

Si BitLocker bloquea la unidad de sistema operativo, use esta configuración para mostrar un mensaje de recuperación personalizado o una dirección URL en la pantalla de recuperación de BitLocker previa al arranque. Esta configuración solo se aplica a dispositivos Windows 10.

Al habilitar esta configuración, seleccione una de las opciones siguientes para el mensaje de recuperación previo al arranque:

- **Usar la dirección URL y el mensaje de recuperación predeterminados**: Muestre el mensaje de recuperación de BitLocker y la dirección URL predeterminados en la pantalla de recuperación de BitLocker previa al arranque. Si anteriormente ha configurado un mensaje de recuperación o una dirección URL personalizados, use esta opción para revertir al mensaje predeterminado.

- **Usar un mensaje de recuperación personalizado**: Incluya un mensaje personalizado en la pantalla de recuperación de BitLocker previa al arranque.

  - **Opción de mensaje de recuperación personalizado**: Escriba el mensaje personalizado que se va a mostrar. Si también quiere especificar una dirección URL de recuperación, inclúyala como parte de este mensaje de recuperación personalizado. La longitud de cadena máxima es de 32 768 caracteres.

- **Usar una dirección URL de recuperación personalizada**: Reemplace la dirección URL predeterminada que se muestra en la pantalla de recuperación de BitLocker previa al arranque.

  - **Opción de dirección URL de recuperación personalizada**: Escriba la dirección URL que se va a mostrar. La longitud de cadena máxima es de 32 768 caracteres.

> [!NOTE]
> No se admiten todos los caracteres y idiomas en el entorno previo al arranque. Primero pruebe el mensaje o la dirección URL personalizados para asegurarse de que aparezca correctamente en la pantalla de recuperación de BitLocker previa al arranque.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMPrebootRecoveryInfo](/powershell/module/configurationmanager/new-cmprebootrecoveryinfo?view=sccm-ps).

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Configuración de cumplimiento de directiva de cifrado (unidad de sistema operativo)

*Configuración sugerida*: **Habilitado**

Configure el número de días que los usuarios pueden posponer el cumplimiento de BitLocker para la unidad de sistema operativo. El **período de gracia de no cumplimiento** comienza cuando Configuration Manager lo detecta como no conforme por primera vez. Una vez expirado el período de gracia, los usuarios no pueden posponer la acción requerida ni solicitar una exención.

Si el proceso de cifrado requiere una entrada de usuario, se abrirá un cuadro de diálogo en Windows que el usuario no podrá cerrar hasta que introduzca la información necesaria. Las futuras notificaciones de errores o estados no tendrán esta restricción.

Si BitLocker no requiere la interacción del usuario para agregar un protector, una vez expirado el período de gracia, BitLocker inicia el cifrado en segundo plano.

Si deshabilita o no establece esta configuración, Configuration Manager no requerirá que los usuarios cumplan las directivas de BitLocker.

Para aplicar la directiva inmediatamente, establezca un período de gracia de `0`.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMUseOsEnforcePolicy](/powershell/module/configurationmanager/new-cmuseosenforcepolicy?view=sccm-ps).

## <a name="fixed-drive"></a>Unidad fija

Mediante las opciones de esta página se configura el cifrado de unidades de datos adicionales de un dispositivo.

### <a name="fixed-data-drive-encryption"></a>Cifrado de unidades de datos fijas

*Configuración sugerida*: **Habilitado**

Administre el requisito de cifrado de unidades de datos fijas. Si habilita esta configuración, BitLocker requerirá que los usuarios pongan todas las unidades de datos fijas bajo protección. A continuación, cifrará las unidades de datos.

Al habilitar esta directiva, habilite el desbloqueo automático o la configuración **Directiva de contraseñas de unidades de datos fijas**.

- **Configurar el desbloqueo automático para la unidad de datos fija**: Permita o requiera que BitLocker desbloquee automáticamente cualquier unidad de datos cifrada. Para usar el desbloqueo automático, también es necesario que BitLocker cifre la [unidad de sistema operativo](#os-drive).

Si no establece esta configuración, BitLocker no requerirá que los usuarios pongan las unidades de datos fijas bajo protección.

Si deshabilita esta configuración, los usuarios no podrán poner sus unidades de datos fijas bajo protección de BitLocker. Si deshabilita esta directiva después de que BitLocker cifre las unidades de datos fijas, BitLocker descifrará las unidades de datos fijas.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMBMSFDVEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsfdvencryptionpolicy?view=sccm-ps).

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Denegar el acceso de escritura a unidades fijas no protegidas por BitLocker

*Configuración sugerida*: **No configurado**.

Requiera la protección de BitLocker para que Windows escriba datos en unidades fijas del dispositivo. BitLocker aplica esta directiva cuando se activa.

Al habilitar esta configuración:

- Si BitLocker protege una unidad de datos fija, Windows la monta con acceso de lectura y escritura.

- En el caso de las unidades de datos fijas que BitLocker no protege, Windows las monta como de solo lectura.

Si no configura esta opción, Windows montará todas las unidades de datos fijas con acceso de lectura y escritura.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMFDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmfdvdenywriteaccesspolicy?view=sccm-ps).

### <a name="fixed-data-drive-password-policy"></a>Directiva de contraseñas de unidades de datos fijas

*Configuración sugerida*: **No configurado**.

Use estas opciones para establecer las restricciones de contraseñas para desbloquear las unidades de datos fijas protegidas por BitLocker.

Si habilita esta configuración, los usuarios podrán configurar una contraseña que cumpla los requisitos que haya definido.

Para mayor seguridad, habilite esta opción y, a continuación, configure las opciones siguientes:

- **Requerir contraseña para unidad de datos fija**: Los usuarios tienen que especificar una contraseña para desbloquear una unidad de datos fija protegida por BitLocker.

- **Configurar complejidad de la contraseña para unidades de datos fijas**: Para requerir el cumplimiento de los requisitos de complejidad, seleccione **Requerir complejidad de la contraseña**.

- **Longitud de contraseña mínima para unidad de datos fija**: De forma predeterminada, la longitud mínima es de `8`.

Si deshabilita esta configuración, los usuarios no podrán configurar una contraseña.

Si no se configura la directiva, BitLocker admite contraseñas con la configuración predeterminada. La configuración predeterminada no incluye los requisitos de complejidad de la contraseña y solo requiere ocho caracteres.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMFDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmfdvpassphrasepolicy?view=sccm-ps).

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Notas de uso general de la directiva de contraseñas de unidades de datos fijas

- Para que la configuración de los requisitos de complejidad sea eficaz, habilite también la configuración de directiva de grupo **Las contraseñas deben cumplir los requisitos de complejidad**, que se encuentra en **Configuración del equipo** > **Configuración de Windows** > **Configuración de seguridad** > **Directivas de cuenta** > **Directiva de contraseñas**.

- BitLocker aplica esta configuración al activarlo, no al desbloquear un volumen. BitLocker permite desbloquear una unidad con cualquiera de los protectores que están disponibles en la unidad.

- Si usa la directiva de grupo para habilitar los algoritmos compatibles con FIPS para el cifrado, el uso de hash y la firma, no puede permitir que las contraseñas actúen como un protector de BitLocker.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Configuración de aplicación de directiva de cifrado (unidades de datos fijas)

*Configuración sugerida*: **Habilitado**

Configure el número de días que los usuarios pueden posponer el cumplimiento de BitLocker para las unidades de datos fijas. El **período de gracia de no cumplimiento** comienza cuando Configuration Manager detecta por primera vez que la unidad de datos fija no es conforme. La directiva de unidades de datos fijas no se aplica hasta que la unidad de sistema operativo es conforme. Una vez expirado el período de gracia, los usuarios no pueden posponer la acción requerida ni solicitar una exención.

Si el proceso de cifrado requiere una entrada de usuario, se abrirá un cuadro de diálogo en Windows que el usuario no podrá cerrar hasta que introduzca la información necesaria. Las futuras notificaciones de errores o estados no tendrán esta restricción.

Si BitLocker no requiere la interacción del usuario para agregar un protector, una vez expirado el período de gracia, BitLocker inicia el cifrado en segundo plano.

Si deshabilita o no establece esta configuración, Configuration Manager no requerirá que los usuarios cumplan las directivas de BitLocker.

Para aplicar la directiva inmediatamente, establezca un período de gracia de `0`.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMUseFddEnforcePolicy](/powershell/module/configurationmanager/new-cmusefddenforcepolicy?view=sccm-ps).

## <a name="removable-drive"></a>Unidad extraíble

Mediante las opciones de esta página se configura el cifrado de unidades extraíbles, como, por ejemplo, claves USB.

### <a name="removable-data-drive-encryption"></a>Cifrado de unidades de datos extraíbles

*Configuración sugerida*: **Habilitado**

Esta configuración controla el uso de BitLocker en unidades extraíbles.

- **Permitir a los usuarios aplicar la protección de BitLocker en unidades de datos extraíbles**: Los usuarios pueden activar la protección de BitLocker para una unidad extraíble.

- **Permitir a los usuarios suspender y descifrar BitLocker en unidades de datos extraíbles**: Los usuarios pueden quitar o suspender temporalmente el cifrado de unidades de BitLocker en una unidad extraíble.

Al habilitar esta opción y permitir que los usuarios apliquen la protección de BitLocker, el cliente de Configuration Manager guarda la información de recuperación de las unidades extraíbles en el servicio de recuperación del punto de administración. Este comportamiento permite que los usuarios recuperen la unidad si olvidan o pierden el protector (contraseña).

Al habilitar esta configuración:

- Habilite la configuración de la **Directiva de contraseñas de unidades de datos extraíbles**.

- *Deshabilite* la configuración de directiva de grupo siguiente en **Sistema** > **Acceso al almacenamiento extraíble** para las configuraciones tanto del equipo como del usuario:

  - **Todas las clases de almacenamiento extraíble: Denegar el acceso a todo**
  - **Discos extraíbles: Denegar acceso de escritura**
  - **Discos extraíbles: Denegar acceso de lectura**

Si deshabilita esta configuración, los usuarios no podrán usar BitLocker en unidades extraíbles.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMRDVConfigureBDEPolicy](/powershell/module/configurationmanager/new-cmrdvconfigurebdepolicy?view=sccm-ps).

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Denegar el acceso de escritura a unidades extraíbles no protegidas por BitLocker

*Configuración sugerida*: **No configurado**.

Requiera la protección de BitLocker para que Windows escriba datos en unidades extraíbles del dispositivo. BitLocker aplica esta directiva cuando se activa.

Al habilitar esta configuración:

- Si BitLocker protege una unidad extraíble, Windows la monta con acceso de lectura y escritura.

- En el caso de las unidades extraíbles que BitLocker no protege, Windows las monta como de solo lectura.

- Si habilita la opción **Denegar el acceso de escritura a los dispositivos configurados en otra organización**, BitLocker solo dará acceso de escritura a las unidades extraíbles con campos de identificación que coincidan con los campos de identificación permitidos. Defina estos campos con la configuración global **Identificadores únicos de la organización** de la página [Configuración](#setup).

Si deshabilita o no establece esta configuración, Windows montará todas las unidades extraíbles con acceso de lectura y escritura.

> [!NOTE]
> Puede reemplazar esta configuración por la configuración de directiva de grupo en **Sistema** > **Acceso al almacenamiento extraíble**. Si habilita la configuración de directiva de grupo **Discos extraíbles: Denegar acceso de escritura**, BitLocker omite esta opción de Configuration Manager.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMRDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmrdvdenywriteaccesspolicy?view=sccm-ps).

### <a name="removable-data-drive-password-policy"></a>Directiva de contraseñas de unidades de datos extraíbles

*Configuración sugerida*: **Habilitado**

Use esta configuración para establecer las restricciones de las contraseñas para desbloquear las unidades extraíbles protegidas por BitLocker.

Si habilita esta configuración, los usuarios podrán configurar una contraseña que cumpla los requisitos que haya definido.

Para mayor seguridad, habilite esta opción y, a continuación, configure las opciones siguientes:

- **Requerir contraseña para unidad de datos extraíble**: Los usuarios tienen que especificar una contraseña para desbloquear una unidad extraíble protegida por BitLocker.

- **Configurar complejidad de la contraseña para unidades de datos extraíbles**: Para requerir el cumplimiento de los requisitos de complejidad, seleccione **Requerir complejidad de la contraseña**.

- **Longitud de contraseña mínima para unidad de datos extraíble**: De forma predeterminada, la longitud mínima es de `8`.

Si deshabilita esta configuración, los usuarios no podrán configurar una contraseña.

Si no se configura la directiva, BitLocker admite contraseñas con la configuración predeterminada. La configuración predeterminada no incluye los requisitos de complejidad de la contraseña y solo requiere ocho caracteres.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMRDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmrdvpassphrasepolicy?view=sccm-ps).

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Notas de uso general de la directiva de contraseñas de unidades de datos extraíbles

- Para que la configuración de los requisitos de complejidad sea eficaz, habilite también la configuración de directiva de grupo **Las contraseñas deben cumplir los requisitos de complejidad**, que se encuentra en **Configuración del equipo** > **Configuración de Windows** > **Configuración de seguridad** > **Directivas de cuenta** > **Directiva de contraseñas**.

- BitLocker aplica esta configuración al activarlo, no al desbloquear un volumen. BitLocker permite desbloquear una unidad con cualquiera de los protectores que están disponibles en la unidad.

- Si usa la directiva de grupo para habilitar los algoritmos compatibles con FIPS para el cifrado, el uso de hash y la firma, no puede permitir que las contraseñas actúen como un protector de BitLocker.

## <a name="client-management"></a>Administración de cliente

Mediante las opciones de esta página se configuran los clientes y servicios de administración de BitLocker.

### <a name="bitlocker-management-services"></a>Servicios de administración de BitLocker

*Configuración sugerida*: **Habilitado**

Si habilita esta opción, Configuration Manager realizará automáticamente y de forma silenciosa una copia de seguridad de la información de recuperación de claves en la base de datos del sitio. Si deshabilita o no establece esta configuración, Configuration Manager no guardará la información de la recuperación de claves.

- **Seleccionar la información de recuperación de BitLocker que debe almacenarse**: Configure el servicio de recuperación de claves para hacer una copia de seguridad de la información de recuperación de BitLocker. Proporciona un método administrativo para recuperar datos cifrados mediante BitLocker a fin de evitar la pérdida de datos debida a la falta de información de claves.

- **Permitir que la información de recuperación se almacene en texto sin formato**: Sin un certificado de cifrado de administración de BitLocker para SQL Server, Configuration Manager almacena la información de la recuperación de claves en texto sin formato. Para obtener más información, consulte el artículo [Cifrado de los datos de recuperación](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **Frecuencia del estado de comprobación del cliente (en minutos)** : Con la frecuencia configurada, el cliente comprueba las directivas de protección de BitLocker y el estado en el equipo, además de hacer una copia de seguridad de la clave de recuperación de cliente. De forma predeterminada, el cliente de Configuration Manager actualiza su información de recuperación de BitLocker cada 90 minutos.

Para obtener más información sobre cómo crear estas directivas con Windows PowerShell, consulte:

- [Set-CMBlmPlaintextStorage](/powershell/module/configurationmanager/set-cmblmplaintextstorage?view=sccm-ps)
- [New-CMBMSClientConfigureCheckIntervalPolicy](/powershell/module/configurationmanager/new-cmbmsclientconfigurecheckintervalpolicy?view=sccm-ps)

### <a name="user-exemption-policy"></a>Directiva de exención de usuario

*Configuración sugerida*: **No configurado**.

Configure un método de contacto para que los usuarios soliciten una exención del cifrado de BitLocker.

Si habilita esta configuración de directiva, proporcione la información siguiente:

- **Número máximo de días de aplazamiento**: Número de días que el usuario puede aplazar una directiva exigida. De forma predeterminada, este valor es de `7` días (una semana).

- **Método de contacto**: Especifique la forma en que los usuarios pueden solicitar una exención: dirección URL, dirección de correo electrónico o número de teléfono.

- **Contacto**: Especifique la dirección URL, la dirección de correo electrónico o el número de teléfono. Cuando un usuario solicite una exención de la protección de BitLocker, verá un cuadro de diálogo de Windows con instrucciones sobre cómo realizar la solicitud. Configuration Manager no valida la información que introduce.

  - **Dirección URL**: Use el formato de dirección URL estándar, `https://website.domain.tld`. Windows muestra la dirección URL como un hipervínculo.

  - **Dirección de correo electrónico**: Use el formato de dirección de correo electrónico estándar, `user@domain.tld`. Windows muestra la dirección como el hipervínculo siguiente: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`.

  - **Número de teléfono**: Especifique el número al que quiera que llamen los usuarios. Windows muestra el número con la descripción siguiente: `Please call <your number> for applying exemption`.

Si deshabilita o no establece esta configuración, Windows no mostrará las instrucciones de solicitud de exención a los usuarios.

> [!NOTE]
> BitLocker administra las exenciones por usuario, no por equipo. Si varios usuarios inician sesión en el mismo equipo y un usuario no está exento, BitLocker cifrará el equipo.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMBMSUserExemptionPolicy](/powershell/module/configurationmanager/new-cmbmsuserexemptionpolicy?view=sccm-ps).

### <a name="url-for-the-security-policy-link"></a>Dirección URL para el vínculo de la directiva de seguridad

*Configuración sugerida*: **Habilitado**

Especifique una dirección URL que se mostrará a los usuarios como **Directiva de seguridad de la compañía** en Windows. Use este vínculo para proporcionar a los usuarios información sobre los requisitos de cifrado. Muestra cuándo BitLocker solicita al usuario el cifrado de una unidad.

Si habilita esta configuración, configure la **dirección URL del vínculo de la directiva de seguridad**.

Si deshabilita o no establece esta configuración, BitLocker no mostrará el vínculo de la directiva de seguridad.

Para obtener más información sobre cómo crear esta directiva con Windows PowerShell, vea [New-CMMoreInfoUrlPolicy](/powershell/module/configurationmanager/new-cmmoreinfourlpolicy?view=sccm-ps).

## <a name="next-steps"></a>Pasos siguientes

Si usa Windows PowerShell para crear estos objetos de directiva, use el cmdlet [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting?view=sccm-ps). Este cmdlet crea un objeto de configuración de la directiva de administración de BitLocker que contiene todas las directivas especificadas. Para implementar la configuración de directiva en una recopilación, use el cmdlet [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment?view=sccm-ps).
