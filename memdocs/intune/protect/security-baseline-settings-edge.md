---
title: Configuración de líneas de base de seguridad de Intune para Microsoft Edge
titleSuffix: Microsoft Intune
description: Configuración de la línea de base de seguridad compatible con Intune para administrar el explorador Microsoft Edge
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6108fc56b978c57bfc70b2bce9911f7901a01a3e
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551735"
---
# <a name="microsoft-edge-baseline-settings-for-intune"></a>Configuración de línea de base de Microsoft Edge para Intune

Vea la configuración de línea de base del explorador web Microsoft Edge admitida por Microsoft Intune. Los valores predeterminados de línea de base de Microsoft Edge representan la configuración recomendada para exploradores Microsoft Edge y podrían no coincidir con los valores predeterminados para otras líneas de base de seguridad.

> [!NOTE]
> La línea de base de Microsoft Edge está en versión preliminar pública. 

## <a name="microsoft-edge"></a>Microsoft Edge

- **Impedir la omisión de los avisos de SmartScreen de Windows Defender para sitios**  
  **Valor predeterminado**: Habilitado  
  CSP de Microsoft Edge: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Esta configuración de directiva le permite decidir si los usuarios pueden invalidar las advertencias de SmartScreen de Microsoft Defender sobre sitios web potencialmente malintencionados. 
  - Si habilita esta opción, los usuarios no podrán omitir las advertencias de SmartScreen de Microsoft Defender y no podrán continuar al sitio. 
  - Si deshabilita o no configura esta opción, los usuarios podrán omitir las advertencias de SmartScreen de Microsoft Defender y continuar al sitio.

- **Versión mínima de SSL habilitada**  
  **Valor predeterminado**: Habilitado  

  Establecer una versión mínima admitida de SSL. Si establece esta directiva en *No configurada*, Microsoft Edge usa una versión mínima predeterminada de *TLS 1.0*. Cuando se establece en *Habilitada*, puede seleccionar una versión mínima de los siguientes valores:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Versión mínima de SSL habilitada**  
    **Valor predeterminado**: TLS 1.2

- **Impedir la omisión de las advertencias de SmartScreen de Microsoft Defender sobre descargas**  
  **Valor predeterminado**: Habilitado  
  CSP de Microsoft Edge: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Esta directiva le permite determinar si los usuarios pueden invalidar las advertencias de SmartScreen de Microsoft Defender sobre las descargas no comprobadas.
  - Si habilita esta directiva, los usuarios de su organización no podrán omitir las advertencias de SmartScreen de Microsoft Defender y se les impedirá que completen las descargas no comprobadas.
  - Si deshabilita o no configura esta directiva, los usuarios podrán omitir las advertencias de SmartScreen de Microsoft Defender y completar descargas no verificadas.

- **Permitir a los usuarios continuar desde la página de advertencia de SSL**  
  **Valor predeterminado**: Deshabilitado  
  CSP de Microsoft Edge: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge muestra una página de advertencia cuando los usuarios visitan sitios que tienen errores de SSL. Si establece esta directiva en *Habilitada* o *No configurada*, los usuarios pueden hacer clic en estas páginas de advertencia. Cuando esta directiva está *Deshabilitada*, se impide que los usuarios hagan clic en cualquier página de advertencia. 

