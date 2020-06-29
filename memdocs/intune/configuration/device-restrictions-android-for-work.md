---
title: Configuración de dispositivos de Android Enterprise en Microsoft Intune (Azure) | Microsoft Docs
description: En dispositivos Android Enterprise o Android for Work, restrinja opciones de configuración en el dispositivo, como copiar y pegar; mostrar notificaciones; permisos de aplicación; uso compartido de datos; longitud de contraseña; errores de inicio de sesión; usar huella digital para desbloquear; reutilizar contraseñas y habilitar el uso compartido de los contactos de trabajo mediante Bluetooth. Configure los dispositivos en modo de pantalla completa de dispositivo dedicado para ejecutar una o varias aplicaciones.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88843cfa1c4f98d87e5eaaefdc0dcd87daf8cb68
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093714"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Configuración de dispositivos Android Enterprise para permitir o restringir características mediante Intune

En este artículo se enumeran y describen los diferentes valores de configuración que puede controlar en los dispositivos Android y Android Enterprise. Como parte de la solución de administración de dispositivos móviles (MDM), use estos valores de configuración para habilitar o deshabilitar características, ejecutar aplicaciones en dispositivos dedicados, controlar la seguridad y mucho más.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de dispositivo](device-restrictions-configure.md).

## <a name="device-owner-only"></a>Solo el propietario del dispositivo

Esta configuración se aplica a los tipos de inscripción Android Enterprise en los que Intune controla todo el dispositivo, como los Android Enterprise totalmente administrados o dedicados.

### <a name="general"></a>General

- **Captura de pantalla**: **Bloquear** impide que se hagan capturas de pantalla en el dispositivo. Además evita que el contenido se muestre en los dispositivos de pantalla que no tengan una salida de vídeo segura. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De manera predeterminada, el sistema operativo podría permitir que los usuarios capturen el contenido de la pantalla como una imagen.
- **Cámara**: **Bloquear** impide el acceso a la cámara del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.

- **Directiva de permisos predeterminada**: con esta opción se define la directiva de permisos predeterminada para las solicitudes de permisos en tiempo de ejecución. Las opciones son las siguientes:
  - **Valor predeterminado del dispositivo**: use la configuración predeterminada del dispositivo.
  - **Símbolo del sistema**: se solicita a los usuarios que aprueben el permiso.
  - **Concesión automática**: los permisos se conceden automáticamente.
  - **Denegación automática**: los permisos se deniegan automáticamente.
- **Cambios de fecha y hora**: **Bloquear** impide que los usuarios configuren manualmente la fecha y hora. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios establezcan la fecha y hora en el dispositivo.
- **Cambios de volumen**: **Bloquear** impide que los usuarios cambien el volumen del dispositivo y silencia el volumen maestro. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen la configuración de volumen en el dispositivo.
- **Restablecimiento de la configuración de fábrica**: **Bloquear** impide que los usuarios usen la opción de restablecimiento de fábrica en la configuración del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen esta configuración en el dispositivo.
- **Arranque seguro**: **Bloquear** impide que los usuarios reinicien el dispositivo en modo seguro. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios reinicien el dispositivo en modo seguro.
- **Barra de estado**: **Bloquear** impide el acceso a la barra de estado, incluidas las notificaciones y las opciones de configuración rápida. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios accedan a la barra de estado.
- **Servicios de datos de itinerancia**: **Bloquear** impide la itinerancia de datos a través de la red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la itinerancia de datos cuando el dispositivo está en una red de telefonía móvil.
- **Cambios en la configuración de Wi-Fi**: **Bloquear** impide que los usuarios cambien la configuración de Wi-Fi que ha creado el propietario del dispositivo. Los usuarios pueden crear sus propias configuraciones de Wi-Fi. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de Wi-Fi del dispositivo.
- **Configuración de punto de acceso Wi-Fi**: **Bloquear** impide que los usuarios creen o cambien las configuraciones de Wi-Fi. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de Wi-Fi del dispositivo.
- **Configuración de Bluetooth**: **Bloquear** impide que los usuarios configuren Bluetooth en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Bluetooth en el dispositivo.
- **Tethering and access to hotspots** (Acceso a zonas y tethering): **Bloquear** impide el tethering y el acceso a zonas Wi-Fi portátiles. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el tethering y el acceso a zonas Wi-Fi portátiles.
- **Almacenamiento USB**: elija **Permitir** para acceder al almacenamiento USB en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir el acceso al almacenamiento USB.
- **USB file transfer** (Transferencia de archivos USB): **Bloquear** impide la transferencia de archivos a través de USB. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la transferencia de archivos.
- **External media** (Medios externos): **Bloquear** impide usar o conectar cualquier soporte físico en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir los soportes físicos externos en el dispositivo.
- **Beam data using NFC** (Transferir datos mediante NFC): **Bloquear** impide el uso de la tecnología Transmisión de datos en proximidad (NFC) para transferir datos desde las aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de NFC para compartir datos entre dispositivos.
- **Características de depuración**: elija **Permitir** para permitir que los usuarios usen las características de depuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los usuarios usen las características de depuración en el dispositivo.
- **Ajuste del micrófono**: **Bloquear** impide que los usuarios silencien el micrófono y ajusten su volumen. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios usar y ajustar el volumen del micrófono en el dispositivo.
- **Correos electrónicos de protección frente al restablecimiento de fábrica**: elija **Direcciones de correo electrónico de la cuenta de Google**. Escriba las direcciones de correo electrónico del dispositivo que los administradores pueden desbloquear una vez que se eliminan los datos del dispositivo. Asegúrese de separar las direcciones de correo electrónico con punto y coma, como en `admin1@gmail.com;admin2@gmail.com`. Si no se especificó ningún correo electrónico, cualquier usuario puede desbloquear el dispositivo una vez que se restaura la configuración de fábrica. Estos correos electrónico solo se aplican al ejecutar un restablecimiento de fábrica que no es de usuario, como la ejecución de un restablecimiento de fábrica mediante el menú recuperación.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

