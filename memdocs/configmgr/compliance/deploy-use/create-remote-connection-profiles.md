---
title: Creación de perfiles de conexión remota
titleSuffix: Configuration Manager
description: Use perfiles de conexión remota de Configuration Manager para permitir a los usuarios conectarse de forma remota a los equipos de trabajo.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 1434d7802eb1ed68cb0a575778bdae1e5e99c9ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694753"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Perfiles de conexión remota en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use perfiles de conexión remota de Configuration Manager para permitir a los usuarios conectarse de forma remota a los equipos de trabajo. Estos perfiles le permiten implementar la configuración de Conexión a Escritorio remoto en usuarios de su jerarquía. Los usuarios pueden tener acceso a cualquiera de sus equipos de trabajo principales mediante Escritorio remoto a través de una conexión VPN.  

> [!IMPORTANT]  
> Cuando se especifica la configuración del perfil de conexión remota con Configuration Manager, el cliente almacena la configuración en la directiva local de Windows. Estas opciones podrían invalidar la configuración de Escritorio remoto que se configura con otra aplicación. Además, si usa la directiva de grupo de Windows para establecer la configuración de Escritorio remoto, la configuración especificada en la directiva de grupo invalidará la configuración de Configuration Manager.

Configuration Manager crea un grupo de seguridad en los clientes, **Conexión de equipo remoto**. Cuando se implementa un perfil de conexión remota, el cliente agrega los usuarios primarios del equipo a este grupo. Un administrador local puede agregar o quitar usuarios manualmente de este grupo, pero Configuration Manager actualiza la pertenencia la próxima vez que evalúa el cumplimiento del perfil.

> [!IMPORTANT]  
> Si la relación de afinidad entre un usuario y un dispositivo cambia, Configuration Manager deshabilita el perfil de conexión remota y la configuración del Firewall de Windows para impedir las conexiones al equipo.

## <a name="prerequisites"></a>Requisitos previos  

### <a name="external-dependencies"></a>Dependencias externas  

