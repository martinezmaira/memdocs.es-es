---
title: Cliente de interoperabilidad extendida
titleSuffix: Configuration Manager
description: Obtenga información sobre el uso del cliente de interoperabilidad extendida para el soporte técnico a largo plazo de un cliente de Configuration Manager estático con un sitio de rama actual.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706983"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Uso del software cliente de Configuration Manager para obtener una interoperabilidad extendida con futuras versiones de un sitio de la Rama actual

*Se aplica a: Configuration Manager (rama actual)*  

Los requisitos empresariales podrían no permitir realizar actualizaciones regulares del cliente de Configuration Manager en algunos dispositivos. Por ejemplo, debe seguir las directivas de administración de cambios, o el dispositivo es de vital importancia. Satisfaga estas necesidades mediante la instalación de un nuevo cliente para uso a largo plazo, denominado cliente de interoperabilidad extendida (EIC). Use el EIC solo para dispositivos específicos que no se puedan actualizar con frecuencia, como dispositivos de pantalla completa o de punto de venta. Siga usando [actualizaciones de cliente automáticas](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) para la mayoría de los clientes.

## <a name="how-it-works"></a>Cómo funciona

Normalmente, cuando instala una nueva [actualización en la consola](../servers/manage/install-in-console-updates.md) para Configuration Manager, los clientes actualizan automáticamente su software cliente de manera que puedan usar esas características nuevas. Con este escenario, se sigue actualizando la rama actual con la recepción de nuevas características y actualizaciones. La mayoría de los dispositivos actualiza el software cliente de Configuration Manager con cada actualización de versión que se instala. En cambio, en un subconjunto de sistemas críticos que no quiere que reciban actualizaciones de software cliente, instalará el cliente de interoperabilidad extendida. Estos clientes no instalan nuevo software cliente hasta que se implementa explícitamente una nueva versión del software cliente para ellos.

## <a name="supported-versions"></a>Versiones admitidas

En la tabla siguiente se enumeran las versiones del cliente de Configuration Manager admitidas para este escenario:

| Version | Fecha de disponibilidad | Fecha de finalización del soporte técnico |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27 de marzo de 2019 | No antes del 27 de mayo de 2021 |
| 1802<br/>5.00.8634 | 1 de mayo de 2018 | No antes del 1 de mayo de 2020 |
| 1606<br/>5.00.8412 | 18 de noviembre de 2016 | 1 de mayo de 2019 |

> [!TIP]  
> El EIC recibe soporte durante al menos dos años a partir de la fecha de lanzamiento. Para más información sobre las fechas de lanzamiento, consulte [Compatibilidad con versiones de la rama actual de Configuration Manager](../servers/manage/current-branch-versions-supported.md).  

Planee la actualización del cliente de interoperabilidad extendida en dispositivos que administre con la rama actual antes de que expire el soporte para el cliente. Para ello, descargue una versión nueva del cliente de Microsoft y, después, implemente ese software cliente actualizado en los dispositivos que usen el cliente de interoperabilidad extendida actual.

## <a name="how-to-use-the-eic"></a>Cómo usar el EIC

1. Agregue estos dispositivos a una colección y excluya esa colección de las actualizaciones automáticas de cliente. Para obtener más información, consulte [Cómo excluir la actualización de clientes](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Obtenga una versión compatible del EIC desde la carpeta `\SMSSETUP\Client` de los soportes de instalación de actualización de Configuration Manager. Asegúrese de copiar todo el contenido de la carpeta.  

    > [!TIP]  
    > Para buscar el medio de Configuration Manager en el [Centro de servicios de licencias por volumen](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), vaya a la pestaña **Downloads and Keys** (Descargas y claves), busque `System Center Config` y, después, seleccione **System Center Config Mgr (rama actual)** .

1. Instale manualmente el EIC en dichos dispositivos. Para obtener más información, vea [Manually install the client](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) (Instalar el cliente de forma manual).  

    > [!Important]  
    > Al actualizar los clientes de la versión 1606 a la versión 1802, use la opción de CCMSETUP **/AlwaysExcludeUpgrade:True**. De lo contrario, el cliente puede recibir la directiva del punto de administración de actualizar automáticamente antes de la directiva de exclusión.  

## <a name="limitations"></a>Limitaciones

- Las actualizaciones del software cliente de interoperabilidad extendida no están disponibles mediante actualizaciones en consola. Para obtener más información sobre cómo actualizar el EIC, consulte [Cómo actualizar un cliente que está en una colección excluida](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- El EIC solo admite las siguientes características:  

  - Actualizaciones de software  
  - Inventario de hardware y software
  - Paquetes y programas

## <a name="next-steps"></a>Pasos siguientes

[Cómo excluir la actualización de clientes](../clients/manage/upgrade/exclude-clients-windows.md)

Para garantizar que los clientes se instalen correctamente en los dispositivos deseados, consulte [Supervisión de clientes](../clients/manage/monitor-clients.md).
