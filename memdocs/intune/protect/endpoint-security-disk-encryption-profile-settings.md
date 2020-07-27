---
title: Configuración de la directiva de cifrado de discos de seguridad de los puntos de conexión de Intune | Microsoft Docs
description: Configuración de la directiva de cifrado de disco de seguridad de los puntos de conexión para BitLocker y FileVault en Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 3760aa9820495db6c2460bf2e6d2e9a08d705a10
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462038"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Configuración de la directiva de cifrado de discos para seguridad de los puntos de conexión en Intune

Vea la configuración que puede definir en los perfiles de la directiva de *Cifrado de discos* en el nodo Seguridad de los puntos de conexión de Intune como parte de una [directiva de seguridad de los puntos de conexión](../protect/endpoint-security-policy.md).

Perfiles y plataformas compatibles:

- **macOS**:
  - Perfil: **FileVault**
- **Windows 10 y versiones posteriores**:
  - Perfil: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Cifrado

**Habilitación de FileVault**  
- **Sin configurar** (*valor predeterminado*).
- **Sí**: habilite el cifrado de disco completo mediante XTS-AES 128 con FileVault en dispositivos que ejecuten macOS 10.13 y versiones posteriores. FileVault se habilita cuando el usuario cierra la sesión del dispositivo.

  Cuando se establece en *Sí*, pueden configurarse otras opciones para FileVault.

  - **Tipo de clave de recuperación** Se crean claves de recuperación de 
    *clave personal* para los dispositivos. Configure las opciones siguientes para la clave personal:

    - **Rotación de clave de recuperación personal**  
      Especifique la frecuencia con la que se rotará la clave de recuperación personal para un dispositivo. Puede seleccionar el valor predeterminado, que es **No configurado**, o un valor de **1** a **12** meses.
    - **Descripción de la ubicación secundaria de la clave de recuperación personal**  
      Especifique un mensaje breve para el usuario que explique cómo puede recuperar su clave de recuperación personal. El usuario ve este texto en la pantalla de inicio de sesión cuando se le pide que escriba su clave de recuperación personal en caso de que se le haya olvidado una contraseña.

  - **Número de veces que se permite omitir**  
    Establece el número de veces que un usuario puede pasar por alto los mensajes para habilitar FileVault antes de que sea necesario para iniciar sesión.
    - **No configurado** (*valor predeterminado*): se requiere cifrado en el dispositivo antes de que se permita el siguiente inicio de sesión.
    - De **1** a **10**: permite al usuario omitir el mensaje de 1 a 10 veces antes de requerir el cifrado en el dispositivo.
    - **No hay límite, avisar siempre**: se solicita al usuario que habilite FileVault, pero el cifrado nunca es necesario.

  - **Permitir aplazamiento hasta el cierre de sesión**  
    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: aplace el aviso para habilitar FileVault hasta que el usuario cierra la sesión.  

  - **Deshabilitar mensaje al cerrar sesión**  
    Evite el mensaje en el que se solicita al usuario que habilite FileVault cuando cierre la sesión. Cuando se establece en Deshabilitar, al cerrar la sesión el mensaje está deshabilitado y, en su lugar, se le solicita cuando el usuario inicia sesión.
    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: deshabilite el aviso para habilitar FileVault que aparece en el cierre de sesión.

  - **Ocultar clave de recuperación**  
     La clave de recuperación personal del usuario del dispositivo macOS se oculta durante el cifrado. Una vez cifrado el disco, un usuario puede usar cualquier dispositivo para ver su clave de recuperación personal a través del sitio web del Portal de empresa de Intune o la aplicación Portal de empresa en una plataforma compatible.
    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: se oculta la clave de recuperación personal durante el cifrado del dispositivo.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker: configuración base

