---
title: Funcionalidades de Technical Preview 1702
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1702.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 73b8111cbada129997cec965ca685f1ef22b1f3a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705313"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Funciones de Technical Preview 1702 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1702 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentarios desde la consola de Configuration Manager

Esta versión preliminar presenta nuevas opciones de comentarios en la consola de Configuration Manager. Las opciones de comentarios le permiten enviar comentarios directamente al equipo de desarrollo, mediante el sitio web de comentarios de UserVoice de Configuration Manager.  

> Puede encontrar la opción **Comentarios**:
> -  En la cinta de opciones, en el extremo izquierdo de la pestaña Inicio de cada nodo.  
>    ![Cinta de opciones](./media/feedback-home.png)

-  Al hacer clic con el botón derecho en cualquier objeto de la consola.   
    ![Opción de hacer clic con el botón derecho](./media/feedback-option.png)   

Al seleccionar **Comentarios**, se abre el explorador en el sitio web de comentarios de UserVoice de Configuration Manager, en https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Cambios para actualizaciones y mantenimiento
Con esta versión preliminar se presenta lo siguiente.

**Opciones de actualización más sencillas**  
La próxima vez que la infraestructura sea apta para dos o más actualizaciones, se descargará únicamente la actualización más reciente. Por ejemplo, si la versión actual del sitio es dos o más versiones más antigua que la versión más reciente disponible, solo se descarga automáticamente la versión más reciente de la actualización.  

Tiene la opción de descargar e instalar las demás actualizaciones disponibles, incluso cuando no sean la versión más reciente. En cambio, recibirá una advertencia de que la actualización se ha reemplazado por la más reciente. Para descargar una actualización que esté *Disponible para descarga*, seleccione la actualización en la consola y después haga clic en **Descargar**.

**Limpieza mejorada de las actualizaciones más antiguas**   
Se ha agregado una función de limpieza automática que elimina las descargas innecesarias de la carpeta "EasySetupPayload" en el servidor de sitio.  


## <a name="peer-cache-improvements"></a>Mejoras de almacenamiento en caché del mismo nivel
A partir de esta versión, un equipo de origen de almacenamiento en caché del mismo nivel rechazará una solicitud de contenido cuando el equipo de origen de almacenamiento en caché del mismo nivel cumpla alguna de las condiciones siguientes:  
-  Está en modo de batería baja.
-  La carga de CPU supera el 80 % en el momento en que se solicita el contenido.
-  E/S de disco tiene un valor *AvgDiskQueueLength* superior a 10.
-  No hay más conexiones disponibles para el equipo.   

Puede configurar estas opciones mediante la clase de configuración de agente cliente de la característica de origen del mismo nivel (*SMS_WinPEPeerCacheConfig*) cuando se usa el SDK de Configuration Manager.

Cuando el equipo rechaza una solicitud del contenido, el equipo solicitante continuará buscando el contenido en orígenes alternativos en su grupo de ubicaciones de origen de contenido disponibles.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a> Usar Azure Active Directory Domain Services para administrar dispositivos, usuarios y grupos

Con esta versión de vista previa técnica puede administrar los dispositivos que están unidos a un dominio administrado de Azure Active Directory (AD) Domain Services. También puede detectar dispositivos, usuarios y grupos en ese dominio con varios métodos de detección de Configuration Manager.

La infraestructura de sitio de vista previa técnica, los clientes y el dominio de Azure AD Domain Services deben ejecutarse en Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configurar Configuration Manager para usar Azure AD
Para usar Azure AD con Configuration Manager, necesitará lo siguiente:
- Suscripción de Azure.
- Azure AD con Domain Services (DS).
- Un sitio de Configuration Manager que se ejecute en una máquina virtual de Azure que esté unida a Azure AD.
- Clientes de Configuration Manager que se ejecuten en el mismo entorno de Azure AD.

