---
title: Actualización de clientes en Windows
titleSuffix: Configuration Manager
description: Actualice clientes en equipos Windows en Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3849f360b2f22f2f48bbe49159b610399158b29
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427760"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Actualización de clientes de equipos Windows con System Center Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Actualice el cliente de Configuration Manager en equipos Windows mediante los métodos de instalación de cliente o la característica de actualización de cliente automática. Los siguientes métodos de instalación de cliente son mecanismos válidos para actualizar el software cliente en equipos Windows:  

- Instalación de directiva de grupo  

- Instalación de script de inicio de sesión  

- Instalación manual  

- Instalación de actualización  

Para obtener más información, consulte [Cómo implementar clientes en equipos Windows](../../deploy/deploy-clients-to-windows-computers.md).

Excluya clientes de la actualización especificando una colección de exclusión. Para obtener más información, consulte [Cómo excluir la actualización de clientes](exclude-clients-windows.md). Los clientes excluidos podrán continuar descargando y ejecutando CCMSETUP, pero no se actualizarán.

> [!TIP]  
> Si actualiza la infraestructura del servidor desde una versión anterior de Configuration Manager, complete las actualizaciones del servidor antes de actualizar los clientes de Configuration Manager. Este proceso incluye la instalación de todas las actualizaciones de la rama actual. La última actualización de la rama actual contiene la versión más reciente del cliente. Actualice los clientes después de haber instalado todas las actualizaciones de Configuration Manager.

> [!NOTE]
> Si piensa volver a asignar el sitio a los clientes durante la actualización, especifique el nuevo sitio mediante la propiedad de client.msi `SMSSITECODE`. Si usa el valor de `AUTO` para `SMSSITECODE`, especifique también `SITEREASSIGN=TRUE`. Esta propiedad permite la reasignación de sitio automática durante la actualización. Para obtener más información, vea [Acerca de las propiedades de instalación de clientes: SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a> Acerca de la actualización de cliente automática

Configure el sitio para actualizar automáticamente los clientes a la última versión de Configuration Manager. Cuando Configuration Manager identifica que la versión de un cliente asignado es anterior a la versión de la jerarquía, actualiza automáticamente el cliente. Este escenario incluye la actualización del cliente a la última versión cuando intenta asignarse a un sitio de Configuration Manager.  

Un cliente puede actualizarse automáticamente en los siguientes escenarios:  

- La versión del cliente es anterior a la que se utiliza en la jerarquía.  

- El cliente del sitio de administración central tiene instalado un paquete de idioma y el cliente existente no lo tiene.  

- Uno de los requisitos previos del cliente de la jerarquía es de una versión diferente a la instalada en el cliente.  

- Uno o varios de los archivos de instalación del cliente son de una versión diferente.  

> [!NOTE]  
> Para identificar las diferentes versiones del cliente de Configuration Manager de su jerarquía, use el informe **Recuento de clientes de Configuration Manager por versiones de cliente** de la carpeta de informes **Sitio - Información del cliente**.  

Configuration Manager crea un paquete de actualización de forma predeterminada. Envía automáticamente el paquete a todos los puntos de distribución de la jerarquía. Si realiza cambios en el paquete de cliente en el sitio de administración central, Configuration Manager actualiza automáticamente el paquete y lo redistribuye. Un cambio de ejemplo es cuando se agrega un paquete de idioma de cliente. Si habilita la actualización automática de cliente, todos los clientes instalan automáticamente el nuevo paquete de idioma del cliente.

> [!NOTE]  
> Configuration Manager no envía de forma automática el paquete de actualización de cliente a los puntos de distribución basados en la nube de Configuration Manager.  

Habilite las actualizaciones de cliente automáticas en la jerarquía. Esta configuración mantiene los clientes actualizados con menos esfuerzo.  

Si también administra sus sistemas de sitio de Configuration Manager como clientes, determine si desea incluirlos como parte del proceso de actualización automática. Puede excluir todos los servidores, o una colección específica, de la actualización de cliente. Algunos roles de sitio de Configuration Manager comparten el marco de trabajo de cliente. Por ejemplo, el punto de administración y el punto de distribución de extracción. Estos roles se actualizan al actualizar el sitio, por lo que la versión del cliente en estos servidores se actualiza al mismo tiempo.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a> Configuración de la actualización automática de cliente

Utilice el siguiente procedimiento para configurar la actualización de cliente automática en el sitio de administración central. Esta configuración se aplica a todos los clientes de la jerarquía.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y después haga clic en el nodo **Sitios**.  

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Sitios**, seleccione **Configuración de jerarquía**.  

1. Cambie a la pestaña **Actualización de cliente**. Revise la versión y la fecha del cliente de producción. Asegúrese de que es la versión que desea usar para actualizar los clientes. Si no es la versión de cliente que espera, quizá sea necesario promover el cliente de preproducción a producción. Para obtener más información, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](test-client-upgrades.md).  

