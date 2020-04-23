---
title: Compatibilidad internacional
titleSuffix: Configuration Manager
description: Configure Configuration Manager para que cumpla con requisitos internacionales específicos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704603"
---
# <a name="international-support-in-configuration-manager"></a>Compatibilidad internacional en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En las siguientes secciones se proporcionan detalles técnicos para que Configuration Manager sea compatible con determinados requisitos internacionales.  

## <a name="gb18030-requirements"></a>Requisitos de GB18030  
 Configuration Manager cumple los estándares definidos en GB18030 para poder usar Configuration Manager en China. Una implementación de Configuration Manager debe tener la configuración siguiente para cumplir los requisitos de GB18030:  

-   Los equipos de servidor de sitio y de SQL Server que se usan con Configuration Manager deben usar un sistema operativo chino.  

-   Las bases de datos del sitio y las instancias de SQL Server en la jerarquía deben utilizar la misma intercalación, y debe ser una las siguientes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estas intercalaciones de base de datos son una excepción de los requisitos que se mencionan en [Versiones de SQL Server compatibles con Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Debe colocar un archivo de nombre **GB18030.SMS** en la carpeta raíz del volumen de sistema de cada equipo de servidor de sitio en la jerarquía. Este archivo no contiene datos y puede ser un archivo de texto vacío con este nombre para cumplir el requisito.  
