---
title: Actualización de Windows 10
titleSuffix: Configuration Manager
description: Actualice los dispositivos a la versión 1709 o posterior de Windows 10, un requisito para la administración conjunta
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691203"
---
# <a name="upgrade-windows-10-for-co-management"></a>Actualización de Windows 10 para la administración conjunta

A medida que trabaja para incorporar su organización a la administración conjunta, ponerse al día es un obstáculo importante para algunos clientes. La administración conjunta requiere [Windows 10, versión 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) o posterior. Una vez que actualiza Windows y configura la inscripción automática, los clientes se inscriben automáticamente en la administración conjunta.

En el siguiente vídeo, el Jefe de Programas Senior Rob York y el Jefe de Marketing de Productos Locky Ainley abordan la actualización a Windows 10 para la administración conjunta y demuestran su funcionamiento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>¿Por qué actualizar?

Entre otros avances de plataforma, la versión 1709 y posteriores de Windows 10 admiten la inscripción automática. Este comportamiento hace que un dispositivo se inscriba automáticamente en Intune cuando se une a Azure Active Directory (Azure AD). 

Para más información, consulte [Habilitar la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Cómo hacerlo

Estas son algunas sugerencias que aprendimos después de ayudar a miles de clientes a ponerse al día rápidamente:

- Use implementaciones en fases para implementar esta actualización a las personas adecuadas en los momentos indicados. Para más información, vea [Crear implementaciones por fases](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Use almacenamiento en caché previa para disminuir los tiempos de espera del usuario. Para obtener más información, vea [Configuración del contenido de la caché previa](../osd/deploy-use/configure-precache-content.md).  

- Use la plantilla para la secuencia de tareas de actualización local predeterminada. Luego, configure los pasos para antes y después de la actualización y cualquier acción en caso de error. Para más información, consulte [Pasos de la secuencia de tareas recomendados para posprocesamiento](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- Si el entorno tiene una fuerza laboral altamente móvil, Configuration Manager admite la actualización local a través de Cloud Management Gateway (CMG). Esta característica permite actualizar los clientes de Windows 10 cuando se basan en Internet. Para más información sobre CMG, vea [Implementar una actualización local de Windows 10 a través de CMG](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Ofrezca una participación en la administración conjunta de los usuarios que quieren ser usuarios pioneros. Este enfoque acelera la adopción inicial. Si identifica a estos usuarios de antemano, puede garantizar una buena cobertura en los primeros días de un lanzamiento. También podrá recibir la validación y los comentarios de los usuarios que se sienten felices de cambiar y que están interesados en lanzamientos más frecuentes. Los programas para los usuarios pioneros generan interés en las nuevas tecnologías y aumentan de tamaño con el tiempo.  


## <a name="case-studies"></a>Casos prácticos

Microsoft IT implementó Windows 10 en 96 000 usuarios distribuidos en Microsoft. La implementación incluyó tanto a usuarios remotos como a usuarios de la red corporativa. La implementación se completó en nueve semanas. Para más información sobre su experiencia, consulte el documento [Deploying Windows 10 at Microsoft as an in-place upgrade](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade) (Implementación de Windows 10 en Microsoft como una actualización local).  

Un fabricante europeo de software de gran tamaño usa exitosamente un grupo de usuarios pioneros. Después de las pruebas iniciales y los grupos piloto, unos 2000 empleados reciben las primeras actualizaciones y software. En este grupo se cuenta el personal de TI y usuarios voluntarios. Este nivel de compromiso con sus usuarios les brinda un mayor nivel de confianza al realizar las pruebas y más credibilidad cuando empiecen las implementaciones masivas.



## <a name="contact-fasttrack"></a>Póngase en contacto con FastTrack

Si necesita ayuda con la actualización de Windows 10 en cualquier punto del proceso, vaya a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sesión y solicite ayuda. 

Para más información, consulte [Ayuda de FastTrack](quickstart-fasttrack.md). 

