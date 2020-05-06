---
title: Inscripción de dispositivos en Análisis de escritorio
titleSuffix: Configuration Manager
description: Aprenda a inscribir dispositivos en Análisis de escritorio.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9cca066d389ea8d3847737651f4994977a5e2f5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708173"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Inscripción de dispositivos en Análisis de escritorio

Al [conectar Configuration Manager](connect-configmgr.md) a Análisis de escritorio, configurará los valores para inscribir dispositivos en Análisis de escritorio. Puede cambiar estos valores en cualquier momento. Asegúrese también de que los dispositivos estén actualizados.

## <a name="update-devices"></a>Actualización de los dispositivos

Análisis de escritorio usa dos componentes principales de Windows:

- **Componente de compatibilidad**: el componente de compatibilidad (**evaluador**) ejecuta diagnósticos en el dispositivo Windows para evaluar su estado de compatibilidad con las versiones más recientes de Windows 10.

- **Servicio Experiencias del usuario y telemetría asociadas**: con los datos de diagnóstico de Windows habilitados, el servicio Experiencias del usuario y telemetría asociadas (**DiagTrack**) recopila datos del sistema, de las aplicaciones y de los controladores. Microsoft analiza estos datos y los comparte con usted a través de Análisis de escritorio.

Instale la versión más reciente de estos componentes para obtener la mejor experiencia con el Análisis de escritorio.

En la tabla siguiente se enumeran las actualizaciones de cada componente en las versiones de sistema operativo admitidas:

