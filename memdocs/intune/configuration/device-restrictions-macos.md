---
title: Configuración de dispositivo macOS en Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Agregue, configure o cree valores en dispositivos macOS para restringir características, lo que incluye establecer requisitos de contraseña, controlar la pantalla de bloqueo, usar aplicaciones integradas, agregar aplicaciones restringidas o aprobadas, controlar dispositivos Bluetooth, conectarse a la nube para realizar copias de seguridad y almacenar, habilitar la pantalla completa, agregar dominios y controlar la manera en que los usuarios interactúan con el explorador web Safari en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4f4ef6bab42f2f1b97c32a422d92247a3e564f7
ms.sourcegitcommit: a198e4efa52b16f87049853b9d8c9854fd9fa057
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "84680411"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Configuración de dispositivos macOS para permitir o restringir características mediante Intune

En este artículo se enumeran y describen los diferentes valores de configuración que se pueden controlar en los dispositivos macOS. Como parte de la solución de administración de dispositivos móviles (MDM), use estos valores para habilitar o deshabilitar características, establecer reglas de contraseña, permitir o restringir determinadas aplicaciones, etc.

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos macOS.

> [!NOTE]
> Es posible que la interfaz de usuario no coincida con los tipos de inscripción de este artículo, pero la información de este artículo es correcta. La interfaz de usuario se está actualizando en una próxima versión.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de restricciones de dispositivos macOS](device-restrictions-configure.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción. Para más información sobre los diferentes tipos de inscripción, consulte [Inscripción en macOS](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>Aplicaciones integradas

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Bloquear Autorrelleno en Safari**: **Sí** deshabilita la característica Autorrellenar de Safari en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración de Autorrellenar del explorador web.
- **Bloquear el uso de la cámara**: **Sí** impide el acceso a la cámara en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara del dispositivo.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.
  
- **Bloquear Apple Music**: **Sí** revierte la aplicación Música al modo clásico y deshabilita el servicio Música. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de la aplicación Apple Music.
- **Bloquear las sugerencias de Spotlight**: **Sí** impide que Spotlight devuelva resultados de una búsqueda en Internet. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la búsqueda de Spotlight se conecte a Internet y proporcione resultados de la búsqueda.
- **Bloquear la transferencia de archivos con Finder o iTunes**: **Sí** deshabilita los servicios de uso compartido de archivos de aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir los servicios de uso compartido de archivos de la aplicación.

  Esta característica se aplica a:  
  - macOS 10.13 y versiones más recientes

## <a name="cloud-and-storage"></a>Nube y almacenamiento

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Bloquear la sincronización de Keychain en iCloud**: **Sí** deshabilita la sincronización de las credenciales almacenadas en Keychain en iCloud. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios sincronicen estas credenciales.
- **Bloquear la sincronización de Documentos y Escritorio en iCloud**: **Sí** impide que iCloud sincronice documentos y datos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de clave-valor y documentos en el espacio de almacenamiento de iCloud.
- **Bloquear la copia de seguridad de iCloud Mail**: **Sí** impide que iCloud se sincronice con la aplicación de correo de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización del Correo con iCloud.
- **Bloquear la copia de seguridad de Contactos en iCloud**: **Sí** impide que iCloud sincronice los contactos de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de los contactos mediante iCloud.
- **Bloquear la copia de seguridad de Calendario en iCloud**: **Sí** impide que iCloud se sincronice con la aplicación de calendario de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización del Calendario con iCloud.
- **Bloquear la copia de seguridad de Recordatorios de iCloud**: **Sí** impide que iCloud se sincronice con la aplicación de recordatorios de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de los Recordatorios con iCloud.
- **Bloquear la copia de seguridad de los marcadores en iCloud**: **Sí** impide que iCloud sincronice los marcadores de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de los Marcadores con iCloud.
- **Bloquear la copia de seguridad de Notas de iCloud**: **Sí** impide que iCloud sincronice las notas de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de Notas con iCloud.
- **Bloquear la copia de seguridad de Fotos de iCloud**: **Sí** deshabilita la Fototeca de iCloud e impide que iCloud sincronice las fotos de los dispositivos. Las fotos que no se hayan descargado de la Fototeca de iCloud se quitarán del almacenamiento local de los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la sincronización de fotos entre el dispositivo y la Fototeca de iCloud.
- **Bloquear Handoff**: esta característica permite que los usuarios comiencen a trabajar en un dispositivo macOS y, luego, seguir con el trabajo iniciado en otro dispositivo iOS/iPadOS o macOS. **Sí** impide la característica Handoff en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica en los dispositivos.

  Esta característica se aplica a:  
  - macOS 10.15 y versiones más recientes

## <a name="connected-devices"></a>Dispositivos conectados

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Bloquear AirDrop**: **Sí** impide el uso de AirDrop en los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir usar la característica AirDrop para intercambiar contenido con dispositivos cercanos.
- **Impedir el desbloqueo automático de Apple Watch**: **Sí** impide que los usuarios desbloqueen el dispositivo macOS con el Apple Watch. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios desbloquear su dispositivo macOS con su Apple Watch.

## <a name="domains"></a>Dominios

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Dominios de correo electrónico sin marcar**: especifique una **Dirección URL de dominio de correo electrónico** (o varias) en la lista. Cuando los usuarios reciben o envían un correo electrónico de un dominio distinto a los agregados, se marca como correo electrónico no de confianza en la aplicación de correo de macOS.

## <a name="general"></a>General

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Block Lookup** (Bloquear búsqueda): **Sí** impide que el usuario resalte una palabra y luego busque su definición en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la característica de búsqueda de definiciones.
- **Bloquear Dictado**: **Sí** impide que los usuarios usen la entrada de voz para escribir texto. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios usen la entrada de dictado.
- **Bloquear almacenamiento en caché de contenido**: **Sí** impide el almacenamiento en caché de contenido. El almacenamiento en caché de contenido almacena localmente en los dispositivos datos de aplicaciones, datos del explorador web, descargas y mucho más. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede habilitar el almacenamiento en caché de contenido.

  Para más información sobre el almacenamiento en caché de contenido en macOS, vea [Gestionar el almacenamiento en caché de contenido en el Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (abre otro sitio web).

  Esta característica se aplica a:  
  - macOS 10.13 y versiones más recientes

- **Aplazar las actualizaciones de software**: **Sí** permite retrasar la visualización de las actualizaciones en el dispositivo, entre 0 y 90 días. Esta configuración no controla cuándo se instalan las actualizaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las actualizaciones en los dispositivos a medida que Apple las publica. Por ejemplo, si Apple publica una actualización de macOS en una fecha concreta, dicha actualización naturalmente se mostrará en los dispositivos en torno a la fecha de publicación. Se permiten las actualizaciones de compilación de inicialización sin retraso.  

  - **Retrasar la visibilidad de las actualizaciones de software**: especifique un valor entre 0 y 90 días. Cuando el retraso expira, los usuarios reciben una notificación para actualizar a la versión más antigua del sistema operativo que estaba disponible cuando se desencadenó el retraso.

    Por ejemplo, si hay una actualización de macOS disponible **el 1 de enero** y **Retrasar la visibilidad** está establecido en **5 días**, la actualización no se muestra como una actualización disponible. Al **sexto día** después de la publicación, esta actualización estará disponible y los usuarios podrán instalarla.

    Esta característica se aplica a:  
    - macOS 10.13.4 y versiones más recientes

- **Bloquear capturas de pantalla y grabación de pantalla**: el dispositivo debe inscribirse en la Inscripción de dispositivo automatizada (DEP) de Apple. **Sí** impide que los usuarios guarden capturas de pantalla. También evita que la aplicación Classroom observe pantallas remotas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios realizar capturas de pantalla y hacer posible que la aplicación Classroom vea pantallas remotas.

  - **Deshabilitar AirPlay, Ver pantalla por aplicación Aula y pantalla compartida**: **Sí** bloquea AirPlay e impide el uso compartido de la pantalla con otros dispositivos. Además, impide que los profesores usen la aplicación Classroom para ver las pantallas de sus alumnos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los profesores vean las pantallas de sus alumnos.

    Para usar esta opción, establezca el valor **Bloquear capturas de pantalla y grabación de pantalla** en **No configurado** (se permiten capturas de pantallas).

  - **Permitir la aplicación Aula para usar AirPlay y Ver pantalla sin avisar**: **Sí** permite a los profesores ver las pantallas de sus alumnos aunque estos no estén de acuerdo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría requerir que los alumnos estén de acuerdo antes de que los profesores puedan ver las pantallas.

    Para usar esta opción, establezca el valor **Bloquear capturas de pantalla y grabación de pantalla** en **No configurado** (se permiten capturas de pantallas).

- **Requerir el permiso del profesor para salir de las clases no administradas de la aplicación Aula**: **Sí** obliga a los alumnos inscritos en un curso de Classroom no administrado a obtener la aprobación del profesor para abandonar el curso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los alumnos abandonen el curso siempre que así lo decidan.

- **Permitir a Aula bloquear el dispositivo sin preguntar**: **Sí** permite a los profesores bloquear el dispositivo o la aplicación de un alumno sin su aprobación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría requerir que los alumnos estén de acuerdo antes de que los profesores puedan bloquear el dispositivo o la aplicación.

- **Los alumnos pueden unirse automáticamente a la clase de Aula sin preguntar**: **Sí** permite a los alumnos unirse a una clase sin preguntar al profesor. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría requerir la aprobación del profesor para unirse a una clase.

## <a name="password"></a>Contraseña

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Requerir contraseña**: **Sí** obliga a que los usuarios escriban una contraseña para acceder a los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no requiera una contraseña. Tampoco obliga a ninguna restricción, como el bloqueo de contraseñas sencillas o la configuración de una longitud mínima.
  - **Tipo de contraseña requerida**: escriba el nivel de complejidad de la contraseña requerido que exija su organización. Cuando se deja en blanco, Intune no cambia ni actualiza esta configuración. Las opciones son:
    - **No configurado**: usa el valor predeterminado del dispositivo.
    - **Alfanumérica**: incluye letras mayúsculas, minúsculas y caracteres numéricos.
    - **Numérica**: la contraseña solo debe contener números, por ejemplo, 123456789.

    Esta característica se aplica a:  
    - macOS 10.10.3 y versiones más recientes

  - **Número de caracteres no alfanuméricos en la contraseña**: escriba el número de caracteres complejos que requiere la contraseña, entre 0 y 4. Un carácter complejo es un símbolo, por ejemplo, `?`. Cuando se deja en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
  - **Longitud mínima de la contraseña**: escriba la longitud mínima que debe tener la contraseña, entre 4 y 16 caracteres. Cuando se deja en blanco, Intune no cambia ni actualiza esta configuración.
  - **Bloquear contraseñas simples**: **Sí** impide el uso de contraseñas sencillas, como `0000` o `1234`. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo permita contraseñas sencillas.
  - **Máximo de minutos de inactividad hasta que se bloquea la pantalla**: escriba el tiempo durante el cual los dispositivos deben estar inactivos antes de que se bloquee automáticamente la pantalla. Por ejemplo, escriba `5` para bloquear los dispositivos tras estar 5 minutos inactivos. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
  - **Máximo de minutos tras bloqueo de pantalla antes de solicitar la contraseña**: escriba el tiempo durante el cual los dispositivos deben estar inactivos antes de que se solicite una contraseña para desbloquearlos. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
  - **Expiración de la contraseña (días)** : escriba el número de días, entre 1 y 65535, hasta que se deba cambiar la contraseña del dispositivo. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando la contraseña expire, se le solicitará a los usuarios que creen una nueva contraseña. Cuando el valor está en blanco o se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.
  - **Impedir la reutilización de contraseñas anteriores**: impida que los usuarios creen contraseñas usadas anteriormente. escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba 5 para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en ninguna de sus cuatro anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.

- **Impedir al usuario modificar el código de acceso**: **Sí** impide que se cambie, se agregue o se quite el código de acceso. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que se cambie, se agregue o se quite el código de acceso.

- **Bloquear Touch ID para desbloquear el dispositivo**: **Sí** impide el uso de huellas digitales para desbloquear los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios desbloqueen el dispositivo mediante una huella digital.

- **Impedir el relleno automático de contraseñas**: **Sí** impide el uso de la característica Autorrellenar contraseñas en macOS. Si elige **Sí**, tendrá también este impacto:

  - No se les pide a los usuarios que usen una contraseña guardada en Safari ni en ninguna aplicación.
  - Se deshabilitan las contraseñas seguras automáticas y no se sugieren contraseñas seguras a los usuarios.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas características.

- **Impedir las solicitudes de proximidad de contraseñas**: **Sí** impide que los dispositivos soliciten contraseñas de dispositivos cercanos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas solicitudes de contraseña.

- **Impedir el uso compartido de contraseñas**: **Sí** impide el uso compartido de contraseñas entre dispositivos mediante AirDrop. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo permita que estas contraseñas se compartan.

## <a name="privacy-preferences"></a>Preferencias de privacidad

En los dispositivos macOS, las aplicaciones y los procesos suelen solicitar a los usuarios que permitan o denieguen el acceso a algunas características del dispositivo, como la cámara, el micrófono, el calendario, la carpeta Documentos, etc. Esta configuración permite a los administradores aprobar o denegar previamente el acceso a estas características del dispositivo. Cuando configure estas opciones, administrará en nombre de los usuarios el consentimiento del acceso a los datos. La configuración que establezca invalidará las decisiones anteriores de los usuarios.

El objetivo de esta configuración consiste en reducir el número de mensajes que muestran las aplicaciones y los procesos.

Esta característica se aplica a:

- macOS 10.14 y versiones más recientes
- Algunos valores de configuración se aplican a macOS 10.15 y versiones más recientes.
- Esta configuración solo se aplica a los dispositivos que tienen el perfil de preferencias de privacidad instalado antes de actualizarse.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos aprobada por el usuario e inscripción de dispositivos automatizada

- **Aplicaciones y procesos**: **agregue** aplicaciones o procesos para configurar el acceso. Indique también:
  - **Nombre**: indique un nombre para la aplicación o el proceso. Por ejemplo, escriba `Microsoft Remote Desktop` o `Microsoft Office 365`.
  
  - **Tipo de identificador**: Las opciones son:
    - **Identificador de lote**: seleccione esta opción para las aplicaciones.
    - **Ruta de acceso**: seleccione esta opción para los archivos binarios no empaquetados, como un proceso o un ejecutable.

    Las herramientas auxiliares insertadas en una agrupación de aplicaciones heredan automáticamente los permisos de la agrupación de aplicaciones envolvente.

  - **Identificador**: escriba el identificador de la agrupación de aplicaciones o la ruta de acceso del archivo de instalación del proceso o ejecutable. Por ejemplo, escriba `com.contoso.appname`.

    Para obtener el identificador de la agrupación de aplicaciones, abra la aplicación Terminal y ejecute el comando `codesign`. Este comando identifica la firma del código. De este modo, puede obtener al mismo tiempo el identificador de la agrupación y la firma del código.

  - **Requisito de código**: escriba la firma de código para la aplicación o el proceso.

    Se crea una firma de código cuando una aplicación o un archivo binario están firmados con un certificado de desarrollador. Para encontrar la designación, ejecute el comando `codesign` manualmente en la aplicación Terminal: `codesign --display -r - /path/to/app/binary`. La firma del código es todo lo que aparece después de `=>`.

  - **Habilitar validación de código estática**: seleccione **Sí** para que la aplicación o el proceso validen estáticamente el requisito de código. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

    Habilite esta opción solo si el proceso invalida la firma de código dinámica. En caso contrario, use **No configurado**.  

  - **Bloquear la cámara**: **Sí** impide que la aplicación acceda a la cámara del sistema. No se puede permitir el acceso a la cámara. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

  - **Bloquear el micrófono**: **Sí** impide que la aplicación acceda al micrófono del sistema. No se puede permitir el acceso al micrófono. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

  - **Bloquear la grabación de pantalla**: **Sí** impide que la aplicación capture el contenido de la pantalla del sistema. No se puede permitir el acceso a la grabación de pantalla y a la captura de pantalla. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

    Requiere macOS 10.15 y versiones más recientes.

  - **Block input monitoring** (Bloquear supervisión de entrada): **Sí** impide que la aplicación use las API CoreGraphics y HID para escuchar los eventos CGEvents y HID de todos los procesos. **Sí** también impide que las aplicaciones y los procesos escuchen y recopilen datos de los dispositivos de entrada, como un mouse, un teclado o un trackpad. No se puede permitir el acceso a las API CoreGraphics y HID.

    Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración.

    Requiere macOS 10.15 y versiones más recientes.

  - **Reconocimiento de voz**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite a la aplicación acceder al reconocimiento de voz del sistema y enviar datos de voz a Apple.
    - **Bloquear**: impide que la aplicación acceda al reconocimiento de voz del sistema y envíe datos de voz a Apple.

    Requiere macOS 10.15 y versiones más recientes.

  - **Accesibilidad**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a la aplicación de accesibilidad del sistema. Esta aplicación incluye subtítulos (CC), activación de texto y control de voz.
    - **Bloquear**: impide que la aplicación acceda a la aplicación de accesibilidad del sistema.

  - **Contactos**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a la información de los contactos administrada por la aplicación de contactos del sistema.  
    - **Bloquear**: impide que la aplicación acceda a esta información de los contactos.

  - **Calendario**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a la información del calendario administrada por la aplicación de calendario del sistema.
    - **Bloquear**: impide que la aplicación acceda a esta información del calendario.

  - **Recordatorios**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a la información de los recordatorios administrada por la aplicación de recordatorios del sistema.
    - **Bloquear**: impide que la aplicación acceda a esta información de los recordatorios.

  - **Fotos**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a las imágenes administradas por la aplicación de fotos del sistema en `~/Pictures/.photoslibrary`.
    - **Bloquear**: impide que la aplicación acceda a estas imágenes.

  - **Biblioteca multimedia**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a Apple Music, la actividad de música y vídeo y la biblioteca multimedia.  
    - **Bloquear**: impide que la aplicación acceda a este contenido multimedia.

    Requiere macOS 10.15 y versiones más recientes.

  - **Presencia del proveedor de archivos**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite a la aplicación acceder a la aplicación del proveedor de archivos y saber en qué momento los usuarios usan archivos administrados por el proveedor de archivos. Una aplicación de proveedor de archivos permite a otras aplicaciones de este tipo acceder a los documentos y los directorios que la aplicación contenedora almacena y administra.
    - **Bloquear**: impide que la aplicación acceda a la aplicación del proveedor de archivos.

    Requiere macOS 10.15 y versiones más recientes.

  - **Full disk access** (Acceso completo al disco): Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a todos los archivos protegidos, incluidos los archivos de administración del sistema. Aplique esta configuración con precaución.
    - **Bloquear**: impide que la aplicación acceda a estos archivos protegidos.

  - **Archivos de administración del sistema**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a algunos archivos que se usan en la administración del sistema.
    - **Bloquear**: impide que la aplicación acceda a estos archivos.

  - **Carpeta Escritorio**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a los archivos de la carpeta Escritorio del usuario.
    - **Bloquear**: impide que la aplicación acceda a estos archivos.

    Requiere macOS 10.15 y versiones más recientes.

  - **Carpeta Documentos**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a los archivos de la carpeta Documentos del usuario.
    - **Bloquear**: impide que la aplicación acceda a estos archivos.

    Requiere macOS 10.15 y versiones más recientes.

  - **Carpeta Descargas**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a los archivos de la carpeta Descargas del usuario.
    - **Bloquear**: impide que la aplicación acceda a estos archivos.

    Requiere macOS 10.15 y versiones más recientes.

  - **Network volumes** (Volúmenes de red): Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a archivos de volúmenes de red.
    - **Bloquear**: impide que la aplicación acceda a estos archivos.

    Requiere macOS 10.15 y versiones más recientes.

  - **Removable volumes** (Volúmenes extraíbles): Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación acceda a archivos de volúmenes extraíbles, como un disco duro.
    - **Bloquear**: impide que la aplicación acceda a estos archivos.

    Requiere macOS 10.15 y versiones más recientes.

  - **Eventos del sistema**: Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración.
    - **Permitir**: permite que la aplicación use las API CoreGraphics para enviar eventos CGEvents al flujo de eventos del sistema.
    - **Bloquear**: impide que la aplicación use las API CoreGraphics para enviar eventos CGEvents al flujo de eventos del sistema.

  - **Eventos de Apple**: esta opción permite que las aplicaciones envíen un evento de Apple restringido a otra aplicación o proceso. Seleccione **Agregar** para incluir una aplicación o proceso receptor. Especifique la siguiente información de la aplicación o proceso receptor:

    - **Tipo de identificador**: seleccione **Id. de agrupación** si el identificador receptor es una aplicación. Seleccione **Ruta de acceso** si el identificador receptor es un proceso o ejecutable.
    
    - **Identificador**: escriba el identificador de la agrupación de aplicaciones o la ruta de acceso de instalación del proceso que recibe el evento de Apple.  

    - **Requisito de código**: escriba la firma de código para la aplicación o el proceso receptor.

      Se crea una firma de código cuando una aplicación o un archivo binario están firmados con un certificado de desarrollador. Para encontrar la designación, ejecute el comando `codesign` manualmente en la aplicación Terminal: `codesign --display -r -/path/to/app/binary`. La firma del código es todo lo que aparece después de `=>`.

    - **Acceso**: permite que se envíe un evento de Apple macOS a la aplicación o proceso receptor. Las opciones son:
      - **No configurado**: Intune no cambia ni actualiza esta configuración.
      - **Permitir**: permite que la aplicación o el proceso envíen el evento de Apple restringido a la aplicación o proceso receptor.
      - **Bloquear**: impide que la aplicación o el proceso envíen un evento de Apple restringido a la aplicación o proceso receptor.

  - Guarde los cambios mediante **Guardar**.

## <a name="restricted-apps"></a>Aplicaciones restringidas

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Tipo de lista de aplicaciones restringidas**: cree una lista de aplicaciones que los usuarios no pueden instalar ni usar. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, los usuarios podrían tener acceso a las aplicaciones que asigne y a las aplicaciones integradas.
  - **Aplicaciones aprobadas**: Enumerar las aplicaciones que los usuarios pueden instalar. Para mantener el cumplimiento, los usuarios no deben instalar otras aplicaciones. Las aplicaciones que se administran mediante Intune están permitidas automáticamente, incluido el Portal de empresa. No se impide a los usuarios que instalen una aplicación que no se encuentra en la lista aprobada, Pero si lo hacen, se notifica en Intune.
  - **Aplicaciones prohibidas**: enumere las aplicaciones (que no se administran mediante Intune) que los usuarios no pueden instalar ni ejecutar. No se evita que los usuarios instalen una aplicación prohibida. Si un usuario instala una aplicación de esta lista, se notifica en Intune.

- **Lista de aplicaciones**: **agregue** aplicaciones a la lista:
  - **Identificador de lote de aplicaciones**: escriba el [id. de agrupación](bundle-ids-built-in-ios-apps.md) de la aplicación. Puede agregar aplicaciones integradas y aplicaciones de línea de negocio. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).

    Para buscar la dirección URL de una aplicación, abra la tienda de aplicaciones de iTunes y busque la aplicación. Por ejemplo, busque `Microsoft Remote Desktop` o `Microsoft Word`. Seleccione la aplicación y copie la dirección URL. También puede usar iTunes para buscar la aplicación y luego usar la tarea **Copiar vínculo** para obtener la dirección URL de la aplicación.

  - **Nombre de la aplicación**: escriba un nombre descriptivo que ayude a identificar el identificador de lote. Por ejemplo, escriba `Intune Company Portal app`.
  - **Publicador**: escriba el editor de la aplicación.

- **Importe** un archivo .csv con detalles sobre la aplicación, incluida la dirección URL. Use el formato `<app bundle ID>, <app name>, <app publisher>`. O bien, use **Exportar** para crear una lista de las aplicaciones agregadas, en el mismo formato.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede restringir la configuración y las características de dispositivos en dispositivos [iOS/iPadOS](device-restrictions-ios.md).
