---
title: ¿Qué información puede ver la empresa cuando el usuario inscribe el dispositivo?
description: Explica lo que el personal de TI puede y no puede ver en su dispositivo administrado.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: ed3f9f6f01c8dc2df3a89daee991d9f8c61056b9
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210322"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>¿Qué información puede ver mi organización cuando inscribo mi dispositivo?

Su organización no puede ver su información personal cuando inscribe un dispositivo a Microsoft Intune. Cuando inscribe un dispositivo, da permiso a su organización para que pueda ver cierta información del dispositivo, como el modelo y el número de serie. Su organización usa esta información para proteger los datos corporativos del dispositivo.

**Contenido que no puede ver nunca su organización:**

- Historial de llamadas y exploración web
- Mensajes de texto y de correo electrónico
- Contactos
- Calendario
- Contraseñas
- Imágenes, ni siquiera lo que hay en la aplicación de fotos ni en el álbum de cámara
- Archivos

**Contenido que puede ver siempre su organización:**

- Modelo del dispositivo, como Google Pixel
- Fabricante del dispositivo (por ejemplo, Microsoft)
- Sistema operativo y versión (por ejemplo, iOS 12.0.1)
- Inventario de aplicaciones y nombres de aplicaciones (por ejemplo, Microsoft Word). en los dispositivos personales, su organización solo puede ver el inventario de aplicaciones administradas. En los dispositivos de propiedad corporativa, su organización puede ver todo el inventario de aplicaciones.
- Propietario del dispositivo
- Nombre del dispositivo
- Número de serie del dispositivo
- IMEI

 > [!NOTE]
 > En el caso de los dispositivos de Android Enterprise totalmente administrados y dedicados, no podrá ver todo el inventario de aplicaciones.    
    
**Contenido que su organización podría ver:**

- Número de teléfono: en el caso de los dispositivos propiedad de la empresa, se puede ver el número de teléfono completo. En el caso de los dispositivos personales, su organización solo puede ver los últimos cuatro dígitos de su número de teléfono. Puede ver el tipo de propiedad de cada dispositivo en la página **Detalles del dispositivo** correspondiente.
- Espacio de almacenamiento del dispositivo: si no puede instalar una aplicación necesaria, su organización podría consultar el espacio de almacenamiento del dispositivo para averiguar si el espacio es insuficiente.  
- Ubicación: su organización nunca puede ver la ubicación de su dispositivo, a menos que necesite recuperar un dispositivo iOS perdido supervisado. Visite la [documentación de Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) para más información sobre los dispositivos supervisados.  
- Detalles del inventario de aplicaciones: si su organización usa Mobile Threat Defense, esta podrá consultar información adicional sobre las aplicaciones instaladas en su dispositivo iOS. Obtenga más información sobre [Mobile Threat Defense](set-up-mobile-threat-defense.md). Si tiene un dispositivo personal, su organización solo puede ver el inventario de aplicaciones administradas. Si tiene un dispositivo de propiedad corporativa, su organización puede ver todo el inventario de aplicaciones.
- Información de red: parte de la información sobre las conexiones de red de los dispositivos Android puede estar disponible para el soporte técnico de su organización. Por ejemplo, si su organización exige que los dispositivos permanezcan dentro de cierto edificio, el dispositivo podría identificar la red donde está conectado. 
