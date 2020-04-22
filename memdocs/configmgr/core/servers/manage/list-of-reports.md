---
title: Lista de informes
titleSuffix: Configuration Manager
description: Revise la lista de informes que se proporcionan con Configuration Manager. Los informes aparecen en varias categorías.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694493"
---
# <a name="list-of-reports-in-configuration-manager"></a>Lista de informes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager proporciona muchos informes integrados que abarcan muchas de las tareas de informes que es posible que le interese realizar. También puede usar las instrucciones SQL en estos informes para ayudarle a escribir sus propios informes.   

Los siguientes informes se incluyen con Configuration Manager. Los informes aparecen en varias categorías.  



## <a name="administrative-security"></a>Seguridad administrativa  

Los seis informes siguientes aparecen en la categoría **Seguridad administrativa**.  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Registro de actividad de administración**|Muestra un registro de los cambios administrativos realizados para los usuarios administrativos, los roles de seguridad, los ámbitos de seguridad y las recopilaciones.|  
|**Asignaciones de seguridad de los usuarios administrativos**|Muestra los usuarios administrativos, sus roles de seguridad asociados y los ámbitos de seguridad asociados a cada rol de seguridad para cada usuario.|  
|**Objetos protegidos por un solo ámbito de seguridad**|Muestra los objetos que un administrador asignó solo al ámbito de seguridad especificado. En este informe no se muestran los objetos que un administrador asocia a más de un ámbito de seguridad.|  
|**Seguridad para un objeto específico de Configuration Manager o para varios objetos**|Muestra los objetos protegibles, los ámbitos de seguridad asociados a los objetos y qué usuarios administrativos tienen derechos sobre los objetos.|  
|**Resumen de roles de seguridad**|Muestra los roles de seguridad y los administradores de Configuration Manager asociados a cada rol.|  
|**Resumen de ámbitos de seguridad**|Muestra los ámbitos de seguridad y los usuarios administrativos y grupos de seguridad de Configuration Manager asociados a cada ámbito.|  



## <a name="alerts"></a>Alertas  

Los dos informes siguientes aparecen en la categoría **Alertas**.  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Cuadro de mandos de alertas**|Muestra un resumen de todas las alertas pospuestas que se generaron entre la fecha de inicio y de finalización especificada.|  
|**Alertas generadas con más frecuencia**|Muestra un resumen de las alertas que se generaron con más frecuencia entre el día actual y la fecha especificada para el área de la característica especificada.|  



## <a name="asset-intelligence"></a>Asset Intelligence  

Los 67 informes siguientes aparecen en la categoría **Asset Intelligence**.  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Hardware 01A - Resumen de los equipos en una recopilación específica**|Muestra una vista de resumen de Asset Intelligence de los equipos de la recopilación especificada.|  
|**Hardware 03A - Usuarios del equipo primario**|Muestra los usuarios y el recuento de equipos en los que son el usuario primario.|  
|**Hardware 03B - Equipos para un usuario primario de la consola específico**|Muestra todos los equipos para los que un usuario especificado es el usuario primario de la consola.|  
|**Hardware 04A - Equipos con varios usuarios (compartidos)**|Muestra los equipos que no tienen un usuario primario porque ningún usuario tiene un tiempo de inicio de sesión superior al 66 %.|  
|**Hardware 05A - Usuarios de la consola en un equipo específico**|Muestra todos los usuarios de la consola en el equipo especificado.|  
|**Hardware 06A - Equipos para los que no se pudo determinar los usuarios de la consola**|Ayuda a los usuarios administrativos a identificar los equipos que necesitan tener activado el registro de seguridad.|  
|**Hardware 07A - Dispositivos USB por fabricante**|Muestra los dispositivos USB, agrupados por fabricante.|  
|**Hardware 07A - Dispositivos USB por fabricante y descripción**|Dispositivos USB, agrupados por fabricante y descripción.|  
|**Hardware 07C - Equipos con un dispositivo USB específico**|Muestra todos los equipos con un dispositivo USB específico.|  
|**Hardware 07D - Dispositivos USB en un equipo específico**|Muestra todos los dispositivos USB en un equipo específico.|  
|**Hardware 08A - Hardware que no está listo para una actualización de software**|Muestra el hardware que no cumple los requisitos mínimos de hardware.|  
|**Hardware 09A - Búsqueda de equipos**|Muestra un resumen de los equipos que coinciden con los filtros de palabra clave. Estos filtros son el nombre de equipo, el sitio de Configuration Manager, el dominio, el principal usuario de la consola, el sistema operativo, el fabricante o el modelo.|  
|**Hardware 10A - Equipos de una recopilación especificada que se modificaron durante un período de tiempo especificado**|Muestra una lista de equipos de una recopilación especificada en los que una clase de hardware cambió durante un período de tiempo especificado.|  
|**Hardware 10B - Cambios en un equipo específico en un período de tiempo especificado**|Muestra las clases que cambiaron en un equipo específico en un período de tiempo especificado.|  
|**Licencia 01A - Libro de contabilidad de licencias por volumen de Microsoft para declaraciones de licencia de Microsoft**|Muestra un inventario de todos los títulos de software de Microsoft que están disponibles en el programa de licencias por volumen de Microsoft.|  
|**Licencia 01B - Artículo del libro de contabilidad de licencias por volumen de Microsoft por canal de ventas**|Identifica y muestra el canal de ventas para el software inventariado de las licencias por volumen de Microsoft.|  
|**Licencia 01C - Equipos con un artículo específico del libro de contabilidad de licencias por volumen de Microsoft y canal de ventas**|Identifica y muestra los equipos que tienen un artículo específico en el libro de contabilidad de licencias por volumen de Microsoft.|  
|**Licencia 01D - Productos del libro de contabilidad de licencias por volumen de Microsoft en un equipo específico**|Identifica y muestra todos los artículos del libro de contabilidad de licencias por volumen de Microsoft en un equipo especificado.|  
|**Licencia 02A - Recuento de licencias que expirarán en breve por intervalos de tiempo**|Muestra el recuento de licencias que expirarán en breve por intervalo de tiempo especificado. Las licencias de los productos que se muestran se administran mediante el Servicio de licencias de software.|  
|**Licencia 02B - Equipos con licencias que expirarán en breve**|Muestra los equipos especificados con licencias que expirarán en breve.|  
|**Licencia 02C - Información de licencia en un equipo específico**|Muestra los productos de un equipo específico cuyas licencias se administran mediante el Servicio de licencias de software.|  
|**Licencia 03A - Recuento de licencias por estado de licencia**|Muestra los productos, por estado de licencia, cuyas licencias se administran mediante el Servicio de licencias de software.|  
|**Licencia 03B - Equipos con un estado de licencia específico**|Muestra los productos, con un estado de licencia especificado, cuyas licencias se administran mediante el Servicio de licencias de software.|  
|**Licencia 04A - Recuento de productos administrados mediante el Servicio de licencias de software**|Muestra el recuento de productos cuyas licencias se administran mediante el Servicio de licencias de software.|  
|**Licencia 04B - Equipos con un producto específico administrado mediante el Servicio de licencias de software**|Muestra los equipos administrados mediante el Servicio de licencias de software que incluyen un producto determinado.|  
|**Licencia 05A - Equipos que proporcionan el Servicio de administración de claves**|Muestra los equipos que actúan como servidores de administración de claves.|  
|**Licencia 06A - Recuentos de procesadores para productos con licencias por procesador**|Muestra el número de procesadores en equipos que usan productos de Microsoft que admiten las licencias por procesador.|  
|**Licencia 06B - Equipos con un producto específico que admite licencias por procesador**|Muestra una lista de los equipos donde está instalado un producto específico de Microsoft que admite las licencias por procesador.|  
|**Licencia 14A - Informe de conciliación de licencias por volumen de Microsoft**|Muestra la conciliación de las licencias de software adquiridas a través del contrato de licencia de volumen de Microsoft y el recuento real de inventario.|  
|**Licencia 14B - Lista del inventario de software de Microsoft no encontrado en MVLS**|Este informe muestra los títulos de software de Microsoft en uso que no se encontraron en el contrato de licencia de volumen de Microsoft.|  
|**Licencia 15A - Informe de conciliación de licencias generales**|Muestra la conciliación de licencias de software generales adquiridas y el recuento real de inventario.|  
|**Licencia 15B - Informe de conciliación de licencias generales por equipo**|Muestra los equipos que instalaron el producto con licencia con una versión especificada.|  
|**Software 01A - Resumen de software instalado en una recopilación específica**|Muestra un resumen del software instalado ordenado por el número de instancias encontradas en el inventario.|  
|**Software 02A - Familias de productos para una recopilación específica**|Muestra las familias de productos y el recuento de software de la familia de una recopilación especificada.|  
|**Software 02B - Categorías de productos para una familia de productos específica**|Muestra las categorías de productos en una familia de productos especificada y el recuento de software dentro de la categoría.|  
|**Software 02C - Software en una familia y una categoría de productos específicas**|Muestra todo el software que se encuentra en la familia y la categoría de productos especificadas.|  
|**Software 02D - Equipos con un software específico instalado**|Muestra todos los equipos con un software específico instalado.|  
|**Software 02E - Software instalado en un equipo específico**|Muestra todo el software instalado en el equipo especificado.|  
|**Software 03A - Software no categorizado**|Muestra el software que se clasifica como desconocido o que no tiene ninguna clasificación.|  
|**Software 04A - Software configurado para ejecutarse automáticamente en equipos**|Muestra una lista del software configurado para ejecutarse automáticamente en equipos.|  
|**Software 04B - Equipos con software específico configurado para ejecutarse automáticamente**|Muestra todos los equipos con software específico configurado para ejecutarse automáticamente.|  
|**Software 04C - Software configurado para ejecutarse automáticamente en un equipo específico**|Muestra el software configurado para ejecutarse automáticamente en un equipo específico.|  
|**Software 05A - Objetos del asistente de explorador**|Muestra los objetos del asistente de explorador instalados en los equipos de una recopilación especificada.|  
|**Software 05B - Equipos con un objeto del asistente de explorador específico**|Muestra todos los equipos con un objeto del asistente de explorador específico.|  
|**Software 05C - Objetos del asistente de explorador en un equipo específico**|Muestra todos los objetos del asistente de explorador en un equipo específico.|  
|**Software 06A - Búsqueda de software instalado**|En este informe se proporciona un resumen del software instalado. Busca en función de los criterios siguientes: nombre de producto, editor o versión.|  
|**Software 06B - Software por nombre de producto**|Muestra un resumen del software instalado en función de un nombre de producto especificado.|  
|**Software 07A - Programas ejecutables usados recientemente por recuento de equipos**|Muestra los programas ejecutables que los usuarios han usado recientemente. También incluye el recuento de los equipos en los que los usuarios usaron el programa. Para ver este informe, la medición de software debe estar habilitada para este sitio.|  
|**Software 07B - Equipos que usaron recientemente un programa ejecutable especificado**|Muestra los equipos en los que los usuarios usaron recientemente un programa ejecutable especificado. Este informe requiere que se habilite la configuración del cliente de disponibilidad de software.|  
|**Software 07C - Programas ejecutables usados recientemente en un equipo especificado**|Muestra los archivos ejecutables que los usuarios han usado recientemente en un equipo especificado. Este informe requiere que se habilite la configuración del cliente de disponibilidad de software.|  
|**Software 08A - Programas ejecutables usados recientemente por recuento de usuarios**|Muestra los programas ejecutables que los usuarios han usado recientemente. También incluye un recuento de los usuarios que han usado más recientemente el programa. Este informe requiere que se habilite la configuración del cliente de disponibilidad de software.|  
|**Software 08B - Usuarios que usaron recientemente un programa ejecutable especificado**|Muestra los usuarios que usaron más recientemente un programa ejecutable especificado. Este informe requiere que se habilite la configuración del cliente de disponibilidad de software.|  
|**Software 08C - Programas ejecutables usados recientemente por un usuario especificado**|Muestra los programas ejecutables que el usuario especificado ha usado recientemente. Este informe requiere que se habilite la configuración del cliente de disponibilidad de software.|  
|**Software 09A - Software usado con poca frecuencia**|Muestra los títulos de software que los usuarios no han usado durante un período de tiempo especificado.|  
|**Software 09B - Equipos con software usado con poca frecuencia instalado**|Muestra los equipos con software instalado que los usuarios no han usado durante un período de tiempo especificado. El período de tiempo especificado se basa en el valor especificado en el informe de 'Software 09A - Software usado con poca frecuencia'.|  
|**Software 10A - Títulos de software con varias etiquetas personalizadas específicas definidas**|Muestra los títulos de software basados en la coincidencia de todos los criterios de etiquetas personalizadas especificadas. Pueden seleccionarse hasta tres etiquetas personalizadas para refinar la búsqueda de un título de software.|  
|**Software 10B - Equipos con un título de software con etiqueta personalizada específico instalado**|Muestra todos los equipos de esta recopilación que tienen instalado el título de software con etiqueta personalizada especificado.|  
|**Software 11A - Títulos de software con una etiqueta personalizada específica definida**|Muestra los títulos de software basados en la coincidencia de al menos uno de los criterios de etiquetas personalizadas especificadas.|  
|**Software 12A - Títulos de software sin una etiqueta personalizada**|Muestra todos los títulos de software que no tienen una etiqueta personalizada definida.|  
|**Software 14A - Búsqueda de software con etiqueta de identificación de software habilitada**|Muestra el recuento de software instalado con una etiqueta de identificación de software habilitada.|  
|**Software 14B - Equipos con etiqueta de identificación de software específica habilitada instalada**|Muestra todos los equipos que tienen software instalado con una etiqueta de identificación de software habilitada especificada.|  
|**Software 14C - Software instalado con etiqueta de identificación de software habilitada en un equipo específico**|Muestra todo el software instalado con una etiqueta de identificación de software especificada habilitada en un equipo especificado.|  
|**Ciclo de vida 01A - Equipos con un producto de software específico**|Vea una lista de equipos en los que se detecta un producto especificado.|
|**Ciclo de vida 02A - Lista de máquinas con productos que han expirado en la organización**|Vea equipos que contienen productos expirados. Este informe se puede filtrar por nombre de producto.|
|**Ciclo de vida 03A - Lista de productos expirados que se encontraron en la organización**|Vea los detalles de productos de su entorno cuyo ciclo de vida ha expirado.|
|**Ciclo de vida 04A - Información general del ciclo de vida de los productos**|Vea una lista de los ciclos de vida de los productos. Filtre la lista por nombre de producto y los días para que expire.|
|**Ciclo de vida 05A: panel de ciclo de vida del producto**|A partir de la versión 1810, este informe incluye información similar a la del panel de consola.|



