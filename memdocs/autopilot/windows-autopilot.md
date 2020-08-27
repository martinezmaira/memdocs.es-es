---
title: Información general de Windows AutoPilot
description: Windows AutoPilot es una colección de tecnologías que se usan para configurar y preconfigurar nuevos dispositivos y prepararlos para su uso productivo.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 8c339e2a55fd8876ce8a144bb72c7c0a37de8346
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907839"
---
# <a name="overview-of-windows-autopilot"></a>Información general de Windows AutoPilot

**Se aplica a**

-  Windows 10

Windows AutoPilot es una colección de tecnologías que se usan para configurar y preconfigurar nuevos dispositivos y prepararlos para su uso productivo. También puede usar Windows AutoPilot para restablecer, reasignar y recuperar dispositivos. Esta solución permite al Departamento de ti lograr lo anterior con poca o ninguna infraestructura que administrar, con un proceso fácil y sencillo.

Windows AutoPilot simplifica el ciclo de vida de los dispositivos Windows, tanto para los usuarios de ti como para los finales, desde la implementación inicial hasta el final de su ciclo de vida. Usar servicios basados en la nube, Windows AutoPilot:
- reduce el tiempo que dedica a implementar, administrar y retirar dispositivos.
- reduce la infraestructura necesaria para mantener los dispositivos.
- maximiza la facilidad de uso para todos los tipos de usuarios finales.

Vea el siguiente vídeo y diagrama:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Información general del proceso](images/image1.png)

Cuando se implementan inicialmente nuevos dispositivos Windows, Windows AutoPilot usa la versión optimizada para OEM de Windows 10. Esta versión está preinstalada en el dispositivo, por lo que no tiene que mantener las imágenes y los controladores personalizados para cada modelo de dispositivo. En lugar de volver a crear la imagen del dispositivo, la instalación existente de Windows 10 se puede transformar en un estado "listo para la empresa" que pueda:
- aplicar la configuración y las directivas
- instalar aplicaciones
- cambie la edición de Windows 10 que se usa (por ejemplo, de Windows 10 Pro a Windows 10 Enterprise) para admitir características avanzadas.

Una vez implementado, puede administrar dispositivos de Windows 10 con:
- Microsoft Intune
- Windows Update para empresas
- Microsoft Endpoint Configuration Manager
- u otras herramientas similares.

Con Windows AutoPilot, puede preparar rápidamente un dispositivo para un nuevo usuario con el restablecimiento de Windows AutoPilot. También puede usar el restablecimiento en escenarios de interrupción y corrección para devolver rápidamente un dispositivo a un estado listo para la empresa.

Windows AutoPilot le permite:
* Unir dispositivos automáticamente a Azure Active Directory (Azure AD) o Active Directory (a través de Unión a Azure AD híbrido). Para obtener más información sobre las diferencias entre estas dos opciones de combinación, vea [Introducción a la administración de dispositivos en Azure Active Directory](/azure/active-directory/device-management-introduction).
* Inscripción automática de dispositivos en servicios MDM, como Microsoft Intune ([*requiere una suscripción Azure ad Premium para la configuración*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Restrinja la creación de la cuenta de administrador.
* Crear y asignar automáticamente dispositivos a grupos de configuración según el perfil de un dispositivo.
* Personalizar el contenido de OOBE específico de la organización.

## <a name="benefits-of-windows-autopilot"></a>Ventajas de Windows AutoPilot

Tradicionalmente, los profesionales de TI dedican mucho tiempo a crear y personalizar las imágenes que se implementarán posteriormente en los dispositivos. Windows AutoPilot presenta un enfoque nuevo.

Desde la perspectiva del usuario, solo realiza algunas operaciones sencillas para que el dispositivo esté listo para usarse.

Desde el punto de vista del profesional de ti, la única interacción requerida por el usuario final es conectarse a una red y comprobar sus credenciales. Todo lo más allá del que se automatiza.

## <a name="requirements"></a>Requisitos

Se requiere una [versión compatible](/windows/release-information/) del canal semianual de Windows 10 para usar Windows AutoPilot. También se admite Windows 10 Enterprise LTSC 2019. Para obtener más información, consulte requisitos de software, [redes](networking-requirements.md), [configuración](configuration-requirements.md)y [licencias](licensing-requirements.md) de [Windows AutoPilot](software-requirements.md).

## <a name="related-topics"></a>Temas relacionados

[Inscripción de dispositivos Windows en Intune mediante Windows AutoPilot](/intune/enrollment-autopilot)<br>
[Escenarios y funcionalidades de Windows AutoPilot](windows-autopilot-scenarios.md)