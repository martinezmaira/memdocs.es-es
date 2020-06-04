---
title: Cifrado de dispositivos Windows 10 con BitLocker en Intune
titleSuffix: Microsoft Intune
description: Cifre dispositivos con el método de cifrado integrado BitLocker y administre las claves de recuperación de esos dispositivos cifrados desde el portal de Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/18/2020
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
ms.openlocfilehash: 16a2558a0f4b002528e749f4a66d3341e83c8576
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989674"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Administración de la directiva de BitLocker para Windows 10 en Intune

Use Intune para configurar el Cifrado de unidad BitLocker en los dispositivos que ejecutan Windows 10.

BitLocker está disponible en dispositivos que ejecutan Windows 10 o versiones posteriores. Algunos valores de configuración de BitLocker requieren que el dispositivo tenga un TPM compatible.

Use uno de los tipos de directiva siguientes para configurar BitLocker en los dispositivos administrados:

- **[Directiva de cifrado de discos de seguridad de punto de conexión para BitLocker en Windows 10](#create-an-endpoint-security-policy-for-bitlocker)** . El perfil de BitLocker en *Seguridad de los puntos de conexión* es un grupo prioritario de opciones dedicado a la configuración de BitLocker.

  Vea la configuración de BitLocker disponible en [Perfiles de BitLocker en la directiva de cifrado de discos](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Perfil de configuración de dispositivo para protección de punto de conexión para BitLocker de Windows 10](#create-an-endpoint-security-policy-for-bitlocker)** . La configuración de BitLocker es una de las categorías de configuración disponibles para la protección de puntos de conexión de Windows 10.

  Vea las opciones de BitLocker disponibles para [BitLocker en los perfiles de protección de punto de conexión de la directiva de configuración de dispositivo](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune proporciona un [informe de cifrado](encryption-monitor.md) integrado que presenta los detalles sobre el estado de cifrado de los dispositivos en todos los dispositivos administrados. Después de que Intune cifre un dispositivo Windows 10 con BitLocker, podrá ver y recuperar las claves de recuperación de BitLocker cuando vea el informe de cifrado.
>
> También puede tener acceso a información importante para BitLocker desde sus dispositivos, tal como se ha encontrado en Azure Active Directory (Azure AD).
[Informe de cifrado](encryption-monitor.md) que presenta detalles sobre el estado de cifrado de los dispositivos en todos los dispositivos administrados.

## <a name="permissions-to-manage-bitlocker"></a>Permisos para administrar BitLocker

Para administrar BitLocker en Intune, la cuenta debe tener los permisos de [control de acceso basado en roles](../fundamentals/role-based-access-control.md) (RBAC) de Intune aplicables.

A continuación se muestran los permisos de BitLocker, que forman parte de la categoría Tareas remotas, y los roles de RBAC integrados que conceden el permiso:

- **Rotación de claves de BitLocker**
  - Operador del departamento de soporte técnico

## <a name="create-and-deploy-policy"></a>Creación e implementación de la directiva

Use uno de los procedimientos siguientes para crear el tipo de directiva que prefiera.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Creación de una directiva de seguridad de punto de conexión para BitLocker

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión** > **Cifrado de disco** > **Crear directiva**.

3. Establece las siguientes opciones:
   1. **Plataforma**: Windows 10 o posterior
   2. **Perfil**: BitLocker

   ![Selección del perfil de BitLocker](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. En la página **Opciones de configuración**, configure los valores de BitLocker para satisfacer las necesidades empresariales.  

   Si quiere habilitar BitLocker de forma silenciosa, vea [Habilitación en modo silencioso de BitLocker en dispositivos](#silently-enable-bitlocker-on-devices), en este artículo para obtener los requisitos previos adicionales y las configuraciones de opciones específicas que debe usar.

   Seleccione **Siguiente**.

5. En la página **Ámbito (etiquetas)** , seleccione **Seleccionar etiquetas de ámbito** para abrir el panel Seleccionar etiquetas a fin de asignar etiquetas de ámbito al perfil.

   Seleccione **Siguiente** para continuar.

6. En la página **Asignaciones**, seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea Asignación de perfiles de usuario y dispositivo.

   Seleccione **Siguiente**.

7. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Creación de un perfil de configuración de dispositivo para BitLocker

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Establece las siguientes opciones:
   1. **Plataforma**: Windows 10 y versiones posteriores
   2. **Tipo de perfil**: Endpoint Protection

   ![Selección del perfil de BitLocker](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Seleccione **Configuración** > **Cifrado de Windows**.

   ![Configuración de BitLocker](./media/encrypt-devices/bitlocker-settings.png)

5. Configure los valores de BitLocker para satisfacer las necesidades empresariales.

   Si quiere habilitar BitLocker de forma silenciosa, vea [Habilitación en modo silencioso de BitLocker en dispositivos](#silently-enable-bitlocker-on-devices), en este artículo para obtener los requisitos previos adicionales y las configuraciones de opciones específicas que debe usar.

6. Seleccione **Aceptar**.

7. Complete la configuración de valores adicionales y luego guarde el perfil.

## <a name="manage-bitlocker"></a>Administración de BitLocker

Para ver información sobre los dispositivos que reciben la directiva de BitLocker, vea [Supervisión de cifrado de discos](../protect/encryption-monitor.md). También puede ver y recuperar las claves de recuperación de BitLocker cuando vea el informe de cifrado.

### <a name="silently-enable-bitlocker-on-devices"></a>Habilitación en modo silencioso de BitLocker en dispositivos

Puede configurar una directiva de BitLocker que habilite de forma automática y silenciosa BitLocker en un dispositivo. Esto significa que BitLocker se habilita correctamente sin presentar ninguna interfaz de usuario al usuario final, aunque ese usuario no sea administrador local en el dispositivo.

**Requisitos previos del dispositivo**:

Un dispositivo debe cumplir las condiciones siguientes para ser apto para habilitar BitLocker de forma silenciosa:

- El dispositivo debe ejecutar Windows 10, versión 1809 o posterior
- El dispositivo debe estar unido a Azure AD  

**Configuración de directivas de BitLocker**:

Las dos opciones siguientes para la *Configuración base de BitLocker* se deben configurar en la directiva de BitLocker:

- **Advertencia para otro cifrado de disco** = *Bloquear*.
- **Permitir a los usuarios estándar habilitar el cifrado durante la unión a Azure AD** = *Permitir*

La directiva de BitLocker **no debe requerir** el uso de un PIN de inicio o una clave de inicio. Cuando se *requiere* un PIN de inicio o una clave de inicio de TPM, BitLocker no se puede habilitar en modo silencioso y requiere la interacción del usuario final.  Este requisito se cumple a través de las tres siguientes *configuraciones de unidad del sistema operativo de BitLocker* de la misma directiva:

- **PIN de inicio de TPM compatible** no se debe establecer en *Requerir PIN de inicio con TPM*
- **Clave de inicio de TPM compatible** no se debe establecer en *Requerir clave de inicio con TPM*
- **PIN y clave de inicio de TPM compatible** no se debe establecer en *Requerir clave y PIN de inicio con TPM*

### <a name="view-details-for-recovery-keys"></a>Visualización de detalles de las claves de recuperación

Intune proporciona acceso la hoja de Azure AD para BitLocker, para que pueda ver los identificadores de clave de BitLocker y las claves de recuperación para los dispositivos Windows 10, desde el portal de Intune. Para que sea accesible, el dispositivo debe tener sus claves custodiadas en Azure AD.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Todos los dispositivos**.

3. Seleccione un dispositivo de la lista y, en *Supervisión*, seleccione **Claves de recuperación**.
  
   Cuando las claves están disponibles en Azure AD, está disponible la siguiente información:
   - Identificador de clave de BitLocker
   - Clave de recuperación de BitLocker
   - Tipo de unidad

   Cuando las claves no están en Azure AD, Intune mostrará *No se encontró ninguna clave de BitLocker para este dispositivo*.

La información de BitLocker se obtiene mediante el [proveedor de servicios de configuración de BitLocker (CSP)](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp). El CSP de BitLocker se admite en Windows 10 versión 1703 y posteriores y en Windows 10 Pro versión 1809 y posteriores.

### <a name="rotate-bitlocker-recovery-keys"></a>Rotación de claves de recuperación de BitLocker

Puede usar una acción de dispositivo de Intune para rotar de forma remota la clave de recuperación de BitLocker de un dispositivo que ejecuta la versión 1909 o posterior de Windows 10.

#### <a name="prerequisites"></a>Requisitos previos

Los dispositivos deben cumplir los siguientes requisitos previos para admitir la rotación de la clave de recuperación de BitLocker:

- Deben ejecutar Windows 10, versión 1909 o posterior.

- Los dispositivos unidos a Azure AD o híbridos deben tener habilitada la compatibilidad con la rotación de claves:

  - **Rotación de contraseña de recuperación controlada por el cliente**

  Esta configuración se encuentra en *Cifrado de Windows* como parte de una directiva de configuración de dispositivos para Windows 10 Endpoint Protection.

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>Para rotar la clave de recuperación de BitLocker:

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Todos los dispositivos**.

3. En la lista de dispositivos que administra, seleccione un dispositivo, seleccione **Más** y, luego, seleccione la acción remota de dispositivo **Rotación de clave BitLocker**.

4. En la página **Información general** del dispositivo, seleccione la **Rotación de claves de BitLocker**. Si no ve esta opción, seleccione los puntos suspensivos ( **...** ) para mostrar otras opciones y, después, seleccione la acción remota de dispositivo **Rotación de claves de BitLocker**.

   ![Selección de los puntos suspensivos para ver más opciones](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Pasos siguientes

[Directiva de administración de FileVault](../protect/encrypt-devices-filevault.md)

[Supervisión del cifrado de discos](../protect/encryption-monitor.md)