## <a name="client-push"></a>Inserción de cliente  

Los cuatro informes siguientes aparecen en la categoría **Inserción de cliente**.  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Detalles de estado de instalación de inserción de cliente**|Muestra información sobre el proceso de instalación de inserción de cliente para todos los sitios.|  
|**Detalles de estado de instalación de inserción de cliente para un sitio específico**|Muestra información sobre el proceso de instalación de inserción de cliente para un sitio específico.|  
|**Resumen de estado de instalación de inserción de cliente**|Muestra una vista de resumen del estado de instalación de inserción de cliente para todos los sitios.|  
|**Resumen de estado de instalación de inserción de cliente para un sitio especificado**|Muestra una vista de resumen del estado de instalación de inserción de cliente para un sitio especificado.|  



## <a name="client-status"></a>Estado de cliente  

Los siete informes siguientes aparecen en la categoría **Estado de cliente**.  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Detalles de corrección de cliente**|Muestra los detalles de las acciones de corrección de cliente para una recopilación especificada.|  
|**Resumen de corrección de cliente**|Muestra un resumen de las acciones de corrección de cliente para una recopilación especificada.|  
|**Historial de estado de cliente**|Muestra una vista histórica del estado general de cliente en el sitio.|  
|**Resumen de estado de cliente**|Muestra los resultados de la comprobación de cliente de los clientes activos de una colección determinada.|  
|**Hora de cliente para solicitar directiva**|Muestra el porcentaje de clientes que solicitaron la directiva al menos una vez en los últimos 30 días. Cada día representa un porcentaje del total de clientes que solicitaron la directiva desde el primer día del ciclo.|  
|**Clientes con detalles de comprobación de cliente con error**|Muestra los detalles de los clientes en los que se produjo un error de comprobación de cliente para una recopilación especificada.|  
|**Detalles de clientes inactivos**|Muestra una lista detallada de los clientes inactivos de una recopilación determinada.|  



## <a name="company-resource-access"></a>Acceso a los recursos de la empresa  

Los tres informes siguientes aparecen en la categoría **Acceso a los recursos de la empresa**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Historial de certificados emitidos**|Muestra el historial de los certificados emitidos por el punto de registro de certificados para los usuarios y los dispositivos en el intervalo de fechas especificado.|  
|**Lista de activos por estado de emisión de certificado**|Muestra los dispositivos o los usuarios en un estado de emisión de certificado especificado después de la evaluación de un perfil de certificado especificado.|  
|**Lista de activos con certificados a punto de expirar**|Muestra los dispositivos o los usuarios con certificados que expiran en la fecha especificada o antes.|  



## <a name="compliance-and-settings-management"></a>Administración de compatibilidad y configuración  

Los veintidós informes siguientes aparecen en la categoría **Administración de compatibilidad y configuración**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Historial de cumplimiento de una línea base de configuración**|Muestra el historial de los cambios en el cumplimiento de una línea base de configuración en el intervalo de fechas especificado.|  
|**Historial de cumplimiento de un elemento de configuración**|Muestra el historial de los cambios en el cumplimiento de un elemento de configuración en el intervalo de fechas especificado.|  
|**Detalles de reglas compatibles de elementos de configuración en una línea base de configuración para un activo**|Muestra información sobre las reglas evaluadas como compatibles para un elemento de configuración especificado para un dispositivo o usuario especificados.|  
|**Detalles de reglas en conflicto de elementos de configuración en una línea base de configuración para un activo**|Muestra información sobre las reglas de un elemento de configuración implementado que entran en conflicto con otras reglas. Incluye las demás reglas en el mismo elemento de configuración implementado o en otro.|  
|**Detalles de errores de elementos de configuración en una línea base de configuración para un activo**|Muestra información sobre los errores que generó un elemento de configuración especificado para un dispositivo o un usuario especificados.|  
|**Detalles de reglas no compatibles de elementos de configuración en una línea base de configuración para un activo**|Muestra información sobre las reglas que se evaluaron como no compatibles para un elemento de configuración especificado para un dispositivo o un usuario especificados.|  
|**Detalles de reglas corregidas de elementos de configuración en una línea base de configuración para un activo**|Muestra información sobre las reglas que corrigió un elemento de configuración especificado para un dispositivo o un usuario especificados.|  
|**Lista de activos por estado de cumplimiento para una línea base de configuración**|Muestra los dispositivos o los usuarios en un estado de cumplimiento especificado después de la evaluación de una línea base de configuración especificada.|  
|**Lista de activos por estado de cumplimiento para un elemento de configuración de una línea base de configuración**|Muestra los dispositivos o los usuarios en un estado de cumplimiento especificado después de la evaluación de un elemento de configuración especificado.|  
|**Lista de aplicaciones y dispositivos no conformes para un usuario específico**|Muestra información sobre los usuarios y los dispositivos que tienen aplicaciones instaladas que no son conformes con la directiva especificada.|  
|**Lista de reglas en conflicto con una regla especificada para un activo**|Muestra una lista de las reglas que están en conflicto con una regla especificada para un elemento de configuración implementado.|  
|**Lista de activos desconocidos para una línea base de configuración**|Muestra una lista de dispositivos o usuarios que todavía no han notificado datos de cumplimiento para una línea de base de configuración especificada.|  
|**Lista de activos desconocidos para un elemento de configuración**|Muestra una lista de dispositivos o usuarios que todavía no han notificado datos de cumplimiento para un elemento de configuración especificado.|  
|**Resumen de reglas y errores de elementos de configuración en una línea base de configuración para un activo**|Muestra un resumen del estado de cumplimiento de las reglas y los errores de configuración de un elemento de configuración especificado. El elemento de configuración se debe implementar en un dispositivo o usuario.|  
|**Resumen del cumplimiento por línea base de configuración**|Muestra un resumen del cumplimiento general de las líneas de base de configuración implementadas en la jerarquía.|  
|**Resumen del cumplimiento por elementos de configuración para una línea base de configuración**|Muestra un resumen del cumplimiento de los elementos de configuración en una línea de base de configuración especificada.|  
|**Resumen de cumplimiento por directivas de configuración**|Muestra un resumen del cumplimiento de las directivas de configuración.|  
|**Resumen del cumplimiento de una línea base de configuración para una recopilación**|Muestra un resumen del cumplimiento general de una línea base de configuración especificada. El elemento de configuración se debe implementar en la colección especificada.|  
|**Resumen de usuarios que tienen aplicaciones no conformes**|Muestra información sobre los usuarios que tienen aplicaciones instaladas que no son conformes con la directiva especificada.|  
|**Aceptación de términos y condiciones**|Muestra los elementos de términos y condiciones y la versión que cada usuario ha aceptado.|  



## <a name="data-warehouse"></a>Almacenamiento de datos  

