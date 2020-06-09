---
title: Configuración de una VPN para dispositivos Android Enterprise
titleSuffix: Microsoft Intune
description: Puede usar una directiva de protección de aplicaciones con el fin de configurar una VPN para dispositivos Android Enterprise.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347423"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Configuración de una VPN para dispositivos Android Enterprise

En este tema se describe cómo crear una directiva de configuración de aplicaciones, que se puede implementar en combinación con un cliente VPN en dispositivos Android Enterprise. Esta configuración permitirá el tráfico de red a las aplicaciones que elija, de modo que puedan acceder a recursos empresariales.

> [!NOTE]
> La plataforma Android actualmente no permite activar de forma automática la conexión de un cliente VPN cuando una de las aplicaciones elegidas está abierta. En primer lugar, la conexión VPN se debe iniciar manualmente, o bien puede usar una [VPN que siempre esté activa](../configuration/vpn-settings-android-enterprise.md).

Los requisitos previos para crear una directiva de configuración con el fin de lograr un acceso VPN correcto incluyen el hecho de que el cliente VPN en cuestión admita los perfiles de configuración de aplicaciones administradas. Algunos de los clientes VPN que actualmente admiten la directiva de configuración de aplicaciones de Intune son los siguientes:
- Cisco AnyConnect
- SSO de Citrix
- F5Access
- Global Connect de Palo Alto
- Pulse Secure
- SonicWall Mobile Connect

Si el método de autenticación de acceso al punto de conexión de la VPN requiere el uso de certificados de cliente, será necesario crear los perfiles de los certificados de antemano para rellenar los valores necesarios de la directiva de configuración de aplicaciones.

> [!NOTE]
> Si bien para los perfiles de trabajo de Android Enterprise se admiten certificados SCEP y PKCS, para propietarios de dispositivos Android Enterprise actualmente solo se admiten los SCEP. 

El flujo básico para crear y probar el perfil de VPN por aplicación es el siguiente:
1.  Elija la aplicación del cliente VPN que sea adecuada para su infraestructura.
2.  Identifique los id. de los paquetes de las aplicaciones de productividad que quiera usar con la conexión VPN.
3.  Implemente los perfiles de los certificados necesarios para cumplir los requisitos de autenticación de la conexión VPN. Asegúrese de comprobar que la implementación sea correcta.
4.  Implemente la aplicación del cliente VPN.
5.  Prepare el perfil de VPN basado en la configuración de la aplicación mediante la información obtenida en pasos anteriores.
6.  Implemente el perfil de VPN recién creado.
7.  Valide que la aplicación del cliente VPN se conecte correctamente a la infraestructura del servidor VPN.
8.  Valide que el tráfico de las aplicaciones de productividad circule correctamente por la VPN, cuando esta esté activa.

## <a name="get-the-app-package-id"></a>Obtención del id. del paquete de las aplicaciones

Identifique el id. del paquete de cada aplicación a la que quiera conceder acceso a la VPN. En el caso de las aplicaciones disponibles públicamente, puede obtener los id. de paquete de cada una de las aplicaciones en Google Play Store. La dirección URL que se muestra para cada aplicación incluye el id. del paquete. Por ejemplo, el id. del paquete de la versión para Android del explorador Microsoft Edge es `com.microsoft.emmx`. El id. del paquete se incluye como parte de la dirección URL.

