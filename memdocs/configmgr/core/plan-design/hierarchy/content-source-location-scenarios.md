---
title: Ubicación de origen de contenido
titleSuffix: Configuration Manager
description: Conozca la configuración de Configuration Manager que permite a los clientes buscar contenido en una red lenta.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703663"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Escenarios de ubicación de orígenes de contenido en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de la versión 1610, Configuration Manager admitía varias opciones que se combinaban para definir cómo y dónde encuentran contenido los clientes cuando están en una red lenta. Las combinaciones posibles afectan a la ubicación de contenido que usan los clientes y a la posibilidad de usar correctamente una ubicación de reserva cuando no está disponible un origen de contenido preferido.  

> [!IMPORTANT]  
> **Si los sitios ejecutan las versiones 1511, 1602 o 1606**, la información de este tema se aplica a la infraestructura. Vea también [Boundary groups for versions 1511,1602, and 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) (Grupos de límites para las versiones 1511, 1602 y 1606) para obtener información específica sobre los grupos de límites con estas versiones de Configuration Manager.
>
> **Si los sitios ejecutan la versión 1610 o posterior**, use la información incluida en [Definir los límites del sitio y los grupos de límites para Configuration Manager](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) para comprender la forma en que los clientes encuentran puntos de distribución con contenido disponible.





**Las siguientes tres opciones definen el comportamiento cuando los clientes solicitan contenido:**

- **Permitir ubicación de origen de reserva para contenido** (habilitado o no habilitado): se trata de una opción que se puede habilitar en la pestaña **Grupos de límites** de un punto de distribución. Esto permite al cliente usar un punto de distribución configurado como ubicación de reserva cuando el contenido no está disponible en un punto de distribución preferido.  

  - **Comportamiento de implementación de la velocidad de conexión de red**: cada implementación se configura con uno de los siguientes comportamientos que se usarán cuando la conexión al punto de distribución es lenta:  

    -   **Descargar contenido desde el punto de distribución y ejecutar localmente**  

    -   **No descargar contenido**: esta opción solo se usa cuando un cliente emplea una ubicación de reserva para obtener contenido.  

    La velocidad de conexión para un punto de distribución está configurada en la pestaña **Referencias** del grupo de límites y es específica de ese grupo de límites.  

  - **Distribución de paquetes a petición** (a los puntos de distribución preferidos): esta opción está habilitada cuando se selecciona la opción **Distribuir el contenido de este paquete en puntos de distribución preferidos** en la pestaña **Configuración de distribución** de las propiedades de un paquete o de una aplicación. Cuando se habilita, esta opción indica a Configuration Manager que copie automáticamente el contenido a un punto de distribución preferido que aún no tiene el contenido después de que un cliente solicita ese contenido desde ese punto de distribución.  


 **Los siguientes requisitos se aplican a todos los escenarios:**


-   El contenido está disponible en un punto de distribución de reserva.  

-   Los puntos de distribución están en línea y se puede acceder a ellos.  


## <a name="scenario-1"></a>Escenario 1  
 Se aplica con la siguiente configuración:  

-   **El contenido está disponible en un punto de distribución preferido**  

-   **Permitir reserva**: no habilitado.  

-   **Comportamiento de implementación para red lenta**: Cualquier configuración.  


**Detalles:** (la configuración para distribución de paquetes a petición no es relevante en este escenario).  

1.  El cliente envía una solicitud de contenido al punto de administración.  

2.  El punto de administración devuelve al cliente una lista de ubicación del contenido con los puntos de distribución preferidos que tienen ese contenido.  

3.  El cliente descarga el contenido desde un punto de distribución preferido de la lista.  

## <a name="scenario-2"></a>Escenario 2  
 Con la configuración siguiente:  

-   **El contenido está disponible en un punto de distribución preferido**  

-   **Permitir reserva**: Habilitado  

-   **Comportamiento de implementación para red lenta**: no descargar contenido.  


**Detalles:** (la configuración para distribución de paquetes a petición no es relevante en este escenario).  

1.  El cliente envía una solicitud de contenido al punto de administración. El cliente incluye una marca con la solicitud que indica que se permiten puntos de distribución de reserva.  

