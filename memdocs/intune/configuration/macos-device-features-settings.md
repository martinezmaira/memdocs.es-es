---
title: 'Configuración de características de dispositivos macOS en Microsoft Intune: Azure | Microsoft Docs'
description: Consulte las opciones para configurar dispositivos macOS para AirPrint y personalizar la ventana de inicio de sesión para mostrar u ocultar los botones de encendido en Microsoft Intune. Consulte los pasos para obtener la dirección IP, la ruta de acceso y la configuración de puertos de un servidor de AirPrint en la red. Use esta configuración en un perfil de configuración de dispositivo para configurar dispositivos macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e70952b0d90222bd31a4e9df997d70e9d528ef24
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194205"
---
# <a name="macos-device-feature-settings-in-intune"></a>Configuración de características de dispositivos macOS en Intune

Intune incluye opciones integradas para personalizar las características de los dispositivos macOS. Por ejemplo, los administradores pueden agregar impresoras AirPrint, elegir cómo los usuarios inician sesión, configurar los controles de energía, usar la autenticación de inicio de sesión único, etc.

Use estas características para controlar los dispositivos macOS como parte de la solución de administración de dispositivos móviles (MDM).

En este artículo se enumeran estas opciones de configuración y se describe lo que hace cada una de ellas. También muestra los pasos para obtener la dirección IP, la ruta de acceso y el puerto de las impresoras AirPrint mediante la aplicación Terminal (emulador). Para más información sobre las características del dispositivo, vaya a [Agregar la configuración de características de dispositivos iOS o macOS en Intune](device-features-configure.md).

> [!NOTE]
> Es posible que la interfaz de usuario no coincida con los tipos de inscripción de este artículo, pero la información del artículo es correcta. La interfaz de usuario se actualizará en una próxima versión.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de características del dispositivo macOS](device-features-configure.md).

