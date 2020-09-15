---
title: 'Configuración de dispositivo iOS/iPadOS en Microsoft Intune: Azure | Microsoft Docs'
titleSuffix: ''
description: Agregue, configure o cree valores en dispositivos iOS/iPadOS para restringir características, lo que incluye establecer requisitos de contraseña, controlar la pantalla de bloqueo, usar aplicaciones integradas, agregar aplicaciones restringidas o aprobadas, controlar dispositivos Bluetooth, conectarse a la nube para realizar copias de seguridad y almacenamiento, habilitar la pantalla completa, agregar dominios y controlar la manera en que los usuarios interactúan con el explorador web Safari en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 273efc6be6b3f93c04c0ce39c2688859d3c96c56
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423890"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Configuración de dispositivos iOS e iPadOS para permitir o restringir características mediante Intune

En este artículo se enumeran y describen los diferentes valores de configuración que se pueden controlar en los dispositivos iOS e iPadOS. Como parte de la solución de administración de dispositivos móviles (MDM), use estos valores para habilitar o deshabilitar características, establecer reglas de contraseña, permitir o restringir determinadas aplicaciones, etc.

Estos valores se agregan a un perfil de configuración del dispositivo en Intune y luego se asignan o implementan en los dispositivos iOS/iPadOS.

