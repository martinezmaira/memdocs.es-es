---
title: Seguridad y privacidad para consultas
titleSuffix: Configuration Manager
description: Analice los procedimientos recomendados de seguridad y privacidad al consultar información de la base de datos del sitio.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695703"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Seguridad y privacidad de las consultas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las consultas de Configuration Manager permiten recuperar información de la base de datos del sitio según los criterios que se especifiquen. Configuration Manager recopila la información de la base de datos del sitio durante el funcionamiento normal. Por ejemplo, con la información que se ha recopilado durante la detección o el inventario, puede configurar una consulta para identificar los dispositivos que cumplen los criterios especificados.  

 Para más información sobre las consultas, vea [Introducción a las consultas](../../../core/servers/manage/introduction-to-queries.md). Para conocer los procedimientos recomendados de seguridad y la información de privacidad de las operaciones de Configuration Manager que recopilan los datos que se pueden recuperar mediante consultas, vea [Seguridad y privacidad en Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Procedimientos recomendados de seguridad para las consultas

 Use este procedimiento recomendado para las consultas.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Al exportar o importar una consulta que está guardada en una ubicación de red, proteja la ubicación y el canal de red.|Restrinja quién puede tener acceso a la carpeta de red.<br /><br /> Use la firma del Bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre la ubicación de red y el servidor de sitio para impedir que un atacante manipule los datos de la consulta antes de que se importen.|  

## <a name="next-steps"></a>Pasos siguientes
  
[Seguridad y privacidad de Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
