---
title: Introducción a la implementación de sistema operativo
titleSuffix: Configuration Manager
description: Comprenda los conceptos antes de implementar sistemas operativos en su entorno de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703873"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Introducción a la implementación del sistema operativo en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede usar Configuration Manager para implementar sistemas operativos de varias maneras diferentes. Use la información de esta sección para comprender cómo implementar sistemas operativos y automatizar tareas. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> El proceso de implementación de sistema operativo  
 Configuration Manager proporciona varios métodos que puede usar para implementar un sistema operativo. Independientemente del método de implementación que use, existen varias acciones que se deben llevar a cabo:  

-   Identifique los controladores de dispositivos de Windows que sean necesarios para iniciar la imagen de arranque o la imagen de sistema operativo que debe implementar.  

-   Identifique la imagen de arranque que desea usar para iniciar el equipo de destino.  

-   Use una secuencia de tareas para capturar una imagen del sistema operativo que va a implementar. Como alternativa, puede usar una imagen de sistema operativo predeterminada.  

-   Distribuya la imagen de arranque, la imagen de sistema operativo y cualquier contenido relacionado en un punto de distribución.  

-   Cree una secuencia de tareas siguiendo las etapas para implementar la imagen de arranque y la imagen de sistema operativo.  

-   Implemente la secuencia de tareas en una recopilación de equipos.  

