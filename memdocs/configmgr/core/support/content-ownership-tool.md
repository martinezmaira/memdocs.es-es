---
title: Content Ownership Tool
titleSuffix: Configuration Manager
description: Use Content Ownership Tool para cambiar la propiedad de los paquetes huérfanos en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707853"
---
# <a name="content-ownership-tool"></a>Content Ownership Tool

*Se aplica a: Configuration Manager (rama actual)*

Content Ownership Tool es una de las [herramientas de Configuration Manager](tools.md). Cambia la propiedad de los paquetes huérfanos en Configuration Manager. Los paquetes huérfanos no tienen un servidor de sitio propietario. Los paquetes pueden quedar huérfanos quitando el servidor de sitio mientras todavía los poseía este servidor de sitio.

Ejecute Content Ownership Tool en cualquier servidor de sitio en la jerarquía de Configuration Manager. Inicie sesión como un usuario administrativo con suficientes permisos de paquete.  

> [!Tip]  
> Use **ContentLibraryCleanup.exe** en `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para *quitar* contenido huérfano desde un punto de distribución. Para obtener más información, vea [Content Library Cleanup Tool](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Funciones

- Mostrar todos los paquetes huérfanos  

- Mostrar todos los paquetes, incluso si no están huérfanos  

- Ver el estado de la conexión a un sitio  

- Filtrar paquetes por nombre, código de sitio o tipo de paquete  

- Ordenar por cualquier columna mostrada  

- Cambiar la asignación de uno o varios paquetes con una sola acción  

- Ver el progreso de la actividad de transferencia de propiedad  



## <a name="usage"></a>Uso

Ejecute **ContentOwnershipTool.exe** para iniciar la herramienta. No se requieren permisos de administrador local en el equipo para ejecutar la herramienta.

No hay parámetros de línea de comandos.

> [!Important]   
> Esta herramienta cambia la propiedad de un paquete huérfano. El propio paquete no se mueve desde el punto de distribución en el que se almacena. Este cambio de propiedad no hace que el paquete actualice los puntos de distribución. Tampoco hace que los clientes vuelvan a evaluar la directiva para la implementación del paquete. Una vez que cambia la propiedad, asegúrese de que el nuevo servidor de sitio puede tener acceso a los archivos de origen. Debe tener al menos permisos de **lectura** a los archivos de origen de cada paquete. 



## <a name="see-also"></a>Vea también

- [Conceptos básicos de la administración de contenido](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [La biblioteca de contenido](../plan-design/hierarchy/the-content-library.md)