- **Trampilla de escape de red**: **Habilitar** permite que los usuarios activen la característica de trampilla de escape de red. Si no se realiza una conexión de red cuando se inicia el dispositivo, la ruta de escape pide conectarse de manera temporal a una red y actualizar la directiva del dispositivo. Después de aplicar la directiva, la red temporal se olvida y el dispositivo sigue arrancando. Esta característica conecta dispositivos a una red si:
  - No hay ninguna red adecuada en la última directiva.
  - El dispositivo se inicia en una aplicación en modo de bloqueo de tareas.
  - Los usuarios no pueden acceder a la configuración del dispositivo.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los usuarios activen la característica de trampilla de escape de red en el dispositivo.

- **Actualización del sistema**: elija una opción para definir de qué forma funciona el dispositivo a través de las actualizaciones inalámbricas. Las opciones son las siguientes:
  - **Valor predeterminado del dispositivo**: use la configuración predeterminada del dispositivo.
  - **Automática**: las actualizaciones se instalan automáticamente sin intervención del usuario. Si se configura esta directiva se instalarán inmediatamente las actualizaciones pendientes.
  - **Pospuesta**: las actualizaciones se posponen durante 30 días. Cuando termine el período de 30 días, Android pedirá a los usuarios que instalen la actualización. Es posible que los fabricantes de dispositivos o los transportistas impidan que se pospongan actualizaciones de seguridad importantes (es decir, que las declaren como exentas). Una actualización exenta muestra a los usuarios una notificación del sistema en el dispositivo.
  - **Ventana de mantenimiento**: instala las actualizaciones automáticamente durante una ventana de mantenimiento diario configurada en Intune. La instalación se intenta diariamente durante 30 días y pueden producirse errores si los niveles de batería o espacio no son suficientes. Después de 30 días, Android solicitará a los usuarios que realicen la instalación. La ventana también se usa para instalar actualizaciones de aplicaciones de Google Play. Use esta opción para dispositivos dedicados, como pantallas completas, ya que las aplicaciones de primer plano de dispositivos dedicados de una sola aplicación se pueden actualizar.

- **Ventanas de notificación**: cuando se establece en **Deshabilitar**, las notificaciones de ventana, incluidas las notificaciones del sistema, las llamadas entrantes, las llamadas salientes, las alertas del sistema y los errores del sistema no se muestran en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las notificaciones.
- **Skip first use hints** (Omitir sugerencias de primer uso): **Habilitar** oculta u omite las sugerencias mostradas en los tutoriales de las aplicaciones o las que aparecen al iniciar la aplicación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar estas sugerencias cuando la aplicación se inicia.

### <a name="system-security"></a>Seguridad del sistema

- **Examen de amenazas en las aplicaciones**: **Requerir** (valor predeterminado) permite a Google Play Protect examinar las aplicaciones antes y después de instalarlas. Si se detecta una amenaza, puede avisar a los usuarios para que quiten la aplicación del dispositivo. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no habilite ni ejecute Google Play Protect para examinar aplicaciones.

### <a name="device-experience"></a>Experiencia del dispositivo

Use estas opciones para configurar una experiencia de tipo pantalla completa en los dispositivos dedicados o totalmente administrados. Puede configurar dispositivos para ejecutar una o muchas aplicaciones. Cuando un dispositivo se establece con pantalla completa, solo están disponibles las aplicaciones que agregue.

**Tipo de perfil de inscripción**: seleccione un tipo de perfil de inscripción para empezar a configurar Microsoft Launcher o Microsoft Managed Home Screen en los dispositivos. Las opciones son:

- **No configurado**: Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que los usuarios vean la experiencia de pantalla principal predeterminada del dispositivo.
- **Dispositivo dedicado**: Configure una experiencia de tipo pantalla completa en los dispositivos dedicados. Antes de configurar estas opciones, asegúrese de [agregar](../apps/apps-add-android-for-work.md) y [asignar](../apps/apps-deploy.md) las aplicaciones que quiera en los dispositivos.

  - **Pantalla completa**: elija si el dispositivo ejecuta una aplicación o varias. Las opciones son:

    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Aplicación única**: los usuarios solo pueden acceder a una aplicación. Cuando se inicia el dispositivo, solo se inicia la aplicación específica. los usuarios no pueden abrir nuevas aplicaciones ni modificar la aplicación en ejecución.

      - **Seleccionar una aplicación para usarla en modo de pantalla completa**: seleccione la aplicación administrada de Google Play en la lista.

      > [!IMPORTANT]
      > Cuando se usa el modo de pantalla completa de una sola aplicación, es posible que las aplicaciones de teléfono y marcado no funcionen correctamente.
  
    - **Varias aplicaciones**: los usuarios pueden acceder a un conjunto limitado de aplicaciones en el dispositivo. Cuando se inicia el dispositivo, solo se inician las aplicaciones que agrega. También puede agregar algunos vínculos web que los usuarios pueden abrir. Al aplicar la directiva, los usuarios ven los iconos de las aplicaciones permitidas en la pantalla principal.

      > [!IMPORTANT]
      > En los dispositivos dedicados con varias aplicaciones, la [aplicación Managed Home Screen](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) de Google Play **debe estar**:
      >   - [Agregado en Intune](../apps/apps-add-android-for-work.md)
      >   - [Asignada al grupo de dispositivos](../apps/apps-deploy.md) creado para los dispositivos dedicados
      >
      > No es necesario que la aplicación **Managed Home Screen** esté en el perfil de configuración, pero es obligatorio que se agregue como aplicación. Cuando se agrega la aplicación **Managed Home Screen**, cualquier otra que se agregue en el perfil de configuración aparece como icono en la aplicación **Managed Home Screen**.
      >
      > Cuando se usa la pantalla completa de varias aplicaciones, es posible que las aplicaciones de teléfono y marcado no funcionen correctamente. 

      - **Agregar**: seleccione las aplicaciones de la lista.

        Si la aplicación **Managed Home Screen** no aparece en la lista, [agréguela desde Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). No olvide [asignar la aplicación](../apps/apps-deploy.md) al grupo de dispositivos creado para los dispositivos dedicados.

        También puede agregar al dispositivo otras [aplicaciones Android](../apps/apps-add-android-for-work.md) y [aplicaciones web](../apps/web-app.md) creadas por la organización. No olvide [asignar la aplicación al grupo de dispositivos creado para los dispositivos dedicados](../apps/apps-deploy.md).

      - **Botón de inicio virtual**: botón de tecla programable que devuelve a los usuarios a Managed Home Screen para que puedan cambiar de aplicación. Las opciones son:
        - **Sin configurar** (valor predeterminado): No se muestra ningún botón Inicio. Los usuarios deben usar el botón Atrás para cambiar de aplicación.
        - **Deslizar rápidamente hacia arriba**: se muestra un botón Inicio cuando un usuario desliza rápidamente el dedo hacia arriba en el dispositivo.
        - **Flotante**: muestra un botón Inicio flotante y persistente en el dispositivo.

      - **Salir del modo de pantalla completa**: **Habilitar** permite que los administradores pausen temporalmente el modo de pantalla completa para actualizar el dispositivo. Para usar esta característica, el administrador hace lo siguiente:
  
        1. Continúa y hace clic en el botón de retroceso hasta que aparece el botón **Exit Kiosk** (Salir de pantalla completa). 
        2. Selecciona el botón **Exit kiosk** (Salir de pantalla completa) y escribe el PIN de **Leave kiosk mode code** (Código para salir del modo de pantalla completa).
        3. Cuando termine, seleccione la aplicación **Managed Home Screen**. Este paso vuelve a bloquear el dispositivo para pantalla completa con varias aplicaciones.

        Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los administradores pausen el modo de pantalla completa. Si el administrador sigue haciendo clic en el botón de retroceso y hace clic en el botón **Exit Kiosk** (Salir de pantalla completa), aparece un mensaje que indica que se requiere un código de acceso.

      - **Código para salir del modo de pantalla completa**: escriba un PIN numérico que tenga entre 4 y 6 dígitos. El administrador usa este PIN para pausar de manera temporal la pantalla completa.

      - **Establecer fondo personalizado de la dirección URL**: escriba una dirección URL para personalizar la pantalla de fondo del dispositivo dedicado. Por ejemplo, escriba `http://contoso.com/backgroundimage.jpg`.

        > [!NOTE]
        > Para la mayoría de los casos, se recomienda partir de imágenes cuyo tamaño es, al menos el siguiente:
        >
        > - Teléfono: 1080 x 1920 px
        > - Tableta: 1920 x 1080 px
        >
        > Para obtener la mejor experiencia y detalles nítidos, se recomienda crear activos de imagen por dispositivo con las especificaciones de pantalla.
        >
        > Las pantallas modernas tienen mayores densidades de píxeles y pueden mostrar imágenes que equivalen a definiciones 2K o 4K.

      - **Configuración de Wi-Fi**: **Habilitar** muestra el control de Wi-Fi en Managed Home Screen y permite que los usuarios conecten el dispositivo a distintas redes Wi-Fi. Si habilita esta característica, también se activa la ubicación del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no muestre el control de Wi-Fi en Managed Home Screen. Impide que los usuarios se conecten a redes Wi-Fi mientras usan Managed Home Screen.

      - **Configuración de Bluetooth**: **Habilitar** muestra el control de Bluetooth en Managed Home Screen y permite a los usuarios emparejar dispositivos a través de Bluetooth. Si habilita esta característica, también se activa la ubicación del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no muestre el control de Bluetooth en Managed Home Screen. Impide que los usuarios configuren el Bluetooth y los dispositivos de emparejamiento mientras usan Managed Home Screen.

      - **Acceso a la linterna**: **Habilitar** muestra el control de la linterna en Managed Home Screen y permite a los usuarios activarla o desactivarla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no muestre el control de la linterna en Managed Home Screen. Impide que los usuarios usen la linterna mientras usan Managed Home Screen.

      - **Control de volumen de elementos multimedia**: **Habilitar** muestra el control de volumen de elementos multimedia en Managed Home Screen y permite a los usuarios ajustar el volumen de los elementos multimedia del dispositivo con un control deslizante. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no muestre el control de volumen de los elementos multimedia en Managed Home Screen. Impide que los usuarios ajusten el volumen multimedia del dispositivo mientras se usa Managed Home Screen, a menos que los botones de hardware lo admitan.

      - **Modo de protector de pantalla**: **Habilitar** muestra un protector de pantalla en Managed Home Screen cuando el dispositivo está bloqueado o agota el tiempo de espera. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no muestre un protector de pantalla en Managed Home Screen.

        Cuando esté habilitado, configure también:

        - **Establecer imagen personalizada del protector de pantalla**: escriba la dirección URL de un archivo PNG, JPG, JPEG, GIF, BMP, WebP o ICOimage personalizado. Si no escribe una dirección URL, se usará la imagen predeterminada del dispositivo, si la hay. 
        
          Por ejemplo, escriba:

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`          

          > [!TIP]
          > Se admite cualquier dirección URL de recurso de archivo que se pueda convertir a un mapa de bits.

        - **Número de segundos que el dispositivo muestra el protector de pantalla antes de desactivar la pantalla**: elija el tiempo durante el cual el dispositivo muestra el protector de pantalla. Especifique un valor entre 0 y 9999999 segundos. El valor predeterminado es `0`segundos. Cuando se deja en blanco o se establece en cero (`0`), el protector de pantalla está activo hasta que un usuario interactúa con el dispositivo.
        - **Número de segundos que el dispositivo está inactivo antes de mostrar el protector de pantalla**: elija el tiempo que va a estar inactivo el dispositivo antes de mostrar el protector de pantalla. Especifique un valor entre 1 y 9999999 segundos. El valor predeterminado es `30` segundos. Debe especificar un número mayor que cero (`0`).
        - **Detectar elementos multimedia antes de iniciar el protector de pantalla**: **Habilitar** (valor predeterminado) no muestra el protector de pantalla si se está reproduciendo audio o vídeo en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar el protector de pantalla, incluso si se está reproduciendo audio o vídeo.

- **Totalmente administrado**: configura la aplicación Microsoft Launcher en los dispositivos totalmente administrados.

  - **Hacer que Microsoft Launcher sea el iniciador predeterminado**: **Habilitar** establece Microsoft Launcher como el iniciador predeterminado en la pantalla principal. Si hace que Launcher sea el iniciador predeterminado, los usuarios no podrán usar otro. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, Microsoft Launcher no se fuerza como iniciador predeterminado.

<!-- The following settings are in a future release. Per PM, we can leave them in GitHub, not live. Remove comment tags when they release.

  - **Configure custom wallpaper**: **Enable** lets you apply your own image as the home screen wallpaper, and choose if users can change the image. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the device keeps its current wallpaper.
    - **Enter URL of wallpaper image**: Enter the URL of your wallpaper image. This image shows on the device home screen. For example, enter `http://www.contoso.com/image.jpg`. 
    - **Allow user to modify wallpaper**: **Enable** allows users to change the wallpaper image. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the wallpaper.
  - **Enable launcher feed**: **Enable** turns on the launcher feed, which shows calendars, documents, and recent activities. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, this feed isn't shown.
    - **Allow user to enable/disable feed**: **Enable** lets users enable or disable the launcher feed. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the launcher feed settings.
  - **Dock presence**: The dock gives users quick access to their apps and tools. Your options:
    - **Not configured** (default): Intune doesn't change or update this setting.
    - **Show**: The dock is shown on devices.
    - **Hide**: The dock is hidden. Users must swipe up to access the dock.
    - **Disabled**: The dock isn't shown on devices, and users are prevented from showing it.

  - **Allow user to change dock presence**: **Enable** allows users to show or hide the dock. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users aren't allowed to change the device dock configuration.

  - **Search bar replacement**: Choose where to put the search bar. Your options:
    - **Not configured** (default): Intune doesn't change or update this setting.
    - **Top**: Search bar is shown at the top of devices.
    - **Bottom**: Search bar is shown at the bottom of devices.
    - **Hide**: Search bar is hidden.

  - **Allow user to change search bar placement**: **Enable** allows users to change the location of the search bar. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the location.

