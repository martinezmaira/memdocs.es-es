---
title: ¿Qué es Configuration Manager?
titleSuffix: Configuration Manager
description: Conozca los aspectos básicos de Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99e02c190e02a5e017fe2c3f41682ad1624b6051
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699354"
---
# <a name="what-is-configuration-manager"></a>¿Qué es Configuration Manager?

*Se aplica a: Configuration Manager (rama actual)*

A partir de la versión 1910, Configuration Manager forma parte de Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager es una solución integrada para administrar todos los dispositivos. Microsoft aúna Configuration Manager e Intune, sin migraciones complejas y con licencia simplificada. Siga aprovechando las inversiones existentes en Configuration Manager y aproveche las ventajas de la eficacia de la nube de Microsoft a su propio ritmo.

Las siguientes soluciones de administración de Microsoft forman parte ahora de la marca **Microsoft Endpoint Manager**:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Análisis de escritorio](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Otras características de la [consola de administración de dispositivos](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760).

Para más información, vea [Preguntas más frecuentes de Microsoft Endpoint Configuration Manager](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Introducción

Use Configuration Manager a modo de ayuda en las siguientes actividades de administración de sistemas:

- Aumentar la eficacia y la productividad de TI al reducir las tareas manuales y permitirle centrarse en proyectos de alto valor.  
- Maximizar las inversiones en hardware y software.  
- Fortalecer la productividad del usuario al proporcionar el software adecuado en el momento oportuno.  

Configuration Manager ayuda a prestar servicios de TI más eficaces al permitir lo siguiente:

- Una implementación segura y escalable de las aplicaciones, actualizaciones de software y sistemas operativos.
- Acciones en tiempo real en los dispositivos administrados.
- Administración y análisis con tecnología de nube e dispositivos locales y basados en Internet.
- Administración de la configuración de cumplimiento.  
- Administración exhaustiva servidores, escritorios y portátiles.

Configuration Manager amplía muchas de las soluciones y tecnologías de Microsoft y trabaja junto a ellas. Por ejemplo, Configuration Manager se integra en:  

- Microsoft Intune, para administrar conjuntamente una amplia variedad de plataformas de dispositivos móviles
- Microsoft Azure, para hospedar servicios en la nube y, así, ampliar los servicios de administración
- Windows Server Update Services (WSUS) para administrar las actualizaciones de software
- Servicios de servidor de certificados
- Exchange Server y Exchange Online
- Directiva de grupo
- DNS
- El kit de implementación automatizada de Windows (ADK de Windows) y la Herramienta de migración de estado de usuario (USMT)
- Servicios de implementación de Windows (WDS)
- Escritorio remoto y Asistencia remota

Configuration Manager también usa:  

- Active Directory Domain Services y Azure Active Directory para la seguridad, la ubicación de servicio, la configuración y la detección de los usuarios y dispositivos que quiera administrar.  
- Microsoft SQL Server como base de datos distribuida de administración de cambios, y se integra con SQL Server Reporting Services (SSRS) para producir informes con el fin de supervisar y realizar un seguimiento de las actividades de administración.  
- Los roles del sistema de sitio que extienden la función de administración y usan los servicios web de Internet Information Services (IIS).
- Optimización de distribución, Windows Low Extra Delay Background Transport, Servicio de transferencia inteligente en segundo plano (BITS), BranchCache y otras tecnologías de almacenamiento en caché del mismo nivel para ayudar a administrar el contenido de las redes y entre dispositivos.

Para utilizar Configuration Manager satisfactoriamente en un entorno de producción, antes hay que planear y probar las características de administración de manera exhaustiva. Configuration Manager es una aplicación de administración muy eficaz que puede afectar en potencia a todos los equipos de su organización. Si implementa y administra Configuration Manager con una planeación rigurosa y tomando en consideración sus requisitos empresariales, Configuration Manager puede reducir su sobrecarga administrativa y el coste total de propiedad.  

## <a name="user-interfaces"></a>Interfaces de usuario

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> La consola de Configuration Manager

Después de instalar Configuration Manager, use la consola de Configuration Manager para configurar sitios y clientes, y para ejecutar y supervisar tareas de administración. Esta consola es el principal punto de administración y permite administrar varios sitios.  

Puede instalar la consola de Configuration Manager en equipos adicionales, restringir el acceso y limitar lo que los usuarios administrativos pueden ver en la consola con la administración basada en roles de Configuration Manager.  

Para más información, vea [Uso de la consola de Configuration Manager](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> Centro de software

El **Centro de software** es una aplicación que se instala al instalar el cliente de Configuration Manager en un dispositivo Windows. Los usuarios usan el Centro de software para solicitar e instalar el software que haya implementado. El Centro de software permite a los usuarios realizar las siguientes acciones:  

- Buscar e instalar aplicaciones, actualizaciones de software y nuevas versiones del sistema operativo
- Ver el historial de solicitudes de software
- Ver el cumplimiento de dispositivos respecto a las directivas de la organización

En el Centro de software también se pueden mostrar pestañas personalizadas para satisfacer requisitos empresariales extra.

Para más información, consulte el [Manual del usuario del Centro de software](software-center.md).

## <a name="next-steps"></a>Pasos siguientes

Antes de instalar Configuration Manager, familiarícese con los conceptos y términos básicos:

- Si está familiarizado con System Center 2012 Configuration Manager, vea [Cambios en System Center Configuration Manager respecto a System Center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Para obtener una descripción técnica general de Configuration Manager, vea [Aspectos básicos de Configuration Manager](fundamentals.md).

Cuando esté familiarizado con los conceptos básicos, use la biblioteca de documentación para implementar y usar correctamente Configuration Manager. Comience por los siguientes artículos:

- [Características y funcionalidades de Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Elegir una solución de administración de dispositivos](../plan-design/choose-a-device-management-solution.md)  
- [Evaluación de Configuration Manager mediante la creación de su propio entorno de laboratorio](../get-started/set-up-your-lab.md)
- [Búsqueda de ayuda para usar Configuration Manager](find-help.md)