---
title: Supervisar clientes
titleSuffix: Configuration Manager
description: Obtenga información detallada acerca de cómo supervisar clientes en Configuration Manager
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a10e169db36c62b083c56114159b54185a1040
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2020
ms.locfileid: "87525920"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Supervisión de clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Una vez que instale el cliente de Configuration Manager en los dispositivos Windows de su sitio, supervise su estado y la actividad en la consola de Configuration Manager.  


## <a name="about-client-status"></a><a name="bkmk_about"></a> Acerca del estado de cliente

Configuration Manager proporciona los siguientes tipos de información como estado de cliente:  

- **Estado de conexión de clientes**: El sitio considera que un dispositivo está **en línea** si está conectado a su punto de administración asignado. Para indicar que el cliente está en línea, envía mensajes de estilo ping al punto de administración. Si el punto de administración no recibe un mensaje después de cinco minutos, el sitio considera al cliente **sin conexión**.  

- **Actividad de cliente**: El sitio considera que el cliente está **activo** si se ha comunicado con Configuration Manager en los últimos siete días. El sitio considera que el cliente está **inactivo** si no ha realizado las siguientes acciones en siete días:  

    - Solicitud de actualización de directiva  
    - Envío de mensaje de latido  
    - Envío de inventario de hardware  

