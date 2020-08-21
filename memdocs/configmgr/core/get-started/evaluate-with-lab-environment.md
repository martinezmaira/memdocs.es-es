---
title: Evaluación en un entorno de laboratorio
titleSuffix: Configuration Manager
description: Cree un entorno de laboratorio para evaluar Configuration Manager para usarlo en la organización.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db59ad55c52f8d937b23704af310dc8879fe8a6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692883"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>Evaluación de Configuration Manager mediante la creación de su propio entorno de laboratorio

*Se aplica a: Configuration Manager (rama actual)*

 Aprenda a crear un entorno de laboratorio para evaluar Configuration Manager para usarlo en su organización.  

 Configuration Manager es una herramienta eficaz y compleja para administrar usuarios, dispositivos y software. Se recomienda realizar una evaluación exhaustiva de Configuration Manager antes de la implementación completa, para que se puedan combinar ejercicios de comprensión conceptual con ejercicios prácticos.  

 Esta guía está destinada principalmente a los administradores que evalúen el uso de Configuration Manager en entornos corporativos:  

-   Administradores que buscan una solución para administrar totalmente equipos, servidores y dispositivos móviles.  

-   Administradores de industrias de alta seguridad que requieren la seguridad de la administración de dispositivos local con la flexibilidad de la administración de dispositivos basada en la nube.  

-   Administradores que quieren administrar el escalado de su arquitectura de servidor local.  

## <a name="what-this-lab-does"></a>Qué pretende este laboratorio  
 El objetivo principal de la creación de este entorno de laboratorio es proporcionarle el conocimiento general para empezar a trabajar con Configuration Manager y para mejorar la comprensión de Configuration Manager. Le guiará a través de un ensamblado rápido de la versión actual de Configuration Manager, con dos servidores:  

-   Uno que hospeda Active Directory, el controlador de dominio y el servidor DNS.  

-   Otro que hospeda Configuration Manager y todos los componentes de SQL Server asociados.  

Las máquinas cliente se instalan en Hyper-V. El laboratorio en sí también puede ejecutarse como un sistema completamente virtualizado en un único servidor.  

## <a name="what-this-lab-does-not-do"></a>Qué no pretende este laboratorio  
 Este laboratorio no le mostrará todos los escenarios de Configuration Manager. No está diseñado para migrarse de inmediato a un entorno activo.  

 Al compilar este laboratorio, tendrá un entorno funcional en el que trabajar. Pero este entorno no estará optimizado para factores como el rendimiento del sistema, la administración del espacio del disco duro y el almacenamiento de SQL Server.  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a> Lecturas recomendadas antes de compilar el laboratorio  
 Hay una gran cantidad de contenido disponible en la [documentación de Configuration Manager](/sccm/). Se recomienda que lea los siguientes temas de esta biblioteca antes de empezar a compilar el laboratorio:  

-   Obtenga información sobre los conceptos básicos de la consola de Configuration Manager, los portales de usuario final y los escenarios de ejemplo en [Introducción a Configuration Manager](../../core/understand/introduction.md).  

-   Obtenga información sobre las funcionalidades de administración principales de Configuration Manager en [Características y funcionalidades de Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Refuerce sus conocimientos con [Aspectos básicos de Configuration Manager](../../core/understand/fundamentals.md).  

-   Conozca la importancia de los roles de seguridad en [Conceptos básicos de la administración basada en roles de Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Obtenga información sobre la administración de contenido en [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Conceptos de la administración de contenido).  

-   Obtenga información sobre cómo admitir correctamente las operaciones diarias de su implementación en [Más información sobre cómo los clientes buscan servicios y recursos de sitio para Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).