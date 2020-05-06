---
title: Integración de Windows Update para empresas
titleSuffix: Configuration Manager
description: Use Windows Update para empresas (WUfB) para mantener Windows 10 actualizado para los dispositivos conectados al servicio Windows Update.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8bfd535c93cb9f1dcfc42705f3cce61874dfe226
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709323"
---
# <a name="integrate-with-windows-update-for-business"></a>Integración con Windows Update para empresas

*Se aplica a: Configuration Manager (rama actual)*

Windows Update para empresas (WUfB) permite mantener los dispositivos basados en Windows 10 de la organización siempre actualizados con las características de Windows y las defensas de seguridad más recientes cuando estos dispositivos se conectan directamente al servicio de Windows Update (WU). Configuration Manager puede diferenciar entre los equipos con Windows 10 que usan WUfB y WSUS para obtener actualizaciones de software.  

> [!WARNING]
> Si va a usar administración conjunta con los dispositivos y ha movido las [directivas de actualización de Windows](../../comanage/workloads.md#windows-update-policies) a Intune, los dispositivos obtendrán sus [directivas de Windows Update para empresas de Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Si sigue instalado el cliente de Configuration Manager en los dispositivos administrados conjuntamente, la configuración de actualizaciones acumulativas y actualizaciones de características se administra mediante Intune. Sin embargo, las revisiones de terceros, si están habilitadas en [**Configuración de cliente**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates), aún se administran con Configuration Manager.  

 Algunas características de Configuration Manager ya no están disponibles cuando los clientes de Configuration Manager se configuran para recibir actualizaciones de WU, lo que incluye WUfB o Windows Insiders:  

- Informes de cumplimiento de Windows Update:  
  - Configuration Manager no tendrá conocimiento de las actualizaciones que se publican en WU. Los clientes de Configuration Manager configurados para recibir actualizaciones de WU mostrarán **desconocido** para estas actualizaciones en la consola de Configuration Manager.  

  - La solución de problemas de estado de cumplimiento general es difícil porque el estado **desconocido** era solo para los clientes que no habían notificado su estado de examen a WSUS. Ahora también incluye los clientes de Configuration Manager que reciben las actualizaciones de WU.  

  - El cumplimiento de las actualizaciones de definición es parte de los informes de cumplimiento general de actualización y no funcionará como sería de esperar.

- Los informes generales de Endpoint Protection para Defender según el estado del cumplimiento de las actualizaciones no devolverán resultados precisos debido a la ausencia de datos de análisis.  

- Configuration Manager no podrá implementar las actualizaciones de Microsoft, como Office, Internet Explorer y Visual Studio, en los clientes que están conectados a WUfB para recibir actualizaciones.  

- Configuration Manager todavía puede implementar actualizaciones de terceros publicadas en WSUS y administradas a través de Configuration Manager en los clientes que están conectados a WUfB para recibir actualizaciones. Si no quiere que se instalen actualizaciones de terceros en los clientes que se conectan a WUfB, deshabilite la configuración de cliente llamada [Habilitar actualizaciones de software en clientes](../../core/clients/deploy/about-client-settings.md#software-updates).

- La implementación del cliente completo de Configuration Manager que usa la infraestructura de actualizaciones de software no funcionará para los clientes que están conectados a WUfB para recibir actualizaciones.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificación de los clientes que utilizan WUfB para las actualizaciones de Windows 10

Use el procedimiento siguiente para identificar los clientes que usan WUfB para obtener las actualizaciones de Windows 10. Después, configure estos clientes para que dejen de usar WSUS para obtener las actualizaciones, e implemente una configuración de agente cliente para deshabilitar el flujo de trabajo de actualizaciones de software para estos clientes.  

### <a name="prerequisites-for-wufb"></a>Requisitos previos para WUfB

- Clientes que ejecutan Windows 10 Desktop Pro o Windows 10 Enterprise Edition versión 1511 o posterior

- [Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) está implementado y los clientes utilizan WUfB para obtener las actualizaciones de Windows 10.  

### <a name="to-identify-clients-that-use-wufb"></a>Para identificar los clientes que utilizan WUfB  

1. Asegúrese de que el agente de Windows Update no examina WSUS, si se habilitó previamente. La clave del Registro siguiente se puede usar para indicar si el equipo se examina con WSUS o Windows Update. Si la clave del Registro no existe, no se examina WSUS.
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Existe un atributo nuevo, **UseWUServer**, que se encuentra en el nodo **Windows Update** del Explorador de recursos de Configuration Manager.
1. Cree una colección basada en el atributo **UseWUServer** para todos los equipos que estén conectados a través de WUfB para conseguir actualizaciones. Puede crear una colección basada en una consulta similar a la siguiente:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Cree una configuración de agente cliente para deshabilitar el flujo de trabajo de actualización de software. Implemente la configuración en la colección de equipos que están conectados directamente a WUfB.
1. Los equipos que se administran a través de WUfB, mostrarán el valor **Desconocido** en el estado de cumplimiento y no se tendrán en cuenta como parte del porcentaje total de cumplimiento.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configuración de directivas de aplazamiento de Windows Update para empresas
<!-- 1290890 -->
A partir de la versión 1706 de Configuration Manager, puede configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente mediante Windows Update para empresas. Puede administrar las directivas de aplazamiento en el nuevo nodo **Directivas de Windows Update para empresas**, en **Biblioteca de Software** > **Mantenimiento de Windows 10**.

> [!NOTE]
> A partir de la versión 1802 de Configuration Manager, se pueden establecer directivas de aplazamiento para Windows Insider. <!--507201-->  
Para obtener más información sobre el programa Windows Insider, consulte [Introducción al programa Windows Insider para empresas](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites-for-deferral-policies"></a>Requisitos previos para las directivas de aplazamiento

- Windows 10, versión 1703 o posteriores.
- Los dispositivos con Windows 10 administrados por Windows Update para empresas deben tener conectividad a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para crear una directiva de aplazamiento para Windows Update para empresas

1. En **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Directivas de Windows Update para empresas**
1. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Create Windows Update for Business Policy** (Crear directiva de Windows Update para empresas) para abrir el Asistente para creación de directiva de Windows Update para empresas.
1. En la página **General**, proporcione un nombre y una descripción para la directiva.
1. En la página **Deferral Policies** (Directivas de aplazamiento), configure si se van a aplazar o pausar las actualizaciones de características. Las actualizaciones de características son generalmente nuevas características de Windows. Después de configurar el parámetro **Nivel de preparación de la rama**, puede definir si le gustaría aplazar la recepción de actualizaciones de características después de que se pongan a disposición de los usuarios por parte de Microsoft, y por cuánto tiempo.
    - **Nivel de preparación de la rama**: Establezca la rama para la que el dispositivo recibirá actualizaciones de Windows. Elija el canal semianual (dirigido), el canal semianual o una compilación de Windows Insider.

        > [!NOTE]
        > Implemente directivas para el **canal semianual (dirigido)** en Windows 10, *versión 1903 o posterior*. Implemente directivas para el **canal semianual** en Windows 10, *versión 1809 o anterior*.
        >
        > Si implementa una directiva para **canal semianual** en Windows 10, versión 1903 o posterior, se produce un error **0x8004100c** en la implementación.<!-- 5593139 -->

    - **Período de aplazamiento (días)** :  especifique el número de días durante los que se aplazarán las actualizaciones de características. Puede aplazar la recepción de estas actualizaciones de características hasta 365 días a partir de su lanzamiento.
    - **Pausar el inicio de las actualizaciones de características:** : seleccione si desea pausar la recepción de actualizaciones de características para los dispositivos durante un máximo de 35 días a partir del momento en que pausa las actualizaciones. Una vez que transcurra el máximo de días, la funcionalidad de pausa expirará automáticamente y el dispositivo buscará actualizaciones aplicables en Windows Update. Después de este análisis, puede pausar las actualizaciones de nuevo. Puede quitar la pausa de las actualizaciones de características desactivando la casilla.
1. Elija si desea aplazar o pausar las actualizaciones de calidad. Las actualizaciones de calidad suelen ser correcciones y mejoras en la funcionalidad de Windows existente y normalmente se publican el primer martes de cada mes, aunque pueden publicarse en cualquier momento por parte de Microsoft. Puede definir si desea aplazar la recepción de actualizaciones de calidad después de su lanzamiento, y por cuánto tiempo.
    - **Período de aplazamiento (días)** : especifique el número de días durante los que se aplazarán las actualizaciones de calidad. Puede aplazar la recepción de estas actualizaciones de calidad hasta 30 días a partir de su lanzamiento.
    - **Pausar el inicio de actualizaciones de calidad:** : seleccione si desea pausar la recepción de actualizaciones de calidad para los dispositivos durante un máximo de 35 días a partir del momento en que pausa las actualizaciones. Una vez que transcurra el máximo de días, la funcionalidad de pausa expirará automáticamente y el dispositivo buscará actualizaciones aplicables en Windows Update. Después de este análisis, puede pausar las actualizaciones de nuevo. Puede quitar la pausa de las actualizaciones de calidad desactivando la casilla.
1. Seleccione **Instalar actualizaciones de otros productos de Microsoft** para habilitar el parámetro de directiva de grupo que permite que la configuración de aplazamiento sea aplicable a Microsoft Update, así como a las actualizaciones de Windows Update.
1. Seleccione **Include drivers with Windows Update** (Incluir controladores con Windows Update) para actualizar automáticamente los controladores desde las actualizaciones de Windows Update. Si desactiva esta opción, no se descargan las actualizaciones de controladores desde Windows Update.
1. Complete el asistente para crear la nueva directiva de aplazamiento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implementar una directiva de aplazamiento para Windows Update para empresas

1. En **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Directivas de Windows Update para empresas**
1. En la pestaña **Inicio** del grupo **Implementación**, seleccione **Implementar la directiva de Windows Update for Business**.
1. Configure las siguientes opciones:
    - **Directiva de configuración que desea implementar**: seleccione la directiva de Windows Update para empresas que quiere implementar.
    - **Colección**: haga clic en **Examinar** para seleccionar la colección en la que quiere implementar la directiva.
    - **Permitir la corrección fuera de la ventana de mantenimiento**: si se ha configurado una ventana de mantenimiento para la colección en la que se va a implementar la directiva, habilite esta opción para permitir que la configuración de la directiva corrija el valor fuera de la ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).
    - **Programación**: especifique la programación de evaluación de cumplimiento según la cual se evalúa la directiva implementada en los equipos cliente. La programación puede ser simple o personalizada.
1. Complete el asistente para implementar la directiva.