Los siete informes siguientes aparecen en la categoría **Almacenamiento de datos**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Implementación de aplicaciones**|Historial: Vea los detalles de la implementación de aplicaciones para una máquina y una aplicación determinada.|
|**Cumplimiento de las actualizaciones de software y Endpoint Protection**|Historial: Vea los equipos a los que les faltan actualizaciones de software.|
|**Inventario de hardware general**|Historial: Vea todo el inventario de hardware para un equipo específico.|
|**Inventario de software general**|Historial: Vea todo el inventario de software para un equipo específico.|
|**Información general del mantenimiento de infraestructura**|Historial: Muestra información general del mantenimiento de su infraestructura de Configuration Manager.|
|**Lista de malware detectado**|Historial: Vea el malware que se ha detectado en la organización.|
|**Resumen de distribución de software**|Historial: Un resumen de distribución de software para un equipo y anuncio específico.|


## <a name="device-management"></a>Administración de dispositivos  

Los treinta y siete informes siguientes aparecen en la categoría **Administración del dispositivo**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los dispositivos móviles propiedad de la empresa**|Muestra todos los dispositivos móviles propiedad de la empresa.|
|**Todos los clientes de dispositivos móviles**|Muestra información sobre todos los clientes de dispositivos móviles. No se incluyen los dispositivos administrados por el conector de Exchange Server.|  
|**Problemas de certificados en los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE y que no tienen un estado correcto**|Muestra información detallada sobre problemas de certificados en los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Errores de implementación de clientes para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE**|Muestra información detallada sobre errores de implementación para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Detalles del estado de implementación de clientes para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE**|Muestra información sobre el estado de los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Implementación correcta de clientes para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE**|Muestra información detallada sobre la implementación correcta para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Problemas de comunicación en los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE y que no tienen un estado correcto**|Este informe contiene información detallada sobre problemas de comunicación en los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Estado de compatibilidad de la directiva predeterminada de buzones de ActiveSync para los dispositivos móviles administrados por el conector de Exchange Server**|Muestra un resumen del estado de cumplimiento con la directiva predeterminada de buzones de Exchange ActiveSync para los dispositivos móviles administrados por el conector de Exchange Server.|  
|**Recuento de dispositivos móviles por configuraciones de pantalla**|Este informe muestra el número de dispositivos móviles por configuraciones de pantalla.|  
|**Recuento de dispositivos móviles por sistema operativo**|Muestra el número de dispositivos móviles por sistema operativo.|  
|**Recuento de dispositivos móviles por memoria de programa**|Muestra el número de dispositivos móviles por memoria de programa.|  
|**Recuento de dispositivos móviles por configuraciones de memoria de almacenamiento**|Recuento de dispositivos móviles por configuraciones de memoria de almacenamiento|  
|**Información de estado para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE**|Muestra información de estado detallada para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Resumen de estado para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE**|Muestra información de estado para los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Dispositivos móviles inactivos administrados por el conector de Exchange Server**|Muestra los dispositivos móviles administrados por el conector de Exchange Server que no se han conectado a Exchange Server en un número especificado de días.|  
|**Lista de dispositivos por estado de atestación de estado**|Muestra una lista de dispositivos con los atributos notificados por el servicio de atestación de estado.|
|**Lista de dispositivos inscritos en Microsoft Intune por usuario**|Muestra todos los dispositivos que un usuario inscribió con Microsoft Intune.|  
|**Lista de dispositivos de una categoría de dispositivo específica**|Muestra información sobre todos los dispositivos dentro de una categoría de dispositivo específica.|
|**Problemas del cliente local en los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE y que no tienen un estado correcto**|Este informe contiene información detallada sobre problemas del cliente local en los dispositivos móviles administrados por el cliente de Configuration Manager para Windows CE.|  
|**Información de cliente de dispositivos móviles**|Muestra información sobre los dispositivos móviles que tienen instalado el cliente de Configuration Manager. Puede usar este informe para comprobar qué dispositivos móviles pueden comunicarse correctamente con un punto de administración.|  
|**Detalles de cumplimiento de dispositivos móviles para el conector de Exchange Server**|Muestra los detalles de cumplimiento de dispositivos móviles para una directiva predeterminada de buzones de Exchange ActiveSync que se configuró mediante el conector de Exchange Server.|  
|**Dispositivos móviles por sistema operativo**|Muestra los dispositivos móviles por sistema operativo.|  
|**Dispositivos móviles descodificados o descifrados**|Muestra los dispositivos móviles liberados.|  
|**Dispositivos móviles que no están administrados porque se inscribieron pero no pudieron asignarse a un sitio**|Muestra los dispositivos móviles que se inscribieron con Configuration Manager, que tienen un certificado, pero cuya asignación de sitio no se pudo completar.|  
|**Dispositivos móviles con una cantidad específica de memoria de programa libre**|Muestra todos los dispositivos móviles con su cantidad específica de memoria de programa libre.|  
|**Dispositivos móviles con una cantidad específica de memoria de almacenamiento extraíble libre**|Muestra todos los dispositivos móviles con la cantidad específica de memoria extraíble libre.|  
|**Dispositivos móviles con problemas de renovación de certificados**|Muestra los dispositivos móviles inscritos que no pudieron renovar su certificado. Si no se renueva el certificado antes del período de expiración, los dispositivos móviles serán no administrados.|  
|**Dispositivos móviles con poca memoria de programa libre (menos de los KB libres especificados)**|Muestra los dispositivos móviles para los que la memoria de programa es inferior a un tamaño especificado en KB.|  
|**Dispositivos móviles con poca memoria de almacenamiento extraíble libre (menos de los KB libres especificados)**|Muestra los dispositivos móviles para los que la memoria de almacenamiento extraíble es inferior a un tamaño especificado en KB.|  
|**Número de dispositivos inscritos en Microsoft Intune por usuario**|Muestra los usuarios habilitados para la suscripción de Microsoft Intune. También muestra el número total de dispositivos inscritos para cada usuario.|  
|**Solicitud de retirada y borrado pendiente para dispositivos móviles**|Muestra las solicitudes de borrado pendientes para los dispositivos móviles.|  
|**Dispositivos móviles inscritos y asignados recientemente**|Muestra dispositivos móviles que se inscribieron recientemente con Configuration Manager y que se asignaron correctamente a un sitio.|  
|**Dispositivos móviles borrados recientemente**|Muestra la lista de dispositivos móviles que se borraron recientemente de forma correcta.|  
|**Resumen de configuración para los dispositivos móviles administrados por el conector de Exchange Server**|Muestra el número de dispositivos móviles que aplican la configuración para cada directiva predeterminada de buzones de Exchange ActiveSync administrada por el conector de Exchange Server.|  
|**Estado detallado de claves de instalación de prueba de Windows RT**|Muestra información detallada de estado para una clave de instalación de prueba de Windows RT especificada.|  
|**Resumen de claves de instalación de prueba de Windows RT**|Muestra el estado de las claves de instalación de prueba de Windows RT.|  



## <a name="driver-management"></a>Administración de controladores  

Los trece informes siguientes aparecen en la categoría **Administración de controladores**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los controladores**|Muestra una lista de todos los controladores.|  
|**Todos los controladores para una plataforma específica**|Muestra todos los controladores para una plataforma específica.|  
|**Todos los controladores para una imagen de arranque específica**|Muestra todos los controladores para una imagen de arranque específica.|  
|**Todos los controladores para una categoría específica**|Muestra todos los controladores para una categoría específica.|  
|**Todos los controladores en un paquete específico**|Muestra todos los controladores para un paquete específico.|  
|**Categorías para un controlador específico**|Muestra las categorías para un controlador específico.|  
|**Equipos que no pudieron instalar controladores para una recopilación específica**|Muestra los equipos que no pudieron instalar controladores para una recopilación específica.|  
|**Informe de coincidencia del catálogo de controladores para una recopilación específica**|Muestra el informe de coincidencia del catálogo de controladores para una recopilación específica.|  
|**Informe de coincidencia del catálogo de controladores para un equipo específico**|Muestra el informe de coincidencia del catálogo de controladores para un equipo específico.|  
|**Informe de coincidencia del catálogo de controladores para un dispositivo específico en un determinado equipo**|Muestra el informe de coincidencia del catálogo de controladores para un dispositivo específico en un determinado equipo.|  
|**Informe de coincidencia del catálogo de controladores para los equipos de una recopilación específica con un determinado dispositivo**|Muestra el informe de coincidencia del catálogo de controladores para los equipos de una recopilación específica con un determinado dispositivo.|  
|**Controladores que no se pudieron instalar en un equipo específico**|Muestra los controladores que no se pudieron instalar en un equipo específico.|  
|**Plataformas admitidas para un controlador específico**|Muestra las plataformas admitidas para un controlador específico.|  



## <a name="endpoint-protection"></a>Endpoint Protection  

Los seis informes siguientes aparecen en la categoría **Endpoint Protection**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Informe de actividad de antimalware**|Muestra información general sobre la actividad de antimalware.|  
|**Historial y estado general de antimalware**|Muestra el historial y el estado general de antimalware.|  
|**Detalles de malware de equipos**|Muestra detalles de un equipo especificado y la lista de malware que se encontró en él.|  
|**Equipos infectados**|Muestra una lista de equipos con una amenaza específica detectada.|  
|**Usuarios principales por amenazas**|Muestra la lista de usuarios con el mayor número de amenazas detectadas.|  
|**Lista de amenazas de usuario**|Muestra la lista de amenazas detectadas para una cuenta de usuario especificada.|  



## <a name="hardware---cd-rom"></a>Hardware - CD-ROM  

Los cuatro informes siguientes aparecen en la categoría **Hardware - CD-ROM**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Información de CD-ROM para un equipo específico**|Muestra información sobre las unidades de CD-ROM en un equipo especificado.|  
|**Equipos para un fabricante de CD-ROM específico**|Muestra una lista de equipos que contienen una unidad de CD-ROM producida por el fabricante especificado.|  
|**Recuento de unidades de CD-ROM por fabricante**|Muestra el número de unidades de CD-ROM inventariadas por fabricante.|  
|**Historial - Historial de CD-ROM para un equipo específico**|Muestra el historial de inventario de las unidades de CD-ROM del equipo especificado.|  



## <a name="hardware---disk"></a>Hardware - Disco  

