---
title: Configuración de cliente
titleSuffix: Configuration Manager
description: Obtenga información sobre la configuración predeterminada y personalizada para controlar los comportamientos del cliente.
ms.date: 07/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f6bb29930a6e2d4faf4ffdd141d3c9cd1831305
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365515"
---
# <a name="about-client-settings-in-configuration-manager"></a>Información sobre la configuración de cliente en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Administre toda la configuración de cliente en la consola de Configuration Manager desde el nodo **Configuración de cliente** del área de trabajo **Administración**. Configuration Manager incluye una configuración predeterminada. Si cambia la configuración predeterminada del cliente, esta configuración se aplicará a todos los clientes de la jerarquía. También puede establecer la configuración personalizada del cliente, que invalida la configuración predeterminada del cliente si la asigna a las recopilaciones. Para obtener más información, vea [Cómo configurar el cliente](configure-client-settings.md).

Las siguientes secciones describen los parámetros de configuración y las opciones con mayor detalle.  


## <a name="background-intelligent-transfer-service-bits"></a>Servicio de transferencia inteligente en segundo plano (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limitar el ancho de banda de red máximo para transferencias BITS en segundo plano

Cuando esta opción es **Sí**, los clientes usan el límite de ancho de banda de BITS. Para configurar las otras opciones de este grupo, debe habilitar esta configuración.

### <a name="throttling-window-start-time"></a>Hora de inicio de período de limitación

Especifique la hora de inicio local del período de limitación de BITS.  

### <a name="throttling-window-end-time"></a>Hora de finalización del período de limitación

Especifique la hora de finalización local del período de limitación de BITS. Si la hora de finalización coincide con la **hora de inicio del período de limitación**, la limitación de BITS siempre está habilitada.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Velocidad de transferencia máxima durante el período de limitación (Kbps)

Especifique la velocidad de transferencia máxima que pueden usar los clientes durante el período en cuestión.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Permitir descargas de BITS fuera del período de limitación

Permite a los clientes usar configuraciones de BITS independientes fuera del período especificado.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Velocidad de transferencia máxima fuera del período de limitación (Kbps)

Especifique la velocidad de transferencia máxima que los clientes pueden usar fuera del período de limitación de BITS.  



## <a name="client-cache-settings"></a>Configuración de la memoria caché del cliente

### <a name="configure-branchcache"></a>Configurar BranchCache

Configure el equipo cliente para [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
). Para permitir el almacenamiento en caché de BranchCache en el cliente, establezca **Habilitar BranchCache** en **Sí**.

- **Habilitar BranchCache**: Habilita BranchCache en los equipos cliente.

- **Tamaño máximo de la caché de BranchCache (porcentaje de disco)** : El porcentaje del disco que se permite usar a BranchCache.

> [!TIP]
> Si establece **Configurar BranchCache** en **No**, Configuration Manager no configura ningún parámetro de BranchCache.
>
> Para deshabilitar BranchCache, establezca **Configurar BranchCache** en **Sí**y, a continuación, establezca **Habilitar BranchCache** en **No**.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Configurar el tamaño de la caché de cliente

En la caché del cliente de Configuration Manager en los equipos Windows se almacenan los archivos temporales que se usan para instalar aplicaciones y programas. Si esta opción se establece en **No**, el tamaño predeterminado es 5120 MB.

Si elige **Sí**, especifique lo siguiente:

- **Tamaño máximo de caché (MB)**
- **Tamaño de caché máximo (porcentaje de disco)** : El tamaño de la caché de cliente se expande hasta el tamaño máximo en megabytes (MB) o el porcentaje del disco, lo que sea inferior.

### <a name="enable-as-peer-cache-source"></a>Habilitación como origen de caché del mismo nivel

> [!Note]  
> En la versión 1902 y versiones anteriores, esta configuración se denominaba **Habilitar el cliente de Configuration Manager en el SO completo para compartir contenido**. El comportamiento de la configuración no cambió.

Habilita la [caché del mismo nivel](../../plan-design/hierarchy/client-peer-cache.md) para los clientes de Configuration Manager. Seleccione **Sí** y, después, especifique el puerto con el que el cliente se comunica con el equipo del mismo nivel.

- **Puerto para difusión de red inicial** (UDP 8004 de manera predeterminada): Configuration Manager usa este puerto en Windows PE o en el sistema operativo Windows completo. El motor de secuencia de tareas de Windows PE envía la difusión para obtener las ubicaciones de contenido antes de iniciar la secuencia de tareas.<!--SCCMDocs issue 910-->

