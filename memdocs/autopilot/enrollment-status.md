---
title: Página estado de inscripción de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Proporciona información general sobre las capacidades de la página estado de inscripción, configuración
keywords: AutoPilot plug and olvídese, Windows 10
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a7d368aef0b10fbe78e2c4ca141a39aa4ed6d803
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606607"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Página estado de inscripción de Windows AutoPilot

**Se aplica a**

-  Windows 10, versión 1803 y posteriores 

Cuando un usuario inicia sesión en un dispositivo por primera vez, la página de estado de inscripción (ESP) muestra el progreso de la configuración del dispositivo. ESP también se asegura de que el dispositivo se encuentra en el estado esperado antes de que el usuario pueda tener acceso al escritorio por primera vez.

El ESP realiza un seguimiento de la instalación de las aplicaciones, las directivas de seguridad, los certificados y las conexiones de red. Un administrador puede implementar perfiles ESP en un usuario de Intune con licencia y configurar opciones específicas en el perfil ESP. Algunos de estos valores son:
- Forzar la instalación de las aplicaciones especificadas.
- Permitir a los usuarios recopilar registros de solución de problemas.
- Especificar lo que puede hacer un usuario si se produce un error en la configuración del dispositivo.

Para obtener más información, consulte Configuración de la [Página de estado de inscripción en Intune](/intune/windows-enrollment-status).  
 
![Página de estado de inscripción](images/enrollment-status-page.png)
 

## <a name="more-information"></a>Más información

Para obtener más información sobre la configuración de la página estado de inscripción, consulte la [documentación de Microsoft Intune](/intune/windows-enrollment-status).<br>
Para obtener más información sobre la implementación subyacente, consulte los [detalles de FirstSyncStatus en la documentación de DMCLIENT CSP](/windows/client-management/mdm/dmclient-csp).<br>
Para obtener más información sobre el bloqueo de la instalación de aplicaciones:
- [Bloqueando la instalación de aplicaciones mediante la página estado de inscripción](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page).
- [Sugerencia de soporte: ahora se realiza un seguimiento de la instalación de Office C2R durante ESP](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).