- **Comprobación de cliente**: El estado de la evaluación periódica que el cliente de Configuration Manager ejecuta en el dispositivo. La evaluación comprueba el dispositivo y puede corregir algunos de los problemas que encuentre. Para obtener más información, vea [Comprobaciones del estado del cliente](#BKMK_ClientHealth).  

     En los dispositivos que ejecutan Windows 7, la comprobación de cliente se ejecuta como una tarea programada. En las versiones de sistemas operativos posteriores, la comprobación de cliente se ejecuta automáticamente en la ventana de mantenimiento de Windows.  

     Puede configurar la corrección para que no se ejecute en dispositivos específicos, por ejemplo, un servidor crítico del negocio. Si hay elementos adicionales que desee a evaluar, utilice la configuración de cumplimiento de Configuration Manager para supervisar las configuraciones adicionales. Para obtener más información sobre la configuración de cumplimiento, consulte [Planear y configurar la configuración de cumplimiento](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

- **Dado de baja**: El sitio ha marcado el registro del dispositivo para su eliminación. Este comportamiento puede ocurrir cuando se asigna un nuevo registro para el mismo dispositivo al mismo sitio primario o a uno diferente en una jerarquía. El sitio elimina estos dispositivos la próxima vez que ejecute la tarea de mantenimiento **Eliminar datos de detección antiguos**.<!-- SCCMDocs issue #1418 -->  

- **Obsoleto**: El sitio ha detectado un nuevo registro de dispositivo con el mismo identificador de hardware, por lo que marca el registro anterior como obsoleto. Los informes no cuentan los registros obsoletos del mismo dispositivo varias veces. Puede seguir destinando directivas a dispositivos obsoletos. Si el sitio no recibe un latido para un registro obsoleto después de 90 días de inactividad, quita el dispositivo obsoleto cuando se ejecuta la tarea de mantenimiento **Eliminar datos obsoletos de detección de cliente**.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a> Supervisión de clientes individuales

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Seleccione el nodo **Dispositivos** o elija una recopilación en **Recopilaciones de dispositivos**.  

    Los iconos al principio de cada fila indican el estado de conexión del dispositivo:  

    | Icono | Descripción |
    | ---- | ----------- |  
    |![icono de estado conectado para los clientes](../../../core/clients/manage/media/online-status-icon.png)|El dispositivo está conectado|  
    |![icono de estado desconectado para los clientes](../../../core/clients/manage/media/offline-status-icon.png)|El dispositivo está desconectado|  
    |![icono de estado desconocido para los clientes](../../../core/clients/manage/media/unknown-status-icon.png)|Se desconoce el estado de conexión|  
    |![cliente no instalado](../../../core/clients/manage/media/client-not-installed.png)|El cliente no está instalado en el dispositivo|  

2. Para obtener el estado en línea más detallado, agregue la información del estado de conexión del cliente a la vista del dispositivo. Haga clic derecho en el encabezado de columna y seleccione los campos del estado de conexión que desea agregar:

    - **Estado de conexión del dispositivo**: Indica si el cliente está actualmente conectado o no. (Esta es la misma información proporcionada por los iconos).  

    - **Última hora en línea**: Indica cuándo cambió el estado de conexión del cliente a conectado.  

    - **Última hora sin conexión** indica cuándo cambió el estado a sin conexión  

3. Seleccione un cliente individual en el panel de lista para ver más estado en el panel de detalles. Esta información incluye la actividad y el estado de comprobación del cliente.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a> Panel de mantenimiento del cliente

<!--3599209-->
Se implementan actualizaciones de software y se usan otras aplicaciones para proteger el entorno, pero estas implementaciones solo llegan a clientes correctos. Los clientes incorrectos de Configuration Manager afectan negativamente al cumplimiento general. ¿Considera que determinar el estado del cliente puede resultar complicado según el denominador "número total de dispositivos que deben estar en el ámbito de administración"? Por ejemplo, si detecta todos los sistemas de Active Directory, incluso si algunos de esos registros son para máquinas retiradas, este proceso aumenta el denominador.

A partir de la versión 1902, puede ver un panel con información sobre el estado de los clientes de Configuration Manager en su entorno. Allí puede ver el estado del cliente, el estado de escenario y errores comunes. Filtre la vista por varios atributos distintos para ver los posibles problemas con las versiones del sistema operativo y de cliente.

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Expanda **Estado del cliente** y seleccione el nodo **Panel de mantenimiento del cliente**.

![Captura de pantalla del panel de mantenimiento del cliente](media/3599209-client-health-dashboard.png)

> [!Tip]  
> No hay cambios en ccmeval.  

De forma predeterminada, el panel de mantenimiento del cliente muestra los clientes en línea y los clientes activos en los últimos tres días. Por lo tanto, puede ver números diferentes en este panel que en otros orígenes históricos del mantenimiento del cliente. Por ejemplo, otros nodos bajo **Estado del cliente**, o informes en la categoría del estado de cliente.

### <a name="filters"></a>Filtros

En la parte superior del panel, hay un conjunto de filtros para ajustar los datos mostrados en el panel.

- **Colección**: de forma predeterminada, el panel muestra los dispositivos de la colección **Todos los sistemas**. Seleccione una recopilación de dispositivos en la lista para definir el ámbito de la vista a un subconjunto de dispositivos de una colección específica.  

- **Con conexión/sin conexión**: de forma predeterminada, el panel muestra solo los clientes en línea. Este estado procede del canal de notificación de cliente que actualiza el estado de un cliente cada cinco minutos. Para más información, vea [Acerca del estado de cliente](monitor-clients.md#bkmk_about).  

- **Activo \# días**: de manera predeterminada, el panel muestra los clientes que están activos en los últimos tres días.  

- **Solo error**: define el ámbito de la vista únicamente a los dispositivos que notifican un error de estado de cliente.  

    > [!Tip]  
    > Puede usar este filtro junto con los iconos de versión de cliente y versión de sistema operativo. Para más información, vea [Iconos de versión](#version-tiles).

### <a name="client-health-percentage"></a>Porcentaje de estado de cliente

Este icono muestra el estado general del cliente en la jerarquía.

Un cliente correcto de Configuration Manager presenta estas propiedades:

- En línea  
- Envía datos de forma activa  
- Pasa todas las comprobaciones de evaluación de estado del cliente  

Para más información, vea [Acerca del estado de cliente](monitor-clients.md#bkmk_about).

Un cliente correcto se comunica correctamente con el sitio. Informa de todos los datos según las programaciones definidas en la configuración del cliente.

Seleccione un segmento de este gráfico para explorar desagrupando datos de una vista de lista de dispositivos.

### <a name="version-tiles"></a>Iconos de versión

Hay dos iconos que muestran el estado del cliente por la versión del cliente de Configuration Manager y la versión del sistema operativo. Estos iconos son útiles cuando se realizan cambios en los filtros, como **Solo error**. Pueden ser útiles para resaltar si los problemas son coherentes en una versión específica. Use esta información para tomar decisiones sobre la actualización de forma más sencilla.

Seleccione un segmento de estos gráficos para explorar desagrupando datos de una vista de lista de dispositivos.

### <a name="scenario-health"></a>Mantenimiento de escenarios

Este gráfico de barras muestra el estado general de los siguientes escenarios principales:

- Directiva de cliente
- Detección de latidos
- Inventario de hardware
- Inventario de software
- Mensajes de estado

Use los selectores para ajustar el foco en escenarios concretos en el gráfico.

Siempre se muestran las dos barras siguientes:

- **Combinados (Todos)** : combinación de todos los escenarios (AND)  
- **Combinados (Cualquiera)** : al menos uno de los escenarios (OR)

> [!Tip]  
> El mantenimiento de escenarios no se mide desde la configuración de las opciones del cliente. Estos valores pueden variar según el conjunto resultante de directivas por dispositivo. Siga estos pasos para ajustar los períodos de evaluación de mantenimiento de escenarios:
>
> - En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del cliente**.  
> - En la cinta de opciones, seleccione **Configuración de estado de cliente**.  
>
> De forma predeterminada, si un cliente no envía datos específicos del escenario en **7 días**, Configuration Manager lo considera incorrecto para ese escenario.

### <a name="top-10-client-health-failures"></a>Principales 10 errores de estado de cliente

En este gráfico se muestran los errores más comunes en su entorno. Estos errores proceden de Windows o Configuration Manager.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Supervisión del estado de todos los clientes

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del cliente**. Revise las estadísticas generales de actividad del cliente y comprobaciones de cliente en todo el sitio. Cambie el ámbito de la información eligiendo una recopilación diferente.  

2. Para profundizar en los detalles sobre las estadísticas notificadas, elija el nombre de la información notificada. Por ejemplo, **clientes activos que han pasado la comprobación de cliente o que no han obtenido resultados**. A continuación, revise la información acerca de los clientes individuales.  

3. Seleccione **Actividad de cliente** para ver gráficos que representan la actividad del cliente en su sitio de Configuration Manager.  

4. Seleccione **Comprobación de cliente** para ver gráficos que representan el estado de las comprobaciones de cliente en el sitio de Configuration Manager.  

    Configure alertas que le avisen cuando la actividad del cliente o los resultados de la comprobación del cliente caigan por debajo de un porcentaje especificado. El sitio también le alerta cuando se produce un error de corrección en un porcentaje específico de clientes. Para obtener más información, vea [Cómo configurar el estado de cliente](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a> Comprobaciones del estado del cliente

La comprobación del cliente ejecuta las siguientes comprobaciones y correcciones:  

|Comprobación de cliente|Acción correctiva|Más información|  
|------------------|------------------------|----------------------|  
|Comprobar que la comprobación de cliente se ha ejecutado recientemente|Ejecutar la comprobación de cliente|Comprueba que la comprobación del cliente ha ejecutado al menos una vez en los últimos tres días.|  
|Comprobar que están instalados los requisitos previos de cliente|Instalar los requisitos previos de cliente|Comprueba que están instalados los requisitos previos de cliente. Lee el archivo ccmsetup.xml en la carpeta de instalación de cliente para detectar los requisitos previos.|  
|Prueba de integridad del repositorio WMI.|Reinstalar el cliente de Configuration Manager|Comprueba que las entradas de cliente de Configuration Manager están presentes en WMI.|  
|Comprobar que el servicio de cliente se está ejecutando|Iniciar el servicio de cliente (Host de agente de SMS)|Sin información adicional|  
|Prueba de receptor de eventos WMI.|Reiniciar el servicio de cliente|Comprobar si se ha perdido el receptor de eventos WMI de Configuration Manager|  
|Comprobar que existe el servicio Instrumental de administración de Windows (WMI)|No hay corrección|Sin información adicional|  
|Comprobar que el cliente se instaló correctamente|Volver a instalar el cliente|Sin información adicional|  
|Comprobar que el tipo de inicio del servicio antimalware sea automático|Restablecer el tipo de inicio de servicio a automático|Sin información adicional|  
|Comprobar que el servicio antimalware se está ejecutando|Iniciar el servicio antimalware|Sin información adicional|  
|Comprobar que el tipo de inicio del servicio Windows Update sea automático o manual|Restablecer el tipo de inicio de servicio a automático|Sin información adicional|  
|Comprobar que el tipo de inicio del servicio de cliente (Host de agente de SMS) sea automático|Restablecer el tipo de inicio de servicio a automático|Sin información adicional|  
|Comprobar que se está ejecutando el servicio Instrumental de administración de Windows (WMI).|Iniciar el servicio Instrumental de administración de Windows|Sin información adicional|  
|Comprobar que el estado de la base de datos de Microsoft SQL CE sea correcto|Reinstalar el cliente de Configuration Manager|Sin información adicional|  
|Prueba de integridad WMI de Microsoft Policy Platform|Reparar Microsoft Policy Platform|Sin información adicional|  
|Comprobar que existe el servicio Microsoft Policy Platform|Reparar Microsoft Policy Platform|Sin información adicional|  
|Verificar que el tipo de inicio del servicio Microsoft Policy Platform es manual|Restablecer el tipo de inicio de servicio a manual|Sin información adicional|  
|Comprobar que existe el Servicio de transferencia inteligente en segundo plano|No hay corrección|Sin información adicional|  
|Comprobar que el tipo de inicio del Servicio de transferencia inteligente en segundo plano sea automático o manual|Restablecer el tipo de inicio de servicio a automático|Sin información adicional|  
|Comprobar que el tipo de inicio del servicio Inspección de red sea manual|Restablecer el tipo de inicio de servicio a manual si está instalado|Sin información adicional|  
|Compruebe que el tipo de inicio del servicio Instrumental de administración de Windows (WMI) sea automático|Restablecer el tipo de inicio de servicio a automático|Sin información adicional|  
|Comprobar si el tipo de inicio del servicio de Windows Update en dispositivos Windows 8 es automático o manual|Restablecer el tipo de inicio de servicio a manual|Sin información adicional|  
|Compruebe que el servicio de cliente (host de agente de SMS) existe.|No hay corrección|Sin información adicional|  
|Comprobar si el tipo de inicio del servicio de control remoto de Configuration Manager es automático o manual|Restablecer el tipo de inicio de servicio a automático|Sin información adicional|  
|Comprobar que el servicio de control remoto de Configuration Manager se está ejecutando|Iniciar el servicio de control remoto|Sin información adicional|  
|Comprobar que el servicio de proxy de reactivación (proxy de reactivación de Configuration Manager) se está ejecutando|Iniciar el servicio de proxy de reactivación de Configuration Manager|Esta comprobación de cliente se realiza solo si la opción de cliente **Administración de energía**: **Habilitar proxy de reactivación** se ha configurado como **Sí** en los sistemas operativos de cliente admitidos.|  
|Comprobar que el tipo de inicio del servicio de proxy de reactivación (proxy de reactivación de Configuration Manager) es automático|Restablecer el tipo de inicio del servicio de proxy de reactivación de Configuration Manager como automático|Esta comprobación de cliente se realiza solo si la opción de cliente **Administración de energía**: **Habilitar proxy de reactivación** se ha configurado como **Sí** en los sistemas operativos de cliente admitidos.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Archivos de registro de implementación de cliente

Para obtener información acerca de los archivos de registro utilizados por la implementación del cliente y las operaciones de administración, consulte los [archivos de registro](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
