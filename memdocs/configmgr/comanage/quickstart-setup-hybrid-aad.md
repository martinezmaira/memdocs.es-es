---
title: Configuración de Azure AD híbrido
titleSuffix: Configuration Manager
description: Si el entorno actualmente tiene dispositivos Windows 10 unidos al dominio, configure Azure AD híbrido antes de habilitar la administración conjunta.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e2f7bbb51c72fa3d0f2a36e8a5419552d468b4c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691223"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configuración de Azure AD híbrido para la administración conjunta

Si tiene dispositivos Windows 10 unidos a una instancia local de Active Directory, antes de habilitar la administración conjunta en Configuration Manager, una estos dispositivos a Azure Active Directory (Azure AD). A este proceso se le denomina Unión a Azure AD híbrido. 

En el vídeo siguiente, el Jefe de Programas Senior Sandeep Deo y el Jefe de Marketing de Productos Adam Harbour analizan y demuestran la configuración de dispositivos en Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

El proceso de unión a Azure AD híbrido registra automáticamente los dispositivos unidos a un dominio local con Azure AD. Para más información sobre este proceso, vea los siguientes artículos:
- [¿Qué es la administración de dispositivos en Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Planeamiento de la implementación de la unión a Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

La unión a Azure AD híbrido es uno de los aspectos clave de la administración conjunta. Este proceso puede ser todo un desafío para algunos clientes, por ejemplo:
- La organización usa una solución de identidad de terceros 
- Las complejidades de configurar los Servicios de federación de Active Directory (AD FS)

Puede ser necesario contar con algunas guías para resolver estos desafíos. En este artículo se ayuda a mitigar cualquier retraso.


## <a name="how-to-do-it"></a>Cómo hacerlo

Los dispositivos son similares a los usuarios cuando se crea una identidad que quiere proteger. Para proteger la identidad de un dispositivo en cualquier momento y en cualquier ubicación, debe introducir la identidad de ese dispositivo en Azure AD.

Según el tipo de dominio que usa, hay dos maneras principales de hacerlo. Configure la unión a Azure AD híbrido para uno de estos tipos de dominio:  
- [Dominios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Dominios administrados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Los dos métodos anteriores ofrecen la mejor experiencia. Para información más detallada, incluido el proceso completamente manual, consulte estos artículos:
- [Manually configure hybrid Azure AD joined devices](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (Configuración manual de dispositivos unidos a Azure AD híbrido)  
- [ADFS pass-through authentication for hybrid Azure AD](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview) (Autenticación de paso a través de ADFS para Azure AD híbrido), que incluye la detección de Azure AD  

Para guías de solución de problemas, consulte el artículo de la [guía de soluciones de problemas en la unión a Azure AD híbrido de Windows 10](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Caso práctico

Una empresa de software europea de gran tamaño, con más de 100 000 usuarios en su red, adoptó un enfoque detallado en fases con respecto a la habilitación de la unión a Azure AD híbrido.

Durante la fase de planeamiento, como la unión a Azure AD híbrido es un elemento clave para la administración conjunta, los administradores de Configuration Manager trabajaron junto con el equipo de identidad. Esta empresa de software tenía muchas reglas de ADFS, algunas de las cuales eran complejas. Para abordar este desafío, el equipo de identidad revisó las reglas de ADFS existentes antes de que se habilitara la unión a Azure AD híbrido. El equipo de TI también eligió actualizar Azure AD Connect a la versión más reciente. Ahora, Azure AD Connect proporciona un flujo de proceso automatizado para habilitar la unión a Azure AD híbrido.

Después de una implementación correcta y de probar en el entorno de preproducción, este cliente habilitó la unión a Azure AD híbrida para todo el espacio de producción. Dentro de una semana, todos los dispositivos Windows 10 se administraban de manera conjunta.



## <a name="contact-fasttrack"></a>Póngase en contacto con FastTrack

Si necesita ayuda para configurar Azure AD en cualquier punto del proceso, vaya a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sesión y solicite ayude. 

Para más información, consulte [Ayuda de FastTrack](quickstart-fasttrack.md). 

