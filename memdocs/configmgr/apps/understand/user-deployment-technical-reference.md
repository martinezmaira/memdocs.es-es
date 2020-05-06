---
title: Referencia técnica de implementación de aplicaciones para usuarios
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de implementaciones de aplicaciones en usuarios para Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690273"
---
# <a name="application-deployment-policy-for-users"></a>Directiva de implementación de aplicaciones para usuarios

*Se aplica a: Configuration Manager (rama actual)*

Cuando se implementa una aplicación en una colección de usuarios, la directiva para la implementación solo se crea para las implementaciones requeridas. En el caso de las implementaciones disponibles, la directiva se crea cuando el usuario intenta instalar la aplicación desde el Centro de software. En este artículo se explica el proceso de implementación para implementaciones requeridas y disponibles.

> [!TIP]
> Toda la información necesaria para revisar los registros de cliente se puede obtener mediante la ejecución de la consulta SQL a la que se hace referencia en la sección [Antes de empezar](app-deployment-technical-reference.md#before-you-begin).

## <a name="required-deployments"></a>Implementaciones requeridas

La directiva para la implementación de una aplicación requerida en una colección de usuarios se destina a todos los usuarios de la colección al crear la implementación. El procesamiento del lado cliente para estas implementaciones es similar a una implementación requerida en una colección de dispositivos. La activación de la implementación se produce a la hora disponible definida y el cumplimiento se produce en la fecha límite definida. Para obtener más información, vea [Implementación de aplicaciones en colecciones de dispositivos](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Implementaciones disponibles

Las aplicaciones que se implementan en una colección de usuarios como disponibles se comportan de otra forma. Este cambio de comportamiento permite al administrador poner las aplicaciones a disposición de los usuarios sin causar contención de recursos para la directiva. Cuando un usuario inicia el Centro de software, se consulta una lista de las aplicaciones que están disponibles para el usuario desde el punto de administración en tiempo real. Esta solicitud se realiza en el directorio virtual `CMUserService_WindowsAuth` del punto de administración y se puede ver en **SCClient_[NombreDeUsuario].log** desde el cliente.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Cuando el punto de administración recibe esta solicitud, consulta la lista de aplicaciones disponibles para el usuario mediante la ejecución del procedimiento almacenado `usp_GetApplicationPropertyValuesFiltered`. Se puede realizar el seguimiento de esta actividad en **UserService.log** en el punto de administración.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

El Centro de software recibe la lista y muestra las aplicaciones que el usuario puede instalar. Cuando el usuario hace clic en la aplicación, se consulta información adicional sobre la aplicación desde el punto de administración, lo que implica la ejecución de procedimientos almacenados como usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp, etc.

La implementación se activa cuando el usuario selecciona la aplicación y hace clic en el botón **Instalar**, y se crea un trabajo del agente de DCM para evaluar la aplicación. Si la aplicación es aplicable, se crea otro trabajo del agente de DCM para descargarla y aplicarla. Se puede realizar el seguimiento de esta actividad en **DCMAgent.log** en el cliente.

## <a name="next-steps"></a>Pasos siguientes

- [Descripción de los componentes de cliente de implementación de aplicaciones](client-components-technical-reference.md)
