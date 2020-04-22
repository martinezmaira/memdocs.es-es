---
title: 'Configuración de restricciones de dispositivos Windows 8.1 en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Descubra las opciones de configuración de Intune que puede usar para controlar la funcionalidad y la configuración de los dispositivos que ejecutan Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59af48b36cb9c76ce7587457d4921356f542493f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407664"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Configuración de restricciones de dispositivos Windows 8.1 de Microsoft Intune

En este artículo se muestra la configuración de restricciones de dispositivos de Microsoft Intune que se puede aplicar a los dispositivos con Windows 8.1.

## <a name="general"></a>General

- **Compartir los datos de uso**: **Bloquear** impide que los dispositivos envíen a Microsoft información de diagnóstico y datos de telemetría de uso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Firewall**: **requiera** que el firewall de Windows esté activado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Control de cuentas de usuario**: configura el Control de cuentas de usuario (UAC). Elija cómo se notifican a los usuarios los cambios en los dispositivos. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Notificarme siempre**
  - **Notificar cambios de aplicaciones**
  - **Notificar cambios de aplicaciones (no atenuar escritorio)**
  - **No notificarme nunca**

## <a name="password"></a>Contraseña

- **Tipo de contraseña requerida**: seleccione si el usuario debe especificar una contraseña para acceder al dispositivo. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Alfanumérica**: la contraseña debe ser una combinación de letras y números.
  - **Numérica**: la contraseña solo debe contener números.
- **Longitud mínima de la contraseña**: escriba el número mínimo de caracteres requeridos, de 6 a 16. Por ejemplo, escriba `6` para exigir al menos seis números o caracteres de longitud de la contraseña.
- **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borre el dispositivo, entre 1 y 14.
- **Máximo de minutos de inactividad hasta que se bloquea la pantalla (en minutos)** : escriba el tiempo durante el que un dispositivo debe estar inactivo antes de que se bloquee automáticamente la pantalla, de 1 a 60 minutos. Por ejemplo, escriba `5` para bloquear el dispositivo tras estar 5 minutos inactivo. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
- **Expiración de la contraseña (días)** : especifique el periodo de tiempo en días tras el cual debe cambiarse la contraseña del dispositivo, de 1 a 255. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Impedir la reutilización de contraseñas anteriores**: escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **PIN y contraseña de imagen**: **Bloquear** impide el uso de una imagen o un PIN como contraseña. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Una contraseña de imagen permite que el usuario inicie sesión mediante gestos en una imagen. Un PIN permite que los usuarios inicien sesión rápidamente con un código de cuatro dígitos.
- **Cifrado**: **requiera** el cifrado en los dispositivos, incluido en los archivos. No todos los dispositivos admiten el cifrado. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

  Para configurar esta opción y notificar correctamente el cumplimiento, configure también lo siguiente:
  - **Tipo de contraseña requerida**: establézcala en al menos **Numérica**.
  - **Longitud mínima de la contraseña**: establézcala en al menos `4`.

  Para forzar el cifrado en los dispositivos que ejecutan Windows 8.1, debe instalar la [Actualización de cliente de diciembre de 2014 MDM en Windows](https://support.microsoft.com/kb/3013816) en cada dispositivo.

  Si habilita esta configuración para dispositivos Windows 8.1, todos los usuarios del dispositivo deben tener una cuenta de Microsoft.

  Para que el cifrado funcione, los dispositivos deben cumplir los requisitos de certificación de hardware de [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97).

  Al exigir el cifrado en un dispositivo, solo se puede obtener acceso a la clave de recuperación desde la cuenta Microsoft de los usuarios, a la que se obtiene acceso desde su cuenta de OneDrive. No se puede recuperar esta clave para un usuario.

## <a name="browser"></a>Explorador

- **Autorrelleno**: **Bloquear** impide que los usuarios cambien la configuración de Autocompletar en el explorador y que los campos de formulario se rellenen automáticamente. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la característica Autorrellenar.
- **Advertencias de fraude**: **Requerir** muestra advertencias de fraude en el explorador en el caso de posibles sitios web fraudulentos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **SmartScreen para Microsoft Edge**: **Bloquear** desactiva SmartScreen de Microsoft Defender. SmartScreen busca posibles correos de suplantación de identidad (phishing) y software malintencionado cuando se accede a sitios y descargas de archivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría activar SmartScreen.
- **JavaScript**: **Bloquear** impide que se ejecuten scripts en el explorador, como JavaScript. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Elementos emergentes**: **Bloquear** activa el bloqueador de elementos emergentes para impedir que estos aparezcan en el explorador web. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Encabezados de no seguimiento**: **Bloquear** impide que el dispositivo envíe encabezados de no seguimiento a los sitios web que soliciten información de seguimiento. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Complementos**: **Bloquear** impide que los usuarios agreguen complementos en Internet Explorer. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Entrada de palabra única en el sitio de la intranet**: la entrada de palabra única permite a los usuarios ir a un sitio de intranet escribiendo una sola palabra, como `hr` o `benefits`. **Bloquear** impide esta característica. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Detección automática del sitio de intranet**: **Bloquear** impide que el explorador detecte automáticamente los sitios de intranet. Las reglas de asignación de intranet están bloqueadas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Nivel de seguridad de Internet**: establece el nivel de seguridad para sitios de Internet. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Media**
  - **Medio-alto**
  - **Alta**
- **Nivel de seguridad de la intranet**: establece el nivel de seguridad para sitios de intranet. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Baja**
  - **Medio-bajo**
  - **Media**
  - **Medio-alto**
  - **Alta**
- **Nivel de seguridad de sitios de confianza**: Configura el nivel de seguridad para la zona de sitios de confianza. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Baja**
  - **Medio-bajo**
  - **Media**
  - **Medio-alto**
  - **Alta**
- **Nivel de seguridad alto para sitios restringidos**: Configura el nivel de seguridad para la zona de sitios restringidos. **Configurado** exige un nivel de seguridad alto para los sitios restringidos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Acceso al menú Modo de empresa**: **Bloquear** impide que los usuarios accedan a las opciones del menú Modo de empresa en Internet Explorer. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Si se establece en **Bloquear**, especifique también lo siguiente:
  - **URL de ubicación del informe de registro**: escriba una ubicación de URL donde obtener informes que muestren los sitios web con el acceso en modo de empresa activado.
- **Ubicación de la lista de sitios del modo de empresa (solo escritorio)** : especifique la ubicación de la lista de sitios web que se pueden abrir en modo de empresa.

## <a name="cellular"></a>Móvil

- **Itinerancia de datos**: **Bloquear** impide la itinerancia de datos cuando los dispositivos están en una red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="cloud-and-storage"></a>Nube y almacenamiento

- **Dirección URL de carpetas de trabajo**: especifique la dirección URL de la carpeta de trabajo para permitir que los documentos se sincronicen en todos los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado) o se deja en blanco, Intune no cambia ni actualiza esta configuración.
- **Acceso a la aplicación Correo de Windows sin una cuenta Microsoft**: **Bloquear** impide el acceso a la aplicación Correo de Windows sin una cuenta Microsoft. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="next-steps"></a>Pasos siguientes

Cree un perfil de restricciones de dispositivos en [Windows 10 y versiones más recientes](device-restrictions-windows-10.md).
