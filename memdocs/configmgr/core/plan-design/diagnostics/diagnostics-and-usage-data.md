---
title: Diagnósticos y datos de uso
titleSuffix: Configuration Manager
description: Obtenga información sobre los datos de uso y diagnóstico que Configuration Manager recopila sobre sí mismo.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904395"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnósticos y datos de uso para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo, que Microsoft usa para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.  

Cada jerarquía de Configuration Manager habilita los datos de diagnóstico y uso. Consta de las consultas de SQL Server que se ejecutan de forma semanal en cada sitio primario y en el sitio de administración central (CAS). Cuando la jerarquía usa un CAS, los sitios principales y secundarios replican sus datos en ese CAS. En el sitio de nivel superior de la jerarquía, el [punto de conexión de servicio](../../servers/deploy/configure/about-the-service-connection-point.md) envía esta información cuando busca actualizaciones. Si el punto de conexión de servicio está en modo sin conexión, transfiere la información usando la [herramienta de conexión de servicio](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager solamente recopila datos de la base de datos de SQL Server del sitio y no recopila datos directamente de los clientes ni de los servidores de sitios.  

Para obtener más información, vea la [Declaración de privacidad de Microsoft](https://privacy.microsoft.com/privacystatement).  

> [!div class="nextstepaction"]
> [Empleo de los datos de diagnóstico y uso por parte de Microsoft](how-diagnostics-and-usage-data-is-used.md)