Para configurar Azure AD Domain Services, consulte [Introducción a Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Detectar recursos
Después de configurar Configuration Manager para que se ejecute en Azure AD, puede usar los siguientes métodos de detección de Active Directory para buscar recursos en Azure AD:  
- Detección de sistemas de Active Directory
- Detección de usuario de Active Directory
- Detección de grupos de Active Directory  

Para cada método que use, modifique la consulta LDAP para buscar las estructuras de unidad organizativa de Azure AD en lugar de los contenedores típicos del Active Directory local. Esto requiere que dirija la consulta para buscar en Active Directory en su suscripción de Azure.  

Los ejemplos siguientes usan el Azure AD *contoso.onmicrosoft.com*:
- **Detección de sistemas**   
  Azure AD almacena los dispositivos bajo la unidad organizativa **AADDC Computers**.  Configurar lo siguiente:  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **Detección de usuarios** AAD almacena los usuarios bajo la unidad organizativa **AADDC Users**.  Configurar lo siguiente:
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Detección de grupos**  
Azure AD no tiene ninguna unidad organizativa que almacene los grupos. En su lugar, use la misma estructura general que las consultas de usuario o de sistema, y configure la consulta LDAP para que apunte a la unidad organizativa que contiene los grupos que quiere detectar.

Para obtener más información sobre Azure AD, consulte lo siguiente:  
- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) en azure.microsoft.com.
- [Documentación acerca de Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services) en docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Mejoras de la directiva de cumplimiento de dispositivos de acceso condicional

Una nueva regla de directiva de cumplimiento de dispositivos está disponible para ayudar a bloquear el acceso a los recursos corporativos que admiten el acceso condicional, cuando los usuarios usan aplicaciones que forman parte de una lista de aplicaciones no compatibles. El administrador puede definir la lista de aplicaciones no compatibles cuando se agrega la nueva regla conforme **Aplicaciones que no se pueden instalar**. Esta regla requiere que el administrador escriba el **Nombre de la aplicación**, el **Id. de la aplicación** y el **Publicador de la aplicación** (opcional) al agregar una aplicación a la lista de aplicaciones no compatibles. Esta configuración solo se aplica a dispositivos iOS y Android.

Además, esto ayuda a las organizaciones a mitigar la pérdida de datos a través de aplicaciones no seguras y evitar el consumo excesivo de datos a través de determinadas aplicaciones.

### <a name="try-it-out"></a>Haga la prueba

**Escenario:** identifique las aplicaciones que podrían estar causando pérdida de datos mediante el envío de datos corporativos fuera de la empresa o que causan el consumo excesivo de datos, y después [cree una directiva de cumplimiento de dispositivos de acceso condicional](../../mdm/understand/what-happened-to-hybrid.md) que agregue estas aplicaciones a la lista de aplicaciones no compatibles. Esto bloqueará el acceso a los recursos corporativos que admiten el acceso condicional hasta que el usuario pueda quitar la aplicación bloqueada.

## <a name="antimalware-client-version-alert"></a>Alerta de versión de cliente antimalware
A partir de esta versión preliminar, Configuration Manager Endpoint Protection proporciona una alerta si más del 20 % (valor predeterminado) de los clientes administrados usan una versión expirada del cliente antimalware (es decir, Windows Defender o el cliente de Endpoint Protection).

### <a name="try-it-out"></a>Haga la prueba
Asegúrese de que Endpoint Protection está habilitado en todos los clientes de escritorio y servidor mediante la directiva de configuración de cliente. Ahora puede ver la **Versión de cliente antimalware** y el **Estado de implementación de Endpoint Protection** si va a **Activos y compatibilidad** > **Información general** > **Dispositivos** > **Todos los clientes de escritorio y servidor**. Para comprobar una alerta, vea **Alertas** en el área de trabajo **Supervisión**. Si más de un 20 % de los clientes administrados ejecutan una versión expirada del software antimalware, la versión de cliente de antimalware está obsoleta y se muestra la alerta. Esta alerta no aparece en la pestaña **Supervisión** > **Información general**. Para actualizar los clientes antimalware expirados, habilite las actualizaciones de software para los clientes antimalware.