End of comment -->

### <a name="password"></a>Contraseña

- **Deshabilitar la pantalla de bloqueo**: elija **Deshabilitar** para evitar que los usuarios usen la característica de bloqueo del teclado en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios usar las características de bloqueo de teclado.
- **Características deshabilitadas en la pantalla de bloqueo**: Si KeyGuard está habilitado en el dispositivo, elija las características que quiere deshabilitar. Por ejemplo, si **Secure Camera** está activado, la característica de cámara se deshabilita en el dispositivo. Las características no activadas están habilitadas en el dispositivo.

  Estas características están disponibles para los usuarios cuando el dispositivo está bloqueado. Los usuarios no podrán ver ni acceder a las características que están activadas.

- **Tipo de contraseña requerida**: especifique el nivel requerido de complejidad de la contraseña y si se pueden usar dispositivos biométricos. Las opciones son:
  - **Valor predeterminado de dispositivo**
  - **Contraseña necesaria, sin restricciones**
  - **Biométrica deficiente**: [Biométricas eficientes frente a deficientes](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre el sitio web de Android)
  - **Numérica**: la contraseña solo debe contener números, por ejemplo, `123456789`. Indique también:
    - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
  - **Numérica compleja**: no se permiten números repetidos ni consecutivos, como "1111" o "1234". Indique también:
    - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
  - **Alfabética**: son necesarias letras del alfabeto. No son necesarios números ni símbolos. Indique también:
    - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
  - **Alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos. Indique también:
    - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
  - **Alfanumérica con símbolos**: incluye letras mayúsculas, minúsculas, caracteres numéricos, signos de puntuación y símbolos. Indique también:

    - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
    - **Número de caracteres requeridos**: escriba el número de caracteres que debe tener la contraseña, entre 0 y 16 caracteres.
    - **Número de caracteres en minúscula requeridos**: escriba el número de caracteres en minúscula que debe tener la contraseña, entre 0 y 16.
    - **Número de caracteres en mayúscula requeridos**: escriba el número de caracteres en mayúscula que debe tener la contraseña, entre 0 y 16.
    - **Número de caracteres que no sean letras requeridos**: escriba el número de caracteres que no son letras del alfabeto que debe tener la contraseña, entre 0 y 16 caracteres.
    - **Número de caracteres numéricos requeridos**: escriba el número de caracteres numéricos (`1`, `2`, `3`, etc.) que debe tener la contraseña, entre 0 y 16.
    - **Número de caracteres de símbolo requeridos**: escriba el número de caracteres de símbolo (`&`, `#`, `%`, etc.) que debe tener la contraseña, entre 0 y 16.

- **Número de días hasta que expire la contraseña**: escriba el número de días, entre 1 y 365, hasta que se deba cambiar la contraseña del dispositivo. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando la contraseña expire, se le solicitará a los usuarios que creen una nueva contraseña. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Número de contraseñas requeridas antes de que el usuario pueda reusar una**: utilice esta configuración para impedir que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borre el dispositivo, entre 4 y 11. `0` (cero) puede deshabilitar la función de borrado del dispositivo. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.

  > [!NOTE]
  > No se pedirá a los dispositivos del Propietario del dispositivo que establezcan una contraseña. La configuración se aplicará y tendrá que establecer la contraseña manualmente. La directiva que aplique esto se notificará como errónea hasta que se establezca la contraseña que cumpla sus requisitos.

