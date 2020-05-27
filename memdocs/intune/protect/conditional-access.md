---
title: Acceso condicional con Microsoft Intune
titleSuffix: Microsoft Intune
description: Obtenga más información sobre cómo definir las condiciones que deben cumplir los usuarios, los dispositivos y las aplicaciones para acceder a los recursos de la empresa en Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/06/2018
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f7f4bf735ee5145bdad269a0ea6a6016d0ad97e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985963"
---
# <a name="learn-about-conditional-access-and-intune"></a>Más información sobre el acceso condicional e Intune

Con el acceso condicional, puede controlar los dispositivos y las aplicaciones que pueden conectarse a los recursos del correo electrónico y la empresa. 

Enterprise Mobility + Security (EMS) no es un producto independiente. Se trata de una solución incluida en todos los servicios y productos que forman parte de EMS. El acceso condicional ofrece un control de acceso granular para mantener seguros los datos corporativos y proporciona a los usuarios una experiencia que les permite trabajar desde cualquier dispositivo en cualquier parte.

Puede definir las condiciones que regulan el acceso a los datos corporativos en función de la ubicación, el dispositivo, el estado del usuario y la confidencialidad de la aplicación.

> [!NOTE]
> El acceso condicional también extiende sus funcionalidades a los [servicios de Office 365](https://docs.microsoft.com/office365/enterprise/office-365-client-support-conditional-access).

![Diagrama del acceso condicional](./media/conditional-access/ca-diagram-1.png)

## <a name="use-conditional-access-with-intune"></a>Uso del acceso condicional con Intune

El acceso condicional es una función de Azure Active Directory que se incluye con una licencia de Azure Active Directory Premium. Intune mejora esta función al agregar el cumplimiento de dispositivos móviles y la administración de aplicaciones móviles a la solución. 

![Intune y el acceso condicional cuando se usa EMS](./media/conditional-access/intune-with-ca-1.png)

Formas de usar el acceso condicional con Intune:

- **Acceso condicional basado en dispositivos**

  - Acceso condicional para Exchange local

  - Acceso condicional basado en el control de acceso a redes

  - Acceso condicional basado en el riesgo del dispositivo

  - Acceso condicional para equipos Windows

    - Propiedad corporativa

    - Bring your own device (BYOD)

- **Acceso condicional basado en la aplicación**

## <a name="next-steps"></a>Pasos siguientes

[Formas habituales de usar el acceso condicional con Intune](conditional-access-intune-common-ways-use.md)
