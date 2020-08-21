---
title: Crear elementos de configuración para Windows
titleSuffix: Configuration Manager
description: Cree elementos de configuración para administrar la configuración de equipos con Windows 10 con la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26846066aa713d40fdacfe75810d43cafd1c3f04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693682"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Crear elementos de configuración para dispositivos Windows con MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use el elemento de configuración Configuration Manager **Windows 8.1 y Windows 10** para administrar la configuración de los dispositivos Windows que administra con la administración local de dispositivos móviles (MDM).

Para obtener más información general sobre la configuración de cumplimiento en Configuration Manager, consulte los siguientes artículos:

- [Introducción a la configuración de cumplimiento](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Planear y configurar la configuración de cumplimiento](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Crear un elemento de configuración

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** , expanda **configuración de cumplimiento**y, a continuación, seleccione el nodo **elementos de configuración** .

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear elemento de configuración**.

1. En el **General** página de la **Asistente para crear un elemento de configuración**, especifique la siguiente información:

    - **Nombre**: un nombre único para identificar este elemento de configuración.

    - **Descripción**: una descripción opcional para proporcionar más información sobre su uso.

    - En **configuración para dispositivos administrados *sin* el cliente de Configuration Manager**, seleccione **Windows 8.1 y Windows 10**.

    - **Categorías**: puede crear y asignar categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.

1. En la página **plataformas admitidas** del asistente, seleccione las plataformas de Windows específicas para evaluar este elemento de configuración.

1. En la página **configuración del dispositivo** , seleccione los grupos de configuración que desea configurar. Para obtener más información sobre la configuración disponible, vea [referencia de configuración](#bkmk_setref).

    > [!TIP]
    > Si el valor que desea no aparece en la lista, seleccione la opción para **configurar opciones adicionales que no están en los grupos de configuración predeterminados**. Esta opción agrega la página **configuración adicional** al asistente.

1. En cada página de configuración, configure las opciones necesarias. Cuando la configuración lo admita, también puede **corregir la configuración no compatible**. Si un dispositivo evalúa la configuración como no compatible con este elemento de configuración, corregirá la configuración para que sea compatible.

    Para cada grupo de configuración, también puede configurar la gravedad que notifica cuando la configuración no es compatible. Elija uno de los siguientes valores para la opción **gravedad de no compatibilidad para informes** :

    - **Ninguna**: los dispositivos que no sigan esta regla de cumplimiento no notificarán ninguna gravedad de error en los informes de Configuration Manager.

    - **Información**

    - **Warning (ADVERTENCIA)**

    - **Critical)** (Crítico)

    - **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **crítico** para informes de Configuration Manager. También registra el estado no compatible como un evento de Windows en el registro de eventos de la aplicación.

1. En la página **aplicabilidad de plataforma** del asistente, revise cualquier configuración que no sea compatible con las plataformas admitidas seleccionadas. Vuelva y quite esta configuración, cambie las plataformas de soporte técnico o continúe.

    > [!IMPORTANT]
    > Los dispositivos no evalúan el cumplimiento de la configuración no admitida.

1. Finalice el asistente.

Puede ver el nuevo elemento de configuración en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a> Referencia de configuración  

En las secciones siguientes se detallan los valores específicos disponibles en cada grupo. Configure estas opciones en la página **configuración del dispositivo** del **Asistente para crear elemento de configuración** para Windows 8.1 y los dispositivos de **Windows 10** administrados *sin* el cliente de Configuration Manager.

### <a name="password"></a>Contraseña

Esta configuración es solo para dispositivos que ejecutan Windows 10 y versiones posteriores.

- **Requerir configuración de contraseña en los dispositivos**: requerir una contraseña en los dispositivos compatibles.
- **Longitud mínima de la contraseña (caracteres)**: la longitud mínima de la contraseña.
- **Expiración de la contraseña en días**: el número de días antes de que el usuario deba cambiar la contraseña.
- **Número de contraseñas recordadas**: evita la reutilización de contraseñas usadas anteriormente.
- **Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**: si se produce un error en este número de intentos de inicio de sesión, MDM borra el dispositivo
- **Tiempo de inactividad antes de que se bloquee el dispositivo**: especifique la cantidad de tiempo que un dispositivo puede estar inactivo antes de que se bloquee. El dispositivo está inactivo cuando no hay datos proporcionados por el usuario.
- **Complejidad de la contraseña**: elija si puede especificar un PIN numérico como `1234` o si debe proporcionar una contraseña segura.
  - **Número de conjuntos de caracteres complejos necesarios en la contraseña**: Si la complejidad de la contraseña es **fuerte**, seleccione el número de tipos de caracteres que requiere la contraseña: letras mayúsculas, letras minúsculas, números o símbolos. De manera predeterminada, este valor es `2`.
- **Enviar NIP de recuperación de contraseña a Exchange Server**

### <a name="device"></a>Dispositivo

- **Captura de pantalla**: habilite esta opción para permitir que el usuario realice una captura de pantalla de la pantalla del dispositivo. (Solo Windows 10)
- **Envío de datos de diagnóstico**: habilite esta opción para permitir datos de diagnóstico de Windows para análisis. (Solo Windows 8.1)
- **Permitir el envío de datos de diagnóstico (Windows 10)**: establezca el nivel de datos de diagnóstico de Windows para análisis: deshabilitar, básico, mejorado o completo. (Solo Windows 10)
- **Geolocalización**: habilite esta opción para permitir que el dispositivo use la información de servicios de ubicación. (Solo Windows 10)
- **Copiar y pegar**: habilite esta opción para usar copiar y pegar para transferir datos entre aplicaciones. (Solo Windows 10)
- **Restablecimiento de fábrica**: habilite esta opción para permitir que el usuario restablezca la configuración inicial del dispositivo. (Solo Windows 10)
- **Bluetooth**: permite o prohíbe el uso de la funcionalidad de Bluetooth del dispositivo.
- **Modo reconocible de Bluetooth**: permite o prohíbe que otros dispositivos Bluetooth puedan detectar el dispositivo. (Solo Windows 10)
- **Anuncios de Bluetooth**: permite o prohíbe el uso de anuncios de Bluetooth. (Solo Windows 10)
- **Grabación de voz**: permite o prohíbe el uso de las características de grabación de voz del dispositivo. (Solo Windows 10)
- **Cortana**: permite o prohíbe el uso del asistente de voz de Cortana. (Solo Windows 10)
- **Notificaciones del centro de actividades**: habilita o deshabilita el panel de notificaciones en Windows 10. (Solo Windows 10)
- **Modificación de la configuración regional (solo escritorio)**: permite o prohíbe al usuario cambiar la configuración regional en el dispositivo.
- **Modificación de la configuración de energía y suspensión (solo escritorio)**: permite o prohíbe al usuario cambiar la configuración de energía y suspensión en el dispositivo.
- **Modificación de la configuración de idioma (solo escritorio)**: permite o prohíbe al usuario cambiar la configuración de idioma en el dispositivo.
- **Modificación de la hora del sistema**: permite o prohíbe al usuario cambiar la fecha y la hora del dispositivo.
- **Modificación del nombre del dispositivo**: permite o prohíbe al usuario cambiar el nombre del dispositivo.

### <a name="email-management"></a>Administración de correo electrónico

Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.  

- **Correo electrónico POP e IMAP**: permite o prohíbe las conexiones a las cuentas de correo electrónico que usan los estándares pop e IMAP.
- **Tiempo máximo de conservación de correo electrónico**: Cuánto tiempo se mantiene el correo electrónico antes de que el servidor lo elimine.
- **Formatos de mensaje permitidos**: especifique si los mensajes de correo electrónico son **texto sin formato** o **HTML y texto sin formato**.
- **Tamaño máximo para correo electrónico de texto sin formato (descargado automáticamente)**: establezca el tamaño máximo de los correos electrónicos de texto sin formato cuando se descargan automáticamente.
- **Tamaño máximo del correo electrónico HTML (descargado automáticamente)**: establezca el tamaño máximo de los correos electrónicos HTML cuando se descarguen automáticamente.
- **Tamaño máximo de datos adjuntos (descargados automáticamente)**: establece el tamaño máximo de los datos adjuntos de correo electrónico que se descargan automáticamente.
- **Sincronización de calendario**: permite o prohíbe la sincronización de calendarios con el dispositivo.
- **Cuenta de correo electrónico personalizada**: permite o prohíbe el uso de una cuenta de correo electrónico no organizativa en el dispositivo.
- **Hacer que la cuenta Microsoft sea opcional en la aplicación Windows Mail**: habilite esta opción para no requerir un cuenta de Microsoft en Windows Mail.

### <a name="store"></a>Tienda

Esta configuración es solo para dispositivos que ejecutan Windows 10 y versiones posteriores.

- **Tienda de aplicaciones**: permite o prohíbe el acceso al Microsoft Store en el dispositivo.
- **Escriba una contraseña para acceder al almacén de la aplicación**: habilite esta opción para requerir a los usuarios que escriban una contraseña para acceder a la aplicación Microsoft Store.
- **Compras desde la aplicación**: permite o prohíbe a los usuarios realizar compras desde la aplicación.
- **Inicio**de la aplicación de la tienda: deshabilite todas las aplicaciones que se instalaron previamente en el dispositivo o que se instalaron desde el Microsoft Store.
- **Actualización automática de aplicaciones desde la tienda**: permite o prohíbe que las aplicaciones instaladas desde el Microsoft Store se actualicen automáticamente.
- **Instalar aplicaciones en la unidad del sistema**: permitir o prohibir el dispositivo para instalar aplicaciones en la unidad del sistema, que suele ser la `C:` unidad.
- **Instalar datos de la aplicación en el volumen del sistema**: habilite esta opción para permitir que las aplicaciones almacenen datos en la unidad del sistema.
- **Usar solo el almacén privado**: requerir a los usuarios que descarguen aplicaciones de la tienda privada.
- **Game DVR**: deshabilitar la transmisión y la grabación de juegos de Windows

### <a name="browser"></a>Browser

Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.

- **Permitir explorador Web**: permite o prohíbe el uso del explorador Web en el dispositivo.
- **Autorrellenar**: permite o prohíbe cambiar la configuración de autocompletar en el explorador.
- **Active Scripting**: permite o prohíbe si el explorador puede ejecutar scripts, como scripts de ActiveX.
- **Complementos**: permite o prohíbe Agregar complementos a Internet Explorer.
- **Bloqueador de elementos emergentes**: permite o prohíbe el bloqueador de elementos emergentes del explorador.
- **Cookies**: permite guardar o prohibir las cookies en el dispositivo.
- **Advertencia de fraude**: permita o prohíba advertencias de posibles sitios web fraudulentos.

### <a name="internet-explorer"></a>Internet Explorer

Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.

- **Enviar siempre el encabezado no realizar seguimiento**: permite o prohíbe el envío de información de exploración a sitios de terceros.
- **Zona de seguridad de intranet**: permite o prohíbe la asignación de un nivel de seguridad a la zona de seguridad de la intranet.
- **Nivel de seguridad para zona de Internet**: establezca el nivel de seguridad de la zona de Internet: alto, medio-alto o medio.
- **Nivel de seguridad de la zona de intranet**: establezca el nivel de seguridad de la zona de intranet: alto, medio-alto, medio, medio-bajo o bajo.
- **Nivel de seguridad para la zona de sitios de confianza**: establezca el nivel de seguridad para la zona de sitios de confianza: alto, medio-alto, medio, medio-bajo o bajo.
- **Nivel de seguridad para zona de sitios restringidos**: establezca el nivel de seguridad para la zona de sitios restringidos: alto.
- **Espacios de nombres para la zona de intranet**: configurar sitios web para agregar o quitar de la zona de intranet.
- **Ir a sitio de intranet para la entrada de una sola palabra**: permitir o prohibir que Internet Explorer vaya automáticamente a un sitio de intranet si el usuario escribe un nombre de sitio válido sin un protocolo anterior, por ejemplo `https://` .
- **Opción de menú modo de empresa**: permite a los usuarios activar y desactivar el modo de empresa desde el menú **herramientas** de Internet Explorer.
  - **Ubicación del informe de registro (URL)**: cuando el modo de empresa está activo, especifique una dirección URL para registrar sitios web visitados.
- **Ubicación de la lista de sitios de modo de empresa (URL)**: cuando el modo de empresa está activo, especifique la lista de sitios web que lo usan.

### <a name="cloud"></a>Nube

Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.

- **Sincronización de configuración**: permite o prohíbe la configuración de la sincronización entre dispositivos.
- **Sincronización de credenciales**: permite o prohíbe que las credenciales se sincronicen entre dispositivos.
- **Cuenta Microsoft**: habilite esta opción para permitir el uso de un cuenta de Microsoft en el dispositivo.
- **Sincronización de la configuración a través de conexiones de uso medido**: permite o prohíbe la sincronización de la configuración cuando se mide la conexión de red.

### <a name="security"></a>Seguridad

- **Instalación de archivos sin firmar**: permite que los usuarios puedan instalar un archivo sin firmar. (Solo Windows 10)
- **Aplicaciones sin firmar**: permite o prohíbe la instalación de aplicaciones sin firmar. (Solo Windows 10)
- **Mensajería SMS y MMS**: permite o prohíbe los protocolos de mensajes de texto en el dispositivo. (Solo Windows 10)
- **Almacenamiento extraíble**: permite o prohíbe el uso de almacenamiento extraíble, como una tarjeta SD. (Solo Windows 10)
- **Cámara**: permite o prohíbe el uso de la cámara del dispositivo. (Solo Windows 10)
- **Transmisión de campos en proximidad (NFC)**: permita o prohíba la comunicación mediante NFC. (Solo Windows 10)
- **Modo antirrobo**: permite o prohíbe el uso del modo antirrobo de Windows 10. (Solo Windows 10)
- **Permitir conexión USB**: permite o prohíbe que otros dispositivos se conecten a este dispositivo mediante una conexión USB. (Solo Windows 10)
- **Perfil de VPN de Windows RT**: aprovisiona un perfil de VPN para dispositivos Windows RT (solo Windows 8.1)

### <a name="peak-synchronization"></a>Sincronización durante horas punta

Esta configuración es solo para dispositivos que ejecutan Windows 10 y versiones posteriores.

- **Especificar hora pico**: establezca la hora máxima y los días de la semana para la sincronización de dispositivos móviles.
- **Frecuencia de sincronización durante horas punta**: configure la frecuencia con la que se produce la sincronización durante las horas punta.
- **Frecuencia de sincronización fuera de horas punta**: configure la frecuencia con la que se produce la sincronización fuera de las horas punta.

### <a name="roaming"></a>Movilidad

- **Administración de dispositivos en itinerancia**: permite o prohíbe a Configuration Manager administrar el dispositivo cuando está en itinerancia. (Solo Windows 10)
- **Descarga de software en movilidad**: permite o prohíbe la descarga de aplicaciones y software en itinerancia. (Solo Windows 10)
- **Descarga de correo electrónico en itinerancia**: permita o prohíba las descargas de correo electrónico en movilidad. (Solo Windows 10)
- **Itinerancia de datos**: permite o prohíbe la itinerancia entre redes al obtener acceso a los datos.
- **VPN sobre Cellular**: permite o prohíbe que el dispositivo use una conexión VPN mientras está conectado a una red de telefonía móvil. (Solo Windows 10)
- **Itinerancia de VPN sobre móvil**: permite o prohíbe que el dispositivo use una conexión VPN mientras se mueve en una red de telefonía móvil. (Solo Windows 10)

### <a name="encryption"></a>Cifrado

- **Cifrado de tarjeta de almacenamiento**: establecido en para requerir que el usuario Cifre las tarjetas de almacenamiento usadas en el dispositivo. (Solo Windows 10)
- **Cifrado de archivos en el dispositivo**: establecido en para cifrar los archivos almacenados en el dispositivo.
- **Requerir firma de correo electrónico**: el usuario tiene que firmar digitalmente los correos electrónicos antes de enviarlos.
  - **Algoritmo de firma**: seleccione el algoritmo para firmar los mensajes de correo electrónico: predeterminado, Sha o MD5
- **Requerir cifrado de correo electrónico**: el usuario tiene que cifrar los correos electrónicos antes de enviarlos.
  - **Algoritmo de cifrado**: seleccione el algoritmo de cifrado de mensajes de correo electrónico: predeterminado, triple DES, des, RC2 128-bit, RC2 64-bit, RC2 40 bits

### <a name="wireless-communications"></a>Comunicaciones inalámbricas

Esta configuración es solo para dispositivos que ejecutan Windows 10 y versiones posteriores.

- **Conexión de red inalámbrica**: permite o prohíbe la funcionalidad de Wi-Fi del dispositivo.
- **Tethering Wi-Fi**: permite al usuario usar el dispositivo como zona activa móvil.
- **Descargar datos a Wi-Fi cuando sea posible**: permita que el dispositivo use la conexión Wi-Fi lo máximo posible.
- **Informes de zonas Wi-Fi**: permite que el dispositivo envíe información acerca de las conexiones Wi-Fi para ayudar al usuario a detectar conexiones cercanas.
- **Configuración de Wi-Fi manual**: permite al usuario configurar manualmente las conexiones inalámbricas.

#### <a name="configured-wireless-network-connections"></a>Conexiones de red inalámbrica configuradas

1. En la página **configurar las opciones de comunicación inalámbrica de dispositivo móvil** , seleccione **Agregar**.

1. En la ventana **conexión de red inalámbrica** , especifique la siguiente información sobre la conexión inalámbrica que se aprovisionará en dispositivos móviles:

    - **Nombre de red (SSID)**: escriba el nombre de la red Wi-Fi.
    - **Conexión de red**: elija **Internet** o **trabajo**.
    - **Autenticación**: elija el método de autenticación para la conexión inalámbrica:
        - **Abrir**
        - **Compartido**
        - **WAP**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Cifrado de datos**: elija el método de cifrado que usa esta conexión. Los valores disponibles cambian en función del método de **autenticación** que seleccione:
        - **Deshabilitada**
        - **WEP**
        - **TKIP**
        - **AES**
    - **Índice de clave**: cuando establezca el **cifrado de datos** en **WEP**, seleccione un índice de clave de **1** a **4**.
    - **Esta red se conecta a Internet**: proporcione la configuración de proxy para permitir que los dispositivos móviles de una red inalámbrica se conecten a Internet.
        - **Configuración del servidor proxy**: configure la configuración del **servidor** y el **Puerto** para los proxies **http**, **WAP**y **Sockets** .
    - **configuración de 802.1 x**:
        - **Habilitar el acceso de red de 802.1 x**: Proteja la conexión mediante la especificación de un tipo de EAP.
        - **Tipo de EAP**: elija uno de los siguientes protocolos de autenticación:
            - **PEAP**
            - **Tarjeta inteligente o certificado**

### <a name="certificates"></a>Certificados

Importar certificados para instalar en dispositivos móviles.

Seleccione **importar**y, a continuación, especifique los valores siguientes:

- **Archivo de certificado**: Busque y seleccione un archivo de certificado (**. cer**) para importar.
- **Almacén de destino**: elija uno o varios de los siguientes almacenes de certificados:
  - **Raíces**
  - **CA**
  - **Normal**
  - **Con privilegios**
  - **SPC**
  - **Peer**
- **Rol**: Si elige el almacén de certificados **SPC** (certificado de editor de software), elija el rol que se va a asociar al certificado:
  - **Operador móvil**
  - **Administrador**
  - **Usuario autenticado**
  - **Administrador de ti**
  - **Usuario sin autenticar**
  - **Servidor de aprovisionamiento de confianza**

### <a name="system-security"></a>Seguridad del sistema

- **Control de cuentas de usuario**: configure el comportamiento del control de cuentas de usuario de Windows en el dispositivo.
- **Firewall de red**: requiere que Windows habilite el firewall integrado. (Windows 8.1)
- **Actualizaciones**: configure el comportamiento de las actualizaciones de software de Windows. (Windows 8.1)
  - **Clasificación mínima de actualizaciones**: elija la clasificación mínima de las actualizaciones que se van a descargar e instalar: **ninguna**, **importante**o **recomendada**.
- **Actualizaciones (Windows 10)**: configure el comportamiento de las actualizaciones de software de Windows. (Solo Windows 10)
  - **Día de instalación**: elija el día programado en el que el dispositivo instala automáticamente las actualizaciones y los reinicios. (Solo Windows 10)
  - **Hora de instalación**: elija la hora programada en que el dispositivo instala automáticamente las actualizaciones y los reinicios. (Solo Windows 10)
- **SmartScreen**: habilita o deshabilita la pantalla inteligente de Windows.
- **Protección antivirus**: requiere que Windows tenga software antivirus.
- Las **firmas de protección antivirus están actualizadas**: requieren que los archivos de firma de antivirus estén actualizados.
- **Vista de notificación de pantalla de bloqueo**: habilite o deshabilite las notificaciones para que se muestren en la pantalla de bloqueo.
- **Características de versión preliminar**: configure si el dispositivo acepta la configuración y las características de la versión preliminar. (Solo Windows 10)
- **Instalación manual del certificado raíz**: habilite o deshabilite el usuario para instalar manualmente un certificado raíz, lo que habilita la confianza para cualquier certificado emitido por esa raíz. (Solo Windows 10)
- **Permitir anulación de la inscripción manual**: permite o prohíbe al usuario anular la inscripción del dispositivo de la administración local de dispositivos móviles con Configuration Manager.

### <a name="windows-server-work-folders"></a>Carpetas de trabajo de Windows Server

Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.

- **URL de carpetas de trabajo**: especifique la ubicación de una carpeta de trabajo de Windows Server a la que los usuarios pueden conectarse desde su dispositivo.

### <a name="allowed-and-blocked-apps-list"></a>Lista de aplicaciones permitidas y bloqueadas

Esta configuración es solo para los dispositivos que ejecutan Windows Phone, que Configuration Manager MDM local no admite. Para más información, consulte [¿Qué ha ocurrido con la MDM híbrida?](../understand/what-happened-to-hybrid.md)

### <a name="windows-10-team"></a>Windows 10 Team

Esta configuración es solo para dispositivos que ejecutan Windows 10 Team.

- **Permitir que la pantalla se active automáticamente cuando los sensores detecten a alguien en la habitación**: permitir o prohibir que el dispositivo se active automáticamente cuando su sensor detecte a alguien en la habitación.
- **Requerir PIN para la proyección inalámbrica**: habilita o deshabilita la posibilidad de escribir un PIN antes de que otro dispositivo pueda conectarse de forma inalámbrica para la proyección.
- **Ventana de mantenimiento**: habilite esta opción para configurar la ventana cuando las actualizaciones puedan instalar y reiniciar el dispositivo.
  - **Hora de inicio**: establezca la hora de inicio de la ventana de mantenimiento.
  - **Duración (horas)**: establezca la duración en horas de la ventana de mantenimiento.
- **Azure Operational Insights**: permita que [Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) recopile, almacene y analice datos de archivos de registro de dispositivos Windows 10 Team.
  - **Identificador de área de trabajo**: escriba un identificador de área de trabajo válido
  - **Clave de área de trabajo**: escriba la clave para el área de trabajo asociada
- **Proyección inalámbrica de miracast**: permite que los dispositivos habilitados para miracast se contengan en este dispositivo de Windows 10 Team.
  - **Canal de miracast**: Seleccione un canal de miracast para el contenido del proyecto.
- **Información de la reunión mostrada en la pantalla de bienvenida**: elija el tipo de información que el dispositivo muestra en el icono **reuniones** de la pantalla de **Inicio** de sesión:
  - **Mostrar solo el organizador y la hora**
  - **Mostrar el organizador, la hora y el asunto (asunto oculto para las reuniones privadas)**
- **URL de imagen de fondo de pantalla de bloqueo**: especifique una dirección URL para mostrar un fondo personalizado en la pantalla de **Inicio** de sesión de un dispositivo de Windows 10 Team. Inicie la dirección URL con `https://` y use el formato PNG.

### <a name="windows-information-protection"></a>Windows Information Protection  

Para obtener más información sobre cómo configurar la protección de datos de empresa con Configuration Manager, consulte [protección de los datos de la empresa mediante Windows Information Protection (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Heredado de Microsoft Edge

Esta configuración es solo para dispositivos que ejecutan Windows 10 y versiones posteriores.  

- **Permitir sugerencias de búsqueda en la barra de direcciones**: permita que el motor de búsqueda sugiera sitios a medida que escribe frases de búsqueda.
- **Permitir no realizar seguimiento**: informar de sitios web que no desea que realicen un seguimiento de su visita.
- **Habilitar SmartScreen**: Compruebe que los archivos descargados no contienen código malintencionado.
- **Permitir elementos emergentes**: Configure los elementos emergentes del explorador.
- **Permitir cookies**: configure el uso de cookies.
- **Permitir Autorrellenar**: permite que el explorador rellene automáticamente los formularios con información almacenada, como el nombre, la dirección y el teléfono.
- **Permitir administrador de contraseñas**: permite que el explorador almacene y administre las contraseñas de los sitios Web.
- **Herramientas de desarrollo**: permita o prohíba la característica herramientas de desarrollo de Edge.
- **Extensiones**: permite o prohíbe extensiones perimetrales.
- **Exploración de InPrivate**: permite o prohíbe la exploración de InPrivate, que no almacena el historial ni las cookies.
- **Dirección IP de localhost de WebRTC**: permite o prohíbe que la dirección IP de localhost del dispositivo se muestre cuando el usuario realiza llamadas telefónicas mediante el protocolo RTC Web.
- **Bloquear el acceso a about: flags**: permitir o prohibir que el usuario tenga acceso a la `about:flags` página, que contiene la configuración experimental y de desarrollador.
- **Invalidación de avisos de SmartScreen para archivos**: permite o prohíbe al usuario omitir las advertencias del Filtro SmartScreen sobre la descarga de archivos potencialmente malintencionados.
- **Invalidación de avisos de SmartScreen**: permite o prohíbe al usuario omitir las advertencias del Filtro SmartScreen sobre sitios Web potencialmente malintencionados.
- **Dirección URL de primera ejecución**: especifique un sitio web para que se muestre cuando un usuario abra Edge por primera vez.

### <a name="windows-defender-antivirus"></a>Antivirus de Windows Defender

Esta configuración es solo para dispositivos que ejecutan Windows 10 y versiones posteriores.

- **Permitir la supervisión en tiempo real**: habilite el examen en tiempo real de malware, spyware y otro software no deseado.
- **Permitir supervisión del comportamiento**: defender comprueba determinados patrones conocidos de actividad sospechosa en los dispositivos.
- **Habilitar sistema de inspección de red**: el sistema de inspección de red (NIS) ayuda a proteger los dispositivos contra las vulnerabilidades de seguridad basadas en red. Usa las firmas de vulnerabilidades conocidas de Microsoft Endpoint Protection Center para ayudar a detectar y bloquear el tráfico malintencionado.
- **Examinar todas las descargas**: defender examina todos los archivos que se descargan de Internet.
- **Permitir análisis de scripts**: defender examina los scripts que se usan en Internet Explorer.
- **Supervisar la actividad de archivos y programas**: defender supervisa la actividad de archivos y programas en los dispositivos.
  - **Archivos supervisados**: elija el tipo de archivos que se van a supervisar: todos, entrantes o salientes.
- **Días para realizar el seguimiento de malware resuelto**: defender continúa realizando el seguimiento de malware resuelto durante el número de días especificado. A continuación, puede comprobar manualmente los dispositivos afectados previamente. Si establece el número de días en 0, el malware permanece en la carpeta de cuarentena y no se quita automáticamente. El valor máximo es 90.
- **Permitir acceso a la interfaz**de usuario del cliente: controla si se va a ocultar la interfaz de usuario de defender de los usuarios. Cuando se cambia esta configuración, surte efecto la próxima vez que se reinicia el dispositivo.
- **Programar un examen del sistema**: elija un examen completo o rápido que se realice periódicamente el día y la hora que seleccione:
  - **Día programado**: elija el día programado en que defender ejecuta el examen.
  - **Hora programada**: elija la hora programada en que defender ejecuta el examen.
- **Programar un examen rápido diario**: elija la hora programada en que defender ejecuta un examen rápido cada día.
- **Limitar el uso de CPU durante un examen**: establezca el porcentaje del procesador que defender puede usar al ejecutar un examen. Escriba un valor entre 1 y 100.
- **Examinar archivos de almacenamiento**: defender examina los archivos comprimidos, como archivos. zip o. cab.
- **Examinar mensajes de correo electrónico**: defender examina los mensajes de correo electrónico cuando llegan al dispositivo.
- **Examinar unidades extraíbles**: defender examina unidades extraíbles, como sticks USB.
- **Examinar unidades asignadas**: defender examina las unidades asignadas a recursos compartidos de red. Por ejemplo, `H:` se asigna a la unidad personal de un usuario. Si los archivos de la unidad son de solo lectura, defender no puede quitar ningún malware que encuentre allí.
- **Examinar archivos abiertos desde carpetas compartidas de red**: defender examina los archivos cuando un usuario los abre desde una ruta de acceso de red compartida. Por ejemplo, `\\server\share\file.doc`. Si el archivo del recurso compartido es de solo lectura, defender no puede quitar ningún malware que encuentre.
- **Intervalo de actualización de firma**: elija el intervalo de tiempo en el que defender comprueba si hay nuevos archivos de firma.
- **Permitir protección**en la nube: defender usa Microsoft Cloud para recibir información acerca de la actividad de malware y habilitar características como bloque en la primera vista.
- **Solicitar a los usuarios el envío de muestras**: elija el comportamiento de defender cuando los archivos puedan requerir un análisis más exhaustivo. Por ejemplo, defender puede enviar archivos automáticamente a Microsoft para determinar si son malintencionados.
- **Detección de aplicaciones potencialmente no deseadas**: protege el dispositivo contra la ejecución de software clasificado por defender como potencialmente no deseado. Puede protegerse de estas aplicaciones en ejecución o usar el modo auditoría para informar cuando un usuario instala una aplicación potencialmente no deseada.
- **Exclusiones de archivos y carpetas**: agregue uno o varios archivos y carpetas a la lista de exclusiones.  Por ejemplo, `C:\Path` o `%ProgramFiles%\Path\filename.exe`. Defender no incluye estos archivos y carpetas en ningún examen en tiempo real ni programado.
- **Exclusiones de extensiones de archivo**: agregue una o más extensiones de archivo a la lista de exclusiones.  Por ejemplo, `java` o `exe`. Defender no incluye ningún archivo con estas extensiones en ningún examen en tiempo real ni programado.
- **Exclusiones de procesos**: agregue procesos específicos a la lista de exclusiones. Por ejemplo, `C:\path\myproc.exe`. Este tipo de exclusión solo admite las siguientes extensiones: `exe` , `com` o `scr` . Defender no incluye estos procesos en ningún examen en tiempo real ni programado.

### <a name="additional-settings"></a>Configuración adicional

En la página **configuración del dispositivo** del asistente, si selecciona la opción para **configurar opciones adicionales que no están en los grupos de configuración predeterminados**, use esta página de **configuración adicional** para configurar estas opciones. Seleccione **Agregar** y, a continuación, elija en la lista de configuraciones móviles disponibles. Elija **seleccionar** para modificar la configuración integrada o **crear configuración** para crear un valor de registro personalizado o un tipo de configuración de URI de OMA.

## <a name="next-steps"></a>Pasos siguientes

[Supervisión de la configuración de cumplimiento](../../compliance/deploy-use/monitor-compliance-settings.md)