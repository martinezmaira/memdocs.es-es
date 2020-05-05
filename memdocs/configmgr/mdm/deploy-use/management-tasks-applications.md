---
title: Administrar aplicaciones para MDM local
titleSuffix: Configuration Manager
description: Administrar aplicaciones para la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724789"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Administrar aplicaciones para MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Cuando administra dispositivos con Configuration Manager la administración de dispositivos móviles (MDM) local, puede administrar los siguientes tipos de aplicaciones:

- Paquete de aplicación de Windows Phone (archivo *.xap)
- Paquete de aplicación de Windows Phone (en la Tienda Windows Phone)
- Windows Installer a través de MDM
- Aplicación web

Para obtener más información general sobre la administración de Configuration Manager Aplicaciones y los tipos de implementación, vea [tareas de administración para aplicaciones de Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Crear Windows Phone aplicación

Una aplicación de Configuration Manager tiene uno o varios tipos de implementación. Los tipos de implementación incluyen los archivos de instalación y la información requerida para implementar software en un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.

Para conocer los pasos generales para crear una aplicación y los tipos de implementación, vea [crear una aplicación](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager admite los siguientes tipos de archivo de aplicación para dispositivos móviles de Windows:

|Tipo de dispositivo|Tipos de archivo admitidos|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8,1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Implemente las aplicaciones de Windows Phone como **Disponible** o **Requerida**. También puede usar las implementaciones para desinstalar las aplicaciones.

## <a name="deploy-and-monitor-apps"></a>Implementación y supervisión de aplicaciones

Implementar y supervisar aplicaciones para dispositivos móviles en Configuration Manager igual que en otros dispositivos, como equipos de escritorio y servidores. Para más información, consulte los siguientes artículos.

- [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md)
- [Supervisar aplicaciones](../../apps/deploy-use/monitor-applications-from-the-console.md)

Revise las siguientes limitaciones específicas de los dispositivos móviles:

- Los dispositivos inscritos en MDM no admiten las implementaciones simuladas, la experiencia del usuario o la configuración de programación.

- No agregue más de 100 configuraciones regionales a una sola aplicación. Esta acción evita que la aplicación se instale en el dispositivo.

## <a name="next-step"></a>Paso siguiente

Para realizar cambios, desinstalar o reemplazar una aplicación implementada por una nueva aplicación, debe administrarla igual que cualquier aplicación en Configuration Manager. Para obtener más información, vea [Actualizar y retirar aplicaciones](../../apps/deploy-use/update-and-retire-applications.md).
