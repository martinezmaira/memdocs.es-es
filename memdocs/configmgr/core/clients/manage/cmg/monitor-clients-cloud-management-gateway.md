---
title: Supervisión de la puerta de enlace de administración de nube
titleSuffix: Configuration Manager
description: Supervise los clientes y el tráfico de red a través de Cloud Management Gateway (CMG).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695153"
---
# <a name="monitor-cloud-management-gateway"></a>Supervisión de la puerta de enlace de administración de nube

*Se aplica a: Configuration Manager (rama actual)*

Después de que se ejecute la instancia de Cloud Management Gateway (CMG) y los clientes se conecten a través de ella, se pueden supervisar los clientes y el tráfico de red para asegurarse de que se sabe cómo está funcionando el servicio.


## <a name="monitor-clients"></a>Supervisar clientes

Los clientes conectados mediante la instancia de CMG aparecen en la consola de Configuration Manager de la misma manera que los clientes locales. Para obtener más información, consulte [Supervisar clientes en System Center Configuration Manager](../monitor-clients.md).


## <a name="monitor-traffic-in-the-console"></a>Supervisar el tráfico en la consola

Puede supervisar el tráfico en la instancia de CMG con la consola de Configuration Manager:

1. Vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  

2. Seleccione CMG en el panel de lista.  

3. Vea la información de tráfico en el panel de detalles para el punto de conexión de la instancia de CMG y los roles de sistema de sitio a los que se conecta. Estas estadísticas muestran las solicitudes de cliente que llegan a estos roles. Las solicitudes incluyen notificaciones de cliente, inventario, contenido, registro, ubicación y directiva.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfico de salida

Las alertas de tráfico de salida ayudan a saber el momento en el que el tráfico se acerca a un nivel de umbral de 14 días. Al crear la instancia de CMG, se pueden configurar alertas de tráfico. Si omite esa parte, todavía puede configurar las alertas después de que se ejecute el servicio. Ajuste la configuración de alertas en cualquier momento.

1. Vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  

2. Seleccione la instancia de CMG en el panel de lista y después seleccione **Propiedades** en la cinta de opciones.  

3. Vaya a la pestaña **Alertas** para habilitar el umbral y las alertas. Especifique el umbral de datos de 14 días en gigabytes (GB). Especifique también el porcentaje de umbral para elevar los distintos niveles de alerta.  

4. Cuando haya terminado, seleccione **Aceptar**.  


## <a name="monitor-logs"></a>Supervisar los registros

La instancia de CMG genera entradas en una serie de archivos de registro. Para obtener más información, consulte [Archivos de registro en System Center Configuration Manager](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Panel de administración en la nube

<!--1358461-->
A partir de la versión 1806, el panel de administración en la nube proporciona una vista centralizada para el uso de CMG. Cuando el sitio está incorporado a [servicios de Azure](../../../servers/deploy/configure/azure-services-wizard.md) para la administración en la nube, también muestra los datos sobre los usuarios en la nube y los dispositivos.  

La captura de pantalla siguiente es una parte del panel de administración en la nube que muestra dos de los iconos disponibles:  
![Iconos del panel de administración: Tráfico de CMG y Clientes en línea actuales](media/1358461-cmg-dashboard.png)

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Seleccione el nodo **Administración en la nube** y vea los iconos del panel.  


## <a name="connection-analyzer"></a>Analizador de conexión

A partir de la versión 1806, use el analizador de conexión de CMG para la comprobación en tiempo real que ayuda a solucionar problemas. La utilidad en la consola comprueba el estado actual del servicio y el canal de comunicación a través del punto de conexión de CMG a todos los puntos de administración que permiten el tráfico CMG.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  

2. Seleccione la instancia de CMG de destino y luego seleccione **Analizador de conexión** en la cinta.  

3. En la ventana del analizador de conexión de CMG, seleccione una de las siguientes opciones para autenticarse con el servicio:  

     1. **Usuario de Azure AD**: use esta opción para simular la comunicación de la misma manera que una identidad de usuario basado en la nube que ha iniciado sesión en un dispositivo con Windows 10 unido a Azure AD. Haga clic en **Iniciar sesión** para escribir las credenciales de forma segura para esta cuenta de usuario de Azure AD.  

     2. **Certificado de cliente**: utilice esta opción para simular la comunicación de la misma manera que un cliente de Configuration Manager con un [certificado de autenticación del cliente](certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Seleccione **Iniciar** para iniciar el análisis. Los resultados se muestran en la ventana del analizador. Seleccione una entrada para ver más detalles en el campo Descripción.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a> Detener CMG cuando se supere el umbral

<!--3735092-->
A partir de la versión 1902, Configuration Manager ahora puede detener un servicio de Cloud Management Gateway (CMG) cuando a transferencia de datos total supera el límite. Use las [alertas](#set-up-outbound-traffic-alerts) para desencadenar las notificaciones cuando el uso alcanza niveles críticos o de advertencia. Para lograr reducir los costos de Azure inesperados debido a un pico de uso, esta opción desactiva el servicio en la nube.

> [!Important]  
> Aunque no se esté ejecutando el servicio, sigue habiendo costos asociados con el servicio en la nube. Si se detiene el servicio no se eliminan todos los costos de Azure asociados. Para quitar todos los costos del servicio en la nube, [quite la instancia de CMG](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> Cuando se detiene el servicio CMG, los clientes basados en Internet no pueden comunicarse con Configuration Manager.  

La transferencia de datos total (salida) incluye datos de la cuenta de almacenamiento y de servicio en la nube. Estos datos proceden de los siguientes flujos:

- CMG al cliente  
- CMG al sitio, incluidos los archivos de registro de CMG  
- Si habilita CMG para la cuenta de almacenamiento de contenido al cliente  

Para más información sobre estos flujos de datos, vea [Puertos y flujo de datos de CMG](plan-cloud-management-gateway.md#ports-and-data-flow).

El umbral de alerta de almacenamiento es independiente. Esta alerta supervisa la capacidad de la instancia de almacenamiento de Azure.

Al seleccionar la instancia de CMG en el nodo **Cloud Management Gateway** de la consola, puede ver la transferencia total de datos en el panel de detalles.

Configuration Manager comprueba el valor de umbral cada seis minutos. Si se produce un pico repentino en el uso, Configuration Manager puede tardar hasta seis minutos en detectar si se superó el umbral y detener el servicio.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Proceso para detener el servicio en la nube cuando se supera el umbral

1. [Configurar alertas de tráfico de salida](#set-up-outbound-traffic-alerts).  

2. En la pestaña **Alertas** de la ventana de propiedades de CMG, habilite la opción para **Detener este servicio cuando se supera el umbral crítico**.  

Para probar esta característica, reduzca temporalmente uno de estos valores:  

- **Umbral de 14 días para transferencia de datos de salida (GB)** . El valor predeterminado es `10000`.  

- **Porcentaje de umbral para generar una alerta crítica**. El valor predeterminado es `90`.  
