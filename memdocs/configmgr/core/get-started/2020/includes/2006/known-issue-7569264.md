---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590546"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a> La autenticación de Azure AD no funciona
<!--7569264-->
El uso del servicio de token de seguridad de Azure Active Directory (Azure AD) de Configuration Manager no funciona. **CCM_STS.log** en el punto de administración contiene una entrada similar al error siguiente: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` También incluye HRESULT 0x80131040.

Otro síntoma son las incidencias con una instancia de Cloud Management Gateway (CMG). Si ejecuta el analizador de conexiones de CMG, se producirá un error al probar el canal CMG para el punto de administración con el error siguiente: `Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Esta incidencia se debe a una discrepancia de versión con una biblioteca de soporte.

Para solucionar la incidencia, copie **System.IdentityModel.Tokens.JWT.dll** desde la carpeta \bin\X64 del directorio de instalación del servidor de sitio en la carpeta SMS_CCM\CCM_STS\bin del punto de administración.
