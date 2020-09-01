---
title: Configurar Wake On LAN
titleSuffix: Configuration Manager
description: Seleccione la configuración de Wake On LAN en Configuration Manager.
ms.date: 08/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 33283b13bc28c7d102f014ac3cb4048681343ac2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907854"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Cómo configurar Wake On LAN en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Especifique la configuración de Wake On LAN para Configuration Manager cuando quiera desactivar el estado de suspensión de los equipos.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a> Wake on LAN a partir de la versión 1810
<!--3607710-->
A partir de Configuration Manager 1810, hay una manera nueva de reactivar los equipos en suspensión. Puede reactivar clientes desde la consola de Configuration Manager aunque el cliente no esté en la misma subred que el servidor de sitio. Si necesita realizar tareas de mantenimiento o consultar dispositivos, no se ve limitado por los clientes remotos que están inactivos. El servidor de sitio usa el canal de notificación de cliente para identificar otros clientes que están activos en la misma subred remota y usa a esos clientes para enviar una solicitud de activación por LAN (paquete mágico). Usar el canal de notificación de cliente ayuda a evitar oscilaciones de la dirección MAC, que podrían provocar que el enrutador apague el puerto. La nueva versión de Wake on LAN se puede habilitar al mismo tiempo que la [versión anterior](#bkmk_wol-previous).

### <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones
<!--7323898, 7363492-->
- Al menos un cliente en la subred de destino debe estar activo.
- Esta característica no es compatible con las siguientes tecnologías de red:
   - IPv6
   - Autenticación de red 802.1x
    >[!NOTE]
    > La autenticación de red 802.1X puede funcionar con una configuración adicional, dependiendo del hardware y su configuración.
- Los equipos solo se reactivan cuando reciben la notificación de cliente **Reactivar**.
    - Para realizar una reactivación cuando se alcanza una fecha límite, se usa la versión anterior de Wake on LAN.
    -  Si no está habilitada la versión anterior, no se producirá la reactivación del cliente para las implementaciones creadas con la configuración **Usar Wake-on-LAN para activar clientes para las implementaciones requeridas** o **Enviar paquetes de reactivación**.  
- La duración de la concesión de DHCP no se puede establecer en infinita. <!--8018584-->
   - Es posible que vea que SleepAgent_&lt;*dominio*\>@SYSTEM_0.log se vuelva muy grande y, posiblemente, una tormenta de difusión en entornos en los que las concesiones de DHCP están configuradas con duración infinita.  

### <a name="security-role-permissions"></a>Permisos del rol de seguridad

- **Notificar a los recursos** en la categoría de colección

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Configuración de los clientes para usar Wake on LAN a partir de la versión 1810

Anteriormente tenía que habilitar manualmente el cliente para activar la LAN en las propiedades del adaptador de red. Configuration Manager 1810 incluye una nueva configuración del cliente llamada **Permitir reactivación de red**. Configure e implemente esta configuración en lugar de modificar las propiedades del adaptador de red.

1. En **Administración**, vaya a **Configuración de cliente**.
1. Seleccione la configuración de cliente que desea editar o cree una configuración de cliente personalizada para implementarla. Para obtener más información, vea [Cómo configurar el cliente](configure-client-settings.md).
1. En la configuración de cliente **Administración de energía**, seleccione **Habilitar** para la configuración **Permitir reactivación de red**. Para más información sobre esta configuración, vea [Acerca de la configuración de cliente](about-client-settings.md#power-management).

4. A partir de Configuration Manager 1902, la nueva versión de Wake On LAN respeta el puerto UDP personalizado que especifique en la [opción de cliente](about-client-settings.md#power-management)**Número de puerto de Wake On LAN (UDP)** . Esta configuración se comparte entre la versión anterior y la nueva de Wake on LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Reactivación de un cliente mediante la notificación de cliente a partir de 1810
 
Puede reactivar un único cliente o cualquier cliente en suspensión de una colección. Para los dispositivos que ya están activos en la colección, no se realiza ninguna acción para ellos. Solo a los clientes inactivos se les enviará una solicitud de Wake on LAN. Para más información sobre cómo notificar la reactivación a un cliente, vea [Notificación de cliente](../manage/client-notification.md).

- **Para reactivar un solo cliente**: Haga clic con el botón derecho en el cliente, vaya a **Notificación de cliente** y, después, seleccione **Reactivar**.

   ![Notificación de cliente para reactivación en la consola](media/wol-wake-up-client-notification.png)

- **Para reactivar todos los clientes en suspensión en una colección**: Haga clic con el botón derecho en la colección de dispositivos, vaya a **Notificación de cliente** y, después, seleccione **Reactivar**.
   - Esta acción no se puede ejecutar en las colecciones integradas.
   - Cuando hay una combinación de clientes inactivos y activos en una colección, solo se envía una solicitud de Wake on LAN a los clientes inactivos.
   - A partir de Configuration Manager 2002, esta acción está disponible desde una consola conectada a un sitio de administración central, un sitio independiente o un sitio primario secundario.
   - En las versiones 1910 y anteriores, esta acción solo está activa cuando la consola de Configuration Manager está conectada a un sitio primario independiente o secundario. Cuando está conectada a un sitio de administración central, la acción no está disponible.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Qué esperar cuando se habilita solo la nueva versión de Wake on LAN

Si solo está habilitada la nueva versión de Wake on LAN, solo se habilita la notificación de cliente **Reactivar**. A los clientes no se les envía una notificación cuando se recibe una fecha límite para las implementaciones, como las secuencias de tareas, la distribución de software o la instalación de las actualizaciones de software. Una vez que el equipo suspendido vuelve a estar en línea, se reflejará en la consola cuando se registre con el punto de administración.

A partir de Configuration Manager versión 1902, puede especificar el puerto de Wake on LAN. Esta configuración se comparte entre la versión anterior y la nueva de Wake on LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Qué esperar cuando se habilitan ambas versiones de Wake on LAN

Cuando tiene ambas versiones de Wake on LAN habilitadas, puede usar la notificación de cliente **Reactivar** para realizar la reactivación en la fecha límite. La notificación de cliente funciona de manera un poco diferente a la versión tradicional de Wake on LAN. Para obtener una breve explicación de cómo funciona la notificación de cliente, vea la sección [Wake on LAN a partir de la versión 1810](#bkmk_wol-1810). La nueva configuración de cliente **Permitir reactivación de red** cambiará las propiedades de la NIC para permitir Wake on LAN. Ya no necesite cambiarla manualmente para los equipos nuevos que se agregan a su entorno. Todas las demás funcionalidades de Wake on LAN no se han modificado.

A partir de la versión 1902, la notificación de cliente **Reactivar** respeta la configuración existente **Número de puerto de Wake on LAN (UDP)**.


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a> Wake on LAN para la versión 1806 y versiones anteriores

Especifique la configuración de Wake On LAN para Configuration Manager si quiere reactivar los equipos que están en estado de suspensión para instalar el software necesario, por ejemplo, actualizaciones de software, aplicaciones, secuencias de tareas y programas.

Puede complementar Wake On LAN mediante la configuración de cliente de proxy de reactivación. No obstante, para usar el proxy de reactivación, primero debe habilitar Wake On LAN para el sitio y especificar **Usar paquetes de reactivación solamente** y la opción **Unidifusión** para el método de transmisión de Wake On LAN. Esta solución de reactivación también admite conexiones ad hoc, por ejemplo, una conexión a Escritorio remoto.

Utilice el primer procedimiento para configurar un sitio primario para Wake On LAN. Luego, use el segundo procedimiento para especificar la configuración de cliente de proxy de reactivación. Este segundo procedimiento configura las opciones de cliente predeterminadas para la configuración de proxy de reactivación que se aplicarán a todos los equipos de la jerarquía. Si desea que esta configuración solo se aplique a equipos seleccionados, cree una configuración de dispositivo personalizada y asígnela a una recopilación que contenga los equipos que desea configurar para el proxy de reactivación. Para más información sobre cómo crear configuraciones de cliente personalizadas, vea [Cómo establecer la configuración de cliente](../../../core/clients/deploy/configure-client-settings.md).

Un equipo que recibe la configuración de cliente de proxy de reactivación es probable que detenga su conexión de red entre 1 y 3 segundos. Esto ocurre porque el cliente debe restablecer la tarjeta de interfaz de red para habilitar el controlador de proxy de reactivación en ella.

> [!WARNING]
> Para evitar una interrupción inesperada en los servicios de red, primero evalúe el proxy de reactivación en una infraestructura de red aislada y representativa. A continuación, utilice la configuración de cliente personalizada para expandir la prueba a un grupo seleccionado de equipos en varias subredes. Para más información sobre cómo funciona el proxy de reactivación, vea [Planear la reactivación de clientes](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Para configurar Wake on LAN para un sitio en la versión 1806 y versiones anteriores

 Para usar Wake on LAN, necesita habilitarlo para cada sitio de una jerarquía.

1. En la consola de Configuration Manager, vaya a **Administración > Configuración del sitio > Sitios**.
2. Haga clic en el sitio primario para configurar y, luego, haga clic en **Propiedades**.
3. Haga clic en la pestaña **Wake on LAN** y configure las opciones que necesite para este sitio. Para admitir el proxy de reactivación, asegúrese de seleccionar **Usar paquetes de reactivación solamente** y **Unidifusión**. Para obtener más información, vea [Planear la reactivación de clientes](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Haga clic en **Aceptar** y repita este procedimiento para todos los sitios primarios de la jerarquía.

![Habilitar Wake on LAN en las propiedades del sitio](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Para configurar el cliente proxy de reactivación

1. En la consola de Configuration Manager, vaya a **Administración > Configuración de cliente**.
2. Haga clic en **Configuración de cliente predeterminada** y luego en **Propiedades**.
3. Seleccione **Administración de energía** y luego elija **Sí** para **Habilitar proxy de reactivación**.
4. Revise y, si es necesario, configure las demás opciones del proxy de reactivación. Para más información sobre esta configuración, vea la [configuración de administración de energía](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo y, a continuación, haga clic en **Aceptar** para cerrar el cuadro de diálogo Configuración de cliente predeterminada .

Puede utilizar los siguientes informes de Wake On LAN para supervisar la instalación y la configuración del proxy de reactivación:

- Resumen de estado de implementación de proxy de reactivación
- Detalles de estado de implementación de proxy de reactivación

> [!TIP]
> Para comprobar si el proxy de reactivación está en funcionamiento, pruebe la conexión en un equipo inactivo. Por ejemplo, establezca una conexión con una carpeta compartida en ese equipo o intente conectarse al equipo mediante Escritorio remoto. Si usa Direct Access, compruebe que los prefijos IPv6 funcionan realizando las mismas pruebas para un equipo inactivo que se encuentra actualmente en Internet.
