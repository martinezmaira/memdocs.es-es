---
title: Seguridad y privacidad de los clientes
titleSuffix: Configuration Manager
description: Obtenga información sobre seguridad y privacidad para los clientes de Configuration Manager.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4922502b49ab2da9ce393fab809e4dc583fd962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694843"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Seguridad y privacidad para los clientes de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo, se describe información de privacidad y seguridad para los clientes de Configuration Manager. También se incluye información para los dispositivos móviles administrados con el [conector de Exchange Server](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a> Prácticas recomendadas de seguridad para clientes  

El sitio de Configuration Manager acepta datos de dispositivos que ejecuten el cliente de Configuration Manager. Este comportamiento introduce el riesgo de clientes que puedan atacar al sitio. Por ejemplo, podrían enviar un inventario con formato incorrecto o intentar sobrecargar los sistemas de sitio. Implemente el cliente de Configuration Manager únicamente en dispositivos fiables. Además, utilice las siguientes prácticas recomendadas de seguridad para proteger el sitio de dispositivos no autorizados o comprometidos:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Usar certificados de infraestructura de clave pública (PKI) para las comunicaciones de cliente con sistemas de sitio donde se ejecute IIS  

- Como una propiedad de sitio, configure **Configuración de sistema de sitio** para **HTTPS solamente**.  

- Instale clientes con la propiedad `UsePKICert` CCMSetup.  

- Utilice una lista de revocación de certificados (CRL) y asegúrese de que los clientes y los servidores de comunicación puedan acceder siempre a la misma.  

Los clientes de dispositivos móviles y algunos clientes basados en Internet necesitan estos certificados. Microsoft recomienda usar estos certificados para todas las conexiones de cliente en la intranet.  