- **Configuración predeterminada de Adobe Flash**  
  **Valor predeterminado**: Habilitado  
  CSP de Microsoft Edge: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) y [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Determina si los sitios web que no están incluidos en "PluginsAllowedForUrls" o "PluginsBlockedForUrls" pueden ejecutar automáticamente el complemento de Adobe Flash. 

  - Seleccione "BlockPlugins" para bloquear Adobe Flash en todos los sitios.
  - Seleccione "ClickToPlay" para permitir la ejecución de Adobe Flash, pero solicite al usuario que haga clic en el marcador de posición para iniciarlo.
  
   En cualquier caso, las directivas "PluginsAllowedForUrls" y "PluginsBlockedForUrls" tienen prioridad sobre "DefaultPluginsSetting". La reproducción automática solo se permite para los dominios enumerados explícitamente en la directiva "PluginsAllowedForUrls". 
   Si quiere habilitar la reproducción automática para todos los sitios, considere la posibilidad de agregar http://* y https://* a esta lista. 
   
   - Si establece esta directiva en *No configurada*, el usuario puede cambiar esta configuración manualmente. * 2: Bloquear el complemento de Adobe Flash; * 3: Haga clic para reproducir la opción "1" anterior establecida en permitir todo, pero ahora esta funcionalidad solo la controla la directiva "PluginsAllowedForUrls". Las directivas existentes con "1" funcionarán en el modo Hacer clic para reproducir.  
 
  - **Configuración predeterminada de Adobe Flash**  
    **Valor predeterminado**: bloquear el complemento de Adobe Flash

- **Habilitar el aislamiento de sitio para cada sitio**  
  **Valor predeterminado**: Habilitado  

  La directiva "SitePerProcess" se puede usar para impedir que los usuarios opten por el comportamiento predeterminado de aislar todos los sitios. También puede usar la directiva IsolateOrigins para aislar orígenes adicionales más precisos.

  - Cuando esta directiva se establece en *Habilitada*, los usuarios no pueden rechazar el comportamiento predeterminado, donde cada sitio se ejecuta en su propio proceso. 
  - Si usa *Deshabilitada* o *No configurada*, un usuario puede rechazar el aislamiento del sitio. (Por ejemplo, mediante el uso de la entrada "Deshabilitar aislamiento de sitio" en edge://flags). El hecho de deshabilitar la directiva o no configurarla no desactiva el aislamiento del sitio.

- **Esquemas de autenticación admitidos**  
  **Valor predeterminado**: Habilitado  

  Especifica los esquemas de autenticación HTTP que se admiten. Puede configurar la directiva con estos valores: "basic", "digest", "ntlm" y "negotiate". Separe varios valores con comas. Si no configura esta directiva, se usarán los cuatro esquemas.
 
  - **Esquemas de autenticación admitidos**  
    Seleccione entre las siguientes opciones: 
    - Básico
    - Digest
    - NTLM *(seleccionado de forma predeterminada)*
    - Negotiate *(seleccionada de forma predeterminada)*

- **Habilitar el guardado de contraseñas en el administrador de contraseñas**  
  **Valor predeterminado**: Deshabilitado  
  CSP de Microsoft Edge: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Habilite Microsoft Edge para guardar las contraseñas de usuario. 
  - Si habilita esta directiva, los usuarios pueden guardar sus contraseñas en Microsoft Edge. La próxima vez que visiten el sitio, Microsoft Edge introducirá la contraseña automáticamente. 
  - Si deshabilita esta directiva, los usuarios no podrán guardar contraseñas nuevas, pero podrán seguir usando contraseñas guardadas anteriormente. 
  
  Al establecer esta directiva en *Habilitada* o *Deshabilitada*, los usuarios no pueden cambiar o invalidar esta directiva en Microsoft Edge. 
  
  Si la establece en *No configurada*, los usuarios podrán guardar las contraseñas, así como desactivar esta característica.

- **Control sobre qué extensiones no se pueden instalar**  
  **Valor predeterminado**: Habilitado  

  Enumere las extensiones específicas que los usuarios no pueden instalar en Microsoft Edge. Cuando se implementa esta directiva, se deshabilitan las extensiones de esta lista que se instalaron previamente y el usuario no podrá habilitarlas. Si quita un elemento de la lista de extensiones bloqueadas, esa extensión se vuelve a habilitar automáticamente en cualquier lugar en el que se haya instalado previamente.
  
  Use **\*** para bloquear todas las extensiones que no aparezcan explícitamente en la lista de permitidas. Si esta directiva se establece en *No configurada*, los usuarios podrán instalar cualquier extensión en Microsoft Edge. 
  
  Valor de ejemplo: extension_id1 extension_id2.  
  <br>
  - **Identificadores de las extensiones que se debería impedir instalar al usuario (o * para todas)**  
    Seleccione **Agregar** y especifique extensiones adicionales. **\*** está seleccionado de forma predeterminada.

- **Configuración de SmartScreen de Microsoft Defender**  
  **Valor predeterminado**: Habilitado  
  CSP de Microsoft Edge: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Esta configuración de directiva le permite configurar si se activa SmartScreen de Microsoft Defender. SmartScreen de Microsoft Defender proporciona mensajes de advertencia para ayudar a proteger a los usuarios de software malintencionado y posibles estafas de suplantación de identidad. 
  
  - De forma predeterminada, SmartScreen de Microsoft Defender está activado. Si habilita esta configuración, SmartScreen de Microsoft Defender estará activado y los usuarios no podrán desactivarlo.
  - Si deshabilita esta configuración, SmartScreen de Microsoft Defender estará desactivado y los usuarios no podrán activarlo. 
  - Si se establece en *No configurada*, los usuarios pueden elegir si quieren usar SmartScreen de Microsoft Defender. 
  
  Esta directiva solo está disponible en las instancias de Windows unidas a un dominio de Microsoft Active Directory o en instancias de Windows 10 Pro o Enterprise que inscritas para la administración de dispositivos.

- **Permitir hosts de mensajería nativa en el nivel de usuario (se instala sin permisos de administrador)**  
  **Valor predeterminado**: Deshabilitado  

  Habilita la instalación de nivel de usuario de hosts de mensajería nativa. 
  - Si deshabilita esta directiva, Microsoft Edge solo usará los hosts de mensajería nativa instalados en el nivel del sistema. De forma predeterminada, si no configura esta directiva, Microsoft Edge permitirá el uso de hosts de mensajería nativa de nivel de usuario.

## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre las líneas de base de seguridad](security-baselines.md)
- [Evitación de conflictos](security-baselines.md#avoid-conflicts)
- [Solución de problemas de directivas y perfiles en Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
