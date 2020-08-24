---
title: Definición de límites
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo definir ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700068"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definición de las ubicaciones de red como límites para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los límites de Configuration Manager son ubicaciones de red que contienen dispositivos que desea administrar. Puede crear diferentes tipos de límites, por ejemplo, un sitio de Active Directory o una dirección IP de red. Cuando el cliente de Configuration Manager identifica una ubicación de red similar, ese dispositivo forma parte del límite.

Configuration Manager admite los siguientes tipos de límites:

- Subred IP
- Sitio de Active Directory
- Prefijo IPv6
- Intervalo de direcciones IP
- VPN (a partir de la versión 2006)

Puede crear límites individuales manualmente o usar la [detección de bosques de Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest). Este método de detección busca y crea automáticamente límites para las subredes IP y los sitios de Active Directory. Cuando la detección de bosques de Active Directory identifica una superred para un sitio de Active Directory, Configuration Manager convierte la superred en un límite de intervalo de direcciones IP.

Si un dispositivo no se encuentra dentro del límite esperado, puede que no se haya definido su ubicación de red como un límite. Cuando la ubicación de red de un dispositivo está en duda, use los siguientes comandos de Windows en el dispositivo para confirmar:

- Dirección IP: `ipconfig`
- Sitio de Active Directory: `nltest /dsgetsite`
- VPN: `ipconfig /all`

## <a name="boundary-types"></a>Tipos de límites

### <a name="ip-subnet"></a>Subred IP

El tipo de límite de subred IP requiere un **Id. de subred**. Por ejemplo: `169.254.0.0`. Si proporciona los valores **Red** (puerta de enlace predeterminada) y **Máscara de subred**, Configuration Manager calcula automáticamente el **Id. de subred**. Al guardar el límite, Configuration Manager solo guarda el valor del identificador de subred.

> [!NOTE]
> Configuration Manager no es compatible con la entrada directa de una superred como un límite. En su lugar, utilice el tipo de límite de intervalo de direcciones IP.

### <a name="active-directory-site"></a>Sitio de Active Directory

En el caso del tipo de límite **Sitio de Active Directory**, especifique el nombre del sitio. Puede escribir el nombre o examinar el bosque local del servidor de sitio.

Cuando se especifica un sitio de Active Directory para un límite, el límite incluye cada subred IP que sea miembro de ese sitio de Active Directory. Si cambia la configuración del sitio de Active Directory en Active Directory, también cambiarán las ubicaciones de red incluidas en este límite.  

Los límites de sitio de Active Directory no funcionan para los dispositivos puros de Azure Active Directory (Azure AD), también denominados dispositivos unidos a un dominio en la nube. Si se desplazan en el entorno local y solo se crean límites de tipo de sitio de Active Directory, estos dispositivos no estarán dentro de un límite.