- Si desea permitir que los usuarios se conecten desde Internet, instale y configure un servidor de puerta de enlace de Escritorio remoto. Para más información sobre cómo instalar y configurar un servidor de puerta de enlace de Escritorio remoto, consulte [Servicios de Escritorio remoto: Acceso desde cualquier lugar](/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- Si los clientes ejecutan un firewall basado en host, debe habilitar el programa mstsc.exe. Si configura un perfil de conexión remota, habilite la configuración **Permitir excepción del Firewall de Windows para conexiones en dominios de Windows y en redes privadas**. Esta configuración permite a Configuration Manager configurar automáticamente el Firewall de Windows.

    > [!TIP]
    > La configuración de la directiva de grupo para configurar Firewall de Windows puede invalidar la configuración establecida en Configuration Manager. Si usa directiva de grupo para configurar el Firewall de Windows, asegúrese de que la configuración de directiva de grupo no bloquea mstsc.exe.

    Si los clientes ejecutan otro firewall basado en host, configure manualmente esta dependencia del firewall.  

### <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

- Para que un usuario se conecte a un equipo del trabajo, dicho equipo debe ser un dispositivo primario del usuario. Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- Para administrar perfiles de conexión remota, la cuenta de usuario necesita permisos específicos en Configuration Manager. El rol integrado **Administrador de configuración de cumplimiento** incluye los permisos necesarios para administrar estos perfiles. Para obtener más información, vea [Configurar la administración basada en roles](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Consideraciones de seguridad y privacidad

### <a name="security-considerations"></a>Consideraciones de seguridad  

- Especifique manualmente la afinidad de dispositivo del usuario en lugar de permitir a los usuarios identificar su dispositivo primario. No habilite la configuración basada en el uso.

  - Para poder implementar un perfil de conexión remota, debe habilitar la opción **Permitir a todos los usuarios principales del equipo del trabajo conectarse remotamente**. Con esta configuración, siempre debe especificar manualmente la afinidad entre usuario y dispositivo. No considere información de autoridad aquella que Configuration Manager recopila de los usuarios o del dispositivo. Si implementa un perfil y un usuario administrativo de confianza no especifica la afinidad entre usuario y dispositivo, es posible que usuarios no autorizados reciban privilegios elevados y puedan conectarse de forma remota a los equipos.

  - Configuration Manager recopila información basada en el uso a través de mensajes de estado, que es un canal de comunicación rápido pero no seguro. Para mitigar esta amenaza, utilice la firma de bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre los equipos cliente y el punto de administración.

- Restringir los derechos de administración locales en el equipo del servidor de sitio. Un administrador local en el servidor de sitio puede agregar manualmente miembros al grupo de seguridad **Conexión a equipos remotos** que Configuration Manager crea y mantiene automáticamente. Esta acción puede causar una elevación de privilegios, ya que los miembros reciben permisos de Escritorio remoto.

### <a name="privacy-considerations"></a>Consideraciones de privacidad  

Cuando un usuario se conecta de forma remota a un equipo de trabajo, descarga un archivo. wsrdp. Este archivo contiene el nombre del dispositivo y el nombre del servidor de puerta de enlace de Escritorio remoto. Estos valores son necesarios para crear la sesión de Escritorio remoto. El archivo .wsrdp se descarga y se guarda automáticamente de forma local. El archivo se sobrescribirá la próxima vez que el usuario ejecute una sesión de Escritorio remoto.  

## <a name="create-a-profile"></a>Creación de un perfil

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione **Perfiles de conexión remota**.  

1. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear perfil de conexión remota**.  

1. En la página **General** del **Asistente para crear perfil de conexión remota**, especifique un nombre y una descripción opcional para el perfil. Ambos valores tienen un límite máximo de 256 caracteres.  

1. En la página **Configuración del perfil**, especifique esta configuración:  

    - **Nombre completo y puerto del servidor de puerta de enlace de Escritorio remoto (opcional)** : Especifique el nombre del servidor de puerta de enlace de Escritorio remoto para las conexiones. Este valor tiene estos requisitos:

        - El nombre del servidor no puede tener más de 256 caracteres.
        - Puede contener caracteres en mayúsculas, minúsculas y numéricos.
        - Aparte de los puntos (`.`) entre los segmentos y un signo de dos puntos (`:`) antes del puerto, los únicos caracteres especiales son los guiones (`–`) y los guiones bajos (`_`).
        - Configuration Manager no admite el uso de un nombre de dominio internacionalizado para este valor.

    - **Permitir conexiones solamente de equipos que ejecutan Escritorio remoto con Autenticación a nivel de red**: esta opción está habilitada de forma predeterminada y agrega un nivel de seguridad adicional para la conexión. Para más información, consulte cómo [conceder acceso de Escritorio remoto](/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Habilite esta configuración de conexión:

        - **Permitir conexiones remotas a equipos de trabajo**

        - **Permitir a todos los usuarios principales del equipo del trabajo conectarse remotamente**

        - **Permitir excepción de Firewall de Windows para conexiones en dominios de Windows y en redes privadas**

        > [!IMPORTANT]  
        > Las tres opciones deben ser iguales para poder continuar.

        Solo debe deshabilitar estas opciones cuando implemente un perfil para desactivar las conexiones remotas.

1. Complete el asistente.

El nuevo perfil se muestra en el nodo **Perfiles de conexión remota** en el área de trabajo **Activos y compatibilidad**.  

## <a name="deploy"></a>Implementar

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione **Perfiles de conexión remota**.

1. En la lista **Perfiles de conexión remota**, seleccione el perfil que quiere implementar. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Implementar**.  

1. En la ventana **Implementar perfil de conexión remota**, especifique la información siguiente:

    - **Colección**: examine para seleccionar la colección de dispositivos en la que quiere implementar el perfil.

    - **Corregir las reglas no compatibles cuando se admita**: habilite esta configuración para corregir automáticamente la configuración de perfil cuando no sea compatible en un dispositivo. El perfil puede ser no compatible cuando no existe.

    - **Permitir la corrección fuera de la ventana de mantenimiento**: si configura una ventana de mantenimiento para la colección donde implementa el perfil, habilite esta opción para permitir que Configuration Manager realice la corrección fuera de la ventana de mantenimiento. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).

    - **Generar una alerta**: habilite esta opción para configurar una alerta de cumplimiento.

    - **Especifique la programación de evaluación de compatibilidad para esta línea de base de configuración**: especifique una programación simple o personalizada mediante la cual el cliente evaluará el perfil.

1. Seleccione **Aceptar** para cerrar la ventana y crear la implementación.

### <a name="client-evaluation"></a>Evaluación del cliente

El cliente evalúa el perfil cuando un usuario inicia sesión.

Si un dispositivo deja una colección en la que se implementa un perfil de conexión remota, Configuration Manager deshabilita la configuración en el dispositivo. Sin embargo, para que esto se realice correctamente, debe haber implementado al menos un elemento de configuración o una línea de base de configuración que contenga un elemento de configuración del sitio.

### <a name="conflict-resolution"></a>Resolución de conflictos

No implemente más de un perfil de conexión remota con una configuración en conflicto en el mismo dispositivo. Por ejemplo, se implementan dos perfiles con configuraciones distintas en la misma colección. Solo se configura una implementación de perfil para **corregir las reglas no compatibles cuando se admita**. Esta implementación podría invalidar la configuración del otro perfil. Configuration Manager no admite este tipo de implementación de perfil de conexión remota.

## <a name="monitor"></a>Supervisión

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione **Implementaciones**. En la lista **Implementaciones**, seleccione la implementación del perfil de conexión remota.

Puede revisar la información de resumen sobre la compatibilidad de la implementación del perfil de conexión remota en la página principal. Para ver información más detallada, seleccione la implementación del perfil. Luego, en la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Ver estado**. Esta acción abre la página **Estado de la implementación**.  

La página **Estado de implementación** contiene las siguientes pestañas:  

- **Conforme**: muestra el cumplimiento del perfil de conexión remota en función del número de recursos afectados.

    > [!IMPORTANT]  
    > El cliente no evalúa un perfil de conexión remota si no es aplicable. Sin embargo, sigue informando que es compatible.

- **Error**: muestra una lista de todos los errores de la implementación seleccionada del perfil de conexión remota, en función del número de recursos afectados.

- **No conforme**: muestra una lista de todas las reglas no compatibles en el perfil de conexión remota en función del número de recursos afectados.

- **Desconocido**: muestra una lista de todos los dispositivos que no notificaron el cumplimiento de la implementación seleccionada del perfil de conexión remota y el estado actual del cliente de los dispositivos.

En cualquier pestaña, abra una regla para crear un subnodo temporal en el nodo **Usuarios** en el área de trabajo **Activos y compatibilidad**. Este subnodo contiene todos los dispositivos con el estado de cumplimiento de la pestaña seleccionada.

En el panel **Detalles del activo** se muestran los dispositivos con el estado de cumplimiento seleccionado para este perfil. Abra un dispositivo de la lista para mostrar más información.

## <a name="reports"></a>Informes

Configuration Manager incluye informes integrados que se pueden usar para supervisar la información de perfiles de conexión remota. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
> Use el carácter comodín (`%`) cuando use los parámetros **Filtro del dispositivo** y **Filtro de usuarios** en los informes de configuración de cumplimiento.  

Para obtener más información sobre cómo configurar informes en Configuration Manager, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).