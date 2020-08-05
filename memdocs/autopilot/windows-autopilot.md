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
ms.openlocfilehash: 171070e1560796763f3c3851afe239237098f756
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757005"
---
# <a name="overview-of-windows-autopilot"></a>Información general de Windows AutoPilot

**Se aplica a**

-   Windows 10

Windows AutoPilot es una colección de tecnologías que se usan para configurar y preconfigurar nuevos dispositivos y prepararlos para su uso productivo. También puede usar Windows AutoPilot para restablecer, reasignar y recuperar dispositivos. Esta solución permite al Departamento de ti lograr lo anterior con poca o ninguna infraestructura que administrar, con un proceso fácil y sencillo.

Windows AutoPilot está diseñado para simplificar todas las partes del ciclo de vida de los dispositivos Windows, tanto de ti como de los usuarios finales, desde la implementación inicial hasta el final de la vida. Aprovechando los servicios basados en la nube, puede reducir los costos generales de la implementación, la administración y la retirada de dispositivos reduciendo la cantidad de tiempo que es necesario gastar en estos procesos y la cantidad de infraestructura que necesitan mantener, a la vez que se asegura la facilidad de uso para todos los tipos de usuarios finales. Vea el siguiente vídeo y diagrama:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Información general del proceso](images/image1.png)

Cuando se implementan inicialmente nuevos dispositivos Windows, Windows AutoPilot aprovecha la versión optimizada para OEM de Windows 10 que está preinstalada en el dispositivo, lo que ahorra a las organizaciones el esfuerzo de tener que mantener imágenes y controladores personalizados para cada modelo de dispositivo que se está usando. En lugar de volver a crear la imagen del dispositivo, la instalación existente de Windows 10 se puede transformar en un estado "listo para la empresa", aplicar la configuración y las directivas, instalar aplicaciones e incluso cambiar la edición de Windows 10 que se usa (por ejemplo, de Windows 10 Pro a Windows 10 Enterprise) para admitir características avanzadas.

Una vez implementados, los dispositivos de Windows 10 pueden administrarse mediante herramientas como Microsoft Intune, Windows Update para empresas, Configuration Manager de puntos de conexión de Microsoft y otras herramientas similares. Windows AutoPilot también puede usarse para cambiar el propósito de un dispositivo mediante el uso del restablecimiento de Windows AutoPilot para preparar rápidamente un dispositivo para un nuevo usuario o en escenarios de interrupción y corrección para permitir que un dispositivo se vuelva rápidamente a un estado listo para la empresa.

Windows AutoPilot le permite:
* Unir dispositivos automáticamente a Azure Active Directory (Azure AD) o Active Directory (a través de Unión a Azure AD híbrido).  Vea [Introducción a la administración de dispositivos en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) para obtener más información acerca de las diferencias entre estas dos opciones de combinación.
* Inscripción automática de dispositivos en servicios MDM, como Microsoft Intune ([*requiere una suscripción Azure ad Premium para la configuración*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Restrinja la creación de la cuenta de administrador.
* Crear y asignar automáticamente dispositivos a grupos de configuración según el perfil de un dispositivo.
* Personalizar el contenido de OOBE específico de la organización.

## <a name="benefits-of-windows-autopilot"></a>Ventajas de Windows AutoPilot

Tradicionalmente, los profesionales de TI dedican mucho tiempo a crear y personalizar las imágenes que se implementarán posteriormente en los dispositivos. Windows AutoPilot presenta un enfoque nuevo.

Desde la perspectiva del usuario, solo realiza algunas operaciones sencillas para que el dispositivo esté listo para usarse.

Desde el punto de vista del profesional de ti, la única interacción requerida por el usuario final es conectarse a una red y comprobar sus credenciales. Todo lo más allá del que se automatiza.

## <a name="requirements"></a>Requisitos

Se requiere una [versión compatible](https://docs.microsoft.com/windows/release-information/) del canal semianual de Windows 10 para usar Windows AutoPilot. También se admite Windows 10 Enterprise LTSC 2019. Consulte [requisitos de Windows AutoPilot](windows-autopilot-requirements.md) para obtener información detallada sobre el software, la configuración, la red y los requisitos de licencia.

## <a name="related-topics"></a>Temas relacionados

[Inscripción de dispositivos Windows en Intune mediante Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Escenarios y funcionalidades de Windows AutoPilot](windows-autopilot-scenarios.md)
