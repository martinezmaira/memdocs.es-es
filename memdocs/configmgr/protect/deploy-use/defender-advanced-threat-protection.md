---
title: Protección contra amenazas avanzada de Microsoft Defender
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar y supervisar Protección contra amenazas avanzada de Microsoft Defender, un nuevo servicio que ayuda a las empresas a responder ante ataques sofisticados.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5feaf05a6829d902b1d8dcbe57722dfce410de6f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693546"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Microsoft Defender

*Se aplica a: Configuration Manager (rama actual)*

Endpoint Protection puede ayudar a administrar y supervisar [Protección contra amenazas avanzada (ATP) de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (anteriormente conocido como ATP de Windows Defender). ATP de Microsoft Defender ayuda a las empresas a detectar e investigar ataques avanzados en sus redes, y responder ante ellos. Las directivas de Configuration Manager pueden ayudarlo a incorporar y supervisar clientes de Windows 10.

ATP de Microsoft Defender es un servicio del [Centro de seguridad de Microsoft Defender](https://securitycenter.windows.com). Al agregar e implementar un archivo de configuración de incorporación de cliente, Configuration Manager puede supervisar el estado de implementación y el mantenimiento del agente de ATP de Microsoft Defender. ATP de Microsoft Defender es compatible con equipos que ejecutan el cliente de Configuration Manager o que se [administran mediante Microsoft Intune](/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Requisitos previos

- Suscripción al servicio en línea Protección contra amenazas avanzada de Microsoft Defender  
- Equipos Mac que ejecutan el cliente de Configuration Manager
- Clientes que usan un sistema operativo que aparece en la sección [Sistemas operativos de cliente compatibles](#bkmk_os) siguiente.

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> Sistemas operativos de cliente compatibles

Según la versión de Configuration Manager que se ejecute, pueden incorporarse los siguientes sistemas operativos de cliente:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager versión 1910 y anteriores

- Equipos cliente que ejecutan Windows 10, versión 1607 y posteriores

#### <a name="configuration-manager-version-2002-and-later"></a>Versión 2002 y posteriores de Configuration Manager
<!--5229962-->
A partir de Configuration Manager versión 2002, puede incorporar los siguientes sistemas operativos:

- Windows 8.1
- Windows 10, versión 1607 o posterior
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, versión 1803 o posterior
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Acerca de la incorporación a ATP con Configuration Manager

Los distintos sistemas operativos tienen diferentes necesidades de incorporación a ATP. Windows 8.1 y otros dispositivos de sistemas operativos de nivel inferior necesitan la **clave del área de trabajo** y el **id. de área de trabajo** para la incorporación. Los dispositivos de nivel superior, como Windows Server versión 1803, necesitan el archivo de configuración de incorporación. Configuration Manager también instala Microsoft Monitoring Agent (MMA) cuando los dispositivos incorporados lo necesitan, pero no lo actualiza de forma automática.

Entre los sistemas operativos de nivel superior se incluyen los siguientes:
- Windows 10, versión 1607 y posteriores
- Windows Server 2016, versión 1803 o posterior
- Windows Server 2019

Entre los sistemas operativos de nivel inferior se incluyen los siguientes:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, versión 1709 y anteriores

Al incorporar dispositivos a ATP con Configuration Manager, implemente la directiva de ATP en una colección de destino o en varias colecciones. En ocasiones, la colección de destino contiene dispositivos que ejecutan cualquier número de los sistemas operativos compatibles. Las instrucciones para la incorporación de estos dispositivos varían en función de si el destino es una colección que contiene dispositivos con sistemas operativos de nivel superior, inferior o ambos.

- Si la recopilación de destino contiene dispositivos de nivel superior y de nivel inferior, siga las instrucciones para [incorporar dispositivos que ejecuten cualquier sistema operativo compatible](#bkmk_any_os) (recomendado).
- Si la colección solo contiene dispositivos de nivel superior, puede usar las [instrucciones de incorporación de nivel superior](#bkmk_uplevel).
- Si la colección solo contiene dispositivos de nivel inferior, puede usar las [instrucciones de incorporación de nivel inferior](#bkmk_downlevel).

> [!Warning]
> - Si la colección de destino contiene dispositivos de nivel superior y usa las instrucciones para dispositivos de nivel inferior, los dispositivos de nivel superior no se incorporarán.
> - Si la colección de destino contiene dispositivos de nivel inferior y usa las instrucciones para dispositivos de nivel superior, los dispositivos de nivel inferior no se incorporarán.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a> Incorporación de dispositivos con cualquier sistema operativo compatible a ATP (recomendado)
 Puede incorporar a ATP dispositivos que ejecuten cualquiera de los [sistemas operativos compatibles](#bkmk_os) si proporciona el archivo de configuración, la **clave del área de trabajo**  y el **identificador de área de trabajo** a Configuration Manager.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Obtención del archivo de configuración, el identificador del área de trabajo y la clave del área de trabajo

1. Vaya a el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/) e inicie sesión.
1. Seleccione **Configuración** y después **Incorporación** en el título **Administración de dispositivos**.
1. Para el sistema operativo, seleccione **Windows 10**.
1. Elija **Microsoft Endpoint Configuration Manager current branch and later** (Rama actual de Microsoft Endpoint Configuration Manager y posteriores) para el método de implementación.
1. Haga clic en **Descargar paquete**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Descarga del archivo de configuración de incorporación" lightbox="media/5229962-onboarding-configuration.png":::
1. Descargue el archivo comprimido (.zip) y extraiga el contenido.
1. Seleccione **Configuración** y después **Incorporación** en el título **Administración de dispositivos**.
1. Para el sistema operativo, seleccione **Windows 7 SP1 y 8.1** o **Windows Server 2008 R2 Sp1, 2012 R2 y 2016** en la lista.
   - La **clave del área de trabajo** y el **id. del área de trabajo** serán iguales, con independencia de las opciones que elija.
1. Copie los valores correspondientes a **Clave del área de trabajo** e **Id. del área de trabajo** de la sección **Configurar conexión**.

   > [!IMPORTANT]
   > El archivo de configuración de ATP de Microsoft Defender contiene información confidencial que debe mantenerse segura.


### <a name="onboard-the-devices"></a>Incorporación de los dispositivos

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** > **Directivas de ATP de Microsoft Defender**.
1. Seleccione **Crear directiva de ATP de Microsoft Defender** para abrir el Asistente para directivas de ATP de Microsoft Defender. 
1. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Incorporación**.
1. **Navegue** al archivo de configuración que ha extraído del archivo .zip descargado.
1. Proporcione la **clave del área de trabajo** y el **id. de área de trabajo**, y después haga clic en **Siguiente**.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Asistente para crear directiva de ATP de Microsoft Defender" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Especifique los ejemplos de archivos de dispositivos administrados que se recopilan y se comparten para su análisis.  
   - **Ninguno**
   - **Todos los tipos de archivo**  
1. Revise el resumen y finalice el asistente.  
1. Haga clic con el botón derecho en la directiva que ha creado y, después, seleccione **Implementar** para dirigir la directiva de ATP de Microsoft Defender a los clientes.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a> Incorporación de dispositivos a ATP que ejecutan sistemas operativos de nivel superior

Los clientes de nivel superior requieren un archivo de configuración de incorporación para la incorporación a ATP. Entre los sistemas operativos de nivel superior se incluyen los siguientes:
- Windows 10, versión 1607 y posteriores 
- Windows Server 2016, versión 1803 y posteriores
- Windows Server 2019

Si la colección de destino contiene dispositivos de nivel superior y de nivel inferior, o si no está seguro, siga las instrucciones para [incorporar dispositivos que ejecuten cualquier sistema operativo compatible](#bkmk_any_os) (recomendado).

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Obtención de un archivo de configuración de incorporación para dispositivos de nivel superior

1. Vaya a el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/) e inicie sesión.
1. Seleccione **Configuración** y después **Incorporación** en el título **Administración de dispositivos**.
1. Para el sistema operativo, seleccione **Windows 10**.
1. Elija **Microsoft Endpoint Configuration Manager current branch and later** (Rama actual de Microsoft Endpoint Configuration Manager y posteriores) para el método de implementación.
1. Haga clic en **Descargar paquete**.
1. Descargue el archivo comprimido (.zip) y extraiga el contenido.

> [!IMPORTANT]
> El archivo de configuración de ATP de Microsoft Defender contiene información confidencial que debe mantenerse segura.


### <a name="onboard-the-up-level-devices"></a>Incorporación de los dispositivos de nivel superior

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** > **Directivas de ATP de Microsoft Defender** y seleccione **Crear directiva de ATP de Microsoft Defender**. Se abre el Asistente para crear directiva de ATP de Microsoft Defender.  
1. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Incorporación**.
1. **Navegue** al archivo de configuración que ha extraído del archivo .zip descargado.
   > [!Note]
   > Para la versión 2002 de Configuration Manager, necesitará la **Clave del área de trabajo** y el **Id. del área de trabajo** incluso si solo va a incorporar dispositivos de nivel superior. Para obtener estos valores, seleccione **Configuración** > **Incorporación** > **Windows 7 y 8.1** en el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/). <!--7054188-->
1. Especifique los ejemplos de archivos de dispositivos administrados que se recopilan y se comparten para su análisis.  
   - **Ninguno**
   - **Todos los tipos de archivo**  
1. Revise el resumen y finalice el asistente.  
1. Haga clic con el botón derecho en la directiva que ha creado y, después, seleccione **Implementar** para dirigir la directiva de ATP de Microsoft Defender a los clientes.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a> Incorporación de dispositivos a ATP que ejecutan sistemas operativos de nivel inferior

Los clientes de nivel inferior requieren la **clave del área de trabajo** y el **id. de área de trabajo** para la incorporación a ATP. Entre los sistemas operativos de nivel inferior se incluyen los siguientes:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, versión 1709 y anteriores

Si la colección de destino contiene dispositivos de nivel superior y de nivel inferior, o si no está seguro, siga las instrucciones para [incorporar dispositivos que ejecuten cualquier sistema operativo compatible](#bkmk_any_os) (recomendado).

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>Obtención del identificador y la clave del área de trabajo para dispositivos de nivel inferior

1. Vaya a el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/) e inicie sesión.
1. Seleccione **Configuración** y después **Incorporación** en el título **Administración de dispositivos**.
1. Para el sistema operativo, seleccione **Windows 7 SP1 y 8.1** o **Windows Server 2008 R2 Sp1, 2012 R2 y 2016** en la lista.
   - La **clave del área de trabajo** y el **id. del área de trabajo** serán iguales, con independencia de las opciones que elija.
1. Copie los valores correspondientes a **Clave del área de trabajo** e **Id. del área de trabajo** de la sección **Configurar conexión**.

### <a name="onboard-the-down-level-devices"></a>Incorporación de los dispositivos de nivel inferior

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** > **Directivas de ATP de Microsoft Defender** y seleccione **Crear directiva de ATP de Microsoft Defender**. Se abre el Asistente para crear directiva de ATP de Microsoft Defender.  
1. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Incorporación**.
1. Proporcione la **clave del área de trabajo** y el **id. del área de trabajo**.
   > [!Note]
   > - Para la versión 2002 de Configuration Manager, necesitará el archivo de configuración incluso si solo va a incorporar dispositivos de nivel inferior. Para obtener estos valores, seleccione **Configuración** > **Incorporación** > **Windows 10** en el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/). <!--7054188--> 
   > - El archivo de configuración de ATP de Microsoft Defender contiene información confidencial que debe mantenerse segura.
1. Especifique los ejemplos de archivos de dispositivos administrados que se recopilan y se comparten para su análisis.  
   - **Ninguno**
   - **Todos los tipos de archivo**  
1. Revise el resumen y finalice el asistente.  
1. Haga clic con el botón derecho en la directiva que ha creado y, después, seleccione **Implementar** para dirigir la directiva de ATP de Microsoft Defender a los clientes.


## <a name="monitor"></a>Supervisión

1. En la consola de Configuration Manager, vaya a **Supervisión** > **Seguridad** y seleccione **ATP de Microsoft Defender**.  

1. Revise el panel de Protección contra amenazas avanzada de Microsoft Defender.  

    - **Estado de incorporación del agente de ATP de Microsoft Defender**: el número y el porcentaje de equipos cliente administrados aptos con directiva de ATP de Microsoft Defender activa incorporados.  

    - **Agent Health para ATP de Microsoft Defender**: porcentaje de equipos cliente que envían informes de estado de su agente de ATP de Microsoft Defender.  

        - **Correcto**: funciona correctamente.  

        - **Inactivo**: no se ha enviado ningún dato al servicio durante el período.  

        - **Estado del agente**: el servicio del sistema del agente en Windows no se está ejecutando  

        - **No incorporado**: la directiva se aplicó, pero el agente no ha notificado la incorporación de la directiva  

## <a name="create-an-offboarding-configuration-file"></a>Creación de un archivo de configuración de retirada  

1. Inicie sesión en el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/).
1. Seleccione **Configuración** y después **Retirada** en el título **Administración de dispositivos**.
1. Seleccione **Windows 10** para el sistema operativo y **Microsoft Endpoint Configuration Manager current branch and later** (Rama actual de Microsoft Endpoint Configuration Manager y posteriores) para el método de implementación.
   - El uso de la opción **Windows 10** garantiza que todos los dispositivos de la colección se retiren y que se desinstale MMA cuando sea necesario.
1. Descargue el archivo comprimido (.zip) y extraiga el contenido. Los archivos de retirada son válidos durante 30 días.

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** > **Directivas de ATP de Microsoft Defender** y seleccione **Crear directiva de ATP de Microsoft Defender**. Se abre el Asistente para crear directiva de ATP de Microsoft Defender.  

1. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Retirada**.

1. **Navegue** al archivo de configuración que ha extraído del archivo .zip descargado.

1. Revise el resumen y finalice el asistente.  

Seleccione **Implementar** para dirigir la directiva de ATP de Microsoft Defender a los clientes.  

> [!IMPORTANT]
> El archivo de configuración de ATP de Microsoft Defender contiene información confidencial que debe mantenerse segura.

## <a name="next-steps"></a>Pasos siguientes

- [Protección contra amenazas avanzada de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Solución de problemas de incorporación de Protección contra amenazas avanzada de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)