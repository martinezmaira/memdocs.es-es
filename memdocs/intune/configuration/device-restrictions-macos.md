---
title: Configuración de dispositivo macOS en Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Agregue, configure o cree valores en dispositivos macOS para restringir características, lo que incluye establecer requisitos de contraseña, controlar la pantalla de bloqueo, usar aplicaciones integradas, agregar aplicaciones restringidas o aprobadas, controlar dispositivos Bluetooth, conectarse a la nube para realizar copias de seguridad y almacenar, habilitar la pantalla completa, agregar dominios y controlar la manera en que los usuarios interactúan con el explorador web Safari en Microsoft Intune.
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
ms.openlocfilehash: 50dd3d245b9a89836e3858d71a7ad124189e0973
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407848"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Configuración de dispositivos macOS para permitir o restringir características mediante Intune

En este artículo se enumeran y describen los diferentes valores de configuración que se pueden controlar en los dispositivos macOS. Como parte de la solución de administración de dispositivos móviles (MDM), use estos valores para habilitar o deshabilitar características, establecer reglas de contraseña, permitir o restringir determinadas aplicaciones, etc.

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos macOS.

## <a name="before-you-begin"></a>Antes de comenzar

[Crear un perfil de configuración de restricciones de dispositivos](device-restrictions-configure.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción. Para más información sobre los diferentes tipos de inscripción, consulte [Inscripción en macOS](../enrollment/macos-enroll.md).

## <a name="general"></a>General

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **Búsqueda de definiciones**: **Bloquear** evita que el usuario resalte una palabra y luego busque su definición en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la característica de búsqueda de definiciones.
- **Dictado**: **Bloquear** impide que los usuarios usen la entrada de voz para escribir texto. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen la entrada de dictado.
- **Almacenamiento en caché de contenido**: **Bloquear** impide el almacenamiento en caché de contenido. El almacenamiento en caché de contenido almacena localmente en los dispositivos datos de aplicaciones, datos del explorador web, descargas y mucho más. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede habilitar el almacenamiento en caché de contenido.

  Para más información sobre el almacenamiento en caché de contenido en macOS, vea [Gestionar el almacenamiento en caché de contenido en el Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (abre otro sitio web).

  Esta característica se aplica a:  
  - macOS 10.13 y versiones más recientes

- **Aplazar las actualizaciones de software**: **Habilitar** permite retrasar la visualización de las actualizaciones en el dispositivo, entre 0 y 90 días. Esta configuración no controla cuándo se instalan las actualizaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las actualizaciones en los dispositivos a medida que Apple las publica. Por ejemplo, si Apple publica una actualización de macOS en una fecha concreta, dicha actualización naturalmente se mostrará en los dispositivos en torno a la fecha de publicación. Se permiten las actualizaciones de compilación de inicialización sin retraso.  

  - **Retrasar la visibilidad de las actualizaciones de software**: especifique un valor entre 0 y 90 días. Cuando el retraso expira, los usuarios reciben una notificación para actualizar a la versión más antigua del sistema operativo que estaba disponible cuando se desencadenó el retraso.

    Por ejemplo, si hay una actualización de macOS disponible **el 1 de enero** y **Retrasar la visibilidad** está establecido en **5 días**, la actualización no se muestra como una actualización disponible. Al **sexto día** después de la publicación, esta actualización estará disponible y los usuarios podrán instalarla.

    Esta característica se aplica a:  
    - macOS 10.13.4 y versiones más recientes

- **Capturas de pantalla**: el dispositivo debe inscribirse en la Inscripción de dispositivo automatizada (DEP) de Apple. **Bloquear** impide que los usuarios guarden capturas de pantalla. También evita que la aplicación Classroom observe pantallas remotas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios realizar capturas de pantalla y hacer posible que la aplicación Classroom vea pantallas remotas.

### <a name="settings-apply-to-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivo automatizada

- **Observación de pantalla remota mediante la aplicación Classroom**: **Deshabilitar** evita que los profesores usen la aplicación Classroom para ver las pantallas de sus alumnos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los profesores vean las pantallas de sus alumnos.

  Para usar esta opción, establezca el valor **Capturas de pantallas** en **No configurado** (se permiten capturas de pantallas).

- **Observación de pantalla sin mensajes por la aplicación Classroom**: **Permitir** habilita a los profesores para ver las pantallas de sus alumnos aunque estos no estén de acuerdo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría requerir que los alumnos estén de acuerdo antes de que los profesores puedan ver las pantallas.

  Para usar esta opción, establezca el valor **Capturas de pantallas** en **No configurado** (se permiten capturas de pantallas).

- **Los alumnos deben solicitar permiso para abandonar la clase de Classroom**: **Requerir** obliga a los alumnos inscritos en un curso de Classroom no administrado a obtener la aprobación del profesor para abandonar el curso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los alumnos abandonen el curso siempre que así lo decidan.

- **Los profesores pueden bloquear automáticamente dispositivos o aplicaciones en la aplicación Classroom**: **Permitir** habilita a los profesores para bloquear el dispositivo o la aplicación de un alumno sin su aprobación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría requerir que los alumnos estén de acuerdo antes de que los profesores puedan bloquear el dispositivo o la aplicación.

- **Los alumnos pueden unirse automáticamente a la clase de Classroom**: **Permitir** habilita a los alumnos para unirse a una clase sin preguntar al profesor. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría requerir la aprobación del profesor para unirse a una clase.

## <a name="password"></a>Contraseña

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **Contraseña**: **Requerir** que los usuarios escriban una contraseña para acceder a los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no requiera una contraseña. Tampoco obliga a ninguna restricción, como el bloqueo de contraseñas sencillas o la configuración de una longitud mínima.
  - **Tipo de contraseña requerida**: escriba el nivel de complejidad de la contraseña requerido que exija su organización. Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Numérica**: la contraseña solo debe contener números, por ejemplo, 123456789.
    - **Alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos.

    Esta característica se aplica a:  
    - macOS 10.10.3 y versiones más recientes

  - **Número de caracteres no alfanuméricos en la contraseña**: escriba el número de caracteres complejos que requiere la contraseña, entre 0 y 4. Un carácter complejo es un símbolo, por ejemplo, `?`.
  - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres.
  - **Contraseñas sencillas**: permita contraseñas sencillas, como `0000` o `1234`.
  - **Máximo de minutos tras bloqueo de pantalla antes de solicitar la contraseña**: escriba el tiempo durante el cual los dispositivos deben estar inactivos antes de que se solicite una contraseña para desbloquearlos. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
  - **Máximo de minutos de inactividad hasta que se bloquea la pantalla**: escriba el tiempo durante el cual los dispositivos deben estar inactivos antes de que se bloquee automáticamente la pantalla. Por ejemplo, escriba 5 para bloquear los dispositivos tras estar 5 minutos inactivos. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
  - **Expiración de la contraseña (días)** : escriba el número de días, entre 1 y 65535, hasta que se deba cambiar la contraseña del dispositivo. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando la contraseña expire, se le solicitará a los usuarios que creen una nueva contraseña. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.
  - **Impedir la reutilización de contraseñas anteriores**: utilice esta configuración para impedir que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba 5 para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en ninguna de sus cuatro anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.

- **Impedir al usuario modificar el código de acceso**: **Bloquear** evita que se cambie, se agregue o se quite el código de acceso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que se cambie, se agregue o se quite el código de acceso.
- **Impedir el desbloqueo mediante huella digital**: **Bloquear** impide el uso de huellas digitales para desbloquear los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios desbloqueen el dispositivo mediante una huella digital.

- **Impedir el relleno automático de contraseñas**: **Bloquear** impide el uso de la característica Autorrellenar contraseñas en macOS. Si elige **Bloquear** tendrá también este impacto:

  - No se les pide a los usuarios que usen una contraseña guardada en Safari ni en ninguna aplicación.
  - Se deshabilitan las contraseñas seguras automáticas y no se sugieren contraseñas seguras a los usuarios.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas características.

- **Impedir las solicitudes de proximidad de contraseñas**: **Bloquear** impide que los dispositivos soliciten contraseñas de dispositivos cercanos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas solicitudes de contraseña.

- **Impedir el uso compartido de contraseñas**: **Bloquear** evita el uso compartido de contraseñas entre dispositivos mediante AirDrop. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo permita que estas contraseñas se compartan.

## <a name="built-in-apps"></a>Aplicaciones integradas

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **Bloquear Autorrelleno en Safari**: **Bloquear** deshabilita la característica Autorrellenar de Safari en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de Autorrellenar del explorador web.
- **Bloquear la cámara**: **Bloquear** impide el acceso a la cámara en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara del dispositivo.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.

- **Bloquear Apple Music**: **Bloquear** revierte la aplicación Música al modo clásico y deshabilita el servicio Música. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Apple Music.
- **Bloquear resultados de búsquedas de Internet de Spotlight**: **Bloquear** evita que Spotlight devuelva resultados de una búsqueda en Internet. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la búsqueda de Spotlight se conecte a Internet y proporcione resultados de la búsqueda.
- **Bloquear transferencia de archivos mediante iTunes**: **Bloquear** deshabilita los servicios de uso compartido de archivos de aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir los servicios de uso compartido de archivos de la aplicación.

  Esta característica se aplica a:  
  - macOS 10.13 y versiones más recientes

## <a name="restricted-apps"></a>Aplicaciones restringidas

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **Tipo de lista de aplicaciones restringidas**: cree una lista de aplicaciones que los usuarios no pueden instalar ni usar. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, los usuarios podrían tener acceso a las aplicaciones que asigne y a las aplicaciones integradas.
  - **Aplicaciones prohibidas**: enumere las aplicaciones (que no se administran mediante Intune) que los usuarios no pueden instalar ni ejecutar. No se evita que los usuarios instalen una aplicación prohibida. Si un usuario instala una aplicación de esta lista, se notifica en Intune.
  - **Aplicaciones aprobadas**: Enumerar las aplicaciones que los usuarios pueden instalar. Para mantener el cumplimiento, los usuarios no deben instalar otras aplicaciones. Las aplicaciones que se administran mediante Intune están permitidas automáticamente, incluido el Portal de empresa. No se impide a los usuarios que instalen una aplicación que no se encuentra en la lista aprobada, Pero si lo hacen, se notifica en Intune.

- **Identificador de lote de aplicaciones**: escriba el [identificador del lote](bundle-ids-built-in-ios-apps.md) de aplicaciones de la aplicación que quiere. Puede mostrar u ocultar aplicaciones integradas y aplicaciones de línea de negocio. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).
- **Nombre de la aplicación**: escriba el nombre de la aplicación que quiere. Puede mostrar u ocultar aplicaciones integradas y aplicaciones de línea de negocio. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).
- **Publicador**: escriba el editor de la aplicación.

