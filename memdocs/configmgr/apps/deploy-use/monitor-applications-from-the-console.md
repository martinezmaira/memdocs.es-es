---
title: Supervisión de aplicaciones desde la consola
titleSuffix: Configuration Manager
description: Supervise la implementación de software, incluidas actualizaciones, configuración de cumplimiento y aplicaciones, mediante el área de trabajo Configuración de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689213"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Supervisar aplicaciones desde la consola de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


En Configuration Manager, puede supervisar la implementación de todo el software, incluidas las actualizaciones de software, la configuración de cumplimiento, las aplicaciones, las secuencias de tareas, los paquetes y los programas. Puede supervisar las implementaciones mediante el área de trabajo **Supervisión** en la consola de Configuration Manager o mediante el uso de informes.  

 Las aplicaciones de Configuration Manager admiten la supervisión basada en estado, lo cual le permite hacer un seguimiento del último estado de implementación de aplicación para usuarios y dispositivos. Estos mensajes de estado muestran información acerca de dispositivos individuales. Por ejemplo, si una aplicación se implementa en una recopilación de usuarios, puede ver el estado de cumplimiento de la implementación y el propósito de la implementación en la consola de Configuration Manager.  

## <a name="learn-about-compliance-states"></a>Más información sobre los estados de cumplimiento
 El estado de implementación de una aplicación puede tener uno de los siguientes estados de cumplimiento:  

-   **Correcto** : la implementación de aplicación se realizó correctamente o se encontró que ya estaba instalada.  

-   **En curso** : la implementación de aplicación está en curso.  

-   **Desconocido** : no se pudo determinar el estado de la implementación de aplicación. Este estado no se aplica a las implementaciones cuyo propósito sea **Disponible**. Este estado suele mostrarse cuando todavía no se han recibido mensajes de estado del cliente.  

-   **Requisitos no cumplidos** : la aplicación no se implementó porque no cumplía con los requisitos de una dependencia o una regla de requisitos, o porque el sistema operativo en el que se iba a implementar no correspondía.  

-   **Error** : la aplicación no pudo implementarse debido a un error.  

Puede ver información adicional para cada estado de cumplimiento, que incluye subcategorías dentro del estado de cumplimiento y la cantidad de usuarios y dispositivos en esa categoría. Por ejemplo, el estado de cumplimiento **Error** incluye las subcategorías siguientes:  

- Error al evaluar los requisitos  

- Errores relacionados con el contenido  

- Errores de instalación  

  Cuando se aplica más de un estado de cumplimiento para la implementación de una aplicación, puede ver el estado agregado que representa el cumplimiento más bajo. Por ejemplo:  

  -   Si un usuario inicia sesión en dos dispositivos y la aplicación se instala correctamente en uno de los dispositivos, pero produce error en el segundo, el estado agregado de implementación de la aplicación para ese usuario indicará **Error**.  

  -   Si se implementa una aplicación para todos los usuarios que inician sesión en un equipo, recibirá varios resultados de implementación para ese equipo. Si se produce un error en una de las implementaciones, el estado de implementación agregado para el equipo indicará **Error**.  

El estado de implementación para las implementaciones de paquete y de programa no se agrega.  

 Utilice estas subcategorías para que le ayuden a detectar rápidamente cualquier problema importante en la implementación de una aplicación. También puede ver información adicional acerca de los dispositivos que corresponden a una subcategoría particular de un estado de cumplimiento.  

 La administración de aplicaciones en Configuration Manager incluye una cantidad de informes integrados que permiten supervisar la información sobre las aplicaciones e implementaciones. Estos informes tienen la categoría de informe **Distribución de software - Supervisión de aplicaciones**.  

 Para obtener más información sobre cómo configurar informes en Configuration Manager, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Supervisión del estado de una aplicación en la consola de Configuration Manager  

1.  En la consola de Configuration Manager, elija **Supervisión** > **Implementaciones**.  

3.  Para ver los detalles de implementación de cada estado de cumplimiento y los dispositivos de ese estado, seleccione una implementación y, después, en la pestaña **Inicio**, en el grupo **Implementación**, pulse **Ver estado** para abrir el panel **Estado de implementación**. En este panel, puede ver los activos con cada estado de cumplimiento. Pulse en cualquier activo para ver información más detallada sobre el estado de implementación para dicho activo.  

    > [!NOTE]  
    >  El panel **Estado de implementación** puede mostrar hasta 20.000 elementos. Si necesita ver más elementos, use los informes de Configuration Manager para ver datos de estado de aplicación.  
    >   
    >  El estado de los tipos de implementación se muestra agregado en el panel **Estado de implementación** . Para ver información más detallada sobre los tipos de implementación, use el informe **Errores de infraestructura de aplicación** en la categoría de informe **Distribución de software - Supervisión de aplicaciones**.  

4.  Para revisar información de estado general sobre una implementación de aplicación, seleccione una implementación y, después, pulse la pestaña **Resumen** en la ventana **Implementación seleccionada**.  

5.  Para revisar información sobre el tipo de implementación de aplicaciones, seleccione una implementación y, después, pulse la pestaña **Tipos de implementación** en la ventana **Implementación seleccionada**.  

La información que se muestra en el panel **Estado de implementación** después de pulsar **Ver estado** está formada por datos en directo de la base de datos de Configuration Manager. La información que se muestra en la pestaña **Resumen** y la pestaña **Tipos de implementación** está formada por datos resumidos.

Si los datos que se muestran en la pestaña **Resumen** y en la pestaña **Tipos de implementación** no coinciden con los datos que se muestran en el panel **Estado de implementación**, pulse **Ejecutar resumen** para actualizar los datos de esas pestañas. Para configurar el intervalo de resumen predeterminado de implementación de aplicación, haga lo siguiente:  

1. En la consola de Configuration Manager, pulse **Administración** > **Configuración del sitio** > **Sitios**.

2. En la lista **Sitios**, seleccione el sitio para el que quiere configurar el intervalo de resumen y, después, en la pestaña **Inicio**, en el grupo **Configuración**, seleccione **Generadores de resumen de estado**.

3. En el cuadro de diálogo **Generadores de resumen de estado**, pulse **Generador de resumen de implementación de aplicación** y, después, seleccione **Editar**.  

4. En el cuadro de diálogo **Propiedades del generador de resumen de implementación de aplicación**, configure los intervalos de resumen requeridos y, después, pulse **Aceptar**.  
