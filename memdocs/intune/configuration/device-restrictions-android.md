---
title: 'Configuración de restricciones de dispositivos para Android en Microsoft Intune: Azure | Microsoft Docs'
description: Vea una lista de todas las configuraciones de administrador de dispositivos Android que puede controlar y restringir en Microsoft Intune. Use estos valores para controlar la contraseña, acceder a Google Play, permitir o prohibir aplicaciones, controlar la configuración del explorador, bloquear aplicaciones, hacer una copia de seguridad en la nube de Google y controlar las opciones de conexión de Bluetooth, Wi-Fi, itinerancia de datos, voz y mensaje.
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
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407866"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Listas de configuraciones de restricciones de dispositivos Android y Samsung Knox en Intune

En este artículo, se muestran todas las opciones de configuración de restricciones de dispositivos de Microsoft Intune que puede configurar para los dispositivos que ejecutan Android.

>[!TIP]
>Si la configuración que quiere no está disponible, es posible que pueda configurar sus dispositivos con un [perfil personalizado](custom-settings-android.md).

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de dispositivo](device-restrictions-configure.md).

## <a name="general"></a>General

- **Cámara**: **Bloquear** impide el acceso a la cámara del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara del dispositivo.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.

- **Copiar y pegar (solo Samsung Knox)** : **Bloquear** impide copiar y pegar. **No configurado** permite las funciones de copiar y pegar en los dispositivos.
- **Uso compartido del Portapapeles entre aplicaciones (solo Samsung Knox)** : **Bloquear** impide el uso del Portapapeles para copiar y pegar entre aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir las funciones de copiar y pegar en los dispositivos.
- **Envío de datos de diagnóstico (solo Samsung Knox)** : **Bloquear** impide que los usuarios envíen informes de errores desde dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios envíen datos.
- **Borrar (solo Samsung Knox)** : permite a los usuarios ejecutar una acción de [borrado](../remote-actions/devices-wipe.md) en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Geolocalización (solo Samsung Knox)** : **Bloquear** deshabilita el uso de la información de ubicación de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los dispositivos usen la información de ubicación.
- **Desconectar (solo Samsung Knox)** : **Bloquear** impide que los usuarios apaguen el dispositivo. También impide que la opción **Número de errores de inicio de sesión antes de borrar el dispositivo** se configure y funcione. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios apaguen dispositivos.
- **Captura de pantalla (solo Samsung Knox)** : **Bloquear** impide las capturas de pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De manera predeterminada, el sistema operativo podría permitir que los usuarios capturen el contenido de la pantalla como una imagen.
- **Asistente de voz (solo Samsung Knox)** : **Bloquear** deshabilita el servicio S Voice. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso del servicio y la aplicación S Voice en los dispositivos. Esta configuración no se aplica a Bixby ni al asistente de voz de accesibilidad que lee el contenido de la pantalla en voz alta.
- **YouTube (solo Samsung Knox)** : **Bloquear** impide que los usuarios usen la aplicación YouTube. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación YouTube en los dispositivos.
- **Dispositivos compartidos (solo Samsung Knox)** : configure un dispositivo Samsung Knox Standard administrado como compartido. **Permitir** habilita a los usuarios para iniciar y cerrar sesión en los dispositivos con sus credenciales de Azure AD. Los dispositivos permanecen administrados, tanto si se están usando como si no.

  Cuando se usa con un perfil de certificado SCEP, esta característica permite que los usuarios compartan un dispositivo con las mismas aplicaciones para todos los usuarios. Sin embargo, cada usuario tiene su propio certificado de usuario SCEP. Cuando los usuarios cierran sesión, se borran todos los datos de la aplicación. Esta característica se limita a las aplicaciones LOB.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que varios usuarios finales inicien sesión en la aplicación Portal de empresa en los dispositivos con sus credenciales de Azure AD.
- **Bloquear cambios de fecha y hora (Samsung Knox)** : **Bloquear** impide que los usuarios cambien la configuración de fecha y hora en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de fecha y hora.

## <a name="password"></a>Contraseña

- **Contraseña**: **Requerir** que los usuarios escriban una contraseña para acceder a los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios accedan a los dispositivos sin tener que escribir una contraseña.

    > [!NOTE]
    > Los dispositivos Samsung Knox requieren automáticamente un PIN de 4 dígitos durante la inscripción de MDM. Es posible que los dispositivos nativos de Android requieran automáticamente un PIN para ser compatibles con el acceso condicional.

