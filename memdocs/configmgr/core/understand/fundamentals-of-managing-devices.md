---
title: Fundamentos de la administración de dispositivos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar Configuration Manager para administrar dispositivos.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707073"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Fundamentos de la administración de dispositivos con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager puede administrar dos amplias categorías de dispositivos:

- Los *clientes* son dispositivos tales como estaciones de trabajo, equipos portátiles, servidores y dispositivos móviles en los que instala el software cliente de Configuration Manager. Algunas funciones de administración, como el inventario de hardware, requieren este software cliente.  

- Los *dispositivos administrados* pueden incluir *clientes*, pero normalmente son un dispositivo móvil en el que no está instalado el software cliente de Configuration Manager. En este tipo de dispositivo, la administración se lleva a cabo mediante la administración de dispositivos móviles local integrada en Configuration Manager.

También puede agrupar e identificar los dispositivos según el usuario, no solo el tipo de cliente.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Administración de dispositivos con el cliente de Configuration Manager

Hay dos maneras de usar el software cliente de Configuration Manager para administrar un dispositivo. La primera consiste en detectar el dispositivo en la red y, después, implementar el software cliente en el dispositivo. La segunda consiste en instalar manualmente el software cliente en un equipo nuevo y, luego, hacer que el equipo se una a su sitio cuando se conecte a la red. Para detectar dispositivos en los que no está instalado el software cliente, ejecute uno o varios de los métodos de detección integrados. Después de que se detecte un dispositivo, use uno de los distintos métodos para instalar el software cliente. Para información sobre la detección, consulte [Ejecutar la detección para Configuration Manager](../servers/deploy/configure/run-discovery.md).  

Después de detectar los dispositivos que pueden ejecutar el software cliente de Configuration Manager, puede usar varios métodos para instalarlo. Cuando se haya instalado el software y se haya asignado el cliente a un sitio principal, puede comenzar a administrar el dispositivo. Entre los métodos de instalación comunes se incluyen los siguientes:

- Instalación de inserción de cliente

- Instalación basada en actualización de software

- Directiva de grupo.

- Instalación manual en un equipo.

- Inclusión del cliente como parte de una imagen de sistema operativo que se implementa.  

Después de instalar el cliente, puede simplificar las tareas de administración de dispositivos mediante el uso de colecciones. Las colecciones son grupos de dispositivos o usuarios que crea para poder administrarlos como un grupo. Por ejemplo, es posible que quiera instalar una aplicación de dispositivo móvil en todos los dispositivos móviles inscritos por Configuration Manager. Si es así, puede usar la recopilación Todos los dispositivos móviles.  

Para más información, consulte estos artículos:  

- [Elegir una solución de administración de dispositivos](../plan-design/choose-a-device-management-solution.md)  

- [Métodos de instalación de cliente](../clients/deploy/plan/client-installation-methods.md)  

- [Introducción a las recopilaciones](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Configuración de cliente

Cuando instala Configuration Manager por primera vez, todos los clientes de la jerarquía se configuran mediante la configuración de cliente predeterminada, que se puede cambiar. La configuración de cliente incluye estas opciones:

- La frecuencia de comunicación de los dispositivos con el sitio.

- Si el cliente está configurado para actualizaciones de software y otras operaciones de administración.

- Si los usuarios pueden inscribir sus dispositivos móviles para que los administre Configuration Manager.  

Puede crear la configuración de cliente personalizada y, a continuación, asignarla a las colecciones. Los miembros de la recopilación están configurados para tener los valores personalizados, y puede crear varias configuraciones de cliente personalizadas que se apliquen en el orden especificado (por orden numérico). En caso de conflicto, la configuración que tenga el número de orden más bajo invalida al resto de configuraciones.  

En el diagrama siguiente se muestra un ejemplo de cómo se crea y se aplica una configuración de cliente personalizada.  

![Configuración de cliente](media/ClientSettings.gif)  

Para más información sobre la configuración de cliente, consulte estos artículos:

- [Cómo establecer la configuración del cliente](../clients/deploy/configure-client-settings.md)
- [Acerca de la configuración de cliente](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Administración de dispositivos sin el cliente de Configuration Manager

Configuration Manager admite la administración de algunos dispositivos que no tienen instalado el software cliente y que no están administrados mediante Intune. Para más información, consulte el artículo sobre cómo [administrar dispositivos móviles con la infraestructura local en Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) y [Administrar dispositivos móviles mediante Configuration Manager y Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Administración basada en el usuario

Configuration Manager admite recopilaciones de usuarios de Azure Active Directory Domain Services. Cuando use una recopilación de usuarios, puede instalar software en todos los equipos que usen los miembros de la recopilación. Para asegurarse de que el software que implementa solo se instala en los dispositivos especificados como dispositivo primario del usuario, configure la afinidad entre usuario y dispositivo. Un usuario puede tener uno o más dispositivos principales.  

Para controlar la experiencia de implementación de software, los usuarios pueden usar la interfaz de cliente del **Centro de software**. El **Centro de software** se instala automáticamente en los equipos cliente y se ejecuta desde el menú **Inicio** de Windows. El **Centro de software** permite que los usuarios administren su propio software y realicen las tareas siguientes:  

- Instalar software  

- Programar software para su instalación automática fuera del horario laboral  

- Configurar cuándo puede instalar Configuration Manager software en un dispositivo.  

- Configurar opciones de acceso para el control remoto, si este está configurado en Configuration Manager.  

- Configurar opciones de administración de energía, si un administrador establece esta opción.  

- Buscar, instalar y solicitar software.

- Configurar opciones de preferencias.

- Cuando termine la configuración, especifique un dispositivo primario para la afinidad entre usuario y dispositivo.

Vea los siguientes artículos para más información:

- [Planeamiento del centro de software](../../apps/plan-design/plan-for-software-center.md)
- [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Manual del usuario del Centro de software](software-center.md)
