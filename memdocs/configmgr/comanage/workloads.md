---
title: Administración conjunta de cargas de trabajo
titleSuffix: Configuration Manager
description: Obtenga información sobre las cargas de trabajo que puede cambiar de Configuration Manager a Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 08261c51170e110dff40ebaaf7699c631ceda7e7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193722"
---
# <a name="co-management-workloads"></a>Administración conjunta de cargas de trabajo

No es necesario que cambie las cargas de trabajo o puede cambiarlas individualmente cuando esté preparado. Configuration Manager sigue administrando todas las demás cargas de trabajo, incluidas las que no cambia a Intune, y todas las demás características de Configuration Manager que no admite la administración conjunta.

Si cambia una carga de trabajo a Intune, pero después cambia de opinión, puede volver a cambiarla a Configuration Manager.

La administración conjunta admite estas cargas de trabajo:

- [Directivas de cumplimiento](#compliance-policies)  

- [Directivas de Windows Update](#windows-update-policies)  

- [Directivas de acceso a recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuración del dispositivo](#device-configuration)  

- [Aplicaciones de Office para hacer clic y ejecutar](#office-click-to-run-apps)  

- [Aplicaciones cliente](#client-apps)  

## <a name="compliance-policies"></a>Directivas de cumplimiento

Las directivas de cumplimiento definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional. A partir de la versión 1910 de Configuration Manager, puede agregar evaluaciones de líneas base de configuración personalizadas como una regla de evaluación de directivas de cumplimiento. Para más información, vea [Inclusión de líneas base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Para más información sobre la característica de Intune, consulte [Directivas de cumplimiento de dispositivos](/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Directivas de Windows Update

Las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas.

Para más información sobre la característica de Intune, consulte [Configuración de directivas de aplazamiento de Windows Update para empresas](/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Directivas de acceso a recursos

Las directivas de acceso a recursos configuran los ajustes de VPN, Wi-Fi, correo electrónico y certificados en los dispositivos.

Para más información sobre la característica de Intune, consulte el artículo sobre cómo [implementar perfiles de acceso a recursos](/intune/device-profiles).

> [!Note]  
> La carga de trabajo del acceso a recursos también forma parte de la configuración del dispositivo. Intune administra estas directivas cuando cambia la carga de trabajo [Configuración del dispositivo](#device-configuration).

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

La carga de trabajo de Endpoint Protection incluye el conjunto de características de protección antimalware de Windows Defender:

- Antimalware de Windows Defender
- Protección de aplicaciones de Windows Defender  
- Firewall de Windows Defender  
- SmartScreen de Windows Defender  
- Cifrado de Windows
- Windows Defender Exploit Guard  
- Control de aplicaciones de Windows Defender  
- Centro de seguridad avanzada de Windows Defender  
- Protección contra amenazas avanzada de Windows Defender (conocido ahora como Protección contra amenazas de Microsoft Defender)

Para más información sobre la característica de Intune, consulte [Endpoint Protection para Microsoft Intune](/intune/endpoint-protection-windows-10).

> [!Note]  
> Al cambiar esta carga de trabajo, las directivas de Configuration Manager permanecen en el dispositivo hasta que las directivas de Intune las sobrescribe. Este comportamiento garantiza que el dispositivo todavía tiene directivas de protección durante la transición.
>
> La carga de trabajo de Endpoint Protection también forma parte de la configuración del dispositivo. El mismo comportamientos e aplica cuando cambia la carga de trabajo [Configuración del dispositivo](#device-configuration).<!-- SCCMDocs.nl-nl issue #4 --> Al cambiar la carga de trabajo de configuración del dispositivo, también incluye directivas para la característica Information Protection de Windows, que no se incluye en la carga de trabajo de Endpoint Protection.<!-- 4184095 -->
>
> La configuración del antivirus de Microsoft Defender que forma parte del tipo de perfil Restricciones de dispositivos para la configuración de dispositivos de Intune no se incluye en el ámbito del control deslizante de Endpoint Protection. Para administrar el antivirus de Microsoft defender para dispositivos administrados conjuntamente con el control deslizante de Endpoint Protection habilitado, use las nuevas directivas de antivirus en **Centro de administración de Microsoft Endpoint Manager** > **Seguridad de los puntos de conexión** > **Antivirus**. El nuevo tipo de directiva tiene opciones nuevas y mejoradas disponibles, y admite todas las opciones de configuración disponibles en el perfil de restricciones de dispositivos. <!--6609171-->
>
> La característica de cifrado de Windows incluye administración de BitLocker. Para obtener más información sobre el comportamiento de esta característica con administración conjunta, vea [Implementación de la administración de BitLocker](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Configuración del dispositivo

<!--1357903-->

La carga de trabajo de configuración de dispositivos incluye la configuración que administra para los dispositivos de la organización. Al cambiar esta carga de trabajo también se mueven las cargas de trabajo **Acceso a los recursos** y **Endpoint Protection**.

Todavía puede implementar la configuración de Configuration Manager en los dispositivos administrados conjuntamente, aunque Intune sea la autoridad de configuración de dispositivos. Esta excepción se podría usar para definir la configuración que necesita la organización, pero que todavía no está disponible en Intune. Especifique esta excepción en una [línea de base de configuración de Configuration Manager](../compliance/deploy-use/create-configuration-baselines.md). Habilite la opción **Aplicar siempre esta línea de base, incluso para clientes administrados conjuntamente** al crear la línea de base. Puede cambiarla más adelante en la pestaña **General** de las propiedades de una línea de base existente.  

Para más información sobre la característica de Intune, consulte [Creación de un perfil de dispositivo en Microsoft Intune](/intune/device-profile-create).  

> [!NOTE]
> Al cambiar la carga de trabajo de configuración del dispositivo, también incluye directivas para la característica Information Protection de Windows, que no se incluye en la carga de trabajo de Endpoint Protection.<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Aplicaciones hacer clic y ejecutar de Office

<!--1357841-->

Esta carga de trabajo administra Aplicaciones de Microsoft 365 en dispositivos administrados conjuntamente.

- Después de mover la carga de trabajo, la aplicación se muestra en el **Portal de empresa** en el dispositivo.  

- Las actualizaciones de Office pueden tardar aproximadamente 24 horas en aparecer en el cliente a menos que se reinicien los dispositivos.  

- Hay una nueva condición global, **¿Las aplicaciones de Office 365 están administradas por Intune en este dispositivo?** Esta condición se agrega de forma predeterminada como requisito a las nuevas aplicaciones de Microsoft 365. Cuando se realiza la transición de esta carga de trabajo, los clientes con administración conjunta no cumplen el requisito en la aplicación. Por tanto, no instalan Microsoft 365 implementado a través de Configuration Manager.  

Para más información sobre la característica de Intune, consulte [Asignación de aplicaciones de Microsoft 365 a dispositivos Windows 10 con Microsoft Intune](/intune/apps-add-office365).

## <a name="client-apps"></a>Aplicaciones cliente

<!--1357892-->

Use Intune para administrar las aplicaciones cliente y los scripts de PowerShell en dispositivos Windows 10 administrados en conjunto. Después de realizar la transición de esta carga de trabajo, las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa. Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software.

Para más información sobre la característica de Intune, consulte [¿Qué es la administración de aplicaciones de Microsoft Intune?](/intune/app-management)

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión 1806 como una [característica de versión preliminar](../core/servers/manage/pre-release-features.md). A partir de la versión 2002, ya no se encuentra en versión preliminar.  
>
> Esta característica puede aparecer en la lista de características como **Aplicaciones móviles para dispositivos administrados conjuntamente**.<!-- 5849669 -->

A partir de la versión 1910, cuando se habilita la caché de conexión de Microsoft en los puntos de distribución de Configuration Manager, estos pueden suministrar aplicaciones Win32 de Microsoft Intune a los clientes administrados conjuntamente. Para más información, vea [Caché con conexión de Microsoft en Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Diagrama para cargas de trabajo de aplicaciones

:::image type="content" source="media/co-management-apps.svg" alt-text="Diagrama de cargas de trabajo de aplicaciones de administración conjunta" lightbox="media/co-management-apps.svg":::

> [!TIP]
> A partir de la versión 2006, puede configurar el Portal de empresa para mostrar también aplicaciones de Configuration Manager. Si cambia esta experiencia del portal de aplicaciones, cambiará los comportamientos descritos en el diagrama anterior. Para más información, consulte [Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente](company-portal.md).<!--CMADO-3601237,INADO-4297660-->

## <a name="known-issues"></a>Problemas conocidos

Cuando la carga de trabajo de Endpoint Protection se mueve a Intune, el cliente puede seguir adherido a las directivas establecidas por Configuration Manager y Microsoft Defender. <!--5024559-->

Para solucionar este problema, aplique CleanUpPolicy.xml con ConfigSecurityPolicy.exe después de que el cliente haya recibido las directivas de Intune mediante los pasos siguientes:

1. Copie y guarde el texto siguiente como `CleanUpPolicy.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```

1. Abra un símbolo del sistema con privilegios elevados en `ConfigSecurityPolicy.exe`. Normalmente, este archivo ejecutable está en uno de los siguientes directorios:
   - C:\Archivos de programa\Windows Defender
   - C:\Archivos de Programa\Microsoft Security Client

1. En el símbolo del sistema, pase el archivo XML para limpiar la directiva. Por ejemplo, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Pasos siguientes

[How to switch workloads](how-to-switch-workloads.md) (Cambio de las cargas de trabajo)