- **Longitud mínima de la contraseña**: escriba el número mínimo de caracteres requeridos, de 4 a 16. Por ejemplo, escriba `6` para exigir al menos seis números o caracteres de longitud de la contraseña.
- **Máximo de minutos de inactividad hasta que se bloquea la pantalla**: escriba el tiempo durante el cual un dispositivo debe estar inactivo antes de que se bloquee automáticamente la pantalla. Por ejemplo, escriba `5` para bloquear los dispositivos tras estar 5 minutos inactivos. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

  En un dispositivo, los usuarios no pueden establecer un valor de tiempo mayor que el tiempo configurado en el perfil. Los usuarios pueden establecer un valor de tiempo menor. Por ejemplo, si el perfil está establecido en `15` minutos, los usuarios pueden establecer el valor en 5 minutos. Pero no podrán establecerlo en 30 minutos.

- **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borren los dispositivos, entre 4 y 11. `0` (cero) puede deshabilitar la función de borrado del dispositivo. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Expiración de la contraseña (días)** : escriba el número de días, entre 1 y 365, hasta que se deba cambiar la contraseña del dispositivo. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando la contraseña expire, se le solicitará a los usuarios que creen una nueva contraseña. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Tipo de contraseña requerida**: especifique el nivel requerido de complejidad de la contraseña y si se pueden usar dispositivos biométricos. Las opciones son:
  - **Valor predeterminado de dispositivo**
  - **Biométrico de seguridad baja**: [Biométricas eficientes frente a deficientes](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre el sitio web de Android)
  - **Al menos numérica**: Incluye caracteres numéricos, como `123456789`.
  - **Numérica compleja**: no se permiten números repetidos ni consecutivos, como "1111" o "1234". Antes de asignar esta configuración a los dispositivos, asegúrese de actualizar la aplicación Portal de empresa a la versión más reciente en esos dispositivos.

    Cuando se establece en **Numérica compleja** y se asigna la configuración a los dispositivos que ejecutan una versión de Android anterior a la 5.0, se aplica el comportamiento siguiente:

    - Si la aplicación Portal de empresa ejecuta una versión anterior a 1704, no se aplica ninguna directiva de PIN a los dispositivos y se muestra un error en el Centro de administración de Microsoft Endpoint Manager.
    - Si la aplicación del Portal de empresa ejecuta la versión 1704 o una versión posterior, solo se puede aplicar un PIN sencillo. Las versiones de Android anteriores a la 5.0 no admiten esta configuración. No se muestra ningún error en el Centro de administración de Microsoft Endpoint Manager.

  - **Al menos alfabética**: incluye letras del alfabeto. No son necesarios números ni símbolos.
  - **Al menos alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos.
  - **Al menos alfanumérica con símbolos**: incluye letras mayúsculas, minúsculas, caracteres numéricos, signos de puntuación y símbolos.

- **Impedir la reutilización de contraseñas anteriores**: utilice esta configuración para impedir que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Desbloqueo de huella digital (solo Samsung Knox)** : **Bloquear** impide el uso de una huella digital para desbloquear los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios desbloqueen dispositivos con una huella digital.
- **Smart Lock y otros agentes de confianza**: **Bloquear** impide que Smart Lock u otros agentes de confianza ajusten la configuración de la pantalla de bloqueo. Si el dispositivo está en una ubicación de confianza, esta característica, conocida también como agente de confianza, permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo. Por ejemplo, use esta característica cuando los dispositivos estén conectados a un dispositivo Bluetooth específico o cuando estén cerca de una etiqueta de NFC. Puede usar esta opción para impedir que los usuarios configuren Smart Lock.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  Esta configuración solo es aplicable a:

  - Samsung KNOX Standard 5.0 y versiones posteriores

- **Cifrado**: seleccione **Requerir** para que se cifren los archivos del dispositivo. No todos los dispositivos admiten el cifrado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Para configurar esta opción y notificar correctamente el cumplimiento, configure también lo siguiente:
  1. **Contraseña**: establézcala en **Requerir**.
  2. **Tipo de contraseña requerida**: establézcala en **Al menos numérica**.
  3. **Longitud mínima de la contraseña**: establézcala en al menos `4`.

  > [!NOTE]
  > Si se aplica una directiva de cifrado, los dispositivos Samsung Knox requieren que los usuarios establezcan una contraseña compleja de 6 caracteres como el código de acceso del dispositivo.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (solo Samsung Knox)** : **Bloquear** impide que los usuarios usen Google Play Store. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios accedan a Google Play Store en los dispositivos.

