---
title: Solución de problemas para implementaciones de aplicaciones
titleSuffix: Configuration Manager
description: Sugerencias para solucionar problemas de implementación de aplicaciones en Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689973"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Sugerencias de solución de problemas para implementaciones de aplicaciones

*Se aplica a: Configuration Manager (rama actual)*

Los problemas más habituales relacionados con las implementaciones de aplicaciones pertenecen a una de las siguientes categorías:

- Errores de descarga de la aplicación

- Cumplimiento de implementación de la aplicación bloqueado en el 0 %

Si experimenta alguno de estos problemas, en este artículo encontrará los pasos que puede seguir para solucionarlos. Para obtener solución de problemas más completa, vea [Referencia técnica de solución de problemas de implementación de aplicaciones](../understand/app-deployment-technical-reference.md).


## <a name="download-failures"></a>Errores de descarga

Los errores de descarga de la aplicación incluyen los siguientes problemas:

- El cliente se bloquea al descargar una aplicación.

- El cliente no puede descargar el contenido de la aplicación.

- El cliente se bloquea en el 0 % al descargar una aplicación.

Lo primero que debe comprobar cuando experimente errores en la descarga de la aplicación es si faltan límites y grupos de límites o si están mal configurados. Por ejemplo, si el cliente está en la intranet y no está configurado para la administración de clientes solo de Internet, su ubicación de red debe estar en un límite configurado. También debe haber un grupo de límites asignado a este límite para que el cliente pueda descargar contenido. Para obtener más información, vea [Definir los límites del sitio y los grupos de límites](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

Si no se puede configurar un límite para un cliente o si un grupo de límites concreto no puede ser miembro de otro grupo de límites:

1. En la consola de Configuration Manager, abra las propiedades del **Tipo de implementación**.  

1. Cambie a la pestaña **Contenido**.

1. En la sección para usar un punto de distribución desde un grupo de límites vecino o el grupo de límites de sitio predeterminado, cambie **Opciones de implementación** a **Descargar contenido desde el punto de distribución y ejecutar localmente**. (De forma predeterminada, esta configuración es **No descargar contenido**).

Si el cliente no puede descargar el contenido de la aplicación, asegúrese de que se distribuya a un punto de distribución. Para comprobar esta configuración, use las características en la consola para supervisar la distribución de contenido a los puntos de distribución. Para obtener más información, vea [Supervisión del contenido que se ha distribuido](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  


## <a name="compliance-stuck-at-0"></a>Cumplimiento bloqueado en el 0 %

Si el cumplimiento de implementación de la aplicación es 0 %, compruebe el estado de implementación de la aplicación en el área de trabajo **Supervisión**, en el nodo **Implementaciones**.

- **En curso**: el cliente podría bloquearse al [descargar contenido](#download-failures).

- **Error**: para más información sobre cómo solucionar este problema, consulte la siguiente entrada de blog: [Sugerencias y trucos: Realización de acciones sobre los recursos que notifican una implementación con errores](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Desconocido**: este estado suele significar que el cliente no ha recibido la directiva. Actualice manualmente la directiva de cliente para ver si el cliente la recibe. Para obtener más información, vea [Iniciar la recuperación de directivas para un cliente de Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).
  
Si estas acciones no resuelven el problema, compruebe el estado del cliente. Podría haber un problema subyacente en el cliente. Para obtener más información, vea [Cómo supervisar clientes](../../core/clients/manage/monitor-clients.md).


## <a name="next-steps"></a>Pasos siguientes

- [Supervisar aplicaciones](monitor-applications-from-the-console.md)
- [Implementar aplicaciones](deploy-applications.md)
- [Tareas de administración para aplicaciones](management-tasks-applications.md)
- [Solución de problemas de referencia técnica de implementación de aplicaciones](../understand/app-deployment-technical-reference.md)