> [!TIP]
> Use el siguiente comando de Windows para ver el sitio de Active Directory actual de un dispositivo: `nltest /dsgetsite`.
>
> Para determinar si un cliente está unido a un dominio en la nube, use el siguiente comando de Windows: `dsregcmd /status`. Para más información, consulte el [comando dsregcmd: estado del dispositivo](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### <a name="ipv6-prefix"></a>Prefijo IPv6

Para el tipo de límite **Prefijo IPv6**, especifique un **prefijo**. Por ejemplo: `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>Intervalo de direcciones IP

Para el tipo de límite **Intervalo de direcciones IP**, especifique **Dirección IP inicial** y **Dirección IP final** para el intervalo. El intervalo puede incluir parte de una subred IP o varias subredes IP. Use un tipo de límite de intervalo de direcciones IP para admitir una superred.

También puede usar este tipo para definir un límite para una única dirección IP. Establezca las direcciones IP inicial y final como el mismo valor. Esta configuración puede ser útil para dispositivos únicos o entornos de prueba.

### <a name="vpn"></a>VPN

<!--7020519-->

A partir de la versión 2006, para simplificar la administración de clientes remotos, cree un tipo de límite para las VPN. Cuando un cliente envía una solicitud de ubicación, incluye información adicional sobre su configuración de red. En función de esta información, el servidor determina si el cliente se encuentra en una VPN. Para que Configuration Manager asocie al cliente en el límite, conecte el dispositivo a la VPN.

Puede configurar un límite de VPN de varias maneras:

- **Detectar VPN automáticamente**: Configuration Manager detecta cualquier solución VPN que use el protocolo de túnel punto a punto (PPTP). Si no detecta la VPN, use una de las otras opciones. El valor del límite de la lista de la consola será `Auto:On`.

- **Nombre de la conexión**: especifique el nombre de la conexión VPN en el dispositivo. Es el nombre del adaptador de red de Windows para la conexión VPN. Configuration Manager coincide con los primeros 250 caracteres de la cadena, pero no admite caracteres comodín ni cadenas parciales. El valor de límite de la lista de la consola será `Name:<name>`, donde `<name>` es el nombre de conexión que especifique.

  Por ejemplo, ejecute el comando `ipconfig` en el dispositivo y una de las secciones comenzará por `PPP adapter ContosoVPN:`. Use la cadena `ContosoVPN` como **nombre de la conexión**. Se muestra en la lista como `Name:CONTOSOVPN`.

- **Descripción de la conexión**: especifique la descripción de la conexión VPN. Configuration Manager coincide con los primeros 243 caracteres de la cadena, pero no admite caracteres comodín ni cadenas parciales. El valor de límite de la lista de la consola será `Description:<description>`, donde `<description>` es la descripción de conexión que especifique.

  Por ejemplo, ejecuta el comando `ipconfig /all` en el dispositivo y una de las conexiones incluye la línea siguiente: `Description . . . . . . . . . . . : ContosoMainVPN`. Use la cadena `ContosoMainVPN` como **descripción de la conexión**. Se muestra en la lista como `Description:CONTOSOMAINVPN`.

> [!IMPORTANT]
> Para aprovechar al máximo esta característica, después de actualizar el sitio, actualice también los clientes a la versión más reciente. La nueva funcionalidad aparece en la consola de Configuration Manager al actualizar el sitio y la consola. Este escenario no funciona completamente hasta que la versión del cliente es también la más reciente.
>
> Para usar este límite de VPN durante una implementación del sistema operativo, asegúrese de actualizar también la imagen de arranque para incluir los archivos binarios de cliente más recientes.

## <a name="create-a-boundary"></a>Creación de un límite

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Límites**.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear límite**.

1. En la pestaña **General** de la ventana **Crear límite**, especifique la información siguiente:

    - **Descripción**: Identifique el límite mediante un nombre descriptivo o una referencia.

        > [!NOTE]
        > Configuration Manager nombra automáticamente el límite en función de su tipo y ámbito. No se puede modificar el nombre.

    - **Tipo**: seleccione el tipo de filtro para crear. Después, especifique la información adicional que requiere el tipo. Para más información, vea [Tipos de límites](#boundary-types).

1. Cambie a la pestaña **Grupos de límites**. Si ya tiene grupos de límites en el sitio, puede agregar inmediatamente este nuevo límite a uno o varios grupos.

1. Seleccione **Aceptar** para guardar el nuevo límite.

## <a name="configure-a-boundary"></a>Configuración de un límite

> [!TIP]
> Al crear un límite, Configuration Manager le asigna un nombre automáticamente en función del tipo y ámbito del límite. No se puede modificar este nombre. Especifique una descripción que ayude a identificar el límite en la consola de Configuration Manager.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Límites**.

1. Seleccione el límite que desea modificar. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.

1. En la pestaña **General** de la ventana **Propiedades** del límite, puede configurar las siguientes opciones:

    - Editar la **Descripción**.
    - Cambiar el **Tipo** de límite.
    - Cambiar el ámbito de un límite mediante la edición de sus ubicaciones de red. Por ejemplo, para un límite de sitio de Active Directory, puede especificar un nuevo nombre de sitio de Active Directory.

1. Para ver los sistemas de sitio asociados con este límite, cambie a la pestaña **Sistemas de sitio**. No puede cambiar esta configuración desde las propiedades de un límite.

    > [!TIP]
    > Para que un servidor se muestre como sistema de sitio para un límite, asócielo como un servidor de sistema de sitio para, al menos, un grupo de límites que incluya este límite. Realice esta configuración en la pestaña **Referencias** de un grupo de límites. Para más información, vea [Configuración de la asignación de sitio y selección de los servidores de sistema de sitio](boundary-group-procedures.md#bkmk_references).

1. Para modificar la pertenencia al grupo de límites de este límite, seleccione la pestaña **Grupos de límites**:

    - Para agregar este límite a uno o varios grupos de límites, seleccione **Agregar**. Seleccione uno o varios grupos de límites y, después, seleccione **Aceptar**.

    - Para quitar este límite de un grupo de límites, elija el grupo de límites y, después, seleccione **Quitar**.

1. Seleccione **Aceptar** para cerrar las propiedades del límite y guardar la configuración.

## <a name="next-steps"></a>Pasos siguientes

Cada límite está disponible para que lo use cada sitio de la jerarquía. Después de crear un límite, agréguelo a uno o varios [grupos de límites](boundary-groups.md).