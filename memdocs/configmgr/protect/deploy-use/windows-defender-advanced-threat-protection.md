---
title: Protección contra amenazas avanzada de Microsoft Defender
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar y supervisar Protección contra amenazas avanzada de Microsoft Defender, un nuevo servicio que ayuda a las empresas a responder ante ataques sofisticados.
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a635ae36875984537c18c4850a3526d57ffceb31
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210152"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Microsoft Defender

*Se aplica a: Configuration Manager (rama actual)*

Endpoint Protection puede ayudar a administrar y supervisar [Protección contra amenazas avanzada (ATP) de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (anteriormente conocido como ATP de Windows Defender). ATP de Microsoft Defender ayuda a las empresas a detectar e investigar ataques avanzados en sus redes, y responder ante ellos. Las directivas de Configuration Manager pueden ayudarlo a incorporar y supervisar clientes de Windows 10.

ATP de Microsoft Defender es un servicio del [Centro de seguridad avanzada de Windows Defender](https://securitycenter.windows.com). Al agregar e implementar un archivo de configuración de incorporación de cliente, Configuration Manager puede supervisar el estado de implementación y el mantenimiento del agente de ATP de Microsoft Defender. ATP de Microsoft Defender es compatible con equipos que ejecutan el cliente de Configuration Manager o que se [administran mediante Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

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
- Windows 7 SP1
- Windows 8.1
- Windows 10, versión 1607 o posterior
- Windows Server 2008 R2 SP1
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, versión 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Creación de un archivo de configuración de incorporación

1. Vaya a el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/) e inicie sesión.
1. Seleccione **Administración de máquinas** en **Configuración** y, a continuación, seleccione **Incorporación**.
1. Seleccione los sistemas operativos de la lista que le gustaría incorporar.
   - Si incorpora Windows 10, Windows Server 1803 y Windows Server 2019:
      1. Seleccione **Configuration Manager (rama actual), versión 1606** y **Descargar paquete**.
      1. Descargue el archivo comprimido (.zip) y extraiga el contenido.
   - Si incorpora otro sistema operativo Windows: 
      1. Seleccione los sistemas operativos de la lista que le gustaría incorporar. Por ejemplo, seleccione **Windows 7 y 8.1**, o bien **Windows Server 2008 R2 SP1, 2012 R2 y 2016**.
      1. Copie los valores correspondientes a **Clave del área de trabajo** e **Id. del área de trabajo** de la sección **Configurar conexión** una vez que se complete el proceso.

> [!IMPORTANT]
> - El archivo de configuración de ATP de Microsoft Defender contiene información confidencial que debe mantenerse segura.

## <a name="onboard-devices"></a>Incorporación de dispositivos

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** > **Directivas de ATP de Windows Defender** y seleccione **Crear directiva de ATP de Windows Defender**. Se abre el Asistente para crear directiva de ATP de Microsoft Defender.  
1. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Incorporación**.
1. **Vaya** al archivo de configuración proporcionado por el espacio empresarial del servicio ATP de Microsoft Defender en la nube de la organización.
   - Para **Windows 7 y 8.1** o **Windows Server 2008 R2 SP1, 2012 R2 y 2016**, indique la **clave del área de trabajo** y el **identificador del área de trabajo**.
   - Para la versión 2002 de Configuration Manager, necesitará la **Clave del área de trabajo** y el **Id. del área de trabajo** incluso si solo va a incorporar dispositivos Windows Server 2019 y Windows Server 1803 o posteriores. Para obtener estos valores, seleccione **Configuración** > **Incorporación** > **Windows 7 y 8.1** en el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/). <!--7054188-->
1. Especifique los ejemplos de archivos de dispositivos administrados que se recopilan y se comparten para su análisis.  

   - **Ninguno**

   - **Todos los tipos de archivo**  
1. Revise el resumen y finalice el asistente.  

Seleccione **Implementar** para dirigir la directiva de ATP de Microsoft Defender a los clientes.

## <a name="monitor"></a>Supervisión

1. En la consola de Configuration Manager, vaya a **Supervisión** > **Seguridad** y seleccione **ATP de Windows Defender**.  

1. Revise el panel de Protección contra amenazas avanzada de Microsoft Defender.  

    - **Estado de implementación del agente de Windows Defender**: el número y el porcentaje de equipos cliente administrados aptos con directiva de ATP de Microsoft Defender activa incorporados.  

    - **Agent Health para ATP de Windows Defender**: porcentaje de equipos cliente que envían informes de estado de su agente de ATP de Microsoft Defender.  

        - **Correcto**: funciona correctamente.  

        - **Inactivo**: no se ha enviado ningún dato al servicio durante el período.  

        - **Estado del agente**: el servicio del sistema del agente en Windows no se está ejecutando  

        - **No incorporado**: la directiva se aplicó, pero el agente no ha notificado la incorporación de la directiva  

## <a name="create-an-offboarding-configuration-file"></a>Creación de un archivo de configuración de retirada  

1. Inicie sesión en el [servicio en línea ATP de Microsoft Defender](https://securitycenter.windows.com/).

1. Seleccione **Administración de máquinas** en **Configuración** y, a continuación, seleccione **Incorporación**.  

1. Seleccione **Configuration Manager (rama actual), versión 1606** y, luego, seleccione **Retirada de punto de conexión**.  

1. Descargue el archivo comprimido (.zip) y extraiga el contenido. Los archivos de retirada son válidos durante 30 días.

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** > **Directivas de ATP de Windows Defender** y seleccione **Crear directiva de ATP de Windows Defender**. Se abre el Asistente para crear directiva de ATP de Microsoft Defender.  

1. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Retirada**.

1. **Vaya** al archivo de configuración proporcionado por el espacio empresarial del servicio ATP de Microsoft Defender en la nube de la organización.

1. Revise el resumen y finalice el asistente.  

Seleccione **Implementar** para dirigir la directiva de ATP de Microsoft Defender a los clientes.  

> [!IMPORTANT]
> El archivo de configuración de ATP de Microsoft Defender contiene información confidencial que debe mantenerse segura.

## <a name="next-steps"></a>Pasos siguientes

- [Protección contra amenazas avanzada de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Solución de problemas de incorporación de Protección contra amenazas avanzada de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