Los ocho informes siguientes aparecen en la categoría **Hardware - Disco**. 

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos con un tamaño de disco duro específico**|Muestra una lista de equipos que tienen discos duros del tamaño especificado.|  
|**Equipos con poco espacio libre en disco (menos de la cantidad especificada como %)**|Muestra una lista de los equipos de una recopilación especificada que tienen menos espacio libre en disco del especificado.|  
|**Equipos con poco espacio libre en disco (menos de la cantidad especificada en MB)**|Muestra una lista de los equipos y los discos en los que los discos tienen poco espacio. La cantidad de espacio libre que se va a buscar se especifica en MB.|  
|**Recuento de configuraciones de disco físico**|Muestra el número de discos duros inventariados por capacidad de disco.|  
|**Información de discos para un equipo específico: discos lógicos**|Muestra información de resumen sobre los discos lógicos en el equipo especificado.|  
|**Información de discos para un equipo específico - Particiones**|Muestra información de resumen sobre las particiones de disco en el equipo especificado.|  
|**Información de discos para un equipo específico - Discos físicos**|Muestra información resumida sobre los discos físicos en un equipo especificado.|  
|**Historial - Historial de espacio en discos lógicos para un equipo específico**|Muestra el historial de inventario de las unidades de disco lógico del equipo especificado.|  



## <a name="hardware---general"></a>Hardware - General  

Los cinco informes siguientes aparecen en la categoría **Hardware - General**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Información de equipo para un equipo específico**|Muestra información de resumen para un equipo específico|  
|**Equipos de un grupo de trabajo o dominio específico**|Muestra una lista de equipos en un grupo de trabajo o dominio especificados.|  
|**Clases de inventario asignadas a una recopilación específica**|Muestra las clases de inventario que se asignan a una recopilación especificada.|  
|**Clases de inventario habilitadas en un equipo específico**|Muestra las clases de inventario que se habilitan en un equipo especificado.|  
|**Información de dispositivo Windows AutoPilot**|Muestra la información de dispositivo de cliente que se necesita para el registro de Windows AutoPilot.|



## <a name="hardware---memory"></a>Hardware - Memoria  

Los cinco informes siguientes aparecen en la categoría **Hardware - Memoria**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos en que cambió la memoria física**|Muestra una lista de equipos en los que la cantidad de RAM cambió desde el último ciclo de inventario.|  
|**Equipos con una cantidad de memoria específica**|Muestra una lista de equipos que tienen una cantidad especificada de RAM (memoria física total redondeada al MB más cercano).|  
|**Equipos con poca memoria (menos o igual que la cantidad especificada en MB)**|Muestra una lista de equipos que tienen poca memoria. La cantidad de memoria que se va a buscar se especifica en MB.|  
|**Recuento de configuraciones de memoria**|Muestra el número de equipos inventariados por cantidad de RAM.|  
|**Información de memoria para un equipo específico**|Muestra información de resumen sobre la memoria del equipo especificado.|  



## <a name="hardware---modem"></a>Hardware - Módem  

Los tres informes siguientes aparecen en la categoría **Hardware - Módem**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos para un fabricante de módems específico**|Muestra una lista de equipos que tienen un módem de un fabricante especificado.|  
|**Recuento de módems por fabricante**|Muestra el número de módems inventariados por cada fabricante de módem.|  
|**Información de módem para un equipo específico**|Muestra información de resumen sobre el módem del equipo especificado.|  



## <a name="hardware---network-adapter"></a>Hardware: adaptador de red  

Los tres informes siguientes aparecen en la categoría **Hardware - Adaptador de red**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos con un adaptador de red específico**|Muestra una lista de equipos que tienen un adaptador de red especificado.|  
|**Recuento de adaptadores de red por tipo**|Muestra el número de tarjetas de adaptadores de red inventariadas de cada tipo.|  
|**Información de adaptador de red para un equipo específico**|Muestra información sobre los adaptadores de red instalados en un equipo especificado.|  



## <a name="hardware---processor"></a>Hardware - Procesador  

Los cinco informes siguientes aparecen en la categoría **Hardware - Procesador**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos para una velocidad de procesador específica**|Muestra una lista de equipos que tienen un procesador con una velocidad especificada.|  
|**Equipos con procesadores rápidos (más o igual que la velocidad de reloj especificada)**|Muestra una lista de equipos que tienen procesadores con una velocidad superior a la velocidad especificada.|  
|**Equipos con procesadores lentos (menos o igual que la velocidad de reloj especificada)**|Muestra una lista de equipos que tienen procesadores con una velocidad igual o inferior a la velocidad de reloj especificada.|  
|**Recuento de velocidades del procesador**|Muestra el número de equipos inventariados por velocidad del procesador.|  
|**Información de procesador para un equipo específico**|Muestra información sobre los procesadores instalados en un equipo especificado.|  



## <a name="hardware---scsi"></a>Hardware - SCSI  

Los cinco informes siguientes aparecen en la categoría **Hardware - SCSI**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos con un tipo de tarjeta SCSI específico**|Muestra una lista de equipos que tienen una tarjeta SCSI especificada instalada.|  
|**Recuento de tipos de tarjeta SCSI**|Muestra el número de tarjetas SCSI inventariadas por tipo de tarjeta.|  
|**Información de tarjeta SCSI para un equipo específico**|Muestra información sobre las tarjetas SCSI instaladas en un equipo especificado.|  



## <a name="hardware---security"></a>Hardware: seguridad

El siguiente informe aparece en la categoría **Hardware - Seguridad**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Detalles de estados de firmware en dispositivos**|Muestra los detalles de los estados de UEFI, SecureBoot y TPM. **Nota**: Este informe no existe en la versión 1810.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Hardware: tarjeta de sonido  

Los tres informes siguientes aparecen en la categoría **Hardware - SCSI**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos con una tarjeta de sonido específica**|Muestra una lista de equipos que tienen una tarjeta de sonido especificada.|  
|**Recuento de tarjetas de sonido**|Muestra el número de equipos inventariados por cada tipo de tarjeta de sonido.|  
|**Información de tarjeta de sonido para un equipo específico**|Muestra información de resumen sobre las tarjetas de sonido del equipo especificado.|  



## <a name="hardware---video-card"></a>Hardware: tarjeta de vídeo  

Los tres informes siguientes aparecen en la categoría **Hardware - Tarjeta de vídeo**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos con una tarjeta de vídeo específica**|Muestra una lista de equipos que tienen una tarjeta de vídeo especificada.|  
|**Recuento de tarjetas de vídeo por tipo**|Muestra una lista de todas las tarjetas de vídeo instaladas en los equipos. También muestra el número de cada tipo de tarjeta de vídeo.|  
|**Información de tarjeta de vídeo para un equipo específico**|Muestra información de resumen sobre las tarjetas de vídeo instaladas en el equipo especificado.|  



## <a name="migration"></a>Migración  

Los cinco informes siguientes aparecen en la categoría **Migración**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Clientes en la lista de exclusión**|Muestra los clientes que se excluyen de la migración.|  
|**Dependencia de una recopilación de Configuration Manager**|Muestra los objetos que dependen de una recopilación de la jerarquía de origen.|  
|**Propiedades del trabajo de migración**|Este informe muestra el contenido del trabajo de migración especificado.|  
|**Trabajos de migración**|Este informe muestra la lista de trabajos de migración.|  
|**Objetos que no se pudieron migrar**|Muestra una lista de objetos que no se pudieron migrar durante el último intento.|  



## <a name="network"></a>Network (Red)  

Los seis informes siguientes aparecen en la categoría **Red**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Recuento de direcciones IP por subred**|Muestra el número de direcciones IP inventariadas para cada subred IP.|  
|**IP - Todas las subredes por máscara de subred**|Muestra una lista de subredes IP y máscaras de subred.|  
|**IP - Equipos en una subred específica**|Muestra una lista de equipos y la información de IP para una subred IP especificada.|  
|**IP - Información para un equipo específico**|Muestra información de resumen sobre la IP del equipo especificado.|  
|**IP - Información para una dirección IP específica**|Muestra información de resumen sobre la dirección IP especificada.|  
|**MAC - Equipos para una dirección MAC específica**|Muestra el nombre del equipo y la dirección IP de los equipos que tienen la dirección MAC especificada.|  



## <a name="operating-system"></a>Sistema operativo  

Los diez informes siguientes aparecen en la categoría **Sistema operativo**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Historial de versiones del sistema operativo del equipo**|Muestra el historial de inventario del sistema operativo del equipo especificado.|  
|**Equipos con un sistema operativo específico**|Muestra los equipos con un sistema operativo específico.|  
|**Equipos con un sistema operativo y un Service Pack específicos**|Muestra los equipos con un sistema operativo y un Service Pack específicos.|  
|**Recuento de versiones de sistema operativo**|Muestra el número de equipos inventariados por sistema operativo.|  
|**Recuento de sistemas operativos y Service Packs**|Muestra el número de equipos inventariados por combinaciones de sistema operativo y Service Pack.|  
|**Servicios - Equipos que ejecutan un servicio específico**|Muestra una lista de equipos que ejecutan un servicio especificado.|  
|**Servicios - Equipos que ejecutan el servidor de acceso remoto**|Muestra una lista de equipos que ejecutan el servidor de acceso remoto.|  
|**Servicios - Información de servicios para un equipo específico**|Muestra información de resumen sobre los servicios del equipo especificado.|  
|**Detalles de mantenimiento de Windows 10 para una recopilación específica**|Muestra información general sobre el mantenimiento de Windows 10 para una recopilación específica.|
|**Equipos Windows Server**|Muestra una lista de equipos que ejecutan sistemas operativos Windows Server.|  


## <a name="power-management"></a>Administración de energía  

Los dieciocho informes siguientes aparecen en la categoría **Administración de energía**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Administración de energía - Actividad de equipo**|Muestra un gráfico con la actividad del monitor, el equipo y el usuario de una recopilación especificada durante un período de tiempo especificado.|  
|**Administración de energía - Actividad de equipo por equipo**|Muestra un gráfico con la actividad del monitor, el equipo y el usuario de un equipo especificado en una fecha especificada.|  
|**Administración de energía - Detalles de actividad de equipo**|Muestra una lista de las capacidades de suspensión y activación de los equipos de la recopilación especificada para una fecha y hora determinadas.|  
|**Administración de energía - Detalles de equipo**|Muestra información detallada sobre las funciones, configuraciones y planes de energía aplicados a un equipo especificado.|  
|**Administración de energía - El equipo no proporciona detalles**|Muestra una lista de equipos que no informan de ninguna actividad de energía para una fecha y hora especificadas.|  
|**Administración de energía - Equipos excluidos**|Muestra una lista de equipos excluidos del plan de energía.|  
|**Administración de energía - Equipos con varios planes de energía**|Muestra una lista de equipos que tienen aplicadas varias configuraciones de energía en conflicto.|  
|**Administración de energía - Consumo de energía**|Muestra el consumo energético mensual total (en kWh) para una recopilación especificada durante un determinado período de tiempo.|  
|**Administración de energía - Consumo de energía por día**|Muestra el consumo energético total (en kWh) para una recopilación especificada en los últimos 31 días.|  
|**Administración de energía - Costo de energía**|Muestra el costo del consumo energético mensual total para una recopilación especificada durante un determinado período de tiempo.|  
|**Administración de energía - Costo de energía por día**|Muestra el costo del consumo energético total para una recopilación especificada en los últimos 31 días.|  
|**Administración de energía - Impacto medioambiental**|Muestra un gráfico que representa las emisiones de dióxido de carbono (CO2) generadas por una recopilación especificada durante un determinado período de tiempo.|  
|**Administración de energía - Impacto medioambiental por día**|Muestra un gráfico que representa las emisiones de CO2 generadas por una recopilación especificada durante los últimos 31 días.|  
|**Administración de energía - Detalles de insomnio de equipo**|Muestra información detallada sobre los equipos que no se suspendieron ni hibernaron durante un período de tiempo especificado.|  
|**Administración de energía - Informe de insomnio**|Muestra una lista de las causas comunes que impidieron el modo de suspensión o hibernación en los equipos. También muestra el número de equipos afectados por cada causa durante un período de tiempo especificado.|  
|**Administración de energía - Capacidades de energía**|Muestra las capacidades de administración de energía de los equipos de la recopilación especificada.|  
|**Administración de energía - Configuración de energía**|Muestra una lista agregada de configuraciones de energía usadas por los equipos de una recopilación especificada.|  
|**Administración de energía - Detalles de configuración de energía**|Se usa para mostrar información adicional sobre los equipos que se especificaron en el informe **Administración de energía - Configuración de energía**.|  



