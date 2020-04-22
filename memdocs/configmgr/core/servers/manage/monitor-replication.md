---
title: Supervisión de la replicación de base de datos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo supervisar la replicación de SQL Server en su jerarquía de Configuration Manager.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 96cce5d4aaa352177b1c24ff78cf15e90ea6e823
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694413"
---
# <a name="monitor-database-replication"></a>Supervisión de la replicación de base de datos

*Se aplica a: Configuration Manager (rama actual)*

Supervise los detalles para la replicación de base de datos con el nodo **Replicación de base de datos** en el área de trabajo **Supervisión** de la consola de Configuration Manager. Puede supervisar el estado de los vínculos de replicación entre sitios. También se muestra la inicialización y replicación de los grupos de replicación para el sitio al que se conecta.  

> [!TIP]  
> Aunque también aparece un nodo **Replicación de base de datos** debajo del nodo **Configuración de jerarquía** en el área de trabajo **Administración**, desde esta ubicación no podrá ver el estado de replicación para los vínculos de replicación de bases de datos.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Estado de vínculo de replicación  

La replicación de bases de datos entre sitios implica la replicación de varios conjuntos de información, denominados *grupos de replicación*. Cada grupo de replicación envía y recibe datos con diferentes prioridades. De forma predeterminada, no puede modificar los datos contenidos en un grupo de replicación ni la frecuencia de replicación.  

Cuando un vínculo de replicación está activo y su estado no es correcto o se ha degradado, todos los grupos se replican rápidamente. Si uno o varios grupos no completan la replicación dentro del período de tiempo esperado, el vínculo se muestra como *degradado*. Los vínculos degradados pueden seguir funcionando, pero debe supervisarlos para asegurarse de que vuelven al estado activo. Investíguelos para asegurarse de que no se producen errores adicionales de degradación o replicación.  

