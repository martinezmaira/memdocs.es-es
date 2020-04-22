---
title: Instalación de aplicaciones para un dispositivo
titleSuffix: Configuration Manager
description: Use Configuration Manager para instalar inmediatamente una aplicación en un dispositivo sin una recopilación.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689453"
---
# <a name="install-applications-for-a-device"></a>Instalación de aplicaciones para un dispositivo

<!--4402180-->

A partir de la versión 1906, desde la consola de Configuration Manager, puede instalar aplicaciones en un dispositivo en tiempo real. Esta característica puede ayudar a reducir la necesidad de colecciones independientes para cada aplicación.

## <a name="prerequisites"></a>Requisitos previos

- Habilite la [característica opcional](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Aprobar solicitudes de aplicación de usuarios por dispositivo**.  

- [Implemente la aplicación](deploy-applications.md) como *Disponible* en una colección de dispositivos.  

    - En la página **Configuración de implementación** del asistente de implementación, especifique la opción siguiente: **Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo**.  

        > [!Note]  
        > Con esta configuración de implementación, no se envía ninguna directiva al cliente. La aplicación no se muestra como disponible en el centro de software y un usuario no puede instalar la aplicación con esta implementación. Después de usar esta acción para instalar la aplicación, el usuario puede ejecutarla y ver su estado de instalación en el Centro de software.

- La cuenta de usuario necesita los permisos siguientes:

    - **Aplicación**: Lectura, Aprobación

    - **Recopilación**: Lectura, Lectura de recursos, Modificar recurso, Ver archivo recopilado

    Por ejemplo, el rol integrado **Administrador de aplicaciones** tiene estos permisos.

> [!TIP]
> En una jerarquía, espere a que la aplicación y la información de implementación se repliquen en el sitio primario al que se asigna el cliente de destino.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Proceso

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**. Seleccione el dispositivo de destino y después la acción **Instalar aplicación** en la cinta.

1. Seleccione una o varias aplicaciones de la lista. En la lista solo se muestran las aplicaciones que ya ha implementado con la configuración de requisitos previos.

Esta acción desencadena la instalación en el dispositivo de las aplicaciones previamente implementadas seleccionadas.

Para ver el estado de la aprobación de aplicación, en el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Solicitudes de aplicación**.

Supervise la instalación de la aplicación de la forma habitual en el nodo **Implementaciones** del área de trabajo **Supervisión**.


## <a name="see-also"></a>Vea también

[Aprobar aplicaciones](app-approval.md)