> [!TIP]
> Esta configuración usa las opciones de MDM de Apple. Para obtener más información sobre esta configuración, vea [Configuración de administración de dispositivos móviles de Apple](https://support.apple.com/guide/mdm/welcome/web) (abre el sitio web de Apple).

## <a name="before-you-begin"></a>Antes de comenzar

[Crear un perfil de configuración de restricciones de dispositivos](device-restrictions-configure.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción, mientras que algunas opciones se aplican a todas las opciones de inscripción. Para más información sobre los diferentes tipos de inscripción, consulte [Inscripción en iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="general"></a>General

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Compartir los datos de uso**: **Bloquear** impide que los dispositivos envíen a Apple datos de diagnóstico y uso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el envío de estos datos.

- **Captura de pantalla**: **Bloquear** impide que se hagan capturas de pantalla en los dispositivos. En iOS/iPadOS 9.0 y versiones más recientes, también se bloquean las grabaciones de pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De manera predeterminada, el sistema operativo podría permitir que los usuarios capturen el contenido de la pantalla como imagen o como vídeo.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Certificados TLS que no son de confianza**: **Bloquear** impide en los dispositivos los certificados de Seguridad de la capa de transporte (TLS) que no sean de confianza. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir certificados de TLS.
- **Bloquear actualizaciones móviles de PKI**: **Bloquear** impide que los usuarios reciban actualizaciones de software, a menos que los dispositivos estén conectados a un equipo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De manera predeterminada, el sistema operativo podría permitir que un dispositivo reciba actualizaciones de software sin estar conectado a un equipo.
- **Limitar el seguimiento de publicidad**: **Limitar** deshabilita el identificador de publicidad del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mantenerlo habilitado.
- **Confianza de aplicaciones empresariales**: **Bloquear** quita de los dispositivos el botón **Trust Enterprise Developer** en Configuración > General > Administración de perfiles y dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el usuario elija confiar en aplicaciones no descargadas de la tienda de aplicaciones.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Modificación de la configuración del envío de diagnósticos**: **Bloquear** impide que los usuarios cambien la configuración de análisis de aplicación y envío de diagnóstico en **Datos de diagnóstico y uso** (configuración del dispositivo). Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración del dispositivo.

  Para usar esta opción, establezca **Compartir datos de uso** en **Bloquear**.

  Esta característica se aplica a:  
  - iOS 9.3.2 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Observación de pantalla remota mediante la aplicación Classroom**: **Bloquear** impide que la aplicación Classroom vea de forma remota la pantalla en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la aplicación Aula de Apple vea la pantalla.

  Para usar esta opción, establezca **Captura de pantalla** en **Bloquear**.

  Esta característica se aplica a:  
  - iOS 9.3 - iOS 12.x: requiere dispositivos supervisados
  - iOS 13.0 y versiones posteriores: no requiere dispositivos supervisados
  - IPadOS 13.0 y versiones posteriores: Los dispositivos deben haberse inscrito con la inscripción de dispositivos o con la inscripción de dispositivos automatizada (ADE).

- **Observación de pantalla sin mensajes por la aplicación Classroom**: **Permitir** habilita a los profesores para observar de manera silenciosa las pantallas iOS/iPadOS de los alumnos con la aplicación Classroom sin que estos lo sepan. Los dispositivos de alumnos inscritos en una clase con la aplicación Classroom automáticamente dan permiso al profesor de ese curso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir esta característica.

  Para usar esta opción, establezca **Captura de pantalla** en **Bloquear**.

- **Modificación de la cuenta**: **Bloquear** impide que los usuarios puedan actualizar la configuración específica del dispositivo en la aplicación de configuración de iOS/iPadOS. Por ejemplo, los usuarios no pueden crear nuevas cuentas de dispositivo ni modificar el nombre de usuario o la contraseña. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración.

  Esta característica también se aplica a la configuración accesible desde la aplicación de configuración de iOS/iPadOS, como Correo, Contactos, Calendario, Twitter, etc. Esta característica no se aplica a las aplicaciones con la configuración de la cuenta que no se pueden configurar desde la aplicación de configuración de iOS/iPadOS, como la aplicación Microsoft Outlook.

- **Tiempo de uso**: **Bloquear** impide que los usuarios establezcan sus propias restricciones en Tiempo de uso (configuración de dispositivo). Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios configurar las restricciones de dispositivo (como las restricciones de privacidad y contenido o el control parental) en los dispositivos.

  Este es el nuevo nombre de que se ha cambiado de la configuración **Habilitación de restricciones en la configuración del dispositivo**. Impacto de este cambio:  
  
  - iOS 11.4.1 y superior: **Bloquear** impide que los usuarios establezcan sus propias restricciones en la configuración del dispositivo. El comportamiento es el mismo y no hay ningún cambio para los usuarios.
  - iOS 12.0 y versiones más recientes: **Bloquear** impide que los usuarios establezcan su propio **Tiempo de uso** en la configuración del dispositivo (Configuración > General > Tiempo de uso), incluidas restricciones de contenido y privacidad. En los dispositivos actualizados a iOS 12.0 ya no aparecerá la pestaña de restricciones en la configuración del dispositivo (Configuración > General > Administración de dispositivos > Perfil de administración > Restricciones). Estas opciones se encuentran en **Tiempo de uso**.
  
- **Usar la opción de borrar todo el contenido y la configuración del dispositivo**: **Bloquear** impide el uso de la opción de borrado de todo el contenido y configuración en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios accedan a esta configuración.
- **Modificación del nombre del dispositivo**: **Bloquear** impide cambiar el nombre del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien el nombre de los dispositivos.
- **Modificación de la configuración de notificaciones**: **Bloquear** impide cambiar la configuración de las notificaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de las notificaciones del dispositivo.
- **Modificación del fondo de pantalla**: **Bloquear** evita que se cambie el fondo de pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien el fondo de pantalla de los dispositivos.
- **Cambios en el perfil de configuración**: **Bloquear** impide los cambios en el perfil de configuración en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios instalen perfiles de configuración.
- **Bloqueo de activación**: **Permitir** habilita el Bloqueo de activación en dispositivos iOS/iPadOS supervisados. Bloqueo de activación dificulta que un dispositivo robado o perdido pueda reactivarse. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Bloquear la eliminación de aplicaciones**: **Bloquear** impide la eliminación de aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios quiten aplicaciones de los dispositivos.
- **Permitir accesorios USB con el dispositivo bloqueado**: **Permitir** habilita a los accesorios USB para intercambiar datos con dispositivos que han estado bloqueados durante más de una hora. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no actualice el modo restringido de USB en los dispositivos y los accesorios USB no puedan transferir datos de los dispositivos si están bloqueados durante más de una hora.

  Esta característica se aplica a:  
  - iOS/iPadOS 11.4.1 y versiones más recientes

- **Forzar fecha y hora automáticas**: **Requerir** obliga a los dispositivos supervisados a establecer la fecha y la hora automáticamente. La zona horaria del dispositivo se actualiza cuando el dispositivo tiene conexiones móviles o tiene Wi-Fi con servicios de ubicación habilitados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Requerir que los estudiantes soliciten permiso para dejar el curso de Classroom**: **Requerir** obliga a los alumnos inscritos en un curso no administrado con la aplicación Aula a pedir permiso al profesor para dejar el curso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no obligar al alumno a pedir permiso.

  Esta característica se aplica a:  
  - iOS 11.3 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Permitir a Classroom bloquearse en una aplicación y bloquear el dispositivo sin preguntar**: **Habilitar** permite que el profesor bloquee aplicaciones o dispositivos mediante la aplicación Classroom sin preguntar al alumno. Al bloquear las aplicaciones, los dispositivos solo pueden acceder a las aplicaciones especificadas por el profesor. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los profesores bloqueen aplicaciones o dispositivos que usan la aplicación Aula sin preguntar al alumno.

  Esta característica se aplica a:  
  - iOS 11.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Unirse a las clases de Classroom automáticamente sin preguntar**: **Habilitar** permite automáticamente a los alumnos unirse a una clase de la aplicación Classroom sin preguntar al profesor. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría notificar al profesor que hay alumnos que quieren unirse a una clase que se encuentra en la aplicación Classroom.

  Esta característica se aplica a:  
  - iOS 11.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Bloquear creación de VPN**: **Bloquear** evita que los usuarios creen una configuración de VPN. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios creen redes VPN en los dispositivos.
- **Modificar la configuración de eSIM**: **Bloquear** impide la eliminación o la incorporación de un plan de telefonía móvil para el eSIM en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración.

  Esta característica se aplica a:  
  - iOS 12.1 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Aplazar las actualizaciones de software**: **Habilitar** permite retrasar la visualización de las actualizaciones en el dispositivo, entre 0 y 90 días. Esta configuración no controla cuándo se instalan las actualizaciones.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las actualizaciones de software en los dispositivos a medida que Apple las publica. Por ejemplo, si Apple publica una actualización de iOS/iPadOS en una fecha concreta, dicha actualización se mostrará de forma natural en los dispositivos en torno a la fecha de publicación.  

  - **Retrasar la visibilidad de las actualizaciones de software**: especifique un valor entre 0 y 90 días. Cuando el retraso expira, los usuarios reciben una notificación para actualizar a la versión más antigua del sistema operativo que estaba disponible cuando se desencadenó el retraso.

    Por ejemplo, si iOS 12.a está disponible **el 1 de enero** y **Retrasar la visibilidad** está establecido en **5 días**, iOS 12.a no se muestra como una actualización disponible en los dispositivos de usuario. Al **sexto día** después de la publicación, esta actualización estará disponible y los usuarios podrán instalarla.

    Esta configuración solo es aplicable a:  
    - iOS 11.3 y versiones más recientes
    - IPadOS 13.0 y versiones más recientes

## <a name="password"></a>Contraseña

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Contraseña**: **Requerir** que los usuarios escriban una contraseña para acceder a los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios accedan a los dispositivos sin tener que escribir una contraseña.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

> [!IMPORTANT]
> En los dispositivos inscritos por usuarios, si configura cualquier opción de contraseña, la configuración de **Contraseñas sencillas** se establece automáticamente en **Bloquear** y se aplica un PIN de 6 dígitos.
>
> Por ejemplo, configura el valor **Caducidad de la contraseña** e inserta esta directiva en dispositivos con usuarios inscritos. En los dispositivos, ocurre lo siguiente:
>
> - Se omite el valor de **Caducidad de la contraseña**.
> - No se permiten contraseñas sencillas, como `1111` o `1234`.
> - Se aplica un PIN de 6 dígitos.

- **Contraseñas sencillas**: **Bloquear** requiere contraseñas más complejas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo permita contraseñas sencillas, como `0000` y `1234`.

- **Tipo de contraseña requerida**: escriba el nivel de complejidad de la contraseña requerido que exija su organización. Las opciones son:
  - **Valor predeterminado de dispositivo**
  - **Numérica**: la contraseña solo debe contener números, por ejemplo, 123456789.
  - **Alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos.

  > [!NOTE]
  > La selección de caracteres alfanuméricos puede afectar a un Apple Watch emparejado. Para más información, vea [Configurar las restricciones de código en un Apple Watch](https://support.apple.com/HT204953) (abre el sitio web de Apple).

- **Número de caracteres no alfanuméricos en la contraseña**: Escriba el número de caracteres de símbolo, como `#` o `@`, que deben incluirse en la contraseña, entre 1 y 4. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

- **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres. En dispositivos inscritos por el usuario, especifique una longitud de entre 4 y 6 caracteres.
  
  > [!NOTE]
  > En el caso de los dispositivos inscritos por el usuario, los usuarios pueden establecer un PIN de más de 6 dígitos. Pero en los dispositivos no se exigen más de 6 dígitos. Por ejemplo, un administrador establece la longitud mínima en `8`. En los dispositivos inscritos por el usuario, solo se exige a los usuarios establecer un PIN de 6 dígitos. Intune no exige un PIN de más de 6 dígitos en los dispositivos inscritos por el usuario.

- **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de errores de inicio de sesión antes de que se borre el dispositivo, entre 4 y 11.
  
  iOS/iPadOS cuenta con seguridad integrada que puede afectar a esta configuración. Por ejemplo, iOS/iPadOS puede retrasar la activación de la directiva en función del número de errores de inicio de sesión. También puede considerar la especificación repetida del mismo código de acceso como un intento. La [guía de seguridad de iOS/iPadOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) de Apple (abre el sitio web de Apple) es un buen recurso y proporciona detalles más concretos sobre los códigos de acceso.
  
- **Máximo de minutos tras bloqueo de pantalla antes de solicitar la contraseña**<sup>1</sup>: Introduzca cuánto tiempo pueden permanecer inactivos los dispositivos antes de que los usuarios deban volver a escribir la contraseña. Si escribe un tiempo mayor al que está establecido actualmente en el dispositivo, este pasará por alto el tiempo que escribió.

  Esta configuración solo es aplicable a:  
  - iOS 8.0 y versiones posteriores
  - iPadOS 13.0 y versiones posteriores

- **Máximo de minutos de inactividad hasta que se bloquea la pantalla**<sup>1</sup>: Escriba el número máximo de minutos de inactividad que se permiten en los dispositivos hasta que se bloquea la pantalla.

  **Opciones de iOS/iPadOS**:  

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Inmediatamente**: la pantalla se bloquea tras 30 segundos de inactividad.
  - **1**: la pantalla se bloquea tras 1 minuto de inactividad.
  - **2**: la pantalla se bloquea tras 2 minutos de inactividad.
  - **3**: la pantalla se bloquea tras 3 minutos de inactividad.
  - **4**: la pantalla se bloquea tras 4 minutos de inactividad.
  - **5**: la pantalla se bloquea tras 5 minutos de inactividad.

  **Opciones de iPadOS**:  

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Inmediatamente**: la pantalla se bloquea tras 2 minutos de inactividad.
  - **2**: la pantalla se bloquea tras 2 minutos de inactividad.
  - **5**: la pantalla se bloquea tras 5 minutos de inactividad.
  - **10**: la pantalla se bloquea tras 10 minutos de inactividad.
  - **15**: la pantalla se bloquea tras 15 minutos de inactividad.

  Si un valor no se aplica a iOS ni iPadOS, Apple usa el valor *inferior* más cercano. Por ejemplo, si especifica `4` minutos, los dispositivos iPadOS usan `2` minutos. Si especifica `10` minutos, los dispositivos iOS usan `5` minutos. Este comportamiento es una limitación de Apple.
  
  > [!NOTE]
  > La interfaz de usuario de Intune para esta configuración no separa los valores admitidos de iOS e iPadOS. La interfaz de usuario podría actualizarse en una versión futura.

- **Expiración de la contraseña (días)** : introduzca el número de días antes de que se deba cambiar la contraseña del dispositivo, entre 1 y 65 535.
- **Impedir la reutilización de contraseñas anteriores**: utilice esta configuración para impedir que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba 5 para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en ninguna de sus cuatro anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
- **Desbloqueo de Touch ID y Face ID**: **Bloquear** impide el uso de una huella digital o una cara para desbloquear dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios desbloqueen los dispositivos mediante datos biométricos.

  El bloqueo de esta configuración también evita el uso de la autenticación de FaceID para desbloquear dispositivos.

  Face ID se aplica a:  
  - iOS 11.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Modificación del código de acceso**: **Bloquear** evita que se cambie, se agregue o se quite el código de acceso. En los dispositivos supervisados, los cambios en las restricciones del código de acceso se ignoran después de bloquear esta característica. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que se cambie, se agregue o se quite el código de acceso.

  - **Modificación de Touch ID y Face ID**: **Bloquear** impide que los usuarios cambien, agreguen o quiten huellas digitales de Touch ID y Face ID. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios actualicen las huellas digitales de TouchID y de Face ID de los dispositivos.

    El bloqueo de esta configuración también evita que los usuarios cambien, agreguen o quiten la autenticación de Face ID.

    Face ID se aplica a:  
    - iOS 11.0 y versiones más recientes
    - IPadOS 13.0 y versiones más recientes

- **Impedir el relleno automático de contraseñas**: **Bloquear** impide el uso de la característica Autorrellenar contraseñas en iOS/iPadOS. Si elige **Bloquear** tendrá también este impacto:

  - No se les pide a los usuarios que usen una contraseña guardada en Safari ni en ninguna aplicación.
  - Se deshabilitan las contraseñas seguras automáticas y no se sugieren contraseñas seguras a los usuarios.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas características.

- **Impedir las solicitudes de proximidad de contraseñas**: **Bloquear** impide que los dispositivos soliciten contraseñas de dispositivos cercanos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas solicitudes de contraseña.
- **Impedir el uso compartido de contraseñas**: **Bloquear** evita el uso compartido de contraseñas entre dispositivos mediante AirDrop. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo permita que estas contraseñas se compartan.
- **Requerir autenticación con Touch ID o Face ID para el relleno automático de datos de tarjetas de crédito o contraseñas**: **Requerir** obliga a los usuarios a autenticarse mediante TouchID o FaceID para que los datos de la tarjeta de crédito o las contraseñas puedan rellenarse automáticamente en Safari y otras aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios controlen esta característica en la configuración del dispositivo.

  Esta característica se aplica a:  
  - iOS 11.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes
  
<sup>1</sup> Al configurar los valores **Máximo de minutos de inactividad hasta que se bloquea la pantalla** y **Máximo de minutos tras bloqueo de pantalla antes de solicitar la contraseña**, se aplican en secuencia. Por ejemplo, si establece el valor para ambas opciones en **5** minutos, la pantalla se apaga automáticamente transcurridos cinco minutos y los dispositivos se bloquean después de cinco minutos más. Sin embargo, si los usuarios apagan la pantalla manualmente, la segunda opción se aplica inmediatamente. En el mismo ejemplo, una vez que los usuarios apagan la pantalla, el dispositivo se bloquea cinco minutos más tarde.

## <a name="locked-screen-experience"></a>Experiencia de pantalla bloqueada

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Acceso a Centro de control con dispositivo bloqueado**: **Bloquear** impide el acceso a la aplicación Centro de control cuando el dispositivo está bloqueado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la aplicación Centro de control cuando los dispositivos están bloqueados.
- **Notificaciones con dispositivo bloqueado**: **Bloquear** impide el acceso a las notificaciones cuando los dispositivos están bloqueados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a las notificaciones sin que sea necesario desbloquear los dispositivos.
- **Vista Hoy con dispositivo bloqueado**: **Bloquear** impide el acceso a la vista Hoy cuando los dispositivos están bloqueados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios vean la vista Hoy cuando los dispositivos están bloqueados.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Notificaciones de Wallet con dispositivo bloqueado**: **Bloquear** impide el acceso a la aplicación Wallet cuando los dispositivos están bloqueados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la aplicación Wallet mientras los dispositivos están bloqueados.

## <a name="app-store-doc-viewing-gaming"></a>Tienda de aplicaciones, presentación de documentos, juegos

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Visualización de documentos corporativos en aplicaciones no administradas**: **Bloquear** evita la visualización de documentos corporativos en aplicaciones no administradas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los documentos corporativos se vean en cualquier aplicación.

  Por ejemplo, se quiere evitar que los usuarios guarden archivos de la aplicación OneDrive en Dropbox. Configure este valor como **Bloquear**. Después de que los dispositivos reciben la directiva (por ejemplo, después de un reinicio), ya no permite guardar.

  > [!NOTE]
  > Cuando esta configuración está bloqueada, también se bloquean los teclados de terceros instalados desde App Store.

  - **Permitir que las aplicaciones no administradas lean en cuentas de contactos administradas**: **Permitir** habilita a las aplicaciones no administradas, como la aplicación Contactos integrada de iOS/iPadOS, para leer información de contacto y acceder a ella desde aplicaciones administradas, incluida la aplicación móvil Outlook. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir la lectura, incluso la eliminación de duplicados, en la aplicación Contactos integrada en los dispositivos.  
  
    Esta configuración permite o evita la lectura de información de contacto. No controla la sincronización de contactos entre las aplicaciones.
  
    Para usar este valor, establezca la opción **Visualización de documentos corporativos en aplicaciones no administradas** en **Bloquear**.

  Para más información sobre estos dos valores y cómo afecta a Outlook para la sincronización de exportación de contactos de iOS/iPadOS, consulte [Sugerencia de soporte técnico: uso de la configuración de perfil personalizada de Intune con la aplicación Contactos nativa de iOS/iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **Tratar AirDrop como destino no administrado**: **Requerir** obliga a que se considere a Airdrop un destino para colocar no administrado. Impide que las aplicaciones administradas envíen datos mediante AirDrop. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Visualización de documentos no corporativos en aplicaciones corporativas**: **Bloquear** evita la visualización de documentos no corporativos en aplicaciones corporativas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que cualquier documento se vea en aplicaciones administradas corporativas.

  **Bloquear** también impide la sincronización de la exportación de contactos en Outlook para iOS/iPadOS. Para obtener más información, vea [Sugerencia de soporte técnico: habilitación de la sincronización de contactos entre Outlook e iOS/iPadOS con controles de MDM de iOS12](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Requerir contraseña de iTunes Store para todas las compras**: **Requerir** exige que los usuarios escriban la contraseña del ID de Apple para cada compra en la aplicación o iTunes. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir las compras sin pedir una contraseña cada vez.
- **Compras desde la aplicación**: **Bloquear** impide las compras en la tienda desde la aplicación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir las compras en la tienda dentro de una aplicación en ejecución.
- **Descargar contenido marcado como "Erótico" en iBooks Store**: **Bloquear** impide que los usuarios descarguen elementos multimedia de iBooks Store marcados como eróticos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir permite que el usuario descargue libros con la categoría "Erotismo".
- **Permitir que las aplicaciones administradas escriban contactos en cuentas de contactos no administradas**: **Permitir** habilita a las aplicaciones administradas, como la aplicación móvil Outlook, para guardar o sincronizar la información de contacto, como los contactos corporativos y empresariales, en la aplicación Contactos integrada de iOS/iPadOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que las aplicaciones administradas guarden o sincronicen la información de contacto con la aplicación Contactos integrada de iOS/iPadOS en los dispositivos.
  
  Para usar este valor, establezca la opción **Visualización de documentos corporativos en aplicaciones no administradas** en **Bloquear**.

- **Región de clasificaciones**: Seleccione la región de clasificaciones que quiere usar para las descargas permitidas. Luego seleccione las clasificaciones permitidas para **Películas**, **Programas de TV** y **Aplicaciones**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Tienda de aplicaciones**: **Bloquear** evita el acceso a la tienda de aplicaciones en dispositivos supervisados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

  - **Instalación de aplicaciones de App Store**: **Bloquear** no muestra App Store en la pantalla principal del dispositivo. Los usuarios pueden seguir usando iTunes o Apple Configurator para instalar aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la tienda de aplicaciones en la pantalla principal.
  - **Descargas de aplicaciones automáticas**: **Bloquear** impide la descarga automática de las aplicaciones compradas en otros dispositivos y actualizaciones automáticas a nuevas aplicaciones. No afecta las actualizaciones de las aplicaciones existentes. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la descarga y actualización en el dispositivo de las aplicaciones compradas en otros dispositivos iOS/iPadOS.

- **Música, podcasts o contenido de noticias explícitos de iTunes**: **Bloquear** impide música, podcasts o contenido de noticias explícitos de iTunes. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el dispositivo acceda a contenido clasificado para adultos en la tienda.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Agregando amigos de Game Center**: **Bloquear** evita que los usuarios agreguen amigos de Game Center. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios agreguen amigos en Game Center.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Game Center**: **Bloquear** el uso de la aplicación Game Center. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Game Center en los dispositivos.
- **Juegos multijugador**: **Bloquear** impide el juego multijugador. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios jugar a juegos multijugador en los dispositivos.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Acceso a la unidad de red en la aplicación Files**: mediante el protocolo Bloque de mensajes del servidor (SMB), los dispositivos pueden acceder a archivos u otros recursos de un servidor de red. **Deshabilitar** evita el acceso a archivos de una unidad SMB de red. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso.

  Esta característica se aplica a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

## <a name="built-in-apps"></a>Aplicaciones integradas

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Siri**: **Bloquear** evita el acceso a Siri. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso del asistente de voz Siri en los dispositivos.
  - **Siri con dispositivo bloqueado**: **Bloquear** impide el acceso a Siri cuando los dispositivos están bloqueados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso del asistente de voz Siri en los dispositivos cuando están bloqueados.

- **Advertencias de fraude de Safari**: **Requerir** obliga a que las advertencias de fraude se muestren en el explorador web de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar esta característica.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)


- **Búsqueda de Spotlight para devolver resultados de Internet**: **Bloquear** evita que Spotlight devuelva resultados de una búsqueda en Internet. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la búsqueda de Spotlight se conecte a Internet para proporcionar resultados de la búsqueda.

  Esta configuración está duplicada en la interfaz de usuario y se corregirá en una próxima versión. Actualmente, esta configuración se aplica a los dispositivos supervisados. En una versión futura, esta configuración se aplicará a los dispositivos inscritos de dispositivo y a los dispositivos inscritos de dispositivo automatizado, y no requerirá supervisión.

- **Cookies de Safari**: seleccione cómo se controlan las cookies en los dispositivos. Las opciones son:
  - Allow
  - Bloquear todas las cookies
  - Permitir cookies de sitios web visitados
  - Permitir cookies del sitio web actual

- **JavaScript de Safari**: **Bloquear** impide que los scripts de Java del explorador se ejecuten en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir los scripts de Java.

- **Ventanas emergentes de Safari**: **Bloquear** bloquea todos los elementos emergentes en el explorador web Safari. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el bloqueador de elementos emergentes.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Cámara**: **Bloquear** impide el acceso a la cámara del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara del dispositivo.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

  - **FaceTime**: **Bloquear** impide el acceso a la aplicación FaceTime. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la aplicación FaceTime en los dispositivos.

    A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Filtro de obscenidad de Siri**: **Requerir** evita que Siri dicte o hable con un lenguaje malsonante. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  Para usar esta opción, establezca **Siri** en **Bloquear**.

  Esta característica se aplica a:  
  - iOS 11.0 y versiones más recientes

- **Siri para consultar contenido generado por usuarios de Internet**: **Bloquear** evita que Siri acceda a sitios web para responder preguntas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que Siri acceda al contenido generado por usuarios de Internet.

  Para usar esta opción, establezca **Siri** en **Bloquear**.

- **Apple News**: **Bloquear** impide el acceso a la aplicación Apple News en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Apple News.
- **iBooks Store**: **Bloquear** evita el acceso a la tienda de iBooks. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios examinen y compren libros en iBooks Store.
- **Aplicación Mensajes del dispositivo**: **Bloquear** impide que los usuarios usen la aplicación Mensajes para iMessage. Si los dispositivos admiten la mensajería de texto, los usuarios podrán seguir enviando y recibiendo mensajes de texto mediante SMS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Mensajes para enviar y leer mensajes mediante Internet.
- **Podcasts**: **Bloquear** evita que los usuarios usen la aplicación Podcasts. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Podcasts.
- **Servicio de música**: **Bloquear** revierte la aplicación Música al modo clásico y deshabilita el servicio Música. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Apple Music.
- **Servicio Radio de iTunes**: **Bloquear** impide el uso de la aplicación iTunes Radio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación iTunes Radio.
- **iTunes Store**: **Bloquear** impide el uso de iTunes en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de iTunes.

  Esta característica se aplica a:  
  - iOS 4.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Buscar mi iPhone**: **Bloquear** evita esta característica de la aplicación Buscar mi. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de esta característica de la aplicación Buscar mi para obtener la ubicación aproximada del dispositivo.

  Esta característica se aplica a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Buscar a mis amigos**: **Bloquear** evita esta característica de la aplicación Buscar mi. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir usar esta característica de la aplicación Buscar mi para encontrar familiares y amigos desde un dispositivo Apple o iCloud.com.

  Esta característica se aplica a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Cambios en la configuración de la aplicación Buscar a mis amigos**: **Bloquear** evita los cambios en la configuración de la aplicación Buscar a mis amigos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el usuario cambie la configuración de la aplicación Buscar a mis amigos.

- **Búsqueda de Spotlight para devolver resultados de Internet**: **Bloquear** evita que Spotlight devuelva resultados de una búsqueda en Internet. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la búsqueda de Spotlight se conecte a Internet para proporcionar resultados de la búsqueda.

  Esta configuración está duplicada en la interfaz de usuario y se corregirá en una próxima versión. Actualmente, esta configuración se aplica a los dispositivos supervisados. En una versión futura, esta configuración se aplicará a los dispositivos inscritos de dispositivo y a los dispositivos inscritos de dispositivo automatizado, y no requerirá supervisión.

- **Bloquear la eliminación de aplicaciones del sistema del dispositivo**: **Bloquear** deshabilita la capacidad de quitar aplicaciones del sistema de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios quiten aplicaciones del sistema.

- **Safari**: **Bloquear** el uso del explorador Safari en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios usar el explorador Safari.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Autorelleno de Safari**: **Bloquear** deshabilita la característica Autorrellenar de Safari en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de Autorrellenar del explorador web.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

## <a name="restricted-apps"></a>Aplicaciones restringidas

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Tipo de lista de aplicaciones restringidas**: cree una lista de aplicaciones que los usuarios no pueden instalar ni usar. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a las aplicaciones que se asignen y a las aplicaciones integradas.
  - **Aplicaciones prohibidas**: enumere las aplicaciones (que no se administran mediante Intune) que los usuarios no pueden instalar ni ejecutar. No se evita que los usuarios instalen una aplicación prohibida. Si un usuario instala una aplicación de esta lista, el dispositivo se muestra en el informe **Dispositivos con aplicaciones restringidas** (centro de administración de [Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Supervisar** > **Dispositivos con aplicaciones restringidas**). 
  - **Aplicaciones aprobadas**: Enumerar las aplicaciones que los usuarios pueden instalar. Para mantener el cumplimiento, los usuarios no deben instalar otras aplicaciones. Las aplicaciones que se administran mediante Intune están permitidas automáticamente, incluido el Portal de empresa. No se impide a los usuarios que instalen una aplicación que no se encuentra en la lista aprobada, Pero si lo hacen, se notifica en Intune.

Para agregar aplicaciones a estas listas, puede:

- **Agregar** la dirección URL de la tienda de aplicaciones de iTunes de la aplicación que quiere instalar. Por ejemplo, para agregar la aplicación Carpetas de trabajo de Microsoft, escriba `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` o `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`.

  Para buscar la dirección URL de una aplicación, abra la tienda de aplicaciones de iTunes y busque la aplicación. Por ejemplo, busque `Microsoft Remote Desktop` o `Microsoft Word`. Seleccione la aplicación y copie la dirección URL.

  También puede usar iTunes para buscar la aplicación y luego usar la tarea **Copiar vínculo** para obtener la dirección URL de la aplicación.

- **Importe** un archivo .csv con detalles sobre la aplicación, incluida la dirección URL. Use el formato `<app url>, <app name>, <app publisher>`. O bien **exporte** una lista existente que incluye la lista de aplicaciones restringidas en el mismo formato.

> [!IMPORTANT]
> Se deben asignar perfiles de dispositivo que usen configuración de aplicaciones restringidas para grupos de usuarios.

## <a name="shared-ipad"></a>iPad compartido

Esta característica se aplica a:

- IPadOS 13.4 y versiones más recientes
- iPad compartido

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Bloqueo de sesiones temporales de iPad compartido**: las sesiones temporales permiten a los usuarios iniciar sesión como invitado, sin necesidad de escribir una contraseña o un identificador de Apple administrado.

  Cuando se establece en **Sí**:

  - los usuarios de iPad compartido no pueden usar sesiones temporales.
  - Los usuarios tendrán que iniciar sesión en el dispositivo con el identificador y la contraseña de Apple administrados.
  - La opción Cuenta de invitado no se muestra en la pantalla de bloqueo de los dispositivos.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo permite a un usuario de iPad compartido iniciar sesión en el dispositivo con la cuenta de invitado. Cuando el usuario cierra la sesión, sus datos no se guardan ni se sincronizan con iCloud.

## <a name="show-or-hide-apps"></a>Aplicaciones visibles u ocultas

Esta característica se aplica a:

- iOS 9.3 y versiones más recientes
- IPadOS 13.0 y versiones más recientes

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Tipo de lista de aplicaciones**: cree una lista de aplicaciones para mostrar u ocultar. Puede mostrar u ocultar aplicaciones integradas y aplicaciones de línea de negocio. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094). Las opciones son:

  - **Aplicaciones ocultas**: Escriba una lista de las aplicaciones ocultas a los usuarios. Los usuarios no pueden ver ni abrir estas aplicaciones.
  
    Apple evita ocultar algunas aplicaciones nativas. Por ejemplo, no puede ocultar la aplicación **Configuración** en el dispositivo. [Delete built-in Apple apps](https://support.apple.com/HT208094) (Eliminar aplicaciones integradas de Apple) muestra las aplicaciones que se pueden ocultar.
  
  - **Aplicaciones visibles**: Especifique una lista de las aplicaciones que los usuarios pueden ver e iniciar. No se puede ver ni iniciar ninguna otra aplicación.

- **Dirección URL de la aplicación**: escriba la dirección URL de la aplicación de la tienda que quiere mostrar u ocultar. Por ejemplo:

  - Para agregar la aplicación Carpetas de trabajo de Microsoft, escriba `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` o `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`. 

  - Para agregar la aplicación Microsoft Word, escriba `https://itunes.apple.com/de/app/microsoft-word/id586447913` o `https://apps.apple.com/de/app/microsoft-word/id586447913`.

  Para buscar la dirección URL de una aplicación, abra la tienda de aplicaciones de iTunes y busque la aplicación. Por ejemplo, busque `Microsoft Remote Desktop` o `Microsoft Word`. Seleccione la aplicación y copie la dirección URL.

  También puede usar iTunes para buscar la aplicación y luego usar la tarea **Copiar vínculo** para obtener la dirección URL de la aplicación.

- **Identificador de lote de aplicaciones**: escriba el [identificador del lote](bundle-ids-built-in-ios-apps.md) de aplicaciones de la aplicación que quiere. Puede mostrar u ocultar aplicaciones integradas y aplicaciones de línea de negocio. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).
- **Nombre de la aplicación**: escriba el nombre de la aplicación que quiere. Puede mostrar u ocultar aplicaciones integradas y aplicaciones de línea de negocio. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).
- **Publicador**: escriba el publicador de la aplicación que quiere.

Para agregar aplicaciones, puede:

- **Agregar**: seleccione para crear la lista de aplicaciones.
- **Importe** un archivo .csv con detalles sobre la aplicación, incluida la dirección URL. Use el formato `<app url>, <app name>, <app publisher>`. O bien, **Exportar** para crear una lista de las aplicaciones restringidas que ha agregado, en el mismo formato.

## <a name="wireless"></a>Inalámbrico

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Itinerancia de datos**: **Bloquear** impide la itinerancia de datos a través de la red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la itinerancia de datos cuando el dispositivo está en una red de telefonía móvil.

  > [!IMPORTANT]
  > Esta configuración se trata como una acción de dispositivo remoto. Por lo tanto, no se muestra en el perfil de administración de los dispositivos. Cada vez que cambia el estado de itinerancia de datos en el dispositivo, el servicio Intune bloquea **Itinerancia de datos**. En Intune, si el estado de las notificaciones muestra que todo es correcto, sepa que funciona, aunque la configuración no se muestre en el perfil de administración del dispositivo.

- **Captura de fondo global durante la itinerancia**: **Bloquear** evita el uso de la característica de captura de fondo global durante la itinerancia a través de la red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los dispositivos capturen datos, como el correo electrónico, durante la itinerancia en una red de telefonía móvil.
- **Marcación por voz**: **Bloquear** impide el uso de la característica de marcación por voz en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la marcación por voz en los dispositivos.
- **Itinerancia de voz**: **Bloquear** impide la itinerancia de voz a través de la red de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la itinerancia de voz cuando los dispositivos están en una red de telefonía móvil.
- **Punto de acceso personal**: **Bloquear** desactiva el punto de acceso personal en los dispositivos con la sincronización de cada dispositivo. Esta opción puede que no sea compatible con algunos operadores. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mantener la configuración de punto de acceso personal como el valor predeterminado establecido por el usuario.

  > [!IMPORTANT]
  > Esta configuración se trata como una acción de dispositivo remoto. Por lo tanto, no se muestra en el perfil de administración de los dispositivos. Cada vez que cambia el estado del punto de acceso personal en el dispositivo, el servicio Intune bloquea **Punto de acceso personal**. En Intune, si el estado de las notificaciones muestra que todo es correcto, significa que funciona, aunque la configuración no se muestre en el perfil de administración del dispositivo.

- **Reglas de uso de datos móviles (solo aplicaciones administradas)** : **Permitir** define los tipos de datos que las aplicaciones administradas pueden usar cuando están en redes de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Las opciones son:
  - **Bloquear el uso de datos móviles**: Bloquee el uso de los datos móviles en **Todas las aplicaciones administradas** o **Elegir aplicaciones específicas**.
  - **Bloquear uso de datos móviles en itinerancia**: Bloquee el uso de los datos móviles en itinerancia en **Todas las aplicaciones administradas** o **Elegir aplicaciones específicas**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Cambios en la configuración de uso de datos móviles de la aplicación**: **Bloquear** impide los cambios en la configuración de uso de datos móviles de la aplicación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el usuario controle qué aplicaciones pueden usar datos móviles.
- **Cambios en la configuración del plan de red de telefonía móvil**: **Bloquear** impide cambiar la configuración en el plan de telefonía móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios hagan cambios.

  Esta característica se aplica a:  
  - iOS 11.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Modificación por el usuario del punto de acceso personal**: **Bloquear** impide cambiar la configuración personal del punto de acceso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios finales habilitar o deshabilitar su punto de acceso personal.

  Si bloquea esta configuración y también **Punto de acceso personal**, se desactiva el punto de acceso personal.

  Esta característica se aplica a:  
  - iOS 12.2 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Conexión a redes Wi-Fi solo con perfiles de configuración**: **Requerir** fuerza a los dispositivos a usar solo las redes Wi-Fi configuradas mediante perfiles de configuración de Intune. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los dispositivos usen otras redes Wi-Fi.

  Si se establece en **Requerir**, asegúrese de que el dispositivo tiene un perfil de Wi-Fi. Si no se asigna un perfil de Wi-Fi, este valor podría evitar que los dispositivos se conecten a Internet. Es decir, si este perfil de restricciones de dispositivos se asigna antes que un perfil de Wi-Fi, es posible que el dispositivo no pueda conectarse a Internet.
  
  Si no se puede conectar, anule la inscripción del dispositivo y vuelva a inscribirlo con un perfil de Wi-Fi. Luego establezca esta opción en **Requerir** en un perfil de restricciones de dispositivos y asigne el perfil al dispositivo.

- **Conexión Wi-Fi siempre activada**: **Requerir** mantiene la conexión Wi-Fi activada en la aplicación Configuración. No se puede desactivar en Configuración ni en el centro de control, aun cuando el dispositivo esté en modo avión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios activen o desactiven la conexión Wi-Fi.

  La configuración de esta opción no evita que los usuarios seleccionen una red Wi-Fi.

  Esta característica se aplica a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

## <a name="connected-devices"></a>Dispositivos conectados

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Detección de muñeca para Apple Watch enlazados**: **Requerir** fuerza a los dispositivos Apple Watch emparejados a usar la detección de muñeca. Cuando se requiere, el dispositivo Apple Watch no mostrará notificaciones si no se lleva puesto. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Requerir contraseña de emparejamiento para solicitudes salientes de AirPlay**: **Requerir** exige una contraseña de emparejamiento cuando se usa AirPlay para transmitir contenido a otros dispositivos de Apple. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios transmitir contenido mediante AirPlay sin tener que escribir una contraseña.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **AirDrop**: **Bloquear** evita el uso de AirDrop en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir usar la característica AirDrop para intercambiar contenido con dispositivos cercanos.
- **Enlace con Apple Watch**: **Bloquear** evita el emparejamiento con Apple Watch. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el emparejamiento de los dispositivos con un Apple Watch.
- **Modificación de Bluetooth**: **Bloquear** impide que los usuarios cambien la configuración de Bluetooth en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración.
- **Emparejamiento de host para controlar los dispositivos con los que se puede emparejar un dispositivo iOS/iPadOS**: **Bloquear** impide el emparejamiento de host. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el emparejamiento de host deje al administrador controlar con qué dispositivos se puede emparejar un dispositivo iOS/iPadOS.
- **Bloquear AirPrint**: **Bloquear** impide el uso de la característica AirPrint en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen AirPrint.
  - **Bloquear el almacenamiento de credenciales de AirPrint en Keychain**: **Bloquear** impide el uso del almacenamiento de Keychain para el nombre de usuario y la contraseña en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir almacenar el nombre de usuario y la contraseña de AirPrint en la aplicación Keychain.
  - **Requerir un certificado de confianza TLS para AirPrint**: **Requerir** fuerza a los dispositivos a usar certificados de confianza para la comunicación de impresión de TLS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Bloquear la detección de iBeacon de impresoras AirPrint**: **Bloquear** evita que balizas Bluetooth de AirPrint malintencionadas suplanten la identidad en el tráfico de red. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el anuncio de impresoras AirPrint en los dispositivos.
- **Bloquear la configuración de nuevos dispositivos cercanos**: **Bloquear** deshabilita el símbolo del sistema para configurar nuevos dispositivos cercanos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir solicitudes de los usuarios para conectarse a otros dispositivos Apple cercanos.

  Esta característica se aplica a:  
  - iOS 11.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Acceso a los archivos de la unidad USB**: los dispositivos pueden conectarse a una unidad USB y abrir los archivos que contiene. **Deshabilitar** evita el acceso del dispositivo a la unidad USB en la aplicación Files cuando hay un USB conectado al dispositivo. Al deshabilitar esta característica también se evita que los usuarios transfieran archivos a una unidad USB conectada a un dispositivo iPad. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a una unidad USB en la aplicación Files.

  Esta característica se aplica a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

## <a name="keyboard-and-dictionary"></a>Teclado y diccionario

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Búsqueda de definiciones de palabras**: **Bloquear** impide el resaltado de una palabra y luego la búsqueda de su definición. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la característica de búsqueda de definiciones.
- **Teclados predictivos**: **Bloquear** impide el uso de teclados predictivos para sugerir las palabras que puedan querer los usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.
- **Autocorrección**: **Bloquear** impide usar la autocorrección. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los dispositivos corrijan automáticamente las palabras mal escritas.
- **Revisión ortográfica de teclado**: **Bloquear** impide el corrector ortográfico. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso del corrector ortográfico.
- **Métodos abreviados de teclado**: **Bloquear** impide que los usuarios usen los métodos abreviados de teclado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de accesos directos de teclado en los dispositivos.
- **Dictado**: **Bloquear** impide que los usuarios usen la entrada de voz para escribir texto. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen la entrada de dictado.
- **QuickPath**: **Bloquear** evita que los usuarios usen QuickPath. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen QuickPath, que permite una entrada continua en el teclado del dispositivo. Los usuarios pueden escribir al deslizar el dedo por las teclas para crear palabras.

  Esta característica se aplica a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

## <a name="cloud-and-storage"></a>Nube y almacenamiento

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Copia de seguridad cifrada**: **Requerir** obliga a que las copias de seguridad del dispositivo se cifren. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Sincronización de aplicaciones administradas con la nube**: **Bloquear** impide que Intune administre las aplicaciones para sincronizar los datos con la cuenta de iCloud de los usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta sincronización de los datos con iCloud.
- **Bloquear la copia de seguridad de libros empresariales**: **Bloquear** impide las copias de seguridad de libros empresariales. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios hagan copias de seguridad de estos libros.
- **Bloquear la sincronización de metadatos de libros empresariales (notas y eventos destacados)** : **Bloquear** evita la sincronización de notas y eventos destacados de libros empresariales. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Sincronización de Photo Stream en iCloud**: **Bloquear** impide la sincronización de Photo Stream en iCloud. El bloqueo de esta característica puede provocar una pérdida de datos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios habiliten **My Photo Stream** en su dispositivo para sincronizar en iCloud y que las fotos estén disponibles en todos los dispositivos del usuario.
- **Fototeca de iCloud**: **Bloquear** deshabilita el uso de la Fototeca de iCloud para almacenar fotos y vídeos en la nube. Las fotos que no se hayan descargado de la Fototeca de iCloud en los dispositivos se quitarán del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir usar la Fototeca de iCloud.
- **Fotos en streaming compartidas**: **Bloquear** deshabilita las **Fotos compartidas de iCloud** en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el streaming de fotografías compartidas.
- **Handoff**: **Bloquear** impide que los usuarios inicien el trabajo en un dispositivo iOS/iPadOS y, después, lo continúen en otro dispositivo iOS/iPadOS o macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica Handoff.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Copia de seguridad en iCloud**: **Bloquear** impide que los usuarios creen una copia de seguridad de los dispositivos en iCloud. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios realicen una copia de seguridad de los dispositivos en iCloud.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Bloquear la sincronización de documentos en iCloud**: **Bloquear** impide que iCloud sincronice documentos y datos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de clave-valor y documentos en el espacio de almacenamiento de iCloud.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

- **Bloquear la sincronización de Keychain en iCloud**: **Bloquear** deshabilita la sincronización de las credenciales almacenadas en Keychain en iCloud. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios sincronicen estas credenciales.

  A partir de iOS/iPadOS 13.0, esta configuración requiere dispositivos supervisados.

## <a name="autonomous-single-app-mode-asam"></a>Modo de aplicación única autónoma (ASAM)

Use estos valores para configurar los dispositivos iOS/iPadOS de modo que ejecuten aplicaciones específicas en modo de aplicación única autónoma (ASAM). Si se configura este modo y los usuarios inician una de las aplicaciones configuradas, el dispositivo se bloqueará para esa aplicación. La conmutación de tareas y aplicaciones se deshabilitará hasta que los usuarios salgan de la aplicación permitida.

Para que se aplique la configuración de ASAM, los usuarios deben abrir manualmente la aplicación específica. Esta tarea también se aplica a la aplicación Portal de empresa.

- Por ejemplo, en un entorno educativo o universitario, agregue una aplicación que permita que los usuarios realicen una prueba en el dispositivo. Otra opción es bloquear el dispositivo en la aplicación Portal de empresa hasta que el usuario se autentique. Cuando los usuarios completen las acciones de la aplicación o quite esta directiva, el dispositivo volverá a su estado normal.

- No todas las aplicaciones admiten el modo de aplicación única autónoma. Para activar el modo de aplicación única autónoma, normalmente se requiere un identificador de lote de aplicaciones o un par clave-valor entregado por una directiva de configuración de aplicaciones. Para obtener más información, consulte el artículo sobre la [restricción `autonomousSingleAppModePermittedAppIDs`](https://developer.apple.com/documentation/devicemanagement/restrictions) en la documentación MDM de Apple. Para obtener más información sobre la configuración específica necesaria para la aplicación que vaya a configurar, consulte la documentación del proveedor.

  Por ejemplo, para configurar las salas de Zoom en el modo de aplicación única autónoma, Zoom indica que es necesario usar el id. de lote de aplicaciones `us.zoom.zpcontroller`. En esta instancia, también se realiza un cambio en el portal web de Zoom. Para obtener más información, consulte el [centro de ayuda de Zoom](https://support.zoom.us/hc/articles/360021322632-Autonomous-Single-App-Mode-for-Zoom-Rooms-with-a-Third-Party-MDM).

- En dispositivos iOS/iPadOS, la aplicación Portal de empresa admite ASAM. Cuando la aplicación Portal de empresa está en ASAM, los usuarios deben abrirla manualmente. Después, el dispositivo se bloquea en la aplicación Portal de empresa hasta que el usuario se autentica. Cuando los usuarios inician sesión en la aplicación Portal de empresa, pueden usar otras aplicaciones y el botón Pantalla principal del dispositivo. Cuando cierran sesión en la aplicación Portal de empresa, el dispositivo vuelve al modo de aplicación única y se bloquea en la aplicación Portal de empresa.

  Para convertir la aplicación Portal de empresa en una aplicación de "inicio y cierre de sesión" (habilitar ASAM), escriba el nombre de la aplicación Portal de empresa, como `Microsoft Intune Company Portal`y el identificador de paquete (`com.microsoft.CompanyPortal`) en esta configuración. Una vez que se haya asignado este perfil, debe abrir la aplicación Portal de empresa para bloquearla de modo que los usuarios puedan iniciar y cerrar sesión en ella. Para que se aplique la configuración de ASAM, los usuarios deben abrir manualmente la aplicación Portal de empresa.
  
  Cuando se quita el perfil de configuración del dispositivo y el usuario cierra la sesión, el dispositivo no está bloqueado en la aplicación Portal de empresa.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Nombre de la aplicación**: escriba el nombre de la aplicación que quiere.
- **Identificador de lote de aplicaciones**: escriba el [identificador del lote](bundle-ids-built-in-ios-apps.md) de la aplicación que quiere.
- **Agregar**: seleccione para crear la lista de aplicaciones.

También puede **importar** un archivo .csv con la lista de nombres de aplicaciones y sus identificadores de lote. O bien puede **Exportar** una lista existente que incluya las aplicaciones.

## <a name="kiosk"></a>Pantalla completa

El [modo de aplicación única](https://support.apple.com/guide/mdm/mdm80a981/web) se denomina Pantalla completa en Intune.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Aplicación para ejecutar en modo de pantalla completa**: seleccione el tipo de aplicaciones que quiere que se ejecuten en modo de pantalla completa. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no aplique la configuración de pantalla completa. El dispositivo no se ejecuta en modo de pantalla completa.
  - **Aplicación de la Tienda**: escriba la dirección URL de una aplicación de la tienda de aplicaciones de iTunes.
  - **Aplicación administrada**: seleccione una aplicación que se haya agregado previamente a Intune.
  - **Aplicación integrada**: escriba el [identificador del lote](bundle-ids-built-in-ios-apps.md) de la aplicación integrada.

- **AssistiveTouch**: **Requerir** que la configuración de accesibilidad AssistiveTouch se establezca en los dispositivos. Esta característica ayuda a los usuarios con gestos en pantalla que podrían ser difíciles para ellos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no ejecutar ni habilitar esta característica en pantalla completa.
- **Invertir colores**: **Requerir** la configuración de accesibilidad Invertir colores para que los usuarios con discapacidades visuales puedan cambiar la pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no ejecutar ni habilitar esta característica en pantalla completa.
- **Audio mono**: **Requerir** que la configuración de accesibilidad Audio mono esté establecida en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no ejecutar ni habilitar esta característica en pantalla completa.
- **Control de voz**: **Requerir** habilita el control de voz en los dispositivos y permite a los usuarios controlar por completo el sistema operativo mediante los comandos de Siri. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar el control de voz.

  Esta configuración solo es aplicable a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes
  
  > [!TIP]
  > Si tiene aplicaciones de LOB disponibles para la organización y no están preparadas para el **Control de voz** en el día 0 cuando se publique iOS 13.0, se recomienda dejar este valor como **Sin configurar**.

- **VoiceOver**: **Requerir** la configuración de accesibilidad VoiceOver para leer en voz alta el texto en pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no ejecutar ni habilitar esta característica en pantalla completa.
- **Zoom**: **Requerir** la configuración de Zoom a fin de que los usuarios puedan tocar para acercar la pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no ejecutar ni habilitar esta característica en pantalla completa.
- **Bloqueo automático**: **Bloquear** impide el bloqueo automático de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.
- **Cambio de timbre**: **Bloquear** deshabilita el conmutador de timbre (silencio) en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.
- **Rotación de pantalla**: **Bloquear** impide cambiar la orientación de la pantalla cuando el usuario gira el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.
- **Botón de suspensión de pantalla**: **Bloquear** deshabilita el botón de reposo/activación de pantalla en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.
- **Toque**: **Bloquear** deshabilita la pantalla táctil en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios usar la pantalla táctil.
- **Botones de volumen**: **Bloquear** impide el uso de los botones de volumen en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir los botones de volumen.
- **Control de AssistiveTouch**: **Permitir** habilita a los usuarios para usar la función AssistiveTouch. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar esta característica.
- **Control Invertir colores**: **Permitir** invierte los cambios de color para que los usuarios puedan ajustar la función Invertir colores. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar esta característica.
- **Leer el texto seleccionado**: **Permitir** que la configuración de accesibilidad Reproducir selección esté establecida en los dispositivos. Esta característica lee en voz alta el texto que los usuarios seleccionan. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar esta característica.
- **Modificación del control de voz**: **Permitir** deja a los usuarios cambiar el estado del control de voz en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir que los usuarios cambien el estado del control de voz en sus dispositivos.

  Esta configuración solo es aplicable a:  
  - iOS 13.0 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

- **Control de VoiceOver**: **Permitir** cambios de VoiceOver para que los usuarios puedan actualizar la función VoiceOver, por ejemplo, la velocidad con que el texto en pantalla se lee en voz alta. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir los cambios en VoiceOver.
- **Control de zoom**: **Permitir** que los usuarios haga cambios en el zoom. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir los cambios en el zoom.

> [!NOTE]
> Antes de configurar un dispositivo iOS/iPadOS para el modo de pantalla completa, se debe usar la herramienta Apple Configurator o el Programa de inscripción de dispositivos de Apple para poner los dispositivos en modo supervisado. Consulte la guía de Apple sobre cómo usar la herramienta Apple Configurator.
> Si la aplicación iOS/iPadOS que escriba se instala después de asignar el perfil, el dispositivo no entrará en el modo de pantalla completa hasta que se lo reinicie.

## <a name="domains"></a>Dominios

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivos, también en el caso de la inscripción automatizada (con supervisión)

- **Dominios de correo electrónico no marcados** > **URL de dominio de correo electrónico**: agregue una o más direcciones URL a la lista. Cuando los usuarios reciben un correo electrónico de un dominio distinto al especificado, el correo electrónico se marca como correo electrónico no de confianza en la aplicación Correo de iOS/iPadOS.

- **Dominios web administrados** > **URL de dominio web**: agregue una o varias URL a la lista. Los documentos que se descargan de los dominios que especifica se consideran administrados. Esta configuración solo se aplica a los documentos que se descargan con el explorador Safari.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada (supervisado)

- **Dominios de relleno automático de contraseña de Safari** > **URL de dominio**: agregue una o más direcciones URL a la lista. Los usuarios solo pueden guardar contraseñas web de las direcciones URL que aparecen en esta lista. Esta configuración solo se aplica al explorador Safari y a dispositivos en modo supervisado. Si no escribe ninguna dirección URL, se podrán guardar contraseñas de todos los sitios web.

  Esta configuración solo es aplicable a:  
  - iOS 9.3 y versiones más recientes
  - IPadOS 13.0 y versiones más recientes

## <a name="settings-that-require-supervised-mode"></a>Configuraciones que necesitan el modo supervisado

El modo supervisado de iOS/iPadOS solo se puede habilitar durante la configuración inicial del dispositivo a través del Programa de inscripción de dispositivos de Apple o con Apple Configurator. Una vez activado el modo supervisado, Intune puede configurar un dispositivo con la funcionalidad siguiente:

- Modo de pantalla completa (modo de aplicación única): Se conoce como "bloqueo de aplicación" en la [documentación para desarrolladores de Apple](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf).
- Deshabilitación del bloqueo de activación 
- Modo de aplicación única autónoma 
- Filtro de contenido web 
- Establecer la pantalla de fondo y la pantalla de bloqueo 
- Inserción de aplicación silenciosa 
- VPN Always-On 
- Permitir la instalación de aplicaciones administradas de forma exclusiva 
- iBookstore 
- iMessages 
- Centro de juegos 
- AirDrop 
- AirPlay 
- Emparejamiento de host 
- Sincronización en la nube 
- Búsqueda en Spotlight 
- Handoff 
- Borrar dispositivo 
- Interfaz de usuario de restricciones 
- Instalación de perfiles de configuración por interfaz de usuario 
- Noticias 
- Métodos abreviados de teclado 
- Modificaciones de código de acceso 
- Cambios en los nombres de dispositivos 
- Descargas de aplicaciones automáticas 
- Apple Music 
- Mail Drop 
- Emparejamiento con Apple Watch 

> [!NOTE]
> Apple ha confirmado que ciertas opciones de configuración se trasladan al modo de solo supervisión en 2019. Le recomendamos que lo tenga en cuenta a la hora de usar estas opciones, en lugar de esperar a que Apple las migre al modo de solo supervisión:
>
> - Instalación de la aplicación por los usuarios finales
> - Eliminación de aplicaciones
> - FaceTime
> - Safari
> - iTunes
> - Contenido explícito
> - Documentos y datos de iCloud
> - Juego multijugador
> - Agregar amigos de Game Center
> - Siri

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede restringir la configuración y las características de los dispositivos en dispositivos [macOS](device-restrictions-macos.md).
