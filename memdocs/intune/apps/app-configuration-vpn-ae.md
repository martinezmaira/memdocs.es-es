---
title: Configuración de VPN o VPN por aplicación para dispositivos Android Enterprise en Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Use una directiva de configuración de aplicaciones para agregar o crear un perfil de VPN o VPN por aplicación para Android Enterprise en Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262904"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Use una directiva de VPN y VPN por aplicación en dispositivos Android Enterprise en Microsoft Intune

Las redes privadas virtuales (VPN) permiten a los usuarios acceder a los recursos de la organización de forma remota; por ejemplo, desde casa, un hotel o una cafetería. En Microsoft Intune, puede configurar aplicaciones cliente VPN en dispositivos Android Enterprise mediante una directiva de configuración de aplicaciones. A continuación, implemente esta directiva con su configuración de VPN en los dispositivos de su organización.

También puede crear directivas de VPN que se usan por aplicaciones específicas. Esta característica se denomina "VPN por aplicación". Cuando la aplicación está activa, puede conectarse a la VPN y acceder a los recursos a través de la VPN. Cuando la aplicación no está activa, no se usa la VPN.

Esta característica se aplica a:

- Android Enterprise

Hay dos formas de crear la directiva de configuración para su aplicación cliente VPN:

- Diseñador de configuraciones
- Datos JSON

En este artículo se muestra cómo crear una VPN por aplicación y una directiva de configuración de la aplicación VPN mediante ambas opciones.

> [!NOTE]
> Muchos de los parámetros de configuración del cliente VPN son similares. Sin embargo, cada aplicación tiene sus claves y opciones únicas. Si tiene alguna pregunta, diríjase a su proveedor de VPN.

## <a name="before-you-begin"></a>Antes de comenzar

- Android no desencadena automáticamente una conexión de cliente VPN cuando se abre una aplicación. La conexión VPN debe iniciarse manualmente. O bien, puede usar [VPN siempre activa](../configuration/vpn-settings-android-enterprise.md) para iniciar la conexión.

- Los siguientes clientes VPN admiten las directivas de configuración de aplicaciones de Intune:

  - Cisco AnyConnect
  - SSO de Citrix
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Al crear la directiva de VPN en Intune, seleccionará claves diferentes para configurar. Estos nombres de clave varían con las distintas aplicaciones de cliente VPN. Por lo tanto, los nombres de clave de su entorno pueden ser diferentes de los ejemplos de este artículo.

- El Diseñador de configuraciones y los datos JSON pueden usar correctamente la autenticación basada en certificados. Si la autenticación VPN requiere certificados de cliente, cree los perfiles de certificado antes de crear la directiva de VPN. Las directivas de configuración de aplicaciones de VPN usan los valores de los perfiles de certificado.

  Los dispositivos de perfil de trabajo de Android Enterprise admiten certificados SCEP y PKCS. Los dispositivos de perfil de trabajo de propiedad corporativa, dedicados y totalmente administrados de Android Enterprise solo admiten certificados SCEP. Para más información, consulte [Uso de certificados para la autenticación en Microsoft Intune](../protect/certificates-configure.md).

## <a name="per-app-vpn-overview"></a>Introducción a VPN por aplicación

Al crear y probar una VPN por aplicación, el flujo básico incluye los pasos siguientes:

1. Seleccione la aplicación cliente VPN. En la sección [Antes de comenzar](#before-you-begin) (de este artículo) se enumeran las aplicaciones compatibles.
2. Obtenga los identificadores de paquete de aplicación de las aplicaciones que usarán la conexión VPN. En la sección [Obtención del id. del paquete de las aplicaciones](#get-the-app-package-id) (en este artículo) se muestra cómo hacerlo.
3. Si usa certificados para autenticar la conexión VPN, cree e implemente los perfiles de certificado antes de implementar la directiva de VPN. Asegúrese de que los perfiles de certificado se implementan correctamente. Para más información, consulte [Uso de certificados para la autenticación en Microsoft Intune](../protect/certificates-configure.md).
4. Agregue la [aplicación cliente VPN](apps-add-android-for-work.md) a Intune e implemente la aplicación en los usuarios y los dispositivos.
5. Cree una directiva de configuración de aplicaciones de VPN. Use los identificadores de paquete de la aplicación y la información del certificado en la directiva.
6. Implemente la nueva directiva de VPN.
7. Confirme que la aplicación cliente VPN se conecta correctamente al servidor VPN.
8. Cuando la aplicación esté activa, confirme que el tráfico de la aplicación atraviesa correctamente la VPN.

## <a name="get-the-app-package-id"></a>Obtención del id. del paquete de las aplicaciones

Obtenga el identificador de paquete para cada aplicación que vaya a usar la VPN. En el caso de las aplicaciones disponibles públicamente, puede obtener el identificador del paquete de la aplicación en la tienda Google Play. La dirección URL que se muestra para cada aplicación incluye el id. del paquete.

En el ejemplo siguiente, el identificador del paquete de la aplicación del explorador Microsoft Edge es `com.microsoft.emmx`. El identificador de paquete forma parte de la dirección URL:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Obtenga el identificador del paquete de la aplicación en la dirección URL de la tienda Google Play.":::

En el caso de las aplicaciones de línea de negocio (LOB), obtenga el identificador del paquete del desarrollador de la aplicación o del proveedor.

## <a name="certificates"></a>Certificados

En este artículo se supone que la conexión VPN utiliza la autenticación basada en certificados. También se supone que ha implementado correctamente todos los certificados de la cadena necesarios para que los clientes se autentiquen correctamente. Normalmente, esta cadena de certificados incluye el certificado de cliente, los certificados intermedios y el certificado raíz.

Para más información sobre los certificados, consulte [Uso de certificados para la autenticación en Microsoft Intune](../protect/certificates-configure.md).

Cuando se implementa el perfil de certificado de autenticación de cliente, se crea un token de certificado en el perfil de certificado. Este token se usa para crear la directiva de configuración de la aplicación de VPN.

Para familiarizarse con la creación de perfiles de configuración de aplicaciones, consulte [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>Uso del Diseñador de configuraciones

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Dispositivos administrados**.
3. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **Directiva de configuración de la aplicación: directiva de VPN de Cisco AnyConnect para dispositivos de perfil de trabajo de Android Enterprise**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.
    - **Plataforma**: seleccione **Android Enterprise**.
    - **Tipo de perfil**: Las opciones son:
      - **Todos los tipos de perfil**: esta opción admite la autenticación mediante nombre de usuario y contraseña. Si usa la autenticación basada en certificados, no utilice esta opción.
      - **Solo perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado**: esta opción admite la autenticación basada en certificados y la autenticación de nombre de usuario y contraseña.
      - **Solo perfil de trabajo**: esta opción admite la autenticación basada en certificados y la autenticación de nombre de usuario y contraseña.
    - **Aplicación de destino**: seleccione la aplicación cliente VPN que agregó anteriormente. En el ejemplo siguiente, se usa la aplicación cliente VPN de Cisco AnyConnect:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Cree una directiva de configuración de aplicaciones para configurar una VPN o una VPN por aplicación en Microsoft Intune":::

4. Seleccione **Siguiente**.
5. En **Configuración**, escriba las propiedades siguientes:

    - **Formato de opciones de configuración**: seleccione **Uso del Diseñador de configuraciones**:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Creación de una directiva de VPN de configuración de aplicaciones en Microsoft Intune mediante el Diseñador de configuraciones: ejemplo.":::

    - **Agregar**: muestra la lista de claves de configuración. Seleccione todas las claves de configuración necesarias para la configuración > **Aceptar**.

      En este ejemplo, seleccionamos una lista mínima para una VPN de AnyConnect, incluida la autenticación basada en certificados y la VPN por aplicación:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Adición de claves de configuración a una directiva de configuración de aplicaciones de VPN en Microsoft Intune mediante el Diseñador de configuraciones (ejemplo).":::

    - **Valor de configuración:** Escriba los valores de las claves de configuración que ha seleccionado. Recuerde que los nombres de clave varían en función de la aplicación cliente VPN que esté usando. En las claves seleccionadas en nuestro ejemplo:

      - **Aplicaciones permitidas de VPN por aplicación**: escriba el identificador de paquete de aplicación que recopiló anteriormente. Por ejemplo:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="Escritura de los identificadores de paquete de aplicación permitidos en una directiva de configuración de aplicaciones de VPN en Microsoft Intune mediante el Diseñador de configuraciones: ejemplo.":::

      - **Alias de certificado de cadena de claves** (opcional): cambie **Tipo de valor** de **cadena** a **certificado**. Seleccione el perfil de certificado de cliente que se usará con la autenticación de VPN. Por ejemplo:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="Cambio del alias del certificado de cliente de cadena de claves en una directiva de configuración de aplicaciones de VPN en Microsoft Intune mediante el Diseñador de configuraciones: ejemplo.":::

      - **Protocolo**: seleccione **SSL** o el protocolo de túnel **IPsec** de la VPN.
      - **Nombre de la conexión**: escriba un nombre descriptivo para esta conexión VPN. Los usuarios ven este nombre de conexión en sus dispositivos. Por ejemplo, escriba `ContosoVPN`.
      - **Host**: escriba la dirección URL del nombre de host para el enrutador de cabecera. Por ejemplo, escriba `vpn.contoso.com`.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Ejemplos de protocolo, nombre de conexión y nombre de host en una directiva de configuración de aplicaciones de VPN en Microsoft Intune mediante el Diseñador de configuraciones":::

6. Seleccione **Siguiente**.
7. En **Asignaciones**, seleccione los grupos para asignar la directiva de configuración de la aplicación de VPN.

    Seleccione **Siguiente**.

8. En **Revisar y crear**, revise la configuración. Al seleccionar **Crear**, los cambios se guardan y la directiva se implementa en los grupos. La directiva también se muestra en la lista de directivas de configuración de la aplicación.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Revisión de la directiva de configuración de la aplicación mediante el flujo del Diseñador de configuraciones en Microsoft Intune: ejemplo.":::

## <a name="use-json"></a>Uso de JSON

Utilice esta opción si no tiene o no conoce toda la configuración de VPN necesaria del **Diseñador de configuraciones**. Si necesita ayuda, póngase en contacto con su proveedor de VPN.

### <a name="get-the-certificate-token"></a>Obtención del token de certificado

En estos pasos, cree una directiva temporal. No se guardará la directiva. La intención es copiar el token de certificado. Usará este token al crear la directiva de VPN mediante JSON (sección siguiente).

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Dispositivos administrados**.
2. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: Escriba cualquier nombre. Esta directiva es temporal y no se guardará.
    - **Plataforma**: seleccione **Android Enterprise**.
    - **Tipo de perfil**: seleccione **Solo perfil de trabajo**.
    - **Aplicación de destino**: seleccione la aplicación cliente VPN que agregó anteriormente.

3. Seleccione **Siguiente**.
4. En **Configuración**, escriba las propiedades siguientes:

    - **Formato de opciones de configuración**: seleccione **Uso del Diseñador de configuraciones**.
    - **Agregar**: muestra la lista de claves de configuración. Seleccione cualquier clave con un **Tipo de valor** de **cadena**. Seleccione **Aceptar**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="En el diseñador de configuración, selección de cualquier clave con un tipo de valor de cadena en la directiva de configuración de la aplicación de VPN de Microsoft Intune":::.

5. Ahora cambie **Tipo de valor** de **cadena** a **certificado**. Este paso le permite seleccionar el perfil de certificado de cliente correcto que autentica la VPN:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="Cambio del nombre de conexión en una directiva de configuración de la aplicación de VPN en Microsoft Intune: ejemplo":::

6. Vuelva a cambiar **Tipo de valor** a **cadena** de inmediato. El **valor de configuración** cambia a un token `{{cert:GUID}}`:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Valor de configuración con token de certificado en una directiva de configuración de la aplicación de VPN en Microsoft Intune":::

7. Copie y pegue este token de certificado en otro archivo, como un editor de texto.

8. Descarte esta directiva. No la guarde. El único propósito es copiar y pegar el token de certificado.

### <a name="create-the-vpn-policy-using-json"></a>Creación de la directiva de VPN mediante JSON

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Dispositivos administrados**.

2. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **Directiva de configuración de la aplicación: directiva de VPN de Cisco AnyConnect de JSON para dispositivos de perfil de trabajo de Android Enterprise en toda la compañía**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.
    - **Plataforma**: seleccione **Android Enterprise**.
    - **Tipo de perfil**: Las opciones son:
      - **Todos los tipos de perfil**: esta opción admite la autenticación mediante nombre de usuario y contraseña. Si usa la autenticación basada en certificados, no utilice esta opción.
      - **Solo perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado**: esta opción admite la autenticación basada en certificados y la autenticación de nombre de usuario y contraseña.
      - **Solo perfil de trabajo**: esta opción admite la autenticación basada en certificados y la autenticación de nombre de usuario y contraseña.
    - **Aplicación de destino**: seleccione la aplicación cliente VPN que agregó anteriormente. 

3. Seleccione **Siguiente**.
4. En **Configuración**, escriba las propiedades siguientes:

    - **Formato de opciones de configuración**: seleccione **Especificar datos JSON**. Puede editar el archivo JSON directamente.
    - **Descargar plantilla JSON**: use esta opción para descargar y actualizar la plantilla en cualquier editor externo. Tenga cuidado con los editores de texto que emplean las **comillas inteligentes**, ya que podrían crear JSON no válido.

    Después de escribir los valores necesarios para la configuración, quite todas las configuraciones que tengan `"STRING_VALUE"` o `STRING_VALUE`.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="Ejemplo del uso del flujo JSON: edición de JSON":::.

5. Seleccione **Siguiente**.
6. En **Asignaciones**, seleccione los grupos para asignar la directiva de configuración de la aplicación de VPN.

    Seleccione **Siguiente**.

7. En **Revisar y crear**, revise la configuración. Al seleccionar **Crear**, los cambios se guardan y la directiva se implementa en los grupos. La directiva también se muestra en la lista de directivas de configuración de la aplicación.

#### <a name="json-example-for-f5-access-vpn"></a>Ejemplo de JSON para la VPN de acceso de F5

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>Información adicional

- [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados](app-configuration-policies-use-android.md)
- [Configuración de dispositivos Android Enterprise para configurar VPN en Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Pasos siguientes

- [Creación de perfiles de VPN para conectarse a servidores VPN en Intune](../configuration/vpn-settings-configure.md)
