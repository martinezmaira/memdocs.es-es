---
title: Configurar actualizaciones de definiciones
titleSuffix: Configuration Manager
description: Aprenda a seleccionar y configurar métodos con Endpoint Protection en Configuration Manager para mantener actualizadas las definiciones de antimalware en los equipos cliente.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697353"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Configuración de actualizaciones de definiciones para Endpoint Protection  

*Se aplica a: Configuration Manager (rama actual)*

 Con Endpoint Protection en Configuration Manager, puede usar cualquiera de los diversos métodos disponibles para mantener las definiciones de antimalware actualizadas en los equipos cliente de la jerarquía. La información de este tema puede ayudarlo a seleccionar y configurar dichos métodos.

 Para actualizar las definiciones de antimalware, puede usar uno o varios de los métodos siguientes:

- [Actualizaciones distribuidas desde Configuration Manager](endpoint-definitions-configmgr.md): este método usa las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones y de motores a los equipos de la jerarquía.

- [Actualizaciones distribuidas desde WSUS (Windows Server Update Services)](endpoint-definitions-wsus.md): este método usa la infraestructura de WSUS para entregar actualizaciones de definiciones y de motores a los equipos.

- [Actualizaciones distribuidas desde Microsoft Update](endpoint-definitions-microsoft-updates.md): este método permite que los equipos se conecten directamente a Microsoft Update para descargar actualizaciones de definiciones y de motores. Este método puede ser útil para los equipos que no suelen conectarse a la red empresarial.

- [Actualizaciones distribuidas desde el Centro de protección contra malware de Microsoft](endpoint-definitions-protection-center.md): este método descarga actualizaciones de definiciones desde el Centro de protección contra malware de Microsoft.

- [Actualizaciones desde recursos compartidos de archivos UNC](endpoint-definitions-network.md): con este método, se pueden guardar las últimas actualizaciones de definiciones y de motores en un recurso compartido en la red. De este modo, los clientes pueden acceder a la red para instalar las actualizaciones.

  Es posible configurar varios orígenes de actualización de definiciones y controlar el orden en el que se accede a ellos y se aplican. Para ello, use el cuadro de diálogo **Configurar orígenes de actualización de definiciones** cuando se cree una directiva antimalware.

> [!IMPORTANT]
>  En el caso de equipos Windows 10, debe configurar Endpoint Protection para actualizar las definiciones de malware de Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Procedimiento para configurar orígenes de actualización de definiciones
 Use el procedimiento siguiente para configurar los orígenes de actualización de definiciones para cada directiva antimalware.

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Endpoint Protection**y haga clic en **Directivas antimalware**.

3.  Abra la página de propiedades de la **Directiva antimalware predeterminada** o cree una nueva. Para más información sobre cómo crear directivas antimalware, consulte [Crear e implementar directivas antimalware para Endpoint Protection](endpoint-antimalware-policies.md).

4.  En la sección **Actualizaciones de inteligencia de seguridad** del cuadro de diálogo de propiedades de antimalware, haga clic en **Establecer origen**.
    - Se ha cambiado el nombre de la sección **Actualizaciones de definiciones** a **Actualizaciones de inteligencia de seguridad** a partir de Configuration Manager versión 1902.

5.  En el cuadro de diálogo **Configurar orígenes de actualización de definiciones** , seleccione los orígenes que se usarán para las actualizaciones de definiciones. Puede hacer clic en **Subir** o **Bajar** para modificar el orden en que se usan estos orígenes.

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar orígenes de actualización de definiciones** .

## <a name="configure-endpoint-protection-definitions"></a>Configurar definiciones de Endpoint Protection

-   [Actualizaciones distribuidas desde Configuration Manager](endpoint-definitions-configmgr.md): este método usa las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones y de motores a los equipos de la jerarquía.

-   [Actualizaciones distribuidas desde WSUS (Windows Server Update Services)](endpoint-definitions-wsus.md): este método usa la infraestructura de WSUS para entregar actualizaciones de definiciones y de motores a los equipos.

-   [Actualizaciones distribuidas desde Microsoft Update](endpoint-definitions-microsoft-updates.md): este método permite que los equipos se conecten directamente a Microsoft Update para descargar actualizaciones de definiciones y de motores. Este método puede ser útil para los equipos que no suelen conectarse a la red empresarial.

-   Actualizaciones distribuidas desde el Centro de protección contra malware de Microsoft: este método descarga actualizaciones de definiciones desde el Centro de protección contra malware de Microsoft.

-   [Actualizaciones desde recursos compartidos de archivos UNC](endpoint-definitions-network.md): con este método, se pueden guardar las últimas actualizaciones de definiciones y de motores en un recurso compartido en la red. De este modo, los clientes pueden acceder a la red para instalar las actualizaciones.