Para agregar aplicaciones a estas listas, puede:

- **Agregar**: seleccione para crear la lista de aplicaciones.
- **Importe** un archivo .csv con detalles sobre la aplicación, incluida la dirección URL. Use el formato `<app bundle ID>, <app name>, <app publisher>`. O bien, use **Exportar** para crear una lista de las aplicaciones agregadas, en el mismo formato.

## <a name="connected-devices"></a>Dispositivos conectados

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **Bloquear AirDrop**: **Bloquear** evita el uso de AirDrop en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir usar la característica AirDrop para intercambiar contenido con dispositivos cercanos.
- **Impedir el desbloqueo automático de Apple Watch**: **Bloquear** evita que los usuarios desbloqueen su dispositivo macOS con su Apple Watch. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios desbloquear su dispositivo macOS con su Apple Watch.

## <a name="cloud-and-storage"></a>Nube y almacenamiento

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **Bloquear la sincronización de Keychain en iCloud**: **Bloquear** deshabilita la sincronización de las credenciales almacenadas en Keychain en iCloud. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios sincronicen estas credenciales.
- **Bloquear la sincronización de documentos en iCloud**: **Bloquear** impide que iCloud sincronice documentos y datos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de clave-valor y documentos en el espacio de almacenamiento de iCloud.
- **Bloquear la copia de seguridad de iCloud Mail**: **Bloquear** evita que iCloud se sincronice con la aplicación de correo de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización del Correo con iCloud.
- **Bloquear la copia de seguridad de Contactos en iCloud**: **Bloquear** impide que iCloud sincronice los contactos de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de los contactos mediante iCloud.
- **Bloquear la copia de seguridad de Calendario en iCloud**: **Bloquear** evita que iCloud se sincronice con la aplicación de calendario de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización del Calendario con iCloud.
- **Bloquear la copia de seguridad de Recordatorios de iCloud**: **Bloquear** evita que iCloud se sincronice con la aplicación de recordatorios de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de los Recordatorios con iCloud.
- **Bloquear la copia de seguridad de los marcadores en iCloud**: **Bloquear** impide que iCloud sincronice los Marcadores de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de los Marcadores con iCloud.
- **Bloquear la copia de seguridad de Notas de iCloud**: **Bloquear** impide que iCloud sincronice las Notas de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de Notas con iCloud.
- **Bloquear la Fototeca de iCloud**: **Bloquear** deshabilita la Fototeca de iCloud e impide que iCloud sincronice las fotos de los dispositivos. Las fotos que no se hayan descargado de la Fototeca de iCloud se quitarán del almacenamiento local de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de fotos entre el dispositivo y la Fototeca de iCloud.
- **Handoff**: esta característica permite que los usuarios comiencen a trabajar en un dispositivo macOS y, luego, seguir con el trabajo iniciado en otro dispositivo iOS/iPadOS o macOS. **Bloquear** impide la característica Handoff en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica en los dispositivos.

  Esta característica se aplica a:  
  - macOS 10.15 y versiones más recientes

## <a name="domains"></a>Dominios

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos e inscripción de dispositivos automatizada

- **URL de dominio de correo electrónico**: **agregue** una o más direcciones URL a la lista. Cuando los usuarios reciben un correo electrónico de un dominio distinto del que ha configurado, este se marca como correo electrónico de no confianza en la aplicación Mail de macOS.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede restringir la configuración y las características de dispositivos en dispositivos [iOS/iPadOS](device-restrictions-ios.md).
