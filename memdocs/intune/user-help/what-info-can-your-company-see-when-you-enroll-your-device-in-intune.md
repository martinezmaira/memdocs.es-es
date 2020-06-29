---
title: ¿Qué información puede ver la empresa cuando el usuario inscribe el dispositivo?
description: Explica lo que el personal de TI puede y no puede ver en su dispositivo administrado.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
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
ms.openlocfilehash: 740d9b68a0101e04e6bf690d09ecce7eaff4509e
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107312"
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
 
 > [!NOTE]
 > Una aplicación se considera como **aplicación administrada** cuando se instala de una de las siguientes maneras:
 > 1. Un usuario la instala desde la aplicación Portal de empresa después de que un administrador de Intune la publique como **disponible**.
 > 2. Un administrador de Intune publica la aplicación como **requerida** y se instala en el dispositivo. 
 >
 > Si es administrador de TI o empleado de soporte técnico de su organización y quiere obtener más información sobre la administración de aplicaciones en Intune, consulte el artículo sobre la [descripción de las funcionalidades de las aplicaciones no administradas, las aplicaciones administradas y las aplicaciones MAM](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164).
    
**Contenido que su organización podría ver:**

- Número de teléfono: en el caso de los dispositivos propiedad de la empresa, se puede ver el número de teléfono completo. En el caso de los dispositivos personales, su organización solo puede ver los últimos cuatro dígitos de su número de teléfono. Puede ver el tipo de propiedad de cada dispositivo en la página **Detalles del dispositivo** correspondiente.
- Espacio de almacenamiento del dispositivo: si no puede instalar una aplicación necesaria, su organización podría consultar el espacio de almacenamiento del dispositivo para averiguar si el espacio es insuficiente.  
- Ubicación: En el caso de los dispositivos de propiedad corporativa, la organización puede ver la ubicación de un dispositivo perdido. En cuanto a los dispositivos personales, la organización nunca puede ver la ubicación del dispositivo, a menos que intente encontrar un dispositivo iOS supervisado que se haya perdido. Visite la [documentación de Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) para más información sobre los dispositivos supervisados.  
- Detalles del inventario de aplicaciones: si su organización usa Mobile Threat Defense, esta podrá consultar información adicional sobre las aplicaciones instaladas en su dispositivo iOS. Obtenga más información sobre [Mobile Threat Defense](set-up-mobile-threat-defense.md). En el caso de los dispositivos personales, la organización solo puede ver el inventario de aplicaciones administradas. En cuanto a los dispositivos de propiedad corporativa, la organización puede ver todo el inventario de aplicaciones.
- Información de red: parte de la información sobre las conexiones de red de los dispositivos Android puede estar disponible para el soporte técnico de su organización. Por ejemplo, si su organización exige que los dispositivos permanezcan dentro de cierto edificio, el dispositivo podría identificar la red donde está conectado. 
