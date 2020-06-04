---
title: Cifrado de dispositivos macOS con cifrado de discos FileVault con Intune
titleSuffix: Microsoft Intune
description: Cifre dispositivos macOS con el método de cifrado integrado FileVault y administre las claves de recuperación de esos dispositivos cifrados desde el portal de Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 99facc87d068239962ab0d40874aa081f5e19189
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989693"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Uso del cifrado de discos FileVault para macOS con Intune

Intune es compatible con el cifrado de discos FileVault de macOS. FileVault es un programa de cifrado de disco completo que se incluye con macOS. Puede usar Intune para configurar FileVault en dispositivos que ejecuten **macOS 10.13 o versiones posteriores**.

Use alguno de los siguientes tipos de directiva para configurar FileVault en los dispositivos administrados:

- **[Directiva de seguridad de puntos de conexión para FileVault de macOS](#create-an-endpoint-security-policy-for-filevault)** . El perfil de FileVault de *Seguridad de los puntos de conexión* es un grupo prioritario de opciones dedicado a la configuración de FileVault.

  Vea las [Opciones de FileVault disponibles en los perfiles de la directiva de cifrado de discos](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Perfil de configuración de dispositivos para la protección de puntos de conexión para FileVault de macOS](#create-an-endpoint-security-policy-for-filevault)** . La configuración de FileVault es una de las categorías de configuración disponibles para la protección de punto de conexión de macOS. Para obtener más información sobre el uso de un perfil de configuración de dispositivos, vea [Creación de un perfil de dispositivo en Microsoft Intune](../configuration/device-profile-create.md).

  Vea las [opciones de FileVault disponibles en los perfiles de protección de puntos de conexión de la directiva de configuración de dispositivos](../protect/endpoint-protection-macos.md#filevault).

Para administrar BitLocker para Windows 10, vea [Directiva de administración de BitLocker](../protect/encrypt-devices.md).

> [!TIP]
> [Informe de cifrado](encryption-monitor.md) que presenta detalles sobre el estado de cifrado de los dispositivos en todos los dispositivos administrados.

Después de crear una directiva para cifrar dispositivos con FileVault, la directiva se aplica a los dispositivos en dos fases. En primer lugar, el dispositivo se prepara para habilitar a Intune a recuperar y hacer una copia de seguridad de la clave de recuperación. Esta acción se denomina custodia. Una vez que se ha custodiado la clave, se puede iniciar el cifrado de disco.

La inscripción de dispositivos aprobados por el usuario es necesaria para que FileVault funcione en un dispositivo. El usuario debe aprobar manualmente el perfil de administración en las preferencias del sistema para que la inscripción se considere aprobada por el usuario.

## <a name="permissions-to-manage-filevault"></a>Permisos para administrar FileVault

Para administrar FileVault en Intune, la cuenta debe tener los permisos de [control de acceso basado en roles](../fundamentals/role-based-access-control.md) (RBAC) de Intune aplicables.

A continuación se muestran los permisos de FileVault, que forman parte de la categoría **Tareas remotas** y los roles de RBAC integrados que conceden el permiso:

- **Obtener la clave de FileVault**:
  - Operador del departamento de soporte técnico
  - Administrador de seguridad de puntos de conexión

- **Rotar la clave de FileVault**
  - Operador del departamento de soporte técnico

## <a name="create-and-deploy-policy"></a>Creación e implementación de directiva

### <a name="create-an-endpoint-security-policy-for-filevault"></a>Creación de una directiva de seguridad de los puntos de conexión para FileVault

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión** > **Cifrado de disco** > **Crear directiva**.

3. En la página **Aspectos básicos**, especifique las siguientes propiedades y seleccione **Siguiente**.
   1. **Plataforma**: macOS
   2. **Perfil**: FileVault

   ![Selección del perfil de FileVault](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. En la página **Opciones de configuración**:
   1. Establezca *Habilitar FileVault* en **Sí**.
   2. En *Tipo de clave de recuperación* solo se admite **Clave de recuperación personal**.
   3. Configure opciones adicionales para satisfacer los requisitos.

   Considere la posibilidad de agregar un mensaje para guiar a los usuarios en el proceso de recuperación de la clave de recuperación de su dispositivo. Esta información puede ser útil para los usuarios cuando se usa la opción Rotación de clave de recuperación personal, que puede generar automáticamente una nueva clave de recuperación para un dispositivo de forma periódica.

   Por ejemplo: para recuperar una clave de recuperación perdida o girada recientemente, inicie sesión en el sitio web Portal de empresa de Intune desde cualquier dispositivo. En el portal, vaya a Dispositivos, seleccione el dispositivo que tiene habilitado FileVault y luego *Obtener clave de recuperación*. Se muestra la clave de recuperación actual.

5. Cuando haya finalizado la configuración, seleccione **Siguiente**.

6. En la página **Ámbito (etiquetas)** , seleccione **Seleccionar etiquetas de ámbito** para abrir el panel Seleccionar etiquetas a fin de asignar etiquetas de ámbito al perfil.

   Seleccione **Siguiente** para continuar.

7. En la página **Asignaciones**, seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea Asignación de perfiles de usuario y dispositivo.
Seleccione **Siguiente**.

8. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

### <a name="create-a-device-configuration-policy-for-filevault"></a>Creación de una directiva de configuración de dispositivos para FileVault

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Establece las siguientes opciones:
   1. **Plataforma**: macOS
   2. **Perfil**: Endpoint Protection

   ![Selección del perfil de FileVault](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Seleccione **Configuración** > **FileVault**.

   ![Configuración de FileVault](./media/encrypt-devices-filevault/filevault-settings.png)

5. En *FileVault*, seleccione **Habilitar**.

6. En *Tipo de clave de recuperación*, solo se admite **Clave personal**.

   Considere la posibilidad de agregar un mensaje para guiar a los usuarios en el proceso de recuperación de la clave de recuperación de su dispositivo. Esta información puede ser útil para los usuarios cuando se usa la opción Rotación de clave de recuperación personal, que puede generar automáticamente una nueva clave de recuperación para un dispositivo de forma periódica.

   Por ejemplo: para recuperar una clave de recuperación perdida o girada recientemente, inicie sesión en el sitio web Portal de empresa de Intune desde cualquier dispositivo. En el portal, vaya a *Dispositivos*, seleccione el dispositivo que tiene habilitado FileVault y, después, seleccione *Obtener clave de recuperación*. Se muestra la clave de recuperación actual.

7. Configure el resto de [valores de FileVault](endpoint-protection-macos.md#filevault) para cumplir con sus necesidades empresariales y luego seleccione **Aceptar**.

8. Complete la configuración de valores adicionales y luego guarde el perfil.

## <a name="manage-filevault"></a>Administración de FileVault

Para ver información sobre los dispositivos que reciben la directiva de FileVault, vea [Supervisión de cifrado de discos](../protect/encryption-monitor.md).

Cuando Intune cifra por primera vez un dispositivo macOS con FileVault, se crea una clave de recuperación personal. Tras el cifrado, el dispositivo muestra la clave personal una sola vez al usuario del dispositivo.

En el caso de los dispositivos administrados, Intune puede custodiar una copia de la clave de recuperación personal. La custodia de las claves habilita a los administradores de Intune para girar claves con el fin de ayudar a proteger los dispositivos y a los usuarios para recuperar una clave de recuperación personal perdida o girada.

Después de que Intune cifre un dispositivo macOS con FileVault:

- Los administradores pueden ver y administrar las claves de recuperación de FileVault mediante el informe de cifrado de Intune.
- Los usuarios pueden ver la clave de recuperación personal de un dispositivo desde el Portal de empresa web en el dispositivo. En el Portal de empresa web, seleccione el dispositivo macOS cifrado y luego "Obtener clave de recuperación" como acción de dispositivo remota.

> [!IMPORTANT]
> Intune no puede administrar los dispositivos que, en vez de cifrar Intune, son los usuarios quienes los cifran. Esto significa que Intune no puede custodiar la recuperación personal de estos dispositivos ni administrar el giro de la clave de recuperación. Antes de que Intune pueda administrar FileVault y las claves de recuperación para el dispositivo, el usuario debe descifrar el dispositivo y, después, dejar que Intune cifre el dispositivo.

### <a name="retrieve-personal-recovery-key"></a>Recuperación de clave de recuperación personal

En un dispositivo macOS cifrado mediante Intune, los usuarios finales pueden recuperar su clave de recuperación personal (clave de FileVault) mediante la aplicación Portal de empresa de iOS, la aplicación Portal de empresa de Android o la aplicación Intune para Android.

El dispositivo que tiene la clave de recuperación personal se debe inscribir en Intune y cifrar con FileVault a través de Intune. Con la aplicación Portal de empresa de iOS, la aplicación Portal de empresa de Android, la aplicación Intune para Android o el sitio web Portal de empresa, el usuario puede ver la clave de recuperación de **FileVault** necesaria para acceder a sus dispositivos Mac.

Los usuarios de dispositivos pueden seleccionar **Dispositivos** > *el dispositivo macOS cifrado e inscrito* > **Obtener clave de recuperación**. El explorador mostrará el Portal de empresa web y se verá la clave de recuperación.

### <a name="rotate-recovery-keys"></a>Giro de claves de recuperación

Intune admite varias opciones para girar y recuperar claves de recuperación personales. Un motivo para girar una clave es si la clave personal actual se pierde o se considera que está en riesgo.

- **Rotación automática**: como administrador, puede configurar el valor de la opción Giro de clave de recuperación personal de FileVault para que genere de forma automática nuevas claves de recuperación periódicamente. Cuando se genera una nueva clave para un dispositivo, esta clave no se muestra al usuario. En lugar de eso, el usuario debe obtener la clave desde un administrador o mediante la aplicación de Portal de empresa.

- **Rotación manual**: como administrador, puede ver la información de un dispositivo que administra con Intune y que está cifrado con FileVault. Luego, puede optar por girar manualmente la clave de recuperación de los dispositivos corporativos. No es posible girar las claves de recuperación de dispositivos personales.

  Para girar una clave de recuperación, realice lo siguiente:

  1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Seleccione **Dispositivos** > **Todos los dispositivos**.

  3. En la lista de dispositivos, seleccione el dispositivo que está cifrado y para el que quiere girar la clave. Luego, en Supervisar, seleccione  **Claves de recuperación**.
  
  4. En el panel Claves de recuperación, seleccione **Girar clave de recuperación de FileVault**.

     La próxima vez que el dispositivo se registre con Intune, se girará la clave personal. Cuando sea necesario, el usuario puede obtener la nueva clave a través del Portal de empresa.

### <a name="recover-recovery-keys"></a>Recuperación de claves de recuperación

- **Administrador**: los administradores no pueden ver las claves de recuperación personales de los dispositivos cifrados con FileVault.

- **Usuario final**: los usuarios finales usan el sitio web de Portal de empresa desde cualquier dispositivo para ver la clave de recuperación personal actual de cualquiera de sus dispositivos administrados. No puede ver las claves de recuperación en la aplicación Portal de empresa.

  Para ver una clave de recuperación, realice lo siguiente:
  
  1. Inicie sesión en el sitio web *Portal de empresa de Intune* desde cualquier dispositivo.

  2. En el portal, vaya a **Dispositivos** y seleccione el dispositivo macOS cifrado con FileVault.

  3. Seleccione **Obtener clave de recuperación**. Se muestra la clave de recuperación actual.

## <a name="next-steps"></a>Pasos siguientes

[Administración de directiva de BitLocker](../protect/encrypt-devices.md)

[Supervisión del cifrado de discos](../protect/encryption-monitor.md)
