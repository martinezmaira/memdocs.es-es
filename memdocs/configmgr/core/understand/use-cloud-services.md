---
title: Usar servicios en la nube
titleSuffix: Configuration Manager
description: Aprovisione recursos en la nube para Configuration Manager a fin de complementar la infraestructura local.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84cb878de3eea56dc68180a83fd4b6a32b2d1073
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906422"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Usar servicios en la nube con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite varias opciones basadas en la nube. Pueden complementar la infraestructura local y ayudar a resolver problemas empresariales como:  

-   Cómo administrar BYOD (mediante Intune para la administración de dispositivos móviles).  

-   Cómo proporcionar recursos de contenido a clientes aislados o recursos de la intranet, fuera del firewall corporativo (mediante puntos de distribución basados en la nube).  

-   Cómo escalar horizontalmente la infraestructura cuando el hardware físico no está disponible o no está lógicamente colocado para satisfacer sus necesidades (mediante máquinas virtuales de Microsoft Azure).  

Aunque el aprovisionamiento de recursos en la nube no es algo que deba hacer antes de implementar Configuration Manager, puede ser conveniente conocer estas opciones antes de avanzar demasiado en el plan de diseño de la jerarquía. El uso de recursos de nube puede ahorrarle tiempo y dinero, además de resolver problemas empresariales que la infraestructura local no puede resolver.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Recursos basados en la nube que puede usar con Configuration Manager  
 Dado que cada opción tiene requisitos diferentes, investigue más a fondo para comprender los requisitos previos, las limitaciones y los posibles costos adicionales según el uso.  

-   Para obtener información sobre los puntos de distribución basados en la nube, consulte [Install cloud-based distribution points](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) (Instalar puntos de distribución basados en la nube).

-   Para obtener más información sobre Azure, consulte [¿Qué es Azure?](https://azure.microsoft.com/overview/what-is-azure/)

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Máquinas virtuales de Azure (para infraestructuras basadas en la nube)  
 Configuration Manager admite el uso de equipos que se ejecutan en máquinas virtuales de Azure, igual que cuando se ejecuta localmente dentro de la red corporativa física. Puede usar máquinas virtuales de Azure en los siguientes escenarios:  

-   **Escenario 1:** puede ejecutar Configuration Manager en una máquina virtual y usarlo para administrar clientes instalados en otras máquinas virtuales.  

-   **Escenario 2:** puede ejecutar Configuration Manager en una máquina virtual y usarlo para administrar clientes que no se ejecutan en Azure.  

-   **Escenario 3:** puede ejecutar diferentes roles de sistema de sitio de Configuration Manager en máquinas virtuales mientras ejecuta otros roles en su red corporativa física (con la conectividad de red adecuada para las comunicaciones).  

Los mismos requisitos para redes, sistemas operativos y requisitos de hardware que se aplican a la instalación de Configuration Manager en su red corporativa física también se aplican a la instalación de Configuration Manager en Azure.  

Se necesita una suscripción a Azure para poder usar las máquinas virtuales de Azure. Se producen cargos según el número de máquinas virtuales que use, su configuración y el uso de recursos basados en la nube.  

Además, los sitios y clientes de Configuration Manager que se ejecutan en máquinas virtuales de Azure están sujetos a los mismos requisitos de licencia que las instalaciones locales.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Servicios de Azure (para puntos de distribución basados en la nube)  
 Puede usar un servicio de Azure para hospedar un punto de distribución de Configuration Manager, que se denomina punto de distribución basado en la nube. Puede [usar puntos de distribución basados en la nube con Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) junto con puntos de distribución locales y puntos de distribución implementados en máquinas virtuales de Azure.  

 Esto es distinto a usar una máquina virtual de Azure en la que implementa un rol de sistema de sitio. Puntos de distribución basados en la nube:  

-   Se ejecutan como un servicio en Azure, no en una máquina virtual.  

-   Ajustan su escala automáticamente para satisfacer las solicitudes de contenido de los clientes.  

-   Admiten clientes en Internet y la intranet.  

Se necesita una suscripción a Azure para poder usar Azure para hospedar puntos de distribución. Se producen gastos en función de la cantidad de datos que se transfieren hacia y desde el servicio.  

### <a name="additional-configuration-manager-capabilities"></a>Funcionalidades adicionales de Configuration Manager  
 Algunas funcionalidades de Configuration Manager pueden conectarse a servicios en la nube, como:  

-   Windows Server Update Services (WSUS).  

-   El servicio en la nube de Configuration Manager para descargar actualizaciones para Configuration Manager.  

Para usar estas capacidades adicionales no es necesario tener una suscripción a Azure. No es necesario configurar conexiones, certificados o servicios en la nube específicos. En su lugar, Configuration Manager las administra automáticamente. Lo único que necesita es asegurarse de que los sistemas de sitio y los dispositivos correspondientes tengan acceso a las URL de Internet.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> Seguridad de los servicios en la nube  
 Configuration Manager usa certificados para aprovisionar y acceder a su contenido en Azure y para administrar los servicios que use. Configuration Manager cifra los datos que se almacenan en Azure, pero no incluye controles adicionales de seguridad o de datos más allá de los que proporciona Azure.  

 Para obtener más información, consulte los detalles de los distintos escenarios de recursos basados en la nube. Consulte también [Introducción a la seguridad de Azure](https://docs.microsoft.com/azure/security/fundamentals/overview).
