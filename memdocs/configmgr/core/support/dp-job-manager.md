---
title: DP Job Queue Manager
titleSuffix: Configuration Manager
description: Use DP Job Queue Manager para solucionar problemas y administrar trabajos de distribución de contenido a puntos de distribución de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694343"
---
# <a name="dp-job-queue-manager"></a>DP Job Queue Manager

*Se aplica a: Configuration Manager (rama actual)*

DP Job Queue Manager es una de las [herramientas de Configuration Manager](tools.md). Úsela para solucionar problemas y administrar trabajos de distribución de contenido en curso a puntos de distribución de Configuration Manager. 

La herramienta muestra la lista de trabajos que tiene el componente de administrador de transferencia de paquetes en la cola. También muestra el estado de los trabajos: listo para ejecutarse, en ejecución o reintentando. Le permite manipular los trabajos en la cola, moverlos más alto en la lista, cancelar un trabajo o iniciar manualmente la ejecución de uno.

También obtiene información del servidor de sitio en el que el punto de distribución ejecuta un trabajo. La herramienta se conecta a través del proveedor al servidor de sitio. No se conecta a cada punto de distribución remoto para recopilar esta información. Dado que desencadena acciones y obtiene información a través del proveedor, hay un retraso a la hora de reflejar los cambios de puntos de distribución remotos.



## <a name="usage"></a>Uso

Ejecute **DPJobMgr.exe**. El menú principal de la herramienta contiene las siguientes pestañas: 

