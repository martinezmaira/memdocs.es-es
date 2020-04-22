---
title: Atestación de estado
titleSuffix: Configuration Manager
description: Obtenga información sobre la funcionalidad de atestación de estado de dispositivos que puede verse en la consola de Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9917ec8a1ed2072903276de438f49d3f783a1284
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692613"
---
# <a name="health-attestation-for-configuration-manager"></a>Atestación de estado para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los administradores pueden ver el estado de la [atestación de estado de los dispositivos de Windows 10](https://technet.microsoft.com/library/mt592023.aspx) en la consola de Configuration Manager.  La atestación de estado del dispositivo permite al administrador garantizar que los equipos cliente tienen habilitadas las siguientes configuraciones BIOS, TPM y de software de arranque de confianza:  

-   Antimalware de inicio temprano: el antimalware de inicio temprano (ELAM) protege su equipo cuando se inicia y antes de inicializar controladores de terceros. [Cómo activar ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker: el Cifrado de unidad BitLocker de Windows es un software que permite cifrar todos los datos almacenados en el volumen del sistema operativo Windows.  [Activación de Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Arranque seguro: el arranque seguro es un estándar de seguridad desarrollado por miembros de la industria de PC para ayudar a garantizar que el equipo arranca solo con el software que el fabricante indica como confiable. [Más información sobre el arranque seguro](https://technet.microsoft.com/library/hh824987.aspx)  
-   Integridad de código: la integridad de código es una característica que mejora la seguridad del sistema operativo al validar la integridad de un controlador o un archivo del sistema cada vez que se carga en memoria. [Más información sobre la integridad de código](https://technet.microsoft.com/library/dd348642.aspx)  

Esta funcionalidad está disponible para equipos y recursos locales administrados por Configuration Manager y dispositivos móviles administrados con Microsoft Intune. Los administradores pueden especificar si la notificación se realiza a través de la nube o de la insfraestructura local. La supervisión de la atestación de estado de dispositivo local permite al administrador supervisar los equipos cliente sin acceso a Internet.

## <a name="enable-health-attestation"></a>Habilitar la atestación de estado

 **Requisitos:**  

-   Dispositivos cliente que ejecutan la versión 1607 de Windows 10 o la versión 1607 de Windows Server 2016 con la [Atestación de estado de dispositivo habilitada](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation).
-   Dispositivos habilitados para TPM 1.2 o TPM 2.
-   Si se usa la administración en la nube, comunicación entre el agente cliente de Configuration Manager y el punto de administración con el servicio Atestación de estado (administración en la nube) de *has.spserv.microsoft.com* (puerto 443). Si es local, el cliente debe poder comunicarse con el punto de administración habilitado para la Atestación de estado de dispositivo.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Cómo habilitar la comunicación del servicio de atestación de estado en los equipos cliente de Configuration Manager

Utilice este procedimiento para habilitar la supervisión de atestación de estado de dispositivo para dispositivos que se conectan a Internet.

1.  En la consola de Configuration Manager, elija **Administración** > **Introducción** > **Configuración de cliente**.  Seleccione la pestaña para configurar el **agente de equipo** .  
2.  En el cuadro de diálogo **Configuración predeterminada** , seleccione **Agente de equipo** y después desplácese hacia abajo hasta **Habilitar comunicación con el servicio de atestación de estado**.  
3.  Establezca **Habilitar comunicación con el servicio de atestación de estado** en **Sí**y luego haga clic en **Aceptar**.  
4. Diríjase a las colecciones de dispositivos que deben notificar el estado del dispositivo.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Cómo habilitar la comunicación del servicio de atestación de estado local en los equipos cliente de Configuration Manager
Utilice este procedimiento para habilitar la supervisión de atestación de estado de dispositivo para dispositivos locales que no se conectan a Internet.

A partir de Configuration Manager 1702, la dirección URL del servicio de atestación de estado de dispositivo puede configurarse en el punto de administración para admitir dispositivos cliente sin acceso a Internet.

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración del sitio** > **Sitios**.
2. Haga clic con el botón derecho en el sitio primario o secundario con el punto de administración que admite clientes de atestación de estado de dispositivo local y seleccione **Configurar componentes de sitio** > **Punto de administración**. Se abre la página **Propiedades de componente de punto de administración**.
3. En la pestaña **Opciones avanzadas**, seleccione **Agregar** y especifique una dirección URL del servicio de atestación de estado de dispositivo local válida. Puede agregar varias direcciones URL. Si se especifican varias direcciones URL locales, los clientes reciben el conjunto completo y eligen aleatoriamente cuál desea utilizar.
4.  En la consola de Configuration Manager, elija **Administración** > **Introducción** > **Configuración de cliente**.  Seleccione la pestaña para configurar el **agente de equipo** .  
5.  Desplácese hacia abajo para **Habilitar comunicación con el servicio de atestación de estado** y establezca la opción en **Sí**.
7.  Haga clic en la opción **Usar un servicio de atestación de mantenimiento local** y establézcala en **Sí**.
8. Diríjase a las colecciones de dispositivos que deben notificar el estado de dispositivo con la configuración del agente cliente para habilitar los informes de atestación de estado de dispositivo.

También puede **editar** o **quitar** direcciones URL del servicio de atestación de estado de dispositivo.

> [!NOTE]
> Si utiliza la atestación de estado de dispositivo antes de actualizar a Configuration Manager 1702, las direcciones URL locales especificadas en la configuración del agente cliente se rellena previamente en las propiedades del punto de administración durante la actualización. Los clientes locales continuarán usando la dirección URL especificada en la configuración del agente cliente hasta que se actualicen. Después cambiarán a una de las direcciones URL especificadas en el punto de administración.

## <a name="monitor-device-health-attestation"></a>Supervisión de atestación de estado de dispositivo

1.  Para ver la atestación de estado de dispositivo, en la consola de Configuration Manager, vaya al área de trabajo de **Supervisión** , haga clic en el nodo **Seguridad** y luego haga clic en **Atestación de estado**.  
2.  Se muestra la atestación de estado de dispositivo.  

La atestación de estado de dispositivos de Configuration Manager muestra lo siguiente:  

-   **Estado de la atestación de estado** : muestra la cantidad de dispositivos que presentan estados de conformidad, no conformidad, error y desconocido.  
-   **Dispositivos que informan de la atestación de estado** : muestra el porcentaje de dispositivos que informan sobre el estado de la atestación de estado.  
-   **Dispositivos no compatibles ordenados por tipo de cliente** : muestra la proporción de dispositivos móviles y equipos que no son compatibles.  
-   **Principales opciones de configuración ausentes de la atestación de estado** : muestra el número de dispositivos que carecen de opciones de configuración de atestación de estado, que se indican por cada opción.