En cada vínculo de replicación, especifique el número de veces que se reintenta un grupo que no se ha replicado correctamente. Después de este número de reintentos, el sitio establece el estado del vínculo en degradado o con errores. Incluso si todos los grupos excepto uno se replican correctamente, el sitio establece el estado del vínculo en degradado o con errores. El sitio establece este estado porque el grupo de replicación no puede completar la replicación en el número de intentos especificado. Para más información, consulte [Umbrales de replicación de base de datos](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

Utilice la siguiente información para conocer el estado de los vínculos de replicación que podrían requerir más investigación:  

### <a name="link-is-active"></a>El vínculo está activo

No se detectó ningún problema y la comunicación a través del vínculo es actual.

Cuando un sitio principal se está actualizando a una nueva versión y ve el estado del vínculo desde el sitio secundario, dicho estado del vínculo se muestra como activo. Después de la actualización, hasta que el sitio secundario esté en la misma versión que el sitio primario, el estado del vínculo se muestra como activo cuando se visualiza desde el sitio primario. Cuando se visualiza desde el sitio secundario, se muestra como configurado.  

### <a name="link-is-degraded"></a>El vínculo está degradado

La replicación es funcional, pero la replicación de al menos un objeto o grupo se retrasó. Supervise los vínculos que se encuentran en este estado. Revise la información de ambos sitios del vínculo para obtener indicaciones sobre el posible error del vínculo.

Un vínculo también puede mostrar el estado degradado si el sitio que recibe los datos replicados no puede confirmar rápidamente los datos en la base de datos. Este comportamiento puede suceder cuando se replican grandes volúmenes de datos. Por ejemplo, cuando implementa una actualización de software en un gran número de equipos. El sitio primario del vínculo puede tardar algún tiempo en procesar este volumen de datos replicados. El retardo en el procesamiento del sitio principal hace que establezca el estado del vínculo en degradado hasta que pueda procesar correctamente el trabajo pendiente de datos.

### <a name="link-has-failed"></a>Se ha producido un error en el vínculo

La replicación no es funcional. Es posible que un vínculo de replicación pueda recuperarse sin necesidad de otras acciones. Para investigar y ayudar a corregir la replicación en este vínculo, utilice Replication Link Analyzer.

Este estado también puede indicar un problema con la red física entre el sitio principal y secundario en el vínculo de replicación.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a> Supervisión del estado de la replicación

Utilice el nodo **Replicación de base de datos** del área de trabajo **Supervisión** para ver el estado de un vínculo de replicación. Vea los detalles sobre la base de datos en cada sitio del vínculo de replicación. También puede ver detalles sobre los grupos de replicación. Para ver estos detalles, seleccione un vínculo de replicación y luego seleccione la pestaña correspondiente al estado de replicación que desea ver.

En las siguientes secciones se proporcionan detalles sobre las diferentes pestañas del estado de replicación:

### <a name="summary"></a>Resumen

Muestra información de alto nivel acerca de la replicación de datos del sitio y datos globales entre los dos sitios de un vínculo.  

Seleccione **Ver informes de datos de tráfico del historial** para ver un informe con detalles sobre el ancho de banda de red usado por la replicación en todo el vínculo.  

### <a name="parent-site"></a>Sitio principal

Para el sitio principal de un vínculo de replicación, muestra detalles acerca de la base de datos, que incluyen:  

- Puertos de firewall para SQL Server  

- Espacio libre en disco  

- Ubicaciones de los archivos de base de datos  

- Certificados  

### <a name="child-site"></a>Sitio secundario

Para el sitio secundario de un vínculo de replicación, muestra detalles acerca de la base de datos, que incluyen:  

- Puertos de firewall para SQL Server  

- Espacio libre en disco  

- Ubicaciones de los archivos de base de datos  

- Certificados  

### <a name="initialization-detail"></a>Detalle de inicialización

Muestra el estado de inicialización para los grupos que se replican a través del vínculo. Esta información puede permitirle identificar cuándo la inicialización de datos de replicación está en curso o no terminó correctamente.  

Utilice esta información para identificar cuándo podría estar un sitio en *modo de interoperabilidad*. El modo de interoperabilidad se produce cuando el sitio secundario no ejecuta la misma versión de Configuration Manager que el sitio principal.  

### <a name="replication-detail"></a>Detalle de la replicación

Consulte el estado de replicación de cada grupo de replicación que se replica a través del vínculo. Use esta información para ayudar a identificar problemas o retrasos en la replicación de datos específicos. Puede ayudar a determinar los umbrales de replicación de base de datos apropiados para este vínculo. Para más información, consulte [Umbrales de replicación de base de datos](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

> [!TIP]  
> Los grupos de replicación de datos de sitio se envían sólo desde el sitio secundario al sitio principal. Los grupos de replicación de datos globales replican en ambas direcciones.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a> Replication Link Analyzer

Configuration Manager incluye **Replication Link Analyzer** (RLA), que se utiliza para analizar y reparar problemas de replicación. Use RLA para corregir errores de vínculo cuando se producen errores en la replicación. También resulta útil cuando la replicación deja de funcionar, pero el sitio todavía no lo ha comunicado como error.

Use RLA para corregir los problemas de replicación entre los siguientes equipos de la jerarquía:  

- Entre un servidor de sitio y el servidor de base de datos del sitio  

- Entre un servidor de base de datos del sitio y el servidor de base de datos del otro sitio, lo que también se conoce como replicación entre sitios  

> [!Note]  
> La dirección del error de replicación no importa.

Ejecute RLA en la consola de Configuration Manager o en un símbolo del sistema:  

- Para ejecutar en la consola de Configuration Manager: Vaya al área de trabajo **Supervisión** y seleccione el nodo **Replicación de base de datos**. Seleccione el vínculo de replicación que desea analizar y luego, en la cinta de opciones, seleccione **Replication Link Analyzer**.  

- Para la ejecución en un símbolo del sistema, escriba el siguiente comando: `%ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

Cuando ejecuta RLA, este detecta los problemas con una serie de comprobaciones y reglas de diagnóstico. Puede ver los problemas que identifica la herramienta. Cuando tiene instrucciones para resolver un problema, los muestra. Si RLA puede corregir automáticamente un problema, le presenta esa opción.

Cuando RLA finaliza, guarda los resultados en el siguiente informe basado en XML y un archivo de registro en el escritorio del usuario que ejecuta la herramienta:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA detiene los servicios siguientes mientras corrige algunos problemas. Reinicia estos servicios cuando se completa la corrección:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Si RLA no puede completar la corrección, reinicie estos servicios en el servidor de sitio si es necesario.  

RLA registra todas las acciones de investigación y corrección para proporcionar detalles adicionales que no se muestran en el asistente.  

### <a name="rla-prerequisites"></a>Requisitos previos de LRA

La cuenta que utiliza para ejecutar LRA debe tener los permisos siguientes:

- Derechos de administrador local en cada equipo implicado en el vínculo de replicación.

- Derechos de administrador del sistema en cada base de datos de SQL Server implicada en el vínculo de replicación.  

> [!Note]  
> La cuenta no requiere un rol específico de seguridad de administración basada en roles de Configuration Manager. Un usuario administrativo con acceso al nodo **Replicación de base de datos** puede ejecutar la herramienta en la consola de Configuration Manager. Un administrador del sistema con derechos suficientes para cada equipo puede ejecutar la herramienta en un símbolo del sistema.  

### <a name="rla-known-issue"></a>Problema conocido de RLA

RLA genera errores de certificado de SQL Server Service Broker (SSB) para sitios primarios que se actualizaron desde System Center 2012 Configuration Manager. Este problema se debe a los cambios en los nombres de los certificados de la rama actual de Configuration Manager. Puede omitir estos errores con seguridad.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a> Supervisión de la replicación de base de datos  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Supervisión del estado de replicación de base de datos entre sitios de alto nivel

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**.  

2. Seleccione el nodo **Jerarquía del sitio** para abrir la vista **Diagrama de jerarquía**.  

3. Mantenga el puntero del mouse sobre la línea entre los dos sitios. Vea el estado de la replicación de datos globales y de sitio para estos sitios.  

### <a name="monitor-the-status-of-a-replication-link"></a>Supervisión del estado de un vínculo de replicación

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**.  

2. Seleccione el nodo **Replicación de base de datos** y luego elija el vínculo de replicación que desea supervisar. A continuación, seleccione la pestaña correspondiente para ver distintos detalles acerca del estado de replicación de ese vínculo.  
