---
title: Planeamiento de Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2c733ef03482ddfc1f3e6502d7f5fe8ae0d20b76
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590514"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Planificación de Endpoint Protection en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


Endpoint Protection en Configuration Manager permite administrar directivas antimalware y la seguridad del Firewall de Windows en equipos cliente de la jerarquía de Configuration Manager.  

> [!IMPORTANT]  
>  Debe tener una licencia para usar Endpoint Protection para administrar clientes en su jerarquía de Configuration Manager.  

Si usa Endpoint Protection con Configuration Manager, disfrutará de las siguientes ventajas:  

-   Configuración de directivas antimalware, configuración del Firewall de Windows y administración de Protección contra amenazas avanzada de Microsoft Defender en grupos de equipos seleccionados  

-   Uso de las actualizaciones de software de Configuration Manager para descargar los archivos de definición de antimalware más recientes a fin de mantener actualizados los equipos cliente  

-   Envíe notificaciones de correo electrónico, use la supervisión en la consola y vea informes para mantener a los usuarios administrativos informados cuando se detecte malware en los equipos cliente.  

Los equipos Windows 10 no requieren ningún cliente adicional para la administración de Endpoint Protection. En Windows 8.1 y versiones anteriores, Endpoint Protection instala a su propio cliente además del cliente de Configuration Manager. El cliente de Endpoint Protection tiene las siguientes capacidades:  

-   Detección y corrección de malware y spyware  

-   Detección y corrección de rootkit  

-   Evaluación y definición automática de vulnerabilidades críticas y actualizaciones del motor  

-   Detección de vulnerabilidades de red a través del Sistema de inspección de red  

-   Integración con Cloud Protection Service para informar a Microsoft sobre malware. Cuando se une a este servicio, Windows Defender o el cliente de Endpoint Protection pueden descargar las definiciones más recientes desde el Centro de protección contra malware cuando se detecta malware no identificado en un equipo.  

> [!NOTE]  
>  El cliente de Endpoint Protection se puede instalar en un servidor que ejecute Hyper-V y en máquinas virtuales invitadas con sistemas operativos compatibles. Para evitar el uso excesivo de la CPU, las acciones de Endpoint Protection tienen un retraso aleatorio integrado para que los servicios no se ejecuten simultáneamente.  

  Además, Endpoint Protection en Configuration Manager le permite administrar la configuración del Firewall de Windows en la consola de Configuration Manager.  

 [Escenario de ejemplo: uso de System Center Endpoint Protection para proteger los equipos frente al malware](../deploy-use/scenarios-endpoint-protection.md): se muestra cómo podría configurar y administrar Endpoint Protection y el Firewall de Windows.  

## <a name="managing-malware-with-endpoint-protection"></a>Administración de malware con Endpoint Protection  

Endpoint Protection en Configuration Manager permite crear directivas antimalware que contengan opciones de configuración de cliente de Endpoint Protection. Después, puede implementar estas directivas antimalware en los equipos cliente y supervisarlos en el nodo **Estado de Endpoint Protection** en el área de trabajo **Supervisión** o mediante informes de Configuration Manager.  

 Información adicional:  

-   [Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager](../deploy-use/endpoint-antimalware-policies.md): cree, implemente y supervise directivas antimalware con una lista de los valores que puede configurar.  

-   [Supervisar Endpoint Protection](../deploy-use/monitor-endpoint-protection.md): supervisión de informes de actividad, equipos cliente infectados, etc.   

-   [Administrar directivas antimalware y opciones de configuración de firewall](../deploy-use/endpoint-antimalware-firewall.md): puede cambiar la prioridad de directiva de [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) o [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [corregir el malware que se encuentre en los equipos cliente](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware) y otras tareas.

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Administración del Firewall de Windows con Endpoint Protection  
 Endpoint Protection en Configuration Manager proporciona administración básica del Firewall de Windows en los equipos cliente. Para cada perfil de red, puede configurar las siguientes opciones:  

-   Habilitar o deshabilitar el Firewall de Windows.  

-   Bloquear todas las conexiones entrantes, incluidas las de la lista de programas permitidos.  

-   Notificar al usuario cuando el Firewall de Windows bloquee un nuevo programa.  

> [!NOTE]  
>  Endpoint Protection es compatible solo con la administración del Firewall de Windows.  

  Para más información sobre cómo crear e implementar las directivas del Firewall de Windows para Endpoint Protection, consulte [Crear e implementar directivas de Firewall de Windows para Endpoint Protection en System Center Configuration Manager](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Microsoft Defender

A partir de la versión 1606 de Configuration Manager (rama actual), Endpoint Protection puede ayudar a administrar y supervisar Protección contra amenazas avanzada (ATP) de Microsoft Defender, anteriormente conocido como ATP de Windows Defender. ATP de Microsoft Defender es un servicio que ayuda a las empresas a detectar ataques avanzados en sus redes, a investigarlos y a responder a ellos. Vea [Protección contra amenazas avanzada de Microsoft Defender](../deploy-use/defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flujo de trabajo de Endpoint Protection  
 Use el siguiente diagrama para entender mejor el flujo de trabajo para implementar Endpoint Protection en su jerarquía de Configuration Manager.  

 ![Flujo de trabajo de Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente de Endpoint Protection para equipos Mac y servidores Linux  
 System Center incluye un cliente de Endpoint Protection para Linux y para equipos Mac. A estos clientes no se les suministra Configuration Manager, por lo que debe descargar los siguientes productos del [Centro de servicios de licencias por volumen de Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Debe ser un cliente de licencia por volumen de Microsoft para descargar los archivos de instalación de Endpoint Protection para Linux y Mac.  

 Estos productos no se pueden administrar desde la consola de Configuration Manager. Sin embargo, se suministra un módulo de administración de System Center Operations Manager con los archivos de instalación, que permite administrar el cliente para Linux mediante Operations Manager.  

 Para más información acerca de cómo instalar y administrar los clientes de Endpoint Protection para equipos Linux y equipos Mac, use la documentación que acompaña a estos productos, que se encuentra en la carpeta **Documentation** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Procedimientos recomendados para Endpoint Protection en Configuration Manager  
 Use los procedimientos recomendados siguientes para Endpoint Protection en System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Establecer una configuración de cliente personalizada para Endpoint Protection  
 Al configurar el cliente para Endpoint Protection no use la configuración predeterminada del cliente, ya que se aplica la configuración a todos los equipos de la jerarquía. En su lugar, configuración personalizada y asignar a estos valores a colecciones de equipos de la jerarquía.  

 Al configurar el cliente personalizado, puede hacer lo siguiente:  

-   Personalizar la configuración de seguridad y antimalware para las distintas partes de su organización.  
-   Probar los efectos de ejecutar Endpoint Protection en un pequeño grupo de equipos antes de implementarlo en toda la jerarquía.  
-   Agregar más clientes a la colección con el tiempo a la fase de la implementación del cliente de Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribución de actualizaciones de definiciones mediante el uso de las actualizaciones de software  
 Si está usando las actualizaciones de software de Configuration Manager para distribuir las actualizaciones de definiciones, considere colocar las actualizaciones de definiciones en un paquete que no contenga otras actualizaciones de software. Esto evita que el tamaño del paquete de actualización de definición más pequeño que permite que se replique en puntos de distribución más rápidamente.