## <a name="restricted-apps"></a>Aplicaciones restringidas

Use esta configuración para permitir o impedir aplicaciones específicas en los dispositivos. Esta característica es compatible con dispositivos Android y Samsung Knox Standard.

- **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
- **Aplicaciones prohibidas**: enumere las aplicaciones (que no se administran mediante Intune) que los usuarios no pueden instalar ni ejecutar. Si un usuario instala una aplicación de esta lista, recibirá una notificación a través de Intune.
- **Aplicaciones aprobadas**: Enumerar las aplicaciones que los usuarios pueden instalar. Para mantener el cumplimiento, los usuarios no deben instalar otras aplicaciones.  Las aplicaciones que se administran mediante Intune están permitidas automáticamente, incluido el Portal de empresa.
- **Lista de aplicaciones**: **agregue** la aplicación:
  - **Identificador de lote de aplicaciones**: escriba el id. del conjunto de la aplicación.
  - **URL de App Store**: escriba la dirección URL de Google Play Store de la aplicación que quiere. Por ejemplo, para agregar la aplicación Escritorio remoto de Microsoft para Android, escriba `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    Para buscar la dirección URL	 de una aplicación, abra [Google Play Store](https://play.google.com/store/apps) y busque la aplicación. Por ejemplo, busque `Microsoft Remote Desktop Play Store` o `Microsoft Planner`. Seleccione la aplicación y copie la dirección URL.
  
  - **Nombre de la aplicación**: escriba el nombre que quiera. Este nombre se muestra a los usuarios.
  - **Publicador** (opcional): introduzca el publicador de la aplicación como, por ejemplo, `Microsoft`.

También puede **Importar** un archivo .csv con detalles sobre la aplicación, incluida la dirección URL. Use el formato <*dirección URL de la aplicación*>, <*nombre de la aplicación*>, <*editor de la aplicación*>. O bien **exporte** una lista existente que incluye la lista de aplicaciones restringidas en el mismo formato.

> [!IMPORTANT]
> Se deben asignar perfiles de dispositivo que usen configuración de aplicaciones restringidas para grupos de usuarios, no para grupos de dispositivos.

## <a name="browser"></a>Explorador

- **Explorador web (solo Samsung Knox)** : **Bloquear** impide que se use el explorador web predeterminado en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que se use el explorador web predeterminado del dispositivo.
- **Autorrellenar (solo Samsung Knox)** : **Bloquear** impide que el explorador rellene automáticamente el texto. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la característica Autorrellenar.
- **Cookies (solo Samsung Knox)** : elija cómo controlar las cookies de los sitios web en los dispositivos. Las opciones son:
  - Allow
  - Bloquear todas las cookies
  - Permitir cookies de sitios web visitados
  - Permitir cookies del sitio web actual
- **JavaScript (solo Samsung Knox)** : **Bloquear** impide la ejecución de JavaScript en el explorador. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estos scripts.
- **Elementos emergentes (solo Samsung Knox)** : **Bloquear** activa el bloqueador de elementos emergentes para impedir que estos aparezcan en el explorador web. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir los elementos emergentes.

## <a name="allow-or-block-apps"></a>Permiso o bloqueo para aplicaciones

Use esta configuración para permitir, bloquear u ocultar aplicaciones específicas en dispositivos Samsung Knox Standard. Los usuarios no puede abrir ni ejecutar las aplicaciones ocultas.

Las opciones son:

- **Aplicaciones cuya instalación se permite (solo Samsung Knox Standard)** : agregue las aplicaciones que los usuarios pueden instalar. No pueden instalar aplicaciones que no estén en la lista.
- **Aplicaciones cuyo inicio está bloqueado (solo Samsung Knox Standard)** : introduzca las aplicaciones que los usuarios no pueden ejecutar en su dispositivo.
- **Aplicaciones ocultas para el usuario (solo Samsung Knox Standard)** : indique las aplicaciones que están ocultas en los dispositivos. Los usuarios no pueden detectar ni ejecutar estas aplicaciones.

Agregue sus aplicaciones para cada configuración:

- **Agregar aplicaciones por nombre de paquete**: Escriba el nombre de la aplicación y el nombre del paquete de la aplicación. se usa fundamentalmente para aplicaciones de línea de negocio. 
- **Agregar aplicaciones por URL**: especifique el nombre de la aplicación y su dirección URL en Google Play Store.
- **Agregar aplicación de la tienda**: seleccione una aplicación de la lista de aplicaciones existente que administra en Intune.

## <a name="cloud-and-storage"></a>Nube y almacenamiento

- **Copia de seguridad de Google (solo Samsung Knox)** : **Bloquear** impide que los dispositivos se sincronicen con la copia de seguridad de Google. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la copia de seguridad de Google.
- **Sincronización automática de la cuenta de Google (solo Samsung Knox)** : **Bloquear** impide la característica de sincronización automática de la cuenta de Google en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la configuración de la cuenta de Google se sincronice automáticamente.
- **Almacenamiento extraíble (solo Samsung Knox)** : **Bloquear** impide que los dispositivos usen almacenamiento extraíble. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los dispositivos usen almacenamiento extraíble, como una tarjeta SD.
- **Cifrado en tarjetas de almacenamiento (solo Samsung Knox)** : **Requerir** exige que las tarjetas de almacenamiento se cifren. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de tarjetas de almacenamiento no cifradas. No todos los dispositivos admiten el cifrado de tarjetas de almacenamiento. Para confirmar, consulte con el fabricante del dispositivo.

## <a name="cellular-and-connectivity"></a>Red de telefonía móvil y conectividad

- **Itinerancia de datos (solo Samsung Knox)** : **Bloquear** impide la itinerancia de datos a través de la red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la itinerancia de datos.
- **Mensajería SMS/MMS (solo Samsung Knox)** : **Bloquear** impide la mensajería de texto en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la mensajería SMS y MMS.
- **Marcación por voz (solo Samsung Knox)** : **Bloquear** impide que los usuarios usen la característica de marcación por voz en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la marcación por voz.
- **Itinerancia de voz (solo Samsung Knox)** : **Bloquear** impide la itinerancia de voz a través de la red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la itinerancia de voz.
- **Bluetooth (solo Samsung Knox)** : **Bloquear** impide el uso de Bluetooth en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Bluetooth.
- **NFC (solo Samsung Knox)** : **Bloquear** deshabilita las operaciones que usen transmisión de datos en proximidad (NFC) en dispositivos compatibles. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir las operaciones de NFC.
- **Wi-Fi (solo Samsung Knox)** : **Bloquear** impide el uso de Wi-Fi en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Wi-Fi.
- **Tethering Wi-Fi (solo Samsung Knox)** : **Bloquear** impide el uso de Tethering Wi-Fi en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Tethering Wi-Fi.

## <a name="kiosk"></a>Pantalla completa

La configuración de pantalla completa solo se aplica a dispositivos Samsung Knox Standard y exclusivamente a las aplicaciones que administra mediante Intune.

- Agregue las aplicaciones que quiere ejecutar cuando el dispositivo está en pantalla completa. En pantalla completa, solo se ejecutan las aplicaciones que se agregan; las que no se agregan no se ejecutan. Los exploradores instalados previamente no se ejecutan como aplicación cuando el dispositivo está en modo de pantalla completa. Si se necesita un explorador, puede utilizar [Managed Browser](../apps/app-configuration-managed-browser.md).

  Las opciones de la aplicación:

  - **Agregar aplicaciones por nombre de paquete**: se usa fundamentalmente para aplicaciones de línea de negocio. Escriba el nombre de la aplicación y el nombre del paquete de la aplicación.
  - **Agregar aplicaciones por URL**: especifique el nombre de la aplicación y su dirección URL en Google Play Store.
  - **Agregar aplicación de la tienda**: seleccione una aplicación de la lista de aplicaciones existente que administra en Intune.

- **Botón de suspensión de pantalla**: **Bloquear** impide u oculta el botón de suspensión de pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el botón de reposo/activación de pantalla en los dispositivos.
- **Botones de volumen**: **Bloquear** impide que los usuarios ajusten el volumen al deshabilitar los botones de volumen. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de los botones de volumen en los dispositivos.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede crear perfiles de pantalla completa para dispositivos [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) y [Windows 10](kiosk-settings.md).
