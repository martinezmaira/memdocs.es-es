---
title: Perfiles de OneDrive para la Empresa
titleSuffix: Configuration Manager
description: Redirija las carpetas conocidas de Windows a OneDrive para la Empresa mediante un perfil de OneDrive para la Empresa en Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 47d44c96e0ae63504278c58a5838c54648665505
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692313"
---
# <a name="onedrive-for-business-profiles"></a>Perfiles de OneDrive para la Empresa

A partir de la versión 1902 de Configuration Manager, puede crear perfiles de OneDrive para la Empresa con el fin de mover las carpetas conocidas de Windows a OneDrive para la Empresa. Estas carpetas incluyen Escritorio, Documentos e Imágenes. En cada perfil, puede especificar opciones para mover las carpetas conocidas de Windows. Para más información sobre OneDrive para la Empresa, consulte [Redirigir y mover las carpetas conocidas de Windows a OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Requisitos previos

- [Búsqueda del identificador de inquilino de Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Implemente la versión de cliente de sincronización de OneDrive 18.111.0603.0004 o una versión posterior. Para más información, consulte [Implementar aplicaciones de OneDrive con System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a> Mover las carpetas conocidas de Windows a OneDrive
<!--3556021-->
Utilice Configuration Manager para mover las carpetas conocidas de Windows a OneDrive para la Empresa. Estas carpetas incluyen Escritorio, Documentos e Imágenes. Para simplificar las actualizaciones de Windows 10, implemente esta configuración en los clientes de Windows 7 antes de implementar una secuencia de tareas. 

1. En la consola de Configuration Manager, vaya el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione el nodo **OneDrive for Business Profiles** (Perfiles de OneDrive para la Empresa).  

   ![Nodo de perfiles de OneDrive para la Empresa](media/onedrive-for-business-profiles-node.png)
2. En la cinta, seleccione **Create OneDrive for Business Profile** (Crear perfil de OneDrive para la Empresa).  

3. Especifique un nombre para identificar esta directiva y seleccione **Siguiente**.  

4. Seleccione las plataformas que se aprovisionarán con el perfil de OneDrive para la Empresa. Cuando haya terminado de seleccionar las plataformas, haga clic en **Siguiente**.

    ![Selección de plataformas para el perfil de OneDrive para la Empresa](media/onedrive-for-business-profile-select-platforms.png) 

5. En la página **Configuración**:

    1. Especifique el identificador del inquilino de Office 365.  

    2. Seleccione una de las siguientes opciones para trasladar las carpetas conocidas a OneDrive:  

        - **Pedir a los usuarios que muevan las carpetas conocidas de Windows a OneDrive**: con esta opción, el usuario ve un Asistente para mover sus archivos. Si quiere aplazar o rechazar el traslado de las carpetas, OneDrive se lo recuerda periódicamente.  

        - **Mover carpetas conocidas de Windows a OneDrive silenciosamente**: cuando esta directiva se aplica al dispositivo, el cliente de OneDrive redirige automáticamente las carpetas conocidas a OneDrive para la Empresa.  

            - **Mostrar una notificación a los usuarios después de haber redirigido las carpetas**: si se habilita esta opción, el cliente de OneDrive notifica al usuario una vez que mueve sus carpetas.  

    3. **Impedir que los usuarios redirijan las carpetas conocidas de Windows a su equipo**: deshabilite la opción de OneDrive para la Empresa en el cliente para que los usuarios lleven de nuevo estas carpetas al dispositivo.  

       ![Configuración para mover carpetas conocidas en OneDrive para la Empresa](media/onedrive-for-business-profile-move-folder-settings.png)

6. Complete el asistente y, después, implemente la directiva.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Implementación del perfil de OneDrive para la Empresa

1. En la consola de Configuration Manager, vaya el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione el nodo **OneDrive for Business Profiles** (Perfiles de OneDrive para la Empresa).  


2. Seleccione el perfil y, a continuación, seleccione **Implementar** en la cinta.

3. Especifique la siguiente configuración para la implementación:

   1. **Recopilación**: haga clic en **Examinar...** para seleccionar la recopilación para la que quiere implementar el perfil.  
   1. **Generar una alerta**:

      - **Cuando la compatibilidad está por debajo de**: porcentaje mínimo de cumplimiento del cliente para mantener la alerta.
      -  **Fecha y hora**: la fecha alerta el primer inicio que se genera en función de la compatibilidad del perfil.
      - **Generar alerta de System Center Operations Manager**: se envía una alerta de cumplimiento a System Center Operations Manager.
   1. **Programación**:

      - **Programación sencilla**: de forma predeterminada, esta configuración usa una programación sencilla para iniciar la evaluación de cumplimiento cada siete días.
      - **Programación personalizada**: define cuándo se debe ejecutar la evaluación de cumplimiento. La hora de inicio se basa en la hora local del equipo que ejecuta la consola de Configuration Manager en el momento de crear la programación o se puede usar UTC.
 
      ![Implementación del perfil de OneDrive para la Empresa](media/onedrive-for-business-deploy-profile.png)

4. Haga clic en **Aceptar** para implementar el perfil de OneDrive para la Empresa.


## <a name="next-steps"></a>Pasos siguientes

[Crear perfiles de conexión remota](create-remote-connection-profiles.md)
