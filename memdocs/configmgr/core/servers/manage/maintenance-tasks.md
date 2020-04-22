---
title: Tareas de mantenimiento
titleSuffix: Configuration Manager
description: Obtenga información sobre las tareas de mantenimiento que deben llevarse a cabo para las jerarquías y los sitios de Configuration Manager y el momento en que deben realizarse.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694443"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Mantenimiento de tareas de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los sitios y las jerarquías de Configuration Manager requieren un mantenimiento y supervisión regulares para poder prestar servicios de forma efectiva y continua. El mantenimiento periódico garantiza que el hardware, el software y la base de datos de Configuration Manager funcionan de manera correcta y eficaz. Un rendimiento óptimo reduce en gran medida el riesgo de error.  

 Para configurar alertas y usar el sistema de estado para supervisar el estado de Configuration Manager, vea [Usar alertas y el sistema de estado de Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a> Tareas de mantenimiento

 Es importante realizar un mantenimiento periódico para garantizar las operaciones correctas en el sitio. Lleve un registro de mantenimiento para documentar las fechas de mantenimiento, quién lo ha realizado y cualquier comentario sobre la tarea relativo al mantenimiento. Para mantener su sitio, considere la posibilidad de realizar un mantenimiento diario o semanal. Algunas tareas podrían requerir una programación diferente. El mantenimiento común puede incluir tareas de mantenimiento integradas y otras tareas, como el mantenimiento de cuentas para cumplir con las directivas de la empresa.  

 Use la siguiente información como guía para planear el momento adecuado para realizar las distintas tareas de mantenimiento. Use estas listas como punto de partida y agregue las tareas que necesite.  

### <a name="daily-tasks"></a>Tareas diarias
A continuación se indican las tareas de mantenimiento que puede realizar a diario:  

- Compruebe que las tareas de mantenimiento predefinidas, programadas para ejecutarse a diario, se ejecutan correctamente.  

- Compruebe el estado de la base de datos de Configuration Manager.  

- Compruebe el estado del servidor de sitio.  

- Compruebe si existen archivos pendientes en las bandejas de entrada del sistema de sitio de Configuration Manager.  

- Compruebe el estado de los sistemas de sitio.  

- Compruebe los registros de eventos del sistema operativo desde los sistemas de sitio.  

- Compruebe el registro de errores de SQL Server desde el equipo de base de datos del sitio.  

- Compruebe el rendimiento del sistema.  

- Compruebe las alertas de Configuration Manager.  

### <a name="weekly-tasks"></a>Tareas semanales

A continuación se indican las tareas de mantenimiento que puede realizar semanalmente:  

- Compruebe que las tareas de mantenimiento predefinidas, programadas para ejecutarse semanalmente, se ejecutan correctamente.  

- Elimine archivos innecesarios de los sistemas de sitio.  

- Produzca y distribuya informes para el usuario final, si es necesario.  

- Realice una copia de seguridad de los registros de eventos de la aplicación, de seguridad y del sistema, y bórrelos.  

- Compruebe el tamaño de la base de datos de sitio y compruebe que hay suficiente espacio en disco disponible en el servidor de base de datos del sitio para que pueda aumentar la base de datos del sitio.  

- Realice el mantenimiento de la base de datos de SQL Server en la base de datos del sitio, según su plan de mantenimiento de SQL Server.  

- Compruebe el espacio en disco disponible en todos los sistemas de sitio.  

- Ejecute las herramientas de desfragmentación de disco en todos los sistemas de sitio.  

### <a name="periodic-tasks"></a>Tareas periódicas

Algunas tareas que no requieren un mantenimiento diario o semanal son importantes para garantizar un buen mantenimiento general del sitio. Estas tareas también garantizan que los planes de seguridad y recuperación ante desastres estén actualizados. Estas son las tareas de mantenimiento que pueden realizarse de forma más periódica que las tareas diarias o semanales:  

- Cambie las cuentas y contraseñas, si es necesario, según el plan de seguridad.  

- Revise el plan de mantenimiento para comprobar que las tareas de mantenimiento programado se programan de manera correcta y eficaz, en función de las opciones del sitio configurado.  

- Revise los cambios requeridos en el diseño de la jerarquía de Configuration Manager.  

- Compruebe el rendimiento de red para asegurarse de que no se han realizado cambios que afecten a las operaciones del sitio.  

- Compruebe que la configuración de Active Directory que afecta a las operaciones del sitio no ha cambiado. Por ejemplo, compruebe que las subredes asignadas a los sitios de Active Directory que se usan como límites para el sitio de Configuration Manager no han cambiado.  

- Revise los cambios requeridos en su plan de recuperación ante desastres.  

- Realice una recuperación del sitio de acuerdo con el plan de recuperación ante desastres en un laboratorio de pruebas mediante una copia de seguridad de la copia de seguridad más reciente creada por la tarea de mantenimiento Copia de seguridad del servidor del sitio.

- Compruebe si hay algún error en el hardware o si hay actualizaciones de hardware disponibles.  

- Compruebe el estado general del sitio.  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Mantenimiento del estado operativo de la base de datos

 Mientras el sitio y la jerarquía de Configuration Manager ejecutan las tareas que el usuario programa y configura, los componentes de sitio agregan continuamente datos a la base de datos de Configuration Manager. A medida que aumenta la cantidad de datos, disminuye el rendimiento de la base de datos y el espacio de almacenamiento libre de la base de datos. Puede configurar las tareas de mantenimiento de sitio para quitar los datos antiguos que ya no necesita.  

 Configuration Manager proporciona tareas de mantenimiento predefinidas que puede usar para mantener el estado de la base de datos de Configuration Manager. No todas las tareas de mantenimiento están disponibles en cada sitio de forma predeterminada. Algunas tareas están habilitadas y otras no, pero todas admiten la programación que configure.  

 La mayoría de las tareas de mantenimiento quitan periódicamente datos obsoletos de la base de datos de Configuration Manager. La reducción del tamaño de la base de datos mediante la supresión de datos innecesarios mejora el rendimiento y la integridad de la base de datos, lo que aumenta la eficacia de la jerarquía y del sitio. Otras tareas, como **Recompilar índices**, permiten mantener la eficacia de la base de datos. Otras tareas, como la tarea **Copia de seguridad del servidor del sitio**, le ayudan a prepararse para la recuperación ante desastres.  

> [!IMPORTANT]
> Al planear la programación de cualquier tarea que elimina datos, considere el uso de los datos en la jerarquía. Cuando una tarea que elimina los datos se ejecuta en un sitio, la información se quita de la base de datos de Configuration Manager, y este cambio se replica en todos los sitios de la jerarquía. Esta eliminación puede afectar a otras tareas que dependen de esos datos. Por ejemplo, en el sitio de administración central, puede configurar la detección para que se ejecute una vez al mes con objeto de identificar equipos no cliente y planear la instalación del cliente de Configuration Manager para estos equipos antes de que transcurran dos semanas desde su detección. En cambio, en un sitio de la jerarquía, un administrador ha configurado la tarea Eliminar datos de detección antiguos para que se ejecute cada siete días. El resultado es que siete días después de que se detecten equipos no cliente, se eliminan de la base de datos de Configuration Manager. En el sitio de administración central, prepare la instalación de inserción del cliente de Configuration Manager en estos equipos nuevos el día 10. Sin embargo, como se había ejecutado la tarea Eliminar datos de detección antiguos y había eliminado datos a partir de siete días de antigüedad, esos equipos recientemente detectados ya no están disponibles en la base de datos.

Después de instalar un sitio de Configuration Manager, revise las tareas de mantenimiento disponibles y habilite las tareas que requieren sus operaciones. Revise la programación predeterminada de cada tarea y, cuando sea necesario, establezca la programación para refinar la tarea de mantenimiento de modo que se ajuste a su entorno y jerarquía. Aunque la programación predeterminada de cada tarea debe adaptarse a la mayoría de los entornos, supervise el rendimiento de los sitios y de la base de datos, y refine las tareas para aumentar la eficacia de las implementaciones. Tenga prevista la revisión periódica del rendimiento del sitio y de la base de datos, y vuelva a configurar las tareas de mantenimiento y sus programaciones para mantener esa eficacia.  

## <a name="set-up-maintenance-tasks"></a>Configurar tareas de mantenimiento

 Cada sitio de Configuration Manager admite tareas de mantenimiento que ayudan a mantener la eficiencia operativa de la base de datos del sitio. De forma predeterminada, se habilitan varias tareas de mantenimiento en cada sitio y todas las tareas compatibles con programaciones independientes. Las tareas de mantenimiento se configuran individualmente para cada sitio y se aplican a la base de datos de ese sitio. A pesar de ello, algunas tareas, como **Eliminar datos de detección antiguos**, afectan a la información que está disponible en todos los sitios de una jerarquía.  

 Solo las tareas de mantenimiento que se pueden configurar en un sitio se muestran en la consola de Configuration Manager. Para obtener una lista completa de las tareas de mantenimiento por tipo de sitio, vea [Referencia de tareas de mantenimiento para Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Use el procedimiento siguiente como ayuda para configurar las opciones de configuración comunes de las tareas de mantenimiento.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Para configurar las tareas de mantenimiento de la versión 1906 de Configuration Manager
<!--3555894-->
A partir de la versión 1906, las tareas de mantenimiento del servidor de sitio ahora se pueden ver, editar y supervisar desde su propia pestaña en la vista de detalles de un servidor de sitio. Puede seguir editando las tareas de mantenimiento si elige **Mantenimiento del sitio** en el grupo **Configuración**, tal como lo hizo en versiones anteriores de Configuration Manager.

1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración de sitio** >**Sitios**.
1. Seleccione un sitio de la lista y, después, haga clic en la pestaña **Tareas de mantenimiento** del panel de detalles.
1. Solo se muestran las tareas disponibles en el sitio seleccionado. Haga clic con el botón derecho en una de las tareas de mantenimiento y elija una de las opciones siguientes:
   - **Habilitar**: se activa la tarea.
   - **Deshabilitar**: se desactiva la tarea.
   - **Editar**: se edita la programación de la tarea o sus propiedades.

![Pestaña para tareas de mantenimiento en la vista de detalles de un servidor de sitio](./media/3555894-maintenance-tasks.png)

En la pestaña **Tareas de mantenimiento** se proporciona la información siguiente:

- Si la tarea está habilitada
- La programación de la tarea
- La última hora de inicio
- La última hora de finalización
- Si la tarea se ha completado correctamente
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Para configurar las tareas de mantenimiento de la versión 1902 de Configuration Manager y versiones anteriores

1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración de sitio** >**Sitios**.
2. Seleccione el sitio que contiene la tarea de mantenimiento que quiere configurar.  
3. En la pestaña **Inicio**, en el grupo **Configuración**, seleccione **Mantenimiento del sitio** y, después, elija la tarea de mantenimiento que quiere configurar. Solo se muestran las tareas disponibles en el sitio seleccionado.

4. Para configurar la tarea, elija **Editar**. Asegúrese de que la casilla **Habilitar esta tarea** esté activada y configure una programación para cuando la tarea se ejecute. Si la tarea también elimina los datos antiguos, configure la antigüedad de los datos que se eliminarán de la base de datos cuando se ejecuta la tarea. Seleccione **Aceptar** para cerrar las **Propiedades** de la tarea.

   > [!NOTE]  
   > Para **Eliminar mensajes de estado antiguos**, configure la antigüedad de los datos que se deben eliminar al configurar las reglas de filtro de estado.  

5. Para habilitar o deshabilitar la tarea sin necesidad de editar las propiedades de la tarea, seleccione el botón **Habilitar** o **Deshabilitar**. El botón etiqueta cambia según la configuración actual de la tarea.  
6. Cuando haya terminado de configurar las tareas de mantenimiento, seleccione **Aceptar** para finalizar el procedimiento.

## <a name="next-steps"></a>Pasos siguientes

[Referencia de las tareas de mantenimiento](reference-for-maintenance-tasks.md)
