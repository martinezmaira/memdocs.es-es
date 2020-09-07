---
title: Información general sobre Microsoft Endpoint Manager - Azure | Microsoft Docs
description: Endpoint Manager incluye Intune, Configuration Manager, administración conjunta, Análisis de escritorio, Windows Autopilot y el centro de administración para administrar todos los dispositivos, incluido el entorno local.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d638cb382aa7abe8859648192837601c86f22ce
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996561"
---
# <a name="microsoft-endpoint-manager-overview"></a>Información general sobre Microsoft Endpoint Manager

Microsoft Endpoint Manager ayuda a proporcionar el área de trabajo y las funciones de administración modernas para mantener los datos en condiciones de seguridad, tanto en la nube como en el entorno local. Endpoint Manager incluye los servicios y herramientas que se usan para administrar y supervisar dispositivos móviles, equipos de escritorio, máquinas virtuales, dispositivos insertados y servidores.

Endpoint Manager combina servicios que es posible que conozca y ya esté usando, como Microsoft Intune, Configuration Manager, Análisis de escritorio, administración conjunta y Windows AutoPilot. Estos servicios forman parte de la pila de Microsoft 365 para ayudar a garantizar un acceso seguro, proteger los datos y responder y administrar los riesgos.

Comience viendo el siguiente vídeo de dos minutos de Brad Anderson, vicepresidente corporativo de Microsoft para Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Qué obtiene

Endpoint Manager incluye los siguientes servicios:

- **Microsoft Intune**: Intune es un proveedor totalmente basado en la nube de administración de dispositivos móviles (MDM) y administración de aplicaciones móviles (MAM) para sus aplicaciones y dispositivos. La permite controlar características y parámetros de configuración en dispositivos Android, Android Enterprise, iOS/iPadOS, macOS y Windows 10. Se integra con otros servicios, como Azure Active Directory (AD), defensores contra amenazas móviles, plantillas ADMX, aplicaciones de LOB personalizadas y Win32, etc.

  Si tiene una infraestructura local, como Exchange o una instancia de Active Directory, también están disponibles los conectores de Intune:

  - El **conector de Intune para Active Directory** agrega entradas al dominio de Active Directory local para los equipos que se inscriben con Windows Autopilot. Para obtener más información, vea [Implementación de dispositivos unidos a Azure AD híbridos](./autopilot/windows-autopilot-hybrid.md).
  - **Intune Certificate Connector** procesa las solicitudes de certificado de los dispositivos que usan certificados para la autenticación y el cifrado de correo electrónico S/MIME. Para obtener más información, vea [Uso de certificados para la autenticación](./intune/protect/certificates-configure.md).

  Como parte de Endpoint Manager, use Intune para crear y comprobar la compatibilidad e implementar aplicaciones, características y configuraciones en los dispositivos mediante la nube.

  Para más información, vea [¿Qué es Microsoft Intune?](/intune/fundamentals/what-is-intune)

- **Configuration Manager**: Configuration Manager es una solución de administración local para administrar equipos de escritorio, servidores y equipos portátiles que se encuentran en la red o en Internet. Puede habilitarla en la nube para que se integre con Intune, Azure Active Directory (AD), ATP de Microsoft Defender y otros servicios en la nube. Use Configuration Manager para implementar aplicaciones, actualizaciones de software y sistemas operativos. También puede supervisar el cumplimiento, consultar los clientes en tiempo real y actuar en ellos (y mucho más).

  Como parte de Endpoint Manager, siga usando Configuration Manager como siempre lo ha hecho. Si está listo para trasladar algunas tareas a la nube, considere la posibilidad de usar la [administración conjunta](/configmgr/comanage/).

  Para obtener más información, vea [¿Qué es Configuration Manager?](/configmgr/core/understand/introduction)

- **Administración conjunta**: la administración conjunta combina su inversión de Configuration Manager local existente con la nube mediante Intune y otros servicios en la nube de Microsoft 365. Elija si Configuration Manager o Intune es la entidad de administración de los siete grupos de cargas de trabajo diferentes.

  Como parte de Endpoint Manager, la administración conjunta utiliza características en la nube, incluido el acceso condicional. Mantiene algunas tareas locales, mientras ejecuta otras tareas en la nube con Intune.

  Para más información, vea [What is co-management?](/configmgr/comanage/overview) (¿Qué es la administración conjunta?).

- **Análisis de escritorio**: Análisis de escritorio es un servicio basado en la nube que se integra con Configuration Manager. Proporciona información detallada e inteligente para que pueda tomar decisiones más fundamentadas sobre la preparación de actualizaciones de sus clientes Windows. El servicio combina datos de su organización con datos agregados de millones de dispositivos conectados a la nube de Microsoft. Proporciona información sobre las actualizaciones de seguridad, las aplicaciones y los dispositivos de la organización, e identifica los problemas de compatibilidad con las aplicaciones y los controladores. Cree una prueba piloto para que los dispositivos tengan más probabilidades de proporcionar la mejor información para los recursos de toda la organización.

  Como parte de Endpoint Manager, use la información con tecnología de la nube de Análisis de escritorio para mantener actualizados los dispositivos Windows 10.

  Vea [¿Qué es Análisis de escritorio?](/configmgr/desktop-analytics/overview) para obtener más información.

