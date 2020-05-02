---
title: Configuración de las opciones de Microsoft Edge
titleSuffix: Configuration Manager
description: Configuración de las opciones para el explorador web Microsoft Edge en los clientes de Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210101"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Configuración de opciones de Microsoft Edge en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!-- 1357310 -->
A partir de la versión 1802, para los clientes que usan el explorador web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) en los clientes de Windows 10, cree una directiva de configuración de cumplimiento de Configuration Manager para configurar varias opciones de Microsoft Edge. 

Esta directiva solo se aplica a clientes de Windows 10, versión 1703 o una versión posterior. <!--511552-->


## <a name="policy-settings"></a>Configuración de la directiva
Actualmente, esta directiva incluye las siguientes opciones:
- **Set Microsoft Edge browser as default** (Establecer el explorador Microsoft Edge como predeterminado): configura los parámetros de la aplicación predeterminada de Windows 10 en cuanto a explorador web para que sea Microsoft Edge.
- **Permitir función desplegable de la barra de direcciones**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [AllowAddressBarDropdown browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown) (Directiva de explorador AllowAddressBarDropdown).
- **Permitir sincronizar favoritos entre exploradores de Microsoft**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [SyncFavoritesBetweenIEAndMicrosoftEdge browser policy](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge) (Directiva de explorador SyncFavoritesBetweenIEAndMicrosoftEdge).
- **Permitir borrar datos de exploración al salir**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [ClearBrowsingDataOnExit browser policy](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit) (Directiva de explorador ClearBrowsingDataOnExit).
- **Permitir encabezados Do Not Track**: para obtener más información, vea [AllowDoNotTrack browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack) (Directiva de explorador AllowDoNotTrack).
- **Permitir autorrelleno**: para obtener más información, vea [AllowAutofill browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill) (Directiva de explorador AllowAutofill).
- **Permitir cookies**: para obtener más información, vea [AllowCookies browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies). (Directiva de explorador AllowCookies).
- **Permitir bloqueador de elementos emergentes**: para obtener más información, vea [AllowPopups browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups). (Directiva de explorador AllowPopups).
- **Permitir sugerencias de búsqueda en la barra de direcciones**: para obtener más información, vea [AllowSearchSuggestionsinAddressBar browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar) (Directiva de explorador AllowSearchSuggestionsinAddressBar).
- **Permitir el envío de tráfico de la intranet a Internet Explorer**: para obtener más información, vea [SendIntranetTraffictoInternetExplorer browser policy](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer) (Directiva de explorador SendIntranetTraffictoInternetExplorer).
- **Permitir administrador de contraseñas**: para obtener más información, vea [AllowPasswordManager browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager) (Directiva de explorador AllowPasswordManager).
- **Permitir Herramientas de desarrollo**: para obtener más información, vea [AllowDeveloperTools browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools) (Directiva de explorador AllowDeveloperTools).
- **Permitir extensiones**: para obtener más información, vea [AllowExtensions browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions) (Directiva de explorador AllowExtensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar SmartScreen de Windows Defender para Microsoft Edge
<!--1353701-->
A partir de la versión 1806, esta directiva agrega tres opciones para [SmartScreen de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). La directiva ahora incluye los siguientes valores adicionales en la página **Configuración de SmartScreen**:

- **Permitir SmartScreen**: especifica si se permite SmartScreen de Windows Defender. Para obtener más información, consulte la [directiva de explorador AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Los usuarios pueden invalidar los avisos de SmartScreen para los sitios**: especifica si los usuarios pueden invalidar las advertencias del filtro SmartScreen de Windows Defender sobre sitios web potencialmente malintencionados. Para obtener más información, consulte la [directiva de explorador PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Los usuarios pueden invalidar los avisos de SmartScreen para los archivos**: especifica si los usuarios pueden invalidar las advertencias del filtro SmartScreen de Windows Defender sobre la descarga de archivos no comprobados. Para obtener más información, consulte la [directiva de explorador PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Crear el perfil del explorador Microsoft Edge

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento** y seleccione el nodo **Perfiles de explorador de Microsoft Edge**. Haga clic en la opción de la cinta **Crear perfil de Microsoft Edge**.
2. Especifique un **nombre** para la directiva, opcionalmente, escriba una **descripción** y haga clic en **Siguiente**.
3. En la página **Configuración general**, cambie el valor a **Configurado** para incluir la configuración en esta directiva y haga clic en **Siguiente**. La configuración **Establecer el explorador Microsoft Edge como predeterminado** debe estar configurada para continuar.
4. En la versión 1806 y posteriores, configure las opciones en la página **Configuración de SmartScreen** y después haga clic en **Siguiente**. 
5. En la página **Plataformas admitidas**, seleccione las versiones y las arquitecturas de sistema operativo a las que se aplica esta directiva y haga clic en **Siguiente**. 
6. Complete el asistente.



## <a name="deploy-the-policy"></a>Implementar la directiva

1. Seleccione la directiva y haga clic en la opción de cinta de opciones **Implementar**.
2. Haga clic en **Examinar** para seleccionar la recopilación de usuarios o dispositivos en la que desea implementar la directiva. 
3. Seleccione opciones adicionales según sea necesario.  
     a. Genere alertas cuando la directiva no sea compatible.  
     b. Establezca la programación según la cual el cliente evalúa el cumplimiento del dispositivo con esta directiva. 
4. Haga clic en **Aceptar** para crear la implementación.



## <a name="next-steps"></a>Pasos siguientes

Como ocurre con cualquier directiva de configuración de cumplimiento, el cliente corrige la configuración según la programación que especifique. [Supervise el cumplimiento del dispositivo y genere informes al respecto](monitor-compliance-settings.md) en la consola de Configuration Manager.
