---
title: Uso de registros de StageNow en dispositivos Android Zebra en Microsoft Intune - Azure | Microsoft Docs
description: Conozca algunos problemas y soluciones comunes derivados de usar StageNow en dispositivos Android con Microsoft Intune. Vea también cómo obtener registros, y consulte algunos ejemplos para saber leer registros en busca de operaciones correctas o con errores.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8cc44cb614154df1a128ee1f1708a3259f88169
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910050"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Solución de problemas y detección de posibles problemas en dispositivos Android Zebra en Microsoft Intune



En Microsoft Intune se pueden usar [extensiones de movilidad (MX) de Zebra para administrar dispositivos Android Zebra](android-zebra-mx-overview.md). Cuando se usan dispositivos Zebra, se crean perfiles en StageNow para administrar la configuración y cargarla en Intune. Intune usa la aplicación StageNow para aplicar la configuración en los dispositivos. La aplicación StageNow también crea un archivo de registro detallado en el dispositivo que se usa para solucionar problemas.

Esta característica se aplica a:

- Android

Por ejemplo, se puede crear un perfil en StageNow para configurar un dispositivo. Al crear el perfil de StageNow, el último paso genera un archivo para probar el perfil. Este archivo se usa con la aplicación StageNow en el dispositivo.

En otro ejemplo, se puede crear un perfil en StageNow y probarlo. En Intune, hay que agregar el perfil de StageNow y, luego, asignarlo a los dispositivos Zebra. Al comprobar el estado del perfil asignado, el perfil muestra un estado de alto nivel.

En ambos casos, se pueden obtener más detalles del archivo de registro de StageNow, que se guarda en el dispositivo cada vez que se aplica un perfil de StageNow.

Algunos problemas no guardan relación con el contenido del perfil de StageNow y no aparecen reflejados en los registros.

En este artículo se describe cómo leer los registros de StageNow, y se incluyen otros posibles problemas con dispositivos Zebra que puede que no aparezcan reflejados en los registros.

En [Uso y administración de dispositivos Zebra con extensiones de movilidad en Intune](android-zebra-mx-overview.md) encontrará más información sobre esta característica.

## <a name="get-the-logs"></a>Obtención de los registros

### <a name="use-the-stagenow-app-on-the-device"></a>Uso de la aplicación StageNow en el dispositivo
Al probar un perfil directamente con StageNow en el equipo, en lugar de usar [Intune para implementar el perfil](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow), la aplicación StageNow del dispositivo guarda los registros generados a raíz de la prueba. Para obtener el archivo de registro, use la opción **Más (...)** en la aplicación StageNow en el dispositivo.

### <a name="get-logs-using-android-debug-bridge"></a>Obtención de registros mediante Android Debug Bridge
Para obtener registros después de que el perfil se haya implementado con Intune, conecte el dispositivo a un equipo con [Android Debug Bridge (ADB)](https://developer.android.com/studio/command-line/adb) (se abre el sitio web de Android).

En el dispositivo, los registros se guardan en `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`.

### <a name="get-logs-from-email"></a>Obtención de registros de correo electrónico
Para obtener registros después de que el perfil se haya implementado con Intune, los usuarios finales pueden enviarle los registros por correo electrónico con una aplicación de correo electrónico en el dispositivo. En el dispositivo Zebra, abra la aplicación Portal de empresa y [envíe los registros](../user-help/send-logs-to-your-it-admin-by-email-android.md). El uso de la característica de envío de registros también crea un identificador de incidente de PowerLift, al que puede hacer referencia si se pone en contacto con el soporte técnico de Microsoft.

## <a name="read-the-logs"></a>Lectura de los registros

Al examinar los registros, hay un error cada vez que aparece la etiqueta `<characteristic-error>`. Los detalles del error se escriben en la etiqueta `<parm-error>` > propiedad `desc`.

## <a name="error-types"></a>Tipos de error

Los dispositivos Zebra incluyen distintos niveles de informes de error:

- El CSP no es compatible con el dispositivo. Por ejemplo, el dispositivo no es un dispositivo de telefonía móvil y carece de un administrador de telefonía móvil.
- La versión de MX o OSX no coincide. Cada CSP tiene una versión. Para consultar una matriz de compatibilidad completa, vea la [documentación de Zebra](http://techdocs.zebra.com/mx/) (se abre el sitio web de Zebra).
- El dispositivo indica otro problema o error.

## <a name="examples"></a>Ejemplos

Tenemos el siguiente perfil de entrada:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

En el registro, el código XML es idéntico a la entrada. Esta salida coincidente significa que el perfil se aplicó correctamente en el dispositivo sin errores:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

En otro ejemplo, tenemos la siguiente entrada:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

El registro muestra un error, ya que contiene una etiqueta `<characteristic-error>`. En este escenario, el perfil intentó instalar un paquete de Android (APK) que no existe en la ruta de acceso especificada:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Otros posibles problemas de los dispositivos Zebra

En esta sección se incluyen otros posibles problemas que pueden aparecer al usar dispositivos Zebra con el administrador de dispositivos. Estos problemas no aparecen en los registros de StageNow.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView no está actualizado

Cuando se inicia sesión en dispositivos más antiguos con la aplicación Portal de empresa, es posible que los usuarios vean un mensaje que les informa de que el componente WebView del sistema no está actualizado y debe actualizarse. Si el dispositivo tiene Google Play instalado, conéctelo a Internet y compruebe si hay actualizaciones. Si el dispositivo no tiene Google Play instalado, obtenga la versión actualizada del componente y aplíquelo en los dispositivos. O bien, actualice al sistema operativo del dispositivo más reciente publicado por Zebra.

### <a name="management-actions-take-a-long-time"></a>Las acciones de administración tardan mucho tiempo

Si los servicios de Google Play no están disponibles, algunas tareas tardan hasta 8 horas en completarse. Un buen recurso para esto puede ser [Limitaciones de la aplicación Portal de empresa de Intune en Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (se abre otro sitio web de Microsoft).

### <a name="device-spoofing-suspected-shows-in-intune"></a>Intune informa de una suplantación de dispositivo sospechosa

Este error significa que Intune sospecha que un dispositivo Android que no es de Zebra está indicando su modelo y fabricante como de Zebra.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>La versión de la aplicación Portal de empresa es anterior a la versión mínima requerida

Intune puede actualizar la versión mínima necesaria de la aplicación Portal de empresa. Si Google Play no está instalado en el dispositivo, la aplicación Portal de empresa no se actualiza automáticamente. Si la versión mínima requerida es más reciente que la versión instalada, la aplicación Portal de empresa dejará de funcionar. Actualice a la aplicación Portal de empresa más reciente mediante la [transferencia en dispositivos Zebra](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Pasos siguientes

[Paneles de discusión sobre Zebra](https://developer.zebra.com/community/home/discussions) (se abre el sitio web de Zebra)

[Usar y administrar dispositivos Zebra con extensiones de movilidad de Zebra en Intune](android-zebra-mx-overview.md)