---
title: Funcionalidades de Technical Preview 1609
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1609.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 51a974247d7281d6134b699a5865f801d1ed6094
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905703"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Funciones de Technical Preview 1609 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*



En este artículo se presentan las características disponibles en la versión 1609 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    

**Problemas conocidos de esta Technical Preview:**  
*  Cuando se actualiza a la Technical Preview 1609 de Configuration Manager, se eliminan todas las directivas de actualización de edición que hubiera implementado. Para seguir usando estas directivas, debe volver a crearlas e implementarlas.


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="improvements-to-endpoint-protection"></a>Mejoras de Endpoint Protection
Mejora en la configuración de directivas antimalware de Endpoint Protection: ahora puede especificar el nivel en el que Endpoint Protection Cloud Protection Service bloqueará los archivos sospechosos. Una nueva opción permite a los administradores especificar equipos "peligrosos" en función de la cantidad de malware que detecten.

## <a name="increased-number-of-enrolled-devices"></a>Mayor número de dispositivos inscritos
Los administradores ahora pueden permitir a los usuarios inscribir hasta 15 dispositivos en la administración híbrida de dispositivos móviles con Intune. Anteriormente el límite era de cinco dispositivos por usuario.

## <a name="additional-apple-dep-settings"></a>Opciones adicionales del DEP de Apple

Ahora, los administradores pueden configurar las siguientes opciones del programa de inscripción de dispositivos (DEP) de Apple en el perfil del DEP para dispositivos iOS y Mac:
- **Touch ID**
- **Zoom**
- **Siri**

Si está habilitado, el Asistente para la instalación de Apple solicita este servicio durante la activación del dispositivo.

## <a name="integration-with-upgrade-analytics"></a>Integración con Upgrade Analytics

Upgrade Analytics permite evaluar y analizar la preparación del dispositivo y la compatibilidad con Windows 10 para permitir unas actualizaciones más sencillas y con menos problemas. Con la integración de Upgrade Analytics y Configuration Manager, puede acceder a los datos de compatibilidad de actualización en la consola de administración de Configuration Manager y luego, en la lista de dispositivos, elegir dispositivos para actualización o corrección.


## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Tipos de conexión nativos para perfiles híbridos de VPN de Windows 10

Ahora, cuando use Configuration Manager con Intune, puede crear perfiles de VPN de Windows 10 con tipos de conexión Microsoft Automatic, IKEv2, PPTP y L2TP en la consola de Configuration Manager sin usar OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Mejoras en la integración de la Tienda Windows para empresas con Configuration Manager

En esta versión, se ha actualizado la [integración de la Tienda Windows para empresas](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) con estas nuevas características:

**Actualización:** en la versión actual de Technical Preview, la característica de sincronización inmediata no es funcional.

- Anteriormente, solo se podían implementar aplicaciones gratuitas de la Tienda Windows para empresas. Configuration Manager ahora además admite la implementación de aplicaciones con licencia en línea de pago (solo para dispositivos inscritos en Intune).
- Ahora puede iniciar una sincronización inmediata entre la Tienda Windows para empresas y Configuration Manager.
- Ahora puede modificar la clave secreta de cliente que ha obtenido de Azure Active Directory.

### <a name="try-it-out"></a>Haga la prueba

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Adquirir y sincronizar una aplicación con licencia en línea de pago

1. Adquiera una aplicación con licencia en línea de pago de la Tienda Windows para empresas.
2. En el área de trabajo **Administración** de la consola de Configuration Manager, haga clic en **Servicios de nube** > **Actualizaciones y mantenimiento** > **Tienda Windows para empresas**.
3. En la pestaña **Inicio**, en el grupo **Sincronizar**, haga clic en **Sincronizar**.
4. Poco después la aplicación adquirida aparecerá en el nodo **Información de licencia para las aplicaciones de la Tienda** del área de trabajo **Administración de aplicaciones**.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Crear e implementar una aplicación de Configuration Manager a partir de los datos de aplicación sincronizados

