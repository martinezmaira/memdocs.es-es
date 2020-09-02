---
title: Agregar y asignar aplicaciones MTD a Microsoft Intune
titleSuffix: Microsoft Intune
description: Use Intune para agregar aplicaciones de Mobile Threat Defense (MTD), la aplicación de Microsoft Authenticator y la directiva de configuración de iOS en Azure Portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b487b9f921e40df8730fab235a2ec2c0d3f0f788
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910866"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Agregar y asignar aplicaciones de Mobile Threat Defense (MTD) con Intune

Puede usar Intune para agregar e implementar las aplicaciones de Mobile Threat Defense (MTD) para que los usuarios finales puedan recibir notificaciones al identificar una amenaza en sus dispositivos móviles y para recibir orientación con el objetivo de solucionarlas.

> [!NOTE]
> Este tema se aplica a todos los asociados de Mobile Threat Defense.

## <a name="before-you-begin"></a>Antes de comenzar

Lleve a cabo los pasos siguientes en Intune. Asegúrese de conocer los siguientes procesos:

- [Agregar una aplicación en Intune](../apps/apps-add.md)
- [Descargar una directiva de configuración de aplicación de iOS en Intune](../apps/app-configuration-policies-use-ios.md)
- [Asignar una aplicación con Intune](../apps/apps-deploy.md).

> [!TIP]
> El Portal de empresa de Intune funciona como el agente de los dispositivos Android, de manera que los usuarios puedan comprobar sus identidades con Azure AD.

## <a name="configure-microsoft-authenticator-for-ios"></a>Configuración de Microsoft Authenticator para iOS

Para los dispositivos iOS, necesita [Microsoft Authenticator](/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) de manera que los usuarios puedan comprobar sus identidades con Azure AD. Además, necesita una directiva de configuración de aplicaciones para iOS que establezca la aplicación iOS de MTD para usarla con Intune.

Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use esta [dirección URL de la tienda de aplicaciones de Microsoft Authenticator](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) al configurar la **información de la aplicación**.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>Configuración de aplicaciones de MTD con una directiva de configuración de aplicaciones

Para simplificar la incorporación de usuarios, las aplicaciones de Mobile Threat Defense en dispositivos administrados por MDM usan la configuración de la aplicación. En el caso de los dispositivos no inscritos, la configuración de aplicaciones basada en MDM no está disponible, por lo que debe consultar [Incorporación de aplicaciones de Mobile Threat Defense a dispositivos no inscritos](../protect/mtd-add-apps-unenrolled-devices.md).

### <a name="lookout-for-work-app-configuration-policy"></a>Directiva de configuración de aplicaciones Lookout for Work

Cree la directiva de configuración de aplicaciones para iOS como se describe en el artículo [Usar la directiva de configuración de aplicaciones para iOS](../apps/app-configuration-policies-use-ios.md).

### <a name="sep-mobile-app-configuration-policy"></a>Directiva de configuración de aplicaciones de SEP Mobile