Para obtener más información sobre los requisitos de certificados PKI y cómo se usan para proteger Configuration Manager, vea [Requisitos de certificados PKI](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Apruebe automáticamente los equipos cliente de dominios de confianza y compruebe y apruebe manualmente los demás equipos  

Si no puede usar la autenticación de PKI, la aprobación identifica un equipo en el que confía para que pueda administrarlo Configuration Manager. La jerarquía tiene las opciones siguientes para configurar la aprobación de cliente:  

- Manual
- Automático para equipos en dominios de confianza
- Automático para todos los equipos  

El método de aprobación más seguro es aprobar automáticamente los clientes que pertenezcan a dominios de confianza. Después, compruebe y apruebe de forma manual el resto de los equipos. No le recomendamos que apruebe automáticamente todos los clientes, excepto si tiene otros controles de acceso para impedir que los equipos que no sean de confianza puedan acceder a la red.  

Para obtener más información sobre cómo aprobar equipos de forma manual, vea [Administrar clientes desde el nodo de dispositivos](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>No use funciones de bloqueo para impedir que los clientes accedan a la jerarquía de Configuration Manager.  

La infraestructura de Configuration Manager rechaza los clientes bloqueados. Los clientes bloqueados no pueden comunicarse con los sistemas de sitio para descargar directivas, cargar datos de inventario o enviar mensajes de estado.

El bloqueo se diseñó para los escenarios siguientes:

- Para bloquear medios de arranque perdidos o en peligro al implementar un SO en clientes.
- Cuando todos los sistemas de sitio aceptan conexiones de cliente HTTPS.

Cuando los sistemas de sitio aceptan conexiones de cliente HTTP, no use el bloqueo para proteger la jerarquía de Configuration Manager ante equipos que no sean de confianza. En este escenario, un cliente bloqueado podría volver a unirse al sitio con un nuevo certificado autofirmado y un nuevo id. de hardware.

La revocación de certificado es la línea de defensa principal ante posibles certificados en peligro. Una lista de revocación de certificados (CRL) solo está disponible desde una infraestructura de clave pública (PKI) admitida. El bloqueo de clientes en Configuration Manager ofrece una segunda línea de defensa para proteger la jerarquía.  

Para obtener más información, vea [Determinar si bloquear clientes](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Usar los métodos de instalación de cliente más seguros que sean prácticos para su entorno  

- Para los equipos de dominio, los métodos de instalación de clientes con directiva de grupo y de instalación de clientes basada en actualizaciones de software son más seguros que la instalación de inserción de cliente.  

- Si aplica controles de acceso y controles de cambio, use métodos de instalación manual y creación de imágenes.  

- En la versión 1806 o posteriores, use la autenticación mutua de Kerberos con la instalación de inserción de cliente.  

De todos los métodos de instalación de cliente, la instalación de inserción de cliente es el menos seguro debido al gran número de dependencias que tiene. Entre estas dependencias, se incluyen los permisos administrativos locales, el recurso compartido Admin$ y las excepciones del firewall. El número y el tipo de estas dependencias hace que se incremente su superficie expuesta a ataques.  

A partir de la versión 1806, al usar la instalación de inserción de cliente, el sitio puede exigir la autenticación mutua de Kerberos si no permite revertir a NTLM antes de establecer la conexión. Esta mejora ayuda a proteger la comunicación entre el servidor y el cliente. Para obtener más información, vea [Cómo instalar clientes con inserción de cliente](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->  

Para obtener más información sobre los distintos tipos de instalación de clientes, vea [Métodos de instalación de cliente](client-installation-methods.md).  

Siempre que sea posible, seleccione un método de instalación de cliente que exija el número mínimo de permisos de seguridad en Configuration Manager. Restrinja los usuarios administrativos que tengan asignados roles de seguridad con permisos que puedan usarse para fines distintos de la implementación de clientes. Por ejemplo, para configurar la actualización de cliente automática, se necesita el rol de seguridad **Administrador total**, que concede a un usuario administrativo todos los permisos de seguridad.  

Para obtener más información sobre las dependencias y los permisos de seguridad necesarios para cada método de instalación de cliente, vea “Dependencias del método de instalación” en [Requisitos previos para clientes de equipos](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Si debe utilizar la instalación de inserción de cliente, tome medidas adicionales para proteger la cuenta de instalación de inserción de cliente  

Esta cuenta necesita ser miembro del grupo de **administradores** locales en cada equipo donde se instale el cliente de Configuration Manager. Nunca agregue la cuenta de instalación de inserción de cliente al grupo **Administradores del dominio**. En su lugar, cree un grupo global y, después, agréguelo al grupo de **administradores** locales en los clientes. Cree un objeto de directiva de grupo para agregar una configuración de grupo restringido y agregar la cuenta de instalación de inserción de cliente al grupo de **administradores** locales.  

Para mejorar la seguridad, cree varias cuentas de instalación de inserción de cliente, cada una con acceso de administrador a un número limitado de equipos. Si una cuenta pierde su carácter confidencial, solo estarán en peligro los equipos cliente a los que acceda esa cuenta.  

### <a name="remove-certificates-before-imaging-clients"></a>Quitar los certificados antes de crear imágenes de clientes  

Al implementar clientes con imágenes de SO, quite siempre los certificados antes de realizar la captura de la imagen. En estos certificados, se incluyen certificados PKI para la autenticación de cliente y certificados autofirmados. Si no quita estos certificados, los clientes podrían suplantarse entre sí. No se pueden verificar los datos de cada cliente.  

Para obtener más información, vea [Crear una secuencia de tareas para capturar un sistema operativo](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Comprobar que los clientes de equipos de Configuration Manager obtengan una copia autorizada de estos certificados  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>El certificado de clave raíz confiable de Configuration Manager  

Cuando las dos afirmaciones siguientes son verdaderas, los clientes usan la clave raíz confiable de Configuration Manager para autenticar puntos de administración válidos:  

- No ha extendido el esquema de Active Directory a Configuration Manager.
- Los clientes no usan certificados PKI cuando se comunican con puntos de administración.  

En este escenario, los clientes no pueden comprobar que el punto de administración es de confianza para la jerarquía, excepto si usan la clave raíz confiable. Sin la clave raíz confiable, un atacante experimentado podría dirigir los clientes a un punto de administración no autorizado.  

Cuando los clientes no pueden descargar la clave raíz confiable de Configuration Manager del catálogo global o mediante el uso de certificados PKI, aprovisione previamente los clientes con la clave raíz confiable. Esta acción garantiza que no se puedan dirigir a un punto de administración no autorizado. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>El certificado de firma de servidor de sitio  

Los clientes usan este certificado para verificar que el servidor del sitio firmó la directiva descargada desde un punto de administración. Este certificado está autofirmado por el servidor de sitio y publicado en Servicios de dominio de Active Directory.  

Cuando los clientes no pueden descargar el certificado de firma del servidor de sitio desde el catálogo global, de forma predeterminada lo descargarán desde el punto de administración. Si el punto de administración está expuesto a una red que no es de confianza (como Internet), instale de forma manual el certificado de firma del servidor de sitio en los clientes. Esta acción garantiza que no se puedan descargar directivas de cliente manipuladas desde un punto de administración en peligro.  

Para instalar manualmente el certificado de firma de servidor de sitio, utilice la propiedad de CCMSetup Client.msi **SMSSIGNCERT**. Para obtener más información, vea [Información sobre las propiedades de instalación de clientes](../about-client-installation-properties.md).  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>No usar la asignación automática de sitios si el cliente descarga la clave raíz confiable desde el primer punto de administración con el que establezca contacto  

Para evitar el riesgo de que un nuevo cliente descargue la clave raíz confiable desde un punto de administración no autorizado, use únicamente la asignación automática de sitios en los escenarios siguientes:  

- El cliente puede acceder a la información del sitio de Configuration Manager publicada en Active Directory Domain Services.  

- Se aprovisiona previamente el cliente con la clave raíz confiable.  

- Se utilizan certificados PKI de una entidad de certificación empresarial para establecer la confianza entre el cliente y el punto de administración.  

Para obtener más información sobre la clave raíz confiable, vea [Planear la clave raíz confiable](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Instale equipos cliente con la opción de CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS  

El método de ubicación de servicio más seguro para que los clientes encuentren los sitios y los puntos de administración consiste en utilizar Active Directory Domain Services. A veces, este método no puede aplicarse en algunos entornos. Por ejemplo, porque no se pueda extender el esquema de Active Directory para Configuration Manager, o bien porque los clientes se encuentren en un grupo de trabajo o bosque que no sea de confianza. Si este método no puede usarse, use la publicación en DNS como un método alternativo de ubicación del servicio. Si ambos métodos producen errores y el punto de administración no se configura para las conexiones de cliente HTTPS, los clientes pueden revertir al uso de WINS.  

Publicar en WINS es menos seguro que el resto de los métodos de publicación. Para configurar los equipos cliente de forma que no reviertan al uso de WINS, especifique **SMSDIRECTORYLOOKUP=NoWINS**. Si necesita usar WINS para la ubicación del servicio, use **SMSDIRECTORYLOOKUP=WINSSECURE**. Esta configuración es la predeterminada. Usa la clave raíz confiable de Configuration Manager para validar el certificado autofirmado del punto de administración.  

> [!NOTE]  
> Si configura el cliente para **SMSDIRECTORYLOOKUP=WINSSECURE** y encuentra un punto de administración desde WINS, el cliente comprobará su copia de la clave raíz confiable de Configuration Manager que se encuentra en WMI.  
>
> Si la firma del certificado de punto de administración coincide con la copia del cliente de la clave raíz confiable, el certificado se considerará válido. Después de validar el certificado, el cliente iniciará la comunicación con el punto de administración encontrado mediante el uso de WINS.  
>
> Si la firma del certificado de punto de administración no coincide con la copia del cliente de la clave raíz confiable, el certificado no se considerará válido. En este escenario, el cliente no se comunica con el punto de administración encontrado mediante el uso de WINS.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Asegúrese de que las ventanas de mantenimiento son lo suficientemente grandes como para implementar las actualizaciones de software imprescindibles  

Las ventanas de mantenimiento para las colecciones de dispositivos restringen los períodos en que Configuration Manager puede instalar software en estos dispositivos. Si configura una ventana de mantenimiento demasiado reducida, es posible que el cliente no pueda instalar actualizaciones de software críticas. Este comportamiento deja vulnerable al cliente ante cualquier ataque que mitigue la actualización de software.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Medidas de seguridad adicionales para reducir la superficie expuesta a ataques en dispositivos de Windows Embedded con filtros de escritura  

Al habilitar filtros de escritura en dispositivos de Windows Embedded, las instalaciones de software o los cambios solo se realizan en la superposición. Estos cambios no persisten después de reiniciar el dispositivo. Si usa Configuration Manager para deshabilitar los filtros de escritura, durante este período, el dispositivo incrustado será vulnerable a cambios en todos los volúmenes. Entre estos volúmenes, también se incluyen las carpetas compartidas.  

Configuration Manager bloquea el equipo durante este período para que solo puedan iniciar sesión los administradores locales. Siempre que sea posible, tome medidas de seguridad adicionales para proteger el equipo. Por ejemplo, habilite restricciones adicionales en el firewall.  

Si usa ventanas de mantenimiento para que persistan los cambios, planee estas ventanas cuidadosamente. Minimice el tiempo en que estarán deshabilitados los filtros de escritura, pero asegúrese de que sean lo suficientemente amplios para permitir que se completen las instalaciones de software y los reinicios.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Usar la versión del cliente más reciente con la instalación de cliente basada en actualizaciones de software

Si usa la instalación de cliente basada en actualizaciones de software e instala una versión posterior del cliente en el sitio, actualice la actualización de software publicada. Después, el cliente recibirá la versión más reciente desde el punto de actualización de software.  

Al actualizar el sitio, no se actualizará automáticamente la actualización de software para la implementación de cliente que se publique en el punto de actualización de software. Vuelva a publicar el cliente de Configuration Manager en el punto de actualización de software y actualice el número de versión.  

Para obtener más información, vea [Instalar clientes de Configuration Manager con la instalación basada en actualizaciones de software](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Solo suspender la indicación de PIN de BitLocker en dispositivos con acceso restringido y de confianza  

Solo establezca la opción de cliente **Suspender indicación de PIN de BitLocker en el reinicio** en **Siempre** en los equipos en los que confíe y que tengan restringido el acceso físico.

Al establecer esta opción de cliente en **Siempre**, Configuration Manager puede completar la instalación de software. Este comportamiento facilita la instalación de actualizaciones de software críticas y la reanudación de los servicios. Si un atacante intercepta el proceso de reinicio, podría tomar el control del equipo. Use esta opción solo cuando confíe en el equipo y cuando el acceso físico al equipo esté restringido. Por ejemplo, esta configuración podría ser adecuada para los servidores de un centro de datos.  

Para obtener más información sobre esta configuración de cliente, vea [Información sobre la configuración de clientes](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>No omitir la directiva de ejecución de PowerShell

Si establece la configuración del cliente de Configuration Manager **Directiva de ejecución de PowerShell** en **Omitir**, Windows permitirá que se ejecuten scripts de PowerShell no firmados. Este comportamiento podría permitir que se ejecutara malware en los equipos cliente. Cuando la organización exige esta opción, use una configuración de cliente personalizada. Asígnela solo a los equipos cliente donde sea necesario ejecutar scripts de PowerShell no firmados.  

Para obtener más información sobre esta configuración de cliente, vea [Información sobre la configuración de clientes](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a> Prácticas recomendadas de seguridad para dispositivos móviles  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Instale el punto de proxy de inscripción en una red perimetral y el punto de inscripción en la intranet  

Para los dispositivos móviles basados en Internet que inscriba con Configuration Manager, instale el punto de proxy de inscripción en una red perimetral y el punto de inscripción en la intranet. Esta separación de roles facilita la protección del punto de inscripción contra los ataques. Si un atacante pone en peligro el punto de inscripción, podría obtener los certificados para la autenticación. También podría robar las credenciales de los usuarios que hayan inscrito sus dispositivos móviles.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Configure la contraseña para facilitar la protección de los dispositivos móviles contra el acceso no autorizado  

*Para dispositivos móviles inscritos por Configuration Manager*: use un elemento de configuración de dispositivos móviles para configurar la complejidad de contraseñas como el PIN. Especifique al menos la longitud mínima de la contraseña predeterminada.  

*Para dispositivos móviles que no tienen instalado el cliente de Configuration Manager, pero que se administran mediante el conector de Exchange Server*: configure las **Opciones de contraseña** para el conector de Exchange Server, como que la complejidad de contraseñas sea el PIN. Especifique al menos la longitud mínima de la contraseña predeterminada.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Solo permitir la ejecución de aplicaciones firmadas por compañías en las que confíe  

Ayuda a impedir la manipulación de información de inventario e información de estado al permitir que las aplicaciones solo se ejecuten cuando estén firmadas por compañías en la se confíe. No permita que los dispositivos instalen archivos no firmados.  

*Para dispositivos móviles inscritos por Configuration Manager*: use un elemento de configuración de dispositivos móviles para establecer la opción de seguridad **Aplicaciones sin firmar** en **Prohibido**. Configure las **Instalaciones de archivos sin firmar** para que sean un origen de confianza.  

*Para dispositivos móviles que no tienen instalado el cliente de Configuration Manager, pero que se administran mediante el conector de Exchange Server*: en la **Configuración de la aplicación** del conector de Exchange Server, establezca **Instalación de archivos sin firmar** y **Aplicaciones sin firmar** como **Prohibido**.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Bloquear los dispositivos móviles cuando no estén en uso  

Ayuda a impedir los ataques de elevación de privilegios al bloquear el dispositivo móvil cuando no esté en uso.

*Para dispositivos móviles inscritos por Configuration Manager*: use un elemento de configuración de dispositivo móvil para configurar la opción de contraseña **Tiempo de inactividad en minutos antes de que se bloquee el dispositivo móvil**.  

*Para dispositivos móviles que no tienen instalado el cliente de Configuration Manager, pero que se administran mediante el conector de Exchange Server*: configure la **Configuración de contraseña** del conector de Exchange Server para establecer el **Tiempo de inactividad en minutos antes de que se bloquee el dispositivo móvil**.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Restringir los usuarios que pueden inscribir sus dispositivos móviles  

Contribuya a evitar ataques de elevación de privilegios mediante la restricción de los usuarios que pueden inscribir sus dispositivos móviles. Utilice una configuración de cliente personalizada en lugar de la configuración de cliente predeterminada para permitir sólo a los usuarios autorizados que inscriban sus dispositivos móviles.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Guía de afinidad entre usuario y dispositivo para dispositivos móviles  

No implemente aplicaciones a los usuarios que tengan dispositivos móviles inscritos por Configuration Manager o Microsoft Intune en los escenarios siguientes:  

- Más de una persona usa el dispositivo móvil.  

- Un administrador ha inscrito el dispositivo en nombre de un usuario.  

- El dispositivo se transfiere a otra persona sin retirarlo y, después, volver a inscribirlo.  

La inscripción de dispositivos crea una relación de afinidad entre usuario y dispositivo. Esta relación asigna el usuario que realiza la inscripción al dispositivo móvil. Si otro usuario usa el dispositivo móvil, podría ejecutar las aplicaciones implementadas para el usuario original, lo que podría causar una elevación de privilegios. De forma similar, si un administrador inscribe el dispositivo móvil para un usuario, las aplicaciones implementadas para el usuario no se instalarán en el dispositivo móvil. En su lugar, podrían instalarse las aplicaciones implementadas para el administrador.  

Al contrario que la afinidad entre usuario y dispositivo para equipos con Windows, no se puede definir de forma manual la información de afinidad entre usuario y dispositivo para los dispositivos móviles inscritos mediante Microsoft Intune.  

Si transfiere la propiedad de un dispositivo móvil inscrito por Intune, primero tendrá que retirar el dispositivo móvil de Intune. Esta acción quitará la relación de afinidad entre usuario y dispositivo. Después, pida al usuario actual que vuelva a inscribir el dispositivo.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Asegúrese de que los usuarios inscriban sus propios dispositivos móviles para Microsoft Intune.  

Durante la inscripción, se crea una relación de afinidad entre usuario y dispositivo. Esta acción asigna el usuario que realiza la inscripción al dispositivo móvil. Si un administrador inscribe el dispositivo móvil para un usuario, las aplicaciones implementadas en el usuario no se instalarán en el dispositivo móvil. En su lugar, podrían instalarse las aplicaciones implementadas para el administrador.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Proteger la conexión entre el servidor de sitio de Configuration Manager y Exchange Server

Si el servidor Exchange se encuentra en un entorno local, use IPsec. Un entorno hospedado de Exchange protege automáticamente la conexión mediante SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Utilice el principio de privilegios mínimos para el conector  

Para obtener una lista de los cmdlet mínimos que necesita el conector de Exchange Server, vea [Administrar dispositivos móviles con Configuration Manager y Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a> Prácticas recomendadas de seguridad para equipos Mac  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Almacenar y acceder a archivos de origen de cliente desde una ubicación segura  

Antes de instalar o inscribir el cliente en un equipo Mac, Configuration Manager no verifica si los archivos de origen de cliente han sido manipulados. Descargue los archivos desde un origen de confianza. Almacénelos y acceda a estos de forma segura.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Supervisar y realizar un seguimiento del período de validez del certificado  

Para garantizar la continuidad de la actividad, supervise el periodo de validez de los certificados que utiliza para los equipos Mac y realice un seguimiento del mismo. Configuration Manager no renueva automáticamente el certificado ni le advierte de que este va a expirar. El período de validez típico suele ser de un año.  

Para obtener más información sobre cómo renovar el certificado, vea [Renovar de forma manual el certificado de cliente Mac](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configurar el certificado raíz de confianza solo para SSL  

Para facilitar la protección contra la elevación de privilegios, configure el certificado de la entidad de certificación raíz de confianza para que solo confíe en el protocolo SSL.

Al inscribir equipos Mac, se instala automáticamente un certificado de usuario para administrar el cliente de Configuration Manager. En este certificado de usuario, se incluyen los certificados raíz de confianza en esta cadena de confianza. Para restringir la confianza de este certificado raíz solo al protocolo SSL, siga este procedimiento:  

1. En el equipo Mac, abra una ventana de terminal.  

2. Escriba este comando: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. En el cuadro de diálogo **Acceso a Llaveros**, en la sección **Llaveros**, haga clic en **Sistema**. Después, en la sección **Categoría**, haga clic en **Certificados**.  

4. Busque el certificado de CA raíz para el certificado de cliente Mac y haga doble clic en este.  

5. En el cuadro de diálogo para el certificado de entidad emisora raíz, expanda la sección **Confianza** y a continuación, realice los siguientes cambios:  

    1. **Al usar este certificado**: cambie la opción **Confiar siempre** a **Usar valores predeterminados del sistema**.  

    2. **Capa de sockets seguros (SSL)** : cambie la opción **No se especificó ningún valor** a **Confiar siempre**.  

6. Cierre el cuadro de diálogo. Cuando se le pida, escriba la contraseña del administrador y, después, haga clic en **Actualizar configuración**.  

Cuando se complete el procedimiento, solo se confiará en el certificado raíz para validar el protocolo SSL. Otros protocolos en los que no confía este certificado raíz son Correo seguro (S/MIME), Autenticación extensible (EAP) o la firma de código.  

> [!NOTE]  
> Además, siga este procedimiento si ha instalado el certificado de cliente de forma independiente de Configuration Manager.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemas de seguridad de los clientes de Configuration Manager  

Los siguientes problemas de seguridad no disponen de mitigación:  

### <a name="status-messages-arent-authenticated"></a>Los mensajes de estado no se autentican

No se realiza la autenticación de los mensajes de estado. Cuando un punto de administración acepta conexiones de cliente HTTP, cualquier dispositivo puede enviar mensajes de estado al punto de administración. Si el punto de administración solo admite conexiones de cliente HTTPS, es necesario que un dispositivo tenga un certificado de autenticación de cliente válido, pero también podría enviar cualquier mensaje de estado. El punto de administración descarta los mensajes de estado no válidos recibidos de un cliente.  

Existen posibles ataques frente a esta vulnerabilidad:

- Un atacante podría enviar un mensaje de estado falso para convertirse en miembro de una colección basada en consultas de mensajes de estado.
- Cualquier cliente podría iniciar una denegación de servicio contra el punto de administración al desbordarlo con mensajes de estado.
- Si los mensajes de estado desencadenan acciones en las reglas de filtro de mensajes de estado, un atacante podría desencadenar la regla de filtro de mensajes de estado.
- Un atacante podría enviar un mensaje de estado que hiciera que la información de los informes no fuera precisa.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>Las directivas pueden redestinarse a clientes sin destino  

Existen varios métodos que los atacantes podrían utilizar para hacer que una directiva destinada a un cliente se aplique a un cliente completamente diferente. Por ejemplo, un atacante desde un cliente de confianza podría enviar información falsa de detección o inventario para agregar el equipo a una colección a la que no tendría que pertenecer. Después, se cliente recibirá todas las implementaciones para esa colección.

Existen controles para impedir que los atacantes puedan modificar directamente una directiva. Pero los atacantes podrían usar una directiva existente para cambiar el formato y volver a implementar un SO y, después, enviarlo a otro equipo. Esta directiva redirigida podría crear una denegación de servicio. Estos tipos de ataques requieren una sincronización precisa y amplios conocimientos de la infraestructura de Configuration Manager.  

### <a name="client-logs-allow-user-access"></a>Los registros de cliente permiten el acceso de usuario  

Todos los archivos de registro de cliente conceden permiso a la cuenta **Grupos** con acceso de *Lectura* y al usuario **Interactivo** especial con acceso de *Escritura*. Si se habilita el registro detallado, los atacantes podrían leer los archivos de registro para buscar información acerca de vulnerabilidades de sistema o compatibilidad. Los procesos, como el software que el cliente instala en el contexto de un usuario, necesitan escribir en registros con una cuenta de usuario de derechos reducidos. Debido a comportamiento, un atacante también podría escribir en los registros con una cuenta de derechos reducidos.  

El riesgo más grave es que un atacante pudiera quitar información de los archivos de registro. Puede que un administrador necesitara esta información para detectar intrusiones y realizar auditorías.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Podría usarse un equipo para obtener un certificado diseñado para la inscripción de dispositivos móviles  

Cuando Configuration Manager procesa una solicitud de inscripción, no puede verificar si la solicitud se ha originado desde un dispositivo móvil o desde un equipo. Si la solicitud proviene de un equipo, puede instalar un certificado PKI que se puede registrar en Configuration Manager.

Para impedir un ataque de elevación de privilegios en este escenario, solo permita que los usuarios de confianza puedan inscribir sus dispositivos móviles. Supervise detenidamente las actividades de inscripción de dispositivos en el sitio.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Un cliente bloqueado sigue siendo capaz de enviar mensajes al punto de administración

Al bloquear un cliente en el que ya no confía, pero que ha establecido una conexión de red para la notificación de cliente, Configuration Manager no desconecta la sesión. El cliente bloqueado puede seguir enviando paquetes a su punto de administración hasta que el cliente se desconecta de la red. Estos paquetes son simplemente paquetes de conexión persistente de tamaño reducido. Este cliente no se puede administrar con Configuration Manager hasta que se desbloquee.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>La actualización de cliente automática no verifica el punto de administración

Al usar la actualización de cliente automática, el cliente puede dirigirse a un punto de administración para descargar los archivos de origen del cliente. En este escenario, el cliente no verifica el punto de administración como el origen de confianza.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Cuando los usuarios inscriben por primera vez equipos Mac, están en riesgo de ataques de suplantación de DNS  

Cuando el equipo Mac se conecta al punto de proxy de inscripción durante la inscripción, es poco probable que ya tenga el certificado de CA raíz de confianza. En este momento, el equipo Mac no confía en el servidor y le pide al usuario que continúe. Si un servidor DNS no autorizado resuelve el nombre de dominio completo (FQDN) del punto de proxy de inscripción, podría dirigir el equipo Mac a un punto de proxy de inscripción no autorizado para instalar certificados desde un origen que no sea de confianza. Para ayudar a reducir este riesgo, siga los procedimientos recomendados para evitar la suplantación de DNS en su entorno.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>La inscripción de equipos Mac no limita las solicitudes de certificado  

Los usuarios pueden volver a inscribir sus equipos Mac y solicitar cada vez un nuevo certificado de cliente. Configuration Manager no comprueba si hay varias solicitudes ni limita el número de certificados solicitados desde un mismo equipo. Un usuario no autorizado podría ejecutar un script que repita la solicitud de inscripción desde la línea de comandos. Este ataque podría causar una denegación de servicio en la red o la entidad de certificación (CA) emisora. Para ayudar a reducir este riesgo, debe supervisar cuidadosamente la CA emisora de certificados para este tipo de comportamiento sospechoso. Bloquee de inmediato desde la jerarquía de Configuration Manager cualquier equipo donde se muestre este patrón de comportamiento.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Una confirmación de borrado no comprueba que el dispositivo se haya borrado correctamente  

Si inicia una acción de borrado para un dispositivo móvil y Configuration Manager confirma el borrado, la verificación es que Configuration Manager ha *enviado* correctamente el mensaje. No comprueba que el dispositivo haya *actuado* en la solicitud.

Para los dispositivos móviles administrados por el conector de Exchange Server, una confirmación de borrado verifica que Exchange haya recibido el comando, pero no que lo haya recibido el dispositivo.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Si usa las opciones para confirmar los cambios en dispositivos de Windows Embedded, las cuentas podrían bloquearse antes de lo esperado  

Si el dispositivo de Windows Embedded ejecuta una versión del sistema operativo anterior a Windows 7 y un usuario intenta iniciar sesión cuando los filtros de escritura están deshabilitados por Configuration Manager, Windows solo permitirá la mitad del número configurado de intentos incorrectos antes de que se bloquee la cuenta.

Por ejemplo, imagine que configura la directiva de dominio **Umbral de bloqueo de cuenta** en seis intentos. Un usuario escribe de forma incorrecta la contraseña tres veces seguidas y la cuenta queda bloqueada. Este comportamiento crea de manera eficaz una denegación de servicio. Si los usuarios necesitan iniciar sesión en los dispositivos incrustados en este escenario, infórmeles sobre la posibilidad de un umbral de bloqueo reducido.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a> Información de privacidad para los clientes de Configuration Manager  

Al implementar el cliente de Configuration Manager, se habilita la configuración del cliente para las características de Configuration Manager. Las opciones que use para configurar las características se pueden aplicar a todos los clientes de la jerarquía de Configuration Manager. Este comportamiento es el mismo, independientemente de si están conectados directamente a la red interna, conectados mediante una sesión remota o conectados a Internet.  

La información del cliente se almacena en la base de datos de Configuration Manager de SQL Server y no se envía a Microsoft. La información se conserva en la base de datos hasta que se elimina mediante la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos** cada 90 días. Puede configurar el intervalo de eliminación. 

Algunos diagnósticos resumidos o agregados y datos de uso se envían a Microsoft. Para obtener más información, vea [Diagnósticos y datos de uso](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Antes de configurar el cliente de Configuration Manager, tenga en cuenta los requisitos de privacidad.  

Puede obtener más información sobre la recopilación y el uso de datos de Microsoft en la [declaración de privacidad de Microsoft](https://privacy.microsoft.com/privacystatement).

### <a name="client-status"></a>Estado de cliente  

Configuration Manager supervisa la actividad de los clientes. Evalúa de forma periódica el cliente de Configuration Manager y puede solucionar problemas con el cliente y sus dependencias. El estado del cliente está habilitado de forma predeterminada. Usa métricas del lado servidor para las comprobaciones de actividad de cliente. El estado de cliente usa acciones del lado cliente para comprobaciones automáticas, correcciones y el envío de información de estado de cliente al sitio. El cliente ejecuta las comprobaciones automáticas según una programación que puede configurar. El cliente envía los resultados de las comprobaciones al sitio de Configuration Manager. Esta información se cifra durante la transferencia.  

La información de estado de cliente se almacena en la base de datos de Configuration Manager de SQL Server y no se envía a Microsoft. La información no se almacena con un formato cifrado en la base de datos del sitio. La información se conserva en la base de datos hasta que se elimina según el valor configurado para la opción de estado de cliente **Retener el historial de estado de cliente durante el siguiente número de días**. El valor predeterminado de esta configuración es 31 días.  

Antes de instalar el cliente de Configuration Manager con comprobación de estado de cliente, tenga en cuenta sus requisitos de privacidad.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a> Información de privacidad para dispositivos móviles administrados mediante el conector de Exchange Server  

El conector de Exchange Server usa el protocolo ActiveSync para detectar y administrar dispositivos que se conecten a una instancia local u hospedada de Exchange Server. Los registros encontrados por el conector de Exchange Server se almacenan en la base de datos de Configuration Manager de SQL Server. La información se recopila desde Exchange Server. No contiene información adicional de lo que envían los dispositivos móviles a Exchange Server.  

La información de dispositivos móviles no se envía a Microsoft. La información de dispositivos móviles se almacena en la base de datos de Configuration Manager de la instancia de SQL Server. La información se conserva en la base de datos hasta que se elimina mediante la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos** cada 90 días. Puede configurar el intervalo de eliminación.  

Antes de instalar y configurar el conector de Exchange Server, tenga en cuenta los requisitos de privacidad.  

Puede obtener más información sobre la recopilación y el uso de datos de Microsoft en la [declaración de privacidad de Microsoft](https://privacy.microsoft.com/privacystatement).
