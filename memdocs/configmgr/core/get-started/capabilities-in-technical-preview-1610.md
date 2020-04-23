---
title: Funcionalidades de Technical Preview 1610
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6402205ae694d719845492b1af37000a0b9335c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705363"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Funciones de Technical Preview 1610 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*



En este artículo se presentan las características disponibles en la versión 1610 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamaño del contenido en las reglas de implementación automática
Ahora se puede filtrar por el tamaño del contenido de las actualizaciones de software en las reglas de implementación automática. Por ejemplo, puede establecer el filtro **Tamaño del contenido (KB)** en **< 2048** para descargar solo las actualizaciones de software que tengan menos de 2 MB. Con este filtro evita que las actualizaciones de software de gran tamaño se descarguen automáticamente con el fin de ofrecer un mantenimiento simplificado de nivel inferior de Windows cuando el ancho de banda de red es limitado. Para más información, vea [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems (Configuration Manager y mantenimiento simplificado de Windows en sistemas operativos de nivel inferior)](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Para configurar el campo Tamaño del contenido
Para configurar el campo **Tamaño del contenido (KB)** , vaya a la página **Actualizaciones de software** del Asistente para crear regla de implementación automática cuando cree una ADR o vaya a la pestaña **Actualizaciones de software** en las propiedades de una ADR existente.

![Campo Tamaño del contenido](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funcionalidad mejorada para los cuadros de diálogo de software obligatorios
Cuando un usuario recibe software obligatorio, desde el valor **Posponer y volver a recordármelo en:** , puede seleccionar las siguientes opciones en la lista desplegable:
- Más adelante: especifica que las notificaciones se programan según la configuración de notificación establecida en Configuración de agente de cliente.
- Hora fija: especifica que la notificación se programará para mostrarse de nuevo después de la hora seleccionada. Por ejemplo, si un usuario selecciona 30 minutos, la notificación se mostrará de nuevo en 30 minutos.

![Página Agente de equipo de Configuración de agente de cliente](media/computeragentsettings.png)

El tiempo máximo que se puede posponer siempre se basa en los valores de notificación configurados en Configuración de agente de cliente en cada momento a lo largo de la escala de tiempo de implementación. Por ejemplo, si la opción **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)** de la página Agente de equipo se configura para 10 horas y pasan más de 24 horas antes de la fecha límite cuando se inicia el cuadro de diálogo, el usuario vería un conjunto de opciones para posponer de hasta 10 horas, pero nunca de más de esas 10 horas. Cuando se acerca la fecha límite, el cuadro de diálogo muestra menos opciones, en consonancia con la configuración de agente de cliente correspondiente a cada componente de la escala de tiempo de implementación.

Además, en una implementación de alto riesgo, como una secuencia de tareas que implementa un sistema operativo, la experiencia de notificación del usuario final es ahora más intrusiva. En lugar de una notificación transitoria en la barra de tareas, cada vez que se notifica al usuario que se necesita mantenimiento de software crítico, aparece un cuadro de diálogo como el siguiente en el equipo del usuario:

![Cuadro de diálogo Software requerido](media/requiredsoftwaredialog.png)


Para obtener más información:
- [Settings to manage high-risk deployments (Configuración para administrar implementaciones de alto riesgo)](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Cómo establecer la configuración del cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Rechazar solicitudes de aplicación aprobadas previamente

Como administrador, ahora puede rechazar una solicitud de aplicación aprobada previamente. Una vez rechazada, para instalar esta aplicación más adelante, los usuarios deben volver a enviar una solicitud. El rechazo no desinstala la aplicación, sino que obliga a volver a aprobar cualquier solicitud nueva de esa aplicación por parte del usuario. Anteriormente, el rechazo de la solicitud de una aplicación solo estaba disponible para solicitudes de aplicación que no habían sido aprobadas.

#### <a name="try-it-out"></a>Haga la prueba
Para rechazar una solicitud de aplicación aprobada:

1. En la consola de Configuration Manager, [cree e implemente una aplicación](../../apps/deploy-use/create-applications.md) que necesite aprobación.
2. En un equipo cliente, abra el Centro de software y envíe una solicitud para la aplicación.
3. En la consola de Configuration Manager, apruebe la solicitud de aplicación.
4. Rechace la solicitud de aplicación aprobada: en la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de aplicaciones** > **Solicitudes de aprobación** y seleccione la solicitud de aplicación que quiere rechazar.  En la cinta, haga clic en **Denegar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir a clientes de la actualización automática
Technical Preview 1610 presenta una nueva opción que se puede usar para excluir un grupo de clientes de la instalación automática de versiones de cliente actualizadas.  Esto se aplica a la actualización automática y a otros métodos como la actualización basada en actualizaciones de software, los scripts de inicio de sesión y la directiva de grupo. Se puede usar para una colección de equipos a la que haya que prestar una mayor atención a la hora de actualizar el cliente. Un cliente que esté en una colección excluida omite las solicitudes para instalar el software de cliente actualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar la exclusión de la actualización automática
Para configurar las exclusiones de la actualización automática:
1. En la consola de Configuration Manager, abra **Configuración de jerarquía** en **Administración > Configuración del sitio > Sitios** y seleccione la pestaña **Actualización de cliente**.
2. Active la casilla correspondiente a **excluir los clientes especificados de la actualización** y, en la **colección de exclusión**, seleccione la colección que quiere excluir. Solo puede seleccionar una colección para la exclusión.
3. Haga clic en **Aceptar** para cerrar y guardar la configuración. Luego, después de que los clientes actualicen la directiva, los de la colección excluida ya no instalarán automáticamente las actualizaciones del software de cliente.

   ![Configuración de exclusión de actualización automática](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Aunque la interfaz de usuario indica que no se actualizarán los clientes mediante ningún método, hay dos que se pueden usar para invalidar esta configuración. Se pueden usar la instalación de inserción de cliente y la instalación de cliente manual para invalidar esta configuración. Para obtener más detalles, vea la siguiente sección.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Cómo actualizar un cliente que está en una colección excluida
Siempre que una colección está configurada para ser excluida, sus miembros solo pueden actualizar el software de cliente mediante uno de dos métodos que invalidan la exclusión:
- **Instalación de inserción de cliente**: se puede usar la instalación de inserción de cliente para actualizar un cliente que está en una colección excluida. Se permite porque se considera la intención del administrador y permite actualizar los clientes sin quitar toda la colección de la exclusión.       
- **Instalación de cliente manual**: puede actualizar manualmente los clientes que están en una colección excluida con el siguiente modificador de la línea de comandos con ccmsetup: ***/ignoreskipupgrade***

  Si intenta actualizar manualmente un cliente que es miembro de la colección excluida y no usa este modificador, el cliente no instalará el nuevo software de cliente. Para más información, vea [How to install Configuration Manager Clients Manually (Instalación manual de clientes de Configuration Manager)](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

Para más información sobre los métodos de instalación de clientes, vea [Cómo implementar clientes en equipos Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Opciones de configuración de Windows Defender

Ahora puede establecer la configuración de cliente de Windows Defender en equipos Windows 10 inscritos en Intune mediante elementos de configuración de la consola de Configuration Manager.

Concretamente, puede configurar las siguientes opciones de Windows Defender:
- Permitir supervisión en tiempo real
- Permitir supervisión del comportamiento
- Habilitar Sistema de inspección de red
- Examinar todas las descargas
- Permitir análisis de scripts
- Supervisar la actividad de archivos y programas
  - Archivos supervisados
- Días de seguimiento de malware resuelto
- Permitir acceso a IU de cliente
- Programar un examen del sistema
  - Día programado
  - Hora programada
- Programar un examen rápido diario
  - Hora programada
- Limitar el uso de la CPU % durante un examen. Analizar archivos
- Analizar mensajes de correo electrónico
- Analizar unidades extraíbles
- Analizar unidades asignadas
- Analizar archivos abiertos desde recursos compartidos de red
- Intervalo de actualización de firmas
- Permitir la protección de la nube
- Solicitar muestras a los usuarios
- Detección de aplicaciones potencialmente no deseadas
- Carpetas o archivos excluidos
- Extensiones de archivo excluidas
- Procesos excluidos

> [!NOTE]
> Estas opciones de configuración solo pueden configurarse en equipos cliente que ejecutan la actualización de noviembre (1511) de Windows 10 y versiones anteriores.

### <a name="try-it-out"></a>Haga la prueba

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Configuración de cumplimiento** > **Elementos de configuración** y cree un nuevo **Elemento de configuración**.
2. Escriba un nombre, seleccione **Windows 8.1 y Windows 10** en **Settings for devices managed without the Configuration Manager client (Configuración de dispositivos administrados sin el cliente de Configuration Manager)** y haga clic en **Siguiente**.
3. Asegúrese de que **Todo Windows 10 (64 bits)** y **Todo Windows 10 (32 bits)** están seleccionados en la página **Plataformas admitidas** y, después, haga clic en **Siguiente**.
4. Seleccione el grupo de configuración **Windows Defender** y, después, haga clic en **Siguiente**.
5. Configure la configuración deseada en esta página y, después, haga clic en **Siguiente**.
6. Complete el asistente.
7. Agregue este elemento de configuración a una línea base de configuración e implemente esta línea base en equipos que ejecutan la actualización de noviembre (1511) de Windows 10 o versiones anteriores.

> [!NOTE]
> Recuerde marcar la casilla **Corregir configuraciones no compatibles** al implementar la línea base de configuración.

## <a name="request-policy-sync-from-administrator-console"></a>Solicitar la sincronización de directivas desde la consola de administrador

Ahora puede solicitar una sincronización de directivas para un dispositivo móvil desde la consola de Configuration Manager, en lugar de solicitar una sincronización desde el propio dispositivo. La información del estado de la solicitud de sincronización está disponible como una columna nueva en las vistas del dispositivo, denominada **Remote Sync State (Estado de la sincronización remota)** . El estado también aparece en la sección **Datos de detección** del cuadro de diálogo **Propiedades** de cada dispositivo móvil.

### <a name="try-it-out"></a>Haga la prueba

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > Dispositivos.
2. En el menú **Acciones de dispositivo remoto**, seleccione **Send Sync Request (Enviar solicitud de sincronización)** .

La sincronización puede tardar de cinco a diez minutos. Cualquier cambio en la directiva se sincroniza con el dispositivo. Puede realizar un seguimiento del estado de la solicitud de sincronización en la columna **Remote Sync State (Estado de la sincronización remota)** de la vista **Dispositivos** o en el cuadro de diálogo **Propiedades** del dispositivo.

## <a name="additional-security-role-support"></a>Compatibilidad adicional del rol de seguridad

Además del rol Administrador total, los siguientes roles de seguridad integrados ahora tienen acceso total a los elementos en el nodo de **todos los dispositivos corporativos**, incluidos los **dispositivos declarados con anterioridad**, los **perfiles de inscripción de iOS** y los **perfiles de inscripción de Windows**:
- **Administrador de activos**
- **Administrador de acceso a los recursos de la empresa**

Aún se concede acceso de solo lectura a estas áreas de la consola de Configuration Manager para el rol **Analista de solo lectura**.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Acceso condicional para perfiles de VPN de Windows 10

Ahora puede requerir que los dispositivos Windows 10 inscritos en Azure Active Directory sean compatibles para disponer de acceso a la VPN a través de perfiles de VPN de Windows 10 creados en la consola de Configuration Manager. Esto es posible a través de la nueva casilla **Habilitar acceso condicional para esta conexión VPN** en la página **Método de autenticación** del Asistente para perfiles de VPN y propiedades de perfil de VPN para perfiles de VPN de Windows 10. También puede especificar un certificado independiente para la autenticación de inicio de sesión único si habilita el acceso condicional para el perfil.

## <a name="see-also"></a>Consulte también
[Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md)
