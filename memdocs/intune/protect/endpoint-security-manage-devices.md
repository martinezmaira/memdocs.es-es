---
title: Administración de dispositivos con seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Obtenga información sobre cómo los administradores de seguridad pueden usar el nodo Seguridad de los puntos de conexión para ver y administrar dispositivos en Microsoft Endpoint Manager.
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
ms.openlocfilehash: 98b1380254a784dfe8939c607ab574f7bdaa8752
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914997"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Administración de dispositivos con seguridad de puntos de conexión en Microsoft Intune

Como administrador de seguridad, puede usar la vista *Todos los dispositivos* del centro de administración de Microsoft Endpoint Manager para revisar y actuar a fin de administrar los dispositivos. En la vista se muestra una lista de todos los dispositivos de la instancia de Azure Active Directory (Azure AD). Esto incluye los dispositivos administrados por Intune, Configuration Manager y a través de la [administración conjunta](/configmgr/comanage/overview), tanto por medio de Intune como Configuration Manager. Los dispositivos pueden estar en la nube y en la infraestructura local cuando se integran con Azure AD.

 Para buscar la vista, abra el [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y seleccione **Seguridad de los puntos de conexión** > **Todos los dispositivos**.

En la vista *Todos los dispositivos* inicial se muestran los dispositivos y se incluye información clave sobre cada uno de ellos:

- Cómo se administra el dispositivo
- Estado de cumplimiento
- Detalles del sistema operativo
- La última vez que se ha sincronizado el dispositivo
- Y mucho más

![Vista Todos los dispositivos del centro de administración](./media/endpoint-security-manage-devices/all-device-view.png)

Al ver los detalles de los dispositivos, puede seleccionar uno para profundizar y obtener más información.

## <a name="available-details-by-management-type"></a>Detalles disponibles por tipo de administración

Al ver los dispositivos en el centro de administración de Microsoft Endpoint Manager, tenga en cuenta cómo se administra el dispositivo. El origen de administración afecta a la información que se presenta en el centro de administración y a las acciones disponibles para administrar el dispositivo.

Tenga en cuenta los campos siguientes:

- **Administrado por**: en esta columna se identifica cómo se administra el dispositivo. Las opciones de Administrado por son las siguientes:

  - **MDM**: estos dispositivos están administrados por Intune. Intune recopila los datos de cumplimiento y los envía al centro de administración.

  - **ConfigMgr**: estos dispositivos aparecen en el centro de administración de Microsoft Endpoint Manager cuando se usa la *asociación de inquilinos* para agregar los dispositivos que se administran con Configuration Manager. Para administrarlo, el dispositivo debe ejecutar el cliente de Configuration Manager y estar en:

    - Un grupo de trabajo (unido a AAD o de otro tipo)
    - Unido a un dominio
    - Unido a AAD híbrido (unido a AD y AAD)

    El estado de cumplimiento de los dispositivos administrados por Configuration Manager no es visible en el centro de administración de Microsoft Endpoint Manager.

    Para obtener más información, vea [Habilitación de la asociación de inquilinos](/configmgr/tenant-attach/device-sync-actions) en la documentación de Configuration Manager.

  - **Agente de MDM/ConfigMgr**: estos dispositivos están en administración conjunta entre Intune y Configuration Manager.

    Con la administración conjunta, se [eligen diferentes cargas de trabajo de administración conjunta](/configmgr/comanage/how-to-switch-workloads) para determinar qué aspectos se administran mediante Configuration Manager o Intune. Estas opciones afectarán a las directivas que se aplican al dispositivo y al modo en que se envían los datos de cumplimiento al centro de administración.

    Por ejemplo, puede usar Intune para configurar la directiva del antivirus, el firewall y el cifrado. Estos tipos de directivas se consideran una directiva para *Endpoint Protection*. Para que un dispositivo administrado de forma conjunta use las directivas de Intune y no las de Configuration Manager, establezca el control deslizante de administración conjunta de Endpoint Protection en *Intune* o *Intune piloto*. Si el control deslizante se establece en Configuration Manager, el dispositivo usa las directivas y la configuración de Configuration Manager en su lugar.

- **Cumplimiento**: el cumplimiento se evalúa de acuerdo a las directivas de cumplimiento que se asignan al dispositivo. El origen de estas directivas y la información que se encuentra en la consola depende de cómo se administre el dispositivo: mediante Intune, Configuration Manager o administración conjunta. Para que los dispositivos administrados conjuntamente notifiquen cumplimiento, establezca el control deslizante de administración conjunta para Conformidad de dispositivos en Intune o Intune piloto.  

  Después de notificar el cumplimiento del dispositivo al centro de administración, puede profundizar para ver detalles adicionales. Cuando un dispositivo no es compatible, profundice en sus detalles para obtener información sobre qué directivas no son compatibles. Esta información puede ayudarle a investigar y conseguir que el dispositivo sea compatible.

- **Última sincronización**: este campo identifica la última vez que el dispositivo ha comunicado su estado.

## <a name="review-a-devices-policy"></a>Revisión de la directiva de un dispositivo

Mientras examina la lista de dispositivos, puede seleccionar uno para profundizar y obtener más información si abre la página *Información general*  de ese dispositivo.

Desde la página Información general de un dispositivo, puede seleccionar **Configuración de seguridad del punto de conexión** para ver las directivas de seguridad del punto de conexión que se aplican a ese dispositivo. Los detalles de la directiva están disponibles para los dispositivos administrados por Intune y MDM.

![Visualización de los detalles de la directiva de seguridad de puntos de conexión](./media/endpoint-security-manage-devices/view-policy-details.png)

Los dispositivos administrados por Configuration Manager no muestran detalles de la directiva. Para ver información adicional para estos dispositivos, use la consola de Configuration Manager.

## <a name="remote-actions-for-devices"></a>Acciones remotas para dispositivos

Las acciones remotas son las que se pueden iniciar o aplicar a un dispositivo desde el centro de administración de Microsoft Endpoint Manager. Mientras examine los detalles de un dispositivo, puede acceder a las acciones remotas que se le aplican.

Las acciones remotas se muestran en la parte superior de la página *Información general* de los dispositivos. Las acciones que no se pueden mostrar porque hay espacio limitado en la pantalla están disponibles al seleccionar los puntos suspensivos del lado derecho:

![Visualización de acciones adicionales](./media/endpoint-security-manage-devices/view-additional-actions.png)

Las acciones remotas que están disponibles dependen de cómo se administra el dispositivo:

- **Intune**: todas las [acciones remotas de Intune](../remote-actions/device-management.md) que se aplican a la plataforma del dispositivo están disponibles.  
- **Configuration Manager**: puede usar las siguientes acciones de Configuration Manager:

  - Sincronizar directiva de máquina
  - Sincronizar directiva de usuario
  - Ciclo de evaluación de aplicaciones

- **Administración conjunta**: puede acceder a las acciones remotas de Intune y a las de Configuration Manager.

Algunas de las acciones remotas de Intune pueden ayudar a proteger los dispositivos o los datos que podrían estar en el dispositivo. Con las acciones remotas puede:

- Bloquear un dispositivo
- Restablecer un dispositivo
- Eliminar datos de la compañía
- Buscar malware fuera de una ejecución programada
- Rotar claves de BitLocker

Las siguientes acciones remotas de Intune son de interés para el administrador de seguridad y son un subconjunto de la [lista completa](../remote-actions/device-inventory.md#view-the-device-details). No todas las acciones están disponibles para todas las plataformas de dispositivos. Los vínculos van a contenido que proporciona información detallada sobre cada acción.

- [Sincronización de dispositivos](../remote-actions/device-sync.md): haga que el dispositivo se sincronice de forma inmediata con Intune. Cuando un dispositivo se sincroniza, recibe las acciones o directivas pendientes que se le han asignado.  

- [Reinicio](../remote-actions/device-restart.md): fuerce el reinicio de un dispositivo Windows 10, en un plazo de cinco minutos. Al propietario del dispositivo no se le notificará de forma automática el reinicio y podría perder trabajo.

- [Examen rápido](../configuration/device-restrictions-windows-10.md): haga que Defender realice un examen rápido del dispositivo en busca de malware y, después, envíe los resultados a Intune. Un examen rápido examina ubicaciones comunes donde podría haber malware registrado, como las claves del Registro y carpetas de inicio de Windows conocidas.

- [Examen completo](../configuration/device-restrictions-windows-10.md): haga que Defender realice un examen del dispositivo en busca de malware y, después, envíe los resultados a Intune. Un examen completo examina ubicaciones comunes donde podría haber malware registrado y también examina todos los archivos y las carpetas del dispositivo.

- Actualizar la inteligencia de seguridad de Windows Defender: haga que el dispositivo actualice sus definiciones de malware para Antivirus de Microsoft Defender. Esta acción no inicia un examen.

- [Rotación de claves de BitLocker](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key): rote de forma remota la clave de recuperación de BitLocker de un dispositivo que ejecuta la versión 1909 o posterior de Windows 10.

También puede usar **Acciones masivas del dispositivo** para administrar algunas acciones como *Retirar* y *Borrar* para varios dispositivos al mismo tiempo. [Acciones en masa](../remote-actions/bulk-device-actions.md) están disponibles en la vista *Todos los dispositivos*. Seleccione la plataforma, la acción y, después, especifique hasta 100 dispositivos.

![Selección de acciones en masa](./media/endpoint-security-manage-devices/select-bulk-actions.png)

Las opciones que administre para los dispositivos no surten efecto hasta que los sincronice con Intune.

## <a name="next-steps"></a>Pasos siguientes

[Administración de la seguridad de puntos de conexión en Intune](../protect/endpoint-security.md)