### <a name="power-settings"></a>Configuración de energía

- **Tiempo antes de que se bloquee la pantalla**: especifique el tiempo máximo que un usuario puede establecer hasta que el dispositivo se bloquee. Por ejemplo, si se fija esta opción en `10 minutes`, los usuarios podrán establecer el tiempo desde 15 segundos hasta 10 minutos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

- **Pantalla activada mientras el dispositivo está conectado**: elija qué fuentes de alimentación hacen que la pantalla del dispositivo permanezca encendida cuando está conectado a la corriente alterna.

### <a name="users-and-accounts"></a>Usuarios y cuentas

- **Agregar nuevos usuarios**: **Bloquear** impide que los usuarios agreguen usuarios nuevos. Cada usuario tiene un espacio personal en el dispositivo para pantallas principales, cuentas, aplicaciones y configuraciones personalizadas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios agreguen otros usuarios en el dispositivo.
- **Eliminación de usuario**: **Bloquear** impide que los usuarios quiten otros usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios quiten otros usuarios del dispositivo.
- **Cambios de cuenta** (solo dispositivos dedicados): **Bloquear** impide que los usuarios modifiquen cuentas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios actualicen las cuentas de usuario en el dispositivo.

  > [!NOTE]
  > Esta configuración no se aplica a los dispositivos del propietario del dispositivo (totalmente administrados). Si configura esta opción, se omitirá la configuración y no tendrá efecto.

- **El usuario puede configurar las credenciales**: **Bloquear** impide que los usuarios configuren certificados asignados a dispositivos, incluso aunque se trate de dispositivos que no estén asociados a una cuenta de usuario. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios configuren o cambien sus credenciales al acceder a ellas en el almacén de claves.
- **Cuentas personales de Google**: **Bloquear** impide que los usuarios agreguen la cuenta personal de Google al dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios agregar su cuenta personal de Google.

### <a name="applications"></a>Aplicaciones

- **Permitir la instalación desde orígenes desconocidos**: **Permitir** habilita a los usuarios para activar los **orígenes desconocidos**. Esta configuración permite que se instalen aplicaciones desde orígenes desconocidos, incluidos los orígenes que no sean Google Play Store. Permite a los usuarios transferir localmente aplicaciones en el dispositivo mediante otros medios que no sean Google Play Store. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los usuarios activen los **orígenes desconocidos**.
- **Permitir el acceso a todas las aplicaciones en Google Play Store**: si se establece en **Permitir**, los usuarios obtienen acceso a todas las aplicaciones de Google Play Store. No obtienen acceso a las aplicaciones que el administrador bloquee en [las aplicaciones cliente](../apps/apps-add-android-for-work.md).

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría:
  
  - Obligar a los usuarios a acceder solo a las aplicaciones que el administrador ponga disponibles en Google Play Store o las aplicaciones necesarias en las [Aplicaciones cliente](../apps/apps-add-android-for-work.md). 
  - Desinstalar automáticamente las aplicaciones detectadas como instaladas por los usuarios fuera de la tienda de Google Play.

  Si desea habilitar la instalación de prueba, establezca la configuración de **Permitir la instalación desde orígenes desconocidos** y **Permitir el acceso a todas las aplicaciones en Google Play Store** en **Permitir**.

- **App auto-updates** (Actualizaciones automáticas de las aplicaciones): los dispositivos comprueban las actualizaciones de las aplicaciones diariamente. elija el momento de instalar las actualizaciones automáticas. Las opciones son:
  - **No configurado**: Intune no cambia ni actualiza esta configuración.
  - **Elección del usuario**: el sistema operativo podría tener como valor predeterminado esta opción. Los usuarios pueden establecer sus preferencias en la aplicación de Google Play administrado.
  - **Nunca**: las actualizaciones no se instalan nunca. No se recomienda esta opción.
  - **Solo Wi-Fi**: las actualizaciones se instalan solo cuando el dispositivo está conectado a una red Wi-Fi.
  - **Siempre**: las actualizaciones se instalan cuando están disponibles.

### <a name="connectivity"></a>Conectividad

- **VPN siempre activa**: **Habilitar** establece el cliente VPN para conectarse y volverse a conectar automáticamente a la VPN. Las conexiones VPN AlwaysOn permanecen conectadas. También puede conectarse inmediatamente cuando los usuarios bloqueen su dispositivo, el dispositivo se reinicie o la red inalámbrica cambie.

  Elija **No configurado** para deshabilitar la VPN siempre activa para todos los clientes VPN.

  > [!IMPORTANT]
  > Asegúrese de implementar una sola directiva de VPN siempre activa en un único dispositivo. No se admite la implementación de varias directivas de VPN siempre activa en un único dispositivo.