| Versión del sistema operativo | Evaluador | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | Incluido<sup>[Nota 1](#bkmk_note1)</sup> | [Actualización acumulativa más reciente](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | Incluido | [Actualización acumulativa más reciente](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | Incluido | [Actualización acumulativa más reciente](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | Incluido | [Actualización acumulativa más reciente](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | Incluido | [Actualización acumulativa más reciente](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup>[Nota 2](#bkmk_note2)</sup> | [Paquete acumulativo mensual más reciente](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup>[Nota 3](#bkmk_note3)</sup> | [Paquete acumulativo mensual más reciente](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Use Configuration Manager para instalar automáticamente estas actualizaciones. Para obtener más información, consulte [Deploy software updates](../sum/deploy-use/deploy-software-updates.md) (Implementación de actualizaciones de software).
>
> Reinicie los dispositivos después de instalar las actualizaciones de compatibilidad por primera vez.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a> Nota 1: Windows 10

Aunque Windows 10 incluye estos componentes de forma predeterminada, los dispositivos Windows 10 requieren la actualización acumulativa más reciente para obtener todas las funcionalidades de Análisis de escritorio. Por ejemplo, para evaluar la compatibilidad del dispositivo con la versión más reciente del sistema operativo y obtener información casi en tiempo real de las implementaciones y el estado de inscripción.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a> Nota 2: Windows 8.1

Microsoft incrementa regularmente las actualizaciones de este componente, pero el número de KB asociado no cambia. Asegúrese de tener siempre la versión más reciente de la actualización.

Este componente ejecuta diagnósticos en los sistemas Windows 8.1 que participan en el Programa para la mejora de la experiencia del usuario de Windows. Estos diagnósticos ayudan a determinar si podría tener problemas de compatibilidad al actualizar a Windows 10.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a> Nota 3: Windows 7

Si su organización no aplica las actualizaciones del "Paquete acumulativo de calidad mensual" a los dispositivos de Windows 7 y solo aplica las actualizaciones de "Solo seguridad", encontrará algunas actualizaciones de este tipo en la [lista de actualizaciones que reemplazan a KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c). Puede instalar estas actualizaciones más recientes en lugar de KB 2952664.

> [!NOTE]
> Para Windows 8.1, Microsoft solo revisa KB 2976978 como parte de las actualizaciones del "Paquete acumulativo de calidad mensual".

## <a name="device-enrollment"></a>Inscripción de dispositivos

El servicio Análisis de escritorio no tiene agentes para instalar. La inscripción de dispositivos requiere la configuración de opciones en los dispositivos que quiera supervisar. Estas opciones controlan a qué instancia de Análisis de escritorio el dispositivo debe enviar sus datos y otras opciones de configuración.

> [!Note]  
> Si anteriormente ha usado Windows Analytics, utilice esa misma área de trabajo para Análisis de escritorio. Deberá volver a inscribir en Análisis de escritorio los dispositivos que inscribió anteriormente en Windows Analytics.
>
> Solo puede tener un área de trabajo de Análisis de escritorio por inquilino de Azure AD. Los dispositivos solo pueden enviar datos de diagnóstico a un área de trabajo.  

Configuration Manager proporciona una experiencia integrada para administrar e implementar esta configuración en los clientes. Para obtener la mejor experiencia, use Configuration Manager.

Al conectar Configuration Manager a Análisis de escritorio, configure los valores para inscribir dispositivos. Para más información, consulte [Conexión de Configuration Manager con Análisis de escritorio](connect-configmgr.md#bkmk_connect).

Para cambiar esta configuración, use el procedimiento siguiente:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione la conexión a Análisis de escritorio y elija **Propiedades** en la cinta de opciones.

2. En la página **Datos de diagnóstico**, realice los cambios necesarios en los valores de configuración siguientes:  

    - **Id. comercial**: este valor se debe rellenar automáticamente con el identificador de la organización. Si no es así, asegúrese de que el servidor proxy esté configurado para permitir todos los [puntos de conexión](enable-data-sharing.md#endpoints) necesarios antes de continuar. También puede recuperar el identificador comercial manualmente desde el [portal de Análisis de escritorio](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Nivel de datos de diagnóstico de Windows 10**: para más información, consulte [Niveles de datos de diagnóstico](enable-data-sharing.md#diagnostic-data-levels).  

    - **Permitir nombre del dispositivo en los datos de diagnóstico**: para más información, consulte [Nombre del dispositivo](#device-name).  

    Cuando se realizan cambios en esta página, la página **Funcionalidad disponible** muestra una vista previa de la funcionalidad de Análisis de escritorio con la configuración de datos de diagnóstico seleccionada.  

3. En la página **Conexión con Análisis de escritorio**, realice los cambios necesarios para los siguientes valores:

    - **Nombre para mostrar**: el portal de Análisis de escritorio muestra esta conexión de Configuration Manager con este nombre.  

    - **Recopilación de destino**: esta recopilación incluye todos los dispositivos que configura Configuration Manager con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que conecta Configuration Manager al servicio Análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usan un proxy autenticado por el usuario para las comunicaciones salientes**: de forma predeterminada, este valor es **No**. Si es necesario en su entorno, establézcalo en **Sí**. Para más información, consulte [Compatibilidad del servidor proxy](enable-data-sharing.md#proxy-server-authentication).

    - **Seleccione recopilaciones específicas para sincronizarlas con Análisis de escritorio**: seleccione **Agregar** para incluir recopilaciones adicionales de la jerarquía **Recopilación de destino**. Estas recopilaciones están disponibles en el portal de Análisis de escritorio para agruparlas con los planes de implementación. Asegúrese de incluir recopilaciones piloto y de exclusión piloto.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Estas recopilaciones se siguen sincronizando a medida que cambia su pertenencia. Por ejemplo, el plan de implementación usa una recopilación con una regla de pertenencia de Windows 7. A medida que esos dispositivos se actualizan a Windows 10 y Configuration Manager evalúa la pertenencia de la recopilación, dichos dispositivos abandonan la colección y el plan de implementación.

### <a name="windows-settings"></a>Configuración de Windows

Cuando Configuration Manager inscribe dispositivos en Análisis de escritorio, establece directivas de Windows destinadas a configurar el dispositivo para Análisis de escritorio. En la mayoría de los casos, use solo Configuration Manager para definir estos valores. No aplique también esta configuración en los objetos de directiva de grupo de dominio.

Para obtener más información, consulte [Configuración de directiva de grupo para Análisis de escritorio](group-policy-settings.md).

### <a name="device-name"></a>Nombre del dispositivo

A partir de la versión 1803 de Windows 10, el nombre del dispositivo ya no se recopila de forma predeterminada. Para recopilar el nombre del dispositivo con los datos de diagnóstico, se necesita una suscripción independiente. Sin el nombre del dispositivo, es más difícil identificar los dispositivos que requieren atención al evaluar una actualización a una nueva versión de Windows.

Si no envía el nombre del dispositivo, aparece en Análisis de escritorio como "desconocido":

![Lista de dispositivos de Análisis de escritorio que muestra nombres "desconocidos"](media/unknown-device-name.png)

Hay una opción en la configuración de Configuration Manager para Análisis de escritorio para configurar esta opción: **Permitir nombre del dispositivo en los datos de diagnóstico**. Este valor de Configuration Manager controla la [configuración de directiva de Windows](group-policy-settings.md), **AllowDeviceNameInTelemetry**.

### <a name="conflict-resolution"></a>Resolución de conflictos

En general, use recopilaciones de Configuration Manager como destino para la configuración y la inscripción de Análisis de escritorio. Use la pertenencia directa o las consultas para incluir o excluir dispositivos de la recopilación. Para obtener más información, vea [Creación de recopilaciones](../core/clients/manage/collections/create-collections.md).

Configuration Manager solo configura las opciones de Windows si aún no existe un valor. Si necesita configurar diferentes valores para un grupo de dispositivos único, puede usar [directiva de grupo](group-policy-settings.md). La configuración de destino de directiva de grupo tiene prioridad sobre la configuración de Configuration Manager.

Al configurar el nivel de datos de diagnóstico, se establece el límite superior para el dispositivo. De forma predeterminada, en la versión 1803 y posterior de Windows 10, los usuarios pueden elegir establecer un nivel inferior. Para controlar este comportamiento, use la configuración de directiva de grupo **Configure telemetry opt-in setting user interface** (Configurar la interfaz de usuario de establecimiento de participación en la telemetría). Para obtener más información, consulte [Configuración de directiva de grupo para Análisis de escritorio](group-policy-settings.md).

### <a name="proxy-settings"></a>Configuración del proxy

Si su organización usa la autenticación de servidor proxy para el acceso a Internet, asegúrese de configurar correctamente la autenticación o los dispositivos. Para más información, consulte [Compatibilidad del servidor proxy](enable-data-sharing.md#proxy-server-authentication).

## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para crear planes de implementación en Análisis de escritorio.
> [!div class="nextstepaction"]
> [Creación de planes de implementación](create-deployment-plans.md)
