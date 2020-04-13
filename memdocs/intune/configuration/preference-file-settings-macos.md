---
title: 'Adición de una configuración de archivo de preferencia para dispositivos macOS en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Agregue un archivo xml o plist que incluya información clave sobre la aplicación. Use un perfil de configuración de dispositivo de archivo de preferencias para cambiar la información clave del archivo de lista de propiedades y asígnelo a sus dispositivos macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9cb8cea30b53c5619580b289f73529668d71e909
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551505"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Adición de un archivo de lista de propiedades a dispositivos macOS con Microsoft Intune

Con Microsoft Intune, puede agregar un archivo de lista de propiedades (.plist) para dispositivos macOS o aplicaciones de dispositivos macOS.

Esta característica se aplica a:

- macOS 10.7 y versiones más recientes

Los archivos de lista de propiedades incluyen información sobre las aplicaciones macOS. Para obtener más información, vea los sitios web de Apple [Información sobre los archivos de lista de propiedades](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) y [Ajustes de carga personalizada](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

En este artículo se enumeran y describen los diferentes valores de configuración de los archivos de lista de propiedades que se pueden agregar a los dispositivos macOS. Como parte de su solución de administración de dispositivos móviles (MDM), use estas opciones de configuración para agregar el identificador del lote de aplicaciones (`com.company.application`) y agregue el archivo .plist de la aplicación.

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos macOS.

## <a name="what-you-need-to-know"></a>Aspectos que debe saber

- Esta configuración no se valida. Asegúrese de probar los cambios antes de asignar el perfil a los dispositivos.
- Si no tiene claro cómo especificar una clave de aplicación, cambie la configuración en la aplicación. Después, revise el archivo de preferencias de la aplicación mediante [Xcode](https://developer.apple.com/xcode/) para ver cómo se ha configurado. Apple recomienda quitar la configuración no administrable con Xcode antes de importar el archivo.
- Solo algunas aplicaciones funcionan con preferencias administradas, y es posible que no le permitan administrar toda la configuración.
- Asegúrese de cargar los archivos de lista de propiedades que tengan como destino la configuración del canal del dispositivo, no la configuración del canal del usuario. Los archivos de lista de propiedades tienen como destino todo el dispositivo.

> [!NOTE]
> La interfaz de usuario de Intune se está actualizando a una experiencia de pantalla completa y puede tardar varias semanas. Hasta que el inquilino reciba esta actualización, tendrá un flujo de trabajo ligeramente diferente cuando cree o edite la configuración que se describe en este artículo.

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione **macOS**.
    - **Perfil**: Seleccione **Archivo de preferencias**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **macOS: Agregue un archivo de preferencias que configure ATP de Microsoft Defender en los dispositivos**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En **Opciones de configuración**, establezca los parámetros:

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

8. Seleccione **Siguiente**.
9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione los usuarios o grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero todavía no hace nada. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Para obtener más información sobre los archivos de preferencia de Microsoft Edge, consulte [Configurar las opciones de directiva de Microsoft Edge en macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
