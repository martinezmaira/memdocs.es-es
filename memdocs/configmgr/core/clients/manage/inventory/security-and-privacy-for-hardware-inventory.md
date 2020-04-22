---
title: Seguridad y privacidad del inventario de hardware
titleSuffix: Configuration Manager
description: Obtenga información sobre seguridad y privacidad del inventario de hardware en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690113"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Seguridad y privacidad del inventario de hardware en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este tema contiene información sobre la seguridad y privacidad del inventario de hardware en Configuration Manager.  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Procedimientos recomendados de seguridad para el inventario de hardware  
 Use los siguientes procedimientos recomendados de seguridad cuando recopile datos de inventario de hardware de los clientes:  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Firmar y cifrar los datos de inventario|Cuando los clientes se comunican con puntos de administración mediante HTTPS, todos los datos que se envían se cifran con SSL. Sin embargo, cuando los equipos cliente usan HTTP para comunicarse con los puntos de administración en la intranet, los datos de inventario de cliente y los archivos recopilados se pueden enviar sin firma y sin cifrar. Asegúrese de que el sitio está configurado para requerir firma y use cifrado. Además, si los clientes pueden admitir el algoritmo SHA-256, seleccione la opción para requerir SHA-256.|  
|No se recopilan los archivos IDMIF y NOIDMIF en entornos de alta seguridad|Puede utilizar la recopilación de archivos IDMIF y NOIDMIF para ampliar la recopilación de inventario de hardware. Cuando es necesario, Configuration Manager crea tablas o modifica tablas existentes en la base de datos de Configuration Manager para adaptarse a las propiedades de los archivos IDMIF y NOIDMIF. En cambio, Configuration Manager no valida los archivos IDMIF y NOIDMIF, por lo que estos archivos podrían usarse para modificar las tablas que no desea modificar. Datos válidos podrían sobrescribirse por datos no válidos. Además, se podrían agregar grandes cantidades de datos cuyo procesamiento podría provocar retrasos en todas las funciones de Configuration Manager. Para mitigar estos riesgos, establezca la opción de configuración de cliente del inventario de hardware **Recopilar archivos MIF** como **Ninguno**.|  

### <a name="security-issues-for-hardware-inventory"></a>Problemas de seguridad del inventario de hardware  
 La recopilación de inventario revela posibles vulnerabilidades. Los atacantes pueden realizar lo siguiente:  

- Enviar datos no válidos, que el punto de administración aceptará incluso cuando la configuración de cliente de inventario de software esté deshabilitada y la recopilación de archivos no esté habilitada.  

- Enviar cantidades de datos excesivamente grandes en un único archivo y en una gran cantidad de archivos, lo que podría producir una denegación de servicio.  

- Obtener acceso a la información del inventario cuando se transfiere a Configuration Manager.  

  Dado que un usuario con privilegios de administrador local puede enviar información como datos de inventario, no dé por hecho que los datos de inventario recopilados por Configuration Manager son fiables.  

  El inventario de hardware está habilitado de forma predeterminada como configuración de cliente.  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Información de privacidad del inventario de hardware  
 El inventario de hardware permite recuperar cualquier información almacenada en el registro y en WMI en los clientes de Configuration Manager. El inventario de software permite detectar todos los archivos de un tipo especificado o recopilar los archivos especificados de los clientes. Asset Intelligence mejora las capacidades de inventario mediante la ampliación del inventario de hardware y software y la adición de la nueva función de administración de licencias.  

 El inventario de hardware está habilitado de forma predeterminada como una configuración de cliente y la información de WMI recopilada se determina mediante las opciones que selecciona. El inventario de software está habilitado de forma predeterminada, pero los archivos no se recopilan de forma predeterminada. La recopilación de datos de Asset Intelligence se habilita automáticamente, aunque puede seleccionar las clases de informes de inventario de hardware que se habilitan.  

 La información de inventario no se envía a Microsoft. La información de inventario se almacena en la base de datos de Configuration Manager. Cuando los clientes usan HTTPS para conectarse a puntos de administración, los datos de inventario que se envían al sitio se cifran durante la transferencia. Si los clientes usan HTTP para conectarse a los puntos de administración, tiene la opción de habilitar el cifrado de inventario. Los datos de inventario no se almacenan en formato cifrado en la base de datos. La información se conserva en la base de datos hasta que las tareas de mantenimiento del sitio **Eliminar historial de inventario antiguo** o **Eliminar archivos recopilados antiguos** la eliminan cada 90 días. Puede configurar el intervalo de eliminación.  

 Antes de configurar el inventario de hardware, el inventario de software, la recopilación de archivos o la recopilación de datos de Asset Intelligence, tenga en cuenta los requisitos de privacidad.  
