---
title: replicación basada en archivos
titleSuffix: Configuration Manager
description: Obtención de información sobre cómo Configuration Manager usa la replicación basada en archivos para transferir datos entre sitios de la jerarquía
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703563"
---
# <a name="file-based-replication"></a>replicación basada en archivos

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager usa la replicación basada en archivos para transferir datos basados en archivos entre sitios de la jerarquía. Estos datos incluyen las aplicaciones y los paquetes que quiere implementar en puntos de distribución de sitios secundarios. También controla los registros de datos de detección no procesados que el sitio transfiere a su sitio principal y que posteriormente procesa.  

La comunicación entre sitios basada en archivos usa el protocolo *Bloque de mensajes del servidor* (SMB) en el puerto TCP/IP 445. Para controlar la cantidad de datos que el sitio transfiere a través de la red, especifique el límite de ancho de banda y el modo por pulsos. Use programaciones para controlar cuándo enviar los datos a través de la red.  

## <a name="routes"></a><a name="bkmk_routes"></a> Rutas

La información siguiente puede ayudar a configurar y usar las rutas de replicación de archivos.  

### <a name="file-replication-route"></a>Ruta de replicación de archivos

Cada ruta de replicación de archivos identifica un sitio de destino al que un sitio transfiere los datos basados en archivos. Cada sitio admite una ruta de replicación de archivos a un sitio de destino específico.  

Para administrar una ruta de replicación de archivos, vaya al área de trabajo **Administración**. Expanda el nodo **Configuración de jerarquía** y seleccione **Replicación de archivos**.  

Puede cambiar los siguientes valores para rutas de replicación de archivos:  

#### <a name="file-replication-account"></a>Cuenta de replicación de archivos

Esta cuenta se conecta al sitio de destino y escribe datos en el recurso compartido **SMS_Site** del sitio. El sitio de destino procesa los datos escritos en este recurso compartido. De manera predeterminada, cuando agrega un sitio a la jerarquía, Configuration Manager asigna una cuenta de equipo del servidor de sitio nuevo como su cuenta de replicación de archivos. A continuación, agrega esta cuenta al grupo `SMS_SiteToSiteConnection_<sitecode>` del sitio de destino. Este grupo es local en el equipo que concede acceso al recurso compartido SMS_Site. Puede cambiar esta cuenta para que sea una cuenta de usuario de Windows. Si cambia la cuenta, asegúrese de agregar la nueva cuenta al grupo `SMS_SiteToSiteConnection_<sitecode>` del sitio de destino.  

> [!NOTE]  
> Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario como la **Cuenta de replicación de archivos**.  

#### <a name="schedule"></a>Programa

Establezca la programación para cada ruta de replicación de archivos. Esta acción restringe el tipo de datos y la hora en que los datos se pueden transferir al sitio de destino.  

#### <a name="rate-limits"></a>Límites de frecuencia

Especifique los límites de frecuencia para cada ruta de replicación de archivos. Esta acción controla el ancho de banda de red que usa el sitio cuando transfiere datos al sitio de destino:  

- **Modo por pulsos**: especifique el tamaño de los bloques de datos que el sitio envía al sitio de destino. También puede especificar un retraso de tiempo entre el envío de cada bloque de datos. Use esta opción cuando tenga que enviar datos a través de una conexión de red con un ancho de banda bajo al sitio de destino.

    Por ejemplo, puede tener limitaciones para enviar 1 KB de datos cada cinco segundos y no 1 KB cada tres segundos. Esta limitación es independiente de la velocidad del vínculo o su uso en un momento dado.

- **Limitado al máximo de velocidades de transferencia por hora**: el sitio envía datos a un sitio de destino únicamente mediante el porcentaje de tiempo que especifica. Configuration Manager no identifica el ancho de banda disponible de la red. Divide el tiempo en que puede enviar datos en intervalos de tiempo. Después, envía los datos durante un período de tiempo corto, seguido de bloques de tiempo durante los cuales no envía ningún dato.

    Por ejemplo, puede establecer la velocidad máxima en **50 %** . Configuration Manager transmite los datos durante un período de tiempo, seguido de un período de tiempo equivalente durante el cual no envía ningún dato. No administra la cantidad real del bloque de datos que envía. El sitio solamente administra la cantidad de tiempo durante el que se envían datos.  

    > [!CAUTION]  
    > De forma predeterminada, un sitio puede utilizar hasta tres **envíos simultáneos** para transferir datos a un sitio de destino. Cuando habilita los límites de frecuencia para una ruta de replicación de archivos, los **envíos simultáneos** a ese sitio se limitan a uno. Este comportamiento se aplica incluso cuando la opción **Limitar ancho de banda disponible (%)** se establece en **100 %** . Por ejemplo, si usa la configuración predeterminada para el remitente, esto reduce la velocidad de transferencia al sitio de destino para que sea un tercio de la capacidad predeterminada.  

#### <a name="routes-between-secondary-sites"></a>Rutas entre sitios secundarios

Configure una ruta de replicación de archivos entre dos sitios secundarios para distribuir contenido basado en archivos entre dichos sitios.  


### <a name="sender"></a>Remitente

Cada sitio tiene un remitente. El remitente administra la conexión de red de un sitio a un sitio de destino. Puede establecer conexiones a varios sitios al mismo tiempo. Para conectarse a un sitio, el remitente utiliza la ruta de replicación de archivos al sitio e identifica la cuenta que utiliza para establecer la conexión de red. El remitente también usa esta cuenta para escribir datos en el recurso compartido SMS_Site del sitio de destino.  

De forma predeterminada, el remitente escribe datos en un sitio de destino mediante el uso de varios **envíos simultáneos**, o un *subproceso*. Cada subproceso, puede transferir un objeto basado en archivo diferente al sitio de destino. Cuando el remitente comienza a enviar un objeto, continúa escribiendo bloques de datos para ese objeto hasta que se envía todo el objeto. Una vez que envía todos los datos para el objeto, un nuevo objeto puede empezar a enviar ese subproceso.  

Para limitar el remitente para un sitio, vaya al área de trabajo **Administración** y expanda el nodo **Configuración del sitio**. Seleccione el nodo **Sitios** y, luego, **Propiedades** para el sitio que quiere administrar. Haga clic en la pestaña **Remitente** para cambiar la configuración del remitente.  

Puede cambiar los siguientes valores para un remitente:  

#### <a name="maximum-concurrent-sendings"></a>Máximo de envíos simultáneos

De manera predeterminada, cada sitio usa cinco envíos simultáneos (subprocesos). Hay tres subprocesos disponibles para usarlos cuando se envían datos a cualquier sitio de destino. Si aumenta este número, podrá aumentar el procesamiento de datos entre sitios. Un mayor número de subprocesos significa que Configuration Manager puede transferir más archivos al mismo tiempo. Si se aumenta este número, también aumenta la demanda de ancho de banda de red entre sitios.  

#### <a name="retry-settings"></a>Configuración de reintento

De forma predeterminada, cada sitio reintenta dos veces una conexión con problemas, con un retraso de un minuto entre intentos de conexión. Puede modificar el número de intentos de conexión que realiza el sitio y el tiempo que hay que esperar entre ellos.  


## <a name="next-steps"></a>Pasos siguientes

[Database replication](database-replication.md)
