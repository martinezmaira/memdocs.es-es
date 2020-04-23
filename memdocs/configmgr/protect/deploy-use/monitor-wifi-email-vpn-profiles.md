---
title: Supervisión de perfiles de correo electrónico, Wi-Fi y VPN
titleSuffix: Configuration Manager
description: Aprenda a supervisar el estado de compatibilidad de los perfiles de correo electrónico, Wi-Fi y VPN en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709433"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Supervisión de perfiles de correo electrónico, Wi-Fi y VPN en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de haber implementado los perfiles de correo electrónico, Wi-Fi y VPN de Configuration Manager en los usuarios de la jerarquía, puede usar estos procedimientos para supervisar el estado de compatibilidad del perfil:  

-   [Ver los resultados de compatibilidad en la consola de Configuration Manager](#BKMK_console)  

-   [Ver los resultados de compatibilidad mediante informes](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Ver los resultados de compatibilidad en la consola de Configuration Manager  
 Use este procedimiento para ver los detalles sobre la compatibilidad de los perfiles implementados en la consola de Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver los resultados de compatibilidad en la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Implementaciones**.  

3.  En la lista **Implementaciones**, seleccione la implementación del perfil para el que quiere revisar la información de compatibilidad.  

4.  Puede revisar la información de resumen sobre la compatibilidad de la implementación del perfil en la página principal. Para ver información más detallada, seleccione la implementación del perfil y luego, en la pestaña **Inicio** del grupo **Implementación**, haga clic en **Ver estado** para abrir la página **Estado de implementación**.  

     La página **Estado de implementación** contiene las siguientes pestañas:  

    -   **Conforme:** muestra la compatibilidad del perfil en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios compatibles con este perfil. El panel **Detalles del activo** muestra los usuarios que son compatibles con el perfil. Haga doble clic en un usuario de la lista para mostrar información adicional.  

        > [!IMPORTANT]  
        >  Un perfil no se evalúa si no es aplicable en un determinado dispositivo cliente, pero se devuelve como compatible.  

    -   **Error:** muestra una lista de todos los errores de la implementación del perfil seleccionada en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios que generaron errores con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

    -   **No compatible:** muestra una lista de todas las reglas no compatibles en el perfil en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios no compatibles con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

    -   **Desconocido:** muestra una lista de todos los usuarios que no han notificado el cumplimiento de la implementación del perfil seleccionada y el estado de cliente actual de los dispositivos.  

5.  En la página **Estado de implementación**, puede revisar información detallada sobre la compatibilidad del perfil implementado. Se crea un nodo temporal en el nodo **Implementaciones** que le permite encontrar esta información rápidamente.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> Ver los resultados de compatibilidad mediante informes  
 La configuración de compatibilidad, que incluye los perfiles de Configuration Manager, también incluye varios informes integrados que permiten supervisar la información sobre los perfiles. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
>  Debe usar un carácter comodín (%) para utilizar los parámetros **Filtro del dispositivo** y **Filtro de usuarios** en los informes de configuración de cumplimiento.  

 Para obtener más información sobre cómo configurar informes en Configuration Manager, consulte [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).  