Use la misma cuenta de Azure AD configurada anteriormente en la [consola de administración de Symantec Endpoint Protection](https://aad.skycure.com), que debe ser la misma que se usó para iniciar sesión en Intune.

- **Descargue** el archivo de la directiva de configuración de la aplicación de iOS:
  - Vaya a la [consola de administración de Symantec Endpoint Protection](https://aad.skycure.com) e inicie sesión con sus credenciales de administrador.

  - Vaya a **Settings** (Configuración) y, en **Integrations** (Integraciones), elija **Intune**. Elija **EMM Integration Selection** (Selección de la integración de EMM). Elija **Microsoft** y guarde la selección.

  - Haga clic en el vínculo **Integration setup files** (Archivos de configuración de la integración) y guarde el archivo \*.zip generado. El archivo .zip contiene el archivo * **.plist**, que se usará para crear la directiva de configuración de aplicaciones iOS en Intune.

  - Para agregar la directiva de configuración de aplicaciones de SEP Mobile, consulte las instrucciones para [usar directivas de configuración de aplicaciones de Microsoft Intune para iOS](../apps/app-configuration-policies-use-ios.md).

    - Para **Formato de opciones de configuración**, seleccione **Especificar datos XML**, copie el contenido del archivo * **.plist** y péguelo en el cuerpo de la directiva de configuración.

> [!NOTE]
> Si no puede recuperar los archivos, póngase en contacto con el [soporte técnico de Symantec Endpoint Protection Mobile Enterprise](https://support.symantec.com/en_US/contact-support.html).

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Directiva de configuración de aplicaciones SandBlast Mobile de Check Point

Consulte las instrucciones para [usar las directivas de configuración de aplicaciones de Microsoft Intune para iOS](../apps/app-configuration-policies-use-ios.md) con el fin de agregar la directiva de configuración de aplicaciones de SandBlast Mobile de Check Point para iOS.

- Para **Formato de opciones de configuración**, seleccione **Especificar datos XML**, copie el contenido siguiente y péguelo en el cuerpo de la directiva de configuración.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Directiva de configuración de aplicaciones de Zimperium

Vea las instrucciones para [usar las directivas de configuración de aplicaciones de Microsoft Intune para iOS](../apps/app-configuration-policies-use-ios.md) para agregar la directiva de configuración de aplicaciones de Zimperium para iOS.

- Para **Formato de opciones de configuración**, seleccione **Especificar datos XML**, copie el contenido siguiente y péguelo en el cuerpo de la directiva de configuración.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Directiva de configuración de aplicaciones de Pradeo

Pradeo no admite la directiva de configuración de aplicaciones en iOS/iPadOS.  En su lugar, para configurar una aplicación, trabaje con Pradeo para implementar archivos IPA o APK personalizados que estén preconfigurados con la configuración que quiera.

### <a name="better-mobile-app-configuration-policy"></a>Directiva de configuración de aplicaciones de Better Mobile

Para agregar la directiva de configuración de aplicaciones de Better Mobile, consulte las instrucciones para [usar directivas de configuración de aplicaciones de Microsoft Intune para iOS](../apps/app-configuration-policies-use-ios.md).

- Para **Formato de opciones de configuración**, seleccione **Especificar datos XML**, copie el contenido siguiente y péguelo en el cuerpo de la directiva de configuración. Reemplace la dirección URL `https://client.bmobi.net` por la dirección URL de consola apropiada.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Directiva de configuración de aplicaciones de Sophos Mobile

Cree la directiva de configuración de aplicaciones para iOS como se describe en el artículo [Usar la directiva de configuración de aplicaciones para iOS](../apps/app-configuration-policies-use-ios.md). Para más información, consulte [Sophos Intercept X para Mobile iOS: configuración administrada disponible](https://community.sophos.com/kb/133963) en la base de conocimientos de Sophos.

### <a name="wandera-app-configuration-policy"></a>Directiva de configuración de aplicaciones de Wandera

> [!NOTE]
> Para las pruebas iniciales, use un grupo de prueba al asignar usuarios y dispositivos en la sección Asignaciones de la directiva de configuración. 

- **Android**
  - Consulte las instrucciones para [usar las directivas de configuración de aplicaciones de Microsoft Intune para Android](../apps/app-configuration-policies-use-android.md) para agregar la directiva de configuración de aplicaciones de Wandera para Android mediante la siguiente información cuando se le solicite.

1. En el **portal RADAR de Wandera**, haga clic en el botón **Add** (Agregar) que aparece en **Configuration settings** (Formato de opciones de configuración).
2. Seleccione **Activation Profile URL** (Dirección URL del perfil de activación) en la lista de **Claves de configuración**. Haga clic en **Aceptar**.
3. En **Activation Profile URL** (Dirección URL del perfil de activación), seleccione **string** (cadena) en el menú **Value type** (Tipo de valor) y, luego, copie la **dirección URL de vínculo compartible** del perfil de activación deseado en RADAR.
4. En la **interfaz de usuario de configuración de aplicaciones de la consola de administración de Intune**, seleccione **Configuración**, defina **Formato de opciones de configuración > Usar diseñador de configuraciones** y pegue la **dirección URL de vínculo compartible**.  

> [!NOTE] 
> A diferencia de iOS, tendrá que definir una directiva de configuración de aplicaciones de Android Enterprise única para cada perfil de activación de Wandera. Si no necesita varios perfiles de activación de Wandera, puede usar una sola configuración de aplicaciones de Android en todos los dispositivos de destino. Al crear perfiles de activación en Wandera, asegúrese de seleccionar "Azure Active Directory" en la configuración de Usuario asociado para asegurarse de que Wandera puede sincronizar el dispositivo con Intune a través de UEM Connect.

- **iOS**
  - Consulte las instrucciones para [usar las directivas de configuración de aplicaciones de Microsoft Intune para iOS](../apps/app-configuration-policies-use-ios.md) para agregar la directiva de configuración de aplicaciones de Wandera para iOS mediante la siguiente información cuando se le solicite.

1. En **RADAR Wandera Portal** (Portal de RADAR de Wandera), vaya a **Dispositivos > Activaciones** y seleccione un perfil de activación. Haga clic en **Estrategias de implementación > Dispositivos administrados > Microsoft Intune** y busque la **opción de configuración de aplicaciones iOS**.  
2. Expanda el cuadro para mostrar el XML de configuración de aplicaciones iOS y cópielo en el Portapapeles del sistema.  
3. En la **interfaz de usuario de configuración de aplicaciones de la consola de administración de Intune**, defina **Formato de opciones de configuración > Especificar datos XML**. 
4. Pegue el código XML en el cuadro de texto de configuración de aplicaciones.

> [!NOTE]
> Se puede usar una única directiva de configuración de iOS en todos los dispositivos que se van a aprovisionar con Wandera.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Asignación de aplicaciones de Mobile Threat Defense a los usuarios finales mediante Intune

Para instalar la aplicación Mobile Threat Defense en el dispositivo del usuario final, puede seguir los pasos que se indican a continuación en Azure Portal. Asegúrese de conocer los siguientes procesos:

- [Asignación de aplicaciones a grupos con Intune](../apps/apps-deploy.md)

Elija la sección que corresponda, según su proveedor MTD:

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [SandBlast Mobile de Check Point](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Asignación de Lookout for Work

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de Lookout for Work en la tienda de aplicaciones de Google](https://play.google.com/store/apps/details?id=com.lookout.enterprise) como la **dirección URL de la tienda App Store**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de Lookout for Work en la App Store de iOS](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) como la **dirección URL de la tienda App Store**.

- **Aplicación Lookout for Work fuera de la tienda de Apple**
  - Debe volver a firmar la aplicación Lookout for Work de iOS. Lookout distribuye su aplicación Lookout for Work de iOS fuera de la tienda App Store de iOS. Antes de distribuir la aplicación, deberá volver a firmar la aplicación con su certificado de desarrollador empresarial de iOS.  
  - Para obtener información sobre cómo volver a firmar las aplicaciones Lookout for Work de iOS, vea [el proceso de volver a firmar la aplicación Lookout for Work de iOS](https://personal.support.lookout.com/hc/articles/114094038714) en el sitio web de Lookout.

  - **Habilite la autenticación de Azure AD para los usuarios de la aplicación Lookout for Work para iOS**.

    1. Vaya a [Azure Portal](https://portal.azure.com), inicie sesión con sus credenciales y, después, vaya a la página de la aplicación.

    2. Agregue la **aplicación Lookout for Work de iOS** como una **aplicación de cliente nativ**.

    3. Reemplace **com.lookout.enterprise.yourcompanyname** por el id. de agrupación del cliente que ha seleccionado al registrar el IPA.

    4. Agregue un URI de redireccionamiento adicional: **&lt;companyportal://code/>** seguido de una versión codificada por URL del URI de redireccionamiento original.

    5. Agregue los **permisos delegados** a la aplicación.

    > [!NOTE]
    > Para obtener más información, vea [Configurar una aplicación de cliente nativo con Azure AD](/azure/app-service/configure-authentication-provider-aad#optional-configure-a-native-client-application).

  - **Agregue el archivo IPA de Lookout for Work**.

    - Cargue el archivo .ipa que se ha vuelto a firmar como se describe en el artículo [Agregar aplicaciones LOB para iOS con Intune](../apps/lob-apps-ios.md). También necesita establecer la versión mínima del sistema operativo en iOS 8.0 o posterior.

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Asignación de Symantec Endpoint Protection Mobile

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de SEP Mobile en la tienda App Store](https://play.google.com/store/apps/details?id=com.skycure.skycure) como la **dirección URL de la tienda App Store**.  En **Versión mínima del sistema operativo**, seleccione **Android 4.0 (Ice Cream Sandwich)** .

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de SEP Mobile en la tienda App Store](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) como la **dirección URL de la tienda App Store**.

### <a name="assigning-check-point-sandblast-mobile"></a>Asignación de SandBlast Mobile de Check Point

- **Android**  
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de SandBlast Mobile de Check Point](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) como la **dirección URL de la tienda App Store**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de SandBlast Mobile de Check Point](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) como la **dirección URL de la tienda App Store**.  

### <a name="assigning-zimperium"></a>Asignación de Zimperium

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de Zimperium en la tienda App Store](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) como la **dirección URL de la tienda App Store**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de Zimperium en la tienda App Store](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) como la **dirección URL de la tienda App Store**.  
 
### <a name="assigning-pradeo"></a>Asignación de Pradeo

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de Pradeo en la tienda App Store](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) como la **dirección URL de la tienda App Store**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de Pradeo en la tienda App Store](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) como la **dirección URL de la tienda App Store**.

### <a name="assigning-better-mobile"></a>Asignación de Better Mobile

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de Active Shield en la tienda App Store](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) como la **dirección URL de la tienda App Store**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de Active Shield en la tienda App Store](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) como la **dirección URL de la tienda App Store**.

### <a name="assigning-sophos"></a>Asignación de Sophos

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de Sophos en la tienda App Store](https://play.google.com/store/apps/details?id=com.sophos.smsec) como la **dirección URL de la tienda App Store**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de Active Shield en la tienda App Store](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) como la **dirección URL de la tienda App Store**.

### <a name="assigning-wandera"></a>Asignación de Wandera

- **Android**
  - Vea las instrucciones para [agregar aplicaciones de la tienda Android en Microsoft Intune](../apps/store-apps-android.md). Use la [dirección URL de Wandera Mobile en la tienda App Store](https://play.google.com/store/apps/details?id=com.wandera.android) como la **dirección URL de la tienda App Store**. En **Versión mínima del sistema operativo**, seleccione **Android 5.0**.

- **iOS**
  - Vea las instrucciones para [agregar aplicaciones de la tienda iOS en Microsoft Intune](../apps/store-apps-ios.md). Use la [dirección URL de Wandera Mobile en la tienda App Store](https://itunes.apple.com/app/wandera/id605469330) como la **dirección URL de la tienda App Store**.

## <a name="next-steps"></a>Pasos siguientes

- [Configuración de la directiva de cumplimiento de dispositivos para MTD](mtd-device-compliance-policy-create.md)