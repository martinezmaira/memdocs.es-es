---
title: Administrador de transferencia de paquetes
titleSuffix: Configuration Manager
description: Descubra cómo el administrador de transferencia de paquetes de Configuration Manager transfiere el contenido desde un servidor de sitio a los puntos de distribución remotos.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706513"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Administrador de transferencia de paquetes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En un sitio de Configuration Manager, el administrador de transferencia de paquetes es un componente del servicio SMS_Executive que administra la transferencia de contenido desde un equipo de servidor de sitio a puntos de distribución remotos en un sitio. (Un punto de distribución remoto es el que no se encuentra en el equipo de servidor del sitio). El administrador de transferencia de paquetes no es compatible con las configuraciones del administrador, pero comprender su funcionamiento puede ayudarle a planear su infraestructura de administración de contenido. También puede ayudarle a solucionar problemas de distribución de contenido.


Al distribuir contenido a uno o más puntos de distribución remotos de un sitio, el **Administrador de distribución** crea un trabajo de transferencia de contenido. Después, envía una notificación al administrador de transferencia de paquetes de los servidores de sitios primario y secundario para que transfiera el contenido a los puntos de distribución remotos.

 El administrador de transferencia de paquetes registra sus acciones en el archivo **pkgxfermgr.log** en el servidor de sitio. El archivo de registro es la única ubicación en la que puede visualizar las actividades del administrador de transferencia de paquetes.  

> [!NOTE]  
>  En versiones anteriores de Configuration Manager, el administrador de distribución gestiona la transferencia de contenido a un punto de distribución remoto. El administrador de distribución también gestiona la transferencia de contenido entre sitios. En Configuration Manager, el administrador de distribuciones sigue administrando la transferencia de contenido entre dos sitios. En cambio, el administrador de transferencia de paquetes ahora administra la transferencia de contenido a un gran número de puntos de distribución. Esto permite aumentar el rendimiento general de la distribución de contenido entre los sitios y los puntos de distribución de un sitio.  

Para transferir contenido a un punto de distribución estándar, el administrador de transferencia de paquetes funciona de la misma manera que el administrador de distribución en versiones anteriores de Configuration Manager. Es decir, administra activamente la transferencia de archivos a cada punto de distribución remoto. En cambio, para distribuir contenido a un punto de distribución de extracción, el administrador de transferencia de paquetes informa al punto de distribución de extracción de que hay contenido disponible. Después, el punto de distribución de extracción ejecuta el proceso de transferencia.  

En la información siguiente se describe cómo el administrador de transferencia de paquetes administra la transferencia de contenido a puntos de distribución estándar y a puntos de distribución configurados como puntos de distribución de extracción:
1.  **El administrador implementa contenido en uno o varios puntos de distribución de un sitio.**  

    -   **Punto de distribución estándar:** El administrador de distribución crea un trabajo de transferencia de contenido para el contenido.  

    -   **Punto de distribución de extracción**: El administrador de distribución crea un trabajo de transferencia de contenido para el contenido.  

2.  **El Administrador de distribución ejecuta comprobaciones preliminares.**  

    -   **Punto de distribución estándar:** El administrador de distribución ejecuta una comprobación básica para confirmar que cada punto de distribución está listo para recibir el contenido. Después de la comprobación, el administrador de distribución envía una notificación al administrador de transferencia de paquetes para iniciar la transferencia de contenido al punto de distribución.  

    -   **Punto de distribución de extracción**: el Administrador de distribución inicia el administrador de transferencia de paquetes, que informa al punto de distribución de extracción sobre la existencia de un nuevo trabajo de transferencia de contenido. El Administrador de distribución no comprueba el estado de los puntos de distribución remotos que son puntos de distribución de extracción, ya que cada punto de distribución de extracción administra sus propias transferencias de contenido.  

