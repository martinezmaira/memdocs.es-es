---
title: Rutas hacia la administración conjunta
titleSuffix: Configuration Manager
description: Conozca los requisitos previos de las dos principales maneras de configurar la administración conjunta.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 27994107c32fac87a465240f07b68d57fddfc140
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983825"
---
# <a name="paths-to-co-management"></a>Rutas hacia la administración conjunta

Hay dos maneras principales de configurar la administración conjunta. Es importante entender los requisitos previos de cada ruta. Cada una de ellas requiere una combinación de Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune y Windows 10. 

1. [Inscripción automática de dispositivos administrados de Configuration Manager en Intune](#bkmk_path1)  
2. [Arranque del cliente de Configuration Manager con aprovisionamiento moderno](#bkmk_path2)  

![Diagramas de las rutas de administración conjunta](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a> Ruta 1: inscripción automática de clientes existentes

Si toma esta ruta, puede inscribir rápidamente sus dispositivos existentes administrados por Configuration Manager en Intune. La administración de estos dispositivos desde Configuration Manager no es distinta de cómo era antes de habilitar la administración conjunta. Ahora recibirá todas las ventajas basadas en la nube. Esta ruta es transparente para los usuarios.

Tendrá que configurar lo siguiente:
- Azure AD híbrido
    - Una de las siguientes [opciones de identidad híbrida de Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Sincronización de hash de contraseña](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) con [ inicio de sesión único de conexión directa (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Autenticación de paso a través](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) con [inicio de sesión único de conexión directa (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [SSO federado (Servicios de federación de Active Directory [AD FS])](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Licencia de Azure AD Premium
    - Configure la unión a Azure AD híbrido (elija una opción):
        - Para dominios administrados
        - Para dominios federados
- Configuración del agente cliente para la unión a Azure AD híbrido
- Configuración de la inscripción automática de dispositivos en Intune
- Habilitación de la administración conjunta en Configuration Manager

Para ver un tutorial sobre esta ruta, consulte [Tutorial: Habilitación de la administración conjunta para clientes existentes de Configuration Manager](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> Ruta 2: arranque con aprovisionamiento moderno

Tendrá que configurar lo siguiente:

1. [Configuración de HTTP mejorado](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Creación de los servicios en la nube en Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Configuración del punto de administración y los clientes para usar Cloud Management Gateway](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Uso de Intune para implementar el cliente de Configuration Manager](how-to-prepare-Win10.md)  

> [!Note]  
> Próximamente habrá disponible un tutorial para esta ruta.

