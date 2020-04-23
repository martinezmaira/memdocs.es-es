---
title: Supervisión de perfiles de certificado
titleSuffix: Configuration Manager
description: Aprenda a supervisar el estado de cumplimiento de los perfiles de certificado de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706313"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Cómo supervisar perfiles de certificado en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver los resultados de cumplimiento en la consola de Configuration Manager  

Para supervisar el cumplimiento del certificado SCEP, no use la consola. En su lugar, use los [informes](#view-compliance-results-by-using-reports). 

1. En la consola de Configuration Manager, elija **Supervisión**>  **Implementaciones**.  

2. Seleccione la implementación de perfil de certificado que le interese.  

3. Revise la información de resumen de compatibilidad de certificado en la página principal. Para obtener información más detallada, seleccione el perfil de certificado y, después, en la pestaña **Inicio**, en el grupo **Implementación**, haga clic en **Ver estado** para abrir la página **Estado de implementación**.  

    La página **Estado de implementación** contiene las siguientes pestañas:  

   -   **Conforme**: muestra la compatibilidad del perfil de certificado en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** . Este nodo contiene todos los usuarios que son compatibles con el perfil de certificado. El panel **Detalles del activo** muestra los usuarios que son compatibles con el perfil. Haga doble clic en un usuario en la lista para obtener más información.  

       > [!IMPORTANT]  
       >  Un perfil de certificado no se evalúa si no es aplicable en un dispositivo cliente. Sin embargo, se devuelve como compatible.  

   -   **Error**: muestra una lista de todos los errores de la implementación de perfil de certificado seleccionada, en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** del área de trabajo **Activos y compatibilidad** . Este nodo contiene todos los usuarios que generaron errores con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario en la lista para mostrar más información.  

   -   **No conforme**: muestra una lista de todas las reglas no compatibles en el perfil de certificado en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** del área de trabajo **Activos y compatibilidad** . El nodo contiene todos los usuarios que no son compatibles con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

   -   **Desconocido**: muestra una lista de todos los usuarios que no notificaron la compatibilidad de la implementación de perfil de certificado seleccionada y el estado de cliente actual de los dispositivos.  

4. En la página **Estado implementación**, puede revisar información detallada sobre la compatibilidad del perfil de certificado implementado. Se crea un nodo temporal en el nodo **Implementaciones** que le permite encontrar esta información rápidamente.  

    El estado de inscripción del certificado se muestra como un número. Utilice la tabla siguiente para determinar el significado de cada número:  


   | Estado de inscripción |                                                                                                                   Descripción                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         La inscripción se realizó correctamente y el certificado se emitió.                                                                                          |
   |    0x00000002     |                                                                    La solicitud se envió y la inscripción está pendiente, o la solicitud se emitió fuera de banda.                                                                    |
   |    0x00000004     |                                                                                                          La inscripción debe aplazarse.                                                                                                           |
   |    0x00000010     |                                                                                                               Error.                                                                                                                |
   |    0x00000020     |                                                                                                        Se desconoce el estado de la inscripción.                                                                                                        |
   |    0x00000040     | Se ha omitido la información de estado. Esto puede ocurrir si una entidad de certificación HYPERLINK "<https://msdn.microsoft.com/windows/ms721572>" \l "_security_certification_authority_gly" no es válida o no se ha seleccionado para la supervisión. |
   |    0x00000100     |                                                                                                           Se ha denegado la inscripción.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Ver los resultados de compatibilidad mediante informes

La configuración de cumplimiento en Configuration Manager incluye informes integrados que se pueden utilizar para supervisar la información de perfiles de certificado. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
>  Debe usar un carácter comodín (%) para utilizar los parámetros **Filtro del dispositivo** y **Filtro de usuarios** en los informes de configuración de cumplimiento.  

Para supervisar el cumplimiento del certificado SCEP, use los informes de certificado que se encuentran en el nodo de informes **Acceso a los recursos de la compañía**:  

-   Historial de certificados emitidos  
-   Lista de activos con certificados a punto de expirar  
-   Lista de activos por estado de emisión de certificado  



 Para obtener más información sobre cómo configurar informes en Configuration Manager, consulte [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).  