## <a name="replication-traffic"></a>Tráfico de replicación  

Los diez informes siguientes aparecen en la categoría **Tráfico de replicación**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Tráfico de replicación de datos globales por vínculo (gráfico de líneas)**|Muestra el tráfico total de replicación de datos globales en un vínculo especificado para el número de días especificado.|  
|**Tráfico de replicación de datos globales por vínculo (gráfico circular)**|Muestra el tráfico total de replicación de datos globales en un vínculo especificado para el número de días especificado.|  
|**Tráfico de replicación de jerarquía por vínculo**|Muestra el tráfico de replicación en total para cada vínculo de la jerarquía durante un número de días especificado.|  
|**Tráfico de los diez grupos de replicación principales de la jerarquía por vínculo (gráfico circular)**|Muestra el tráfico de replicación para los diez grupos de replicación principales de toda la jerarquía identificados por vínculo.|  
|**Tráfico de replicación del vínculo**|Muestra el tráfico de replicación en total de todos los datos durante un número de días especificado.|  
|**Tráfico de grupo de replicación por vínculo**|Muestra el tráfico de red del grupo de replicación en un vínculo de replicación de base de datos especificado durante un número de días especificado.|  
|**Tráfico de replicación de datos de sitio por vínculo (gráfico de líneas)**|Muestra el tráfico total de replicación de datos del sitio en un vínculo especificado para el número de días especificado.|  
|**Tráfico de replicación de datos del sitio por vínculo (gráfico circular)**|Muestra el tráfico total de replicación de datos del sitio en un vínculo especificado para el número de días especificado.|  
|**Tráfico de replicación de jerarquía en total (gráfico de líneas)**|Muestra la replicación de datos del sitio y de la jerarquía global agregada para cada una de las direcciones de los vínculos durante un número de días especificado.|  
|**Tráfico de replicación de jerarquía en total (gráfico circular)**|Muestra la replicación de datos del sitio y de la jerarquía global agregada para cada una de las direcciones de los vínculos durante un número de días especificado.|  



## <a name="site---client-information"></a>Sitio: información del cliente  

Los diecinueve informes siguientes aparecen en la categoría **Sitio - Información del cliente**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Informe de estado detallado de asignación de cliente**|Muestra información detallada sobre el estado de asignación de cliente.|  
|**Detalles de error de asignación de cliente**|Muestra información detallada sobre los errores de asignación de cliente.|  
|**Detalles de estado de asignación de cliente**|Muestra información general sobre el estado de asignación de cliente.|  
|**Detalles de asignación correcta de cliente**|Muestra información detallada sobre los clientes asignados correctamente.|  
|**Informe de error de implementación de cliente**|Muestra información detallada para los clientes con errores de implementación.|  
|**Detalles de estado de implementación de cliente**|Muestra información de resumen para el estado de las instalaciones de cliente.|  
|**Informe de implementación correcta de cliente**|Muestra información detallada para los clientes con una implementación correcta.|  
|**Clientes sin capacidad de comunicación HTTPS**|Muestra información detallada sobre todos los clientes que ejecutan la herramienta HTTPS Communication Readiness Tool y que notifican no tener capacidad de comunicación sobre HTTPS.|  
|**Equipos asignados pero no instalados para un sitio en particular**|Muestra una lista de los equipos que se asignaron a un sitio especificado, pero que no informan a ese sitio.|  
|**Equipos con una versión de cliente de Configuration Manager específica**|Muestra una lista de equipos que ejecutan una versión especificada del software de cliente de Configuration Manager.|  
|**Recuento de clientes y protocolo usado para la comunicación**|Muestra un resumen de los métodos de comunicación usados por los clientes (HTTP o HTTPS).|  
|**Recuento de clientes asignados e instalados para cada sitio**|Muestra el número de equipos asignados e instalados para cada sitio. Los clientes con una ubicación de red asociada a varios sitios solo se cuentan como instalados si informan a ese sitio.|  
|**Recuento de clientes con capacidad de comunicación HTTPS**|Muestra información detallada sobre todos los clientes que ejecutan la herramienta HTTPS Communication Readiness Tool y que notifican tener o no tener capacidad de comunicación sobre HTTPS.|  
|**Recuento de clientes para cada sitio**|Muestra el número de clientes de Configuration Manager instalados por código de sitio.|  
|**Recuento de clientes de Configuration Manager por versiones de cliente**|Muestra el número de equipos detectados por la versión de cliente de Configuration Manager.|  
|**Detalles de problemas notificados al punto de estado de reserva para una recopilación especificada**|Muestra información detallada de los problemas notificados por los clientes en una recopilación especificada. Estos clientes deben tener un punto de estado de reserva asignado.|  
|**Detalles de problemas notificados al punto de estado de reserva para un sitio especificado**|Muestra información detallada sobre los problemas notificados por los clientes en un sitio especificado. Estos clientes deben tener un punto de estado de reserva asignado.|  
|**Resumen de problemas notificados al punto de estado de reserva**|Muestra información sobre todos los problemas notificados por los clientes. Estos clientes deben tener un punto de estado de reserva asignado.|  
|**Resumen de problemas notificados al punto de estado de reserva para una recopilación específica**|Muestra información de resumen de los problemas notificados por los clientes en una recopilación especificada. Estos clientes deben tener un punto de estado de reserva asignado.|  



## <a name="site---discovery-and-inventory-information"></a>Sitio: información de detección e inventario  

Los diez informes siguientes aparecen en la categoría **Sitio - Información de detección e inventario**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Clientes que no informaron recientemente (en un número de días especificado)**|Muestra una lista de clientes que no han notificado datos de detección, inventario de hardware o inventario de software en un número de días especificado.|  
|**Equipos detectados por un sitio específico**|Muestra una lista de todos los equipos detectados por el sitio especificado. También muestra la fecha de la detección más reciente.|  
|**Equipos detectados recientemente por método de detección**|Muestra una lista de los equipos detectados por el sitio en el número de días especificado. También se enumeran los agentes que los detectaron. Si varios agentes detectaron un equipo, puede aparecer más de una vez en la lista.|  
|**Equipos no detectados recientemente (en un número de días especificado)**|Muestra una lista de los equipos que el sitio no ha detectado recientemente. También muestra el número de días desde que el sitio detectó el equipo.|  
|**Equipos no inventariados recientemente (en un número de días especificado)**|Muestra una lista de los equipos de los que el sitio no ha hecho inventario recientemente. También muestra las últimas veces que el cliente inventarió el equipo.|  
|**Los equipos que podrían compartir el mismo identificador único de Configuration Manager**|Muestra una lista de equipos cuyos nombres cambiaron. Un cambio de nombre es una posible indicación de que un equipo comparte un identificador único de Configuration Manager con otro equipo.|  
|**Equipos con direcciones MAC duplicadas**|Muestra los equipos que comparten la dirección MAC.|  
|**Recuento de equipos en dominios de recursos o grupos de trabajo**|Muestra el número de equipos de cada dominio de recursos o grupo de trabajo.|  
|**Información de detección para un equipo específico**|Muestra una lista de los agentes y los sitios que detectaron un equipo especificado.|  
|**Fechas de inventario para un equipo específico**|Muestra la fecha y la hora en que el inventario se ejecutó por última vez en un equipo especificado.|  



## <a name="site---general"></a>Sitio - General  

Los tres informes siguientes aparecen en la categoría **Sitio - General**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos en un sitio específico**|Muestra una lista de equipos cliente en un sitio especificado.|  
|**Estado de sitio para la jerarquía**|Muestra la lista de sitios en la jerarquía con información de versión de sitio y estado de sitio.|  
|**Estado de actualización de Configuration Manager dentro de la jerarquía**|Muestra información acerca de las actualizaciones del sitio de Configuration Manager para la jerarquía.|  



## <a name="site---server-information"></a>Sitio: información del servidor  

El informe siguiente aparece en la categoría **Sitio - Información del cliente**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Roles de sistema de sitio y servidores de sistema de sitio para un sitio específico**|Muestra una lista de servidores de sistema de sitio y sus roles de sistema de sitio para un sitio especificado.|  



## <a name="software---companies-and-products"></a>Software: compañías y productos  

Los quince informes siguientes aparecen en la categoría **Software - Compañías y productos**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los productos inventariados para una compañía de software específica**|Muestra una lista de los productos de software inventariados y sus versiones de una compañía de software especificada.|  
|**Todas las compañías de software**|Muestra una lista de todas las compañías que fabrican software inventariado.|  
|**Todas las aplicaciones de Windows**|Muestra un resumen de las aplicaciones de Windows instaladas. Busca mediante los criterios siguientes: nombre de la aplicación, arquitectura o editor.|  
|**Equipos con un producto específico**|Muestra una lista de los equipos en los que está inventariado un producto determinado, así como las versiones de ese producto.|  
|**Equipos con un nombre y versión de producto específicos**|Muestra una lista de los equipos en los que está inventariada una versión especificada de un producto.|  
|**Equipos con software específico registrado en Agregar o quitar programas**|Muestra un resumen de todos los equipos con software especificado registrado en Agregar o quitar programas o Programas y características.|  
|**Recuento de todos los productos y versiones inventariados**|Muestra una lista de los productos y versiones de software inventariados, así como el número de equipos en los que está instalado cada uno.|  
|**Recuento de productos y versiones inventariados para un producto específico**|Muestra una lista de las versiones inventariadas de un producto especificado, así como el número de equipos en los que está instalada cada una.|  
|**Recuento de todas las instancias de software registradas con Agregar o quitar programas**|Muestra un resumen de todas las instancias de software instaladas y registradas con Agregar o quitar programas o Programas y características en equipos de la recopilación especificada.|  
|**Recuento de instancias de software específico registradas con Agregar o quitar programas**|Muestra un recuento de instancias de los paquetes del software especificado instaladas y registradas con Agregar o quitar programas o Programas y características.|  
|**Cantidad de exploradores predeterminados**|Muestra la cantidad de clientes con un explorador web específico como el predeterminado de Windows. <br>Utilice la siguiente referencia para los valores BrowserProgID más habituales:<br> - AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge<br> - IE.HTTP: Microsoft Internet Explorer<br> - ChromeHTML: Google Chrome<br> - OperaStable: Opera Software<br> - FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> - Desconocido: el sistema operativo de cliente no es compatible con la consulta, la consulta no se ha ejecutado o un usuario no ha iniciado sesión|
|**Instalaciones de aplicaciones de Windows especificadas**|En este informe se enumeran todos los equipos con una aplicación de Windows especificada.|  
|**Productos en un equipo específico**|Muestra un resumen de los productos de software inventariados y sus fabricantes en un equipo especificado.|  
|**Software registrado en Agregar o quitar programas en un equipo específico**|Muestra un resumen del software instalado en el equipo especificado que se registró en Agregar o quitar programas o Programas y características.|  
|**Aplicaciones de Windows instaladas para el usuario especificado**|Muestra todas las aplicaciones de Windows instaladas para el usuario especificado|  