- **Habilitar el cifrado de disco completo para las unidades de datos fijas y de sistema operativo**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Si la unidad se cifró antes de aplicar esta directiva, no se realiza ninguna acción adicional. Si el método y las opciones de cifrado coinciden con los de esta directiva, la configuración debe devolver un valor correcto. Si una opción de configuración de BitLocker en contexto no coincide con esta directiva, es probable que la configuración devuelva un error.
  
  Para aplicar esta directiva a un disco ya cifrado, descifre la unidad y vuelva a aplicar la directiva MDM. El valor predeterminado de Windows es no requerir cifrado de unidad BitLocker. Aunque es posible que el cifrado automático de registro/inicio de sesión en Unión a Azure AD y la cuenta Microsoft (MSA) apliquen la habilitación de BitLocker en el cifrado XTS-AES de 128 bits.

  - **No configurado** (*valor predeterminado*): no se produce la aplicación de BitLocker.
  - **Sí**: se aplica el uso de BitLocker.

- **Exigir cifrado de tarjeta de almacenamiento (solo dispositivos móviles)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Esta opción solo se aplica a dispositivos de SKU de Windows Mobile y Mobile Enterprise.
  - **No configurado** (*valor predeterminado*): está opción vuelve al valor predeterminado del sistema operativo, que no requiere cifrado de tarjeta de almacenamiento.
  - **Sí**: se requiere cifrado en tarjetas de almacenamiento para dispositivos móviles.

- **Ocultar aviso sobre el cifrado de terceros**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Si BitLocker está habilitado en un sistema que ya está cifrado mediante un producto de cifrado de terceros, es posible que el dispositivo no se pueda usar. Puede producirse una pérdida de datos y es posible que haya que volver a instalar Windows. Se recomienda no habilitar nunca BitLocker en un dispositivo que tenga instalado o habilitado el cifrado de terceros.

  De forma predeterminada, el Asistente para la instalación de BitLocker solicita al usuario que confirme que no hay ningún cifrado de terceros.

  - **No configurado** (*valor predeterminado*): el Asistente para la instalación de BitLocker muestra una advertencia y pide a los usuarios que confirmen que no existe ningún cifrado de terceros.
  - **Sí**: oculta el aviso del Asistente para la instalación de BitLocker de los usuarios.

  Si se requieren características de habilitación silenciosa de BitLocker, se debe ocultar la advertencia de cifrado de otro fabricante, ya que los mensajes de confirmación necesarios interrumpen los flujos de trabajo de habilitación silenciosa.

  Cuando se establece en *Sí*, se pueden configurar estos valores:

  - **Permitir a los usuarios estándar habilitar el cifrado durante Autopilot**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **No configurado** (*valor predeterminado*): durante escenarios de habilitación silenciosa de Azure Active Directory (AADJ), los usuarios no han de ser administradores locales para habilitar BitLocker.
    - **Sí**: el valor se deja como cliente predeterminado, que requiere acceso de administrador local para habilitar BitLocker.

    En los escenarios de habilitación no silenciosa y Autopilot, el usuario debe ser un administrador local para completar el Asistente para la instalación de BitLocker.

- **Habilitar la contraseña de recuperación controlada por el cliente para**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  No se admiten dispositivos de adición de cuenta profesional (AWS, Unidos al área de trabajo) para la rotación de claves.
  - **No configurado** (*valor predeterminado*): el cliente no girará las claves de recuperación de BitLocker.
  - **Deshabilitado**
  - **Dispositivos unidos a Azure AD**
  - **Dispositivos unidos a Azure AD híbridos**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker: configuración de unidades de datos fijas