- [Conectar](#bkmk_connect): establece la conexión inicial con el servidor del sitio primario.  

- [Información general](#bkmk_overview): resume en una sola vista todos los trabajos que se ejecutan en todos los puntos de distribución.  

- [Información del punto de distribución](#bkmk_dp-info): seleccione varios puntos de distribución para realizar un seguimiento de estos y administrar un solo trabajo de interés.  

- [Administrar trabajos](#bkmk_manage-jobs): Muestra en una vista plana una lista de todos los trabajos y sus estados. Manipule los trabajos, muévalos hacia arriba, cancélelos o inícielos manualmente.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> Pestaña conectar

Use esta pestaña para establecer la conexión inicial con el servidor de sitio primario. Usa las credenciales del usuario que ha iniciado sesión actualmente. No se puede conectar al sitio de administración central o sitios secundarios. La conexión requiere el rol de seguridad **Administrador total**.

Una notificación en la parte inferior de la herramienta confirma que está conectada al servidor de sitio cuando establece correctamente una conexión. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a> Pestaña Información general

Muestra un resumen de todos los trabajos en todos los puntos de distribución. Consulte las siguientes columnas:  

- **Punto de distribución**: muestra una lista de los nombres de los puntos de distribución.  

- **Trabajos en ejecución**: muestra el número de trabajos simultáneos que se ejecutan en un punto de distribución específico.  

    > [!Tip]  
    > El número de distribuciones de software simultáneas es una configuración de sitio. Puede modificar esta configuración en las propiedades de componente de distribución de software.  

- **Total de trabajos**: muestra el número de todos los trabajos destinados a un punto de distribución específico. Este número incluye los trabajos que se están ejecutando, reintentando o esperando para ejecutarse.  

- **Reintentos totales**: muestra el número de veces que los trabajos han reintentado un punto de distribución específico. Un número más alto puede representar un problema general con ese punto de distribución particular.  


> [!Tip]  
> - Para ordenar cada columna en esta pestaña, haga clic en el nombre de columna  
> 
> - Actualice manualmente la información de esta pestaña haciendo clic en **Actualizar**  
> 
> - Actualice automáticamente la información en esta pestaña haciendo clic en **Iniciar actualización automática** y estableciendo el intervalo de actualización automática. El intervalo de actualización predeterminado es de dos minutos.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a> Pestaña Información del punto de distribución

Muestra la lista de todos los puntos de distribución en el sitio conectado. El panel de la izquierda muestra todos los puntos de distribución. Haga clic en **Seleccionar todo** o **Anular selección de todo** según sea necesario, o seleccione varios puntos de distribución específicos en esta lista. El panel de la derecha muestra los trabajos de puntos de distribución seleccionados.

Hay ocho columnas:  

- **Icono de estado**: hay tres iconos de estado posibles:  

    - **Listo**: indica que un trabajo determinado ha finalizado todos los pasos de comprobación. Está listo para agregarse a los trabajos simultáneos en ejecución. Los trabajos en este estado normalmente están en una fase de espera. Esperan a que finalicen los procesos en ejecución actuales para liberar espacio para ellos.  

    - **En ejecución**: indica que actualmente se está ejecutando un trabajo determinado en un punto de distribución. Para los trabajos de larga ejecución (los paquetes grandes), normalmente hay tiempo para obtener el progreso (%) para la finalización. Muestra este porcentaje en la columna **Progreso** en esta vista. Para los paquetes pequeños, la columna **Progreso** puede permanecer vacía. El trabajo puede estar completado en el momento en que recibe el estado del punto de distribución remoto.  

    - **Reintentar**: indica que se ha producido un error en un trabajo determinado y ahora está en estado de reintento. Este trabajo se reintenta tras el intervalo de reintento. Este intervalo es configurable y se establece en 30 minutos de forma predeterminada.  

- **Software**: nombre del paquete que tiene como destino un punto de distribución específico.  

- **Identificador de paquete**: identificador del paquete que tiene como destino un punto de distribución específico.  

- **Tamaño**: tamaño del paquete en KB.  

- **Progreso**: porcentaje de finalización del trabajo. Para obtener más información, consulte la descripción del icono de estado **Ejecutando**.  

- **Hora de inicio/reinicio**: para un trabajo en ejecución, este valor equivale a la hora de inicio (verde). Para un trabajo de reintento, este valor es el momento en que se volverá a intentar el trabajo.  

- **Reintentos**: número de veces que se ha reintentado ejecutar este paquete.  

- **Nombre del punto de distribución:** nombre de dominio completo (FQDN) del punto de distribución que se va a limpiar.  

> [!Tip]  
> - Para ordenar cada columna en esta pestaña, haga clic en el nombre de columna  
> 
> - Actualice manualmente la información de esta pestaña haciendo clic en **Actualizar**  
> 
> - Actualice automáticamente la información en esta pestaña haciendo clic en **Iniciar actualización automática** y estableciendo el intervalo de actualización automática. El intervalo de actualización predeterminado es de dos minutos.  
> 
> - Si tiene que modificar un trabajo determinado, haga clic con el botón derecho en el trabajo en esta vista y seleccione **Administrar trabajo**. Esta acción abre la [pestaña Administrar trabajos](#bkmk_manage-jobs).  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a> Pestaña Administrar trabajos

Muestra en una vista plana una lista de todos los trabajos y sus estados. Contiene las mismas ocho columnas que la [pestaña Información de punto de distribución](#bkmk_dp-info). En esta vista, haga clic con el botón derecho en los trabajos para ver las siguientes acciones:  

- **Ejecutar**: inicia un trabajo que se encuentra en cualquier estado distinto de ejecución  

- **Mover arriba**: uno o más trabajos se mueven a la parte superior de la cola. Esta acción puede tener como resultado que los trabajos se ejecuten inmediatamente. Puede pausarse un trabajo de prioridad inferior debido a esta acción.  

- **Subir**: mueve un determinado trabajo a una fila superior. Puede pausarse un trabajo de prioridad inferior en ejecución debido a esta acción.  

- **Bajar**: mueve un determinado trabajo a una fila inferior.  

- **Mover abajo:** uno o más trabajos se mueven a la parte inferior de la cola.  

    > [!Tip]  
    > Arrastre y coloque trabajos en la lista para moverlos.  

- **Cancelar**: intenta cancelar uno o más trabajos.  

    > [!Note]  
    > No puede cancelar trabajos que están a punto de completarse. No puede cancelar los trabajos en el servidor de sitio si el servidor de sitio también es un punto de distribución.  



## <a name="see-also"></a>Vea también

- [Conceptos básicos de la administración de contenido](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Administrador de transferencia de paquetes](../plan-design/hierarchy/package-transfer-manager.md)