- **Windows Autopilot**: Windows Autopilot prepara y configura previamente nuevos dispositivos y los prepara para su uso. Está diseñado para simplificar el ciclo de vida de los dispositivos Windows, tanto para los usuarios de TI como para los finales, desde la implementación inicial hasta el final de su ciclo de vida.

  Como parte de Endpoint Manager, use Autopilot para preconfigurar dispositivos e inscribirlos automáticamente en Intune. También puede integrar Autopilot con Configuration Manager y la administración conjunta para configuraciones de dispositivo más complejas (en versión preliminar).

  Para más información, consulte [Introducción a Windows Autopilot](/windows/deployment/windows-autopilot/windows-autopilot) e [Inscripción de dispositivos Windows en Intune](./autopilot/enrollment-autopilot.md).

- **Azure Active Directory (AD)** : Endpoint Manager usa Azure AD para la identidad de dispositivos, usuarios, grupos y Multi-Factor Authentication (MFA). **Azure AD Premium**, que puede ser un costo añadido, tiene [características adicionales](https://azure.microsoft.com/pricing/details/active-directory/) para ayudar a proteger los dispositivos, las aplicaciones y los datos, incluidos los grupos dinámicos, la inscripción automática y el acceso condicional.

  Para obtener más información, vea [Adición de usuarios](./intune/fundamentals/users-add.md), [Configuración de la inscripción de dispositivos Windows](./intune/enrollment/windows-enroll.md) y [Más información sobre el acceso condicional](./intune/protect/conditional-access.md).

- **Centro de administración de Endpoint Manager**: el [centro de administración](https://go.microsoft.com/fwlink/?linkid=2109431) es un sitio web único para crear directivas y administrar los dispositivos. Se conecta a otros servicios clave de administración de dispositivos, incluidos los grupos, la seguridad, el acceso condicional y los informes. Este centro de administración también muestra los dispositivos administrados por Configuration Manager e Intune (en versión preliminar).

## <a name="choose-whats-right-for-you"></a>Selección de lo más conveniente

Hay varias maneras de determinar qué es lo más adecuado para la organización. Los pasos siguientes dependen de lo que hace la organización. Tenga en cuenta lo que está intentando lograr.

Por ejemplo:

- Si aprovisiona constantemente nuevos dispositivos, empiece con Windows Autopilot.
- Si agrega reglas y valores de control para los usuarios, las aplicaciones y los dispositivos, empiece con Intune.
- Si actualmente usa Configuration Manager para implementar aplicaciones y quiere usar el acceso condicional en función de los requisitos de seguridad, empiece con la administración conjunta.
- Si actualmente usa Configuration Manager y es responsable de mantener los dispositivos de Windows 10 actualizados, empiece con Análisis de escritorio.
- Si está familiarizado con MDM y MAM, o usa plantillas de ADMX para controlar la configuración de Office, Microsoft Edge y Windows, empiece con Intune.

También puede pensar en Endpoint Manager en tres partes: nube, local y nube+local:

- **Nube**: todos los datos están almacenados en Azure. Y no hay más centros de datos. Este enfoque ofrece las ventajas de movilidad de la nube y las ventajas de seguridad de Azure.

- **Local**: si tiene una infraestructura local que incluye Configuration Manager, o que no está lista para usar la nube, puede mantener los sistemas existentes.

- **Nube+local**: muchos entornos son mixtos y usan un enfoque de conexión en la nube. Es decir, usan una combinación de la nube y el entorno local. En el caso de los nuevos dispositivos, use las ventajas de Intune para acceder a los datos y protegerlos. Si usa Configuration Manager, conéctese a la nube para obtener más funcionalidad y análisis. Si desea trasladar algunas cargas de trabajo a la nube, la administración conjunta es una buena opción.

## <a name="what-you-need-to-get-started"></a>Qué necesita para empezar

Microsoft Endpoint Manager es una plataforma de soluciones que unifica varias tecnologías. No se trata de una nueva licencia. Los servicios se conceden según sus términos de licencias individuales. Para obtener más información, vea [Términos de licencia del producto](https://www.microsoft.com/licensing/product-licensing/products).

Si actualmente usa Configuration Manager, también puede obtener Microsoft Intune para la administración conjunta de sus dispositivos Windows. Para otras plataformas, como iOS/iPadOS y Android, necesitará una licencia de Intune independiente.

En la mayoría de los escenarios, Microsoft 365 puede ser la mejor opción, ya que proporciona Endpoint Manager y Office. Para obtener más información, vea [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## <a name="next-steps"></a>Pasos siguientes

[Use la eficacia de la inteligencia de la nube para simplificar y acelerar la TI y pasar a un área de trabajo moderna.](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Tutorial: Intune en Microsoft Endpoint Manager](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Módulo de aprendizaje ¿Qué es Microsoft 365?](/learn/modules/what-is-m365/index)