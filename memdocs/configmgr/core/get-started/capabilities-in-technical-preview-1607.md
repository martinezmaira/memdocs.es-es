---
title: Funcionalidades de Technical Preview 1607
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 73aac9e1bfb7b902a7db28ba4be00a2a02277324
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905689"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Funciones de Technical Preview 1607 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1607 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a> Mejoras en la directiva de actualización de la edición de Windows 10

En esta versión se han realizado las siguientes mejoras de esta directiva:

* Ahora puede usar la directiva de actualización de la edición con equipos Windows 10 que ejecuten el cliente de Configuration Manager además de con equipos Windows 10 inscritos en Microsoft Intune.
* Puede actualizar desde Windows 10 Professional a cualquiera de las plataformas del asistente compatibles con el hardware.

[Más información sobre la directiva de actualización de la edición de Windows 10](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>Haga la prueba

1. Use la información del [tema sobre la actualización de directiva de la edición existente](../../compliance/deploy-use/upgrade-windows-version.md) para crear una directiva de actualización de la edición.
2. Implemente esta directiva en un equipo Windows 10 con el cliente de Configuration Manager.
Una vez que la directiva alcance un equipo Windows de destino, el equipo se reiniciará durante las dos horas posteriores a la aplicación de la actualización. De momento no se puede suprimir este reinicio. Asegúrese de informar a los usuarios a los que implemente la directiva, o prográmela para que se ejecute fuera del horario laboral de los usuarios.

### <a name="known-issue-with-this-release"></a>Problemas conocidos de esta versión
En la configuración de cliente de Configuration Manager, puede que vea la configuración de **Actualización de edición**. En esta versión, esta configuración no es funcional. Use las instrucciones anteriores para actualizar Windows 10 a una versión más reciente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Cuadros de diálogo personalizables de personalización de marca del Centro de software

La personalización de marca del Centro de software se presentó en la versión 1602 de Configuration Manager. En Technical Preview versión 1607, se ha ampliado a todos los cuadros de diálogo asociados y a las notificaciones de la barra de tareas para proporcionar una experiencia más coherente a los usuarios del Centro de software.

### <a name="try-it-out"></a>Haga la prueba

La personalización de marca del Centro de software se aplica conforme a las siguientes reglas:

1. Si no está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de organización especificado en el cliente **Agente de equipo** que establece el **Nombre de organización mostrado en el Centro de software**. Para obtener instrucciones, vea [Cómo establecer la configuración del cliente](../../core/clients/deploy/configure-client-settings.md).

2. Si está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de la organización y el color especificados en las propiedades del rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones. Para más información, vea [Configuration options for Application Catalog website point (Opciones de configuración del punto de sitios web del catálogo de aplicaciones)](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Si una suscripción de Microsoft Intune está configurada y conectada al entorno de Configuration Manager, el Centro de software mostrará el nombre de la organización, el color y el logotipo de la empresa especificados en las propiedades de la suscripción de Intune.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Usar el mismo adaptador de red para varias implementaciones iniciadas por PXE
En Technical Preview versión 1607, cuando se usa un adaptador Ethernet para crear una imagen de varios dispositivos (como un adaptador Ethernet USB que use en varios dispositivos), puede habilitar una nueva opción que permita especificar los identificadores de hardware para los adaptadores Ethernet. Configuration Manager omite los identificadores de hardware de la lista al realizar una instalación PXE y para el registro de cliente.

Para más información sobre este problema, vea el [Blog del equipo de soporte técnico de Configuration Manager OSD](https://techcommunity.microsoft.com/t5/configuration-manager-archive/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in/ba-p/273721).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Habilitar la característica para administrar identificadores de hardware duplicados  
1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Actualizaciones y mantenimiento** > **Características**.
2. En el panel de información, seleccione **Administrar identificadores de hardware duplicados**.
3. En la pestaña **Inicio**, en el grupo **Características**, haga clic en **Activar**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Agregar identificadores de hardware para que Configuration Manager los omita  
1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. En la pestaña **Inicio** , en el grupo **Sitios** , haga clic en **Configuración de jerarquía**.
3. Vaya a la pestaña **Aprobación de cliente y registros conflictivos**.
4. Haga clic en **Agregar** en la sección **Identificadores de hardware duplicados** para agregar nuevos identificadores de hardware.
