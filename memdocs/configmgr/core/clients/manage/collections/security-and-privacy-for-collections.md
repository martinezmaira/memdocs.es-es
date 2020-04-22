---
title: Seguridad y privacidad de recopilaciones
titleSuffix: Configuration Manager
description: Obtenga procedimientos recomendados sobre la seguridad y la privacidad de las recopilaciones en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695533"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Seguridad y privacidad de las recopilaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este tema contiene procedimientos recomendados de seguridad e información de privacidad sobre las recopilaciones de Configuration Manager.  

 No hay ninguna información de privacidad específica para las recopilaciones en Configuration Manager. Las recopilaciones son contenedores para recursos, como usuarios y dispositivos. La pertenencia a la recopilación depende a menudo de la información que recopila Configuration Manager durante el funcionamiento normal. Por ejemplo, con la información de recursos que se ha recopilado de la detección o inventario, se puede configurar una recopilación para que contenga los dispositivos que cumplen los criterios especificados. Las recopilaciones también pueden basarse en la información de estado actual de las operaciones de administración de cliente, como la implementación de software y la comprobación de cumplimiento. Además de estas colecciones basadas en consultas, los usuarios administrativos también pueden agregar recursos a las colecciones.  

 Para más información sobre las recopilaciones, vea [Introducción a las recopilaciones](../../../../core/clients/manage/collections/introduction-to-collections.md). Para más información sobre los procedimientos recomendados de seguridad e información de privacidad de las operaciones de Configuration Manager que se pueden usar para configurar la pertenencia a una recopilación, vea [Procedimientos recomendados de seguridad e información de privacidad de Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Procedimientos recomendados de seguridad para recopilaciones  
 Use el siguiente procedimiento recomendado de seguridad para las recopilaciones.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Al exportar o importar una recopilación mediante el archivo Managed Object Format (MOF) que está guardado en una ubicación de red, proteja la ubicación y el canal de red.|Restringe quién puede tener acceso a la carpeta de red.<br /><br /> Use la firma del Bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre la ubicación de red y el servidor de sitio para impedir que un atacante manipule los datos de la recopilación exportada. Use IPsec para cifrar los datos en la red y así evitar la revelación de información.|  

### <a name="security-issues-for-collections"></a>Problemas de seguridad para recopilaciones  
 Las recopilaciones tienen los siguientes problemas de seguridad:  

-   Si se usan variables de recopilación, los administradores locales pueden leer información potencialmente confidencial.  

     Las variables de recopilación pueden usarse al implementar un sistema operativo.  
