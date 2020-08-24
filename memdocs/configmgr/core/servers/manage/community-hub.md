---
title: GitHub y Centro de comunidad
titleSuffix: Configuration Manager
description: Habilitación y uso del Centro de comunidad en Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128178"
---
# <a name="community-hub-and-github"></a>GitHub y Centro de comunidad
<!--3555935, 3555936-->

La comunidad de administradores de TI ha desarrollado una gran cantidad de conocimientos con el paso de los años. En lugar de reinventar elementos como scripts e informes desde cero, hemos creado un **Centro de comunidad de Configuration Manager** donde los administradores de TI pueden compartir contenido entre sí. Al aprovechar el trabajo de los demás, puede ahorrarse horas de trabajo. El Centro de comunidad fomenta la creatividad al permitir construir sobre los trabajos de otros y que otros construyan sobre los suyos. GitHub ya tiene procesos y herramientas en todo el sector diseñados para el uso compartido. Ahora, el Centro de comunidad usará estas herramientas directamente en la consola de Configuration Manager como las piezas fundamentales para impulsar esta nueva comunidad. Para la versión inicial, el contenido disponible en el Centro de comunidad solo será cargado por Microsoft. En el futuro, los administradores de TI podrán cargar el contenido por su cuenta, mediante su propia cuenta de GitHub.

> [!Note]  
> El Centro de comunidad es una característica opcional basada en la nube. Se presentó por primera vez en junio de 2020. Para información sobre cómo participar en el Centro de comunidad, consulte [Características opcionales](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Acerca del Centro de comunidad

El Centro de comunidad admite los siguientes objetos:

- Consultas de CMPivot
- Aplicaciones
- Secuencias de tareas
- Elementos de configuración
- Scripts de PowerShell
- Informes

## <a name="prerequisites"></a>Requisitos previos

- El dispositivo que ejecuta la consola de Configuration Manager utilizado para acceder al Centro de comunidad necesita los siguientes elementos:
   - .Net Framework, versión 4.6 o posterior
   - Compilación 17110 o versiones posteriores de Windows 10
      - Windows Server no es compatible, por lo que la consola de Configuration Manager debe instalarse en un dispositivo Windows 10 distinto del servidor de sitio.
   - La cuenta de usuario de inicio de sesión no puede ser la cuenta de administrador integrada.

- El [servicio de administración](../../../develop/adminservice/set-up.md) de Configuration Manager debe estar configurado y encontrarse en funcionamiento.

- Si la organización restringe la comunicación de red con Internet mediante un dispositivo proxy o un firewall, tiene que permitir que la consola de Configuration Manager acceda a los puntos de conexión de Internet. Para más información, consulte los [requisitos de acceso a Internet](../../plan-design/network/internet-endpoints.md#community-hub).

## <a name="permissions"></a>Permisos

- Para importar un script: Permiso **Crear** para la clase **SMS_Scripts**.
- Para importar un informe: Rol de seguridad Administrador total.


## <a name="use-the-community-hub"></a>Unión al Centro de comunidad

1. Vaya al nodo **Centro de comunidad** en el área de trabajo **Comunidad**.
1. Seleccione un elemento para descargarlo.
1. Necesitará los permisos apropiados del sitio de Configuration Manager para descargar objetos del centro e importarlos en el sitio.
    - Para importar un script: **Cree** el permiso para la clase SMS_Scripts.
    - Para importar un informe: Rol de seguridad Administrador total.
1. Los informes descargados se implementan en una carpeta de informes llamada **centro** en el punto de servicios de informes. Los scripts descargados pueden verse en el nodo **Ejecutar scripts**.
1. Para ver todos los elementos descargados del Centro por su organización, haga clic en la carpeta de **sus descargas** en el nodo **Centro de la comunidad**.

[![Todos los elementos descargados del Centro de comunidad](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Vínculos directos a elementos del Centro de comunidad
<!--4224406-->
*(Se incorporó en la versión 2006)* Puede desplazarse fácilmente hasta los elementos del nodo Centro de comunidad de la consola de Configuration Manager, y hacer referencia a ellos, con un vínculo directo. Esta característica tiene como fin facilitar la colaboración y poder compartir vínculos a elementos del Centro de comunidad con los compañeros. Actualmente, estos vínculos profundos solo son para los elementos del nodo Centro de comunidad de la consola.

### <a name="prerequisites-for-direct-links"></a>Requisitos previos de los vínculos directos

- Consola de Configuration Manager, versión 2006 o posterior
- No se puede usar la cuenta predefinida de administrador local al seguir un vínculo del Centro de comunidad.

### <a name="sharing-and-opening-direct-links"></a>Compartir y abrir vínculos directos

Para compartir un elemento:
1. Vaya al elemento en el centro y seleccione **Compartir**.
1. Pegue el vínculo copiado y compártalo con otros usuarios.

Para abrir un vínculo compartido:
1. Haga clic en el vínculo desde un equipo que tenga instalada la consola de Configuration Manager.
   - Por ejemplo, use este vínculo para compartir el [script de configuración de la actualización automática de Edge](https://communityhub.microsoft.com/item/7200) (`https://communityhub.microsoft.com/item/7200`).
1. Seleccione **Iniciar el Centro de comunidad** cuando se le solicite.
1. La consola se abre directamente en el script del Centro de comunidad.

## <a name="known-issues"></a><a name="bkmk_known"></a> Problemas conocidos

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>No se puede acceder al nodo Centro de comunidad cuando se ejecuta la consola como un usuario diferente
<!--7826897-->
Si ha iniciado sesión como un usuario con derechos más restringidos y elige **Ejecutar como** otro usuario para abrir la consola de Configuration Manager, es posible que no pueda acceder al nodo **Centro de comunidad**.

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>Los informes descargados no se quitan de la página de descargas
<!--7851305-->
Si elimina un informe descargado del nodo **Supervisión** > **Informes**, el informe no se elimina de la página **Centro de comunidad** > **Sus descargas** y no puede volver a descargar el informe. 

## <a name="next-steps"></a>Pasos siguientes

Más información sobre la creación y el uso de los siguientes objetos:

- [Crear y ejecutar scripts de PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introducción a los informes](introduction-to-reporting.md)
- [Creación y administración de secuencias de tareas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Crear e implementar una aplicación](../../../apps/get-started/create-and-deploy-an-application.md)
- [Crear elementos de configuración](../../../compliance/deploy-use/create-configuration-items.md)