## <a name="software---files"></a>Software - Archivos  

Los cinco informes siguientes aparecen en la categoría **Software - Archivos**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los archivos inventariados para un producto específico**|Mostrar un resumen de los archivos inventariados que están asociados con un producto de software especificado.|  
|**Todos los archivos inventariados en un equipo específico**|Muestra un resumen de todos los archivos inventariados en un equipo especificado.|  
|**Comparar inventario de software en dos equipos**|Muestra las diferencias entre los inventarios de software notificados para dos equipos especificados.|  
|**Equipos con un archivo específico**|Muestra una lista de equipos que recopilaron el inventario de software para un nombre de archivo especificado. Si un equipo contiene varias copias del archivo, es posible que aparezca más de una vez en la lista.|  
|**Recuento de equipos con un nombre de archivo específico**|Muestra el número de equipos que recopilaron el inventario de software para un archivo especificado.|  



## <a name="software-distribution---application-monitoring"></a>Distribución de software: supervisión de aplicaciones  

Los diez informes siguientes aparecen en la categoría **Distribución de software - Supervisión de aplicaciones**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todas las implementaciones de aplicaciones (avanzado)**|Muestra información de resumen detallada para todas las implementaciones de la aplicación.|  
|**Todas las implementaciones de aplicaciones (básico)**|Muestra información de resumen para todas las implementaciones de la aplicación.|  
|**Compatibilidad de aplicación**|Muestra información de compatibilidad para la aplicación especificada en la recopilación especificada.|  
|**Implementaciones de aplicación por activo**|Muestra las aplicaciones implementadas para un dispositivo o un usuario especificados.|  
|**Errores de infraestructura de aplicación**|Muestra errores de infraestructura de aplicación. Estos errores incluyen los problemas de infraestructura interna, o bien errores resultantes de reglas de requisitos no válidas.|  
|**Estado detallado del uso de aplicaciones**|Muestra los detalles de uso de las aplicaciones instaladas.|  
|**Estado de resumen del uso de aplicaciones**|Muestra un resumen del uso de las aplicaciones instaladas.|  
|**Implementaciones de secuencia de tareas que contienen aplicación**|Muestra las implementaciones de secuencia de tareas que instalan una aplicación especificada.|  


## <a name="software-distribution---collections"></a>Distribución de software: recopilaciones  

Los tres informes siguientes aparecen en la categoría **Distribución de software - Recopilaciones**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todas las colecciones**|Muestra todas las recopilaciones de la jerarquía.|  
|**Todos los recursos de una recopilación específica**|Muestra todos los recursos de una recopilación especificada.|  
|**Ventanas de mantenimiento disponibles para un cliente especificado**|Muestra todas las ventanas de mantenimiento que se aplican al cliente especificado.|  



## <a name="software-distribution---content"></a>Distribución de software: contenido  

Los dieciséis informes siguientes aparecen en la categoría **Distribución de software - Contenido**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todas las distribuciones de contenido activas**|Muestra todos los puntos de distribución en los que se está instalando o quitando contenido actualmente.|  
|**Todo el contenido**|Muestra todas las aplicaciones y paquetes de un sitio.|  
|**Todo el contenido de un punto de distribución específico**|Muestra todo el contenido instalado actualmente en un punto de distribución especificado.|  
|**Todos los puntos de distribución**|Muestra información sobre los puntos de distribución para cada sitio.|  
|**Todos los mensajes de estado para un paquete específico en un determinado punto de distribución**|Muestra todos los mensajes de estado para un paquete específico en un determinado punto de distribución.|  
|**Estado de distribución del contenido de la aplicación**|Muestra información sobre el estado de distribución para el contenido de la aplicación.|  
|**Aplicaciones dirigidas a un grupo de puntos de distribución**|Muestra información sobre el contenido de la aplicación que se implementó en un grupo de puntos de distribución especificado.|  
|**Aplicaciones que no están sincronizadas en un grupo de puntos de distribución especificado**|Muestra las aplicaciones para las que no se han actualizado los archivos de contenido asociados con la última versión de un grupo de puntos de distribución especificado.|  
|**Grupo de puntos de distribución**|Muestra información sobre un grupo de puntos de distribución especificado.|  
|**Resumen de uso de los puntos de distribución**|Muestra el resumen de uso de cada punto de distribución.|  
|**Estado de distribución del paquete especificado**|Muestra el estado de distribución para contenido de paquete especificado en cada punto de distribución.|  
|**Paquetes dirigidos a un grupo de puntos de distribución**|Muestra información sobre los paquetes dirigidos a un grupo de puntos de distribución especificado.|  
|**Paquetes que no están sincronizados en un grupo de puntos de distribución especificado**|Muestra los paquetes para los que no se han actualizado los archivos de contenido asociados con la última versión de un grupo de puntos de distribución especificado.|  
|**Rechazo del contenido de origen de la caché del mismo nivel**|Muestra el número de rechazos de origen de la caché del mismo nivel por grupo de límites.|
|**Rechazo del contenido de origen de la caché del mismo nivel por condición**|Muestra los orígenes de la caché del mismo nivel que rechazaron servir contenido según una condición.|
|**Detalles del rechazo del contenido de origen de la caché del mismo nivel**|Muestra el nombre del contenido que rechazó un origen del mismo nivel.|



## <a name="software-distribution---package-and-program-deployment"></a>Distribución de software: implementación de paquete y programa 

Los cinco informes siguientes aparecen en la categoría **Distribución de software - Implementación de paquete y programa**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todas las implementaciones de un paquete y un programa especificados**|Muestra información sobre todas las implementaciones de un paquete y un programa especificados.|  
|**Todas las implementaciones de paquete y programa**|Muestra todas las implementaciones del paquete y el programa en este sitio.|  
|**Todas las implementaciones de paquete y programa en una recopilación especificada**|Muestra todas las implementaciones de paquete y programa en una recopilación especificada.|  
|**Todas las implementaciones de paquete y programa en un equipo especificado**|Muestra todas las implementaciones de paquete y programa que se aplican en un equipo especificado.|  
|**Todas las implementaciones de paquete y programa en un usuario especificado**|Muestra todas las implementaciones de paquete y programa en un usuario especificado.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Distribución de software: estado de implementación de paquete y programa  

Los cinco informes siguientes aparecen en la categoría **Distribución de software - Estado de implementación de paquete y programa**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los recursos de sistema para implementaciones de paquete y programa con estado**|Muestra todas las implementaciones paquete y programa para el sitio con un estado de resumen de cada implementación.|  
|**Todos los recursos de sistema para una implementación de paquete y programa especificada en un determinado estado**|Muestra una lista de recursos que se encuentran en un estado especificado para una implementación de paquete y programa especificada.|  
|**Gráfico - Estado de finalización de implementaciones de paquete y programa por hora**|Muestra el porcentaje de equipos que instalaron correctamente el paquete. La lista se organiza por cada hora desde que un administrador crea la implementación de paquete y programa. Se puede usar para realizar un seguimiento del tiempo medio para una implementación de paquete y programa.|  
|**Estado de implementación de paquete y programa para un cliente y una implementación especificados**|Muestra los mensajes de estado notificados para un equipo especificado y la implementación de paquete y programa.|  
|**Estado de una implementación de paquete y programa especificada**|Muestra el resumen de estado de una implementación de paquete y programa especificada.|  



## <a name="software-metering"></a>Disponibilidad de software  

Los trece informes siguientes aparecen en la categoría **Medición de software**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todas las reglas de disponibilidad de software aplicadas a este sitio**|Muestra una lista de todas las reglas de disponibilidad de software del sitio.|  
|**Equipos que tienen un programa medido instalado pero que no han ejecutado el programa desde una fecha especificada**|Muestra todos los equipos con la aplicación de uso medido especificada, pero ningún usuario ha ejecutado el programa desde la fecha especificada.|  
|**Equipos que ejecutaron un programa de software medido específico**|Muestra una lista de equipos que ejecutaron los programas que coinciden con la regla de disponibilidad de software especificada en el mes y el año especificados.|  
|**Uso simultáneo para todos los programas de software medidos**|Muestra el número máximo de usuarios que ejecutaron simultáneamente cada programa de software medido en el mes y año especificados.|  
|**Análisis de tendencias de uso simultáneo de un programa de software medido específico**|Muestra el número máximo de usuarios que ejecutaron simultáneamente el programa de software medido especificado en todos los meses del año pasado.|  
|**Base de instalación para todos los programas de software medidos**|Muestra el número de equipos que tienen programas de software medidos instalados como indica el inventario de software. Este informe requiere que el equipo recopile el inventario de software.|  
|**Progreso del resumen de disponibilidad de software**|Muestra la hora a la que se procesaron los datos de medición resumidos más recientemente en el servidor de sitio. Los informes de medición de software solo reflejan los datos de medición procesados antes de estas fechas.|  
|**Resumen de uso por horas del día para un programa de software medido específico**|Muestra el promedio de uso de un programa determinado en los últimos 90 días, desglosado por hora y día.|  
|**Uso total para todos los programas de software medidos**|Muestra el número de usuarios que ejecutaron programas en el mes y año especificados, y que coinciden con cada regla de medición de software. Estas reglas son para el software instalado localmente o mediante Terminal Services.|  
|**Uso total para todos los programas de software medidos en servidores de Windows Terminal Server**|Muestra el número de usuarios que ejecutaron programas que coinciden con cada regla de disponibilidad de software usando Terminal Services en el mes y año especificados.|  
|**Análisis de tendencias de uso total para un programa de software medido específico**|Muestra el número de usuarios que ejecutaron programas durante todos los meses del año pasado y que coinciden con la regla de medición de software especificada. Estas reglas son para el software instalado localmente o mediante Terminal Services.|  
|**Análisis de tendencias de uso total para un programa de software medido específico en servidores de Windows Terminal Server**|Muestra el número de usuarios que ejecutaron programas durante todos los meses del año pasado y que coinciden con la regla de medición de software especificada. Estas reglas son para el uso de Terminal Services.|  
|**Usuarios que ejecutaron un programa de software medido específico**|Muestra una lista de los usuarios que han ejecutado programas en el mes y el año especificados, y que coinciden con la regla de medición de software especificada.|  