- **Directiva de unidad fija de BitLocker**  
  [Configuración de directiva de grupo de BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Recuperación de unidad fija**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Controle cómo se recuperan las unidades de datos fijas protegidas por BitLocker en ausencia de la información de clave de inicio necesaria.

    - **No configurado** (*valor predeterminado*): se admiten las opciones de recuperación predeterminadas incluido el Agente de recuperación de datos (DRA). El usuario final puede especificar opciones de recuperación y no se realiza una copia de seguridad de la información de recuperación en Azure Active Directory.
    - **Configurar**: permite el acceso para configurar varias técnicas de recuperación de unidad.

    Cuando se establece en *Configurar*, están disponibles las opciones siguientes:

    - **Creación de clave de recuperación por el usuario**  
      - **Bloqueado** (*valor predeterminado*)
      - **Requerido**
      - **Permitido**

    - **Configurar el paquete de recuperación de BitLocker**
      - **Contraseña y clave** (*valor predeterminado*): incluya la contraseña de recuperación de BitLocker que usan los administradores y usuarios para desbloquear las unidades protegidas y los paquetes de claves de recuperación utilizados por los administradores para la recuperación de datos) en Active Directory.
      - **Solo contraseña**: es posible que los paquetes de claves de recuperación no sean accesibles cuando sea necesario.

    - **Require device to back up recovery information to Azure Ad** (Requerir que el dispositivo realice copias de seguridad de la información de recuperación en Azure AD)
      - **No configurado** (*valor predeterminado*): la habilitación de BitLocker se completará aunque se produzca un error en la copia de seguridad de la clave de recuperación en Azure AD. Esto puede traducirse en que no se almacene externamente ninguna información de recuperación.
      - **Sí**: BitLocker no completará la habilitación hasta que se hayan guardado correctamente las claves de recuperación en Azure Active Directory.

    - **Creación de contraseña de recuperación por el usuario**  
      - **Bloqueado** (*valor predeterminado*)
      - **Requerido**
      - **Permitido**

    - **Hide recovery options during BitLocker setup** (Ocultar opciones de recuperación durante la configuración de BitLocker)
      - **No configurado** (*valor predeterminado*): permite al usuario acceder a opciones de recuperación adicionales.
      - **Sí**: impide que el usuario final elija opciones de recuperación adicionales, como la impresión de claves de recuperación durante el Asistente para la instalación de BitLocker.

    - **Habilitar BitLocker después de la información de recuperación para almacenar**
      - **Sin configurar** (*valor predeterminado*).  
      - **Sí**

    - **Bloquear el uso del Agente de recuperación de datos basada en certificados (DRA)**
      - **No configurado** (*valor predeterminado*): permite configurar el uso de DRA. La configuración de DRA requiere una PKI de empresa y objetos de directiva de grupo para implementar el agente y los certificados de DRA.
      - **Sí**: bloquee la capacidad de usar el Agente de recuperación de datos (DRA) para recuperar las unidades habilitadas para BitLocker.

  - **Denegar acceso de escritura a unidad de datos fija no protegida con BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Esta opción está disponible cuando *Directiva de unidades fijas de BitLocker* se establece en *Configurar*.

    - **No configurado** (*valor predeterminado*): pueden escribirse datos en unidades fijas no cifradas.
    - **Sí**: Windows no permitirá que se escriban datos en unidades fijas que no estén protegidas con BitLocker. Si no se cifra una unidad fija, el usuario ha de completar el Asistente para la instalación de BitLocker para la unidad antes de que se conceda acceso de escritura.

  - **Cifrado para unidades de datos fijas**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Configure el método de cifrado y la intensidad de cifrado para los discos de unidades de datos fijas. *XTS-AES de 128 bits* es el método de cifrado predeterminado de Windows y el valor recomendado.

    - **Sin configurar** (*valor predeterminado*).
    - **CBC-AES de 128 bits**
    - **AES-CBC de 256 bits**
    - **XTS-AES de 128 bits**
    - **AES-XTS de 256 bits**

### <a name="bitlocker---os-drive-settings"></a>BitLocker: configuración de unidades de sistema operativo

