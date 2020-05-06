---
title: Cómo crear perfiles de Wi-Fi
titleSuffix: Configuration Manager
description: Aprenda a usar perfiles de Wi-Fi en Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690233"
---
# <a name="create-wi-fi-profiles"></a>Crear perfiles de Wi-Fi

*Se aplica a: Configuration Manager (rama actual)*

Use perfiles de Wi-Fi en Configuration Manager para implementar la configuración de red inalámbrica para los usuarios de su organización. Al implementar estas opciones, les resultará más fácil a los usuarios conectarse a la Wi-Fi.  

Por ejemplo, quiere permitir que todos los equipos portátiles Windows se conecten a una red Wi-Fi que tiene. Cree un perfil de Wi-Fi que contenga la configuración necesaria para conectarse a la red inalámbrica. Luego, implemente el perfil para todos los usuarios que tengan equipos portátiles Windows en la jerarquía. Los usuarios de estos dispositivos ven la empresa en la lista de redes inalámbricas y pueden conectarse fácilmente a esta red.  

Puede configurar perfiles de Wi-Fi para las versiones de sistema operativo siguientes:

- Windows 8.1 de 32 bits o 64 bits

- Windows RT 8.1

- Windows 10 o Windows 10 Mobile

También puede usar Configuration Manager para implementar la configuración de red inalámbrica en dispositivos móviles mediante la administración de dispositivos móviles (MDM) local. Para más información, consulte [¿Qué es la MDM local?](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)

Cuando se crea un perfil de Wi-Fi, puede incluir una amplia gama de opciones de seguridad. Estas opciones incluyen certificados para la validación de servidor y la autenticación de cliente que se han insertado mediante perfiles de certificado de Configuration Manager. Para más información sobre perfiles de certificado, consulte [Perfiles de certificado](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Crear un perfil de Wi-Fi

1. Vaya al área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la empresa** y seleccione **Perfiles de Wi-Fi**.

1. En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear perfil de Wi-Fi**.

1. En la página **General** del Asistente para crear perfil de Wi-Fi, especifique la información siguiente:

    - **Nombre**: escriba un nombre único para identificar el perfil en la consola.

    - **Descripción**: si quiere, agregue una descripción para proporcionar más información para el perfil de Wi-Fi.

    - **Importar un elemento de perfil de Wi-Fi existente desde un archivo**: seleccione esta opción para usar la configuración de otro perfil de Wi-Fi. Al seleccionar esta opción, las páginas restantes del asistente se simplifican a dos páginas: **Importar perfil de Wi-Fi** y **Plataformas compatibles**.

        > [!IMPORTANT]
        > Asegúrese de que el perfil de Wi-Fi que desea importar contiene XML válido para un perfil de Wi-Fi. Al importar el archivo, Configuration Manager no valida el perfil.

    - **Gravedad de la falta de cumplimiento de los informes**: elija uno de los niveles de gravedad siguientes que el dispositivo notifica si evalúa que el perfil de Wi-Fi no es compatible. Por ejemplo, si se produce un error en la instalación del perfil, no es compatible.

        - **Ninguna**: los equipos que no respeten esta regla de cumplimiento no notificarán ninguna gravedad de error en los informes de Configuration Manager.

        - **Información**

        - **Advertencia**

        - **Crítica**

        - **Crítica con evento**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager. Los dispositivos también registran el estado de falta de cumplimiento como un evento de Windows en el registro de eventos de la aplicación.

1. En la página **Perfil de Wi-Fi** del Asistente, especifique la información siguiente:

    - **Nombre de red**: proporcione el nombre que los dispositivos mostrarán como nombre de red.

        > [!IMPORTANT]
        > Configuration Manager no admite el uso de los caracteres apóstrofo (`'`) ni coma (`,`) en el nombre de red.

    - **SSID**: especifique el identificador que distingue mayúsculas de minúsculas de la red inalámbrica.

    - **Conectarse automáticamente cuando esta red esté dentro del alcance**
    - **Buscar otras redes inalámbricas mientras se esté conectado a esta red**
    - **Conectarse cuando la red no está difundiendo su nombre (SSID)**

1. En la página **Configuración de seguridad**, especifique la información siguiente:

    > [!IMPORTANT]
    > Si va a crear un perfil de Wi-Fi para la [MDM local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md), la rama actual de Configuration Manager solo admite estas configuraciones de seguridad de Wi-Fi:  
    >
    > - Tipos de seguridad: **WPA2 Enterprise** o **WPA2 Personal**  
    > - Tipos de cifrado: **AES** o **TKIP**  
    > - Tipos de EAP: **tarjeta inteligente u otro certificado** o **PEAP**  

    - **Tipo de seguridad**: seleccione el protocolo de seguridad que la red inalámbrica utiliza, o seleccione **Sin autenticación (sistema abierto)** si la red no es segura.

    - **Cifrado**: si el tipo de seguridad lo admite, establezca el método de cifrado para la red inalámbrica.

    - **Tipo de EAP**: seleccione el protocolo de autenticación para el método de cifrado seleccionado.

        > [!NOTE]
        > Solo para dispositivos Windows Phone: no se admiten los tipos de EAP **LEAP** y **EAP-FAST** .

        Seleccione **Configurar** para especificar las propiedades para el tipo de EAP seleccionado. Esta opción no está disponible para algunos tipos de EAP seleccionados.

        > [!IMPORTANT]
        > La ventana Configuración de tipo de EAP es de Windows. Asegúrese de ejecutar la consola de Configuration Manager en un equipo que admite el tipo de EAP seleccionado.

    - **Recordar las credenciales de usuario en cada inicio de sesión**: seleccione esta opción para almacenar las credenciales de usuario a fin de que los usuarios no tengan que escribir las credenciales de red inalámbrica cada vez que inicien sesión en Windows.

1. En la página **Configuración avanzada** del asistente, especifique la configuración adicional para el perfil de Wi-Fi. Es posible que la configuración avanzada no esté disponible o que pueda variar según las opciones seleccionadas en la página **Configuración de seguridad** del asistente. Por ejemplo, el modo de autenticación o las opciones de inicio de sesión único.

1. En la página **Configuración de proxy**, si la red inalámbrica usa un servidor proxy, active la opción **Configurar proxy para este perfil Wi-Fi**. A continuación, proporcione la información de configuración para el proxy.

1. En la página **Plataformas compatibles**, seleccione las versiones del sistema operativo en las que se aplica este perfil de Wi-Fi.

1. Complete el asistente.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Implementación de perfiles de Wi-Fi](deploy-wifi-vpn-email-cert-profiles.md)