> [!NOTE]
> Esta configuración se aplica a diferentes tipos de inscripción, mientras que algunas opciones se aplican a todas las opciones de inscripción. Para más información sobre los diferentes tipos de inscripción, vea [Inscripción en macOS](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Destinos de AirPrint**: **Agregue** una o varias impresoras AirPrint en las que los usuarios puedan imprimir desde sus dispositivos. Indique también:
  - **Puerto** (iOS 11.0+, iPadOS 13.0+): escriba el puerto de escucha del destino de AirPrint. Si se deja esta propiedad en blanco, AirPrint usa el puerto predeterminado.
  - **Dirección IP**: escriba la dirección IPv4 o IPv6 de la impresora. Por ejemplo, escriba `10.0.0.1`. Si usa nombres de host para identificar las impresoras, puede obtener la dirección IP haciendo ping a la impresora en la aplicación Terminal. En la sección [Obtención de la dirección IP y la ruta de acceso](#get-the-ip-address-and-path) (en este artículo) se incluyen más detalles.
  - **Ruta de acceso**: escriba la ruta de acceso al recurso de la impresora. La ruta de acceso suele ser `ipp/print` para las impresoras de la red. En la sección [Obtención de la dirección IP y la ruta de acceso](#get-the-ip-address-and-path) (en este artículo) se incluyen más detalles.
  - **TLS** (iOS 11.0+, iPadOS 13.0+): Las opciones son:
    - **No** (valor predeterminado): No se aplica Seguridad de la capa de transporte (TLS) al conectarse a impresoras AirPrint.
    - **Sí**: Protege las conexiones AirPrint con Seguridad de la capa de transporte (TLS).

- **Importe** un archivo delimitado por comas (.csv) que incluya una lista de impresoras AirPrint. Además, después de agregar impresoras AirPrint en Intune, puede **Exportar** esta lista.

### <a name="get-the-ip-address-and-path"></a>Obtención de la dirección IP y la ruta de acceso

Para agregar servidores AirPrinter, necesita la dirección IP de la impresora, la ruta de acceso de recursos y el puerto. Los pasos siguientes muestran cómo obtener esta información.

1. En un equipo Mac conectado a la misma red local (subred) que las impresoras AirPrint, abra **Terminal** (en **/Aplicaciones/Utilidades**).
2. En la aplicación Terminal, escriba `ippfind` y seleccione Entrar.

    Anote la información de la impresora. Por ejemplo, puede devolver algo parecido a `ipp://myprinter.local.:631/ipp/port1`. La primera parte es el nombre de la impresora. La última parte (`ipp/port1`) es la ruta de acceso del recurso.

3. En Terminal, escriba `ping myprinter.local` y seleccione Entrar.

   Anote la dirección IP. Por ejemplo, puede devolver algo parecido a `PING myprinter.local (10.50.25.21)`.

4. Use los valores de dirección IP y de ruta de acceso del recurso. En este ejemplo, la dirección IP es `10.50.25.21` y la ruta de acceso del recurso es `/ipp/port1`.

## <a name="associated-domains"></a>Dominios asociados

En Intune, puede:

- Agregar muchas asociaciones de aplicación a dominio.
- Asociar muchos dominios a la misma aplicación.

Esta característica se aplica a:

- macOS 10.15 y versiones más recientes

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos aprobada por el usuario e inscripción de dispositivos automatizada

- **Dominios asociados**: **Agregue** una asociación entre su dominio y una aplicación. Esta característica comparte las credenciales de inicio de sesión entre una aplicación de Contoso y un sitio web de Contoso. Indique también:

  - **Id. de la aplicación**: escriba el identificador de la aplicación que se va a asociar a un sitio web. El identificador de la aplicación incluye el identificador del equipo y un identificador de paquete: `TeamID.BundleID`.

    El identificador del equipo es una cadena alfanumérica de diez caracteres (letras y números) que Apple genera para los desarrolladores de aplicaciones, como `ABCDE12345`. En el vínculo [Localizar su identificador de equipo](https://help.apple.com/developer-account/#/dev55c3c710c)  (abre el sitio web de Apple) hay más información.

    El identificador de paquete identifica la aplicación de forma única y, normalmente, tiene el formato de notación de nombre de dominio inversa. Por ejemplo, el identificador de paquete de Finder es `com.apple.finder`. Para buscar el identificador de paquete, use AppleScript en Terminal:

    `osascript -e 'id of app "ExampleApp"'`

  - **Dominio**: escriba el dominio del sitio web que se va a asociar a una aplicación. El dominio incluye un tipo de servicio y un nombre de host completo, como `webcredentials:www.contoso.com`.

    Puede hacer coincidir todos los subdominios de un dominio asociado escribiendo `*.` (un carácter comodín de asterisco y un punto) antes del principio del dominio. El punto es obligatorio. Los dominios exactos tienen una prioridad más alta que los dominios con caracteres comodín. Por lo tanto, los patrones de los dominios primarios coinciden *si* no se encuentra ninguna coincidencia en el subdominio completo.

    El tipo de servicio puede ser:

    - **authsrv**: Extensión de aplicación de inicio de sesión único
    - **applink**: vínculo universal
    - **webcredentials**: relleno automático de contraseñas

> [!TIP]
> Para solucionar problemas, en el dispositivo macOS, abra **Preferencias del Sistema** > **Perfiles**. Confirme que el perfil que ha creado está en la lista de perfiles del dispositivo. Si aparece en la lista, asegúrese de que la **configuración de dominios asociados** está en el perfil e incluye el id. de la aplicación y los dominios correctos.

## <a name="content-caching"></a>Almacenamiento en caché de contenido

El almacenamiento en caché de contenido guarda una copia local del contenido. Otros dispositivos de Apple pueden recuperar esta información sin necesidad de conectarse a Internet. Este almacenamiento en caché acelera las descargas al guardar las actualizaciones de software, las aplicaciones, las fotografías y otros contenidos la primera vez que se descargan. Como las aplicaciones se descargan una vez y se comparten en otros dispositivos, las escuelas y las organizaciones con muchos dispositivos ahorran ancho de banda.

> [!NOTE]
> Use solo un perfil para esta configuración. Si asigna varios perfiles con esta configuración, se produce un error.
>
> Para obtener más información sobre la supervisión del almacenamiento en caché de contenido, vea [Visualización de registros y estadísticas de almacenamiento en caché de contenido](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (abre el sitio web de Apple).

Esta característica se aplica a:

- macOS 10.13.4 y versiones más recientes

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

Para obtener más información sobre esta configuración, vea [Configuración de carga de almacenamiento en caché de contenido](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (abre el sitio web de Apple).

**Habilitar almacenamiento en caché de contenido**: **Sí** activa el almacenamiento en caché de contenido y los usuarios no pueden deshabilitarlo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede desactivarlo.

- **Tipos de contenidos almacenados en caché**: Las opciones son:
  - **Todo el contenido**: almacena en caché el contenido de iCloud y el contenido compartido.
  - **Solo contenido de usuario**: almacena en caché el contenido de iCloud del usuario, incluidas las fotos y los documentos.
  - **Solo contenido compartido**: almacena en caché las aplicaciones y las actualizaciones de software.

- **Tamaño de caché máximo**: escriba la cantidad máxima de espacio en disco (en bytes) que se usa para almacenar en caché el contenido. Cuando se deja en blanco (el valor predeterminado), Intune no lo cambia ni actualiza. De forma predeterminada, el sistema operativo puede establecer este valor en cero (`0`) bytes, lo que proporciona espacio en disco ilimitado a la caché.

  Asegúrese de que no supere el espacio disponible en los dispositivos. Para obtener más información sobre la capacidad de almacenamiento del dispositivo, vea [Cómo se indica la capacidad de almacenamiento en iOS y macOS](https://support.apple.com/HT201402) (abre el sitio web de Apple).

- **Ubicación de la caché**: escriba la ruta de acceso para almacenar el contenido en caché. La ubicación predeterminada es `/Library/Application Support/Apple/AssetCache/Data`. Se recomienda no cambiar esta ubicación.

  Si cambia este valor, el contenido en caché no se mueve a la nueva ubicación. Para moverlo de forma automática, los usuarios deben cambiar la ubicación en el dispositivo (**Preferencias del sistema** > **Uso compartido** > **Almacenamiento en caché del contenido**).

- **Puerto**: escriba el número de puerto TCP en los dispositivos para que la caché acepte las solicitudes de descarga y carga, desde 0-65535. Escriba cero (`0`) (valor predeterminado) para usar cualquier puerto que esté disponible.
- **Bloquear conexión a Internet y uso compartido de contenido de caché**: también se conoce como almacenamiento en caché anclado a red. **Sí** impide el uso compartido de la conexión a Internet, además del uso compartido de contenido almacenado en caché con dispositivos iOS/iPadOS conectados mediante USB al equipo Mac. Los usuarios no pueden habilitar esta característica. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

- **Habilitar conexión compartida a Internet**: también se conoce como almacenamiento en caché anclado a red. **Sí** permite el uso compartido de la conexión a Internet, además del uso compartido de contenido almacenado en caché con dispositivos iOS/iPadOS conectados mediante USB al equipo Mac. Los usuarios no pueden deshabilitar esta característica. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría desactivarlo.

  Esta característica se aplica a:

  - macOS 10.15.4 y versiones más recientes

- **Habilitar caché para registrar detalles de clientes**: **Sí** registra la dirección IP y el número de puerto de los dispositivos que solicitan contenido. Si va a solucionar problemas del dispositivo, este archivo de registro puede ayudar. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no registre esta información.

- **Mantener siempre el contenido de la caché, incluso cuando el sistema necesite espacio en disco para otras aplicaciones**: **Sí** mantiene el contenido en la caché y se asegura de que no se elimine nada, incluso cuando el espacio en disco es bajo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría purgar automáticamente el contenido de la memoria caché cuando necesita espacio de almacenamiento para otras aplicaciones.

  Esta característica se aplica a:

  - macOS 10.15 y versiones más recientes

- **Mostrar alertas de estado**: **Sí** muestra las alertas como notificaciones del sistema. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo no muestre estas alertas como notificaciones del sistema.

  Esta característica se aplica a:

  - macOS 10.15 y versiones más recientes

- **Impedir que el dispositivo entre en reposo mientras el almacenamiento en caché está activado**: **Sí** impide que el equipo entre en suspensión cuando el almacenamiento en caché está activado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo permita que el dispositivo entre en reposo.

  Esta característica se aplica a:

  - macOS 10.15 y versiones más recientes

- **Dispositivos para almacenar en caché**: elija los dispositivos que pueden almacenar contenido en caché. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. 
  - **Los dispositivos que usan la misma red local**: la caché de contenido ofrece contenido a los dispositivos de la misma red local inmediata. No se ofrece contenido a los dispositivos de otras redes, incluidos aquellos a los que puede acceder la caché de contenido.
  - **Los dispositivos que usan la misma dirección IP pública**: la caché de contenido ofrece contenido a los dispositivos que usan la misma dirección IP pública. No se ofrece contenido a los dispositivos de otras redes, incluidos aquellos a los que puede acceder la caché de contenido.
  - **Los dispositivos que usan redes locales personalizados**: la caché de contenido proporciona contenido a los dispositivos en los intervalos IP que especifique.
    - **Intervalos de escucha de clientes**: escriba el intervalo de direcciones IP que pueden recibir la caché de contenido.
  - **Los dispositivos que usan redes locales personalizados con reserva**: la caché de contenido proporciona contenido a los dispositivos en los intervalos de escucha, los intervalos de escucha del mismo nivel y las direcciones IP principales.
    - **Intervalos de escucha de clientes**: escriba el intervalo de direcciones IP que pueden recibir la caché de contenido.

- **Direcciones IP públicas personalizadas**: escriba un intervalo de direcciones IP públicas. Los servidores en la nube usan este intervalo para hacer coincidir los dispositivos cliente con las cachés.

- **Compartir el contenido con otras cachés**: cuando la red tiene más de una caché de contenido, las cachés de otros dispositivos se convierten automáticamente en elementos del mismo nivel. Estos dispositivos pueden consultar y compartir el software almacenado en caché. 

  Cuando un elemento solicitado no está disponible en una caché de contenido, comprueba los elementos del mismo nivel del elemento. Si el elemento está disponible, se descarga de la caché de contenido en el dispositivo del mismo nivel. Si sigue sin estar disponible, la caché de contenido descarga el elemento de:

  - Una dirección IP principal, si se ha configurado alguna.
  
    O bien,
    
  - Desde Apple a través de Internet.

  Cuando hay más de una caché de contenido disponible, los dispositivos seleccionan de forma automática la correcta. 

  Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Las cachés de contenido que usan las mismas redes locales**: la caché de contenido solo se empareja con otras de la misma red local inmediata.
  - **Las cachés de contenido que usan la misma dirección IP pública**: la caché de contenido solo se empareja con otras en la misma dirección IP pública.
  - **Las cachés de contenido que usan redes locales personalizadas**: la caché de contenido solo se empareja con otras en el intervalo de escucha de direcciones IP que escriba:

    - **Intervalos de escucha de pares**: escriba las direcciones IPv4 o IPv6 inicial y final para el intervalo. La caché de contenido solo responde a las solicitudes de caché del mismo nivel procedentes de cachés de contenido en los intervalos de direcciones IP que especifique.
    - **Intervalos de filtro de pares**: escriba las direcciones IPv4 o IPv6 inicial y final para el intervalo. La caché de contenido filtra su lista de elementos del mismo nivel con los intervalos de direcciones IP que especifique.

- **Direcciones IP principales**: escriba la dirección IP local de otra caché de contenido para agregarla como caché primaria. La caché carga y descarga contenido en estas cachés, en lugar de cargarlo o descargarlo directamente con Apple. Solo tiene que agregar una dirección IP principal una vez.
- **Política de selección de principal**: cuando haya muchas cachés primarias, seleccione cómo se elige la dirección IP principal. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Round robin**: use las direcciones IP principales en orden. Esta opción es adecuada para los escenarios de equilibrio de carga.
  - **Primera disponible**: use siempre la primera dirección IP disponible en la lista.
  - **Hash**: crea un valor hash para la parte de la ruta de acceso de la dirección URL solicitada. Esta opción garantiza que siempre se use la misma dirección IP principal para la misma dirección URL.
  - **Aleatorio**: se usa una dirección IP aleatoria de la lista. Esta opción es adecuada para los escenarios de equilibrio de carga.
  - **Nota adhesiva disponible**: use siempre la primera dirección IP de la lista. Si no está disponible, use la segunda dirección IP de la lista. Para continuar, use la segunda dirección IP hasta que no esté disponible, etc.

## <a name="login-items"></a>Elementos de inicio de sesión

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Agregue los archivos, carpetas y aplicaciones personalizadas que se iniciarán durante el inicio de sesión**: **agregue** la ruta de acceso de un archivo, una carpeta, una aplicación personalizada o una aplicación del sistema que se abra cuando los usuarios inicien sesión en los dispositivos. Indique también:

  - **Ruta de acceso del elemento**: Escriba la ruta de acceso al archivo, la carpeta o la aplicación. Las aplicaciones del sistema o las aplicaciones creadas o personalizadas para su organización suelen estar en la carpeta `Applications`, con una ruta de acceso similar a `/Applications/AppName.app`.

    Puede agregar muchos archivos, carpetas y aplicaciones. Por ejemplo, escriba:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Al agregar una aplicación, una carpeta o un archivo, asegúrese de escribir la ruta de acceso correcta. No todos los elementos se encuentran en la carpeta `Applications`. Si un usuario mueve un elemento de una ubicación a otra, la ruta de acceso cambia. Este elemento movido no se abrirá cuando el usuario inicie sesión.

  - **Ocultar**: elija entre mostrar u ocultar la aplicación. Las opciones son:
    - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo muestre los elementos en la lista de elementos de inicio de sesión de usuarios y grupos con la opción Ocultar desactivada.
    - **Sí**: Oculta la aplicación en la lista de elementos de inicio de sesión de usuarios y grupos.

## <a name="login-window"></a>Ventana de inicio de sesión

### <a name="settings-apply-to-all-enrollment-types"></a>Las opciones se aplican a: Todos los tipos de inscripción

- **Mostrar información adicional en la barra de menús**: cuando se selecciona el área de tiempo en la barra de menús, **Sí** muestra el nombre de host y la versión de macOS. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no mostrar esta información en la barra de menús.
- **Banner**: escriba un mensaje que se muestre en la pantalla de inicio de sesión de los dispositivos. Por ejemplo, escriba la información de su organización, un mensaje de bienvenida, información de objetos perdidos, etc.
- **Requerir los campos de texto de nombre de usuario y contraseña**: elija cómo inician sesión los usuarios en los dispositivos. **Sí** exige que los usuarios escriban un nombre de usuario y una contraseña. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede exigir que los usuarios seleccionen su nombre de usuario en una lista y luego escriban su contraseña.

  Indique también:

  - **Ocultar los usuarios locales**: **Sí** no muestra las cuentas de usuarios locales en la lista de usuarios, que puede incluir las cuentas de administrador y estándar. Se muestran únicamente las cuentas de usuario de red y del sistema. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las cuentas de usuarios locales en la lista de usuarios.
  - **Ocultar las cuentas móviles**: **Sí** no muestra las cuentas móviles en la lista de usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las cuentas móviles en la lista de usuarios. Algunas cuentas móviles pueden aparecer como usuarios de red.
  - **Mostrar los usuarios de red**: seleccione **Sí** para mostrar los usuarios de la red en la lista de usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no mostrar las cuentas de usuarios de red en la lista de usuarios.
  - **Ocultar los administradores del equipo**: **Sí** no muestra las cuentas de usuarios administradores en la lista de usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar las cuentas de usuarios administradores en la lista de usuarios.
  - **Mostrar otros usuarios**: seleccione **Sí** para mostrar los usuarios de **Otros...** en la lista de usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no mostrar otras cuentas de usuarios en la lista de usuarios.

- **Ocultar el botón de apagado**: **Sí** no muestra el botón de apagado en la pantalla de inicio de sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar el botón de apagado.
- **Ocultar el botón de reinicio**: **Sí** no muestra el botón de reinicio en la pantalla de inicio de sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar el botón de reinicio.
- **Ocultar el botón de suspensión**: **Sí** no muestra el botón de suspensión en la pantalla de inicio de sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar el botón de suspensión.
- **Deshabilitar inicio de sesión del usuario desde la consola**: **Sí** oculta la línea de comandos de macOS usada para iniciar sesión. En el caso de los usuarios típicos, establezca esta opción en **Sí**. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios avanzados iniciar sesión con la línea de comandos de macOS. Para entrar en modo de consola, los usuarios escriben `>console` en el campo de nombre de usuario de campo y deben autenticarse en la ventana de la consola.
- **Deshabilitar el apagado con la sesión iniciada**: **Sí** impide que los usuarios seleccionen la opción **Apagar** después de iniciar sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios seleccionen el elemento de menú **Apagar** en los dispositivos.
- **Deshabilitar el reinicio con la sesión iniciada**: **Sí**  impide que los usuarios seleccionen la opción **Reiniciar** después de iniciar sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios seleccionen el elemento de menú **Reiniciar** en los dispositivos.
- **Deshabilitar la desconexión con la sesión iniciada**: **Sí** impide que los usuarios seleccionen la opción **Desconectar** después de iniciar sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios seleccionen el elemento de menú **Desconectar** en los dispositivos.
- **Deshabilitar el cierre de sesión con la sesión iniciada** (macOS 10.13 y versiones posteriores): **Sí** impide que los usuarios seleccionen la opción **Cerrar sesión** después de iniciar sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios seleccionen el elemento de menú **Cerrar sesión** en los dispositivos.
- **Deshabilitar la pantalla de bloqueo con la sesión iniciada** (macOS 10.13 y versiones posteriores): **Sí** impide que los usuarios seleccionen la opción **Bloquear pantalla** después de iniciar sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios seleccionen el elemento de menú **Bloquear pantalla** en los dispositivos.

## <a name="single-sign-on-app-extension"></a>Extensión de aplicación de inicio de sesión único

Esta característica se aplica a:

- macOS 10.15 y versiones más recientes

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Las opciones se aplican a: Inscripción de dispositivos aprobada por el usuario e inscripción de dispositivos automatizada

- **Tipo de extensión de la aplicación de SSO**: elija el tipo de extensión de la aplicación de SSO. Las opciones son:

  - **No configurado**: no se usan las extensiones de la aplicación. Para deshabilitar una extensión de aplicación, cambie el tipo de extensión de la aplicación de SSO a **Sin configurar**.
  - **Microsoft Azure AD**: 

    > [!IMPORTANT]
    > Todavía se está desarrollando la extensión de SSO de Microsoft Azure AD. Aparece en la interfaz de usuario de Intune, pero no funciona según lo previsto. No use **Microsoft Azure AD** para el tipo de extensión de la aplicación de SSO.

    usa el complemento de Microsoft Enterprise Single Sign-On, que es una extensión de la aplicación de SSO de tipo redirección. Este complemento proporciona inicio de sesión único para las cuentas de Active Directory en todas las aplicaciones macOS compatibles con la característica [Enterprise Single Sign-On de Apple](https://developer.apple.com/documentation/authenticationservices). Use este tipo de extensión de la aplicación de SSO para habilitar el inicio de sesión único en las aplicaciones de Microsoft, las aplicaciones de la organización y los sitios web que se autentican mediante Azure AD.

    El complemento de SSO actúa como agente de autenticación avanzado que ofrece mejoras en la seguridad y la experiencia del usuario.

    > [!IMPORTANT]
    > Para lograr el inicio de sesión único con el tipo de extensión de aplicación de inicio de sesión único de Microsoft Azure AD, instale la aplicación del Portal de empresa para macOS en los dispositivos. La aplicación del Portal de empresa suministra el complemento Enterprise Single Sign-On de Microsoft a los dispositivos. La configuración de la extensión de aplicación de inicio de sesión único de MDM activa el complemento. Después de instalar la aplicación del Portal de empresa y el perfil de extensión de aplicación de inicio de sesión único en los dispositivos, los usuarios inician sesión con sus credenciales y crean una sesión en sus dispositivos. Esta sesión se usa en aplicaciones diferentes sin necesidad de que los usuarios se autentiquen de nuevo.
    >
    > Para más información sobre la aplicación del Portal de empresa, consulte [¿Qué ocurre si instala la aplicación de Portal de empresa e inscribe el dispositivo macOS en Intune?](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md). [Descargue](https://go.microsoft.com/fwlink/?linkid=853070) la aplicación del Portal de empresa.

  - **Redireccionamiento**: use una extensión de la aplicación de redireccionamiento genérica y personalizable para usar SSO con flujos de autenticación modernos. Asegúrese de que conoce la extensión y el identificador del equipo correspondiente a la extensión de la aplicación de su organización.
  - **Credenciales**: use una extensión de la aplicación de credenciales genérica y personalizable para realizar el inicio de sesión único con flujos de autenticación de desafío y respuesta. Asegúrese de que conoce el identificador de la extensión y del equipo correspondiente a la extensión de la aplicación de inicio de sesión único de su organización.  
  - **Kerberos**: use la extensión integrada de Kerberos de Apple, que se incluye en macOS Catalina 10.15 y versiones más recientes. Esta opción es una versión específica de Kerberos de la extensión de la aplicación de **Credenciales**.

  > [!TIP]
  > Con los tipos **Redireccionamiento** y **Credenciales**, se agregan sus propios valores de configuración para pasar a través de la extensión. Si utiliza **Credenciales**, considere la posibilidad de usar las opciones de configuración integradas proporcionadas por Apple en el tipo **Kerberos**.

- **Id. de extensión** (redireccionamiento y credenciales): escriba el identificador de lote que identifica la extensión de la aplicación de SSO, como `com.apple.ssoexample`.
- **Id. de equipo** (redireccionamiento y credenciales): escriba el identificador de equipo de la extensión de la aplicación de SSO. Un identificador de equipo es una cadena alfanumérica de 10 caracteres (números y letras) que Apple genera, como `ABCDE12345`. 

  En [Búsqueda del identificador de equipo](https://help.apple.com/developer-account/#/dev55c3c710c) (se abre el sitio web de Apple) puede encontrar más información.

- **Dominio** (credenciales y Kerberos): escriba el nombre del dominio de autenticación. El nombre de dominio debe escribirse en mayúsculas, por ejemplo, `CONTOSO.COM`. Normalmente, el nombre de dominio es el mismo que el nombre de dominio DNS, pero en mayúsculas.

- **Dominios** (credenciales y Kerberos): escriba los nombres de dominio o host de los sitios que pueden autenticarse mediante SSO. Por ejemplo, si el sitio web es `mysite.contoso.com`, `mysite` es el nombre de host y `contoso.com` es el nombre de dominio. Cuando los usuarios se conectan a cualquiera de estos sitios, la extensión de la aplicación controla el desafío de autenticación. Esta autenticación permite a los usuarios usar Face ID, Touch ID o el código PIN/código de acceso de Apple para iniciar sesión.

  - Todos los dominios de los perfiles de Intune de la extensión de la aplicación de inicio de sesión único deben ser exclusivos. No se puede repetir un dominio en ningún perfil de extensión de la aplicación de inicio de sesión, aunque se usen distintos tipos de extensiones de la aplicación de SSO.
  - Estos dominios no distinguen mayúsculas de minúsculas.

- **Direcciones URL** (solo redireccionamiento): escriba los prefijos de dirección URL de los proveedores de identidades en cuyo nombre la extensión de la aplicación de redireccionamiento usa el inicio de sesión único. Cuando se redirige a los usuarios a estas direcciones URL, la extensión de la aplicación de inicio de sesión único interviene y solicita el inicio de sesión único.

  - Todas las direcciones URL de los perfiles de extensión de la aplicación de inicio de sesión único de Intune deben ser únicas. No se puede repetir un dominio en ningún perfil de extensión de la aplicación de SSO, aunque se usen distintos tipos de extensiones de la aplicación de SSO.
  - Las direcciones URL deben comenzar por `http://` or `https://`.

- **Configuración adicional** (Microsoft Azure AD, redireccionamiento y credenciales): escriba datos adicionales específicos de la extensión para pasarlos a la extensión de la aplicación de SSO:
  - **Clave**: escriba el nombre del elemento que quiere agregar, como `user name`.
  - **Tipo**: escriba el tipo de datos. Las opciones son:

    - String
    - Booleano: en **Valor de configuración**, escriba `True` o `False`.
    - Entero: en **Valor de configuración**, escriba un número.

  - **Valor**: escriba los datos.
  
  - **Agregar**: seleccione esta opción para agregar las claves de configuración.

- **Uso de la cadena de claves** (solo Kerberos): elija **Bloquear** para impedir que las contraseñas se guarden y almacenen en la cadena de claves. Si está bloqueado, no se le pedirá a los usuarios que guarde la contraseña y tendrá que volver a escribirla cuando expire el vale de Kerberos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir guardar y almacenar las contraseñas en la cadena de claves. No se pedirá a los usuarios que vuelvan a escribir la contraseña cuando expire el vale.
- **Face ID, Touch ID o código de acceso** (solo Kerberos): **Requerir** obliga a los usuarios a usar su Face ID, Touch ID o código de acceso del dispositivo cuando se necesitan las credenciales para actualizar el vale de Kerberos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no exigir que los usuarios usen información biométrica o el código de acceso del dispositivo para actualizar el vale de Kerberos. Si **Uso de la cadena de claves** está bloqueado, no se aplica esta configuración.
- **Dominio predeterminado** (solo Kerberos): elija **Habilitar** para establecer el valor de **Dominio** que ha especificado como dominio predeterminado. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no establecer un dominio Kerberos predeterminado.

  > [!TIP]
  > - **Habilite** esta opción si va a configurar varias extensiones de la aplicación de SSO de Kerberos en su organización.
  > - **Habilite** esta opción si usa varios dominios. Establece el valor de **Dominio** que escribió como dominio predeterminado.
  > - Si solo tiene un dominio, déjelo como **No configurado** (valor predeterminado).

- **Detección automática** (solo Kerberos): cuando se establece en **Bloquear**, la extensión de Kerberos no usa automáticamente LDAP y DNS para determinar su nombre de sitio de Active Directory. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que la extensión busque automáticamente el nombre del sitio de Active Directory.
- **Cambios de contraseña** (solo Kerberos): **Bloquear** impide que los usuarios cambien las contraseñas que usan para iniciar sesión en los dominios que ha escrito. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir cambiar las contraseñas.  
- **Sincronización de contraseñas** (solo Kerberos): elija **Habilitar** para sincronizar las contraseñas locales de los usuarios con Azure AD. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría deshabilitar la sincronización de contraseñas en Azure AD. Use esta opción como alternativa o copia de seguridad en SSO. Esta configuración no funciona si los usuarios han iniciado sesión con una cuenta móvil de Apple.
- **Complejidad de contraseña de Windows Server Active Directory** (solo Kerberos): elija **Requerir** para exigir que las contraseñas de usuario cumplan los requisitos de complejidad de contraseñas de Active Directory. Para obtener más información, consulte [Las contraseñas deben cumplir los requisitos de complejidad](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no requerir que los usuarios cumplan los requisitos de contraseña de Active Directory.
- **Longitud mínima de contraseña** (solo Kerberos): escriba el número mínimo de caracteres que pueden formar las contraseñas de los usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no exigir una longitud de contraseña mínima en los usuarios.
- **Límite de reutilización de contraseñas** (solo Kerberos): escriba el número de contraseñas nuevas, de 1 a 24, que se usan hasta que se pueda reutilizar una contraseña anterior en el dominio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no aplicar un límite de reutilización de contraseñas.
- **Vigencia mínima de la contraseña** (solo Kerberos): escriba el número de días que se usa una contraseña en el dominio antes de que los usuarios puedan cambiarla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no exigir una vigencia mínima para las contraseñas antes de que se puedan cambiar.
- **Días hasta la notificación de expiración de la contraseña** (solo Kerberos): escriba el número de días antes de que una contraseña expire en que los usuarios recibirán una notificación en la que se les indicará que la contraseña va a expirar. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría usar `15` días.
- **Caducidad de la contraseña** (solo Kerberos): escriba el número de días antes de que se deba cambiar la contraseña del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría establecer que las contraseñas no expiren nunca.
- **Dirección URL de cambio de contraseña** (solo Kerberos): escriba la dirección URL que se abre cuando los usuarios inician un cambio de contraseña de Kerberos.
- **Nombre de la entidad de seguridad** (solo Kerberos): escriba el nombre de usuario de la entidad de seguridad de Kerberos. No es necesario incluir el nombre de dominio. Por ejemplo, en `user@contoso.com`, `user` es el nombre de la entidad de seguridad y `contoso.com` es el nombre de dominio.

  > [!TIP]
  > - También puede usar variables en el nombre de la entidad de seguridad mediante llaves `{{ }}`. Por ejemplo, para mostrar el nombre de usuario, escriba `Username: {{username}}`. 
  > - Sin embargo, tenga cuidado con la sustitución de variables porque estas no se validan en la interfaz de usuario y distinguen mayúsculas de minúsculas. Asegúrese de especificar la información correcta.
  
- **Código de sitio de Active Directory** (solo Kerberos): escriba el nombre del sitio de Active Directory que la extensión de Kerberos debe usar. Es posible que no necesite cambiar este valor, ya que la extensión de Kerberos puede encontrar automáticamente el código del sitio de Active Directory.
- **Nombre de la caché** (solo Kerberos): escriba el nombre de los servicios de seguridad genéricos (GSS) de la memoria caché de Kerberos. Lo más probable es que no tenga que establecer este valor.  
- **Mensaje de requisitos de contraseñas** (solo Kerberos): escriba una versión de texto de los requisitos de contraseña de su organización que se muestra a los usuarios. El mensaje se muestra si no necesita los requisitos de complejidad de la contraseña de Active Directory, o bien no escribe una longitud mínima de la contraseña.  
- **Modo de dispositivo compartido** (solo Microsoft Azure AD): Seleccione **Sí** si se va a implementar el complemento Microsoft Enterprise Single Sign-On en dispositivos macOS configurados para la característica de modo de dispositivo compartido de Azure AD. Los dispositivos en modo compartido permiten a muchos usuarios iniciar sesión de forma global y fuera de las aplicaciones que admiten el modo de dispositivo compartido. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración. 

  Cuando se establece en **Sí**, todas las cuentas de usuario existentes se borran de los dispositivos. Para evitar la pérdida de datos o impedir que se restablezca la configuración de fábrica, asegúrese de comprender cómo esta configuración cambia los dispositivos.

  Para más información sobre el modo de dispositivo compartido, consulte [Introducción al modo de dispositivo compartido](/azure/active-directory/develop/msal-shared-devices).

- **Identificadores de lote de aplicaciones** (Microsoft Azure AD, Kerberos): **agregue** los identificadores de lote de aplicaciones que deben usar el inicio de sesión único en los dispositivos. Estas aplicaciones obtienen acceso al vale de concesión de vales de Kerberos y al vale de autenticación. Las aplicaciones también autentican a los usuarios en los servicios a los que están autorizados a acceder.
- **Asignación de dominio** (solo Kerberos): **agregue** los sufijos DNS de dominio que se deben asignar al dominio. Use esta opción cuando los nombres DNS de los hosts no coincidan con el nombre de dominio. Lo más probable es que no tenga que crear esta asignación personalizada de dominio a dominio.
- **Certificado PKINIT** (solo Kerberos): **seleccione** el certificado de criptografía de clave pública de la autenticación inicial (PKINIT) que se puede usar en la autenticación Kerberos. Puede elegir entre los certificados [PKCS](../protect/certficates-pfx-configure.md) o [SCEP](../protect/certificates-scep-configure.md) que ha agregado en Intune. Para más información sobre los certificados, consulte [Uso de certificados para la autenticación en Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede configurar las características del dispositivo en [iOS/iPadOS](ios-device-features-settings.md).