- **Directiva de unidad del sistema de BitLocker**  
  CSP: [Configuración de directiva de grupo de BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configurar** (*valor predeterminado*)  
  - **No configurado**.

  Cuando se establece en *Configurar*, se pueden configurar estos valores:

  - **Autenticación de inicio requerida**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: configure los requisitos de autenticación adicionales al inicio del sistema, como el uso del Módulo de plataforma segura (TPM) o los requisitos del PIN de inicio.

    Cuando se establece en *Sí*, se pueden configurar estos valores:

    - **Inicio de TPM compatible**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Se recomienda exigir un TPM para BitLocker. Esta configuración solo se aplica cuando BitLocker se habilita por primera vez y no tiene ningún efecto si BitLocker ya está habilitado.

      - **Bloqueado** (*valor predeterminado*): BitLocker no usa el TPM.
      - **Obligatorio**: BitLocker solo se habilita si un TPM está presente y se puede usar.
      - **Permitido**: BitLocker usa el TPM, si está presente.

    - **PIN de inicio de TPM compatible**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloqueado** (*valor predeterminado*): bloquea el uso de un PIN.
      - **Obligatorio**: requiere que un PIN y el TPM estén presentes para habilitar BitLocker.
      - **Permitido**: BitLocker usa el TPM si está presente y permite que el usuario configure un PIN de inicio.

      En los escenarios de habilitación silenciosa, ha de establecerla en *Bloqueado*. Los escenarios de habilitación silenciosa (como Autopilot) no se realizarán correctamente cuando se requiera la interacción del usuario.

    - **Clave de inicio de TPM compatible**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloqueado** (*valor predeterminado*): bloquea el uso de claves de inicio.
      - **Obligatorio**: requiere que una clave de inicio y el TPM estén presentes para habilitar BitLocker.
      - **Permitido**: BitLocker usa el TPM si está presente y permite que una clave de inicio (como una unidad USB) esté presente para desbloquear las unidades.

      En los escenarios de habilitación silenciosa, ha de establecerla en *Bloqueado*. Los escenarios de habilitación silenciosa (como Autopilot) no se realizarán correctamente cuando se requiera la interacción del usuario.

    - **PIN y clave de inicio de TPM compatible**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloqueado** (*valor predeterminado*): bloquea el uso de una combinación de teclas de inicio y de PIN.
      - **Obligatorio**: requiere que BitLocker tenga una clave de inicio y el PIN presente para que se habilite.
      - **Permitido**: BitLocker usa el TPM si está presente y permite una clave de inicio y la combinación de PIN.

      En los escenarios de habilitación silenciosa, ha de establecerla en *Bloqueado*. Los escenarios de habilitación silenciosa (como Autopilot) no se realizarán correctamente cuando se requiera la interacción del usuario.

    - **Deshabilitar BitLocker en dispositivos en los que TPM es incompatible**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Si no hay ningún TPM presente, BitLocker requiere una contraseña o una unidad USB para el inicio.

      Esta configuración solo se aplica cuando BitLocker se habilita por primera vez y no tiene ningún efecto si BitLocker ya está habilitado.

      - **Sin configurar** (*valor predeterminado*).
      - **Sí**: bloquea la configuración de BitLocker sin un chip TPM compatible.

    - **Habilitar dirección URL y mensaje de recuperación previos al arranque**  
      CSP: configuración de [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)

      - **No configurado** (*valor predeterminado*): use la información de recuperación previa al arranque de BitLocker predeterminada.
      - **Sí**: habilite la configuración de una dirección URL y un mensaje de recuperación previo al arranque para ayudar a los usuarios a comprender cómo encontrar su contraseña de recuperación. Los usuarios ven el mensaje y la dirección URL previos al arranque cuando están bloqueados en el modo de recuperación.

      Cuando se establece en *Sí*, se pueden configurar estos valores:

      - **Mensaje de recuperación previo al arranque**  
        Especifique un mensaje de recuperación previo al arranque personalizado.

      - **Dirección URL de recuperación previa al arranque**  
        Especifique una dirección URL de recuperación previa al arranque personalizada.

    - **Recuperación de unidad fija**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Sin configurar** (*valor predeterminado*).  
      - **Configurar**: habilite la configuración de opciones adicionales.

      Cuando se establece en *Configurar*, están disponibles las opciones siguientes:

      - **Creación de clave de recuperación por el usuario**  
        - **Bloqueado** (*valor predeterminado*)
        - **Requerido**
        - **Permitido**

      - **Configurar el paquete de recuperación de BitLocker**
        - **Contraseña y clave** (*valor predeterminado*): incluya la contraseña de recuperación de BitLocker que usan los administradores y usuarios para desbloquear las unidades protegidas y los paquetes de claves de recuperación utilizados por los administradores para la recuperación de datos) en Active Directory.
        - **Solo contraseña**: es posible que los paquetes de claves de recuperación no sean accesibles cuando sea necesario.

      - **Require device to back up recovery information to Azure Ad** (Requerir que el dispositivo realice copias de seguridad de la información de recuperación en Azure AD)
        - **No configurado** (*valor predeterminado*): la habilitación de BitLocker se completará aunque se produzca un error en la copia de seguridad de la clave de recuperación en Azure AD. Esto puede traducirse en que no se almacene externamente ninguna información de recuperación.
        - **Sí**: BitLocker no completará la habilitación hasta que se hayan guardado correctamente las claves de recuperación en Azure Active Directory.

      - **Creación de contraseña de recuperación por el usuario**  
        - **Bloqueado** (*valor predeterminado*)
        - **Requerido**
        - **Permitido**

      - **Hide recovery options during BitLocker setup** (Ocultar opciones de recuperación durante la configuración de BitLocker)
        - **No configurado** (*valor predeterminado*): permite al usuario acceder a opciones de recuperación adicionales.
        - **Sí**: impide que el usuario final elija opciones de recuperación adicionales, como la impresión de claves de recuperación durante el Asistente para la instalación de BitLocker.

      - **Habilitar BitLocker después de la información de recuperación para almacenar**
        - **Sin configurar** (*valor predeterminado*).  
        - **Sí**

      - **Bloquear el uso del Agente de recuperación de datos basada en certificados (DRA)**
        - **No configurado** (*valor predeterminado*): permite configurar el uso de DRA. La configuración de DRA requiere una PKI de empresa y objetos de directiva de grupo para implementar el agente y los certificados de DRA.
        - **Sí**: bloquee la capacidad de usar el Agente de recuperación de datos (DRA) para recuperar las unidades habilitadas para BitLocker.

    - **Longitud mínima del PIN**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Especifique la longitud mínima del PIN de inicio cuando se requiere TPM+PIN durante la habilitación de BitLocker. La longitud mínima del PIN debe tener entre 4 y 20 dígitos.

      Si no configura esta opción, los usuarios pueden configurar un PIN de inicio de cualquier longitud (entre 4 y 20 dígitos).

      Esta configuración solo se aplica cuando BitLocker se habilita por primera vez y no tiene ningún efecto si BitLocker ya está habilitado.

  - **Cifrado para unidades del sistema operativo**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Configure el método de cifrado y la intensidad de cifrado para las unidades del sistema operativo. *XTS-AES de 128 bits* es el método de cifrado predeterminado de Windows y el valor recomendado.

    - **Sin configurar** (*valor predeterminado*).
    - **CBC-AES de 128 bits**
    - **AES-CBC de 256 bits**
    - **XTS-AES de 128 bits**
    - **AES-XTS de 256 bits**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker: configuración de unidades de datos extraíbles