## <a name="software-updates---a-compliance"></a>Actualizaciones de software: A Cumplimiento  

Los ocho informes siguientes aparecen en la categoría **Actualizaciones de software - A Cumplimiento**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Cumplimiento 1 - Cumplimiento general**|Muestra los datos de cumplimiento general de un grupo de actualizaciones de software.|  
|**Cumplimiento 2 - Actualización de software específica**|Muestra los datos de cumplimiento para una actualización de software especificada.|  
|**Cumplimiento 3 - Grupo de actualización (por actualización)**|Muestra los datos de cumplimiento de las actualizaciones de software que se definen en un grupo de actualizaciones de software.|  
|**Cumplimiento 4 - Actualizaciones por proveedor, mes y año**|Muestra los datos de cumplimiento de las actualizaciones de software publicadas por un proveedor durante un mes y un año especificados.|  
|**Cumplimiento 5 - Equipo específico**|Este informe devuelve los datos de cumplimiento de la actualización de software para un equipo específico. Para limitar la cantidad de información devuelta, puede especificar el proveedor y la clasificación de la actualización de software.|  
|**Cumplimiento 6 - Estados de actualización de software específica (secundario)**|Muestra el recuento y el porcentaje de equipos en cada estado de cumplimiento para la actualización de software especificada.|  
|**Cumplimiento 7 - Equipos en un estado de cumplimiento específico para un grupo de actualización (secundario)**|Muestra todos los equipos de una recopilación que tienen un estado de cumplimiento general especificado en un grupo de actualizaciones de software.|  
|**Cumplimiento 8 - Equipos en un estado de cumplimiento específico para una actualización (secundario)**|Muestra todos los equipos de una recopilación que tienen un estado de cumplimiento especificado para una actualización de software.|  
|**Cumplimiento 9: Estado general y cumplimiento**|Muestra los datos de cumplimiento y estado general de un grupo de actualizaciones de software. (A partir de la versión 1806).| 


## <a name="software-updates---b-deployment-management"></a>Actualizaciones de software: B Administración de implementación  

Los ocho informes siguientes aparecen en la categoría **Actualizaciones de software - B Administración de implementación**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Administración 1 - Implementaciones de un grupo de actualización**|Muestra todas las implementaciones que incluyen todas las actualizaciones de software que se definen en un grupo de actualizaciones de software especificado.|  
|**Administración 2 - Actualizaciones necesarias pero no implementadas**|Muestra todas las actualizaciones de software específicas del proveedor que los clientes detectan como necesarias pero que un administrador no ha implementado en una recopilación especificada.|  
|**Administración 3 - Actualizaciones en una implementación**|Muestra las actualizaciones de software que se encuentran en una implementación especificada.|  
|**Administración 4 - Implementaciones dirigidas a una recopilación**|Muestra todas las implementaciones de actualización de software destinadas a una recopilación especificada.|  
|**Administración 5 - Implementaciones dirigidas a un equipo**|Muestra todas las implementaciones de actualización de software implementadas en un equipo especificado.|  
|**Administración 6 - Implementaciones que contienen una actualización específica**|Muestra todas las implementaciones que incluyen una actualización de software especificada y la recopilación de destino asociada para la implementación.|  
|**Administración 7 - Actualizaciones en una implementación a la que falta contenido**|Muestra las actualizaciones de software de una implementación especificada que no han recuperado todo el contenido asociado. Este estado impide que los clientes instalen la actualización, lo que impide que la implementación consiga un cumplimiento del 100 %.|  
|**Administración 8 - Equipos a los que falta contenido (secundario)**|Muestra todos los equipos que requieren la actualización de software especificada, pero el contenido asociado todavía no se ha distribuido a un punto de distribución.|  



## <a name="software-updates---c-deployment-states"></a>Actualizaciones de software: C Estados de implementación  

Los seis informes siguientes aparecen en la categoría **Actualizaciones de software - C Estados de implementación**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Estados 1 - Estados de aplicación para una implementación**|Muestra los estados de aplicación para una implementación de actualización de software específica, que suele ser la segunda fase de una evaluación de implementación.|  
|**Estados 2 - Estados de evaluación para una implementación**|Muestra el estado de evaluación para una implementación de actualización de software específica, que suele ser la primera fase de una evaluación de implementación.|  
|**Estados 3 - Estados para una implementación y un equipo**|Muestra los estados de todas las actualizaciones de software en la implementación especificada para un equipo especificado.|  
|**Estados 4 - Equipos en un estado específico para una implementación (secundario)**|Muestra todos los equipos en un estado especificado para una implementación de actualización de software.|  
|**Estados 5 - Estados para una actualización en una implementación (secundario)**|Muestra un resumen de los estados para una actualización de software especificada de destino de una implementación especificada.|  
|**Estados 6 - Equipos en un estado de aplicación específico para una actualización (secundario)**|Muestra todos los equipos en un estado de aplicación especificado para una actualización de software especificada.|  



## <a name="software-updates---d-scan"></a>Actualizaciones de software: D Examen  

Los cuatro informes siguientes aparecen en la categoría **Actualizaciones de software - D Examen**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Examen 1 - Últimos estados de examen por recopilación**|Especifique una recopilación para mostrar el número de equipos en cada estado de examen de cumplimiento. Los clientes devuelven el estado durante el último examen de cumplimiento.|  
|**Examen 2 - Últimos estados de examen por sitio**|Especifique un sitio para mostrar el número de equipos en cada estado de examen de cumplimiento. Los clientes devuelven el estado durante el último examen de cumplimiento.|  
|**Examen 3 - Clientes de una recopilación que informan de un estado específico (secundario)**|Muestra todos los equipos de una recopilación especificada y un estado de examen de cumplimiento especificado durante su último examen de cumplimiento.|  
|**Examen 4 - Clientes de un sitio que informan de un estado específico (secundario)**|Especifique un sitio para mostrar todos los equipos con un estado de examen de cumplimiento especificado. Los clientes devuelven el estado durante su último examen de cumplimiento.|  



## <a name="software-updates---e-troubleshooting"></a>Actualizaciones de software: E Solución de problemas  

Los cuatro informes siguientes aparecen en la categoría **Actualizaciones de software - E Solución de problemas**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Solución de problemas 1 - Errores de examen**|Muestra los errores de examen en el sitio y el recuento de equipos que experimentan cada error.|  
|**Solución de problemas 2 - Errores de implementación**|Muestra los errores de implementación en el sitio y el recuento de equipos que experimentan cada error.|  
|**Solución de problemas 3 - Equipos con un error de examen específico (secundario)**|Muestra una lista de los equipos en los que se produjo un error de examen debido a un error especificado.|  
|**Solución de problemas 4 - Equipos con un error de implementación específico (secundario)**|Muestra una lista de los equipos en los que se produce un error en la implementación de la actualización debido a un error especificado.|  



## <a name="state-migration"></a>Migración de estado  

Los tres informes siguientes aparecen en la categoría **Migración de estado**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Información de migración de estado para un equipo de origen específico**|Muestra información de migración de estado para un equipo específico.|  
|**Información de migración de estado para un punto de migración de estado específico**|Muestra información de migración de estado para un punto de migración de estado específico.|  
|**Puntos de migración de estado para un sitio específico**|Muestra los puntos de migración de estado para un sitio específico.|  



## <a name="status-messages"></a>Mensajes de estado  

Los doce informes siguientes aparecen en la categoría **Mensajes de estado**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los mensajes para un identificador de mensaje específico**|Muestra una lista de mensajes de estado que tienen un identificador de mensaje especificado.|  
|**Clientes que informan de errores en las últimas 12 horas para un sitio específico**|Muestra una lista de equipos y componentes que informan de errores en las últimas 12 horas, así como el número de errores notificados.|  
|**Mensajes de componentes para las últimas 12 horas**|Muestra una lista de mensajes de componentes para las últimas 12 horas para un código de sitio, equipo y componente especificados.|  
|**Mensajes de componentes en la última hora**|Muestra una lista de los mensajes de estado creados en la última hora por un componente especificado en un determinado equipo de un sitio especificado.|  
|**Recuento de mensajes de componentes en la última hora para un sitio específico**|Muestra el número de mensajes de estado por componente y gravedad notificada en la última hora en un sitio especificado.|  
|**Recuento de errores en las últimas 12 horas**|Muestra el número de mensajes de estado de error de componente de servidor en las últimas 12 horas.|  
|**Errores irrecuperables (por componente)**|Muestra una lista de equipos que notifican errores irrecuperables por componente.|  
|**Errores irrecuperables (por nombre de equipo)**|Muestra una lista de equipos que notifican errores irrecuperables por nombre de equipo.|  
|**Últimos 1000 mensajes para un equipo específico (errores y advertencias)**|Muestra un resumen de los últimos 1000 mensajes de estado de componente de errores y advertencias para un equipo especificado.|  
|**Últimos 1000 mensajes para un equipo específico (errores, advertencias e información)**|Muestra un resumen de los últimos 1000 mensajes de estado de componente de errores, advertencias e información para un equipo especificado.|  
|**Últimos 1000 mensajes para un equipo específico (errores)**|Muestra un resumen de los últimos 1000 mensajes de estado de componente de servidor de errores para un equipo especificado.|  
|**Últimos 1000 mensajes para un componente del servidor específico**|Muestra un resumen de los 1000 mensajes de estado más recientes para un componente de servidor especificado.|  



## <a name="status-messages---audit"></a>Mensajes de estado: auditoría  

Los tres informes siguientes aparecen en la categoría **Mensajes de estado - Auditoría**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los mensajes de auditoría para un usuario específico**|Muestra un resumen de todos los mensajes de estado de auditoría para un usuario especificado. Mensajes de auditoría describen las acciones realizadas en la consola de Configuration Manager que agregan, modifican o eliminan objetos en Configuration Manager.|  
|**Control remoto - Todos los equipos controlados remotamente por un usuario específico**|Muestra un resumen de mensajes de estado que indica el control remoto de equipos cliente por parte de un usuario especificado.|  
|**Control remoto - Toda la información de control remoto**|Muestra un resumen de los mensajes de estado relacionados con el control remoto de equipos cliente.|  