- **Puerto para descarga de contenido desde sistema del mismo nivel** (TCP 8003 de manera predeterminada): Configuration Manager configura automáticamente las reglas de Firewall de Windows para permitir este tráfico. Debe configurar los puertos manualmente si usa otro firewall.  

    Para más información, consulte [Puertos usados para las conexiones](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Duración mínima antes de que se pueda quitar contenido almacenado en caché (minutos)

<!--4485509-->
A partir de la versión 1906, especifique el tiempo mínimo durante el cual el cliente de Configuration Manager mantendrá el contenido almacenado en caché. Esta configuración de cliente define el tiempo mínimo que el agente de Configuration Manager debe esperar para quitar contenido de la memoria caché en caso de que se necesite más espacio.

De forma predeterminada, este valor es de 1.440 minutos (24 horas).
El valor máximo de esta configuración es de 10 080 minutos (una semana).

Esta opción proporciona mayor control sobre la caché de cliente en diferentes tipos de dispositivos. Puede reducir el valor en clientes que tienen unidades de disco duro pequeñas y no necesitan mantener el contenido existente antes de que se ejecute otra implementación.


## <a name="client-policy"></a>Directiva de cliente  

### <a name="client-policy-polling-interval-minutes"></a>Intervalo de sondeo de directiva de cliente (minutos)

Especifica con qué frecuencia descargan los siguientes clientes de Configuration Manager la directiva de cliente:

- Equipos Windows (por ejemplo, equipos de sobremesa, servidores, equipos portátiles)  
- Dispositivos móviles inscritos por Configuration Manager  
- Equipos Mac  
- Equipos que ejecutan Linux o UNIX  

De forma predeterminada, este valor es de 60 minutos. La reducción de este valor provoca que los clientes sondeen el sitio con más frecuencia. Con muchos clientes, este comportamiento puede tener un impacto negativo en el rendimiento del sitio. La [guía sobre el tamaño y la escala](../../plan-design/configs/size-and-scale-numbers.md) se basa en el valor predeterminado. El aumento de este valor provoca que los clientes sondeen el sitio con menos frecuencia. Los clientes tardan más en descargar y procesar los cambios realizados en las directivas de cliente, incluidas las nuevas implementaciones.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Habilitar directiva de usuario en clientes

Al establecer esta opción en **Sí**y usar la [detección de usuarios](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), los clientes reciben las aplicaciones y programas destinados al usuario que ha iniciado sesión.  

Si esta opción se establece en **No**, los usuarios no recibirán las aplicaciones necesarias que implemente para ellos. Los usuarios tampoco recibirán otras tareas de administración de directivas de usuario.  

Esta configuración se aplica a los usuarios cuando sus equipos estén en la intranet o en Internet. Debe ser **Sí** si también quiere habilitar directivas de usuario en Internet.  

> [!Note]  
> A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. No es posible instalar nuevos roles de catálogo de aplicaciones.
>
> Si sigue usando el catálogo de aplicaciones, este recibe la lista de software disponible para los usuarios desde el servidor de sitio. Por tanto, no es necesario establecer esta opción en **Sí** para que los usuarios puedan ver y solicitar aplicaciones del catálogo de aplicaciones. Si esta opción es **No**, los usuarios no podrán instalar las aplicaciones que vean en el catálogo de aplicaciones.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Habilitar solicitudes de directiva de usuario de clientes de Internet

Establezca esta opción en **Sí** para que los usuarios reciban la directiva de usuario en equipos basados en Internet. Los requisitos siguientes también son de aplicación:  

- El cliente y el sitio están configurados para la [administración de cliente basada en Internet](../manage/plan-internet-based-client-management.md) o [Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md).  

- El valor **Habilitar directiva de usuario en clientes** es **Sí**.  

- El punto de administración basado en Internet autentica correctamente al usuario mediante la autenticación de Windows (Kerberos o NTLM). Para obtener más información, vea [Consideraciones sobre las comunicaciones de cliente desde Internet](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- Cloud Management Gateway autentica correctamente al usuario mediante el uso de Azure Active Directory. Para obtener más información, vea cómo [implementar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

Si esta opción se establece en **No** (o no se cumple alguno de los requisitos anteriores), un equipo conectado a Internet solo recibirá directivas de equipo. En este escenario, los usuarios sí podrán ver, solicitar e instalar aplicaciones desde un catálogo de aplicaciones basado en Internet. Si esta opción se establece en **No**, pero la opción **Habilitar directiva de usuario en clientes** se establece en **Sí**, los usuarios no recibirán las directivas de usuario hasta que el equipo se conecte a la intranet.  

> [!NOTE]  
> Para la administración de cliente basada en Internet, las solicitudes de aprobación de aplicación de los usuarios no necesitan directivas de usuario ni autenticación de usuarios. Cloud Management Gateway no es compatible con solicitudes de aprobación de aplicación.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Habilitar directiva de usuario para varias sesiones de usuario

<!--4737447-->

*Se aplica a la versión 1910*

Esta configuración está deshabilitada de forma predeterminada. Incluso si se habilitan directivas de usuario, a partir de la versión 1906 el cliente las deshabilitará de forma predeterminada en cualquier dispositivo que permita varias sesiones de usuario activas simultáneas (por ejemplo, varios servidores de Terminal Server o una sesión múltiple de Windows 10 Enterprise en [Windows Virtual Desktop](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)).

El cliente solo deshabilita la directiva de usuario cuando detecta este tipo de dispositivo durante una instalación nueva. En un cliente existente de este tipo que actualice a la versión 1906 o posterior, se conserva el comportamiento anterior. En un dispositivo existente, establece la configuración de directiva de usuario incluso si detecta que el dispositivo permite varias sesiones de usuario.

Si requiere una directiva de usuario en este escenario y acepta cualquier posible impacto en el rendimiento, habilite esta configuración de cliente.


## <a name="cloud-services"></a>Servicios en la nube

### <a name="allow-access-to-cloud-distribution-point"></a>Permitir acceso al punto de distribución de nube

Establezca esta opción en **Sí** para que los clientes obtengan contenido desde un punto de distribución de nube. Esta configuración no necesita que el dispositivo esté basado en Internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory

Al configurar Azure Active Directory para admitir la combinación híbrida, Configuration Manager configura los dispositivos Windows 10 para esta funcionalidad. Para obtener más información, vea [Configuración de dispositivos híbridos unidos a Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Permitir que los clientes usen una instancia de Cloud Management Gateway

De forma predeterminada, todos los clientes de itinerancia de Internet usan cualquier instancia de [Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md) disponible. Un ejemplo de cuándo se debe establecer esta opción en **No** es para el uso de ámbito del servicio, por ejemplo durante un proyecto piloto o para ahorrar costos.



## <a name="compliance-settings"></a>Configuración de cumplimiento  

### <a name="enable-compliance-evaluation-on-clients"></a>Habilitar la evaluación de cumplimiento de normas en clientes

Establezca esta opción en **Sí** para configurar el resto de las opciones de este grupo.

### <a name="schedule-compliance-evaluation"></a>Programar evaluación de compatibilidad

Seleccione **Programación** para crear la programación predeterminada para las implementaciones de línea base de configuración. Este valor se puede configurar para cada línea de base en el cuadro de diálogo **Implementar línea de base de configuración**.  

### <a name="enable-user-data-and-profiles"></a>Habilitar perfiles y datos de usuario

Seleccione **Sí** si quiere implementar elementos de configuración de [perfiles y datos de usuario](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agente de equipo  

### <a name="user-notifications-for-required-deployments"></a>Notificaciones de usuario para las implementaciones requeridas

Para obtener más información sobre las siguientes tres configuraciones, vea [Notificaciones de usuario para las implementaciones requeridas](../../../apps/deploy-use/deploy-applications.md#bkmk_notify):

- **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)**
- **La fecha límite de la implementación es antes de 24 horas. Recordar al usuario cada (horas)**
- **La fecha límite de la implementación es antes de 1 hora. Recordar al usuario cada (minutos)**

### <a name="default-application-catalog-website-point"></a>Punto de sitios web del catálogo de aplicaciones predeterminado

> [!Important]  
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager utiliza este valor para conectar a los usuarios al catálogo de aplicaciones desde el Centro de software. Seleccione **Sitio web** para especificar un servidor que hospede el punto de sitios web del catálogo de aplicaciones. Escriba su nombre NetBIOS o FQDN, especifique la detección automática o una dirección URL para implementaciones personalizadas. En la mayoría de los casos, la detección automática es la mejor opción.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer

> [!Important]  
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Si esta opción es **Sí**, el cliente agrega de forma automática la dirección URL del sitio web del catálogo de aplicaciones predeterminado actual a la zona de sitios de confianza de Internet Explorer.  

Este valor garantiza que no esté habilitada la configuración de Internet Explorer para el modo protegido. Si el modo protegido está habilitado, es posible que el cliente de Configuration Manager no pueda instalar aplicaciones desde el catálogo de aplicaciones. De manera predeterminada, la zona de sitios de confianza también admite el inicio de sesión de usuario para el catálogo de aplicaciones, lo que requiere la autenticación de Windows.  

Si esta opción se mantiene como **No**, es posible que los clientes de Configuration Manager no puedan instalar aplicaciones desde el catálogo de aplicaciones. Un método alternativo consiste en configurar estas opciones de Internet Explorer en otra zona para la dirección URL del catálogo de aplicaciones que usan los clientes.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado.

> [!Important]  
> El cliente no instala Silverlight automáticamente.
>
> A partir de la versión 1806, la **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite. Los usuarios deben utilizar el nuevo Centro de software. Para obtener más información, consulte [Configurar el centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Este valor debe ser **Sí** para que los usuarios utilicen el catálogo de aplicaciones.  

Si cambia esta configuración, entrará en vigor cuando los usuarios carguen sus exploradores o actualicen las ventanas del explorador que tengan abiertas.  

Para obtener más información sobre esta configuración, vea [Certificados de Microsoft Silverlight 5 y modo de confianza elevado necesarios para el catálogo de aplicaciones](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Nombre de organización mostrado en el Centro de software

Escriba el nombre que ven los usuarios en el Centro de software. Esta información de marca ayuda a los usuarios a identificar a esta aplicación como un origen de confianza. Para obtener más información acerca de la prioridad de esta configuración, consulte [Branding Software Center](../../../apps/plan-design/plan-for-software-center.md#branding-software-center) (Centro de software de personalización de marca).  

### <a name="use-new-software-center"></a>Usar el nuevo Centro de software

El valor predeterminado es **Sí**.

Cuando establece esta opción en **Sí**, todos los equipos cliente usan el Centro de software. El Centro de software muestra software, actualizaciones de software y secuencias de tareas que se implementan en usuarios o dispositivos.

### <a name="enable-communication-with-health-attestation-service"></a>Habilitar la comunicación con el servicio de atestación de estado

Establezca esta opción en **Sí** para que los dispositivos con Windows 10 usen la [Atestación de estado](../../servers/manage/health-attestation.md). Al habilitar esta opción, la siguiente también está disponible para la configuración.

### <a name="use-on-premises-health-attestation-service"></a>Usar el servicio de atestación de estado local

Establezca esta opción en **Sí** para que los dispositivos usen un servicio local. Establezca esta opción en **No** para que los dispositivos usen el servicio basado en la nube de Microsoft.  

### <a name="install-permissions"></a>Permisos de instalación

Configure cómo los usuarios pueden instalar software, actualizaciones de software y secuencias de tareas:  

- **Todos los usuarios**: usuarios con cualquier permiso excepto Invitado.  

- **Solo los administradores**: los usuarios deben ser miembros del grupo de administradores local.  

- **Solo administradores y usuarios primarios**: los usuarios deben ser miembros del grupo de administradores local o usuarios primarios del equipo.  

- **Ningún usuario**: ningún usuario que haya iniciado sesión en un equipo cliente podrá instalar software, actualizaciones de software y secuencias de tareas. Las implementaciones necesarias para el equipo siempre se instalan en la fecha límite. Los usuarios no pueden instalar software desde el Centro de software.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Suspender indicación de PIN de BitLocker en el reinicio

Si los equipos requieren la indicación de PIN de BitLocker, esta opción omite el requisito de escribir un PIN cuando se reinicia el equipo después de una instalación de software.  

- **Siempre**: Configuration Manager suspende temporalmente BitLocker después de que haya instalado software que requiere un reinicio y reinicia el equipo. Esta configuración solo se aplica cuando Configuration Manager reinicia el equipo. Esta configuración no suspende el requisito de escribir el PIN de BitLocker cuando el usuario reinicia el equipo. El requisito de indicación de PIN de BitLocker se reanuda tras el inicio de Windows.

- **Nunca**: Configuration Manager no suspende BitLocker después de instalar software que necesite un reinicio. En este escenario, la instalación del software no puede finalizar hasta que el usuario escriba el PIN para completar el proceso de inicio estándar y se cargue Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Un software adicional administra la implementación de aplicaciones y actualizaciones de software

Habilite esta opción solo si se cumple alguna de las siguientes condiciones:  

- Utiliza una solución de proveedor que requiere que esta opción esté habilitada.  

- Utilice el kit de desarrollo de software (SDK) de Configuration Manager para administrar las notificaciones de agente de cliente y la instalación de aplicaciones y actualizaciones de software.  

> [!WARNING]  
> - Si selecciona esta opción y no se cumple ninguna de estas condiciones, el cliente no instalará las actualizaciones de software y las aplicaciones necesarias. Esta configuración no impide que los usuarios instalen software disponible desde el Centro de software, incluidas aplicaciones, paquetes y secuencias de tareas.  
> -  Al habilitar esta opción, no se producen en los clientes notificaciones del sistema para software nuevo o software necesario. <!--6347668-->

### <a name="powershell-execution-policy"></a>Directiva de ejecución de PowerShell

Configure cómo pueden ejecutar los clientes de Configuration Manager scripts de Windows PowerShell. Puede utilizar estos scripts para la detección de elementos de configuración para la configuración de compatibilidad. También puede enviar los scripts en una implementación como script estándar.  

- **Desviar**: el cliente de Configuration Manager desvía la configuración de Windows PowerShell en el equipo cliente para que puedan ejecutarse los scripts sin firmar.  

- **Restringido**: el cliente de Configuration Manager usa la configuración actual de PowerShell en el equipo cliente. Esta configuración determina si se pueden ejecutar scripts sin firmar.  

- **Todos firmados**: el cliente de Configuration Manager ejecuta scripts solo si los ha firmado un editor de confianza. Esta restricción se aplica independientemente de la configuración actual de PowerShell del equipo cliente.  

Esta opción requiere al menos la versión 2.0 de Windows PowerShell. El valor predeterminado es **Todos firmados**.  

> [!TIP]  
> Si no se ejecutan los scripts sin firmar debido a esta configuración de cliente, Configuration Manager informará de este error de las siguientes maneras:  
>
> - En el área de trabajo **Supervisión** de la consola se muestra el identificador de error **0x87D00327**. También muestra la descripción **El script no se firmó**.  
> - Los informes muestran el tipo de error **Error de detección**. Luego muestran el código de error **0x87D00327** y la descripción **El script no se firmó**, o bien el código de error **0x87D00320** y la descripción **Aún no se ha instalado el host de script**. Un informe de ejemplo es **Detalles de errores de elementos de configuración en una línea base de configuración para un activo**.  
> - El archivo **DcmWmiProvider.log** muestra el mensaje **El script no se firmó (Error: 87D00327; Origen: CCM)** .  

### <a name="show-notifications-for-new-deployments"></a>Mostrar notificaciones para nuevas implementaciones

Elija **Sí** para mostrar una notificación para las implementaciones disponibles durante menos de una semana. Este mensaje se muestra cada vez que se inicie el agente cliente.

### <a name="disable-deadline-randomization"></a>Deshabilitar selección aleatoria de fecha límite

Después de la fecha límite de la implementación, esta configuración determina si el cliente usa un retardo de activación de hasta dos horas para instalar las actualizaciones de software necesarias. De forma predeterminada, el retardo de activación está deshabilitado.  

Para escenarios de infraestructura de escritorio virtual (VDI), este retardo ayuda a distribuir el procesamiento de la CPU y la transferencia de datos para un equipo host con varias máquinas virtuales. Aunque no use VDI, si un gran número de clientes instalan las mismas actualizaciones al mismo tiempo, puede incrementarse negativamente el uso de CPU en el servidor de sitio. Este comportamiento también puede ralentizar los puntos de distribución y reducir considerablemente el ancho de banda de red disponible.  

Si los clientes tienen que instalar las actualizaciones de software en la fecha límite de la implementación sin demora, establezca esta opción en **Sí**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)

Si quiere proporcionar a los usuarios más tiempo para instalar las implementaciones de actualizaciones de software o aplicaciones necesarias después de la fecha límite, establezca un valor para esta opción. Este período de gracia es para un equipo desactivado durante un período prolongado y el usuario tiene que instalar muchas implementaciones de aplicación o actualización. Por ejemplo, este ajuste es útil si un usuario vuelve de vacaciones y tiene que esperar mucho tiempo mientras el cliente instala las implementaciones de aplicación atrasadas.

Establezca un período de gracia de entre 0 y 120 horas. Use esta configuración junto con la propiedad de implementación **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario**. Para obtener más información, consulte [Deploy applications](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period) (Implementar aplicaciones).


### <a name="enable-endpoint-analytics-data-collection"></a>Habilitación de la recopilación de datos del análisis de puntos de conexión

Esta opción permite habilitar la recopilación de datos locales en el cliente para cargarlos en el análisis de puntos de conexión. Establezca esta opción en **Sí** para configurar los dispositivos para la recopilación de datos locales. De lo contrario, establézcala en **No** para deshabilitar la recopilación de los datos locales. Para obtener más información, consulte [Inscripción de dispositivos de Configuration Manager en el análisis de puntos de conexión](../../../../analytics/enroll-configmgr.md).

## <a name="computer-restart"></a>Reinicio de equipo

Para más información sobre esta configuración, consulte [Notificaciones de reinicio del dispositivo](device-restart-notifications.md).<!-- 7182335 -->

## <a name="delivery-optimization"></a>Optimización de entrega

<!-- 1324696 -->
Los grupos de límites de Configuration Manager se usan para definir y regular la distribución de contenido a través de la red corporativa y en las oficinas remotas. La [optimización de distribución de Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) es una tecnología entre iguales basada en la nube para compartir contenido entre los dispositivos de Windows 10. Configure Optimización de entrega para usar los grupos de límites al compartir contenido entre iguales.

> [!Note]
> - La optimización de distribución solo está disponible en clientes de Windows 10.
> - El acceso al servicio en la nube Optimización de distribución a través de Internet es un requisito para utilizar su funcionalidad punto a punto. Para obtener información sobre los puntos de conexión de Internet necesarios, vea [Preguntas más frecuentes sobre Optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - Cuando se usa CMG para el almacenamiento de contenido, el contenido de las actualizaciones de terceros no se descarga en los clientes si está habilitada la [opción de cliente](#allow-clients-to-download-delta-content-when-available) **Descarga de contenido diferencial cuando esté disponible**. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Uso de grupos de límites de Configuration Manager para el identificador del grupo de optimización de distribución

Seleccione **Sí** para aplicar el identificador del grupo de límites como identificador del grupo de optimización de entrega en el cliente. Cuando el cliente se comunica con el servicio en la nube de Optimización de entrega, utiliza este identificador para buscar elementos del mismo nivel con el contenido. Al habilitar esta configuración, también se establece el modo de descarga Optimización de distribución en la opción Grupo (2) en los clientes de destino.

> [!Note]
> Microsoft recomienda permitir que el cliente configure esta opción a través de la directiva local, en lugar de la directiva de grupo. De esta manera, el identificador del grupo de límites puede establecerse como identificador del grupo de optimización de entrega en el cliente. Para obtener más información, consulte [Optimización de entrega](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Permitir que los dispositivos administrados por Configuration Manager usen servidores de caché con conexión de Microsoft para la descarga de contenido

<!--3555764-->
Elija **Sí** para permitir que los clientes descarguen contenido desde un punto de distribución local que haya habilitado como servidor de caché con conexión de Microsoft. Para más información, vea [Caché con conexión de Microsoft en Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> Además de la información siguiente, encontrará más detalles sobre el uso de las opciones de cliente de Endpoint Protection en [Escenario de ejemplo: uso de Endpoint Protection para proteger los equipos frente al malware](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Administrar el cliente de Endpoint Protection en equipos cliente

Seleccione **Sí** si quiere administrar los clientes existentes de Endpoint Protection y Windows Defender en los equipos de la jerarquía.  

Seleccione esta opción si ya ha instalado el cliente de Endpoint Protection y quiere administrarlo con Configuration Manager. En esta instalación independiente se incluye un proceso incluido en script en el que se usa una aplicación o un paquete de Configuration Manager y un programa. No es necesario que los dispositivos Windows 10 tengan instalado el agente de Endpoint Protection. Aun así, seguirá siendo necesario habilitar la **administración del cliente de Endpoint Protection en equipos cliente** para estos dispositivos. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Instalar cliente de Endpoint Protection en equipos cliente

Seleccione **Sí** para instalar y habilitar el cliente de Endpoint Protection en los equipos cliente donde aún no se ejecute. No es necesario que los clientes Windows 10 tengan instalado el agente de Endpoint Protection.  

> [!NOTE]  
> Si el cliente de Endpoint Protection ya está instalado y se selecciona **No**, el cliente de Endpoint Protection no se desinstalará. Para desinstalar el cliente de Endpoint Protection, establezca la configuración de cliente **Administrar el cliente de Endpoint Protection en equipos cliente** en **No**. Después, implemente un paquete y un programa para desinstalar el cliente de Endpoint Protection.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Permitir la instalación y los reinicios del cliente de Endpoint Protection fuera de las ventanas de mantenimiento. Las ventanas de mantenimiento deben conceder, como mínimo, 30 minutos para la instalación del cliente.

Establezca esta opción en **Sí** para invalidar los comportamientos de instalación típicos con las ventanas de mantenimiento. Esta opción cumple los requisitos empresariales para la prioridad del mantenimiento del sistema por motivos de seguridad.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Para dispositivos de Windows Embedded con filtros de escritura, confirmar la instalación del cliente de Endpoint Protection (reinicios necesarios)

Seleccione **Sí** para deshabilitar el filtro de escritura en el dispositivo Windows Embedded y reiniciar el dispositivo. Esta acción confirma la instalación en el dispositivo.  

Si establece opción en **No**, el cliente se instala en una superposición temporal que se borra cuando se reinicia el dispositivo. En este escenario, el cliente de Endpoint Protection no se instala de forma completa hasta que otra instalación confirme los cambios en el dispositivo. Esta configuración es la predeterminada.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Suprimir cualquier reinicio de equipo obligatorio después de instalar el cliente de Endpoint Protection

Elija **Sí** para suprimir un reinicio del equipo si es necesario después de instalar el cliente de Endpoint Protection.  

> [!IMPORTANT]  
> Si el cliente de Endpoint Protection requiere un reinicio del equipo y esta configuración es **No**, el equipo se reinicia, independientemente de las ventanas de mantenimiento configuradas.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Período de tiempo permitido que los usuarios pueden posponer un reinicio obligatorio para llevar a cabo la instalación de Endpoint Protection (horas)

Si es necesario reiniciar una vez instalado el cliente de Endpoint Protection, esta configuración especifica el número de horas que los usuarios pueden posponer el reinicio obligatorio. Esta configuración requiere que deshabilite la configuración siguiente: **Suprimir cualquier reinicio de equipo obligatorio después de instalar el cliente de Endpoint Protection**.

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Deshabilitar orígenes alternativos (como Microsoft Windows Update, Microsoft Windows Server Update Services o recursos compartidos de UNC) para la actualización de definición inicial en los equipos cliente

Seleccione **Sí** si quiere que Configuration Manager solo instale la actualización de definición inicial en los equipos cliente. Esta configuración puede ser útil para evitar conexiones de red innecesarias y reducir el ancho de banda de red durante la instalación inicial de la actualización de definiciones.  



## <a name="enrollment"></a>Inscripción

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervalo de sondeo para clientes heredados de dispositivos móviles

Seleccione **Establecer intervalo** para especificar el período de tiempo (en horas o minutos) que los dispositivos móviles heredados sondean la directiva. Estos dispositivos incluyen plataformas como Windows CE, macOS y Unix o Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Intervalo de sondeo para dispositivos modernos (minutos)

Escriba el número de minutos que los dispositivos modernos sondean la directiva. Esta configuración es para dispositivos Windows 10 que se administran a través de la administración local de dispositivos móviles.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Permitir a los usuarios inscribir dispositivos móviles y equipos Mac

Para habilitar la inscripción basada en usuario de dispositivos heredados, establezca esta opción en **Sí** y, después, establezca la configuración siguiente:

- **Perfil de inscripción**: Seleccione **Establecer perfil** para crear o seleccionar un perfil de inscripción. Para obtener más información, vea [Configurar las opciones del cliente para la inscripción](deploy-clients-to-macs.md#configure-client-settings).

### <a name="allow-users-to-enroll-modern-devices"></a>Permitir a los usuarios inscribir dispositivos modernos

Para habilitar la inscripción basada en usuario de dispositivos modernos, establezca esta opción en **Sí** y, después, establezca la configuración siguiente:

- **Perfil de inscripción de dispositivo moderno**: Seleccione **Establecer perfil** para crear o seleccionar un perfil de inscripción. Para obtener más información, vea [Crear un perfil de inscripción que permita a los usuarios inscribir dispositivos modernos](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Inventario de hardware  

### <a name="enable-hardware-inventory-on-clients"></a>Habilitar inventario de hardware en clientes

De forma predeterminada, esta opción es **Sí**. Para obtener más información, vea [Introducción al inventario de hardware](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Programación de inventario de hardware

Seleccione **Programación** para ajustar la frecuencia con la que los clientes ejecutan el ciclo de inventario de hardware. De forma predeterminada, este ciclo tiene lugar cada siete días.

### <a name="maximum-random-delay-minutes"></a>Retraso aleatorio máximo (minutos)

Especifique el número máximo de minutos para que el cliente de Configuration Manager seleccione de forma aleatoria el ciclo de inventario de hardware de la programación definida. Esta selección aleatoria entre todos los clientes ayuda a procesar el inventario de equilibrio de carga en el servidor de sitio. Puede especificar cualquier valor entre 0 y 480 minutos. De forma predeterminada, este valor está establecido en 240 minutos (4 horas).

### <a name="maximum-custom-mif-file-size-kb"></a>Tamaño de archivo MIF personalizado máximo (KB)

Especifique el tamaño máximo, en kilobytes (KB), que se permite para cada archivo MIF personalizado que el cliente recopila durante un ciclo de inventario de hardware. El agente de inventario de hardware de Configuration Manager no procesa los archivos MIF personalizados que superan este tamaño. Puede especificar un tamaño de entre 1 y 5 120 KB. De forma predeterminada, este valor está establecido en 250 KB. Esta configuración no afecta al tamaño del archivo de datos de inventario de hardware normal.  

> [!NOTE]  
> Este valor solo está disponible en la configuración predeterminada del cliente.  

### <a name="hardware-inventory-classes"></a>Clases de inventario de hardware

Seleccione **Establecer clases** para ampliar la información de hardware que se recopila de los clientes sin necesidad de modificar manualmente el archivo sms_def.mof. Para obtener más información, vea [Cómo configurar el inventario de hardware](../manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>Recopilar archivos MIF

Use esta opción para especificar si quiere recopilar archivos MIF de los clientes de Configuration Manager durante el inventario de hardware.  

Para que un archivo MIF sea recopilado por el inventario de hardware, debe estar en la ubicación correcta del equipo cliente. De forma predeterminada, los archivos se encuentran en las rutas de acceso siguientes:  

- Los **archivos IDMIF** deben estar en la carpeta Windows\System32\CCM\Inventory\Idmif.

- Los **archivos NOIDMIF** deben estar en la carpeta Windows\System32\CCM\Inventory\Noidmif.

> [!NOTE]  
> Este valor solo está disponible en la configuración predeterminada del cliente.



## <a name="metered-internet-connections"></a>Conexiones a Internet de uso medido  

Administre la forma en que los equipos con Windows 8 y versiones posteriores usan las conexiones a Internet de uso medido para comunicarse con Configuration Manager. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

> [!NOTE]  
> La configuración de cliente establecida no se aplica en los escenarios siguientes:  
>
> - Si el equipo está en una conexión de datos de itinerancia, el cliente de Configuration Manager no realiza ninguna tarea que necesite la transferencia de datos a sitios de Configuration Manager.  
> - Si las propiedades de conexión de red de Windows se configuran como de uso no medido, el cliente de Configuration Manager se comporta como si la conexión fuera de uso no medido y, de este modo, transfiere datos al sitio.  

### <a name="client-communication-on-metered-internet-connections"></a>Comunicación de clientes en conexiones a Internet de uso medido

Elija una de las opciones siguientes para esta configuración:  

- **Permitir**: se permiten todas las comunicaciones del cliente a través de la conexión a Internet de uso medido, a menos que el dispositivo cliente use una conexión de datos en movilidad.  

- **Limitar**: solo se permiten las siguientes comunicaciones de cliente a través de la conexión a Internet de uso medido:  

    - Recuperación de la directiva de cliente  

    - Mensajes de estado del cliente para enviar al sitio  

    - Solicitudes de instalación de software desde el Centro de software  

    - Implementaciones requeridas (una vez alcanzada la fecha límite de instalación)  

    Si se alcanza el límite de transferencia de datos para la conexión a Internet de uso medido, el cliente ya no intentará comunicarse con los sitios de Configuration Manager.  

- **Bloquear**: el cliente de Configuration Manager no intenta comunicarse con los sitios de Configuration Manager si se encuentra en una conexión a Internet de uso medido. Esta opción es el valor predeterminado.  

> [!IMPORTANT]  
> El cliente siempre permite las instalaciones de software desde el Centro de software, independientemente de la configuración de la conexión de Internet de uso medido. Si el usuario solicita una instalación de software mientras el dispositivo está en una red medida, el Centro de software respeta la intención del usuario.<!-- MEMDocs#285 -->


## <a name="power-management"></a>Administración de energía  

### <a name="allow-power-management-of-devices"></a>Permitir la administración de energía de dispositivos

Establezca esta opción en **Sí** para habilitar la administración de energía en los clientes. Para obtener más información, consulte [Introduction to power management](../manage/power/introduction-to-power-management.md) (Introducción a la administración de energía).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Permitir a los usuarios excluir su dispositivo de la administración de energía

En la lista desplegable, seleccione **Sí** para permitir que los usuarios del Centro de software excluyan sus equipos de cualquier configuración de administración de energía establecida.  

### <a name="allow-network-wake-up"></a>Permitir reactivación de la red

Cuando se habilita esta opción, el cliente establece la configuración de energía en el equipo para permitir que el adaptador de red reactive el dispositivo. Si deshabilita esta opción, el adaptador de red del equipo no podrá reactivar el dispositivo.

### <a name="enable-wake-up-proxy"></a>Habilitar proxy de reactivación

Especifique **Sí** para complementar la configuración de Wake on LAN del sitio cuando se configure para paquetes de unidifusión.  

Para obtener más información sobre el proxy de reactivación, vea [Planear la reactivación de clientes](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> No habilite el proxy de reactivación en una red de producción sin entender primero cómo funciona y evaluarlo en un entorno de prueba.  

Después, configure las siguientes opciones adicionales según sea necesario:

- **Número de puerto de proxy de reactivación (UDP)** : El número de puerto que los clientes usan para enviar paquetes de reactivación a equipos en suspensión. Mantenga el puerto predeterminado 25536, o bien cambie el número por un valor de su elección.  

- **Número de puerto de Wake on LAN (UDP)** : Mantenga el valor predeterminado de 9, a menos que haya cambiado el número de puerto de Wake on LAN (UDP) en la pestaña **Puertos** en las **Propiedades** del sitio.  

    > [!IMPORTANT]  
    > Este número debe coincidir con el número en las **Propiedades**del sitio. Si cambia este número en un lugar, este no se actualizará automáticamente en el otro lugar.  

- **Excepción del Firewall de Windows Defender para el proxy de reactivación**: El cliente de Configuration Manager configura automáticamente el número de puerto del proxy de reactivación en los dispositivos que ejecutan Firewall de Windows Defender. Seleccione **Configurar** para especificar los perfiles de firewall.  

    Si los clientes ejecutan otro firewall, necesita configurarlo manualmente para permitir el **Número de puerto de proxy de reactivación (UDP)** .  

- **Prefijos de IPv6 si son necesarios para DirectAccess u otros dispositivos de red que intervengan. Use una coma para especificar varias entradas**: Escriba los prefijos de IPv6 necesarios para que el proxy de reactivación funcione en la red.



## <a name="remote-tools"></a>Herramientas remotas  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Habilitar control remoto en clientes y Perfiles de excepción de firewall

Seleccione **Configurar** para habilitar la característica de control remoto de Configuration Manager. Opcionalmente, configure las opciones del firewall para permitir que el control remoto trabaje en los equipos cliente.  

El control remoto está deshabilitado de forma predeterminada.  

> [!IMPORTANT]  
> Si no se configuran las opciones del firewall, el control remoto podría no funcionar correctamente.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Los usuarios pueden cambiar la directiva o la configuración de notificaciones en el Centro de software

Seleccione si los usuarios pueden cambiar opciones del control remoto desde el Centro de software.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Permitir el control remoto de un equipo desatendido

Seleccione si un administrador puede usar el control remoto para tener acceso a un equipo cliente que ha cerrado la sesión o está bloqueado. Solo se puede usar el control remoto en un equipo que ha iniciado sesión y está desbloqueado cuando esta opción está deshabilitada.  

### <a name="prompt-user-for-remote-control-permission"></a>Solicitar al usuario permiso de control remoto

Seleccione si el equipo cliente muestra un mensaje solicitando el permiso del usuario antes de permitir una sesión de control remoto.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Solicitar permiso al usuario para transferir contenido del Portapapeles compartido

Antes de transferir el contenido desde el Portapapeles compartido en una sesión de control remoto, permita que los usuarios acepten o denieguen las transferencias de archivos. Los usuarios solo necesitan conceder permiso una vez por sesión. El visor no puede concederse permiso a sí mismo para transferir el archivo.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Conceder permiso de control remoto al grupo de administradores locales

Seleccione si los administradores locales del servidor que inicia la conexión de control remoto pueden establecer sesiones de control remoto en los equipos cliente.  

### <a name="access-level-allowed"></a>Nivel de acceso permitido

Especifique el nivel de acceso de control remoto que se permite. Elija una de las opciones siguientes:  

- **Sin acceso**
- **Solo vista**
- **Control total**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Visores permitidos de control remoto y asistencia remota

Seleccione **Establecer visores** para especificar los nombres de los usuarios de Windows que pueden establecer sesiones de control remoto en los equipos cliente.  

### <a name="show-session-notification-icon-on-taskbar"></a>Mostrar icono de notificación de sesión en la barra de tareas

Establezca esta opción en **Sí** para mostrar un icono en la barra de tareas de Windows del cliente para indicar una sesión de control remoto activa.  

### <a name="show-session-connection-bar"></a>Mostrar barra de conexión a la sesión

Establezca esta opción en **Sí** para mostrar una barra de conexión a la sesión de alta visibilidad en los clientes e indicar que hay una sesión de control remoto activa.  

### <a name="play-a-sound-on-client"></a>Reproducir un sonido en el cliente

Seleccione esta opción para indicar mediante un sonido si una sesión de control remoto está activa en un equipo cliente. Seleccione una de las siguientes opciones:

- **Sin sonido**
- **Inicio y final de la sesión** (valor predeterminado)
- **Varias veces durante la sesión**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Administrar configuración de asistencia remota no solicitada

Establezca esta opción en **Sí** para permitir que Configuration Manager administre sesiones de asistencia remota no solicitadas.  

En una sesión de asistencia remota no solicitada, el usuario del equipo cliente no ha solicitado ayuda para iniciar la sesión.  

### <a name="manage-solicited-remote-assistance-settings"></a>Administrar configuración de asistencia remota solicitada

Establezca esta opción en **Sí** para permitir que Configuration Manager administre sesiones de asistencia remota solicitada.  

En una sesión de asistencia remota solicitada, el usuario del equipo cliente envió una solicitud de asistencia remota al administrador.  

### <a name="level-of-access-for-remote-assistance"></a>Nivel de acceso de asistencia remota

Seleccione el nivel de acceso que se va a asignar a las sesiones de asistencia remota que se inician en la consola de Configuration Manager. Seleccione una de las siguientes opciones:

- **Ninguna** (valor predeterminado)
- **Visualización remota**
- **Control total**

> [!NOTE]  
> El usuario en el equipo cliente siempre debe conceder permiso para que se produzca una sesión de asistencia remota.  

### <a name="manage-remote-desktop-settings"></a>Administrar configuración de Escritorio remoto

Establezca esta opción en **Sí** para permitir que Configuration Manager administre sesiones de Escritorio remoto en equipos.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Permitir a los usuarios permitidos conectarse mediante la conexión a Escritorio remoto

Establezca esta opción en **Sí** para agregar los usuarios especificados en la lista de visores permitidos al grupo de usuarios local de Escritorio remoto en los clientes.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Requerir autenticación de nivel de red en equipos que ejecutan el sistema operativo Windows Vista y versiones posteriores

Establezca esta opción en **Sí** para usar autenticación de nivel de red (NLA) para establecer conexiones de Escritorio remoto con los equipos cliente. La autenticación a nivel de red requiere menos recursos del equipo remoto al principio dado que finaliza la autenticación del usuario antes de establecer una conexión de Escritorio remoto. El uso de NLA es una configuración más segura. NLA ayuda a proteger al equipo frente a software o usuarios malintencionados, y reduce el riesgo de ataques por denegación de servicio.  



## <a name="software-center"></a>Centro de software

### <a name="select-these-new-settings-to-specify-company-information"></a>Seleccionar la configuración nueva para especificar la información de la compañía

Establezca esta opción en **Sí** y, después, especifique las opciones siguientes para personalizar el Centro de software para su organización:

- **Nombre de la empresa**: Escriba el nombre de la organización que ven los usuarios en el Centro de software.  

- **Combinación de colores del Centro de software**: haga clic en **Seleccionar color** para definir el color principal que usa el Centro de software.  

- **Seleccionar un logotipo para el Centro de software**: haga clic en **Examinar** para seleccionar una imagen para mostrar en el Centro de software. El logotipo debe ser un archivo JPEG, PNG o BMP de 400 x 100 píxeles, con un tamaño máximo de 750 KB. El nombre del archivo de logotipo no puede contener espacios.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a> Ocultar aplicaciones no aprobadas en el Centro de software

Cuando esta opción está habilitada, las aplicaciones disponibles para el usuario que requieren aprobación están ocultas en el Centro de software.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a> Ocultar aplicaciones instaladas en el Centro de software

Cuando esta opción está habilitada, las aplicaciones que ya están instaladas ya no se muestran en la pestaña Aplicaciones. Esta opción se establece como valor predeterminado al instalar o actualizar a Configuration Manager. Las aplicaciones instaladas siguen estando disponibles para su revisión en la pestaña Estado de la instalación. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a> Ocultar el vínculo del catálogo de aplicaciones en el Centro de software

Especifique la visibilidad del vínculo al sitio web del catálogo de aplicaciones en el Centro de software. Al establecer esta opción, los usuarios no verán el vínculo al sitio web del catálogo de aplicaciones en el nodo Estado de la instalación del Centro de software. <!--1358214-->

> [!Important]  
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  

### <a name="software-center-tab-visibility"></a>Visibilidad de las pestañas del Centro de software

#### <a name="starting-in-version-1906"></a>A partir de la versión 1906
<!--4063773-->

Elija las pestañas que estarán visibles en el Centro de software. Use el botón **Agregar** para mover una pestaña a **Pestañas visibles**. Use el botón **Quitar** para moverla a la lista **Pestañas ocultas**. Ordene las pestañas con los botones **Subir** o **Bajar**. 

Pestañas disponibles:
- **Aplicaciones**
- **Actualizaciones**
- **Sistemas operativos**
- **Estado de la instalación**
- **Cumplimiento de dispositivos**
- **Opciones**
- Haga clic en el botón **Agregar pestaña** para agregar hasta cinco pestañas personalizadas.
  - Especifique los valores para **Nombre de la pestaña** y **Dirección URL de contenido** para la pestaña personalizada.
  - Seleccione **Eliminar pestaña** para quitar una pestaña personalizada.  

  >[!Important]  
  > - Puede que algunas de las características de los sitios web no funcionen cuando se usen como una pestaña personalizada en el Centro de software. Asegúrese de probar los resultados antes de implementar esto en los clientes. <!--519659-->
  > - Cuando agregue una pestaña personalizada, especifique solo direcciones de sitio web de intranet o de confianza.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Versión 1902 y versiones anteriores

Establezca las opciones adicionales de este grupo en **Sí** para que las pestañas siguientes sean visibles en el Centro de software:

- **Aplicaciones**
- **Actualizaciones**
- **Sistemas operativos**
- **Estado de la instalación**
- **Cumplimiento de dispositivos**
- **Opciones**
- **Especifique una pestaña personalizada para el Centro de Software** <!--1358132-->
    - **Nombre de pestaña**
    - **URL de contenido**

    >[!Important]  
    > Puede que algunas de las características de los sitios web no funcionen cuando se usen como una pestaña personalizada en el Centro de software. Asegúrese de probar los resultados antes de implementar esto en los clientes. <!--519659-->
    >
    > Cuando agregue una pestaña personalizada, especifique solo direcciones de sitio web de intranet o de confianza.<!--SCCMDocs issue 1575-->

Por ejemplo, si la organización no usa las directivas de cumplimiento y quiere ocultar la pestaña Compatibilidad de dispositivos en el Centro de software, establezca la opción **Habilitar pestaña Cumplimiento del dispositivo** en **No**.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a> Configuración de vistas predeterminadas en el Centro de software
<!--3612112-->
*(Se introdujo en la versión 1902)*

- Configure el **filtro de aplicación predeterminado**, ya sean **todas** las aplicaciones o solo las **requeridas**.  

  - Centro de software siempre usa la configuración predeterminada. Los usuarios pueden cambiar este filtro, pero el Centro de software no conserva sus preferencias.  

- Establezca la **vista de aplicación predeterminada** como **vista de mosaico** o **vista de lista**.

  - Si un usuario cambia esta configuración, el Centro de software mantiene la preferencia del usuario en el futuro.


## <a name="software-deployment"></a>Implementación de software  

### <a name="schedule-re-evaluation-for-deployments"></a>Programar la reevaluación para implementaciones

Configure una programación para cuando Configuration Manager vuelva a evaluar las reglas de requisitos para todas las implementaciones. El valor predeterminado es cada siete días.  

> [!IMPORTANT]  
> Esta configuración es más invasiva para el cliente local que para el servidor de red o de sitio. Una programación de reevaluación más agresiva afecta de forma negativa al rendimiento de los equipos cliente y de red. Microsoft no recomienda establecer un valor inferior al valor predeterminado. Si modifica este valor, supervise de cerca el rendimiento.  

Inicie esta acción desde un cliente del modo siguiente: en el panel de control de **Configuration Manager**, en la pestaña **Acciones**, seleccione **Ciclo de evaluación de implementación de aplicaciones**.  



## <a name="software-inventory"></a>Inventario de software  

### <a name="enable-software-inventory-on-clients"></a>Habilitar inventario de software en clientes

Esta opción se establece en **Sí** de forma predeterminada. Para obtener más información, vea [Introducción al inventario de software](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Programar inventario de software y recopilación de archivos

Seleccione **Programación** para ajustar la frecuencia con la que los clientes ejecutan los ciclos de inventario de software y recopilación de archivos. De forma predeterminada, este ciclo tiene lugar cada siete días.

### <a name="inventory-reporting-detail"></a>Detalle de notificación de inventario

Especifique uno de los niveles siguientes de información de archivo para incluir en el inventario:

- **Solo archivo**
- **Solo producto**
- **Detalles completos** (valor predeterminado)

### <a name="inventory-these-file-types"></a>Inventariar estos tipos de archivo

Si quiere especificar los tipos de archivo para incluir en el inventario, seleccione **Tipos** y, después, configure las opciones siguientes:  

> [!NOTE]  
> Si se aplican varias configuraciones de cliente personalizadas a un equipo, se combina el inventario devuelto por cada configuración.  

- Seleccione **Nuevo** para agregar un nuevo tipo de archivo al inventario. Después, especifique la información siguiente en el cuadro de diálogo **Propiedades de archivo inventariado**:  

    - **Nombre**: asigne un nombre al archivo que quiere inventariar. Use un carácter comodín de asterisco (`*`) para representar cualquier cadena de texto y un signo de interrogación (`?`) para representar cualquier carácter individual. Por ejemplo, si quiere hacer un inventario de todos los archivos con la extensión .doc, especifique el nombre de archivo `*.doc`.  

    - **Ubicación**: seleccione **Establecer** para abrir el cuadro de diálogo **Propiedades de ruta de acceso**. Configure el inventario de software para buscar el archivo especificado en todos los discos duros del cliente, buscar en una ruta de acceso especificada (por ejemplo, `C:\Folder`) o buscar una variable especificada (por ejemplo, `%windir%`). También puede buscar en todas las subcarpetas de la ruta de acceso especificada.  

    - **Excluir archivos cifrados y comprimidos**: al seleccionar esta opción, en el inventario no se incluye ningún archivo comprimido o cifrado.  

    - **Archivos excluidos en la carpeta Windows**: al seleccionar esta opción, en el inventario no se incluye ningún archivo de la carpeta Windows y sus subcarpetas.  

    Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades de archivo inventariado**. Agregue todos los archivos que quiera incluir en el inventario y, después, seleccione **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente**.  

### <a name="collect-files"></a>Recopilar archivos

Si quiere recopilar archivos de los equipos cliente, seleccione **Archivos** y, después, configure las opciones siguientes:  

> [!NOTE]  
> Si se aplican varias configuraciones de cliente personalizadas a un equipo, se combina el inventario devuelto por cada configuración.  

- En el cuadro de diálogo **Configurar valor de cliente**, seleccione **Nuevo** para agregar un archivo para la recopilación.  

- En el cuadro de diálogo **Propiedades del archivo recopilado** , proporcione la siguiente información:  

    - **Nombre**: asigne un nombre al archivo que quiera recopilar. Use un carácter comodín de asterisco (`*`) para representar cualquier cadena de texto y un signo de interrogación (`?`) para representar cualquier carácter individual.  

    - **Ubicación**: seleccione **Establecer** para abrir el cuadro de diálogo **Propiedades de ruta de acceso**. Configure el inventario de software para buscar el archivo que quiere recopilar en todos los discos duros del cliente, buscar en una ruta de acceso especificada (por ejemplo, `C:\Folder`) o buscar una variable especificada (por ejemplo, `%windir%`). También puede buscar en todas las subcarpetas de la ruta de acceso especificada.  

    - **Excluir archivos cifrados y comprimidos**: al seleccionar esta opción, no se recopila incluye ningún archivo comprimido o cifrado.  

    - **Detener la recopilación de archivos cuando el tamaño total de archivos supere (KB)** : especifique el tamaño del archivo, en kilobytes (KB), después del cual el cliente detiene la recopilación de los archivos especificados.  

    > [!NOTE]  
    > El servidor de sitio recopila las cinco versiones cambiadas recientemente de los archivos recopilados y las almacena en el directorio `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol`. Si un archivo no ha cambiado desde el último ciclo de inventario de software, el archivo no se volverá recopilar.  
    >
    > El inventario de software no recopila archivos con un tamaño superior a 20 MB.  
    >
    > El valor **Tamaño máximo para todos los archivos recopilados (KB)** del cuadro de diálogo **Configurar valor de cliente** muestra el tamaño máximo de todos los archivos recopilados. Cuando se alcanza este tamaño, se detiene la recopilación de archivos. Los archivos que ya se han recopilado se conservan y se envían al servidor de sitio.  

    > [!IMPORTANT]
    > Si configura el inventario de software para recopilar muchos archivos de gran tamaño, es posible que esta configuración afecte de forma negativa al rendimiento de la red y el servidor de sitio.  

    Para obtener información sobre cómo ver los archivos recopilados, vea [Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades del archivo recopilado**. Agregue todos los archivos que quiera recopilar y, después, seleccione **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente**.  

### <a name="set-names"></a>Establecer nombres

El agente de inventario de software recupera los nombres de fabricante y producto de la información del encabezado de archivo. Estos nombres no siempre están estandarizados en la información del encabezado de archivo. Al ver el inventario de software en el Explorador de recursos, pueden aparecer versiones diferentes del mismo nombre de fabricante o producto. Para estandarizar estos nombres para mostrar, seleccione **Establecer nombres** y, después, configure las opciones siguientes:  

- **Tipo de nombre**: El inventario de software recopila información acerca de los fabricantes y los productos. Seleccione si quiere configurar los nombres para mostrar de un **Fabricante** o un **Producto**.  

- **Nombre para mostrar**: especifica el nombre para mostrar que quiere usar en lugar de los nombres de la lista **Nombres inventariados**. Seleccione **Nuevo** para especificar un nuevo nombre para mostrar.  

- **Nombres inventariados**: seleccione **Nuevo** para agregar un nombre inventariado. Este nombre se sustituye en el inventario de software por el nombre seleccionado en la lista **Nombre para mostrar**. Puede agregar varios nombres para reemplazar.  



## <a name="software-metering"></a>Medición de software

### <a name="enable-software-metering-on-clients"></a>Habilitar disponibilidad de software en clientes

De forma predeterminada, esta opción está establecida en **Sí**. Para obtener más información, vea [Medición de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Programar recopilación de datos

Seleccione **Programación** para ajustar la frecuencia con la que los clientes ejecutan el ciclo de medición de software. De forma predeterminada, este ciclo tiene lugar cada siete días.



## <a name="software-updates"></a>Actualizaciones de software  

### <a name="enable-software-updates-on-clients"></a>Habilitar actualizaciones de software en clientes

Use esta opción para habilitar las actualizaciones de software en los clientes de Configuration Manager. Si deshabilita esta opción, Configuration Manager quitará del cliente las directivas de implementación existentes. Cuando vuelva a activar esta opción, el cliente descarga la directiva de implementación actual.  

> [!IMPORTANT]  
> Cuando se deshabilita esta configuración, las directivas de cumplimiento que se basan en las actualizaciones de software dejan de funcionar.  

### <a name="software-update-scan-schedule"></a>Programación de exploración de actualización de software

Seleccione **Programación** para especificar la frecuencia con la que el cliente inicia un análisis de evaluación del cumplimiento. Este análisis determina el estado de las actualizaciones de software en el cliente (por ejemplo, requerida o instalada). Para obtener más información sobre la evaluación de cumplimiento, consulte [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (Evaluación del cumplimiento de las actualizaciones de software).  

De forma predeterminada, en este análisis se usa una programación simple para iniciar cada siete días. Puede crear una programación personalizada. Puede especificar un día y hora de inicio exactos, usar el Horario universal coordinado (UTC) o la hora local, y configurar el intervalo de repetición en un determinado día de la semana.  

> [!NOTE]  
> Si especifica un intervalo de menos de un día, Configuration Manager lo establece automáticamente de forma predeterminada en un día.  

> [!WARNING]  
> La hora de inicio en los equipos cliente es la hora de inicio más una cantidad de tiempo aleatoria de hasta dos horas. Esta cantidad aleatoria evita que los equipos cliente inicien el análisis y al mismo tiempo se conecten al punto de actualización de software activo.  

### <a name="schedule-deployment-re-evaluation"></a>Programar reevaluación de implementación

Seleccione **Programación** para configurar la frecuencia con que el agente cliente de actualizaciones de software vuelve a evaluar el estado de la instalación de actualizaciones de software en equipos cliente de Configuration Manager. Cuando las actualizaciones de software instaladas previamente ya no se encuentran en los clientes pero siguen siendo necesarias, el cliente vuelve a instalar las actualizaciones de software.

Ajuste esta programación según la directiva de la empresa para el cumplimiento de actualización de software y si los usuarios pueden desinstalar las actualizaciones de software. Cada ciclo de reevaluación de implementación comporta actividad del procesador del equipo cliente y la red. De forma predeterminada, esta configuración usa una programación simple para iniciar el análisis de reevaluación de implementación cada siete días.  

> [!NOTE]  
> Si especifica un intervalo de menos de un día, Configuration Manager lo establece automáticamente de forma predeterminada en un día.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Cuando se alcance una fecha límite de implementación de actualización de software, instale todas las demás implementaciones de actualización de software cuya fecha límite tenga lugar dentro de un período de tiempo específico.

Establezca esta opción en **Sí** para instalar todas las actualizaciones de software de las implementaciones necesarias con fechas límite que se producen en un período de tiempo especificado. Cuando una implementación de actualización de software requerida alcanza una fecha límite, el cliente inicia la instalación de las actualizaciones de software en la implementación. Esta configuración determina si se deben instalar las actualizaciones de software desde otras implementaciones necesarias que tienen una fecha límite en el tiempo especificado.  

Use esta opción para acelerar la instalación de actualizaciones de software necesarias. Esta configuración también tiene la posibilidad de aumentar la seguridad de cliente, reducir las notificaciones al usuario y minimizar los reinicios del cliente. De forma predeterminada, esta opción está establecida en **No**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Período de tiempo durante el cual también se instalarán todas las implementaciones pendientes cuya fecha límite sea durante este período

Use esta opción para especificar el período de tiempo para la configuración anterior. Puede especificar un valor entre 1 y 23 horas y entre 1 y 365 días. De forma predeterminada, esta opción se configura con un valor de siete días.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Permitir que los clientes descarguen contenido diferencial cuando esté disponible

*(Se introdujo en la versión 1902)*

Establezca esta opción en **Sí** para permitir que los clientes usen archivos de contenido diferencial. Esta configuración permite al Agente de Windows Update del dispositivo determinar qué contenido se necesita y descargarlo de forma selectiva. 

- Antes de habilitar esta configuración de cliente, asegúrese de que Optimización de distribución está configurada correctamente en el entorno. Para obtener más información, vea [Optimización de distribución de Windows](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) y [Configuración de cliente de Optimización de distribución](#delivery-optimization).
 - Esta configuración de cliente reemplaza a **Habilitar instalación de archivos de instalación Express en clientes**. Establezca esta opción en **Sí** para permitir que los clientes usen archivos de instalación rápida. Para obtener más información, consulte [Administración de archivos de instalación rápida para actualizaciones de Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - A partir de la versión 1910 de Configuration Manager, cuando esta opción se establece, se usa la descarga delta con todos los archivos de instalación de Windows Update, no solo con los archivos de instalación rápida.
    - Cuando se usa CMG para el almacenamiento de contenido, el contenido de las actualizaciones de terceros no se descarga en los clientes si está habilitada la opción de cliente **Descarga de contenido diferencial cuando esté disponible**. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Puerto que los clientes usan para recibir solicitudes para el contenido diferencial

*(Se introdujo en la versión 1902)*

Esta opción configura el puerto local para el que agente de escucha HTTP descargue contenido diferencial. De forma predeterminada, se establece en 8005. No es necesario abrir este puerto en el firewall del cliente. 

> [!NOTE]
>Esta configuración de cliente reemplaza a **Puerto usado para descargar contenido para archivos de instalación Express**.


### <a name="enable-management-of-the-office-365-client-agent"></a>Habilitar administración del Agente cliente de Office 365

Cuando esta opción se establece en **Sí**, se habilita la configuración de opciones de instalación de Office 365. También permite descargar archivos desde redes de Content Delivery Network (CDN) de Office e implementar los archivos como una aplicación en Configuration Manager. Para más información, vea [Administración de Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a> Habilitar la instalación de actualizaciones de software en la ventana de mantenimiento "Todas las implementaciones" cuando esté disponible la ventana de mantenimiento "Actualización de software"

Al establecer esta opción en **Sí** y si el cliente tiene al menos una ventana de mantenimiento "Actualización de Software" definida, las actualizaciones de software se instalarán durante una ventana de mantenimiento "Todas las implementaciones".

De forma predeterminada, esta opción está establecida en **No**. Este valor usa el mismo comportamiento que antes: si ambos tipos existen, se omite la ventana. <!--2839307-->

> [!NOTE]
> Esta opción también es válida en las ventanas de mantenimiento que se configuren para aplicarse a **secuencias de tareas**.<!-- SCCMDocs-pr #4596 -->
>
> Si el cliente solo tiene una ventana **Todas las implementaciones** disponible, sigue instalando las actualizaciones de software o las secuencias de tareas en esa ventana.

#### <a name="maintenance-window-example"></a>Ejemplo de ventana de mantenimiento

Imaginemos que configura las siguientes ventanas de mantenimiento:

- **Toda la implementación**: 02:00-04:00
- **Actualizaciones de software**: 04:00-06:00

De forma predeterminada, el cliente solo instalará actualizaciones de software durante la segunda ventana de mantenimiento. Omite la ventana de mantenimiento para todas las implementaciones de este escenario. Cuando esta configuración se cambia a **Sí**, el cliente instala actualizaciones de software entre 02:00-06:00.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a> Especificación de la prioridad de subproceso para las actualizaciones de características

<!--3734525-->
A partir de la versión 1902 de Configuration Manager, puede ajustar la prioridad con la que los clientes de Windows 10 versión 1709 o posterior instalan una actualización de características mediante el [mantenimiento de Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). Esta opción no influye en las secuencias de tareas de actualización en contexto de Windows 10.

Esta nueva configuración de cliente proporciona estas opciones:

- **No configurado**: Configuration Manager no cambia la configuración. Los administradores pueden preconfigurar su propio archivo setupconfig.ini. Este valor es el predeterminado.

- **Normal**: el programa de instalación de Windows usa más recursos del sistema y se actualiza con más rapidez. Usa más tiempo del procesador, por lo que el tiempo total de instalación es más corto, pero la interrupción del usuario es más larga.  

    - Configura el archivo setupconfig.ini en el dispositivo con la [opción de línea de comandos de instalación de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) de `/Priority Normal`.

- **Bajo**: puede seguir trabajando en el dispositivo mientras se descarga y se actualiza en segundo plano. El tiempo de instalación total es superior, pero la interrupción del usuario es más corta. Es posible que necesite aumentar el tiempo máximo de ejecución de la actualización para evitar el agotamiento del tiempo de espera cuando use esta opción.  

    - Quita la [opción de línea de comandos de instalación de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) de `/Priority` desde el archivo setupconfig.ini.


### <a name="enable-third-party-software-updates"></a>Habilitar actualizaciones de software de terceros

Cuando esta opción se configura como **Sí**, se establece la directiva para **permitir actualizaciones firmadas para una ubicación del servicio Microsoft Update en la intranet** y se instala el certificado de firma en el almacén de editores de confianza en el cliente.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Habilitación de la actualización dinámica de las actualizaciones de características
<!--4062619-->
A partir de la versión 1906 de Configuration Manager, puede configurar la [actualización dinámica de Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847). La actualización dinámica instala paquetes de idioma, características a petición, controladores y actualizaciones acumulativas durante la instalación de Windows al dirigir al cliente a descargar estas actualizaciones de Internet. Cuando esta configuración se establece en **Sí** o en **No**, Configuration Manager modifica el archivo [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) que se usa durante la instalación de la actualización de las características.

- **No configurado**: el valor predeterminado. No se realiza ningún cambio en el archivo setupconfig.
  - La actualización dinámica está habilitada de manera predeterminada en todas las versiones compatibles de Windows 10.
    - En las versiones 1803 y anteriores de Windows 10, la actualización dinámica revisa si en el servidor WSUS del dispositivo hay actualizaciones dinámicas aprobadas. En entornos de Configuration Manager, las actualizaciones dinámicas nunca se aprueban directamente en el servidor WSUS, por lo que estos dispositivos no las instalan.
    - A partir de la versión 1809 de Windows 10, la actualización dinámica usa la conexión a Internet del dispositivo para obtener actualizaciones dinámicas desde Microsoft Update. Estas actualizaciones dinámicas no se publican para el uso de WSUS.
- **Sí**: habilita la actualización dinámica.
- **No**: deshabilita la actualización dinámica.


## <a name="state-messaging"></a>Mensajes de estado

### <a name="state-message-reporting-cycle-minutes"></a>Ciclo de notificación de mensaje de estado (minutos)

Especifica la frecuencia con la que los clientes notifican mensajes de estado. De forma predeterminada esta configuración es de 15 minutos.



## <a name="user-and-device-affinity"></a>Afinidad entre usuario y dispositivo  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Umbral de uso de afinidad de dispositivo de usuario (minutos)

Especifique el número de minutos antes de que Configuration Manager cree una asignación de afinidad de dispositivo de usuario. De forma predeterminada, este valor es de 2880 minutos (dos días).

### <a name="user-device-affinity-usage-threshold-days"></a>Umbral de uso de afinidad de dispositivo de usuario (días)

Especifique el número de días durante los que el cliente mide el umbral de afinidad de dispositivo basado en uso. De forma predeterminada, este valor es de 30 días.

> [!NOTE]  
> Por ejemplo, se puede especificar **Umbral de uso de afinidad de dispositivo de usuario (minutos)** como **60** minutos y **Umbral de uso de afinidad de dispositivo de usuario (días)** como **5** días. Después, el usuario debe utilizar el dispositivo durante 60 minutos durante un período de 5 días para crear afinidad automática con el dispositivo.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario

Seleccione **Sí** para crear afinidad de dispositivo automático de usuarios en función de la información de uso que recopila Configuration Manager.  

### <a name="allow-user-to-define-their-primary-devices"></a>Permitir al usuario definir sus dispositivos primarios
<!--3485366-->
Si este valor es **Sí**, los usuarios pueden identificar sus propios dispositivos primarios en el Centro de software. Para más información, consulte el [Manual del usuario del Centro de software](../../understand/software-center.md#work-information).

## <a name="windows-analytics"></a>Windows Analytics

> [!Important]  
> El servicio Windows Analytics se retiró el 31 de enero de 2020. Para más información, consulte [KB 4521815: Windows Analytics se retirará el 31 de enero de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Análisis de escritorio es la evolución de Windows Analytics. Vea [¿Qué es Análisis de escritorio?](../../../desktop-analytics/overview.md) para obtener más información.
