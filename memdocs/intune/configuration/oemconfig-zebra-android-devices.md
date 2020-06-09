---
title: 'Implementación de varios perfiles de OEMConfig en dispositivos Zebra mediante Microsoft Intune: Azure | Microsoft Docs'
description: Use Microsoft Intune para crear e implementar varios perfiles de configuración de dispositivos OEMConfig en dispositivos Zebra que ejecuten Android Enterprise. Use acciones y pasos de Zebra para ordenar los perfiles.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311183"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Implementación de varios perfiles de OEMConfig en dispositivos Zebra en Microsoft Intune

En Microsoft Intune, use OEMConfig a fin de personalizar la configuración específica de OEM para dispositivos Android Enterprise. Esta configuración es específica del fabricante del dispositivo y se implementa mediante perfiles de configuración en Intune.

En los dispositivos Zebra puede implementar o asignar varios perfiles al mismo dispositivo. Los perfiles de OEMConfig existentes pueden usar esta característica la próxima vez que se sincronicen los dispositivos con Intune.

Esta característica se aplica a:

- Dispositivos Zebra que ejecutan Android Enterprise

Para obtener más información sobre OEMConfig, incluido lo que hace y cómo usarlo, vea [Perfil de configuración de OEMConfig](android-oem-configuration-overview.md).

En este artículo se describe la implementación de varios perfiles de OEMConfig en dispositivos Zebra, así como el orden y el uso de las características de generación de informes en Microsoft Intune.

## <a name="prerequisites"></a>Requisitos previos

Cree un [perfil de configuración de OEMConfig](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Uso de varios perfiles

En los dispositivos Zebra, se pueden tener muchos perfiles simultáneamente en cada dispositivo. Esta característica permite dividir la configuración de OEMConfig de Zebra en perfiles más pequeños. Por ejemplo, cree un perfil de línea de base que afecte a todos los dispositivos. Luego, cree más perfiles que configuren las opciones específicas de un dispositivo.

El esquema OEMConfig de Zebra también usa **acciones**. Las acciones son operaciones que se ejecutan en el dispositivo. No configuran ningún valor. Use estas acciones para desencadenar la descarga de un archivo, borrar contenido del Portapapeles y mucho más. Para obtener una lista completa de acciones admitidas, vea la [documentación de Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/), disponible en su sitio web.

Por ejemplo, puede crear un perfil de OEMConfig de Zebra que aplique algunas opciones de configuración al dispositivo. Otro perfil de OEMConfig de Zebra incluye una acción que borra el contenido del Portapapeles. El primer perfil se asigna a un grupo de dispositivos Zebra. Más adelante, deberá borrar el contenido del Portapapeles de esos dispositivos. El segundo perfil se asigna al mismo grupo de dispositivos, sin cambiar el primero. El contenido del Portapapeles del dispositivo se borra sin volver a enviar o afectar a las opciones de configuración creadas en el primer perfil.

En otro ejemplo, se ha asignado un perfil de OEMConfig que ha configurado algunas opciones de configuración del dispositivo Zebra. Recientemente, los usuarios notifican incidencias con una aplicación específica y quiere borrar la caché de la aplicación. Cree un nuevo perfil de OEMConfig que incluya solo la acción "Borrar caché". Asigne el perfil a los dispositivos que lo necesiten.

## <a name="ordering"></a>Ordenación

Con varios perfiles en cada dispositivo, no se garantiza el orden en el que se implementan los perfiles. Este comportamiento es una limitación de Google Play. Para ejecutar operaciones en secuencia, se puede usar la [característica de paso de transacción de Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/), disponible en su sitio web. 

En resumen, si el orden es importante, use la [característica de paso de transacción de Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/), disponible en su sitio web. Si no importa, use varios perfiles de Intune. 

Echemos un vistazo a algunos ejemplos:

- Quiere activar Bluetooth para todos los dispositivos Zebra recientemente inscritos antes de configurar cualquier otro valor en estos dispositivos. Para ejecutar las operaciones en secuencia, use la característica **Pasos** en el esquema de Zebra.

  Cree un perfil de Intune que tenga dos pasos de transacción. El primer paso incluye la configuración del Bluetooth y el segundo configura la otra opción. Cuando la aplicación OEMCong de Zebra recibe el perfil, ejecuta los pasos en orden.

  Para obtener más información, vea [Pasos de la transacción de Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/), disponible en su sitio web.

- Quiere que todos los dispositivos Zebra muestren la hora en el formato de 24 horas. En algunos de estos dispositivos, quiere desactivar la cámara. La configuración de hora y cámara no dependen la una de la otra.

  Cree dos perfiles de Intune:

  - **Perfil 1**: muestra la hora en el formato de 24 horas. El lunes, este perfil se asigna al grupo **All Zebra AE devices** (Todos los dispositivos de Zebra AE).
  - **Perfil 2**: desactiva la cámara. El martes, este perfil se asigna al grupo **Zebra AE factory devices** (Dispositivos de fábrica de Zebra AE).

  El miércoles, se inscriben 10 dispositivos Zebra nuevos con Intune. Se han asignado el perfil 1 y el perfil 2. Una vez que los dispositivos nuevos se sincronizan con Intune, reciben los perfiles. Los dispositivos pueden obtener el perfil 2 antes de obtener el perfil 1.

## <a name="enhanced-reporting"></a>Generación de informes mejorada

Se va a implementar un perfil y lo ejecutará la aplicación OEMConfig de Zebra en el dispositivo. La aplicación OEMConfig de Zebra notifica el estado del perfil a Intune. En el Centro de administración de Endpoint Manager, se puede ver el estado de los perfiles de OEMConfig implementados, así como los errores o advertencias.

1. Abra el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione el perfil de OEMConfig de Zebra > **Supervisar** > **Estado del dispositivo**. Esta opción muestra los dispositivos que tienen el perfil de OEMConfig asignado.
3. Seleccione un dispositivo > **Configuración del dispositivo** > Seleccionar el perfil de OEMConfig de Zebra. Esta opción muestra la configuración del perfil que se ha realizado correctamente o que ha producido un error.

    Seleccione una fila con errores. Se muestran los detalles que tienen más información sobre por qué se ha producido un error.

## <a name="next-steps"></a>Pasos siguientes

- Obtenga más información sobre los [perfiles de configuración de OEMConfig](android-oem-configuration-overview.md).
- En el administrador de dispositivos Android, configure [Mobility Extensions (MX)](android-zebra-mx-overview.md).
- [Supervisión del estado del perfil](device-profile-monitor.md).