![Ejemplo de cómo encontrar el id. del paquete de la aplicación.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

En el caso de las aplicaciones de línea de negocio (LOB), deberá solicitar al proveedor o equipo de desarrollo que se lo faciliten.

## <a name="certificates"></a>Certificados

En este tema, daremos por hecho que su conexión VPN usa la autenticación basada en certificados y que ya ha implementado correctamente todos ellos en la cadena necesaria para la adecuada autenticación del cliente. Normalmente, sería el caso del certificado de cliente, cualquier certificado intermedio y el certificado raíz.
Para obtener más información sobre la implementación de certificados para Android Enterprise, consulte el tema [Uso de certificados para la autenticación en Microsoft Intune](../protect/certificates-configure.md).

Una vez implementado el perfil de certificado para la autenticación del cliente, necesitará algunos detalles sobre dicho perfil para crear la directiva de configuración de la aplicación VPN.
Para familiarizarse con la creación de perfiles de configuración de aplicaciones, consulte el tema [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados](../apps/app-configuration-policies-use-android.md).
 

## <a name="build-the-vpn-profile"></a>Creación del perfil de VPN

Hay dos formas de crear la directiva de configuración para su aplicación VPN. Puede usar el **diseñador de configuración** o la opción **Datos JSON**. La opción **Datos JSON** es necesaria cuando en el método del **diseñador de configuración** no están disponibles todos los valores de configuración necesarios para la VPN. Si determina que la opción JSON es la adecuada en su caso, diríjase a su proveedor de VPN para obtener ayuda. En este tema, se mostrarán ejemplos de ambos métodos. En ambos métodos, tanto para la opción **Datos JSON** como el **diseñador de configuración**, puede incorporar correctamente la autenticación basada en certificados. Al emplear el método **Datos JSON**, puede empezar utilizando el **diseñador de configuración** para extraer los valores del perfil que sean necesarios.

> [!NOTE]
> Aunque muchos de los parámetros de la configuración del cliente VPN son similares, cada aplicación tiene sus claves y opciones únicas. Si tiene alguna pregunta, diríjase a su proveedor de VPN. 

## <a name="use-the-configuration-designer-flow"></a>Uso del flujo del diseñador de configuración

1.  Para empezar, agregue una nueva directiva de configuración de aplicaciones para **dispositivos administrados**.
2.  Escriba un nombre adecuado.
3.  Seleccione **Android Enterprise** como plataforma.
4.  Si la autenticación basada en certificados es necesaria, seleccione **Solo perfil de trabajo** o **Solo el propietario del dispositivo** como tipo de perfil. La opción **Perfil de trabajo y perfil del propietario del dispositivo** no es compatible con la autenticación basada en certificados.
5.  Para la aplicación de destino, seleccione el cliente VPN que ha implementado; en este ejemplo, se usa el cliente VPN Cisco AnyConnect que se ha implementado anteriormente.

  ![Ejemplo del proceso de creación de una directiva de configuración de la aplicación (conceptos básicos).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. En la página siguiente, abra el menú desplegable de los valores de configuración y seleccione la opción **Usar diseñador de configuraciones**.

  ![Ejemplo del uso del flujo del diseñador de configuraciones (configuración).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Haga clic en **Agregar** para mostrar la lista de claves de configuración.
8.  Seleccione todas las claves de configuración que necesite para la configuración que elija. En este ejemplo, se usa una lista mínima para establecer una VPN de AnyConnect, incluida la autenticación basada en certificados y la VPN por aplicación.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. Escriba los valores apropiados para las claves **Nombre de conexión**, **Host** y **Protocolo**.

  ![Ejemplo del uso del flujo del diseñador de configuraciones (selección de las clave de configuración).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > Los nombres de estas claves pueden variar en función de la aplicación del cliente VPN para la que cree la directiva.

10. Escriba los id. de los paquetes de aplicaciones que ha recopilado anteriormente en la clave **Per App VPN Allowed Apps** (Aplicaciones VPN permitidas por aplicación).

  ![Ejemplo del uso del flujo del diseñador de configuraciones (id. de los paquetes de aplicaciones).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. En la clave opcional **KeyChain Certificate Alias** (Alias de certificado de cadena de claves), cambie **Tipo de valor** de **cadena** a **certificado**. De este modo, podrá elegir el perfil de certificado de cliente correcto que se utilizará con la autenticación de la VPN.

  ![Ejemplo del uso del flujo del diseñador de configuraciones (actualización del alias de certificado de cadena de bloques).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. En la página siguiente, elija las etiquetas de ámbito adecuadas.
13. En la página siguiente, indique los grupos en los que quiera implementar la directiva de configuración de aplicaciones.
14. Seleccione **Crear** para completar la creación e implementación de la directiva.

  ![Ejemplo del uso del flujo del diseñador de configuraciones (revisión).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>Uso del flujo JSON

Crear un perfil temporal:
1.  Para empezar, agregue una nueva directiva de configuración de aplicaciones para **dispositivos administrados**.
2.  Escriba un nombre adecuado (el uso de este perfil es temporal, ya que NO se guardará).
3.  Seleccione **Android Enterprise** como plataforma.
4.  Para la aplicación de destino, seleccione el cliente VPN que ha implementado.
5.  Si la autenticación basada en certificados es necesaria, seleccione **Solo perfil de trabajo** o **Solo el propietario del dispositivo** como tipo de perfil. La opción **Perfil de trabajo y perfil del propietario del dispositivo** no es compatible con la autenticación basada en certificados.

  ![Ejemplo del uso del flujo JSON (conceptos básicos).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  En la página siguiente, abra el menú desplegable **Opciones de configuración** y seleccione la opción **Usar diseñador de configuraciones**.

  ![Ejemplo del uso del flujo JSON (formato de las opciones de configuración).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Haga clic en **Agregar** para mostrar la lista de claves de configuración.
8.  Seleccione cualquiera de las claves que tenga la opción **Tipo de valor** establecida como **cadena** y haga clic en **Aceptar**.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Ahora cambie **Tipo de valor** de **cadena** a **certificado**. De este modo, podrá elegir el perfil de certificado de cliente correcto que se utilizará con la autenticación de la VPN.

  ![Ejemplo del uso del flujo JSON (nombre de la conexión).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. Vuelva a cambiar **Tipo de valor** a **cadena** de inmediato. Observe que la opción **Valor de configuración** cambia a un token de formato `{{cert:GUID}}`.
11. Seleccione la representación del token del certificado y cópiela en otra ubicación, por ejemplo, un editor de texto.

  ![Ejemplo del uso del flujo JSON (valor de configuración).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Descarte el perfil que está creando, ya que el único objetivo del paso anterior era determinar el token del certificado.

### <a name="create-the-vpn-profile"></a>Creación del perfil de VPN

1.  Para empezar, agregue un nuevo perfil de configuración de aplicaciones para **dispositivos administrados**.
2.  Escriba un nombre adecuado.
3.  Seleccione **Android Enterprise** como plataforma.
4.  Para la aplicación de destino, seleccione el cliente VPN que ha implementado.
5.  Si la autenticación basada en certificados es necesaria, seleccione **Solo perfil de trabajo** o **Solo el propietario del dispositivo** como tipo de perfil. La opción **Perfil de trabajo y perfil del propietario del dispositivo** no es compatible con la autenticación basada en certificados.
6.  Abra el menú desplegable **Opciones de configuración** y seleccione la opción **Especificar datos JSON**.
7.  Puede editar los datos JSON directamente, o bien, si lo prefiere, usar el botón **Descargar plantilla JSON** para descargar la plantilla y, luego, modificarla en el editor externo que prefiera. Tenga cuidado con los editores de texto que emplean las **comillas inteligentes**, ya que su uso invalidaría los datos JSON.

  ![Ejemplo del uso del flujo JSON (edición de JSON).](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Con independencia del método que use, una vez que haya rellenado los valores que necesite para su configuración, deberá eliminar de los datos JSON el resto de opciones de configuración que tengan un valor "STRING_VALUE" o STRING_VALUE.

#### <a name="example-json-for-f5-access-vpn"></a>Ejemplo de JSON para el cliente VPN de F5Access.

A continuación tiene un ejemplo de datos JSON para el cliente VPN de F5Access.

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

## <a name="summary"></a>Resumen

El uso de una directiva de configuración de aplicaciones para dispositivos Android Enterprise inscritos permite aprovechar el comportamiento de VPN por aplicación, a pesar de no ser directamente compatible con la plataforma. 

## <a name="additional-information"></a>Información adicional

Para obtener información relacionada, consulte los temas siguientes:
- [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados](../apps/app-configuration-policies-use-android.md)
- [Configuración de dispositivos Android Enterprise para configurar VPN en Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Pasos siguientes

- [Creación de perfiles de VPN para conectarse a servidores VPN en Intune](../configuration/vpn-settings-configure.md)
