---
title: Sitio web de administración y supervisión de BitLocker
titleSuffix: Configuration Manager
description: Procedimiento para usar el sitio web de administración y supervisión de BitLocker (portal de soporte técnico) en Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf9301e4fcb279b7d79a6f6c3d0a90ab3d15e277
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697320"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Sitio web de administración y supervisión de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

El sitio web de administración y supervisión de BitLocker es una interfaz administrativa para el Cifrado de unidad BitLocker. También se conoce como portal de soporte técnico. Use este sitio web para revisar informes, recuperar unidades de usuarios y administrar TPM de dispositivos.

[![Captura de pantalla del sitio web predeterminado de administración y supervisión de BitLocker](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Para poder usarlo, debe instalar este componente en un servidor web. Para obtener más información, vea [Configuración de informes y portales de BitLocker](setup-websites.md).

Acceda al sitio web de administración y supervisión a través de la siguiente dirección URL: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Puede ver el **Informe de auditoría de recuperación** en el sitio web de administración y supervisión. Agregue otros informes de administración de BitLocker al punto de servicios de informes. Para obtener más información, vea [Consulta de los informes de BitLocker](view-reports.md).

## <a name="groups"></a>Grupos

Para acceder a áreas específicas del sitio web de administración y supervisión, la cuenta de usuario debe estar en uno de los siguientes grupos. Cree estos grupos en Active Directory, con el nombre que quiera. Al instalar este sitio web, se especifican estos nombres de grupo. Para obtener más información, vea [Configuración de informes y portales de BitLocker](setup-websites.md).

|Grupo|Descripción|
|--- |--- |
|Administradores de soporte técnico de BitLocker|Proporciona acceso a todas las áreas del sitio web de administración y supervisión. Cuando ayuda a un usuario a recuperar sus unidades, solo tiene que escribir la clave de recuperación, no el dominio ni el nombre de usuario. Si un usuario es miembro de este grupo y del grupo de usuarios de soporte técnico de BitLocker, los permisos del grupo de administradores reemplazan los permisos del grupo de usuarios.|
|Usuarios de soporte técnico de BitLocker|Proporciona acceso a las áreas **Administrar TPM** y **Recuperación de unidad** del sitio web de administración y supervisión. Al usar cualquiera de estas áreas, debe rellenar todos los campos, incluidos el dominio y el nombre de la cuenta del usuario. Si un usuario es miembro de este grupo y del grupo de administradores de soporte técnico de BitLocker, los permisos del grupo de administradores reemplazan los permisos del grupo de usuarios.|
|Usuarios de informes de BitLocker|Proporciona acceso al área **Informes** del sitio web de administración y supervisión.|

## <a name="manage-tpm"></a>Administrar TPM

Si un usuario escribe el PIN incorrecto demasiadas veces, puede bloquear el TPM. El número de veces que un usuario puede escribir un PIN incorrecto antes de que se bloquee el TPM varía según el fabricante. En el área **Administrar TPM** del sitio web de administración y supervisión, acceda al sistema de datos de recuperación de claves centralizado.

Para obtener más información acerca de la propiedad del TPM, vea [Configurar MBAM para custodiar TPM y almacenar contraseñas OwnerAuth](/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> A partir de Windows 10, versión 1607, Windows no mantiene la contraseña de propietario de TPM al aprovisionar el TPM.

1. Vaya al sitio web de administración y supervisión en el explorador web, por ejemplo `https://webserver.contoso.com/HelpDesk`.

1. En el panel izquierdo, seleccione el área **Administrar TPM**.

    ![Página Administrar TPM del sitio web de administración y supervisión de BitLocker](media/bitlocker-admin-manage-tpm.png)

1. Escriba el nombre de dominio completo del equipo y el nombre del equipo.

1. Si es necesario, escriba el nombre de usuario y el dominio del usuario para recuperar el archivo de contraseña de propietario de TPM.

1. Elija una de las siguientes opciones como **Motivo de la solicitud del archivo de contraseña de propietario de TPM**:

    - Restablecer bloqueo de PIN
    - Activar TPM
    - Desactivar TPM
    - Cambiar contraseña de TPM
    - Quitar TPM
    - Otros

    Después de **Enviar** el formulario, el sitio web devuelve una de las siguientes respuestas:

    - Si no encuentra un archivo de contraseña de propietario de TPM coincidente, devuelve un mensaje de error.

    - Archivo de contraseña de propietario del TPM del equipo enviado

    Después de recuperar el archivo de contraseña de propietario de TPM, el sitio web muestra la contraseña de propietario.

1. Para guardar la contraseña en un archivo, seleccione **Guardar**.

1. En el área **Administrar TPM**, seleccione la opción **Restablecer bloqueo de TPM** y proporcione el archivo de contraseña de propietario de TPM.

    Se restablece el bloqueo de TPM. BitLocker restaura el acceso del usuario al dispositivo.

    > [!IMPORTANT]
    > No comparta el valor de hash de TPM o el archivo de contraseña de propietario de TPM.

## <a name="drive-recovery"></a>Recuperación de unidad

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> Recuperación de una unidad en modo de recuperación

Las unidades entran en modo de recuperación en los escenarios siguientes:

- El usuario pierde u olvida su PIN o contraseña
- El Módulo de plataforma segura (TPM) detecta cambios en el BIOS o en los archivos de inicio del equipo

Para obtener una contraseña de recuperación, use el área **Recuperación de unidad** del sitio web de administración y supervisión.

> [!IMPORTANT]
> Las contraseñas de recuperación expiran después de un solo uso. En unidades del sistema operativo y unidades de datos fijas, la regla de un solo uso se aplica automáticamente. En unidades extraíbles, se aplica cuando se extrae y se vuelve a insertar la unidad.

1. Vaya al sitio web de administración y supervisión en el explorador web, por ejemplo `https://webserver.contoso.com/HelpDesk`.

1. En el panel izquierdo, seleccione el área **Recuperación de unidad**.

    ![Página Recuperación de unidad del sitio web de administración y supervisión de BitLocker](media/bitlocker-admin-drive-recovery.png)

1. Si es necesario, escriba el nombre de usuario y el dominio del usuario para ver información de recuperación.

1. Para ver una lista de las claves de recuperación coincidentes posibles, escriba los primeros ocho dígitos del identificador de la clave de recuperación. Para obtener la clave de recuperación exacta, escriba el identificador completo de la clave de recuperación.

1. Elija una de las siguientes opciones como **Motivo del desbloqueo de la unidad**:

    - Orden de arranque del sistema operativo cambiado
    - BIOS cambiado
    - Archivos del sistema operativo modificados
    - Clave de inicio perdida
    - PIN perdido
    - TPM restablecido
    - Frase de contraseña perdida
    - Tarjeta inteligente perdida
    - Otros

    Después de **Enviar** el formulario, el sitio web devuelve una de las siguientes respuestas:

    - Si el usuario tiene varias contraseñas de recuperación coincidentes, devuelve varias coincidencias posibles.

    - Contraseña de recuperación y paquete de recuperación del usuario enviado.

        > [!NOTE]
        > Si va a recuperar una unidad dañada, la opción del paquete de recuperación proporciona a BitLocker la información crítica necesaria para recuperar la unidad.

    - Si no encuentra una contraseña de recuperación coincidente, devuelve un mensaje de error.

    Después de recuperar la contraseña de recuperación y el paquete de recuperación, el sitio web muestra la contraseña de recuperación.

1. Para copiar la contraseña, seleccione **Copiar clave**. Para guardar la contraseña de recuperación en un archivo, seleccione **Guardar**.

Para desbloquear la unidad, escriba la contraseña de recuperación o use el paquete de recuperación.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> Recuperación de una unidad migrada

Cuando se mueve una unidad a un nuevo equipo, ya que el TPM es diferente, BitLocker no acepta el PIN anterior. Para recuperar la unidad migrada, obtenga el identificador de la clave de recuperación para recuperar la contraseña de recuperación.

Para recuperar una unidad migrada, use el área **Recuperación de unidad** del sitio web de administración y supervisión.

1. En el equipo que tiene la unidad movida, inicie el equipo en modo de Entorno de recuperación de Windows (WinRE).

1. En WinRE, BitLocker trata la unidad del sistema operativo movida como una unidad de datos fija. BitLocker muestra el identificador de la contraseña de recuperación de la unidad y solicita la contraseña de recuperación.

    > [!NOTE]
    > En algunas situaciones, durante el proceso de inicio, seleccione **Olvidé el PIN** si la opción está disponible. Posteriormente, escriba el modo de recuperación para mostrar el identificador de la clave de recuperación.

1. Use el identificador de la clave de recuperación para obtener la contraseña de recuperación desde el sitio web de administración y supervisión. Para obtener más información, vea [Cómo recuperar una unidad en modo de recuperación](#bkmk_recovery).

Si configuró la unidad que se movió para usar el chip de TPM en el equipo original, siga estos pasos. Si no, el proceso de recuperación se ha completado.

1. Después de desbloquear la unidad, inicie el equipo en modo WinRE. Abra un símbolo del sistema en WinRE y use el comando `manage-bde` para descifrar la unidad. Esta herramienta es la única forma de quitar la protección de **TPM y PIN** sin el chip de TPM original. Para obtener más información sobre este comando, vea [Manage-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Cuando haya finalizado, inicie el equipo normalmente. Configuration Manager aplicará la directiva de BitLocker para cifrar la unidad con el TPM del nuevo equipo y el PIN.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> Recuperación de una unidad dañada

Use el identificador de la clave de recuperación para obtener un paquete de claves de recuperación desde el sitio web de administración y supervisión. Para obtener más información, vea [Cómo recuperar una unidad en modo de recuperación](#bkmk_recovery).

1. Guarde el **paquete de claves de recuperación** en el equipo y, posteriormente, cópielo en el equipo con la unidad dañada.

1. Abra un símbolo del sistema como administrador y escriba el comando siguiente:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Reemplace los siguientes valores:

    - `<corrupted drive>`: La letra de unidad de la unidad dañada; por ejemplo, `D:`
    - `<fixed drive>`: La letra de unidad de una unidad de disco duro disponible de un tamaño similar o mayor que la unidad dañada. BitLocker recupera y mueve los datos de la unidad dañada a la unidad especificada. Se sobrescriben todos los datos de esta unidad.
    - `<key package>`: La ubicación del paquete de claves de recuperación
    - `<recovery password>`: La contraseña de recuperación asociada

    Por ejemplo:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Para obtener más información sobre este comando, vea [Repair-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Informes

El sitio web de administración y supervisión incluye el **Informe de auditoría de recuperación**. Hay otros informes disponibles en el punto de servicios de informes de Configuration Manager. Para obtener más información, vea [Consulta de los informes de BitLocker](view-reports.md).

1. Vaya al sitio web de administración y supervisión en el explorador web, por ejemplo `https://webserver.contoso.com/HelpDesk`.

1. En el panel izquierdo, seleccione el área **Informes**.

1. En la barra de menús superior, seleccione el **Informe de auditoría de recuperación**.

Para obtener más información sobre este informe, vea [Informe de auditoría de recuperación](view-reports.md#bkmk-audit)

> [!TIP]
> Para guardar los resultados del informe, seleccione **Exportar** en la barra de menús **Informes**.