## <a name="task-sequence---deployment-status"></a>Secuencia de tareas: estado de implementación  

Los once informes siguientes aparecen en la categoría **Secuencia de tareas - Estado de implementación**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los recursos de sistema para una implementación de secuencia de tareas en un estado específico**|Muestra una lista de los equipos de destino para la implementación de secuencia de tareas especificada en un estado de implementación especificado.|  
|**Todos los recursos de sistema para una implementación de secuencia de tareas que se encuentra en un estado específico y que está disponible para equipos desconocidos**|Muestra una lista de los equipos de destino para la implementación de secuencia de tareas especificada que se encuentra en un estado de implementación especificado.|  
|**Recuento de recursos de sistema que tienen asignadas implementaciones de secuencias de tareas aún no ejecutadas**|Muestra el número de equipos que han aceptado secuencias de tareas, pero no han ejecutado la secuencia de tareas.|  
|**Historial de una implementación de secuencia de tareas en un equipo**|Muestra el estado de cada paso de la implementación de secuencia de tareas especificada en el equipo de destino especificado. Si no se devuelve ningún registro, significa que la secuencia de tareas no se ha iniciado en el equipo.|  
|**Lista de equipos que superaron un período de tiempo especificado para ejecutar una implementación de secuencia de tareas**|Muestra la lista de equipos de destino que superaron el tiempo especificado para ejecutar una secuencia de tareas.|  
|**Tiempo de ejecución para una implementación de secuencia de tareas específica en un determinado equipo de destino**|Muestra el tiempo total que tardó en completarse correctamente una secuencia de tareas especificada en un equipo especificado.|  
|**Tiempo de ejecución para cada paso de una implementación de secuencia de tareas en un determinado equipo de destino**|Muestra el tiempo que se tardó en completar cada paso de la implementación de secuencia de tareas especificada en el equipo de destino especificado.|  
|**Estado de una implementación de secuencia de tareas específica para un determinado equipo**|Muestra el resumen de estado de una implementación de secuencia de tareas especificada en un equipo especificado.|  
|**Estado de una implementación de secuencia de tareas en un equipo de destino desconocido**|Muestra el estado de la implementación de secuencia de tareas especificada en el equipo de destino desconocido especificado.|  
|**Resumen de estado de una implementación de secuencia de tareas específica**|Muestra un resumen de estado de todos los recursos de destino de una implementación.|  
|**Resumen de estado de una implementación de secuencia de tareas específica disponible para equipos desconocidos**|Muestra el resumen de estado de todos los recursos de destino de la implementación especificada que está disponible para una recopilación que contiene equipos desconocidos.|  



## <a name="task-sequence---deployments"></a>Secuencia de tareas: implementaciones  

Los once informes siguientes aparecen en la categoría **Secuencia de tareas - Implementaciones**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los recursos de sistema actualmente en un grupo o fase específicos de una determinada implementación de secuencia de tareas**|Muestra una lista de los equipos que se están ejecutando en un grupo o fase especificados de una determinada implementación de secuencia de tareas.|  
|**Todos los recursos de sistema con una implementación de secuencia de tareas con errores dentro de un grupo o fase específicos**|Muestra una lista de los equipos con errores en un grupo o fase especificados de la implementación de secuencia de tareas especificada.|  
|**Todas las implementaciones de secuencias de tareas**|Muestra los detalles de todas las implementaciones de secuencia de tareas iniciadas desde el sitio actual.|  
|**Todas las implementaciones de secuencias de tareas disponibles para equipos desconocidos**|Muestra los detalles de todas las implementaciones de secuencia tareas iniciadas desde el sitio e implementadas en recopilaciones que contienen equipos desconocidos.|  
|**Recuento de errores en cada fase o grupo de una secuencia de tareas específica**|Muestra el número de errores en cada fase o grupo de la secuencia de tareas especificada.|  
|**Recuento de errores en cada fase o grupo de una implementación de secuencia de tareas específica**|Muestra el número de errores en cada fase o grupo de la implementación de secuencia de tareas especificada.|  
|**Estado de implementación de todas las implementaciones de secuencias de tareas**|Muestra el progreso global de todas las implementaciones de secuencia de tareas.|  
|**Progreso de una secuencia de tareas en ejecución**|Muestra el progreso de la secuencia de tareas especificada.|  
|**Progreso de una implementación de secuencia de tareas en ejecución**|Muestra la información de resumen para la implementación de secuencia de tareas especificada.|  
|**Progreso de todas las implementaciones para una secuencia de tareas específica**|Muestra el progreso de todas las implementaciones para la secuencia de tareas especificada.|  
|**Informe de resumen para una implementación de secuencia de tareas**|Muestra la información de resumen para la implementación de secuencia de tareas especificada.|  



## <a name="task-sequence---progress"></a>Secuencia de tareas: progreso  

Los cinco informes siguientes aparecen en la categoría **Secuencia de tareas - Progreso**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Gráfico - Progreso semanal de una secuencia de tareas**|Muestra el progreso semanal de una secuencia de tareas, a partir de la fecha de implementación.|  
|**Progreso de una secuencia de tareas**|Muestra el progreso de la secuencia de tareas especificada.|  
|**Progreso de todas las secuencias de tareas**|Muestra un resumen del progreso de todas las secuencias de tareas.|  
|**Progreso de las secuencias de tareas para implementaciones de sistemas operativos**|Muestra el progreso de todas las secuencias de tareas que implementan sistemas operativos.|  
|**Estado de todos los equipos desconocidos**|Muestra una lista de los equipos que eran desconocidos en el momento en que ejecutaron una implementación de secuencia de tareas y si ahora son equipos conocidos.|  



## <a name="task-sequences---references"></a>Secuencias de tareas: referencias  

El informe siguiente aparece en la categoría **Secuencia de tareas - Referencias**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Contenido al que hace referencia una secuencia de tareas específica**|Muestra el contenido al que hace referencia una secuencia de tareas especificada.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Usuario: afinidad con el dispositivo  

Los dos informes siguientes aparecen en la categoría **Afinidad entre usuario y dispositivo**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Asociaciones de afinidad de dispositivos de usuario pendientes por recopilación**|Este informe muestra todas las asignaciones de afinidad de dispositivo de usuario pendientes basadas en los datos de uso para los miembros de una recopilación.|  
|**Asociaciones de afinidad de dispositivos de usuario por recopilación**|Muestra todas las asociaciones de dispositivo de usuario de la recopilación especificada y agrupa los resultados por tipo de recopilación (por ejemplo, usuario o dispositivo).|  



## <a name="user-data-and-profiles-health"></a>Mantenimiento de perfiles y datos de usuario  

Los cuatro informes siguientes aparecen en la categoría **Mantenimiento de perfiles y datos de usuario**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Informe de mantenimiento de redirección de carpetas - Detalles**|Muestra los detalles del estado de mantenimiento de la redirección de carpetas para cada una de las carpetas redirigidas para un usuario en concreto.|  
|**Informe de mantenimiento de perfiles de usuario móvil - Detalles**|Muestra los detalles del estado de mantenimiento del perfil de usuario móvil para un usuario especificado.|  
|**Informe de mantenimiento de perfiles y datos de usuario - Detalles**|Muestra los detalles de error o advertencia del redireccionamiento de carpetas o los perfiles de usuario móviles. Este informe es el destino de detalles en el informe de resumen.|  
|**Informe de mantenimiento de perfiles y datos de usuario - Resumen**|Muestra el resumen de los estados de mantenimiento para perfiles de usuario móvil y redirección de carpetas.|  



## <a name="users"></a>Usuarios  

Los tres informes siguientes aparecen en la categoría **Usuarios**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Equipos para un nombre de usuario específico**|Muestra una lista de los equipos usados por un usuario especificado.|  
|**Recuento de usuarios por dominio**|Muestra el número de usuarios en cada dominio.|  
|**Usuarios en un dominio específico**|Muestra una lista de usuarios y sus equipos en un dominio especificado.|  



## <a name="virtual-applications"></a>Aplicaciones virtuales  

Los siete informes siguientes aparecen en la categoría **Aplicaciones virtuales**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Resultados del entorno virtual de App-V**|Muestra información acerca de un entorno virtual especificado que se encuentra en un determinado estado para una recopilación especificada.|  
|**Resultados de entorno virtual de App-V para activo**|Muestra información sobre un entorno virtual especificado para un recurso especificado. También muestra los tipos de implementación para el entorno virtual especificado.|  
|**Estado del entorno virtual de App-V**|Muestra información de cumplimiento de un entorno virtual especificado para una recopilación especificada.|  
|**Equipos con una aplicación virtual específica**|Muestra un resumen de los equipos que tienen el acceso de directo especificado de la aplicación de App-V creado mediante Application Virtualization Management Sequencer.|  
|**Equipos con un paquete de aplicación virtual específico**|Muestra un resumen de los equipos que tienen el paquete de aplicación de App-V especificado.|  
|**Recuento de todas las instancias de paquetes de aplicación virtual**|Muestra un recuento de todos los paquetes de aplicación de App-V detectados.|  
|**Recuento de todas las instancias de aplicaciones virtuales**|Muestra un recuento de las aplicaciones de App-V detectadas.|  



## <a name="vulnerability-assessment"></a>Evaluación de vulnerabilidad

El siguiente informe aparece en la categoría **Evaluación de vulnerabilidad**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Informe general de la evaluación de vulnerabilidad**|Identifica vulnerabilidades de seguridad, administrativas y de cumplimiento de un equipo específico.|  



## <a name="wake-on-lan"></a>Wake On LAN  

Los siete informes siguientes aparecen en la categoría **Wake On LAN**.

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Todos los equipos seleccionados para la actividad Wake On LAN**|Especifique el tipo de implementación para mostrar una lista de los equipos seleccionados para la actividad Wake On LAN.|  
|**Todos los objetos con actividad de reactivación pendiente**|Muestra los objetos que están programados para su reactivación.|  
|**Todos los sitios habilitados para Wake On LAN**|Muestra una lista de todos los sitios de la jerarquía que están habilitados para Wake On LAN.|  
|**Errores recibidos al enviar paquetes de reactivación para un período definido**|Muestra los errores recibidos al enviar paquetes de reactivación a los equipos para un período definido.|  
|**Historial de actividad Wake On LAN**|Muestra un historial de la actividad de reactivación que se produjo desde un período determinado.|  
|**Detalles de estado de implementación de proxy de reactivación**|Muestra información sobre el estado de implementación del proxy de reactivación para cada dispositivo en una recopilación especificada.|  
|**Resumen de estado de implementación de proxy de reactivación**|Muestra un resumen del estado de implementación de un proxy de reactivación en una recopilación especificada.|  
