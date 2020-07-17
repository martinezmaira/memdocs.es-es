---
title: Configuración de las opciones de Microsoft Edge
titleSuffix: Configuration Manager
description: Configuración de las opciones del explorador web Microsoft Edge (versión heredada) en los clientes de Windows 10
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 57eb9bbaed39ec463afc00d12202a9829729a086
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240553"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Configuración de opciones de Microsoft Edge (versión heredada) en Configuration Manager

> [!IMPORTANT]
> Si usa la versión 77 de Microsoft Edge o una versión posterior e intenta abrir el panel de configuración, escriba `edge://settings/profiles` en la barra de direcciones del explorador en lugar de buscar. Para más información, consulte [Conocer Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> Este artículo está dirigido a profesionales de TI para que administren la configuración de Microsoft Edge (versión heredada) con Microsoft Endpoint Configuration Manager.

*Se aplica a: Configuration Manager (rama actual)*

<!-- 1357310 -->
Para los clientes que usan el explorador web [Microsoft Edge (versión heredada)](https://docs.microsoft.com/microsoft-edge/deploy/) en los clientes de Windows 10, cree una directiva de cumplimiento de Configuration Manager para configurar las opciones del explorador.

Esta directiva solo se aplica a los clientes en la versión 1703 o posteriores de Windows 10 y a la versión 45 y anteriores de Microsoft Edge (versión heredada). <!--511552-->

Para más información sobre cómo administrar la versión 77 o versiones posteriores de Microsoft Edge con Configuration Manager, consulte [Implementación de Microsoft Edge, versión 77 y posteriores](../../apps/deploy-use/deploy-edge.md). Para más información sobre cómo configurar directivas para Microsoft Edge, versión 77 o posteriores, consulte [Microsoft Edge: directivas](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies).

## <a name="policy-settings"></a>Configuración de la directiva

Actualmente, esta directiva incluye las siguientes opciones:

- **Set Microsoft Edge browser as default** (Establecer el explorador Microsoft Edge como predeterminado): configura los parámetros de la aplicación predeterminada de Windows 10 en cuanto a explorador web para que sea Microsoft Edge.

- **Permitir función desplegable de la barra de direcciones**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [AllowAddressBarDropdown browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown) (Directiva de explorador AllowAddressBarDropdown).

- **Permitir sincronizar favoritos entre exploradores de Microsoft**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [SyncFavoritesBetweenIEAndMicrosoftEdge browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge) (Directiva de explorador SyncFavoritesBetweenIEAndMicrosoftEdge).

- **Permitir borrar datos de exploración al salir**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [ClearBrowsingDataOnExit browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit) (Directiva de explorador ClearBrowsingDataOnExit).

- **Permitir encabezados Do Not Track**: para obtener más información, vea [AllowDoNotTrack browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack) (Directiva de explorador AllowDoNotTrack).

- **Permitir autorrelleno**: para obtener más información, vea [AllowAutofill browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill) (Directiva de explorador AllowAutofill).

- **Permitir cookies**: para obtener más información, vea [AllowCookies browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies). (Directiva de explorador AllowCookies).

- **Permitir bloqueador de elementos emergentes**: para obtener más información, vea [AllowPopups browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups). (Directiva de explorador AllowPopups).

- **Permitir sugerencias de búsqueda en la barra de direcciones**: para obtener más información, vea [AllowSearchSuggestionsinAddressBar browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar) (Directiva de explorador AllowSearchSuggestionsinAddressBar).

- **Permitir el envío de tráfico de la intranet a Internet Explorer**: para obtener más información, vea [SendIntranetTraffictoInternetExplorer browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer) (Directiva de explorador SendIntranetTraffictoInternetExplorer).

- **Permitir administrador de contraseñas**: para obtener más información, vea [AllowPasswordManager browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager) (Directiva de explorador AllowPasswordManager).

- **Permitir Herramientas de desarrollo**: para obtener más información, vea [AllowDeveloperTools browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools) (Directiva de explorador AllowDeveloperTools).

- **Permitir extensiones**: para obtener más información, vea [AllowExtensions browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions) (Directiva de explorador AllowExtensions).

> [!TIP]
> Para más información sobre cómo usar una directiva de grupo para configurar estas y otras opciones, consulte el artículo sobre las [directivas de grupo de Microsoft Edge (versión heredada)](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Configuración de SmartScreen de Windows Defender para Microsoft Edge (versión heredada)
<!--1353701-->
Esta directiva agrega tres opciones para [SmartScreen de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). La directiva ahora incluye los siguientes valores adicionales en la página **Configuración de SmartScreen**:

- **Permitir SmartScreen**: especifica si se permite SmartScreen de Windows Defender. Para obtener más información, consulte la [directiva de explorador AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Los usuarios pueden invalidar los avisos de SmartScreen para los sitios**: especifica si los usuarios pueden invalidar las advertencias del filtro SmartScreen de Windows Defender sobre sitios web potencialmente malintencionados. Para obtener más información, consulte la [directiva de explorador PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).

- **Los usuarios pueden invalidar los avisos de SmartScreen para los archivos**: especifica si los usuarios pueden invalidar las advertencias del filtro SmartScreen de Windows Defender sobre la descarga de archivos no comprobados. Para obtener más información, consulte la [directiva de explorador PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).

## <a name="create-the-browser-profile"></a>Creación del perfil del explorador

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento** y seleccione el nodo **Perfiles de explorador de Microsoft Edge**. En la cinta de opciones, seleccione **Crear perfil de Microsoft Edge**.

2. Especifique un **nombre** para la directiva y, si quiere, escriba una **descripción**, y seleccione **Siguiente**.

3. En la página **Configuración general**, cambie el valor a **Configurado** para incluir la configuración en esta directiva. Para continuar con el asistente, asegúrese de configurar la opción **Establecer el explorador Microsoft Edge como predeterminado**.

4. Configure las opciones en la página **Configuración de SmartScreen**.

5. En la página **Plataformas admitidas**, seleccione las versiones y las arquitecturas de sistema operativo a las que se aplica esta directiva.

6. Complete el asistente.

## <a name="deploy-the-policy"></a>Implementar la directiva

1. Seleccione la directiva y, en la cinta de opciones, seleccione **Implementar**.

2. Haga clic en **Examinar** para seleccionar la recopilación de usuarios o dispositivos en la que quiere implementar la directiva.

3. Seleccione opciones adicionales según sea necesario:

    1. Genere alertas cuando la directiva no sea compatible.

    2. Establezca la programación según la cual el cliente evalúa el cumplimiento del dispositivo con esta directiva.

4. Seleccione **Aceptar** para crear la implementación.

## <a name="next-steps"></a>Pasos siguientes

Como ocurre con cualquier directiva de configuración de cumplimiento, el cliente corrige la configuración según la programación que especifique. [Supervise el cumplimiento del dispositivo y genere informes al respecto](monitor-compliance-settings.md) en la consola de Configuration Manager.
