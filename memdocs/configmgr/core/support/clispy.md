---
title: Cliente Spy
titleSuffix: Configuration Manager
description: Use Client Spy para solucionar problemas de distribución de software, inventario y disponibilidad de software en clientes de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707913"
---
# <a name="client-spy"></a>Cliente Spy

*Se aplica a: Configuration Manager (rama actual)*

Client Spy es una de las [herramientas de Configuration Manager](tools.md). Es una herramienta para solucionar problemas de distribución de software, inventario y disponibilidad de software en clientes de Configuration Manager. 

La mayoría de la información recuperada por la herramienta pertenece a las implementaciones de software:
- Todas las implementaciones de software actuales 
- Historial de distribución de software
- La configuración del tamaño de la caché de cliente
- Elementos en caché
- Implementaciones necesarias pendientes
- Implementaciones disponibles  

También muestra la siguiente información de inventario
- La fecha del ciclo de inventario más reciente
- La fecha del último informe
- Versiones principales y secundarias de inventario de software
- Colección de archivos
- Inventario de hardware
- Colección de IDMIF
- Registros de datos de detección (DDR) 

También se muestran las reglas de medición de software. 

> [!Note]   
> Para mejorar el rendimiento, la herramienta solo recopila información para cada pestaña cuando la selecciona. De forma similar, al hacer clic en **Actualizar**, solo se actualiza la información de la pestaña mostrada actualmente.



## <a name="usage"></a>Uso


### <a name="tools-menu"></a>Menú Herramientas

Las acciones siguientes están disponibles en el menú **Herramientas**:  

#### <a name="connect"></a>Conectar
Recupere información desde otro equipo.  

- De forma predeterminada, la herramienta muestra información del equipo actual. 

- Conéctese con el nombre del equipo remoto, el nombre de usuario y la contraseña para la cuenta. La herramienta realiza una conexión al recurso compartido de IPC$ en el equipo remoto. Elimina la conexión cuando se cierra la herramienta o se conecta a otro equipo.  

- Requiere una cuenta con suficientes credenciales para obtener la información.  

- Si no especifica un nombre de usuario y una contraseña, Client Spy utiliza el contexto de seguridad del usuario que ha iniciado sesión actualmente para intentar realizar la conexión.  

- Cuando se conecta a un equipo remoto, todas las pestañas que aparecen muestran información desde el equipo remoto.

