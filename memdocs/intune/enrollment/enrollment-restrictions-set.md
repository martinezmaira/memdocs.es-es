---
title: Establecer restricciones de inscripción en Microsoft Intune
titleSuffix: ''
description: Restrinja las inscripciones por plataforma y establezca un límite de inscripciones de dispositivos en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/17/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f13be3c277605f11a1b16e9bcd3484cf4cdc7027
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907065"
---
# <a name="set-enrollment-restrictions"></a>Establecer restricciones de inscripción

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Como administrador de Intune, puede crear y administrar las restricciones de inscripción que definen los dispositivos que se pueden inscribir en la administración con Intune, lo que incluye:
- El número de dispositivos
- Los sistemas operativos y sus versiones

Puede crear varias restricciones y aplicarlas a diferentes grupos de usuarios. Puede establecer el [orden de prioridad](#change-enrollment-restriction-priority) para las distintas restricciones.

>[!NOTE]
>Las restricciones de inscripción no son características de seguridad. Los dispositivos en peligro pueden falsificar su carácter. Estas restricciones son un obstáculo al mejor esfuerzo para los usuarios no malintencionados.

Las restricciones de inscripción específicas que se pueden crear son:

- Número máximo de dispositivos inscritos.
- Plataformas de dispositivo que se pueden inscribir:
  - Administrador de dispositivos Android
  - Perfil de trabajo de Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows
- Versión del sistema operativo de la plataforma para iOS y iPadOS, el administrador de dispositivos Android, el perfil de trabajo de Android Enterprise y Windows.
  - Versión mínima.
  - Versión máxima.
- Restrinja los [dispositivos de propiedad personal](device-enrollment.md#bring-your-own-device) (iOS, administrador de dispositivos Android, perfil de trabajo de Android Enterprise, macOS y Windows).

## <a name="default-restrictions"></a>Restricciones predeterminadas

Las restricciones predeterminadas se proporcionan automáticamente para las restricciones de inscripción de tipo de dispositivo y límite de dispositivo. Puede cambiar las opciones para los valores predeterminados. Las restricciones predeterminadas se aplican a todos los usuarios e inscripciones sin usuario. Puede invalidar estos valores predeterminados mediante la creación de nuevas restricciones con prioridades más altas.

## <a name="create-a-device-type-restriction"></a>Creación de una restricción de tipo de dispositivo

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción** > **Crear restricción** > **Restricción de tipo de dispositivo**.
2. En la página **Aspectos batos básicos**, especifique la información de **Nombre** y, opcionalmente, **Descripción** de la restricción.
3. Elija **Siguiente** para ir a la página **Configuración de plataforma**.
4. En **Plataforma**, elija **Permitir** para las plataformas en las que quiera que esta restricción se permita.
    ![Captura de pantalla de la elección de configuración de plataforma](./media/enrollment-restrictions-set/choose-platform-settings.png)
5. En **Versiones**, elija las versiones mínima y máxima que quiera que admita la plataforma permitida. Para iOS y Android, las restricciones de versión solo se aplican a los dispositivos inscritos con el Portal de empresa.
     Entre los formatos de las versiones admitidas se incluyen los siguientes:
    - El administrador de dispositivos Android y el perfil de trabajo de Android Enterprise admiten major.minor.rev.build.
    - iOS/iPadOS admite major.minor.rev. Las versiones de sistema operativo no son relevantes en dispositivos Apple que se inscriban en el Programa de inscripción de dispositivos, Apple School Manager ni la aplicación Apple Configurator.
    - Windows admite major.minor.build.rev únicamente para Windows 10.
    
    > [!IMPORTANT]
    > Las plataformas del administrador de dispositivos Android y de Android Enterprise (perfil de trabajo) tienen el siguiente comportamiento:
    > - Si ambas plataformas están permitidas en el mismo grupo, los usuarios se inscribirán con un perfil de trabajo si el dispositivo lo admite; si no, se inscribirán como administradores de dispositivos. 
    > - Si ambas plataformas están permitidas en el grupo y se han refinado para versiones específicas y no superpuestas, los usuarios recibirán el flujo de inscripción definido para su versión del sistema operativo. 
    > - Si ambas plataformas se permiten, pero están bloqueadas en las mismas versiones, los usuarios de los dispositivos con las versiones bloqueadas se desconectarán del flujo de inscripción de administrador de dispositivos Android, se bloquearán de la inscripción y se les pedirá que cierren sesión. 
    >
    > Merece la pena mencionar que ni el perfil de trabajo ni la inscripción del administrador de dispositivos funcionarán a menos que se hayan completado los requisitos previos adecuados en la inscripción de Android. 
    
   > [!Note]
   > Windows 10 no proporciona el número de rev durante la inscripción; por lo tanto, si, por ejemplo, escribe 10.0.17134.100 y el dispositivo coincide con 10.0.17134.174, durante la inscripción este se bloqueará.

6. En **Propiedad personal**, elija **Permitir** para las plataformas que quiera permitir como dispositivos de propiedad personal.
7. En **Fabricante del dispositivo**, escriba una lista separada por comas de los fabricantes que desea bloquear.
8. Elija **Siguiente** para ir a la página **Etiquetas de ámbito**.
9. En la página **Etiquetas de ámbito**, puede agregar las etiquetas de ámbito que quiere aplicar a esta restricción. Para obtener más información sobre las etiquetas de ámbito, consulte [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Uso del control de acceso basado en roles y de las etiquetas de ámbito para la TI distribuida). Al usar etiquetas de ámbito con restricciones de inscripción, los usuarios solo pueden cambiar el orden de las directivas en las que tienen ámbito. Además, solo pueden cambiar el orden de las posiciones de directivas en las que tienen ámbito. Los usuarios ven el número de prioridad de directiva verdadero en cada directiva. Un usuario con ámbito puede indicar la prioridad relativa de sus directivas aunque no pueda ver todas las demás directivas.
10. Elija **Siguiente** para ir a la página **Asignaciones**.
11. Elija **Seleccionar grupos para incluir** y luego use el cuadro de búsqueda para buscar los grupos que quiere incluir en esta restricción. La restricción se aplica únicamente a los grupos a los que está asignada. Si no asigna una restricción al menos a un grupo, no tendrá ningún efecto. Luego, elija **Seleccionar**. 
    ![Captura de pantalla de la elección de configuración de plataforma](./media/enrollment-restrictions-set/select-groups.png)
12. Elija **Siguiente** para ir a la página **Revisar y crear**.
13. Seleccione **Crear** para crear la restricción.
14. La nueva restricción se crea con una prioridad justo por encima del valor predeterminado. También puede [cambiar la prioridad](#change-enrollment-restriction-priority).


## <a name="create-a-device-limit-restriction"></a>Creación de una restricción de límite de dispositivos

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción** > **Crear restricción** > **Restricción de límite de dispositivos**.
2. En la página **Aspectos batos básicos**, especifique la información de **Nombre** y, opcionalmente, **Descripción** de la restricción.
3. Elija **Siguiente** para ir a la página **Límite de dispositivo**.
4. En **Límite de dispositivo**, seleccione el número máximo de dispositivos que un usuario puede inscribir.
    ![Captura de pantalla de la elección del límite de dispositivos](./media/enrollment-restrictions-set/choose-device-limit.png)
5. Elija **Siguiente** para ir a la página **Etiquetas de ámbito**.
6. En la página **Etiquetas de ámbito**, puede agregar las etiquetas de ámbito que quiere aplicar a esta restricción. Para obtener más información sobre las etiquetas de ámbito, consulte [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Uso del control de acceso basado en roles y de las etiquetas de ámbito para la TI distribuida). Al usar etiquetas de ámbito con restricciones de inscripción, los usuarios solo pueden cambiar el orden de las directivas en las que tienen ámbito. Además, solo pueden cambiar el orden de las posiciones de directivas en las que tienen ámbito. Los usuarios ven el número de prioridad de directiva verdadero en cada directiva. Un usuario con ámbito puede indicar la prioridad relativa de sus directivas aunque no pueda ver todas las demás directivas.
7. Elija **Siguiente** para ir a la página **Asignaciones**.
8. Elija **Seleccionar grupos para incluir** y luego use el cuadro de búsqueda para buscar los grupos que quiere incluir en esta restricción. La restricción se aplica únicamente a los grupos a los que está asignada. Si no asigna una restricción al menos a un grupo, no tendrá ningún efecto. Luego, elija **Seleccionar**. 
    ![Captura de pantalla de selección de grupos](./media/enrollment-restrictions-set/select-groups-device-limit.png)
9. Elija **Siguiente** para ir a la página **Revisar y crear**.
10. Seleccione **Crear** para crear la restricción.
11. La nueva restricción se crea con una prioridad justo por encima del valor predeterminado. También puede [cambiar la prioridad](#change-enrollment-restriction-priority).

Durante las inscripciones de BYOD, los usuarios recibirán una notificación en la que se les informará cuando hayan alcanzado el límite de dispositivos inscritos. Por ejemplo, en iOS:

![Notificación del límite en un dispositivo iOS](./media/enrollment-restrictions-set/enrollment-restrictions-ios-set-limit-notification.png)

> [!IMPORTANT]
> No se aplican restricciones de límite de dispositivos para los siguientes tipos de inscripción de Windows:
> - Inscripciones con administración conjunta
> - Inscripciones de GPO
> - Inscripciones unidas a Azure Active Directory
> - Inscripciones masivas unidas a Azure Active Directory
> - Inscripciones de AutoPilot
> - Inscripciones del administrador de inscripciones de dispositivos
>
> No se aplican restricciones de límite de dispositivos para estos tipos de inscripción porque se consideran escenarios de dispositivos compartidos.
> Puede establecer límites estrictos para estos tipos de inscripción [en Azure Active Directory](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).


## <a name="change-enrollment-restrictions"></a>Cambio de las restricciones de inscripción

Para cambiar la configuración de una restricción de inscripción, siga estos pasos. Estas restricciones no afectan a los dispositivos que ya se han inscrito. Los dispositivos inscritos con el [agente de PC de Intune](../fundamentals/manage-windows-pcs-with-microsoft-intune.md) no se puede bloquear con esta característica.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción** > elija la restricción que quiera cambiar > **Propiedades**.
2. Elija **Editar** junto a la configuración que quiere cambiar.
3. En la página **Editar**, realice los cambios que quiera y siga en la página **Revisar y guardar**; luego, elija **Guardar**.


## <a name="blocking-personal-android-devices"></a>Bloquear dispositivos Android personales
- Aunque bloquee la inscripción de dispositivos del administrador de dispositivos Android de propiedad personal, aún pueden inscribirse los dispositivos del perfil de trabajo de Android Enterprise de propiedad personal.
- De forma predeterminada, la configuración de los dispositivos de perfil de trabajo de Android Enterprise es igual que la configuración de los dispositivos del administrador de dispositivos Android. Después de cambiar la configuración del perfil de trabajo de Android Enterprise o del administrador de dispositivos Android, ya no será así.
- Si bloquea la inscripción del perfil de trabajo personal de Android Enterprise, tan solo los dispositivos Android de propiedad corporativa podrán inscribirse como perfil de trabajo de Android Enterprise.

## <a name="blocking-personal-windows-devices"></a>Bloquear dispositivos Windows personales
Si impide la inscripción de dispositivos Windows de uso personal, Intune realiza comprobaciones para asegurarse de que se ha autorizado cada nueva solicitud de inscripción de Windows como una inscripción corporativa. Las inscripciones no autorizadas se bloquearán.

Los métodos siguientes se consideran como autorizados como una inscripción corporativa de Windows:
- El usuario que se inscribe usa una [cuenta de administrador de inscripción de dispositivos]( device-enrollment-manager-enroll.md).
- El dispositivo se inscribe a través de [Windows AutoPilot](../../autopilot/enrollment-autopilot.md).
- El dispositivo está registrado con Windows Autopilot, pero no es la única opción de inscripción de MDM que encontrará en la configuración de Windows.
- El número IMEI del dispositivo aparece en **Inscripción del dispositivo** >  **[Identificadores de dispositivo corporativos](corporate-identifiers-add.md)** .
- El dispositivo se inscribe a través de un [paquete de aprovisionamiento en masa](windows-bulk-enroll.md).
- El dispositivo se inscribe a través de GPO, o la [inscripción automática de Configuration Manager para la administración conjunta](/configmgr/comanage/quickstart-paths#bkmk_path1).
 
Intune marcó como corporativas las inscripciones siguientes. Pero se bloquearán porque no ofrecen control por dispositivo del administrador de Intune:
- [Inscripción automática de MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) con [combinación de Azure Active Directory durante la instalación de Windows](/azure/active-directory/device-management-azuread-joined-devices-frx)\*.
- [Inscripción automática de MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) con [combinación de Azure Active Directory desde la instalación de Windows](/azure/active-directory/user-help/user-help-register-device-on-network)*.
 
También se bloquearán los siguientes métodos de inscripción personal:
- [Inscripción automática de MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) con [incorporación de cuenta profesional desde la instalación de Windows](/azure/active-directory/user-help/user-help-join-device-on-network)\*.
- Opción de [solo inscripción de MDM]( /windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) desde la instalación de Windows.

\* Estos no se bloquearán si se han registrado con Autopilot.


## <a name="blocking-personal-iosipados-devices"></a>Bloquear dispositivos iOS/iPadOS personales
De forma predeterminada, Intune clasifica los dispositivos iOS/iPadOS como de propiedad personal. Para que se clasifiquen como de propiedad de la empresa, un dispositivo iOS/iPadOS debe cumplir una de las siguientes condiciones:
- [Estar registrado con un número de serie](corporate-identifiers-add.md).
- Estar inscrito mediante la Inscripción de dispositivo automatizada (anteriormente Programa de inscripción de dispositivos)


## <a name="change-enrollment-restriction-priority"></a>Cambiar la prioridad de las restricciones de inscripción

La prioridad se usa cuando un usuario existe en varios grupos a los que se asignan restricciones. Los usuarios solo están sujetos a la restricción de prioridad más alta asignada a un grupo al que pertenecen. Por ejemplo, Juan está en el grupo A asignado a restricciones de prioridad 5, así como en el grupo B asignado a restricciones de prioridad 2. Juan solo está sujeto a las restricciones de prioridad 2.

Cuando se crea una restricción, se agrega a la lista justo encima de la predeterminada.

La inscripción de dispositivos incluye restricciones predeterminadas para el tipo y límite de dispositivo. Estas dos restricciones se aplican a todos los usuarios a menos que se reemplacen por restricciones de prioridad más alta.

>[!NOTE]
>Las restricciones de inscripción se aplican a los usuarios. En escenarios de inscripción que no están basados en usuarios (por ejemplo, el modo de autoimplementación de Windows Autopilot o el aprovisionamiento preferencial), solo se aplicarán las restricciones de prioridad predeterminadas (destinadas a "Todos los usuarios").


Puede cambiar la prioridad de cualquier restricción que no sea la predeterminada.

1. Inicie sesión en Azure Portal.
2. Seleccione **Más servicios**, busque **Intune** y, después, seleccione **Intune**.
3. Seleccione **Inscripción de dispositivos** > **Restricciones de inscripción**.
4. Mantenga el puntero sobre la restricción en la lista de prioridades.
5. Con los tres puntos verticales, arrastre la prioridad a la posición deseada en la lista.