2.  El punto de administración devuelve al cliente una lista de ubicación del contenido con los puntos de distribución preferidos y los puntos de distribución de reserva que tienen ese contenido.  

3.  El cliente descarga el contenido desde un punto de distribución preferido de la lista.  

## <a name="scenario-3"></a>Escenario 3  
 Con la configuración siguiente:  

-   **El contenido está disponible en un punto de distribución preferido**  

-   **Permitir reserva**: Habilitado  

-   **Comportamiento de implementación para red lenta**: descargar e instalar contenido.  


**Detalles:** (la configuración para distribución de paquetes a petición no es relevante en este escenario).  

1.  El cliente envía una solicitud de contenido al punto de administración. El cliente incluye una marca con la solicitud que indica que se permiten puntos de distribución de reserva.  

2.  El punto de administración devuelve al cliente una lista de ubicación del contenido con los puntos de distribución preferidos y los puntos de distribución de reserva que tienen ese contenido.  

3.  El cliente descarga el contenido desde un punto de distribución preferido de la lista.  

## <a name="scenario-4"></a>Escenario 4  
 Con la configuración siguiente:  

-   **El contenido no está disponible en un punto de distribución preferido**  

-   **Distribuir el contenido de este paquete en puntos de distribución preferidos** no está habilitado  

-   **Permitir reserva**: no habilitado.  

-   **Comportamiento de implementación para red lenta**: Cualquier configuración.  


**Detalles:**  

1.  El cliente envía una solicitud de contenido al punto de administración.  

2.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos que tienen el contenido. No hay ningún punto de distribución preferido en la lista.  

3.  Se produce un error en el cliente con el mensaje **El contenido no está disponible** y entra en modo de reintento. Cada hora, se inicia una nueva solicitud de contenido.  

## <a name="scenario-5"></a>Escenario 5  
 Con la configuración siguiente:  

-   **El contenido no está disponible en un punto de distribución preferido**  

-   **Distribuir el contenido de este paquete en puntos de distribución preferidos** no está habilitado  

-   **Permitir reserva**: Habilitado  

-   **Comportamiento de implementación para red lenta**: no descargar contenido.  


**Detalles:**  

1.  El cliente envía una solicitud de contenido al punto de administración. El cliente incluye una marca con la solicitud que indica que se permiten puntos de distribución de reserva.  

2.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos y los puntos de distribución de reserva que tienen el contenido. No hay puntos de distribución preferidos que tienen el contenido, pero al menos un punto de distribución de reserva tiene el contenido.  

3.  No se descarga el contenido porque la propiedad de implementación para cuando el cliente usa un punto de distribución de reserva está establecida en **No descargar contenido** (que se usa cuando los clientes permiten la reserva para obtener el contenido). Se produce un error en el cliente con el mensaje **El contenido no está disponible** y entra en modo de reintento. El cliente realiza una solicitud de contenido nueva cada hora.  

## <a name="scenario-6"></a>Escenario 6  
 Con la configuración siguiente:  

-   **El contenido no está disponible en un punto de distribución preferido**  

-   **Distribuir el contenido de este paquete en puntos de distribución preferidos** no está habilitado  

-   **Permitir reserva**: Habilitado  

-   **Comportamiento de implementación para red lenta**: descargar e instalar contenido.  


**Detalles:**  

1.  El cliente envía una solicitud de contenido al punto de administración. El cliente incluye una marca con la solicitud que indica que se habilitan los puntos de distribución de reserva.  

2.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos y los puntos de distribución de reserva que tienen el contenido. No hay puntos de distribución preferidos que tienen el contenido, pero al menos un punto de distribución de reserva tiene el contenido.  

3.  Se descarga el contenido desde un punto de distribución de reserva de la lista porque la propiedad de implementación si el cliente usa un punto de distribución de reserva está configurada como **Descargar e instalar el contenido**.  

## <a name="scenario-7"></a>Escenario 7  
 Con la configuración siguiente:  

-   **El contenido no está disponible en un punto de distribución preferido**  

-   **Distribuir el contenido de este paquete en puntos de distribución preferidos** está habilitado  

-   **Permitir reserva**: no habilitado.  