Para configurar el porcentaje en el que se genera la alerta, expanda **Supervisión** > **Alertas** > **Todas las alertas**, haga doble clic en **Clientes antimalware obsoletos** y modifique la opción **Generar alerta si el porcentaje de clientes administrados con una versión obsoleta del cliente antimalware es más de**.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Evaluación del cumplimiento para actualizaciones de Windows Update for Business
Ahora puede configurar una regla de actualización de directivas de cumplimiento para incluir un resultado de evaluación de Windows Update for Business como parte de la evaluación de acceso condicional.
> [!IMPORTANT]
> Debe tener Windows 10 Insider Preview, compilación 15019 o posterior, para usar la evaluación del cumplimiento para actualizaciones de Windows Update for Business.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Permitir a Windows Update for Business administrar las actualizaciones de Windows 10
Para recopilar información de evaluación de cumplimiento para actualizaciones de Windows Update for Business, siga los pasos siguientes para configurar el agente cliente para permitir explícitamente que Windows Update for Business administre las actualizaciones de Windows 10.
1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**.
2. En las propiedades de la configuración de cliente, vaya a **Actualizaciones de software** y seleccione **Sí** en el valor **Administrar actualizaciones de Windows 10 con Windows Update for Business**.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Crear una directiva de cumplimiento para la evaluación de Windows Update for Business
1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Configuración de cumplimiento** > **Directivas de cumplimiento**.
2. Haga clic en **Crear directiva de cumplimiento** o seleccione una directiva de cumplimiento existente para modificarla.
3. En la página General, proporcione un nombre y una descripción, seleccione **Reglas de cumplimiento para dispositivos administrados con el cliente de Configuration Manager**, establezca la gravedad de no compatibilidad para la creación de informes y haga clic en **Siguiente**.
4. En la página Plataformas admitidas, seleccione **Windows 10** y después haga clic en **Siguiente**.
5. En la página Reglas, haga clic en **Nuevo...**  y, después, para **Condición**, seleccione **Requerir cumplimiento para Windows Update for Business**. La opción **Valor** se establece automáticamente en **True**.

La nueva directiva se muestra en el nodo **Directivas de cumplimiento** del área de trabajo **Activos y compatibilidad** .

### <a name="deploy-a-compliance-policy"></a>Implementar una directiva de cumplimiento
1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Configuración de cumplimiento** y después haga clic en **Directivas de cumplimiento**.
2. En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.
3. En el cuadro de diálogo **Implementar directiva de cumplimiento** , haga clic en **Examinar** para seleccionar la recopilación de usuarios en la que se va a implementar la directiva.
   Además, puede seleccionar opciones para generar alertas cuando la directiva no es compatible y también para configurar la programación por medio de la cual se evaluará esta directiva para el cumplimiento.
4. Cuando haya terminado, haga clic en **Aceptar**.

### <a name="monitor-the-compliance-policy"></a>Supervisar la directiva de cumplimiento
Después de crear la directiva de cumplimiento, puede supervisar los resultados de compatibilidad en la consola de Configuration Manager. Para obtener más información, consulte [Monitor the compliance policy (Supervisar la directiva de cumplimiento)](../../mdm/understand/what-happened-to-hybrid.md).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Mejoras en la configuración del Centro de software y los mensajes de notificación para las secuencias de tareas de alto impacto
Esta versión incluye las siguientes mejoras en la configuración del Centro de software y los mensajes de notificación para las secuencias de tareas de implementación de alto impacto:

- En las propiedades de la secuencia de tareas, ahora se puede configurar cualquier secuencia de tareas, incluidas las que no son del sistema operativo, como una implementación de alto riesgo. Cualquier secuencia de tareas que cumpla determinadas condiciones se define automáticamente como de alto impacto. Para obtener información detallada, vea [Administrar implementaciones de alto riesgo](../servers/manage/settings-to-manage-high-risk-deployments.md).
- En las propiedades de la secuencia de tareas, puede elegir usar el mensaje de notificación predeterminado o crear su propio mensaje de notificación personalizado para las implementaciones de alto impacto.
- En las propiedades de la secuencia de tareas, puede configurar las propiedades del Centro de software, que incluyen realizar un reinicio obligatorio, el tamaño de descarga de la secuencia de tareas y el tiempo de ejecución estimado.
- El mensaje de la implementación de alto impacto predeterminado para actualizaciones en contexto indica ahora que las aplicaciones, los datos y la configuración se migran automáticamente. Anteriormente, el mensaje predeterminado para cualquier instalación de sistema operativo indicaba que todas las aplicaciones, datos y configuraciones se perderían, lo que no era cierto para una actualización en contexto.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Establecer una secuencia de tareas como una secuencia de tareas de alto impacto
Siga este procedimiento para establecer una secuencia de tareas como de alto impacto.
> [!NOTE]
> Cualquier secuencia de tareas que cumpla determinadas condiciones se define automáticamente como de alto impacto. Para obtener información detallada, vea [Administrar implementaciones de alto riesgo](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Sistemas operativos** > **Secuencias de tareas**.
2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.
3. En la pestaña **Notificación de usuario**, seleccione **Es una secuencia de tareas de alto impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Crear una notificación personalizada para implementaciones de alto riesgo
1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Sistemas operativos** > **Secuencias de tareas**.
2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.
3. En la pestaña **Notificación de usuario**, seleccione **Usar texto personalizado**.
   > [!NOTE]
   >  Solo se puede establecer el texto de la notificación del usuario cuando se selecciona **Es una secuencia de tareas de alto impacto**.

4. Configure las siguientes opciones (máximo de 255 caracteres para cada cuadro de texto):

   **Texto del título de la notificación de usuario**: especifica el texto de color azul que aparece en la notificación de usuario del Centro de software. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene algo como "Confirme que quiere actualizar el sistema operativo en este equipo".

   **Texto del mensaje de notificación de usuario**: hay tres cuadros de texto que proporcionan el cuerpo de la notificación personalizada.
   - Cuadro de texto 1: especifica el cuerpo principal del texto, que normalmente contiene instrucciones para el usuario. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene algo como "La actualización del sistema operativo llevará un tiempo y es posible que el equipo se reinicie varias veces".
   - Cuadro de texto 2: especifica el texto en negrita debajo del cuerpo de texto principal. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene algo como "Esta actualización en contexto instala el nuevo sistema operativo y migra automáticamente sus aplicaciones, datos y configuración".
   - Cuadro de texto 3: especifica la última línea de texto debajo del texto en negrita. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene algo como "Haga clic en Instalar para comenzar. De lo contrario, haga clic en Cancelar".   

   Supongamos que configura la siguiente notificación personalizada en las propiedades.

   ![Notificación personalizada para una secuencia de tareas](./media/user-notification.png)

   Se mostrará el siguiente mensaje de notificación cuando el usuario final abra la instalación desde el Centro de software.

   ![Notificación personalizada para una secuencia de tareas](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurar propiedades del Centro de software
Siga este procedimiento para configurar los detalles de la secuencia de tareas que aparece en el Centro de software. Estos detalles son meramente informativos.  
1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Sistemas operativos** > **Secuencias de tareas**.
2. Seleccione la secuencia de tareas que se va editar y haga clic en **Propiedades**.
3. En la pestaña **General**, está disponible la siguiente configuración para el Centro de software:
   - **Es necesario reiniciar**: permite al usuario saber si es necesario reiniciar durante la instalación.
   - **Tamaño de la descarga (MB)** : especifica cuántos megabytes se muestran en el Centro de software para la secuencia de tareas.  
   - **Tiempo de ejecución estimado (minutos)** : especifica el tiempo de ejecución estimado en minutos que se muestra en el Centro de software para la secuencia de tareas.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Comprobar los archivos ejecutables en ejecución antes de instalar una aplicación

En el cuadro de diálogo **Propiedades** de *\<nombre del tipo de implementación>* de un tipo de implementación, en la pestaña Comportamiento de instalación, ahora se puede especificar uno o varios archivos ejecutables que, si se ejecutan, bloquearán la instalación del tipo de implementación. El usuario debe cerrar el archivo ejecutable en ejecución (o se puede cerrar automáticamente para las implementaciones con un propósito de requerido) antes de poder instalar el tipo de implementación.

### <a name="try-it-out"></a>Pruébelo.

1. En las propiedades de un tipo de implementación de Configuration Manager, haga clic en la pestaña **Comportamiento de instalación**.
2. Pulse **Agregar** para agregar uno o más nombres de archivo ejecutable que quiere activar. También puede agregar un nombre para mostrar para facilitar a los usuarios la identificación de las aplicaciones de la lista.
3. Si la implementación va tener un propósito de requerido, en el Asistente para implementar software, se puede optar por **Cerrar automáticamente los ejecutables en ejecución especificados en la pestaña Comportamiento de instalación del cuadro de diálogo de propiedades del tipo de implementación**.

Si la aplicación se ha implementado como **Disponible** y un usuario final intenta instalar una aplicación, se le pedirá que cierre los ejecutables en ejecución especificados antes de poder continuar con la instalación.

Si la aplicación se ha implementado como **Requerido** y la opción **Cerrar automáticamente los ejecutables en ejecución especificados en la pestaña Comportamiento de instalación del cuadro de diálogo de propiedades del tipo de implementación** está seleccionada, verán un cuadro de diálogo que les informa de que los archivos ejecutables especificados se cerrarán automáticamente cuando se alcance la fecha límite de instalación de la aplicación. Puede programar estos cuadros de diálogo en **Configuración de cliente** > **Agente de equipo**. Si no quiere que el usuario final vea estos mensajes, seleccione **Ocultar en el Centro de software y ocultar todas las notificaciones** en la pestaña **Experiencia del usuario** de las propiedades de la implementación.

Si la aplicación se ha implementado como **Requerido** y la opción **Cerrar automáticamente los ejecutables en ejecución especificados en la pestaña Comportamiento de instalación del cuadro de diálogo de propiedades del tipo de implementación** no está seleccionada, no se podrá instalar la aplicación si una o varias de las aplicaciones especificadas está en ejecución.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Crear certificados PFX con compatibilidad con S MIME

Ahora se puede crear un perfil de certificado PFX que sea compatible con S/MIME e implementarlo a los usuarios.  Después, este certificado puede usarse para el cifrado y descifrado de S/MIME en los dispositivos inscritos por el usuario.

Además, ahora se pueden especificar varias entidades de certificación (CA) en varios roles de sistema de sitio de punto de registro de certificado y después asignar qué entidad de certificación procesa las solicitudes como parte del perfil de certificado.

Para dispositivos iOS, puede asociar un perfil de certificado PFX a un perfil de correo electrónico y habilitar el cifrado de S/MIME.  Después, esto habilita S/MIME en el cliente de correo electrónico nativo de iOS y le asocia el certificado de cifrado S/MIME correcto.

Para más información sobre los certificados en Configuration Manager, vea [Introducción a los perfiles de certificado]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Nueva configuración de cumplimiento para dispositivos iOS

Se han agregado nuevas opciones que se pueden usar en los elementos de configuración para dispositivos iOS. Son opciones que existían con anterioridad en Microsoft Intune en una configuración independiente y que ahora están disponibles al usar Intune con Configuration Manager. Si necesita ayuda con cualquiera de estas configuraciones, vea [Configuración de directivas de iOS en Microsoft Intune](/mem/intune/configuration/device-restrictions-ios).

- **Sincronización de datos desde aplicaciones administradas en iCloud**
- **Handoff para continuar las actividades en otro dispositivo**
- **Uso compartido de fotografías de iCloud**
- **Biblioteca de fotografías de iCloud**
- **Confiar en nuevos autores de aplicaciones empresariales**
- **Permitir al usuario descargar contenido desde la tienda de iBooks marcado como "Erótico"** (solo en modo supervisado)
- **Forzar a los dispositivos Apple Watch enlazados a usar la detección de muñeca**
- **Contraseña para las solicitudes salientes de AirPlay**
- **Modificar la configuración de la cuenta** (solo en modo supervisado)
- **Cambios en la configuración de uso de datos móviles de la aplicación** (solo en modo supervisado)
- **Borrar todo el contenido y la configuración** (solo en modo supervisado)
- **Configurar restricciones en el dispositivo** (solo en modo supervisado)
- **Usar emparejamiento de host para controlar los dispositivos que puede emparejar un dispositivo iOS** (solo en modo supervisado)
- **Instalar los certificados y los perfiles de configuración** (solo en modo supervisado)
- **Modificación del nombre de dispositivo** (solo en modo supervisado)
- **Modificación del código de acceso** (solo en modo supervisado)
- **Emparejamiento de Apple Watch** (solo en modo supervisado)
- **Modificación de la configuración de notificación** (solo en modo supervisado)
- **Modificación del fondo de pantalla** (solo en modo supervisado)
- **Modificación de la configuración de envío de diagnósticos** (solo en modo supervisado)
- **Modificación de Bluetooth** (solo en modo supervisado)
- **AirDrop** (solo en modo supervisado)
- **Usar Siri para consultar el contenido generado por el usuario de Internet** (solo en modo supervisado)
- **Filtro de obscenidad de Siri** (solo en modo supervisado)
- **Devolver resultados de Internet en búsquedas de Spotlight** (solo en modo supervisado)
- **Búsqueda de definiciones de palabras** (solo en modo supervisado)
- **Teclados predictivos** (solo en modo supervisado)
- **Corrección automática** (solo en modo supervisado)
- **Revisión ortográfica de teclado** (solo en modo supervisado)
- **Métodos abreviados de teclado** (solo en modo supervisado)
  <!--- - **Enterprise app trust settings modification** --->
- **Instalación de aplicaciones solo con Apple Configurator e iTunes** (solo en modo supervisado)
- **Descargas de aplicaciones automáticas** (solo en modo supervisado)
- **Realizar cambios en la configuración de la aplicación Buscar a mis amigos** (solo en modo supervisado)
- **Acceso a la tienda de iBooks** (solo en modo supervisado)
- **Aplicación de mensajes** (solo en modo supervisado)
- **Podcasts** (solo en modo supervisado)
- **Apple Music** (solo en modo supervisado)
- **iTunes Radio** (solo en modo supervisado)
- **Apple News** (solo en modo supervisado)
- **Game Center** (solo en modo supervisado)
- **Tratar AirDrop como un destino no administrado**

## <a name="android-for-work-support"></a>Compatibilidad de Android for Work

A partir de la versión Technical Preview 1702, puede enlazar una cuenta de Google a su inquilino MDM híbrido. Esto le permite hacer lo siguiente:

- Inscribir [dispositivos Android compatibles](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) como Android for Work, para crear perfiles de trabajo en los dispositivos inscritos
- Aprobar aplicaciones en la tienda Play for Work, sincronizarlas con la consola de Configuration Manager y, después, implementarlas en los perfiles de trabajo de los dispositivos
- Crear e implementar elementos de configuración para configurar las opciones de perfiles y contraseñas de trabajo para los dispositivos
- Crear e implementar elementos de directiva de cumplimiento y perfiles de acceso de recursos para dispositivos Android for Work como ya se hace para dispositivos Android
- Realizar la eliminación selectiva en dispositivos Android for Work

Cuando se inscribe un dispositivo como Android for Work, crea un perfil de trabajo en el dispositivo que Intune puede administrar. Este perfil de trabajo existe en paralelo con el perfil personal en el dispositivo Android. Los usuarios pueden cambiar fácilmente entre aplicaciones de perfil de trabajo y aplicaciones de perfil personal. No se pueden administrar elementos en el perfil personal. Las aplicaciones y los datos personales permanecen sin administrar. Configuration Manager tiene control total sobre el perfil de trabajo y su contenido, y puede quitarlo del dispositivo.

Android for Work es una plataforma independiente de Android y deberá decidir qué forma de administración usar para los dispositivos Android compatibles con perfiles de trabajo.

### <a name="try-it-out"></a>Haga la prueba
Las secciones siguientes describen la administración de Android for Work.

#### <a name="enable-android-for-work-management"></a>Habilitar la administración de Android for Work
1. Cree una cuenta de Google en https://accounts.google.com/SignUp para usarla como la cuenta de administrador de Android for Work que va a estar asociada a todas las tareas de administración de Android for Work de este inquilino de Intune. Podría ser una cuenta de Google que se comparte entre los administradores que administran dispositivos Android. Se trata de la cuenta de Google que su organización usa para administrar y publicar aplicaciones en la consola de Play for Work. Usará esta cuenta para aprobar aplicaciones en la tienda de Play for Work, por lo que debe realizar el seguimiento del nombre y la contraseña de la cuenta.
2. Habilite la inscripción de Android enlazando la cuenta de Google con el inquilino de Intune administrado en Configuration Manager:
   1. Vaya a **Administración** > **General** > **Cloud Services** > **Suscripciones a Microsoft Intune** y seleccione la suscripción a Intune.
   2. En la cinta, haga clic en **Configurar plataformas** > **Android** y asegúrese de que **Habilitar inscripción de Android** está activada.
   3. En la cinta, haga clic en **Configurar plataformas** > **Android for Work**.
   4. En el cuadro de diálogo, haga clic en **Configurar Android for Work en la consola de Intune**. Se abre la consola de Intune en el explorador web.
   5. Use sus credenciales de administrador de Intune para iniciar sesión en el portal de Intune.
   6. Haga clic en **Configurar** para abrir el sitio web Android for Work de Google Play.
   7. En la página de inicio de sesión de Google, escriba las credenciales de la cuenta de Google del paso 1 y después proporcione la información de su empresa.
3. Cuando vuelva al portal de Intune, Android for Work está habilitado y tiene tres opciones de inscripción para dispositivos Android for Work:
   - **Administrar todos los dispositivos como Android**: (deshabilitado) Todos los dispositivos Android se inscribirán, incluidos los dispositivos que admiten Android for Work, como dispositivos Android convencionales
   - **Administrar dispositivos compatibles como Android for Work**: (habilitado) Todos los dispositivos que admiten Android for Work se inscriben como dispositivos Android for Work. Todo dispositivo Android que no admita Android for Work se inscribe como dispositivo Android convencional.
   - **Administrar los dispositivos compatibles para los usuarios únicamente en estos grupos como Android for Work**: (pruebas) Le permite dirigir la administración de Android for Work a un conjunto limitado de usuarios. Solo los miembros de los grupos seleccionados que inscriben un dispositivo que admita Android for Work se inscriben como dispositivos Android for Work. Todos los demás se inscriben como dispositivos Android.
  
> [!NOTE]
> Un problema conocido impide que la opción **Administrar los dispositivos compatibles para usuarios solo en estos grupos como Android for Work** funcione según lo esperado. Los dispositivos de los usuarios en los grupos de Azure AD especificados se inscribirán como Android en lugar de Android for Work. Para probar Android for Work, debe usar la opción **Manage all supported devices as Android for Work** (Administrar todos los dispositivos compatibles como Android for Work).


  Para habilitar la inscripción de Android for Work, debe elegir una de las dos opciones de la parte inferior. La opción **Administrar los dispositivos compatibles para los usuarios únicamente en estos grupos como Android for Work** requiere configurar primero los grupos de seguridad de Azure Active Directory.

Verá el nombre de la cuenta y el nombre de la organización en el portal de Intune cuando se complete el enlace. Después, podrá cerrar los dos exploradores.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Aprobar e implementar aplicaciones Android for Work
Siga estos pasos para aprobar aplicaciones en la tienda Play for Work, sincronizarlas con la consola de Configuration Manager e implementarlas en dispositivos Android for Work administrados. Para implementar aplicaciones en los perfiles de trabajo de los usuarios, debe aprobar las aplicaciones en Play for Work y después sincronizarlas con la consola de Configuration Manager.

1. Abra un explorador y vaya a: https://play.google.com/work.
2. Inicie sesión con la cuenta de administrador de Google enlazada a su inquilino de Intune.
3. Busque las aplicaciones que le gustaría implementar en su entorno y haga clic en **Aprobar** en cada una de ellas.
4. En la consola de Configuration Manager, vaya a **Administrador** > **General** > **Cloud Services** > **Android for Work** y haga clic en **Sincronizar**.
5. Espere hasta 10 minutos para que las aplicaciones se sincronicen y, después, vaya a **Biblioteca de software** > **General** > **Administración de aplicaciones** > **Información de licencia para las aplicaciones de la Tienda**.
6. Haga clic en una aplicación sincronizada desde Play for Work y después en **Crear aplicación**.
7. Complete el asistente y haga clic en **Cerrar**.
8. Vaya a **Biblioteca de software** > **General** > **Administración de aplicaciones** > **Aplicaciones**, seleccione una aplicación de Android for Work e impleméntela como de costumbre.

Para sincronizar aplicaciones Play for Work con Configuration Manager, debe aprobar al menos una aplicación en el sitio web de Play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Inscribir un dispositivo Android for Work
La forma de inscribir dispositivos Android for Work es similar a la inscripción para Android. Descargue y ejecute la aplicación Portal de empresa para Android en el dispositivo móvil. Se le pedirá crear un perfil de trabajo como parte del proceso de inscripción.  Una vez creado el perfil de trabajo, debe cambiar a la versión administrada del Portal de empresa. El Portal de empresa administrado se etiqueta con un pequeño maletín de color naranja en la esquina inferior derecha.

#### <a name="create-and-deploy-a-configuration-item"></a>Crear e implementar un elemento de configuración
Android for Work tiene dos grupos de configuración para elementos de configuración:
- Contraseña
- Perfil de trabajo

Puede configurar el uso compartido de contenido entre los perfiles de trabajo, así como los siguientes elementos de configuración en dispositivos que ejecuten Android 6 o una versión superior:
- El comportamiento de las aplicaciones que solicitan permisos específicos
- Si las notificaciones para aplicaciones en el perfil de trabajo son visibles en la pantalla de bloqueo

Para probarlo, cree un elemento de configuración mediante el flujo de trabajo estándar, elija **Android for Work** en la página **General** y configure los valores para cada uno de los grupos de configuración, agregando el elemento de configuración a una línea base e implementándolo como de costumbre. Esta configuración solo se aplicará a los dispositivos inscritos como Android for Work y no a los inscritos como Android.

#### <a name="perform-selective-wipe"></a>Realizar la eliminación selectiva
Los dispositivos inscritos como Android for Work solo se pueden eliminar de forma selectiva porque solo se administra el perfil de trabajo. Esto evita que el perfil personal se elimine. Realizar una eliminación selectiva en un dispositivo Android for Work quita el perfil de trabajo, incluidas todas las aplicaciones y los datos, y anula la inscripción del dispositivo.

Para eliminar de forma selectiva un dispositivo Android for Work, use el [proceso de eliminación selectiva](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) normal en la consola de Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problemas conocidos de Android for Work
**Al configurar la programación de sincronización en Android for Work, los perfiles de correo electrónico no se pueden implementar** Una de las opciones en la interfaz de usuario de ConfigMgr para los perfiles de correo electrónico de Android for Work es "Programar". En otras plataformas, esto permite al administrador configurar una programación para la sincronización de correo electrónico y otros datos de la cuenta de correo en los dispositivos móviles en que se implementa. En cambio, no funciona para perfiles de correo electrónico de Android for Work y si se escoge cualquier opción que no sea "No configurado", el perfil no se implementará en ningún dispositivo.
