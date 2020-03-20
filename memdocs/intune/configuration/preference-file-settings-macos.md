---
title: 'Adición de una configuración de archivo de preferencia para dispositivos macOS en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Agregue un archivo xml o plist que incluya información clave sobre la aplicación. Use un perfil de configuración de dispositivo de archivo de preferencias para cambiar la información clave del archivo de lista de propiedades y asígnelo a sus dispositivos macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360761"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Adición de un archivo de lista de propiedades a dispositivos macOS con Microsoft Intune

Con Microsoft Intune, puede agregar un archivo de lista de propiedades (.plist) para dispositivos macOS o aplicaciones de dispositivos macOS.

Esta característica se aplica a:

- dispositivos macOS con 10.7 y versiones más recientes

Los archivos de lista de propiedades suelen incluir información sobre las aplicaciones macOS. Para obtener más información, vea los sitios web de Apple [Información sobre los archivos de lista de propiedades](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) y [Ajustes de carga personalizada](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

En este artículo se enumeran y describen los diferentes valores de configuración de los archivos de lista de propiedades que se pueden agregar a los dispositivos macOS. Como parte de su solución de administración de dispositivos móviles (MDM), use estas opciones de configuración para agregar el identificador del lote de aplicaciones (`com.company.application`) y agregue su archivo .plist.

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos macOS.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree el perfil](device-profile-create.md).

## <a name="what-you-need-to-know"></a>Aspectos que debe saber

- Esta configuración no se valida. Asegúrese de probar los cambios antes de asignar el perfil a los dispositivos.
- Si no tiene claro cómo especificar una clave de aplicación, cambie la configuración en la aplicación. Después, revise el archivo de preferencias de la aplicación mediante [Xcode](https://developer.apple.com/xcode/) para ver cómo se ha configurado. Apple recomienda quitar la configuración no administrable con Xcode antes de importar el archivo.
- Solo algunas aplicaciones funcionan con preferencias administradas, y es posible que no le permitan administrar toda la configuración.
- Asegúrese de cargar los archivos de lista de propiedades que tengan como destino la configuración del canal del dispositivo, no la configuración del canal del usuario. Los archivos de lista de propiedades tienen como destino todo el dispositivo.

## <a name="preference-file"></a>Archivo de preferencia

- **Nombre de dominio de preferencia**: los archivos de lista de propiedades se suelen usar en exploradores web (Microsoft Edge), [Advanced Threat Protection de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) y aplicaciones personalizadas. Al crear un dominio de preferencia, también se crea un identificador de agrupación. Escriba el identificador de agrupación, como `com.company.application`. Por ejemplo, escriba `com.Contoso.applicationName`, `com.Microsoft.Edge` o `com.microsoft.wdav`.
- **Archivo de la lista de propiedades**: seleccione el archivo de lista de propiedades asociado a la aplicación. Asegúrese de que es un archivo `.plist` o `.xml`. Por ejemplo, cargue un archivo `YourApp-Manifest.plist` o `YourApp-Manifest.xml`.
- **Contenido del archivo**: La información clave se muestra en el archivo de lista de propiedades. Si necesita cambiar la información clave, abra el archivo de lista en otro editor y, después, vuelva a cargar el archivo en Intune.

Asegúrese de que el archivo tiene el formato correcto. El archivo solo debe tener pares clave-valor, y no debe incluirse entre etiquetas `<dict>`, `<plist>` ni `<xml>`. Por ejemplo, su archivo de lista de propiedades debe ser similar al siguiente:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Seleccione **Aceptar** > **Crear** para guardar los cambios. El perfil se crea y se muestra en la lista de perfiles.

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero todavía no hace nada. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Para obtener más información sobre los archivos de preferencia de Microsoft Edge, consulte [Configurar las opciones de directiva de Microsoft Edge en macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
