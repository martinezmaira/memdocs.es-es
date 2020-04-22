---
title: Acciones remotas con la administración conjunta
titleSuffix: Configuration Manager
description: Ejecute acciones remotas desde Intune para dispositivos administrados conjuntamente.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7dc4753a94dccf8a6a15751a436cecf8374e399
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691233"
---
# <a name="remote-actions-with-co-management"></a>Acciones remotas con la administración conjunta

Debe asegurarse de que se pueda acceder a cada dispositivo que administre, sin importar dónde esté, siempre que se conecte. También debe proporcionar a cada usuario todo lo que necesite para mantenerse productivo, al tiempo que protege las aplicaciones y los datos. Con las acciones del dispositivo compatibles con Intune, puede resolver estas funciones críticas de forma remota.

En el siguiente video, la Jefa Principal de Programas Heidi Cheng (F) y el Jefe de Programas Senior Danny Guillory debate sobre las acciones remotas con la administración conjunta y demuestran su funcionamiento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Ventajas

Las acciones remotas del dispositivo le brindan controles de administración en el dispositivo sin interferir con los datos personales. Estas acciones remotas del dispositivo le permiten: 
- Eliminar datos de la empresa en dispositivos perdidos o robados  
- Cambiar el nombre de un dispositivo  
- Reiniciar un dispositivo  
- Revisar el inventario de dispositivos  
- Controlar de forma remota un dispositivo  
- Borrar las aplicaciones de OEM preinstaladas con un reinicio para empezar de cero  
- Realizar una restablecimiento de la configuración de fábrica en cualquier dispositivo con Windows 10  

Estas funciones son una manera simple e importante de proteger los datos corporativos almacenados en estos dispositivos, ya sea en el correo electrónico o OneDrive.

Para obtener más información sobre estas acciones, consulte [Acciones remotas disponibles](#available-remote-actions). 



## <a name="case-studies"></a>Casos prácticos

La empresa de consultoría global Avanade utiliza regularmente acciones remotas para administrar los dispositivos utilizados por sus 30 000 empleados. En una [entrada de blog reciente](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), el director de sistemas de información indicaba lo siguiente:

> *Nuestra ventaja inmediata a raíz de tener la funcionalidad de Intune fue la capacidad de restablecer remotamente Windows en una máquina. Esto es importante para nosotros para equipos perdidos o robados, que es más común en nuestros recursos altamente móviles.* 
> *Esto es una funcionalidad que, en caso contrario, hubiésemos tenido que crear y mantener en un paquete personalizado de Configuration Manager.*

Para obtener más información sobre estas acciones, consulte [Acciones de dispositivo disponibles](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Propuesta de valor

Cuando un dispositivo de Configuration Manager se administra conjuntamente, agrega inmediatamente estas funciones que Configuration Manager no tiene de forma nativa. Ahora puede realizar cualquier acción remota que sea compatible con Intune. 

Con la administración conjunta, los dispositivos de Configuration Manager son exactamente iguales que cualquier otro dispositivo administrado por Intune. Por ejemplo, tienen una presencia completa en la nube y es posible acceder a ellos siempre que tengan acceso a Internet. Puede hacer todas estas acciones sin realizar ningún paso adicional más allá de habilitar la administración conjunta.

Puesto que el proceso de inscripción automática es transparente para el usuario, no hay impacto en su productividad. No es necesario que el usuario haga nada.


### <a name="available-remote-actions"></a>Acciones remotas disponibles

Utilice estas acciones remotas de Intune una vez que [habilite la administración conjunta](how-to-enable.md) en Configuration Manager.

#### <a name="remove-devices"></a>Retirada de dispositivos
- **Retirar**: Esta acción elimina las aplicaciones administradas y los datos (si procede), la configuración y los perfiles de correo electrónico que se asignaron a ese dispositivo. El dispositivo, a continuación, se quita de la administración de Intune. Este proceso ocurre la siguiente vez que el dispositivo se registra y recibe la acción remota de retirada. La función Retirar deja los datos personales del usuario en el dispositivo.  

- **Borrar**: Esta acción restaura el dispositivo a su configuración predeterminada de fábrica. Si elige la opción de **Conservar el estado de inscripción y la cuenta de usuario**, se mantienen los datos de usuario. En caso contrario, la unidad se borra de forma segura.  

- **Eliminar**: Si desea quitar los dispositivos de Intune en Azure Portal, puede eliminarlos desde el panel de dispositivos específicos. La próxima vez que se registre el dispositivo, se quitarán los datos de la organización almacenados en él.  

Para obtener más información, consulte [Eliminación de dispositivos mediante el borrado, la retirada o la anulación manual de la inscripción del dispositivo](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Borrado selectivo
<!--SCCMDocs issue 973-->
Cuando se elige un **Borrado selectivo de aplicaciones**, se quitan los datos de la aplicación de empresa sin quitar los datos personales. Use esta acción cuando un dispositivo se notifique como perdido o robado. 

Para obtener más información, consulte [Borrado solo de datos corporativos de aplicaciones administradas por Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>Sincronización
La acción del dispositivo **Sincronizar** obliga al dispositivo seleccionado a registrarse inmediatamente con Intune. Cuando un dispositivo se registra, recibe inmediatamente cualquier acción o directiva pendiente que se le haya asignado.

Esta característica puede ayudarle a validar y solucionar problemas de inmediato con las directiva que haya asignado, sin esperar al siguiente registro programado.

Para obtener más información, consulte [Sincronización de dispositivos para obtener las directivas y las acciones más recientes con Intune](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Reiniciar
La acción de dispositivo **Reiniciar** hace que el dispositivo que elija se reinicie. Esta acción resulta útil cuando hay un reinicio pendiente, pero el usuario no está disponible para hacerlo.

Para obtener más información, consulte [Reinicio remoto de los dispositivos con Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Empezar de cero
La acción del dispositivo **Empezar de cero** elimina cualquier aplicación instalada en un dispositivo que ejecute Windows 10, versión 1703 o posterior. Empezar de cero ayuda a eliminar aplicaciones preinstaladas (OEM) que normalmente se instalan con un nuevo dispositivo.

Si elige no conservar los datos de usuario, el dispositivo se restaura a su estado de inicio. Anula la inscripción de Azure AD y MDM.

Si tiene estándares predeterminados con respecto a qué aplicaciones deberían estar en el dispositivo, esta acción elimina las que no cumplen con sus criterios.

Para obtener más información, consulte [Uso de Empezar de cero para restablecer dispositivos Windows 10 con Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Control remoto
Los dispositivos administrados por Intune se pueden administrar de forma remota utilizando [TeamViewer](https://www.teamviewer.com/). TeamViewer es un programa de terceros que se adquiere por separado.

Para obtener más información, consulte [Uso de TeamViewer para administrar dispositivos de Intune de forma remota](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurar

Además del control remoto a través de TeamViewer, para comenzar a usar estas acciones remotas en dispositivos en Intune no se requiere ninguna configuración adicional después de que [habilite la administración conjunta](how-to-enable.md).

Para obtener más información sobre cómo usar TeamViewer para el control remoto, consulte [Uso de TeamViewer para administrar dispositivos de Intune de forma remota](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