El procedimiento para crear e implementar una aplicación de Configuration Manager a partir de una aplicación de pago de la tienda es el mismo que para crear una aplicación a partir de otra gratuita. Vea la sección **Crear e implementar una aplicación de Configuration Manager a partir de una aplicación de la Tienda Windows para empresas** de [Administrar aplicaciones de la Tienda Windows para empresas con Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modificar la clave secreta de cliente de Azure Active Directory

1. En el área de trabajo **Administración** de la consola de Configuration Manager, haga clic en **Servicios de nube** > **Actualizaciones y mantenimiento** > **Tienda Windows para empresas**.
2. Seleccione la cuenta de la Tienda Windows para empresas y haga clic en **Propiedades**.
3. En el cuadro de diálogo **Propiedades de la cuenta de la Tienda Windows para empresas**, escriba una nueva clave en el campo **Clave secreta de cliente** y haga clic en **Comprobar**. Una vez comprobada, haga clic en **Aplicar** y cierre el cuadro de diálogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Nueva configuración de cumplimiento para elementos de configuración

Se han agregado muchas opciones nuevas que se pueden usar en los elementos de configuración de varias plataformas de dispositivo.
Son opciones que existían con anterioridad en Microsoft Intune en una configuración independiente y que ahora están disponibles al usar Intune con Configuration Manager.
Si necesita ayuda con cualquiera de estas opciones, abra [Administrar la configuración y las características de los dispositivos con directivas de Microsoft Intune](/mem/intune/configuration/device-profiles) y luego seleccione el subtema de configuración de la plataforma que quiera.


### <a name="new-settings-for-android-devices"></a>Nuevas opciones para dispositivos Android

#### <a name="password-settings"></a>Configuración de contraseña

- **Recordar el historial de contraseñas**
- **Permitir desbloqueo mediante huellas digitales**

#### <a name="security-settings"></a>Configuración de seguridad

- **Requerir cifrado en tarjetas de almacenamiento**
- **Permitir captura de pantalla**
- **Permitir el envío de datos de diagnóstico**

#### <a name="browser-settings"></a>Configuración del explorador

- **Permitir explorador web**
- **Permitir autorrelleno**
- **Permitir bloqueador de elementos emergentes**
- **Permitir cookies**
- **Permitir Active scripting**

#### <a name="app-settings"></a>Configuración de aplicaciones

- **Permitir Google Play Store**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos

- **Permitir almacenamiento extraíble**
- **Permitir tethering Wi-Fi**
- **Permitir geolocalización**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir itinerancia de voz**
- **Permitir itinerancia de datos**
- **Permitir mensajería SMS/MMS**
- **Permitir asistente de voz**
- **Permitir marcación por voz**
- **Permitir copiar y pegar**


### <a name="new-settings-for-ios-devices"></a>Nuevas opciones para dispositivos iOS

#### <a name="password-settings"></a>Configuración de contraseña

- **Número de caracteres complejos necesarios en la contraseña**
- **Permitir contraseñas sencillas**
- **Minutos de inactividad antes de que se requiera la contraseña**
- **Recordar el historial de contraseñas**

### <a name="new-settings-for-mac-os-x-devices"></a>Nuevas opciones para dispositivos Mac OS X

#### <a name="password-settings"></a>Configuración de contraseña

- **Número de caracteres complejos necesarios en la contraseña**
- **Permitir contraseñas sencillas**
- **Recordar el historial de contraseñas**
- **Minutos de inactividad antes de que se active el protector de pantalla**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nuevas opciones para dispositivos Windows 10 Escritorio y Mobile

#### <a name="password-settings"></a>Configuración de contraseña

- **Número mínimo de conjuntos de caracteres**
- **Recordar el historial de contraseñas**
- **Requerir una contraseña cuando el dispositivo vuelva de un estado de inactividad**

#### <a name="security-settings"></a>Configuración de seguridad

- **Requerir cifrado en el dispositivo móvil**
- **Permitir cancelar suscripción manualmente**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos

- **Permitir VPN sobre móvil**
- **Permitir itinerancia de VPN sobre móvil**
- **Permitir restablecer teléfono**
- **Permitir conexión USB**
- **Permitir a Cortana**
- **Permitir notificaciones del centro de actividades**

### <a name="new-settings-for-windows-10-team-devices"></a>Nuevas opciones para dispositivos Windows 10 Team

#### <a name="device-settings"></a>Configuración del dispositivo

- **Habilitar Visión operativa de Azure**
- **Habilitar proyección inalámbrica de Miracast**
- **Seleccione la información sobre la reunión que se muestra en la pantalla de inicio de sesión**
- **URL de imagen de fondo de pantalla de bloqueo**


### <a name="new-settings-for-windows-81-devices"></a>Nuevas opciones para dispositivos Windows 8.1

#### <a name="applicability-settings"></a>Configuración de la aplicación

- **Aplicar todas las configuraciones a Windows 10**

#### <a name="password-settings"></a>Configuración de contraseña

- **Tipo de contraseña requerida**
- **Número mínimo de conjuntos de caracteres**
- **Longitud mínima de la contraseña**
- **Número de errores de inicio de sesión consecutivos permitidos antes de que se borre el dispositivo**
- **Minutos de inactividad antes de que se apague la pantalla**
- **Expiración de la contraseña (días)**
- **Recordar el historial de contraseñas**
- **Impedir la reutilización de contraseñas anteriores**
- **Permitir contraseña de imagen y PIN**

#### <a name="browser-settings"></a>Configuración del explorador

- **Permitir la detección automática de redes de intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Nuevas opciones para dispositivos Windows Phone 8.1

#### <a name="applicability-settings"></a>Configuración de la aplicación

- **Aplicar todas las configuraciones a Windows 10**

#### <a name="password-settings"></a>Configuración de contraseña

- **Número mínimo de conjuntos de caracteres**
- **Permitir contraseñas sencillas**
- **Recordar el historial de contraseñas**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos

- **Permitir conexión automática a zonas Wi-Fi gratuitas**


## <a name="improvements-for-boundary-groups"></a>Mejoras en los grupos de límites
Esta vista previa presenta cambios importantes en los grupos de límites y en su funcionamiento con los puntos de distribución. Estos cambios ayudarán a simplificar el diseño de la infraestructura de contenido y le proporcionarán más control sobre cómo y cuándo usan la reserva los clientes para buscar puntos de distribución adicionales como ubicaciones de origen de contenido. Esto incluye tanto puntos de distribución locales como basados en la nube.

Estas mejoras reemplazan conceptos y comportamientos con los que puede que esté familiarizado (como la configuración de puntos de distribución como rápidos o lentos) por un nuevo modelo que debería ser más fácil de configurar y mantener. Estos cambios también constituyen la base para futuros cambios que mejorarán otros roles de sistema de sitio que asocia a los grupos de límites.  

Durante la actualización a 1609, las configuraciones de los grupos de límites actuales se convierten para ajustarse al nuevo modelo, de modo que estos cambios no afecten a las configuraciones de distribución de contenido (vea [Actualizar grupos de límites existentes al nuevo modelo](capabilities-in-technical-preview-1609.md#bkmk_update)).

En las secciones siguientes se detallan los cambios presentados en esta vista previa, cómo funciona el modelo nuevo y lo que puede esperar al actualizar un sitio que ya tiene grupos de límites configurados.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Cambios en la interfaz de usuario y comportamiento de los grupos de límites y las ubicaciones de contenido
Estos son los principales cambios realizados en los grupos de límites y en la forma en que los clientes buscan contenido. Muchos de estos conceptos y cambios funcionan conjuntamente.
- **Se quitan las configuraciones de Rápido o Lento:** Ya no se configuran los puntos de distribución individuales para que sean rápidos o lentos.  En su lugar, se trata igual cada sistema de sitio asociado a un grupo de límites. Debido a este cambio, la pestaña **Referencias** de las propiedades del grupo de límites ya no admite la configuración de Rápido o Lento.
- **Nuevo grupo de límites predeterminado en cada sitio:**  Cada sitio primario tiene un nuevo grupo de límites predeterminado denominado ***Default-Site-Boundary-Group\<sitecode>***.  Cuando un cliente no esté en una ubicación de red asignada a un grupo de límites, ese cliente usará los sistemas de sitio asociados con el grupo predeterminado de su sitio asignado. Este grupo de límites se puede considerar un sustituto del concepto de ubicación de contenido de reserva.    
  -  Se ha eliminado **"Permitir a los clientes usar una ubicación de origen de reserva para el contenido"** : ya no se configuran puntos de distribución de forma explícita para usarse como reserva y las opciones para hacerlo se han quitado de la interfaz de usuario.

  Además, el resultado de establecer **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** en un tipo de implementación para aplicaciones ha cambiado. Esta opción en un tipo de implementación ahora permite a un cliente usar el grupo de límites de sitio predeterminado como una ubicación de origen de contenido.

  -  **Relaciones de grupos de límites:** cada grupo de límites se puede vincular a uno o varios grupos de límites adicionales. Estos vínculos forman relaciones que se configuran en la nueva pestaña de propiedades de grupos de límites denominada **Relaciones**:
  -   Cada grupo de límites asociado directamente a un cliente se denomina grupo de límites **actual**.  
  -   Cualquier grupo de límites que un cliente pueda usar debido a una asociación entre el grupo de límites *actual* de ese cliente y otro grupo se denomina grupo de límites **vecino**.
  -  Es en la pestaña **Relaciones** donde se agregan los grupos de límites que se pueden usar como grupos de límites *vecinos*. También puede configurar un tiempo en minutos que determine cuándo empezará un cliente que no pueda encontrar contenido de un punto de distribución del grupo *actual* a buscar ubicaciones de contenido de esos grupos de límites *vecinos*.

      Al agregar o cambiar la configuración de un grupo de límites, tendrá la opción de bloquear la reserva de ese grupo de límites concreto desde el grupo actual que está configurando.

  Para usar la nueva configuración, defina asociaciones explícitas (vínculos) de un grupo de límites con otro y configure todos los puntos de distribución de ese grupo asociado con el mismo tiempo en minutos. El tiempo que configure determina si un cliente que no encuentra un origen de contenido de su grupo de límites *actual* puede empezar a buscar orígenes de contenido en ese grupo de límites vecino.

  Además de los grupos de límites que se configuran explícitamente, cada grupo de límites tiene un vínculo implícito al grupo de límites de sitio predeterminado. Este vínculo se activa después de 120 minutos, momento en que el grupo de límites de sitio predeterminado se convierte en un grupo de límites vecino que permite a los clientes usar los puntos de distribución asociados a ese grupo de límites como ubicaciones de origen de contenido.

  Este comportamiento reemplaza a lo que anteriormente se conocía como reserva de contenido.  Puede anular este comportamiento predeterminado de 120 minutos si asocia explícitamente el grupo de límites de sitio predeterminado a un grupo *actual* y establece un tiempo concreto en minutos o bloquea la reserva completamente para evitar su uso.


- **Los clientes intentan obtener contenido de cada punto de distribución hasta un máximo de dos minutos:** cuando un cliente busca una ubicación de origen de contenido, intenta acceder a cada punto de distribución durante dos minutos antes de intentarlo con otro punto de distribución. Esto supone un cambio con respecto a las versiones anteriores, donde los clientes intentaban conectarse a un punto de distribución hasta un máximo de dos horas.

  - El primer punto de distribución que un cliente intenta usar se selecciona aleatoriamente en el grupo de puntos de distribución disponibles del grupo (o grupos) de límites *actual* del cliente.

  - Después de dos minutos, si el cliente no ha encontrado el contenido, cambia a un nuevo punto de distribución e intenta obtener contenido de ese servidor. Este proceso se repite cada dos minutos hasta que el cliente encuentra el contenido o alcanza el último servidor de su grupo.

  - Si un cliente no puede encontrar una ubicación de origen de contenido válida de su grupo *actual* antes de que se alcance la reserva de un grupo de límites *vecino*, el cliente agrega los puntos de distribución de ese grupo *vecino* al final de su lista actual y luego busca en el grupo ampliado de ubicaciones de origen que incluye los puntos de distribución de ambos grupos de límites.

      > [!TIP]  
      > Al crear un vínculo explícito entre el grupo de límites actual y el grupo de límites de sitio predeterminado y definir un tiempo de reserva menor que el tiempo de reserva de un vínculo a un grupo de límites vecino, los clientes empiezan a buscar ubicaciones de origen en el grupo de límites de sitio predeterminado antes de incluir el grupo vecino.

  - Cuando el cliente no puede obtener contenido del último servidor del grupo, el proceso comienza de nuevo.


### <a name="how-the-new-model-works"></a>Funcionamiento del nuevo modelo
Al configurar grupos de límites, se asocian límites (ubicaciones de red) y roles de sistema de sitio, como los puntos de distribución, al grupo de límites. Esto ayuda a vincular clientes a servidores de sistema de sitio como puntos de distribución ubicados cerca de los clientes en la red.   
- Puede asignar el mismo límite a varios grupos de límites.
- Los servidores de sistema de sitio, como los puntos de distribución, pueden asociarse a varios grupos de límites, lo que los pone a disposición de una gama más amplia de ubicaciones de red.
- Si un punto de distribución no está asociado a un grupo de límites, los clientes no podrán usar ese punto de distribución como ubicación de origen de contenido.

A partir de esta Technical Preview, se definen relaciones de grupos de límites para configurar el comportamiento de reserva de las ubicaciones de origen de contenido. Este nuevo comportamiento se configura en la pestaña **Relaciones** de las propiedades del grupo de límites y reemplaza a la configuración de los sistemas de sitio como lentos o rápidos y a la configuración de un grupo de límites para permitir la ubicación de origen de reserva para el contenido.

En la pestaña Relaciones se agregan otros grupos de límites para configurar una relación con esos grupos. Cada relación es un vínculo unidireccional desde el grupo de límites **actual** al grupo de límites que se agrega, que se denomina **vecino**. Se pueden configurar puntos de distribución con un tiempo de reserva en minutos para cada vínculo que se crea. Este tiempo se usa para determinar después de cuánto tiempo los clientes del grupo de límites *actual* pueden empezar a usar puntos de distribución del grupo de límites *vecino* si no pueden encontrar una ubicación de origen de contenido válida en su actual grupo de límites.

Cuando un cliente no encuentra el contenido y empieza a buscar en ubicaciones de grupos de límites vecinos, se incrementa el grupo de puntos de distribución disponibles para ese cliente de una manera controlada.  

- Un grupo de límites puede tener más de una relación. Esto permite configurar la reserva de los distintos vecinos para que se produzca después de períodos de tiempo diferentes.
- Los clientes solo usarán como reserva un grupo de límites que sea vecino directo de su actual grupo de límites.
- Cuando un cliente es miembro de varios grupos de límites, el grupo de límites actual se define como una unión de todos los grupos de límites de ese cliente.  Ese cliente puede usar como reserva un vecino de cualquiera de esos grupos de límites originales.

Además de los vínculos que se definen, hay un vínculo implícito que se crea automáticamente entre los grupos de límites que se crean y el grupo de límites predeterminado que se crea automáticamente para cada sitio. Este vínculo automático:
- es usado por los clientes que no se encuentran en un límite asociado a algún grupo de límites de la jerarquía que use automáticamente el grupo de límites predeterminado de su sitio asignado para identificar ubicaciones de origen de contenido válidas;   
-  es una opción de reserva predeterminada del grupo de límites actual al grupo de límites de sitio predeterminado que se usa después de 120 minutos.

**Ejemplo de uso del nuevo modelo:** Cree tres grupos de límites que no compartan los límites ni los servidores de sistema de sitio:
- Grupo BG_A con puntos de distribución DP_A1 y DP_A2 asociados al grupo
- Grupo BG_B con puntos de distribución DP_B1 y DP_B2 asociados al grupo
- Grupo BG_C con puntos de distribución DP_C1 y DP_C2 asociados al grupo

Agregue las ubicaciones de red de los clientes como límites para el grupo de límites BG_A y luego configure relaciones desde ese grupo de límites con los otros dos grupos de límites:
- Configure los puntos de distribución para usar el primer grupo *vecino* (BG_B) después de 10 minutos. Este grupo contiene los puntos de distribución DP_B1 y DP_B2. Ambos están bien conectados a las primeras ubicaciones de límite de grupos.
- Configure el segundo grupo *vecino* (BG_C) para usarse después de 20 minutos. Este grupo contiene los puntos de distribución DP_C1 y DP_C2. Ambos están separados por WAN de los otros dos grupos de límites.
- Agregue también un punto de distribución adicional que se encuentre en el servidor de sitio al grupo de límites de sitio predeterminado de los sitios. Se trata de la ubicación de origen de contenido menos preferida, pero tiene una ubicación central con respecto a todos los grupos de límites.

  Ejemplo de grupos de límites y tiempos de reserva:

  ![BG_Fallack](media/BG_Fallback.png)


Con esta configuración:
- El cliente empieza a buscar contenido en los puntos de distribución de su grupo de límites *actual* (BG_A), buscando en cada punto de distribución durante dos minutos antes de pasar al siguiente punto de distribución del grupo de límites. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1 y DP_A2.
- Si el cliente no puede encontrar contenido en su grupo de límites *actual* después de buscar durante 10 minutos, agrega los puntos de distribución del grupo de límites BG_B a su búsqueda. Luego continúa buscando contenido en un punto de distribución de su grupo combinado de puntos de distribución que ahora incluye los de los grupos de límites BG_A y BG_B. El cliente sigue poniéndose en contacto con cada punto de distribución durante dos minutos antes de pasar al siguiente punto de distribución de su grupo. El grupo de clientes de ubicaciones de origen de contenido válidas incluye DP_A1, DP_A2, DP_B1 y DP_B2.
- Después de otros 10 minutos (un total de 20 minutos), si el cliente aún no ha encontrado un punto de distribución con contenido, amplía su grupo de puntos de distribución disponibles para incluir los del segundo grupo *vecino*, el grupo de límites BG_C. El cliente ahora tiene seis puntos de distribución para la búsqueda (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 y DP_C2) y sigue pasando a un nuevo punto de distribución cada dos minutos hasta que encuentra contenido.
- Si el cliente no ha encontrado contenido después de un total de 120 minutos, usa la reserva para incluir el *grupo de límites de sitio predeterminado* como parte de su búsqueda continuada. Ahora el grupo de puntos de distribución incluye todos los puntos de distribución de los tres grupos de límites configurados y el punto de distribución final ubicado en el equipo de servidor de sitio.  El cliente sigue buscando contenido, cambiando de punto de distribución cada dos minutos hasta que encuentra contenido.

Mediante la configuración de los distintos grupos vecinos para que estén disponibles en momentos diferentes, se controla cuándo se agregan puntos de distribución concretos como ubicación de origen de contenido y cuándo, o si, el cliente usa la reserva del grupo de límites de sitio predeterminado como una red de seguridad para el contenido que no está disponible desde cualquier otra ubicación.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a> Actualizar grupos de límites existentes al nuevo modelo
Al instalar la versión 1609 y actualizar el sitio, se realizan automáticamente las siguientes configuraciones. Su objetivo es garantizar que el comportamiento de reserva actual siga estando disponible hasta que configure nuevos grupos de límites y relaciones.  
- Se agregan puntos de distribución sin proteger en un sitio al grupo de límites*Default-Site-Boundary-Group\<sitecode&gt;* de ese sitio.
- Se realiza una copia de cada grupo de límites existente que incluye un servidor de sitio configurado con una conexión lenta. El nombre del nuevo grupo es ***\<nombre original del grupo de límites>-Slow-Tmp***:  
  -   Los sistemas de sitio con una conexión rápida se dejan en el grupo de límites original.
  -   Se agrega una copia de los sistemas de sitio con una conexión lenta a la copia del grupo de límites. Los sistemas de sitio originales configurados como lentos permanecen en el grupo de límites original por razones de compatibilidad, pero no se usan desde ese grupo de límites.
  -   Esta copia del grupo de límites no tiene límites asociados, pero se crea un vínculo de reserva entre el grupo original y la nueva copia del grupo de límites con un tiempo de reserva establecido en cero.

  En la siguiente tabla se identifica el nuevo comportamiento de reserva que se puede esperar de la combinación de las configuraciones de implementación originales y las configuraciones de los puntos de distribución:

Configuración de implementación original "No ejecutar programa" de la red lenta  |Configuración de punto de distribución original "Permitir a los clientes usar una ubicación de origen de reserva para el contenido"  |Nuevo comportamiento de reserva  
---------|---------|---------
Seleccionado     |  Seleccionado    |  **Sin reserva**: se usan solo los puntos de distribución del grupo de límites actual       
Seleccionado     |  No seleccionado|  **Sin reserva**: se usan solo los puntos de distribución del grupo de límites actual       
No seleccionado |  No seleccionado|  **Reserva a vecino**: se usan los puntos de distribución del grupo de límites actual y luego se agregan los puntos de distribución del grupo de límites vecino. A menos que se configure un vínculo explícito al grupo de límites de sitio predeterminado, los clientes no usarán la reserva a ese grupo.    
No seleccionado | Seleccionado |   **Reserva normal**: se usan los puntos de distribución del grupo de límites actual y luego los de los grupos de límites vecinos y predeterminados de sitios

 Todas las demás configuraciones de implementación darán lugar a una **reserva normal**.  



## <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365  
Configuration Manager 1609 Technical Preview presenta un nuevo panel. Para ver el panel, en la consola de Configuration Manager vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.
>[!NOTE]
>En el área de trabajo **Novedades** de la consola de Configuration Manager, el nuevo panel se denomina incorrectamente **panel de mantenimiento de Office 365**.

El panel muestra gráficos para lo siguiente:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365     
Para más información, vea [Información general de los canales de actualización para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/overview-update-channels).
- Reglas de implementación automática que tienen seleccionado el cliente de Office 365 en el conjunto de productos disponibles

En el panel se pueden realizar las siguientes acciones:
- En la parte superior del panel, use la opción desplegable **Colección** para filtrar los datos del panel por miembros de una colección determinada.
- En el lado superior derecho del panel, haga clic en **Programa de instalación de Office 365** para iniciar el Asistente para la instalación del cliente de Office 365 a fin de implementar aplicaciones de Office 365 en clientes. Para obtener detalles, vea [Implementar aplicaciones de Office 365 en clientes](#deploy-office-365-apps-to-clients).
- En la parte central derecha del panel, haga clic en **Crear una ADR** para abrir el Asistente para crear regla de implementación automática a fin de crear una nueva regla de implementación automática (ADR). Para crear una ADR para aplicaciones de Office 365, seleccione **Cliente de Office 365** al elegir el producto. Para más información, vea [Implementar actualizaciones de software automáticamente](../../sum/deploy-use/automatically-deploy-software-updates.md).
- En la parte inferior derecha del panel, haga clic en **Crear configuración de agente de cliente** para abrir la configuración del agente de cliente. Para más información, vea [Acerca de la configuración de cliente](../clients/deploy/about-client-settings.md).



Para más información sobre las actualizaciones de Office 365 ProPlus, vea [Manage Office 365 ProPlus updates with Configuration Manager (Administrar las actualizaciones de Office 365 ProPlus con Configuration Manager)](../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicaciones de Office 365 en clientes
En esta versión, desde el panel Administración de clientes de Office 365, puede iniciar el programa de instalación de Office 365, que le permite configurar las opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office e implementar los archivos como una aplicación en Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Limitaciones de la implementación de Office 365
- Es posible que tenga problemas al intentar importar la configuración de cliente existente (XML) en el Asistente para la instalación de aplicaciones de Office 365. Puede configurar manualmente la configuración de cliente sin problemas.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Para implementar aplicaciones de Office 365 en clientes
1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.
2. Haga clic en **Programa de instalación de Office 365** en el panel superior derecho. Se abre el Asistente para la instalación del cliente de Office 365.
3. En la página **Configuración de la aplicación**, proporcione un nombre y una descripción para la aplicación, escriba la ubicación de descarga de los archivos y haga clic en **Siguiente**. Tenga en cuenta que la ubicación se debe especificar con el formato &#92;&#92;*servidor*&#92;*recurso compartido*.
4. En la página **Importar configuración de cliente**, elija si quiere importar la configuración del cliente de Office 365 desde un archivo de configuración XML existente o especificarla manualmente y, luego, haga clic en **Siguiente**.
Si tiene un archivo de configuración existente, escriba su ubicación y vaya al paso 7. Tenga en cuenta que la ubicación se debe especificar con el formato &#92;&#92;*servidor*&#92;*recurso compartido*&#92;*nombre archivo*.XML.

    > [!IMPORTANT]
    >Es posible que tenga problemas al intentar importar la configuración de cliente existente (XML) en esta Technical Preview.

5. En la página **Productos de cliente**, seleccione el conjunto de Office 365 que usa, seleccione las aplicaciones que quiere incluir, seleccione los productos de Office adicionales que deberían incluirse y luego haga clic en **Siguiente**.
6. En la página **Configuración de cliente**, elija la configuración que quiere incluir y luego haga clic en **Siguiente**.
7. En la página **Implementación**, elija si quiere implementar la aplicación y haga clic en **Siguiente**.
Si decide no implementar el paquete en el asistente, vaya al paso 9.
8. Configure el resto de las páginas del asistente como lo haría para una implementación de aplicación normal. Para más información, vea [Crear e implementar una aplicación](../../apps/get-started/create-and-deploy-an-application.md).
9. Complete el asistente.
10. Puede implementar o modificar la aplicación igual que cualquier otra aplicación de Configuration Manager desde **Biblioteca de software** > **Información general** > **Administración de aplicaciones** > **Aplicaciones**.

>[!NOTE]
>Después de implementar las aplicaciones de Office 365, puede crear reglas de implementación automática para mantener esas aplicaciones. Para crear una ADR para aplicaciones de Office 365, haga clic en **Crear una ADR** y seleccione **Cliente de Office 365** al elegir el producto. Para más información, vea [Implementar actualizaciones de software automáticamente](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a> Mejoras en BIOS para la conversión UEFI
Ahora puede personalizar una secuencia de tareas de implementación de sistema operativo con una nueva variable, TSUEFIDrive, para que el paso Reiniciar el equipo prepare una partición FAT32 en la unidad de disco duro para la transición a UEFI. En el procedimiento siguiente se proporciona un ejemplo de cómo crear pasos de secuencia de tareas para preparar la unidad de disco duro para la conversión de BIOS en UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar la partición FAT32 para la conversión a UEFI:
En una secuencia de tareas existente para instalar un sistema operativo, agregue un nuevo grupo con pasos para realizar la conversión de BIOS a UEFI.

1. Cree un nuevo grupo de secuencia de tareas después de los pasos para capturar archivos y configuraciones y antes de los pasos para instalar el sistema operativo. Por ejemplo, cree un grupo después del grupo **Capturar archivos y configuraciones** denominado **BIOS a UEFI**.
2. En la pestaña **Opciones** del nuevo grupo, agregue una nueva variable de secuencia de tareas como una condición donde **_SMSTSBootUEFI** **No es igual** a **true**. Esto evita que los pasos del grupo se ejecuten cuando un equipo ya está en modo UEFI.
![Grupo BIOS a UEFI](media/BIOS-to-UEFI-group.png)
3. Debajo del nuevo grupo, agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.  
4. En la pestaña **Opciones**, agregue una variable de secuencia de tareas como una condición donde **_SMSTSInWinPE es igual a false**. Esto evita que este paso se ejecute si el equipo ya está en Windows PE.

    ![Paso Reiniciar el equipo](media/Restart-in-Windows-PE.png)
5. Agregue un paso para iniciar la herramienta de OEM que va a convertir el firmware de BIOS a UEFI. Normalmente será un paso de secuencia de tareas **Ejecutar línea de comandos** con una línea de comandos para iniciar la herramienta de OEM.
5. Agregue el paso de secuencia de tareas Formatear y crear particiones en el disco que va a crear particiones en la unidad de disco duro y a aplicarle formato. En el paso, haga lo siguiente:
    1. Cree la partición FAT32 que se convertirá en UEFI antes de instalar el sistema operativo. Elija **GPT** para **Tipo de disco**.
    ![Paso Formatear y crear particiones en el disco](media/Format-and-partition-disk.png)
    2. Vaya a las propiedades de la partición FAT32. Escriba **TSUEFIDrive** en el campo **Variable**. Cuando la secuencia de tareas detecte esta variable, se preparará para la transición a UEFI antes de reiniciar el equipo.
    ![Propiedades de la partición](media/Partition-properties.png)
    3. Cree una partición NTFS que el motor de secuencia de tareas use para guardar su estado y para almacenar archivos de registro.
6. Agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.  




## <a name="intune-compliance-charts"></a>Gráficos de cumplimiento de Intune
En esta versión, puede obtener una vista rápida del cumplimiento general de los dispositivos y de las principales razones del incumplimiento con los nuevos gráficos del **área de trabajo Supervisión** de la consola de Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Para ver los gráficos de cumplimiento de Intune
1. En la consola de Configuration Manager, vaya a **Supervisión** > **Información general** > **Configuración de cumplimiento**.
2. Se muestra el gráfico **Cumplimiento general del dispositivo**.
3. Haga clic en el nodo **Directivas de cumplimiento** para ver los gráficos **Cumplimiento general del dispositivo** y **Principales razones de incumplimiento**.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitaciones de los gráficos de cumplimiento de Intune en TP 1609
- La obtención de detalle del gráfico **Cumplimiento general del dispositivo** actualmente genera un error.
- El gráfico **Principales razones de incumplimiento** muestra el nombre de la directiva y no los motivos de incumplimiento individuales. Puede hacer clic en la directiva para obtener detalles y ver los dispositivos que no cumplen esa directiva.

### <a name="try-it-out"></a>Haga la prueba
Complete las secciones siguientes en orden:

#### <a name="check-overall-compliance-chart"></a>Revisar el gráfico de cumplimiento general
1. Agregue dos directivas de cumplimiento de iOS en Configuration Manager. Una directiva debe tener un conjunto de configuraciones para los dispositivos (por ejemplo, establecer la longitud del PIN en 6). La otra directiva debe tener otro conjunto de configuraciones (por ejemplo, la complejidad del PIN). Las configuraciones de las directivas no deben superponerse ni entrar en conflicto.
2. Implemente las dos directivas en un conjunto de usuarios.
3. Inscriba dos dispositivos iOS en Intune mediante la misma cuenta de usuario y una cuenta que recibiera las directivas en el paso anterior. Los dispositivos no deben cumplir los criterios de la directiva de cumplimiento.
4. En Configuration Manager, revise el gráfico **Cumplimiento general del dispositivo**. Ambos dispositivos deben aparecer como no conformes.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Comprobar el gráfico de principales razones de incumplimiento
5. Revise el gráfico **Principales razones de incumplimiento**. En él aparecen las cinco principales razones de incumplimiento, pero cuando se han establecido únicamente dos configuraciones de cumplimiento en las directivas, solo se muestran las dos principales razones de incumplimiento.
6. Haga clic en una de las secciones del gráfico. Ambos dispositivos deben aparecer en la vista filtrada de **Activos y compatibilidad** > **Información general** > **Dispositivo**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Hacer conformes los dispositivos y revisar los gráficos
7. Haga que uno de los dispositivos sea conforme con una de las directivas. Vuelva a revisar el gráfico **Cumplimiento general del dispositivo**. El gráfico debería mostrar un dispositivo conforme y otro no conforme.
8. Haga conforme al otro dispositivo con la misma directiva. Esto hará que un dispositivo sea conforme con ambas directivas y el otro con solo una de ellas.
9. Revise el gráfico **Principales razones de incumplimiento**. Solo debería aparecer una razón de incumplimiento.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Consulte también
[Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md)