#### <a name="software-distribution"></a>Distribución de software
Muestra la pestaña [Distribución de software](#software-distribution) y oculta las demás pestañas. De forma predeterminada, Client Spy muestra la pestaña Distribución de software.

#### <a name="inventory"></a>Tema de
Muestra la pestaña Inventario y oculta las demás pestañas.

#### <a name="software-metering"></a>Medición de software
Muestra la pestaña Medición de software y oculta las demás pestañas.

#### <a name="save-current-tab-to-file"></a>Guardar pestaña actual en archivo
Guarda la información de la pestaña mostrada actualmente en un archivo de texto que especifique. 

#### <a name="save-all-tabs-to-file"></a>Guardar todas las pestañas en el archivo
Guarda la información de todas las pestañas en un archivo de texto que especifique. Solo se guarda información que puede ver su cuenta.



## <a name="software-distribution-tab"></a>Pestaña Distribución de software

Configure opciones en las siguientes cuatro pestañas:
- [Solicitudes de ejecución de distribución de software](#bkmk_exec-requests)
- [Historial de distribución de software](#bkmk_history)
- [Información de caché de distribución de software](#bkmk_cache-info)
- [Ejecuciones pendientes de distribución de software](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a> Solicitudes de ejecución de distribución de software

Esta pestaña muestra todas las implementaciones existentes, incluyendo las implementaciones dirigidas a dispositivos y a usuarios.

Cada elemento de árbol en la pestaña Solicitudes de ejecución de distribución de software contiene los siguientes cuatro atributos:
- Id. de anuncio. Este valor puede estar en blanco, si es una implementación disponible. 
- Identificador de paquete 
- Nombre de programa 
- Usuario. Esto podría ser el SID del usuario de destino o el SID del usuario que inició la solicitud. Si ambos son solicitudes del sistema, el usuario mostrado es el sistema. 

Para cada solicitud de ejecución, también muestra la siguiente información en una estructura de subárbol:
- Nombre de programa 
- Identificador de paquete 
- Nombre del paquete 
- Hora de creación de solicitud 
- Estado 
- Estado de ejecución, si se está ejecutando el estado 
- Contexto de ejecución (usuario o administrador) 
- Historial de estado (correcto, error o NotRun) 
- LastRunTime (nunca, si no se ha ejecutado el programa antes) 
- RetryCount, si el estado es WaitingRetry 
- ContentAccess (número de reintentos, si el estado es WaitingRetry) 
- FailureCode, si el estado es WaitingRetry 
- FailureReason, si el estado es WaitingRetry 

Si la solicitud requiere contenido, el estado es WaitingContent. La pestaña Información de caché de distribución de software muestra los detalles para esta solicitud de descarga.

Si la solicitud de ejecución es una solicitud de descarga, también muestra el número de bytes descargados.

> [!Note]   
> Utiliza iconos diferentes para distintos estados de una solicitud de ejecución.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a> Historial de distribución de software

Esta pestaña contiene información sobre todos los programas ejecutados con anterioridad. Esta información se almacena en el registro.

Las ramas principales de este árbol son los historiales de otros usuarios, incluido el sistema. Muestra un subárbol que contiene la lista de paquetes desde los que se han ejecutado programas para cada usuario. 

El nombre del paquete y el Id. de paquete para cada subárbol de paquete muestra una lista de programas que se han ejecutado. Muestra los siguientes atributos para cada uno: 
- Nombre de programa
- Estado de la ejecución
- Hora de última ejecución
- Código de error
- Motivo del error  

El código de error y el motivo del error están en blanco si un programa se ha ejecutado correctamente.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a> Información de caché de distribución de software

#### <a name="cache-config"></a>Configuración de caché
Contiene información sobre la caché de cliente de Configuration Manager. Esta información incluye la ubicación de caché, el tamaño de caché y si se encuentra actualmente en uso. 

#### <a name="cached-items"></a>Elementos en caché
Contiene un subárbol de todos los elementos que se encuentran actualmente en la memoria caché. Cada elemento de árbol incluye la información siguiente sobre cada elemento: 
- La ubicación del elemento (carpeta) en la memoria caché
- Estado actual
- Identificador de paquete
- Nombre del paquete
- Versión del paquete
- Tamaño del paquete
- Recuento de referencias actual
- Última vez que se hace referencia (UTC)  

#### <a name="downloading-items"></a>Elementos que se están descargando
Estos son los elementos que el cliente está descargando actualmente. Cada uno de ellos muestra la misma información que se muestra en los elementos almacenados en caché y el número de kilobytes descargados. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a> Ejecuciones pendientes de distribución de software

Esta pestaña contiene información que detalla las implementaciones necesarias pasadas y futuras y una lista de las implementaciones disponibles.

Cada rama del árbol es para cada cuenta de usuario con las implementaciones disponibles, incluido el sistema.

Para cada usuario, un subárbol contiene los siguientes tres elementos:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Anuncios obligatorios con ejecuciones futuras
Estos son los anuncios obligatorios que todavía tienen programas que tienen que ejecutarse. Pueden ser periódicos, un solo uso, o varios anuncios programados. Cada uno muestra el identificador de anuncio, el siguiente tiempo de ejecución y la programación en la que se ejecuta el anuncio. 

#### <a name="optional-advertisements"></a>Anuncios opcionales
Muestra una lista de todos los anuncios que se publican. También muestra detalles como el Id. de anuncio, el nombre del programa y el nombre del paquete para cada uno. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Los anuncios obligatorios anteriores sin ejecuciones futuras programadas
Es una lista de anuncios que existen en el cliente que no tienen ningún programa con ejecuciones futuras. Se muestran el Id. de anuncio, el nombre de paquete y el nombre del programa. Se muestra un elemento del subárbol para los anuncios que son opcionales.

> [!Note]  
> La información de nombre de paquete solo está disponible para los paquetes que tienen directivas anunciadas asociadas a ellos en el equipo que se está viendo. Los paquetes que ya no tienen directivas disponibles asociadas a ellos muestran el mensaje "El nombre del paquete ya no está disponible".  



## <a name="inventory-tab"></a>Pestaña Inventario

Solo hay una ficha que contiene información de inventario. El árbol principal contiene los siguientes cinco elementos:  

- **Inventario de software**: contiene la fecha en que se ha iniciado el último ciclo, la fecha del último informe y las versiones secundarias y principales del último informe.  

- **Recopilación de archivos**: contiene la fecha en que se ha iniciado el último ciclo, la fecha del último informe y las versiones secundarias y principales del último informe.  

- **Inventario de hardware**: contiene la fecha en que se ha iniciado el último ciclo, la fecha del último informe y las versiones secundarias y principales del último informe.  

- **Colección de IDMIF**: contiene la fecha en que se ha iniciado el último ciclo, la fecha del último informe y las versiones secundarias y principales del último informe.  

- **DDR**: contiene la fecha en que se ha iniciado el último ciclo, la fecha del último informe y las versiones secundarias y principales del último informe. La información de DDR también se muestra en un subárbol.



## <a name="software-metering-tab"></a>Pestaña Medición de software

Esta pestaña muestra información como un subárbol e incluye todas las reglas de medición de software. Muestra cada regla como un nodo, que se identifica por el identificador de regla y el nombre de archivo. Expanda cada nodo del árbol y vea la siguiente información:
- Nombre de archivo del explorador 
- Nombre de archivo original
- Id. de regla
- Versión de archivo
- Lenguajes