-   Supervise la implementación.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> Escenarios de implementación de sistema operativo  
 Hay muchos escenarios de implementación de sistema operativo en Configuration Manager que puede elegir dependiendo de su entorno y del propósito de la instalación de sistema operativo.  Por ejemplo, puede particionar y formatear un equipo existente con una nueva versión de Windows o actualizar Windows a la versión más reciente. Para ayudarle a determinar el método de implementación que satisfaga sus necesidades, revise [Escenarios para implementar sistemas operativos de empresa](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Puede elegir entre los siguientes escenarios de implementación de sistema operativo:  

-   [Actualizar Windows a la versión más reciente](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Actualizar un equipo existente con una nueva versión de Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Reemplazar un equipo existente y transferir la configuración](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> Métodos para implementar sistemas operativos  
 Existen varios métodos que puede usar para implementar sistemas operativos en equipos cliente de Configuration Manager.  

- **Implementaciones iniciadas por PXE**: las implementaciones iniciadas por PXE permiten a los equipos cliente solicitar una implementación a través de la red. En este método de implementación, la imagen de sistema operativo y una imagen de arranque de Windows PE se envían a un punto de distribución que está configurado para aceptar solicitudes de arranque de PXE. Para más información, consulte [Usar PXE para implementar Windows a través de la red con Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **Hacer que los sistemas operativos estén disponibles en el Centro de software**: puede implementar un sistema operativo y hacer que esté disponible en el Centro de software. Los clientes de Configuration Manager pueden iniciar la instalación de sistema operativo desde el Centro de software. Para obtener más información, consulte [Reemplazar un equipo existente y transferir la configuración](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Implementaciones de multidifusión**: las implementaciones de multidifusión ahorran ancho de banda de red al enviar datos a varios clientes a la vez en lugar de enviar una copia de los datos a cada cliente a través conexiones diferentes. En este método de implementación, la imagen de sistema operativo se envía a un punto de distribución. Esto, a su vez, implementa la imagen cuando los equipos cliente solicitan la implementación. Para obtener más información, consulte [Usar multidifusión para implementar Windows a través de la red](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Implementaciones de medios de arranque**: las implementaciones de medios de arranque le permiten implementar el sistema operativo al iniciar el equipo de destino. Cuando se inicia el equipo de destino, recupera la secuencia de tareas, la imagen de sistema operativo y cualquier otro tipo de contenido necesario de la red. Debido a que el contenido no se incluye en los medios, puede actualizar el contenido sin tener que volver a crear los medios. Para obtener más información, consulte [Crear medios de arranque](../deploy-use/create-bootable-media.md).  

- **Implementaciones de medios de arranque**: las implementaciones de medios independientes le permiten implementar sistemas operativos en las condiciones siguientes:  

  - En entornos donde no resulta práctico copiar una imagen de sistema operativo u otros paquetes grandes a través de la red.  

  - En entornos sin conectividad de red o conectividad de red de bajo ancho de banda.  

    Para obtener más información, consulte [Crear medios independientes](../deploy-use/create-stand-alone-media.md).  

- **Implementaciones de medios preconfigurados**: las implementaciones de medios preconfigurados le permiten implementar un sistema operativo en un equipo que no está aprovisionado por completo. Los medios preconfigurados son un archivo Windows Imaging Format (WIM) que puede ser instalado en un equipo sin sistema operativo por el fabricante o en un centro de configuración empresarial no relacionado con el entorno de Configuration Manager.  

   Más adelante, cuando el equipo se inicie en el entorno de Configuration Manager, lo hará por medio de la imagen de arranque proporcionada por los medios y, después, se conectará al punto de administración del sitio en busca de secuencias de tareas disponibles que completen el proceso de descarga. Este método de implementación puede reducir el tráfico de red porque la imagen de arranque y la imagen de sistema operativo ya están en el equipo de destino. Puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiera incluir en los medios preconfigurados. Para obtener más información, consulte [Crear medios preconfigurados](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a> Imágenes de arranque  
 Una imagen de arranque de Configuration Manager es una imagen de Windows PE (WinPE) que se usa durante la implementación del sistema operativo. Las imágenes de arranque se usan para iniciar un equipo en WinPE, que es un sistema operativo mínimo con componentes y servicios limitados que prepara el equipo de destino para la instalación de Windows. Configuration Manager proporciona dos imágenes de arranque: Una para plataformas x86 y otra para plataformas x64. Se consideran imágenes de arranque predeterminadas. Las imágenes de arranque que crea y agrega a Configuration Manager se consideran imágenes personalizadas. Las imágenes de arranque predeterminadas se pueden reemplazar automáticamente al actualizar Configuration Manager. Para obtener más información sobre las imágenes de arranque, consulte [Administrar imágenes de arranque](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> Imágenes de sistema operativo  
 Las imágenes de sistema operativo de Configuration Manager se almacenan en el archivo de formato de archivo Windows Imaging (WIM) y representan una recopilación comprimida de carpetas y archivos de referencia que se necesitan para instalar y configurar correctamente un sistema operativo en un equipo. Para todos los escenarios de implementación de sistema operativo, debe seleccionar una imagen de sistema operativo. Puede usar la imagen de sistema operativo predeterminada o crearla desde un equipo de referencia que configure. Para obtener más información, consulte [Administrar imágenes de sistema operativo](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a> Paquetes de actualización del sistema operativo  
 Los paquetes de actualización de sistema operativo se usan para actualizar un sistema operativo y son implementaciones de sistema operativo iniciadas por el programa de instalación. Los paquetes de actualización de sistema operativo se importan en Configuration Manager desde un DVD o un archivo ISO montado. Para más información, consulte [Administrar paquetes de actualización de sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a> Medios usados para implementar sistemas operativos  
 Puede crear varios tipos de medios que se pueden utilizar para implementar sistemas operativos. Esto incluye los medios de captura que se utilizan para capturar imágenes de sistema operativo, y medios independientes, preconfigurados y de arranque que se utilizan para implementar un sistema operativo. Mediante el uso de medios, puede implementar sistemas operativos en equipos que no tienen una conexión de red o que tienen una conexión de ancho de banda bajo al sitio de Configuration Manager. Para obtener más información sobre cómo usar los medios, consulte [Crear medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Controladores de dispositivo  
 Puede instalar controladores de dispositivos en equipos de destino sin incluirlos en la imagen del sistema operativo que se va a implementar. Configuration Manager proporciona un catálogo de controladores con referencias a todos los controladores de dispositivos que se importan a Configuration Manager. El catálogo de controladores se encuentra en el área de trabajo **Biblioteca de software** y consta de dos nodos: **Controladores** y **Paquetes de controladores**. El nodo **Controladores** enumera todos los controladores que haya importado en el catálogo de controladores. Puede usar este nodo para detectar detalles acerca de cada controlador importado, para cambiar el paquete de controladores o imagen de arranque al que pertenece un controlador, para habilitar o deshabilitar un controlador, y muchas cosas más. Para obtener más información, consulte [Administrar controladores](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> Guardar y restaurar el estado de usuario  
 Cuando implemente sistemas operativos, puede guardar el estado del usuario en el equipo de destino, implementar el sistema operativo y, a continuación, restaurar el estado del usuario después de implementar los sistemas operativos. Este proceso se suele usar cuando se instala el sistema operativo en un equipo cliente de Configuration Manager.  

 La información del estado del usuario se captura y restaura mediante el uso de secuencias de tareas. Cuando se captura la información del estado del usuario, esta información se puede almacenar de una de las siguientes maneras:  

- Puede guardar los datos de estado de usuario de forma remota mediante la configuración de un punto de migración de estado. La secuencia de tareas de captura envía los datos al punto de migración de estado. A continuación, una vez que se implementa el sistema operativo, la secuencia de tareas de restauración recupera los datos y restaura el estado del usuario en el equipo de destino.  

- Puede almacenar los datos de estado de usuario localmente en una ubicación específica. En este escenario, la secuencia de tareas de captura copia los datos de usuario en una ubicación específica del equipo de destino. A continuación, una vez implementado el sistema operativo, la secuencia de tareas de restauración recupera los datos del usuario desde esa ubicación.  

- Puede especificar vínculos físicos que pueden utilizarse para restaurar los datos del usuario a su ubicación original. En este escenario, los datos de estado de usuario permanecen en la unidad cuando se quita el sistema operativo antiguo. A continuación, una vez implementado el sistema operativo, la secuencia de tareas de restauración utiliza los vínculos físicos para restaurar los datos de estado de usuario a su ubicación original.  

  Para obtener más información, consulte [Administrar el estado de usuario](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Implementación en equipos desconocidos  
 Puede implementar un sistema operativo en equipos no administrados por Configuration Manager. No hay ningún registro de estos equipos en la base de datos de Configuration Manager. Estos equipos se conocen como equipos desconocidos. Los equipos desconocidos incluyen los siguientes:  

- Un equipo que no tiene instalado el cliente de Configuration Manager  

- Un equipo que no se importa en Configuration Manager  

- Un equipo que no ha detectado Configuration Manager  

  Para obtener más información, consulte [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> Asociar usuarios a un equipo  
 Al implementar un sistema operativo, puede asociar los usuarios al equipo de destino para admitir las acciones de la afinidad de dispositivo de usuario. Cuando asocia un usuario a un equipo de destino, el usuario administrativo puede realizar acciones más adelante en el equipo que esté asociado a ese usuario, como implementar una aplicación en el equipo de un usuario específico. Sin embargo, cuando se implementa un sistema operativo, no se puede implementar el sistema operativo en el equipo de un usuario específico. Para obtener más información, consulte [Asociar usuarios a un equipo de destino](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> Usar secuencias de tareas para automatizar etapas  
 Puede crear secuencias de tareas que realicen diversas tareas en su entorno de Configuration Manager. Las acciones de la secuencia de tareas se definen en los pasos individuales de la secuencia. Cuando se ejecuta una secuencia de tareas, se realizan las acciones de cada paso en el nivel de la línea de comandos sin necesidad de intervención del usuario. Puede usar las secuencias de tareas para lo siguiente:  

-   [Crear una secuencia de tareas para instalar un sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Crear una secuencia de tareas para implementaciones que no son de sistema operativo](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Crear una secuencia de tareas para capturar un sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Crear una secuencia de tareas para capturar y restaurar el estado del usuario](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Crear una secuencia de tareas personalizada](../deploy-use/create-a-custom-task-sequence.md)  
