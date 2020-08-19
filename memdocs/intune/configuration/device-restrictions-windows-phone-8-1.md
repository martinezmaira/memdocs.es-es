---
title: Configuración de restricciones de dispositivos de Microsoft Intune para Windows Phone 8.1
titleSuffix: ''
description: Descubra las opciones de configuración de Intune que puede usar para controlar la funcionalidad y la configuración de los dispositivos que ejecutan Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a655ea2c3770e00ccc685cbe9d59f0fe7e49cd6
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146225"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Configuración de restricciones de dispositivos Windows Phone 8.1 de Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

En este artículo, se muestran las opciones de configuración de restricciones de dispositivos de Microsoft Intune que puede configurar para los dispositivos que ejecutan Windows Phone 8.1.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de restricciones de dispositivos de Windows Phone 8.1](device-restrictions-configure.md).

## <a name="general"></a>General

- **Cámara**: **Bloquear** impide el acceso a la cámara del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.

- **Copiar y pegar**: **Bloquear** impide el uso de Copiar y pegar entre aplicaciones en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Almacenamiento extraíble**: **Bloquear** impide el uso de dispositivos de almacenamiento externo en los dispositivos, como tarjetas SD. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Geolocalización**: **Bloquear** impide la activación de servicios de ubicación en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Cuenta Microsoft**: **Bloquear** impide que los usuarios asocien una cuenta Microsoft al dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Captura de pantalla**: **Bloquear** impide obtener capturas de pantallas en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Envío de datos de diagnóstico**: **Bloquear** impide que los dispositivos envíen datos de telemetría de uso y diagnóstico a Microsoft. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Sincronización de cuentas de correo electrónico personalizadas**: **Bloquear** impide que los dispositivos se conecten a cuentas de correo electrónico que no sean de Microsoft. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="password"></a>Contraseña

- **Contraseña**: **Requerir** que los usuarios escriban una contraseña para acceder a los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Solo se aplica a cuentas locales. Las contraseñas de las cuentas de dominio siguen siendo configuradas por Active Directory (AD) y Azure AD.
  - **Tipo de contraseña requerida**: elija el tipo de contraseña. Las opciones son:
    - **Valor predeterminado del dispositivo**: la contraseña puede incluir números y letras.
    - **Alfanumérica**: la contraseña debe ser una combinación de letras y números.
    - **Numérica**: la contraseña solo debe contener números.
  - **Longitud mínima de la contraseña**: escriba el número mínimo de caracteres requeridos, de 4 a 16. Por ejemplo, escriba `6` para exigir al menos seis caracteres de longitud de la contraseña.
  - **Contraseñas sencillas**: **Bloquear** impide que los usuarios creen contraseñas sencillas, como `1234` o `1111`. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borren los dispositivos.
  - **Máximo de minutos de inactividad hasta que se bloquea la pantalla**: escriba el tiempo durante el cual un dispositivo debe estar inactivo antes de que se bloquee automáticamente la pantalla. Por ejemplo, escriba `5` para bloquear los dispositivos tras estar 5 minutos inactivos. Cuando se establece en **Sin configurar** o se deja en blanco, Intune no cambia ni actualiza esta configuración.
  - **Expiración de la contraseña (días)** : especifique el periodo de tiempo en días tras el cual debe cambiarse la contraseña del dispositivo, de 1 a 255. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
  - **Impedir la reutilización de contraseñas anteriores**: escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Cifrado**: **Requerir** el cifrado en el dispositivo, incluido en los archivos. No todos los dispositivos admiten el cifrado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Para configurar esta opción y notificar correctamente el cumplimiento, configure también lo siguiente:
  - **Requerir contraseña**: establézcala en **Requerir**.
  - **Tipo de contraseña requerida**: establézcala en al menos **Numérica**.
  - **Longitud mínima de la contraseña**: establézcala en al menos `4`.

## <a name="app-store"></a>Tienda de aplicaciones

- **Tienda de aplicaciones**: **Bloquear** impide que los usuarios accedan a la tienda de aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="restricted-apps"></a>Aplicaciones restringidas

En la lista de aplicaciones restringidas, puede configurar una de las listas siguientes:

- **Aplicaciones bloqueadas**: Enumerar las aplicaciones (que no se administran mediante Intune) que los usuarios no pueden instalar ni ejecutar.
- **Aplicaciones permitidas**: Enumerar las aplicaciones que los usuarios pueden instalar. Las aplicaciones que se administran mediante Intune están permitidas automáticamente.

Para configurar la lista, haga clic en **Agregar** y especifique un nombre de su elección. Opcionalmente, puede indicar el editor de la aplicación y la dirección URL de la aplicación en la tienda de aplicaciones.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Especificación de la dirección URL para una aplicación de la tienda

Para especificar la dirección URL de una aplicación en la lista de aplicaciones permitidas y bloqueadas, use el siguiente formato:

Desde la página de la [Tienda de Windows Phone](https://www.microsoft.com/store/apps/windows-phone), busque la aplicación que quiere usar.

Abra la página de la aplicación y copie la dirección URL en el Portapapeles. Ya puede usarla como dirección URL en la lista de aplicaciones permitidas o bloqueadas.

Ejemplo: Busque en la tienda la aplicación Skype. La dirección URL usada es `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Opciones adicionales

También puede hacer clic en **Importar** para rellenar la lista a partir de un archivo .csv con el formato <*dirección URL de aplicación*>, <*nombre de aplicación*>, <*editor de aplicación*> o en **Exportar** para crear un archivo .csv que contenga la lista de aplicaciones restringidas en el mismo formato.

## <a name="browser"></a>Explorador

- **Explorador web**: **Bloquear** desactiva el explorador web integrado en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="cellular-and-connectivity"></a>Red de telefonía móvil y conectividad

- **Wi-Fi**: **Bloquear** deshabilita la función de Wi-Fi de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Tethering Wi-Fi**: **Bloquear** impide el uso de Tethering Wi-Fi en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Conectar automáticamente a zonas Wi-Fi**: Permite que los dispositivos se conecten automáticamente a zonas Wi-Fi gratuitas y acepte automáticamente las condiciones de uso.
- **Informes de zonas Wi-Fi**: **Bloquear** impide que los dispositivos envíen información de conexión de zonas Wi-Fi. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **NFC**: **Bloquear** deshabilita las operaciones que usen transmisión de datos en proximidad (NFC) en dispositivos compatibles. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Bluetooth**: **Bloquear** evita que los usuarios habiliten Bluetooth. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información general sobre el perfil de restricciones de dispositivos, vea [Configurar restricciones de dispositivos en Microsoft Intune](device-restrictions-configure.md).
