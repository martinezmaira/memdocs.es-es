---
title: 'Partners de cumplimiento de dispositivos en Microsoft Intune: Azure | Microsoft Docs'
description: Use un partner externo de cumplimiento de dispositivos como origen de datos de cumplimiento de los dispositivos que administra con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643710"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Compatibilidad con partners externos de cumplimiento de dispositivos en Intune

Microsoft Intune puede agregar datos de estado de cumplimiento a Azure Active Directory (Azure AD) para los dispositivos que administra con uno o más partners externos de cumplimiento de dispositivos. Con esta configuración, los datos de cumplimiento de esos dispositivos se pueden usar con sus directivas de acceso condicional.

De forma predeterminada, Intune está configurado para ser la entidad de administración de dispositivos móviles (MDM) para sus dispositivos. Al agregar un partner de cumplimiento a Azure AD e Intune, está configurando ese partner para que sea un origen de la entidad de administración de dispositivos móviles (MDM) para los dispositivos que asigne a ese partner a través de un grupo de usuarios de Azure AD.

Para habilitar el uso de datos de partners de cumplimiento de dispositivos, complete las tareas siguientes:

1. **Configure Intune para que funcione con el partner de cumplimiento de dispositivos** y, después, configure grupos de usuarios cuyos dispositivos están administrados por ese partner de cumplimiento.

2. **Configure el partner de cumplimiento para que envíe datos a Intune**.

3. **Inscriba sus dispositivos iOS o Android en ese partner de cumplimiento de dispositivos**.

Una vez finalizadas estas tareas, el partner de cumplimiento de dispositivos envía detalles sobre el estado del dispositivo a Intune. A continuación, Intune agrega esta información a Azure AD. Por ejemplo, los dispositivos cuyo estado es no conforme, tienen ese estado agregado a su registro de dispositivo en Azure AD.

Después, el estado de cumplimiento se evalúa mediante directivas de acceso condicional, al igual que los datos de estado de cumplimiento en los dispositivos administrados por Intune.  De forma predeterminada, Intune es un partner de cumplimiento registrado para iOS y Android. Si agrega otros partners, puede establecer el orden de prioridad para asegurarse de que el partner adecuado administra el dispositivo para que se adapte a sus necesidades empresariales.

## <a name="supported-device-compliance-partners"></a>Partners de cumplimiento de dispositivos admitidos

En versión preliminar pública:

- VMware Workspace ONE UEM (antes AirWatch)

## <a name="prerequisites"></a>Requisitos previos

- Suscripción a Microsoft Intune y acceso al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

- Suscripción al partner de cumplimiento de dispositivos.

- Revise la documentación de su partner de cumplimiento para conocer las plataformas de dispositivos compatibles y los requisitos previos adicionales.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Configuración de Intune para trabajar con un partner de cumplimiento de dispositivos

Habilite la compatibilidad con un asociado de cumplimiento de dispositivos para usar los datos de estado de cumplimiento de ese asociado con las directivas de acceso condicional.

### <a name="add-a-compliance-partner-to-intune"></a>Adición de un partner de cumplimiento a Intune

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vaya a **Administración de inquilinos** > **Conectores y tokens** > **Administración de cumplimiento de partners** > **Agregar partner de cumplimiento**.

   > [!div class="mx-imgBorder"]
   > ![Adición de un partner de cumplimiento de dispositivos](./media/device-compliance-partners/add-compliance-partner.png)

3. En la página **Datos básicos**, expanda la lista desplegable **Partner de cumplimiento** y seleccione el partner que va a agregar.

   - Para usar VMware Workspace ONE UEM como asociado de cumplimiento para plataformas iOS o Android, seleccione **VMware Workspace ONE mobile compliance** (Cumplimiento con dispositivos móviles de VMware Workspace ONE).

   Después, seleccione la lista desplegable de **Plataforma** y seleccione la plataforma. macOS no es compatible con esta versión preliminar.

   Está limitado a un solo partner por plataforma, incluso aunque haya agregado varios partners de cumplimiento a Azure AD.

4. En **Asignaciones**, seleccione los grupos de usuarios que tendrán dispositivos administrados por este partner. Con esta asignación, cambiará la entidad de MDM para que los dispositivos aplicables usen este partner. Los usuarios que tengan dispositivos administrados por el asociado también deben tener asignada una licencia de Intune.

5. En la página **Revisar y crear**, revise las selecciones y, después, seleccione **Crear** para completar esta configuración.

La configuración aparece ahora en la página Administración de cumplimiento de partners.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Modificación de la configuración de un partner de cumplimiento

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vaya a **Administración de inquilinos** > **Conectores y tokens** > **Administración de cumplimiento de partners** y, después, seleccione la configuración de partner que quiera modificar. Las configuraciones están ordenadas por tipo de plataforma.

3. En la página **Información general** de la configuración del partner, seleccione **Propiedades** para abrir la página Propiedades en la que podrá editar las asignaciones.

4. En la página **Propiedades**, seleccione **Editar** para abrir la vista Asignaciones, en la que podrá cambiar los grupos que usarán esta configuración.

5. Seleccione **Revisar y guardar** y, luego, **Guardar** para guardar los cambios.

6. *Este paso solo se aplica cuando se usa VMware Workspace ONE*:

   En la consola de VMware Workspace ONE, debe sincronizar manualmente los cambios guardados en el centro de administración de Microsoft Endpoint Manager. Hasta que se sincronicen manualmente los cambios, VMware Workspace ONE no tiene constancia de los cambios de configuración y los usuarios de los grupos nuevos que ha asignado no notificarán correctamente el cumplimiento.

   Para realizar una sincronización manual desde los servicios de Azure:
   1. Inicie sesión en la consola de VMware Workspace ONE UEM.
   2. Vaya a **Settings** > **System** > **Enterprise Integration** > **Directory Services** (Configuración > Sistema > Integración empresarial > Servicios de directorio).
   3. En *Sync Azure Services* (Sincronizar servicios de Azure), haga clic en **SYNC** (SINCRONIZAR).

      Todos los cambios realizados en los servicios de Azure desde la configuración inicial o la última sincronización manual se sincronizan con UEM.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Configuración del partner de cumplimiento para que funcione con Intune

Para permitir que un partner de cumplimiento de dispositivos funcione con Intune, se deben completar las configuraciones específicas de ese partner. Para obtener información sobre esta tarea, consulte la documentación correspondiente al partner:

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Inscripción de dispositivos iOS o Android en el partner de cumplimiento de dispositivos

Consulte la documentación de los partners de cumplimiento de dispositivos para obtener información sobre cómo inscribir dispositivos con ese partner. Después de la inscripción de dispositivos y del envío de datos de cumplimiento al partner, esos datos de cumplimiento se reenvían a Intune y se agregan a Azure AD.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Supervisión de dispositivos administrados por partners externos de cumplimiento de dispositivos

Después de configurar partners externos de cumplimiento de dispositivos e inscribir dispositivos con ellos, el partner reenviará los detalles de cumplimiento a Intune. Después de que Intune reciba esos datos, puede ver los detalles de los dispositivos en Azure Portal.

Inicie sesión en Azure Portal y vaya a **Azure AD** > **Dispositivos** > [**Todos los dispositivos**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## <a name="next-steps"></a>Pasos siguientes

Use la documentación de su asociado de terceros para crear directivas de cumplimiento para los dispositivos.

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