1. Seleccione **Actualizar todos los clientes en la jerarquía con un cliente de producción**. Seleccione **Aceptar** para confirmar.  

1. Si no quiere que las actualizaciones de cliente se apliquen a los servidores, seleccione **No actualizar servidores**.  

1. Especifique el número de días en que los dispositivos deben actualizar el cliente. Una vez que el dispositivo recibe la directiva, actualiza el cliente en un intervalo aleatorio dentro de este número de días. Este comportamiento impide que un gran número de clientes se actualicen simultáneamente.

    > [!NOTE]
    > Un equipo debe estar en ejecución para actualizar el cliente. Si no hay ningún equipo en ejecución cuando se ha programado la recepción de la actualización, esta no se lleva a cabo. Cuando el equipo se enciende y recibe la directiva, programa la actualización en una hora aleatoria dentro del número de días permitido. Si esto ocurre una vez transcurrido el número de días para actualizar, programa la actualización para que se produzca a una hora aleatoria en las próximas 24 horas después de reiniciar el equipo.
    >
    > Debido a este comportamiento, los equipos que habitualmente se apagan pueden tardar más de lo esperado en actualizarse si la hora de actualización programada de forma aleatoria no se encuentra dentro de las horas normales de trabajo.

1. Si quiere excluir clientes de la actualización, seleccione **Excluir los clientes especificados de la actualización** y especifique la colección que se va a excluir. Para obtener más información, consulte [Cómo excluir la actualización de clientes para equipos Windows](exclude-clients-windows.md).

1. Si quiere que el sitio copie el paquete de instalación de cliente a los puntos de distribución habilitados para [contenido preconfigurado](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent), seleccione la opción **Distribuir automáticamente un paquete de instalación de cliente a los puntos de distribución habilitados para contenido preconfigurado**.  

1. Haga clic en **Aceptar** para guardar la configuración y cerrar las propiedades de configuración de jerarquía.

Los clientes reciben esta configuración la próxima vez que descarguen la directiva.

> [!NOTE]
> Las actualizaciones de cliente cumplen las ventanas de mantenimiento de Configuration Manager que ha configurado. El subproceso execmgr solo ejecuta el programa de arranque del programa de instalación del cliente (ccmsetup.exe) durante una ventana de mantenimiento. Si el dispositivo ejecuta una edición de Windows con un filtro de escritura, ccmsetup intenta descargar e instalar al mismo tiempo. De lo contrario, ccmsetup aleatoriza una hora para descargar el contenido. Después de descargar el contenido y de compilar la directiva local, execmgr programa la actualización del cliente durante la siguiente ventana de mantenimiento.<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>Pasos siguientes

Para obtener métodos alternativos para actualizar clientes, vea [Cómo implementar clientes en equipos Windows](../../deploy/deploy-clients-to-windows-computers.md).

Excluya clientes específicos de la actualización automática. Para obtener más información, consulte [Cómo excluir la actualización de clientes](exclude-clients-windows.md).
