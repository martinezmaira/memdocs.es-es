---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128346"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

A partir de la versión 1906, puede usar CMPivot como una aplicación independiente. CMPivot independiente solo está disponible en inglés. Ejecútelo fuera de la consola de Configuration Manager para ver el estado en tiempo real de los dispositivos en su entorno. Este cambio le permite usar CMPivot en un dispositivo sin instalar primero la consola.

> [!Tip]  
> Esta característica se incluyó por primera vez en la versión 1906 como [característica de versión preliminar](../pre-release-features.md). A partir de la versión 2002, ya no se encuentra en versión preliminar.  

Puede compartir la eficacia de CMPivot con otras personas, como administradores de seguridad o del departamento de soporte técnico, que no tienen la consola instalada en su equipo. Estas otras personas pueden usar CMPivot para consultar Configuration Manager junto con las otras herramientas que usan tradicionalmente. Al compartir estos datos de administración enriquecidos, pueden trabajar juntos para resolver proactivamente los problemas empresariales de los roles.

#### <a name="install-cmpivot-standalone"></a>Instalación de CMPivot independiente

1. Configurar los permisos necesarios para ejecutar CMPivot. Para más información, consulte los [requisitos previos](../cmpivot.md#prerequisites). También puede usar el [rol Administrador de seguridad](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) si los permisos son adecuados para el usuario.
2. Encuentre el instalador de la aplicación CMPivot en la ruta de acceso siguiente: `<site install path>\tools\CMPivot\CMPivot.msi`. Puede ejecutarlo desde esa ruta de acceso o copiarlo en otra ubicación.
3. Cuando ejecute la aplicación CMPivot independiente, se le pedirá que se conecte a un sitio. Especifique el nombre de dominio completo o el nombre de equipo del servidor del sitio primario o del servidor del sitio de administración central.
   - Cada vez que abra CMPivot independiente se le pedirá conectarse a un servidor de sitio.
4. Vaya a la colección donde quiere ejecutar CMPivot y, luego, ejecute la consulta.

   ![Vaya a la colección donde quiere ejecutar la consulta](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - Las acciones del menú contextual, como **Ejecutar scripts**, **Explorador de recursos** y las búsquedas web, no están disponibles en la versión independiente de CMPivot. El uso principal de la versión independiente de CMPivot es realizar consultas de manera independiente de la infraestructura de Configuration Manager. Para ayudar a los administradores de seguridad, la versión independiente de CMPivot incluye la posibilidad de conectarse al Centro de seguridad de Microsoft Defender. <!--5605358-->
> - A partir de la versión 1910, puede realizar una [evaluación de una consulta de dispositivo local con la versión independiente de CMPivot](../cmpivot-changes.md#bkmk_local-eval). <!--3197353--> 