- **Cifrado para unidades del sistema operativo**  
  CSP: [Configuración de directiva de grupo de BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Sin configurar** (*valor predeterminado*).  
  - **Configure**

  Cuando se establece en *Configurar*, se pueden configurar estos valores.

  - **Cifrado para unidades de datos extraíbles**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Seleccione el método de cifrado para los discos de unidades de datos extraíbles.

    - **Sin configurar** (*valor predeterminado*).
    - **CBC-AES de 128 bits**
    - **AES-CBC de 256 bits**
    - **XTS-AES de 128 bits**
    - **AES-XTS de 256 bits**

  - **Denegar acceso de escritura a discos de datos extraíbles no protegidos con BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **No configurado** (*valor predeterminado*): pueden escribirse datos en unidades extraíbles no cifradas.
    - **Sí**: Windows no permitirá que se escriban datos en unidades extraíbles que no estén protegidas por BitLocker. Si una unidad extraíble insertada no se cifra, el usuario ha de completar el Asistente para la instalación de BitLocker antes de que se conceda acceso de escritura a la unidad.

    - **Denegar acceso de escritura a discos de datos extraíbles no protegidos con BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **No configurado** (*valor predeterminado*): se puede usar cualquier unidad cifrada de BitLocker.
      - **Sí**: bloquea el acceso a las unidades extraíbles a menos que se hayan cifrado en un equipo propiedad de su organización.

## <a name="next-steps"></a>Pasos siguientes

[Directiva de seguridad de los puntos de conexión para cifrado de discos](../protect/endpoint-security-disk-encryption-policy.md)