- **Cliente VPN**: elija un cliente VPN que admita Always On. Las opciones son:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Personalizada
    - **Id. de paquete**: escriba el identificador de paquete de la aplicación en Google Play Store. Por ejemplo, si la dirección URL de la aplicación en Play Store es `https://play.google.com/store/details?id=com.contosovpn.android.prod`, el identificador del paquete es `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - El cliente VPN que elija debe instalarse en el dispositivo y debe admitir VPN por aplicación en los perfiles de trabajo. De lo contrario, se produce un error. 
  > - Necesita aprobar la aplicación de cliente VPN en **Google Play Store administrado**, sincronizar la aplicación en Intune e implementar la aplicación en el dispositivo. Una vez hecho esto, la aplicación queda instalada en el perfil de trabajo del usuario.
  > - Todavía debe configurar el cliente VPN con un [perfil de VPN](vpn-settings-android-enterprise.md) o a través de un [perfil de configuración de la aplicación](../apps/app-configuration-policies-use-android.md).
  > - Existen problemas conocidos al usar VPN por aplicación con F5 Access para Android 3.0.4. Para obtener más información, vea las [notas de la versión de F5 Access para Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Modo de bloqueo**: **Habilitar** exige que todo el tráfico use el túnel VPN. Si no se establece una conexión a la VPN, el dispositivo no tendrá acceso a la red. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el tráfico fluya a través del túnel VPN o de la red móvil.

- **Proxy global recomendado**: **Habilitar** agrega un proxy global a los dispositivos. Cuando está habilitado, el tráfico HTTP y HTTPS, incluidas algunas aplicaciones del dispositivo, usan el proxy que especifique. Este proxy es solo una recomendación. Es posible que algunas aplicaciones no usen el proxy. **No configurado** (valor predeterminado) no agrega un proxy global recomendado.

  Para obtener más información sobre esta característica, vea [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (abre un sitio de Android).

  Cuando está habilitado, especifique también el **Tipo** de proxy. Las opciones son:

  - **Directo**: escriba manualmente los detalles del servidor proxy, incluido lo siguiente:
    - **Host**: escriba el nombre de host o la dirección IP del servidor proxy. Por ejemplo, escriba `proxy.contoso.com` o `127.0.0.1`.
    - **Número de puerto**: escriba el número de puerto TCP usado por el servidor proxy. Por ejemplo, escriba `8080`.
    - **Hosts excluidos**: especifique una lista de nombres de host o direcciones IP que no usarán el proxy. Esta lista puede incluir un carácter comodín de asterisco (`*`) y varios hosts separados por punto y coma (`;`) sin espacios. Por ejemplo, escriba `127.0.0.1;web.contoso.com;*.microsoft.com`.

  - **Configuración automática de proxy**: escriba la **dirección URL de PAC** para un script de configuración automática de proxy. Por ejemplo, escriba `https://proxy.contoso.com/proxy.pac`.

    Para obtener más información sobre los archivos PAC, vea [Archivo de configuración automática de proxy (PAC)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file), aunque tenga en cuenta que este sitio no pertenece a Microsoft.

  Para obtener más información sobre esta característica, vea [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (abre un sitio de Android).

## <a name="work-profile-only"></a>Solo perfil de trabajo

Esta configuración se aplica a los tipos de inscripción Android Enterprise donde Intune controla solo el perfil de trabajo, como la inscripción de perfil de trabajo Android Enterprise en un dispositivo personal o BYOD.

### <a name="work-profile-settings"></a>Configuración de perfil de trabajo

- **Copiar y pegar entre perfiles personales y de trabajo**: **Bloquear** impide copiar y pegar entre aplicaciones personales y profesionales. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios compartan datos mediante copiar y pegar con aplicaciones en el perfil personal.
- **Uso compartido de datos entre el perfil profesional y el personal**: elija si las aplicaciones del perfil de trabajo pueden compartirse con aplicaciones del perfil personal. Por ejemplo, puede controlar las acciones de uso compartido dentro de las aplicaciones, como la opción **Compartir…** en la aplicación del explorador Chrome. Esta configuración no se aplica al comportamiento del Portapapeles de copiar y pegar. Las opciones son:
  - **Valor predeterminado del dispositivo**: el comportamiento predeterminado del uso compartido del dispositivo varía según la versión de Android:
    - En los dispositivos que ejecutan Android 6.0 y versiones más recientes, el uso compartido desde el perfil de trabajo hasta el perfil personal está bloqueado. Se permite el uso compartido desde el perfil personal hasta el perfil de trabajo.
    - En los dispositivos que ejecutan Android 5.0 y versiones anteriores, el uso compartido desde el perfil de trabajo hasta el perfil personal está bloqueado en ambas direcciones.
  - **Las aplicaciones del perfil profesional pueden controlar una solicitud de uso compartido del perfil personal**: habilita la característica de Android integrada que permite el uso compartido del perfil personal al perfil de trabajo. Cuando esta opción está habilitada, una solicitud de uso compartido que se inicia en una aplicación del perfil personal se podrá compartir con las aplicaciones del perfil de trabajo. Esta opción es el comportamiento predeterminado de los dispositivos Android que ejecutan versiones anteriores a 6.0.
  - **No hay restricciones para el uso compartido**: permite el uso compartido a través del límite del perfil de trabajo en ambas direcciones. Cuando selecciona esta configuración, las aplicaciones del perfil de trabajo pueden compartir datos con aplicaciones no administradas del perfil personal. Esta configuración permite administrar aplicaciones en el perfil de trabajo para compartirlas con aplicaciones del lado sin administrar del dispositivo. Por lo tanto, use esta configuración con precaución.

- **Notificaciones del perfil profesional con dispositivo bloqueado**: **Bloquear** impide que las notificaciones de ventana, incluidas las notificaciones del sistema, las llamadas entrantes, las llamadas salientes, las alertas del sistema y los errores del sistema se muestren en los dispositivos bloqueados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las notificaciones.
- **Permisos de aplicación predeterminados**: Establece la directiva de permisos predeterminada para todas las aplicaciones del perfil de trabajo. A partir de Android 6, se solicita a los usuarios que concedan determinados permisos que requieren las aplicaciones cuando se inician. Esta configuración de directiva permite decidir si se pedirá a los usuarios que concedan permisos para todas las aplicaciones del perfil de trabajo. Por ejemplo, suponga que asigna una aplicación al perfil de trabajo que requiere acceso mediante la ubicación. Normalmente, esa aplicación solicita a los usuarios que aprueben o denieguen el acceso a la aplicación mediante la ubicación. Use esta directiva para conceder permisos y denegar permisos automáticamente sin preguntar a los usuarios o dejar que estos decidan. Las opciones son:
  - **Valor predeterminado de dispositivo**
  - **Aviso**
  - **Concesión automática**
  - **Denegación automática**

  También puede usar una directiva de configuración de aplicaciones a fin de conceder permisos para aplicaciones individuales (**Aplicaciones cliente** > **Directivas de configuración de aplicaciones**).

- **Agregar y quitar cuentas**: **Bloquear** impide que los usuarios agreguen o quiten cuentas manualmente en el perfil de trabajo. Por ejemplo, cuando implemente la aplicación de Gmail en un perfil de trabajo Android, podrá impedir que los usuarios agreguen o quiten cuentas en este perfil de trabajo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la incorporación de cuentas en el perfil de trabajo.  

  > [!NOTE]
  > Las cuentas de Google no se pueden agregar a un perfil de trabajo.

- **Uso compartido de contactos a través de Bluetooth**: **Habilitar** permite el uso compartido y el acceso a los contactos del perfil de trabajo desde otro dispositivo, incluido un automóvil, que esté emparejado con Bluetooth. Si se habilita, puede permitir que ciertos dispositivos Bluetooth almacenen en caché los contactos de trabajo en la primera conexión. Si se deshabilita esta directiva después de un emparejamiento o una sincronización inicial no puede eliminar los contactos de trabajo desde un dispositivo Bluetooth.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no comparta contactos de trabajo.

  Esta configuración solo es aplicable a:

  - Dispositivos de perfil de trabajo Android que ejecutan la versión del sistema operativo Android 6.0 y posteriores

- **Captura de pantalla**: **Bloquear** impide capturas de pantalla en el dispositivo en el perfil de trabajo. Además evita que el contenido se muestre en los dispositivos de pantalla que no tengan una salida de vídeo segura. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la obtención de capturas de pantalla.

- **Mostrar el identificador de llamada de contacto profesional en el perfil personal**: **Bloquear** no muestra el número del autor de la llamada de contacto profesional en el perfil personal. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar los detalles del autor de la llamada de contacto profesional.

  Esta configuración solo es aplicable a:

  - Versiones del sistema operativo Android 6.0 y posteriores

- **Buscar contactos profesionales del perfil personal**: **Bloquear** impide que los usuarios busquen contactos de trabajo en las aplicaciones del perfil personal. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la búsqueda de contactos de trabajo en el perfil personal.

- **Cámara**: **Bloquear** impide el acceso a la cámara del dispositivo en el perfil de trabajo. La configuración no afecta a la cámara en el perfil personal. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara.

- **Permitir widgets de las aplicaciones del perfil de trabajo**: **Habilitar** permite a los usuarios colocar widgets expuestos por aplicaciones en la pantalla principal. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar esta característica.

  Por ejemplo, Outlook se instala en los perfiles de trabajo de los usuarios. Cuando se establece en **Habilitar**, los usuarios pueden colocar el widget de la agenda en la pantalla principal del dispositivo.

- **Requerir contraseña del perfil de trabajo**: **Requerir** fuerza una directiva de código de acceso que se aplica únicamente a las aplicaciones del perfil de trabajo. De forma predeterminada, los usuarios pueden usar los dos PIN definidos por separado. También pueden combinar los PIN en el más seguro de los dos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen las aplicaciones de trabajo sin tener que escribir una contraseña.

  Esta configuración solo es aplicable a:

  - Android 7.0 y versiones más recientes con el perfil de trabajo habilitado

- **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
- **Cantidad máxima de minutos de inactividad hasta que el perfil de trabajo se bloquea**: escriba el tiempo durante el cual los dispositivos deben estar inactivos antes de que se bloquee automáticamente la pantalla. Los usuarios deberán introducir sus credenciales para volver a obtener acceso. Por ejemplo, escriba `5` para bloquear el dispositivo tras estar 5 minutos inactivo. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

  En los dispositivos, los usuarios no pueden establecer un valor de tiempo mayor que el tiempo configurado en el perfil. Los usuarios pueden establecer un valor de tiempo menor. Por ejemplo, si el perfil está establecido en `15` minutos, los usuarios pueden establecer el valor en 5 minutos. Pero no podrán establecerlo en 30 minutos.

- **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borre el dispositivo, entre 4 y 11. `0` (cero) puede deshabilitar la función de borrado del dispositivo. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.

- **Expiración de la contraseña (días)** : escriba el número de días hasta que se deba cambiar las contraseñas de un usuario (**1**-**365**).
- **Tipo de contraseña requerida**: especifique el nivel requerido de complejidad de la contraseña y si se pueden usar dispositivos biométricos. Las opciones son:
  - **Valor predeterminado de dispositivo**
  - **Biométrico de seguridad baja**: [Biométricas eficientes frente a deficientes](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre el sitio web de Android)
  - **Requerido**
  - **Al menos numérica**: Incluye caracteres numéricos, como `123456789`.
  - **Numérica compleja**: no se permiten números repetidos ni consecutivos, como `1111` o `1234`.
  - **Al menos alfabética**: incluye letras del alfabeto. No son necesarios números ni símbolos.
  - **Al menos alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos.
  - **Al menos alfanumérica con símbolos**: incluye letras mayúsculas, minúsculas, caracteres numéricos, signos de puntuación y símbolos.

- **Impedir la reutilización de contraseñas anteriores**: utilice esta configuración para impedir que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Desbloqueo con huella digital**: **Bloquear** impide que los usuarios usen el escáner de huella digital del dispositivo para desbloquearlo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios desbloqueen el dispositivo mediante una huella digital.
- **Smart Lock y otros agentes de confianza**: **Bloquear** impide que Smart Lock u otros agentes de confianza ajusten la configuración de la pantalla de bloqueo en dispositivos compatibles. Si los dispositivos están en una ubicación de confianza, esta característica, conocida también como agente de confianza, permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo. Por ejemplo, se puede omitir la contraseña de perfil de trabajo cuando los dispositivos están conectados a un dispositivo Bluetooth específico o cuando están cerca de una etiqueta de NFC. Use esta opción para impedir que los usuarios configuren Smart Lock.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

### <a name="password"></a>Contraseña

Esta configuración de contraseña se aplica a los perfiles personales de los dispositivos que usan un perfil de trabajo.

- **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
- **Máximo de minutos de inactividad hasta que se bloquea la pantalla**: escriba el tiempo durante el cual los dispositivos deben estar inactivos antes de que se bloquee automáticamente la pantalla. Los usuarios deberán introducir sus credenciales para volver a obtener acceso. Por ejemplo, escriba `5` para bloquear el dispositivo tras estar 5 minutos inactivo. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

  En los dispositivos, los usuarios no pueden establecer un valor de tiempo mayor que el tiempo configurado en el perfil. Los usuarios pueden establecer un valor de tiempo menor. Por ejemplo, si el perfil está establecido en `15` minutos, los usuarios pueden establecer el valor en 5 minutos. Pero no podrán establecerlo en 30 minutos.

- **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borre el dispositivo, entre 4 y 11. `0` (cero) puede deshabilitar la función de borrado del dispositivo. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Expiración de la contraseña (días)** : escriba el número de días, entre 1 y 365, hasta que se deba cambiar la contraseña del dispositivo. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando la contraseña expire, se le solicitará a los usuarios que creen una nueva contraseña. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Tipo de contraseña requerida**: especifique el nivel requerido de complejidad de la contraseña y si se pueden usar dispositivos biométricos. Las opciones son:
  - **Valor predeterminado de dispositivo**
  - **Biométrico de seguridad baja**: [Biométricas eficientes frente a deficientes](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (abre el sitio web de Android)
  - **Requerido**
  - **Al menos numérica**: Incluye caracteres numéricos, como `123456789`.
  - **Numérica compleja**: no se permiten números repetidos ni consecutivos, como `1111` o `1234`.
  - **Al menos alfabética**: incluye letras del alfabeto. No son necesarios números ni símbolos.
  - **Al menos alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos.
  - **Al menos alfanumérica con símbolos**: incluye letras mayúsculas, minúsculas, caracteres numéricos, signos de puntuación y símbolos.

- **Impedir la reutilización de contraseñas anteriores**: utilice esta configuración para impedir que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Desbloqueo con huella digital**: **Bloquear** impide que los usuarios usen el escáner de huella digital del dispositivo para desbloquearlo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios desbloqueen el dispositivo mediante una huella digital.
- **Smart Lock y otros agentes de confianza**: **Bloquear** impide que Smart Lock u otros agentes de confianza ajusten la configuración de la pantalla de bloqueo en dispositivos compatibles. Si los dispositivos están en una ubicación de confianza, esta característica, conocida también como agente de confianza, permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo. Por ejemplo, se puede omitir la contraseña de perfil de trabajo cuando los dispositivos están conectados a un dispositivo Bluetooth específico o cuando están cerca de una etiqueta de NFC. Use esta opción para impedir que los usuarios configuren Smart Lock.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

### <a name="system-security"></a>Seguridad del sistema

- **Examen de amenazas en las aplicaciones**: **Requerir** exige que la configuración **Verificar aplicaciones** esté habilitada para los perfiles personales y profesionales. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  Esta configuración solo es aplicable a:

  - Android 8 (Oreo) y versiones posteriores

- **Impedir la instalación de aplicaciones de orígenes desconocidos en el perfil personal**: por diseño, los dispositivos de perfil de trabajo Android Enterprise no pueden instalar aplicaciones desde orígenes distintos a Play Store. Esta configuración permite a los administradores tener un mayor control de las instalaciones de aplicaciones de orígenes desconocidos. **Bloquear** impide la instalación de aplicaciones desde orígenes distintos a Google Play Store en el perfil personal. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la instalación de aplicaciones de orígenes desconocidos en el perfil personal. Por naturaleza, los dispositivos de perfil de trabajo están diseñados para tener un perfil dual:

  - Un perfil de trabajo administrado mediante MDM.
  - Un perfil personal aislado de la administración de MDM.

### <a name="connectivity"></a>Conectividad

- **VPN siempre activa**: **Habilitar** establece un cliente VPN para conectarse y volverse a conectar automáticamente a la VPN. Las conexiones VPN AlwaysOn permanecen conectadas. También puede conectarse inmediatamente cuando los usuarios bloqueen su dispositivo, el dispositivo se reinicie o la red inalámbrica cambie.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar la VPN AlwaysOn para todos los clientes VPN.

  > [!IMPORTANT]
  > Asegúrese de implementar una sola directiva de VPN siempre activa en un único dispositivo. No se admite la implementación de varias directivas de VPN siempre activa en un único dispositivo.

- **Cliente VPN**: elija un cliente VPN que admita Always On. Las opciones son:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Personalizada
    - **Id. de paquete**: escriba el identificador de paquete de la aplicación en Google Play Store. Por ejemplo, si la dirección URL de la aplicación en Play Store es `https://play.google.com/store/details?id=com.contosovpn.android.prod`, el identificador del paquete es `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - El cliente VPN que elija debe instalarse en el dispositivo y debe admitir VPN por aplicación en los perfiles de trabajo. De lo contrario, se produce un error.
  > - Necesita aprobar la aplicación de cliente VPN en **Google Play Store administrado**, sincronizar la aplicación en Intune e implementar la aplicación en el dispositivo. Una vez hecho esto, la aplicación queda instalada en el perfil de trabajo del usuario.
  > - Existen problemas conocidos al usar VPN por aplicación con F5 Access para Android 3.0.4. Para más información, consulte las [notas de la versión de F5 Access para Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Modo de bloqueo**: **Habilitar** exige que todo el tráfico use el túnel VPN. Si no se establece una conexión a la VPN, el dispositivo no tendrá acceso a la red.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el tráfico fluya a través del túnel VPN o de la red móvil.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede crear perfiles de pantalla completa de dispositivo dedicado para dispositivos [Android](device-restrictions-android.md#kiosk) y [Windows 10](kiosk-settings.md).

[Configuración y solución de problemas de dispositivos Android Enterprise en Microsoft Intune](https://support.microsoft.com/help/4476974).