3.  **El administrador de transferencia de paquetes prepara la transferencia de contenido.**  

    -   **Punto de distribución estándar:** el administrador de transferencia de paquetes examina el almacén de contenido de instancia única de todos los puntos de distribución remotos especificados. El objetivo de esto es identificar los archivos que ya están en ese punto de distribución. A continuación, el administrador de transferencia de paquetes coloca en la cola para la transferencia solo a los archivos que no están todavía presentes.  

        > [!NOTE]  
        >  Para copiar todos los archivos de la distribución al punto de distribución (incluso si los archivos ya se incluían en el almacén de instancia única del punto de distribución), use la acción **Redistribuir** para contenido.  

    -   **Punto de distribución de extracción**: para cada punto de distribución de extracción en la distribución, el administrador de transferencia de paquetes comprueba los puntos de distribución de origen de los puntos de distribución de extracción para confirmar si el contenido está disponible.  

        -   Si el contenido está disponible como mínimo en un punto de distribución de origen, el administrador de transferencia de paquetes envía una notificación a ese punto de distribución de extracción. La notificación dirige ese punto de distribución para iniciar el proceso de transferencia de contenido. La notificación incluye atributos, valores hash y nombres y tamaños de archivos.  

        -   Si el contenido todavía no está disponible, el administrador de transferencia de paquetes no envía ninguna notificación al punto de distribución. En vez de ello, repetirá la comprobación cada 20 minutos hasta que el contenido esté disponible. A continuación, cuando el contenido esté disponible, el administrador de transferencia de paquetes envía la notificación al punto de distribución de extracción.  

        > [!NOTE]  
        >  Para que el punto de distribución de extracción copie todos los archivos de la distribución al punto de distribución (incluso si los archivos ya se incluían en el almacén de instancia única del punto de distribución de extracción), use la acción **Redistribuir** para contenido.  

4.  **Se inicia la transferencia de contenido.**  

    -   **Punto de distribución estándar:** El administrador de transferencia de paquetes copia los archivos a cada punto de distribución remoto. Durante la transferencia a un punto de distribución estándar:  

        -   De manera predeterminada, el administrador de transferencia de paquetes puede procesar simultáneamente tres paquetes únicos y distribuirlos en cinco puntos de distribución en paralelo. En conjunto, estos se denominan **Configuración de distribución simultánea**. Para configurar la distribución simultánea, en las **Propiedades del componente de distribución de software** de cada sitio, vaya a la pestaña **General**.  

        -   El administrador de transferencia de paquetes usa las configuraciones de programación y ancho de banda de red de cada punto de distribución para transferir contenido al punto de distribución correspondiente. Para configurar estas opciones, en las **Propiedades** de cada punto de distribución remoto, vaya a las pestañas **Programación** y **Límites de frecuencia**. Para más información, vea [Administración del contenido y de la infraestructura de contenido en Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Punto de distribución de extracción**: Cuando un punto de distribución de extracción recibe un archivo de notificación, el punto de distribución empieza el proceso de transferencia de contenido. El proceso de transferencia se ejecuta de forma independiente en cada punto de distribución de extracción:  

        1.   El punto de distribución de extracción identifica en la distribución de contenido los archivos que no figuran en su almacenamiento de instancia única y se prepara para descargar el contenido de uno de sus puntos de distribución de origen.  

        2.   A continuación, el punto de distribución de extracción busca de forma ordenada en los puntos de distribución de origen hasta encontrar un punto de distribución de origen con el contenido disponible. Cuando el punto de distribución de extracción identifica un punto de distribución de origen con el contenido, comienza la descarga de dicho contenido.  

        > [!NOTE]  
        >  El proceso de descarga de contenido con el punto de distribución de extracción es el mismo que usan los clientes de Configuration Manager. La configuración de transferencia simultánea no se usa para transferir contenido con el punto de distribución de extracción. Tampoco se usarán las opciones de programación y limitación que configure para los puntos de distribución estándar.  

5.  **La transferencia de contenido se completa.**  

    -   **Punto de distribución estándar:** cuando el administrador de transferencia de paquetes termina de transferir archivos a todos los puntos de distribución remotos designados, comprueba el hash del contenido en el punto de distribución. Después, informa al Administrador de distribución de que se ha completado la distribución.  

    -   **Punto de distribución de extracción**: cuando el punto de distribución de extracción completa la descarga de contenido, el punto de distribución comprueba el hash del contenido. Después, envía un mensaje de estado al punto de administración del sitio para indicar que se ha completado correctamente. Si no se recibe este estado después de 60 minutos, volverá a activarse el administrador de transferencia de paquetes. Comprueba el punto de distribución de extracción para confirmar si el punto de distribución de extracción ha descargado el contenido. Si la descarga de contenido está en curso, el administrador de transferencia de paquetes se suspende durante 60 minutos antes de volver a comprobar el punto de distribución de extracción. Este ciclo continúa hasta que el punto de distribución de extracción completa la transferencia de contenido.  
