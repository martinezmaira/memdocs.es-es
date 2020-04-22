---
title: Seguridad y privacidad de Asset Intelligence
titleSuffix: Configuration Manager
description: Obtenga información de seguridad y privacidad de Asset Intelligence en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3cf35b050b110c655ac85e82a7990f9ea2ac3636
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695033"
---
# <a name="security-and-privacy-for-asset-intelligence-in-configuration-manager"></a>Seguridad y privacidad de Asset Intelligence en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este tema contiene información de seguridad y privacidad de Asset Intelligence en Configuration Manager.  

##  <a name="security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Procedimientos recomendados de seguridad de Asset Intelligence  
 Siga los procedimientos recomendados de seguridad que se muestran a continuación cuando utilice Asset Intelligence.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Cuando importe un archivo de licencia (un archivo de licencias por volumen de Microsoft o un archivo de declaración de licencias general), proteja el archivo y el canal de comunicación.|Utilice permisos del sistema de archivos NTFS para asegurarse de que solo los usuarios autorizados puedan acceder a los archivos de licencia y use firma de bloque de mensajes del servidor (SMB), para garantizar la integridad de los datos cuando se transfieren al servidor del sitio durante el proceso de importación.|  
|Utilice el principio de permisos mínimos para importar los archivos de licencia.|Use la administración basada en roles para conceder el permiso Administrar Asset Intelligence al usuario administrativo que importe archivos de licencia. La función integrada del Administrador de activos incluye este permiso.|  

##  <a name="privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Información de privacidad de Asset Intelligence  
 Asset Intelligence amplía las capacidades de inventario de Configuration Manager para ofrecer un mayor nivel de visibilidad de los activos de la empresa. La recopilación de información de Asset Intelligence no se habilita automáticamente. Puede modificar el tipo de información que se recopila mediante la habilitación de clases de informes de inventario de hardware. Para más información, vea [Configuración de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 La información de Asset Intelligence se almacena en la base de datos de Configuration Manager de la misma manera que la información de inventario. Cuando los clientes se conecten a puntos de administración mediante HTTPS, los datos siempre se cifran durante la transferencia al punto de administración. Cuando los clientes se conecten mediante HTTP, puede configurar la transferencia de datos de inventario para que se firmen y cifren. Los datos de inventario no se almacenan en formato cifrado en la base de datos. La información se guarda en la base de datos, hasta que la tarea de mantenimiento del sitio **Eliminar historial de inventario antiguo** la elimina cada 90 días. Puede configurar el intervalo de eliminación.  

 Asset Intelligence no envía información relativa a los usuarios y equipos o el uso de licencias a Microsoft. Puede optar por enviar solicitudes a System Center Online para su clasificación, lo que significa que puede etiquetar uno o más títulos de software sin clasificar y enviarlos a System Center Online para su investigación y categorización. Cuando se carga un título de software, los investigadores de Microsoft identifican, categorizan y ponen ese conocimiento a disposición de todos los clientes que usan el servicio en línea. Debe tener en cuenta las implicaciones de privacidad siguientes cuando envíe información a System Center Online:  

- La carga solo corresponde a la información de título de software genérico (nombre, publicador, etc.) que decida enviar a System Center Online. No se envía información de inventario con ninguna carga.  

- La carga nunca se produce automáticamente y el sistema no está diseñado para que se automatice dicha tarea. Debe seleccionar manualmente y aprobar la carga de cada título de software.  

- Un cuadro de diálogo muestra exactamente los datos que se van a cargar, antes de que comience el proceso de carga.  

- No se envía información de la licencia a Microsoft. La información de la licencia se almacena en un área distinta de la base de datos de Configuration Manager y no se puede enviar a Microsoft.  

- Cualquier título de software que se haya cargado se hace público, en el sentido de que el conocimiento de esa determinada aplicación y su categorización pasan a formar parte del catálogo Asset Intelligence de System Center Online, y posteriormente descargan otros consumidores del catálogo.  

- El origen del título de software no se registra en el catálogo Asset Intelligence y no estará disponible para otros clientes. Sin embargo, debe comprobar que no se cargan títulos de aplicaciones que contengan información privada.  

- Los datos cargados no se pueden recuperar.  

  Antes de configurar la recopilación de datos de Asset Intelligence y decidir si quiere enviar información a System Center Online, tenga en cuenta los requisitos de privacidad de su organización.  