-   **Comportamiento de implementación para red lenta**: Cualquier configuración.  


**Detalles:**  

1.  El cliente envía una solicitud de contenido al punto de administración.  

2.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos que tienen el contenido. No hay puntos de distribución preferidos con el contenido.  

3.  Se produce un error en el cliente con el mensaje **El contenido no está disponible** y entra en modo de reintento. Cada hora se realiza una nueva solicitud de contenido.  

4.  El punto de administración crea un desencadenador para el administrador de distribución para distribuir el contenido a todos los puntos de distribución preferidos para el cliente que realizó la solicitud de contenido.  

5.  El administrador de distribución distribuye el contenido a todos los puntos de distribución preferidos. En la mayoría de los casos, el contenido se distribuye correctamente a los puntos de distribución preferidos en una hora.  

6.  El cliente inicia una nueva solicitud de contenido al punto de administración.  

7.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos que tienen el contenido. El cliente descarga el contenido desde un punto de distribución preferido de la lista.  

## <a name="scenario-8"></a>Escenario 8  
 Con la configuración siguiente:  

-   **El contenido no está disponible en un punto de distribución preferido**  

-   **Distribuir el contenido de este paquete en puntos de distribución preferidos** está habilitado  

-   **Permitir reserva**: Habilitado  

-   **Comportamiento de implementación para red lenta**: no descargar contenido.  


**Detalles:**  

1.  El cliente envía una solicitud de contenido al punto de administración. El cliente incluye una marca con la solicitud que indica que se permiten puntos de distribución de reserva.  

2.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos y los puntos de distribución de reserva que tienen el contenido. No hay puntos de distribución preferidos que tienen el contenido, pero al menos un punto de distribución de reserva tiene el contenido.  

3.  No se descarga el contenido porque la propiedad de implementación si el cliente usa un punto de distribución de reserva está configurada como **No descargar**. Se produce un error en el cliente con el mensaje **El contenido no está disponible** y entra en modo de reintento. El cliente realiza una solicitud de contenido nueva cada hora.  

4.  El punto de administración crea un desencadenador para el administrador de distribución para distribuir el contenido a todos los puntos de distribución preferidos para el cliente que realizó la solicitud de contenido.  

5.  El administrador de distribución distribuye el contenido a todos los puntos de distribución preferidos. En la mayoría de los casos, el contenido se distribuye correctamente a los puntos de distribución preferidos en una hora.  

6.  El cliente inicia una nueva solicitud de contenido al punto de administración.  

7.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos que tienen el contenido.  

8.  El cliente descarga el contenido desde un punto de distribución preferido de la lista.  

## <a name="scenario-9"></a>Escenario 9  
 Con la configuración siguiente:  

-   **El contenido no está disponible en un punto de distribución preferido**  

-   **Distribuir el contenido de este paquete en puntos de distribución preferidos** está habilitado  

-   **Permitir reserva**: Habilitado  

-   **Comportamiento de implementación para red lenta**: descargar e instalar contenido.  


**Detalles:**  

1.  El cliente envía una solicitud de contenido al punto de administración. El cliente incluye una marca con la solicitud que indica que se permiten puntos de distribución de reserva.  

2.  Se devuelve al cliente una lista de la ubicación del contenido desde el punto de administración con los puntos de distribución preferidos y los puntos de distribución de reserva que tienen el contenido. No hay puntos de distribución preferidos que tienen el contenido, pero al menos un punto de distribución de reserva tiene el contenido.  

3.  Se descarga el contenido desde un punto de distribución de reserva de la lista porque la propiedad de implementación si el cliente usa un punto de distribución de reserva está configurada como **Descargar e instalar el contenido**. Esta configuración de implementación permite que un cliente que debe usar una ubicación de contenido de reserva obtenga el contenido de esa ubicación.  

4.  El punto de administración crea un desencadenador para el administrador de distribución para distribuir el contenido a todos los puntos de distribución preferidos para el cliente que realizó la solicitud de contenido.  

5.  El administrador de distribución distribuye el contenido a todos los puntos de distribución preferidos, lo que permite a los clientes adicionales obtener el contenido sin utilizar un punto de distribución de reserva.  
