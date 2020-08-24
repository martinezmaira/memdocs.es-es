---
title: Configurar grupos de límites
titleSuffix: Configuration Manager
description: Ayude a los clientes a encontrar sistemas de sitio mediante grupos de límites para organizar de manera lógica las ubicaciones de red relacionadas denominadas límites.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a925c29b5d186f3ca6f320741f5ca602b0bbb79
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128399"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configuración de grupos de límites para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use los grupos de límites en Configuration Manager para organizar de forma lógica las ubicaciones de red relacionadas ([límites](boundaries.md)) para que sea más fácil administrar la infraestructura. Asigne límites a grupos de límites para poder usar el grupo de límites.

De forma predeterminada, Configuration Manager crea un grupo de límites de sitio de forma predeterminada en cada sitio.

Para configurar grupos de límites, asocie límites (ubicaciones de red) y roles de sistema de sitio, como los puntos de distribución, al grupo de límites. Esta configuración ayuda a asociar clientes a servidores de sistema de sitio como puntos de distribución ubicados cerca de los clientes en la red.

Para aumentar la disponibilidad de los servidores a una variedad más amplia de ubicaciones de red, asigne el mismo límite y el mismo servidor a más de un grupo de límites.

Los clientes usan un grupo de límites para:  

- Asignación automática de sitio  
- Para buscar un servidor de sistema de sitio que puede proporcionar un servicio, que incluya:

  - Puntos de distribución para la ubicación del contenido  
  - Puntos de actualización de software  
  - Puntos de migración de estado  

    > [!NOTE]
    > El punto de migración de estado no usa relaciones de reserva. Para más información, vea [Reserva](#fallback).

  - Puntos de administración preferidos  

    > [!NOTE]  
    > Si usa puntos de administración preferidos, habilite esta opción para la jerarquía y no desde la configuración del grupo de límites. Para más información, vea [Habilitar el uso de puntos de administración preferidos](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Cloud Management Gateway (a partir de la versión 1902)

## <a name="boundary-groups-and-relationships"></a>Grupos de límites y relaciones

Para cada grupo de límites de la jerarquía, puede asignar:

- Uno o varios límites. El grupo de límites **actual** de un cliente es una ubicación de red que se define como un límite asignado a un grupo de límites específico. Un cliente puede tener más de un grupo de límites actual.  

- Uno o varios roles de sistema de sitio. Los clientes siempre pueden usar los roles asociados con su grupo de límites actual. En función de las configuraciones adicionales, pueden usar los roles en grupos de límites adicionales.  

Para cada grupo de límites creados, puede configurar un vínculo de un solo uso a otro grupo de límites. Al vínculo se le denomina **relación**. Los grupos de límites vinculados se denominan grupos de límites **vecinos**. Un grupo de límites puede tener más de una relación, cada una con un grupo de límites vecino específico.

Cuando un cliente no encuentra un sistema de sitio disponible en su grupo de límites actual, la configuración de cada relación determina cuándo empieza a buscar un grupo de límites vecino. Esta búsqueda de grupos adicionales se denomina **reserva**.

Para más información, vea los siguientes procedimientos:  

- [Creación de un grupo de límites](boundary-group-procedures.md#bkmk_create)  
- [Configuración de un grupo de límites](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a> Visualización de los grupos de límites de los dispositivos

<!--6521835-->

A partir de la versión 2002, para ayudarle a identificar mejor y solucionar los problemas de comportamiento de los dispositivos con grupos de límites, puede ver los grupos de límites de dispositivos específicos. En el nodo **Dispositivos**, o cuando se muestran los miembros de una **Colección de dispositivos**, agregue la nueva columna **Grupos de límites** a la vista de lista.

- Si un dispositivo está en más de un grupo de límites, el valor es una lista separada por comas de nombres de grupos de límites.

- Los datos se actualizan cuando el cliente realiza una solicitud de ubicación al sitio o, como máximo, cada 24 horas.

- Si un cliente está en itinerancia y no es miembro de un grupo de límites, el valor está en blanco.

> [!NOTE]
> Esta información consiste en datos del sitio y solo está disponible en los sitios primarios. No verá un valor para esta columna cuando conecte Configuration Manager a un sitio de administración central.

## <a name="fallback"></a>Reserva

Para evitar problemas cuando los clientes no pueden encontrar un sistema de sitio disponible en su grupo de límites actual, se definen relaciones entre los grupos de límites para el comportamiento de reserva. La reserva permite a un cliente expandir la búsqueda a grupos de límites adicionales para encontrar un sistema de sitio disponible.

Las relaciones se configuran en la pestaña **Relaciones** de las propiedades de un grupo de límites. Cuando se configura una relación, se define un vínculo a un grupo de límites vecino. Para cada tipo de rol de sistema de sitio admitido, configure opciones independientes para la reserva en el grupo de límites vecino. Para más información, vea [Configuración del comportamiento de reserva](boundary-group-procedures.md#bkmk_bg-fallback).

Por ejemplo, cuando se configura una relación con un grupo de límites concreto, se puede establecer que la reserva para los puntos de distribución se produzca después de 20 minutos. El tiempo predeterminado es de 120 minutos. Para obtener un ejemplo más extenso, vea [Ejemplo de uso de grupos de límites](#example-of-using-boundary-groups).

Si un cliente no puede encontrar un rol de sistema de sitio disponible en su grupo de límites actual, el cliente usa el tiempo de reserva en minutos. Este tiempo de reserva determina cuándo comienza el cliente a buscar un sistema de sitio disponible asociado con el grupo de límites vecino.  

Cuando un cliente no encuentra un sistema de sitio disponible, empieza a buscar en ubicaciones de los grupos de límites vecinos. Este comportamiento incrementa el grupo de sistemas de sitio disponibles. La configuración de los grupos de límites y sus relaciones define el uso del cliente de este grupo de sistemas de sitio disponibles.

- Un grupo de límites puede tener más de una relación. Con esta configuración, se puede configurar la reserva de cada tipo de sistema de sitio en los distintos vecinos para que se produzca después de otros períodos.  

- Los clientes solo usarán como reserva un grupo de límites que sea vecino directo de su actual grupo de límites.  

- Cuando un cliente es miembro de más de un grupo de límites, define su grupo de límites actual como una unión de todos los grupos de límites. El cliente puede usar como reserva vecinos de cualquiera de esos grupos de límites originales.  

> [!NOTE]
> El rol del punto de migración de estado no usa relaciones de reserva. Si agrega el punto de migración de estado y los roles de punto de distribución al mismo servidor de sistema de sitio, no configure la reserva en el grupo de límites. Si necesita usar la reserva de grupo de límites para el punto de distribución, agregue el rol del punto de migración de estado en un servidor de sistema de sitio diferente.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>El grupo de límites de sitio predeterminado

Puede crear sus propios grupos de límites y cada sitio tiene un grupo de límites de sitio predeterminado creado por Configuration Manager. Este grupo se denomina **Grupo-Límites-Sitio-Predeterminado&lt;códigodesitio>** . Por ejemplo, el grupo del sitio ABC se denominaría **Grupo-Límites-Sitio-Predeterminado&lt;ABC>** .

Para cada grupo de límites creado, Configuration Manager crea automáticamente un vínculo implícito a cada grupo de límites de sitio predeterminado de la jerarquía.  

- El vínculo implícito es una opción de reserva predeterminada de un grupo de límites actual al grupo de límites de sitio predeterminado. Tiene un tiempo de reserva predeterminado de 120 minutos.  

- Para los clientes que no se encuentran en un límite asociado con ningún grupo de límites: para identificar roles de sistema de sitio válidos, use el grupo de límites de sitio predeterminado de su sitio asignado.  

Para administrar la reserva para el grupo de límites de sitio predeterminado:  

- Abra las propiedades del grupo de límites de sitio predeterminado y cambie los valores en la pestaña **Comportamiento predeterminado**. Los cambios que realice aquí se aplican a *todos* vínculos implícitos a este grupo de límites. Cuando configura el vínculo explícito a este grupo de límites de sitio predeterminado desde otro grupo de límites, se invalida esta configuración predeterminada.  

- Abra las propiedades de un grupo de límites personalizado. Cambie los valores del vínculo explícito a un grupo de límites de sitio predeterminado. Cuando se establece un nuevo tiempo en minutos para la reserva o reserva en bloque, ese cambio afecta únicamente al vínculo que se va a configurar. La configuración del vínculo explícito invalida la que se establece en la pestaña **Comportamiento predeterminado** de un grupo de límites de sitio predeterminado.  

## <a name="site-assignment"></a>Asignación de sitio  

Puede configurar cada grupo de límites con un sitio asignado para los clientes.  

- Un cliente recién instalado que usa la asignación automática de sitio se unirá al sitio asignado de un grupo de límites que contiene la ubicación de red actual del cliente.  

- Una vez recibida la asignación a un sitio, el cliente no la modifica al cambiar la ubicación de red. Por ejemplo, un cliente se desplaza a una nueva ubicación de red. Esta ubicación es un límite en un grupo de límites con una asignación de sitio diferente. El sitio asignado del cliente no cambia.  

- Cuando la detección de sistemas de Active Directory detecta un nuevo recurso, el sitio evalúa la información de red para el recurso en relación con los límites en los grupos de límites. Este proceso asocia el nuevo recurso con un sitio asignado para que use el método de instalación de inserción de cliente.  

- Cuando un límite es miembro de más de un grupo de límites que tienen diferentes sitios asignados, los clientes seleccionan uno de los sitios de forma aleatoria.  

- Los cambios que se realicen a un sitio de grupo de límites asignado solo se aplicarán a las nuevas acciones de asignación de sitio. Los clientes previamente asignados a un sitio no vuelven a evaluar su asignación de sitio según los cambios en la configuración de un grupo de límites o en su propia ubicación de red.  

Para más información sobre la asignación de sitio de cliente, vea [Uso de la asignación de sitio automática para los equipos](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Para más información sobre cómo configurar la asignación de sitio, vea los siguientes procedimientos:

- [Configuración de la asignación de sitio y selección de los servidores de sistema de sitio](boundary-group-procedures.md#bkmk_references)
- [Configuración de un sitio de reserva para la asignación de sitios automática](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Puntos de distribución

Cuando un cliente solicita la ubicación de un punto de distribución, Configuration Manager envía al cliente una lista de sistemas de sitio. Estos sistemas de sitio son del tipo adecuado asociado a cada grupo de límites que incluye la ubicación de red actual de los clientes:

- **Durante la distribución de software**, los clientes solicitan una ubicación para el contenido de la implementación en un origen de contenido válido. Esta ubicación puede ser un punto de distribución o un origen de caché del mismo nivel.  

- **Durante la implementación de sistema operativo**, los clientes solicitan una ubicación para enviar o recibir su información de estado de la migración.  

  - Los clientes obtienen el contenido en función de los comportamientos del grupo de límites. Para obtener más información, vea [Task sequence support for boundary groups](#bkmk_bgr-osd) (Compatibilidad de la secuencia de tareas con grupos de límites).  

Durante la implementación de contenido, si un cliente solicita contenido que no está disponible desde un origen de su grupo de límites actual, el cliente continúa con la solicitud de ese contenido. El cliente prueba otros orígenes de contenido en su grupo de límites actual hasta que alcanza el período de reserva para un vecino o el grupo de límites de sitio predeterminado. Si el cliente aún no encuentra contenido, expande la búsqueda de los orígenes de contenido para incluir los grupos de límites vecinos.

Si configura el contenido para distribuir a petición y no está disponible cuando lo solicita un cliente en un punto de distribución, el sitio empieza a transferir el contenido a ese punto de distribución. Es posible que el cliente encuentre ese servidor como un origen de contenido antes de recurrir a un grupo de límites vecino.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a> Instalación de cliente

El instalador del cliente de Configuration Manager, ccmsetup, puede obtener el contenido de instalación desde un origen local o a través de un punto de administración. Su comportamiento inicial depende de los parámetros de la línea de comandos que use para instalar el cliente:<!-- MEMDocs#286 -->

- Si no usa los parámetros **/mp** o **/source**, ccmsetup intenta obtener una lista de puntos de administración de Active Directory o DNS.
- Si solo especifica **/source**, se exige la instalación desde la ruta de acceso especificada. No detecta puntos de administración. Si no puede encontrar ccmsetup.cab en la ruta de acceso especificada, se produce un error en ccmsetup.
- Si especifica tanto **/mp** como **/source**, comprobará los puntos de administración especificados y los detectará. Si no puede encontrar un punto de administración válido, recurre a la ruta de acceso de origen especificada.

Para obtener más información sobre estos parámetros de ccmsetup, vea [Acerca de los parámetros y propiedades de instalación de cliente](../../../clients/deploy/about-client-installation-properties.md).

<!--1358840-->
Cuando ccmsetup entra en contacto con el punto de administración para buscar el contenido necesario, el punto de administración devuelve los puntos de distribución en función de la configuración del grupo de límites. Si define las relaciones que se establecen en el grupo de límites, el punto de administración devuelve los puntos de distribución en el orden siguiente:

1. Grupo de límites actual  
2. Grupos de límites vecinos  
3. Grupo de límites predeterminado del sitio  

> [!Note]  
> El proceso de configuración del cliente no usa el tiempo de retroceso. Para localizar contenido de la forma más rápida posible, retrocede inmediatamente al grupo de límites siguiente.
>
> En versiones anteriores de Configuration Manager, durante este proceso, el punto de administración solo devolvía puntos de distribución en el grupo de límites actual del cliente. Si no había contenido disponible, el proceso de configuración recurría a descargar contenido del punto de administración. No existía la opción de recurrir a puntos de distribución de otros grupos de límites que pudiesen tener el contenido necesario.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a> Compatibilidad de la secuencia de tareas para grupos de límites

<!--1359025-->
Cuando un dispositivo ejecuta una secuencia de tareas y necesita adquirir contenido, usa comportamientos de grupo de límites similares al cliente de Configuration Manager.

Puede configurar este comportamiento mediante la siguiente configuración en la página **Puntos de distribución** de la implementación de la secuencia de tareas:

- **Cuando no haya disponible ningún punto de distribución local, usar un punto de distribución remoto**: para esta implementación, la secuencia de tareas puede revertirse a los puntos de distribución en un grupo de límites próximo.  

- **Permitir que los clientes usen puntos de distribución del grupo de límite del sitio predeterminado**: para esta implementación, la secuencia de tareas puede revertirse a los puntos de distribución en el grupo de límites del sitio predeterminado.  

Para usar este nuevo comportamiento, asegúrese de que los clientes estén actualizados a la versión más reciente.

#### <a name="location-priority"></a>Prioridad de ubicación  

La secuencia de tareas intenta adquirir contenido en el orden siguiente:  

1. Orígenes de caché del mismo nivel  

2. Puntos de distribución en el grupo de límites *actual*  

3. Puntos de distribución en el grupo de límites *vecino*  

    > [!Important]  
    > Dada la naturaleza de tiempo real del procesamiento de la secuencia de tareas, no espera el tiempo de conmutación por error en un grupo de límites vecino, sino que usa los tiempos de conmutación por error para priorizar los grupos de límites vecinos. Por ejemplo, si la secuencia de tareas no puede adquirir contenido desde un punto de distribución de su grupo de límites actual, inmediatamente prueba un punto de distribución de un grupo de límites vecino con el menor tiempo de conmutación por error. Si se produce un error durante el proceso, la conmutación por error se realiza en un punto de distribución de un grupo de límites vecino con un mayor tiempo de conmutación por error.  

4. Puntos de distribución en el grupo de límites *predeterminado del sitio*  

En el archivo de registro **smsts.log** de la secuencia de tareas se muestra la prioridad de los orígenes de ubicación que utiliza en función de las propiedades de implementación.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> Opciones de grupo de límites para descargas del mismo nivel

<!--1356193, 1358749-->
Los grupos de límites incluyen los siguientes valores de configuración adicionales para ofrecer mayor control sobre la distribución de contenido en el entorno:  

- [Permitir descargas del mismo nivel en este grupo de límites](#bkmk_bgoptions1)  

- [Usar solo elementos del mismo nivel dentro de la misma subred durante las descargas del mismo nivel](#bkmk_bgoptions2)  

- [Preferir puntos de distribución sobre elementos del mismo nivel con la misma subred](#bkmk_bgoptions3)  

- [Preferir puntos de distribución de nube sobre puntos de distribución](#bkmk_bgoptions4)  

Para obtener más información sobre cómo configurar estas opciones, vea [Configure a boundary group](boundary-group-procedures.md#bkmk_config) (Configuración de un grupo de límites).

Si un dispositivo está en más de un grupo de límites, se aplican los comportamientos siguientes para esta configuración:

- **Permitir descargas del mismo nivel en este grupo de límites**: si está deshabilitado en un grupo de límites, el cliente no usará la optimización de entrega.
- **Durante las descargas del mismo nivel, use solo elementos del mismo nivel dentro de la misma subred**: si está habilitado en un grupo de límites, este valor surte efecto.
- **Preferir puntos de distribución sobre elementos del mismo nivel dentro de la misma subred**: si está habilitado en un grupo de límites, este valor surte efecto.
- **Preferir los orígenes basados en la nube frente a los orígenes locales**: si está habilitado en un grupo de límites, este valor surte efecto.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a> Permitir descargas del mismo nivel en este grupo de límites

Esta opción está habilitada de forma predeterminada. El punto de administración proporciona a los clientes una lista de ubicaciones de contenido que incluye orígenes del mismo nivel. Este valor afecta también a la aplicación de los identificadores de grupo para la [optimización de entrega](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).  

Hay dos escenarios comunes en que debe considerar la deshabilitación de esta opción:  

- Si tiene un grupo de límites que incluye límites de ubicaciones dispersas geográficamente, como una VPN. Dos clientes pueden estar en el mismo grupo de límites porque se conectan a través de la VPN, pero en ubicaciones muy diferentes que resultan inapropiadas para el uso compartido de contenido del mismo nivel.  

- Si utiliza un único grupo de límites grande para la asignación de sitio, no hace referencia a ningún punto de distribución.  

> [!IMPORTANT]
> Si un dispositivo está en más de un grupo de límites, asegúrese de habilitar esta configuración en todos los grupos de límites para el dispositivo. De lo contrario, el cliente no usará la optimización de entrega. Por ejemplo, no establece la clave del Registro DOGroupID.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a> Durante las descargas del mismo nivel, use solo elementos del mismo nivel dentro de la misma subred

Esta configuración depende de la opción anterior. Si habilita esta opción, el punto de administración solo se incluye en los orígenes del mismo nivel de la lista de ubicaciones de contenido que se encuentran en la misma subred que el cliente.

Escenarios comunes para habilitar esta opción:

- El diseño del grupo de límites para la distribución de contenido incluye un grupo de límites grande que se superpone a otros más pequeños. Con esta nueva configuración, la lista de orígenes de contenido que el punto de administración proporciona a los clientes solo incluye los orígenes del mismo nivel de la misma subred.

- Tiene un único grupo de límites grande para todas las ubicaciones de oficinas remotas. Habilite esta opción, que permite que los clientes solo compartan contenido dentro de la subred en la ubicación de la oficina remota, en lugar de arriesgarse a compartir contenido entre ubicaciones.

A partir de la versión 2002, en función de la configuración de su red, puede excluir ciertas subredes para que no coincidan. Por ejemplo, en el caso de que quiera incluir un límite, pero excluir una subred de VPN específica. De forma predeterminada, Configuration Manager excluye la subred de Teredo (`2001:0000:%`).<!--3555777-->

> [!NOTE]
> En la versión 2002, cuando [expande un sitio primario independiente](../install/prerequisites-for-installing-sites.md#bkmk_expand) para agregar un sitio de administración central (CAS), la lista de exclusión de subredes vuelve al valor predeterminado. Para solucionar este problema, después de la expansión del sitio, ejecute el script de PowerShell para personalizar la lista de exclusión de subredes en el CAS.<!-- 6309068 -->

Importe la lista de exclusión de subredes como una cadena de subredes separadas por comas. Use el carácter de porcentaje (`%`) como carácter comodín. En el servidor de sitio de nivel superior, establezca o lea la propiedad insertada de **SubnetExclusionList** para el componente **SMS_HIERARCHY_MANAGER** de la clase **SMS_SCI_Component**. Para obtener más información, vea [Clase WMI de servidor SMS_SCI_Component](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md).

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Ejemplo de script de PowerShell para actualizar la lista de exclusión de subredes

El script que hay a continuación es un ejemplo de cómo cambiar esta valor. Anexe las subredes a la variable **PropertyValue** después de `2001:0000:%,172.16.16.0`. Es una cadena separada por comas. Ejecute este script en el servidor de sitio de nivel superior de la jerarquía.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> De forma predeterminada, Configuration Manager incluye la subred de Teredo en esta lista. Cuando cambie la lista, primero tiene que leer siempre el valor existente. Anexe las subredes adicionales a la lista y, a continuación, establezca el nuevo valor.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a> Preferir puntos de distribución sobre elementos del mismo nivel con la misma subred

De forma predeterminada, el punto de administración da prioridad a los orígenes de caché del mismo nivel en la parte superior de la lista de ubicaciones de contenido. Esta configuración revierte dicha prioridad para los clientes que están en la misma subred que el origen de caché del mismo nivel.

> [!TIP]
> Este comportamiento se aplica al cliente de Configuration Manager. No se aplica cuando la secuencia de tareas descarga contenido. Cuando se ejecuta la secuencia de tareas, prefiere los orígenes de la caché del mismo nivel a los puntos de distribución.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a> Preferir puntos de distribución de nube sobre puntos de distribución

Si tiene una sucursal con un vínculo de Internet más rápido, ahora puede dar prioridad al contenido de la nube.  

En la versión 1902, esta configuración ahora se denomina **Prefer cloud based sources over on-premise sources** (Preferir los orígenes basados en la nube sobre los orígenes locales). Entre los orígenes basados en la nube se incluyen los siguientes:<!-- SCCMDocs#1529 -->

- Puntos de distribución en la nube
- Microsoft Update (agregado en la versión 1902)

## <a name="software-update-points"></a><a name="bkmk_sup"></a> Puntos de actualización de software 

Los clientes usan grupos de límites para buscar un punto de actualización de software nuevo. Para controlar qué servidores puede buscar un cliente, agregue puntos de actualización de software individuales a otros grupos de límites.

Si agrega todos los puntos de actualización de software existentes al grupo predeterminado de límites del sitio, el cliente selecciona un punto de actualización de software del grupo de servidores disponibles. Este comportamiento es similar a las versiones anteriores de la rama actual de Configuration Manager. Para el comportamiento controlado de selección y reserva, agregue puntos de actualización de software individuales a grupos de límites diferentes.

Si se instala un sitio nuevo, no se agregan puntos de actualización de software al grupo de límites de sitio predeterminado. Asigne los puntos de actualización de software a un grupo de límites para que los clientes pueden buscarlos y usarlos.

### <a name="fallback-for-software-update-points"></a>Reserva de los puntos de actualización de software

La reserva de puntos de actualización de software se configura como otros roles de sistema de sitio, pero tiene las siguientes observaciones:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Los nuevos clientes utilizan grupos de límites para seleccionar puntos de actualización de software.

Si instala nuevos clientes, estos seleccionan un punto de actualización de software de los servidores asociados a los grupos de límites que se configuren. Este comportamiento sustituye al anterior, en el que los clientes seleccionan un punto de actualización de software aleatoriamente de una lista de servidores que comparten el bosque del cliente.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Los clientes seguirán usando el último punto de actualización de software válido conocido hasta que recurran a la reserva para buscar uno nuevo.

Los clientes que ya tienen un punto de actualización de software lo siguen usando hasta que no se puede alcanzar. Este comportamiento incluye el uso continuado de un punto de actualización de software que no está asociado al grupo de límites actual del cliente.

Este comportamiento es intencionado. El cliente continúa con el uso de un punto de actualización de software existente, incluso cuando no se encuentra en el grupo de l´limites actual del cliente. Cuando se cambia el punto de actualización de software, el cliente sincroniza los datos con el nuevo servidor, lo que supone un uso de red significativo. Si todos los clientes cambian a un servidor nuevo al mismo tiempo, el retraso en la transición ayuda a evitar la saturación de la red.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Antes de iniciar la reserva, un cliente siempre trata de acceder al último punto de actualización de software válido conocido durante 120 minutos.

Después de ese tiempo, si el cliente no ha establecido contacto, se inicia la reserva. Cuando se inicia la reserva, el cliente recibe una lista de todos los puntos de actualización de software de su grupo de límites actual. En función de las configuraciones de reserva, hay más puntos de actualización de software disponibles en los grupos de límites vecinos y de sitio predeterminados.

### <a name="fallback-configurations-for-software-update-points"></a>Configuraciones de reserva de los puntos de actualización de software

Puede configurar **Tiempos de reserva (en minutos)** para que los puntos de actualización de software sean inferiores a 120 minutos. Sin embargo, el cliente continúa realizando intentos para alcanzar su punto de actualización de software original durante 120 minutos. Después, amplía su búsqueda a otros servidores. Los tiempos de reserva del grupo de límites se inician la primera vez que el cliente no puede alcanzar su servidor original. Cuando el cliente amplía la búsqueda, el sitio proporciona los grupos de límites configurados para menos de 120 minutos.

Para bloquear la reserva de un punto de actualización de software en un grupo de límites vecino, establezca la opción en **No usar reserva nunca**.

Transcurridas dos horas sin conseguir acceder al servidor original, el cliente utiliza un ciclo más corto para establecer conexión con un nuevo punto de actualización de software. Este comportamiento permite al cliente buscar de forma rápida por la lista expandida de posibles puntos de actualización de software.

#### <a name="example"></a>Ejemplo

Configure los puntos de actualización de software en el grupo de límites *A* para usarlos como reserva después de **10** minutos. Establezca la misma configuración para el grupo de límites *B* en **130** minutos. Un cliente del grupo de límites *Z* no logra alcanzar su último punto de actualización de software válido conocido.

- Durante los próximos 120 minutos, el cliente intenta alcanzar solo su servidor original en el grupo de límites Z. Después de 10 minutos, Configuration Manager agrega los puntos de actualización de software del grupo de límites A al grupo de servidores disponibles. Sin embargo, el cliente no intenta ponerse en contacto con ellos o cualquier otro servidor hasta que transcurre el período inicial de 120 minutos.  

- Después de intentar ponerse en contacto con el punto de actualización de software original durante 120 minutos, el cliente amplía su búsqueda. Agrega servidores al grupo disponible de puntos de actualización de software del grupo de límites actual del cliente y todos los grupos de límites vecinos configurados para 120 minutos o menos. Este grupo incluye los servidores del grupo de límites A que se agregaron anteriormente al grupo de servidores disponibles.  

- Una vez transcurridos más de 10 minutos, el cliente amplía la búsqueda para incluir los puntos de actualización de software del grupo de límites B. Este período es un tiempo total de 130 minutos después de que el cliente tenga problemas para acceder por primera vez a su último punto de actualización de software válido conocido.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Cambio manual a un nuevo punto de actualización de software

Junto con la reserva, use la notificación de cliente para forzar manualmente a que un dispositivo cambie a un nuevo punto de actualización de software.

Cuando se cambia a un nuevo servidor, los dispositivos utilizan la reserva para buscar ese servidor nuevo. Los clientes cambian al nuevo punto de actualización de software durante su siguiente ciclo de detecciones de actualizaciones de software.<!-- SCCMDocs#1537 -->

Revise las configuraciones de los grupos de límites. Antes de iniciar este cambio, asegúrese de que los puntos de actualización de software se encuentran en los grupos de límites correctos.

Para obtener más información, consulte [Cambio manual de clientes a un nuevo punto de actualización de software](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a><a name="bkmk_cmg-sup"></a> Los clientes de la intranet pueden usar un punto de actualización de software de CMG
<!--7102873-->
A partir de la versión 2006, los clientes de la intranet pueden acceder a un punto de actualización de software de CMG cuando se asigna a un grupo de límites y la opción [**Permitir tráfico de Cloud Management Gateway en Configuration Manager** está habilitada](../../../clients/manage/cmg/setup-cloud-management-gateway.md#bkmk_role) en el punto de actualización de software. Puede permitir que los dispositivos de la intranet examinen con un punto de actualización de software de CMG en los siguientes escenarios:

- Cuando un equipo de Internet se conecta a la VPN, seguirá examinando con el punto de actualización de software CMG a través de Internet.
- Si el único punto de actualización de software para el grupo de límites es el punto de actualización de software de CMG, todos los dispositivos de la intranet y de Internet explorarán con él.

## <a name="management-points"></a>Puntos de administración

<!-- 1324594 -->
Configure las relaciones de reserva para los puntos de administración entre grupos de límites. Este comportamiento proporciona mayor control para los puntos de administración que utilizan los clientes. En la pestaña **Relaciones** de las propiedades del grupo de límites, hay una columna para el punto de administración. Cuando se agrega un nuevo grupo de límites de reserva, el tiempo de reserva para el punto de administración actualmente siempre es cero (0). Este comportamiento es el mismo para el **comportamiento predeterminado** en el grupo de límites predeterminado del sitio.

Anteriormente, solía producirse un problema cuando se tenía un punto de administración protegido en una red segura. Los clientes de la red principal recibían una directiva que incluía este punto de administración protegido, incluso aunque no se podían comunicar con él a través de un firewall. Para solucionar este problema, use la opción **No usar reserva nunca** para asegurarse de que los clientes solo reservan para los puntos de administración con los que pueden comunicarse.

> [!Note]  
> Si habilita puntos de distribución en el grupo de límites predeterminado del sitio para la reserva, y un punto de administración se coloca en un punto de distribución, el sitio también agrega dicho punto de administración al grupo de límites predeterminado del sitio.<!--VSO 2841292-->  

Si un cliente está en un grupo de límites sin ningún punto de administración asignado, el sitio proporciona al cliente la lista completa de puntos de administración. Este comportamiento garantiza que un cliente siempre reciba una lista de puntos de administración.

La reserva del grupo de límites del punto de administración no cambia el comportamiento durante la instalación de cliente (ccmsetup.exe). Si la línea de comandos no especifica el punto de administración inicial mediante el parámetro /MP, el cliente nuevo recibe la lista completa de puntos de administración disponibles. Para su proceso de arranque inicial, el cliente utiliza el primer punto de administración al que pueda tener acceso. Una vez que el cliente se registre en el sitio, recibirá la lista de puntos de administración ordenada correctamente de acuerdo con este nuevo comportamiento.

Para obtener más información sobre el comportamiento del cliente para adquirir contenido durante la instalación, vea [Client installation](#bkmk_ccmsetup) (Instalación del cliente).

Durante la actualización de cliente, si no se especifica el parámetro de línea de comandos /MP, el cliente consulta orígenes, como Active Directory y WMI, para conocer cualquier punto de administración disponible. La actualización de cliente no acepta la configuración del grupo de límites. <!--VSO 2841292-->  

Para los clientes que usen esta función, habilite la siguiente opción: **Los clientes prefieren usar puntos de administración especificados en grupos de límites** en **Configuración de jerarquía**.

> [!Note]  
> Los procesos de implementación de sistema operativo no operan de acuerdo con los grupos de límites para los puntos de administración.  

### <a name="troubleshooting"></a>Solución de problemas

Las nuevas entradas aparecen en **LocationServices.log**. El atributo **Localidad** identifica uno de los siguientes estados:

- **0**: Unknown  

- **1**: el punto de administración especificado solo está en el grupo de límites predeterminado del sitio para la reserva.  

- **2**: el punto de administración especificado está en un grupo de límites remoto o vecino. Cuando el punto de administración está simultáneamente en un grupo vecino y en un grupo de límites predeterminado del sitio, la localidad es 2.  

- **3**: el punto de administración especificado está en el grupo de límites local o actual. Cuando el punto de administración está en el grupo de límites actual y en un grupo vecino o de límites predeterminado del sitio, la localidad es 3. Si no habilita la configuración de los puntos de administración preferidos en la configuración de jerarquía, la localidad siempre es 3, con independencia de en qué grupo de límites se encuentre el punto de administración.  

Los clientes utilizan puntos de administración locales primero (localidad 3), luego remotos (localidad 2) y por último reserva (localidad 1).

Cuando un cliente recibe cinco errores en 10 minutos y no puede comunicarse con un punto de administración de su grupo de límites actual, trata de contactar con un punto de administración en un grupo vecino o el grupo de límites predeterminado del sitio. Si el punto de administración del grupo de límites actual más adelante vuelve a estar conectado, el cliente volverá al punto de administración local en el siguiente ciclo de actualización. El ciclo de actualización es de 24 horas, o cuando se reinicia el servicio del agente de Configuration Manager.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a> Puntos de administración preferidos

> [!Note]
> El comportamiento de esta configuración de jerarquía (**Los clientes prefieren usar puntos de administración especificados en grupos de límites**) ha cambiado en la versión 1802. Si habilita esta opción, Configuration Manager usa la funcionalidad de grupo de límites para el punto de administración asignado. Para obtener más información, vea [Puntos de administración](#management-points).

Los puntos de administración preferidos permiten que un cliente identifique un punto de administración asociado con su ubicación de red (límite) actual.  

- Un cliente intenta usar un punto de administración preferido de su sitio asignado antes de usar otro que no está configurado como el preferido.  

- Para usar esta opción, habilite **Los clientes prefieren usar puntos de administración especificados en grupos de límites** en **Configuración de jerarquía**. Después, configure los grupos de límites en sitios primarios individuales. Incluya los puntos de administración que se deben asociar con los límites asociados de ese grupo de límites. Para más información, vea [Habilitar el uso de puntos de administración preferidos](boundary-group-procedures.md#bkmk_proc-prefer).  

- Al configurar puntos de administración preferidos, y cuando un cliente organiza su lista de puntos de administración, el cliente coloca los puntos de administración preferidos en la parte superior de la lista. En esta lista se incluyen todos los puntos de administración del sitio asignado del cliente.  

> [!NOTE]  
> La movilidad del cliente significa que cambia sus ubicaciones de red. Por ejemplo, cuando un equipo portátil viaja a una ubicación de oficina remota. Cuando un cliente se desplaza, es posible que use un punto de administración del sitio local antes de intentar usar un servidor de su sitio asignado. En esta lista de servidores de su sitio asignado se incluyen los puntos de administración preferidos. Para obtener más información, vea [Más información sobre cómo los clientes buscan servicios y recursos de sitio](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Superposición de los límites  

Configuration Manager admite configuraciones de límites que se superponen para la ubicación del contenido. Cuando la ubicación de red del cliente pertenece a más de un grupo de límites:

- Cuando un cliente solicita contenido, Configuration Manager envía al cliente una lista de todos los puntos de distribución que lo tienen.  

- Cuando un cliente solicita a un servidor que envíe o reciba información de migración de su estado, Configuration Manager envía al cliente una lista de todos los puntos de migración de estado asociados a un grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que se va a transferir el contenido o información de migración de estado.  

## <a name="example-of-using-boundary-groups"></a>Ejemplo de uso de grupos de límites

En el ejemplo siguiente se usa un cliente que busca contenido desde un punto de distribución. Este ejemplo se puede aplicar a otros roles de sistema de sitio que utilizan grupos de límites.

Cree tres grupos de límites que no compartan los límites ni los servidores de sistema de sitio:  

- Grupo BG_A con puntos de distribución DP_A1 y DP_A2  

- Grupo BG_B con puntos de distribución DP_B1 y DP_B2  

- Grupo BG_C con puntos de distribución DP_C1 y DP_C2  

Agregue las ubicaciones de red de los clientes como límites solo al grupo de límites BG_A. Después, configure las relaciones de ese grupo de límites a los otros dos:  

- Configure los puntos de distribución para usar el primer grupo *vecino* (BG_B) después de 10 minutos. Este grupo contiene los puntos de distribución DP_B1 y DP_B2. Ambos están bien conectados a las primeras ubicaciones de límite de grupos.  

- Configure el segundo grupo *vecino* (BG_C) para usarse después de 20 minutos. Este grupo contiene los puntos de distribución DP_C1 y DP_C2. Ambos están separados por WAN de los otros dos grupos de límites.  

- Agregue también al grupo de límites de sitio predeterminado otro punto de distribución que se encuentre en el servidor de sitio. Este servidor se encuentra en la ubicación de origen de contenido menos preferida, pero tiene una ubicación central con respecto a todos los grupos de límites.

    Ejemplo de grupos de límites y tiempos de reserva:

    ![Ejemplo de grupos de límites y tiempos de reserva](media/BG_Fallback.png)  

Con esta configuración:  

- El cliente comienza a buscar contenido de los puntos de distribución en su grupo de límites *actual* (BG_A). Busca durante dos minutos en cada punto de distribución y, después, cambia al siguiente punto de distribución del grupo de límites. El grupo de ubicaciones de origen de contenido válidas del cliente incluye DP_A1 y DP_A2.  

- Si el cliente no puede encontrar contenido en su grupo de límites *actual* después de buscar durante 10 minutos, agrega los puntos de distribución del grupo de límites BG_B a su búsqueda. Después, continúa la búsqueda de contenido de un punto de distribución en su grupo combinado de servidores. En este grupo ahora se incluyen los servidores de los grupos de límites BG_A y BG_B. El cliente sigue poniéndose en contacto con cada punto de distribución durante dos minutos y después cambia al servidor siguiente de su grupo. El grupo de ubicaciones de origen de contenido válidas del cliente incluye DP_A1, DP_A2, DP_B1 y DP_B2.  

- Después de otros 10 minutos (un total de 20), si el cliente todavía no ha encontrado un punto de distribución con contenido, amplía su grupo para incluir los servidores disponibles del segundo grupo de límites *vecino*, BG_C. El cliente ahora tiene seis puntos de distribución donde buscar: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 y DP_C2. Continúa cambiando a un punto de distribución nuevo cada dos minutos hasta que encuentra el contenido.  

- Si el cliente no ha encontrado contenido después de un total de 120 minutos, usa la reserva para incluir el *grupo de límites de sitio predeterminado* como parte de su búsqueda continuada. Ahora el grupo incluye todos los puntos de distribución de los tres grupos de límites configurados y el punto de distribución final ubicado en el servidor de sitio. El cliente sigue buscando contenido, cambiando de punto de distribución cada dos minutos hasta que encuentra contenido.  

Mediante la configuración de otros grupos vecinos como disponibles en momentos diferentes, se puede controlar cuándo se agregan puntos de distribución específicos como una ubicación de origen de contenido. El cliente usa la reserva para el grupo de límites de sitio predeterminado como una red de seguridad para el contenido que no está disponible desde ninguna otra ubicación.

## <a name="changes-from-prior-versions"></a>Cambios con respecto a las versiones anteriores

Estos son los cambios principales en los grupos de límites y en la forma en que los clientes buscan contenido en la rama actual de Configuration Manager. Muchos de estos conceptos y cambios funcionan conjuntamente.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Se quitan las configuraciones de Rápido o Lento

Ya no se configuran los puntos de distribución individuales para que sean rápidos o lentos. En su lugar, se trata igual cada sistema de sitio asociado a un grupo de límites. Debido a este cambio, la pestaña **Referencias** de las propiedades del grupo de límites ya no admite la configuración de Rápido o Lento.  

### <a name="new-default-boundary-group-at-each-site"></a>Nuevo grupo de límites predeterminado en cada sitio

Cada sitio primario tiene un nuevo grupo de límites predeterminado denominado **Default-Site-Boundary-Group&lt;sitecode>** . Cuando un cliente no está en una ubicación de red asignada a un grupo de límites, usa los sistemas de sitio asociados con el grupo predeterminado de su sitio asignado. Este grupo de límites se puede considerar un sustituto del concepto de ubicación de contenido de reserva.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Permitir a los clientes usar una ubicación de origen de reserva para el contenido** se ha quitado

Ya no se configuran puntos de distribución de forma explícita para usarse como reserva. Las opciones para configurar esta opción se han quitado de la consola.

Además, el resultado de establecer **Permitir a los clientes usar una ubicación de origen de reserva para el contenido** en un tipo de implementación para aplicaciones ha cambiado. Esta opción en un tipo de implementación ahora permite a un cliente usar el grupo de límites de sitio predeterminado como una ubicación de origen de contenido.

#### <a name="boundary-groups-relationships"></a>Relaciones de grupos de límites

Cada grupo de límites se puede vincular a uno o varios grupos de límites adicionales. Estos vínculos forman relaciones que se configuran en la nueva pestaña de propiedades de grupos de límites denominada **Relaciones**:  

- Cada grupo de límites asociado directamente a un cliente se denomina grupo de límites **actual**.  

- Cualquier grupo de límites que un cliente pueda usar debido a una asociación entre el grupo de límites *actual* de cliente y otro grupo se denomina grupo de límites **vecino**.  

- Es en la pestaña **Relaciones**, agregue los grupos de límites que se van a usar como grupos de límites *vecinos*. Configure también un tiempo en minutos para la reserva. Cuando un cliente no puede encontrar contenido de un punto de distribución del grupo *actual*, este es el tiempo cuando empieza a buscar ubicaciones de contenido de los grupos de límites *vecinos*.  

    Al agregar o cambiar la configuración de un grupo de límites, puede bloquear la reserva de ese grupo de límites concreto desde el grupo actual que está configurando.  

Para usar la nueva configuración, defina asociaciones explícitas (vínculos) de un grupo de límites a otro. Configure todos los puntos de distribución de ese grupo asociado con el mismo tiempo en minutos. Cuando un cliente no encuentra un origen de contenido de su grupo de límites *actual*, el tiempo que se configure determina cuándo empieza a buscar orígenes de contenido en su grupo de límites vecino.

Además de los grupos de límites que se configuran explícitamente, cada grupo de límites tiene un vínculo implícito al grupo de límites de sitio predeterminado. Este vínculo se activa después de 120 minutos. Luego, el grupo de límites de sitio predeterminado se convierte en un grupo de límites vecino. Este comportamiento permite a los clientes usar como ubicaciones de origen de contenido los puntos de distribución asociados a ese grupo de límites.

Este comportamiento reemplaza a lo que anteriormente se conocía como reserva de contenido. Para invalidar este comportamiento predeterminado de 120 minutos, asocie de forma explícita el grupo de límites de sitio predeterminado a un grupo *actual*. Establezca un tiempo específico en minutos, o bien bloquee completamente la reserva para impedir su uso.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Los clientes intentan obtener contenido de cada punto de distribución hasta un máximo de dos minutos

Cuando un cliente busca una ubicación de origen de contenido, intenta acceder a cada punto de distribución durante dos minutos antes de intentarlo con otro punto de distribución. Este comportamiento supone un cambio con respecto a las versiones anteriores, donde los clientes intentaban conectarse a un punto de distribución hasta un máximo de dos horas.

- El cliente selecciona aleatoriamente el primer punto de distribución del grupo de servidores disponibles del grupo (o grupos) de límites *actual* del cliente.  

- Después de dos minutos, si el cliente no ha encontrado el contenido, cambia a un nuevo punto de distribución e intenta obtener contenido de ese servidor. Este proceso se repite cada dos minutos hasta que el cliente encuentra el contenido o alcanza el último servidor de su grupo.  

- Si un cliente no puede encontrar una ubicación de origen de contenido válida de su grupo *actual* antes de que se alcance el periodo de reserva para un grupo de límites *vecino*, el cliente agrega los puntos de distribución de ese grupo *vecino* al final de su lista actual. Después, busca en el grupo ampliado de ubicaciones de origen en el que se incluyen los puntos de distribución de ambos grupos de límites.  

    > [!TIP]  
    > Al crear un vínculo explícito entre el grupo de límites actual y el grupo de límites de sitio predeterminado, y definir un tiempo de reserva menor que el tiempo de reserva de un vínculo a un grupo de límites vecino, los clientes empiezan a buscar en las ubicaciones de origen del grupo de límites de sitio predeterminado antes de incluir el grupo vecino.  

- Cuando el cliente no puede obtener contenido del último servidor del grupo, el proceso comienza de nuevo.  

## <a name="see-also"></a>Vea también

- [Procedimientos de los grupos de límites](boundary-group-procedures.md)  

- [Sobre los límites](boundaries.md)  

- [Conceptos básicos de la administración de contenido](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
