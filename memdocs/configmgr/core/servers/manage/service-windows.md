---
title: Ventanas de servicio
titleSuffix: Configuration Manager
description: Use las ventanas de servicio para controlar cuándo los sitios de Configuration Manager instalan actualizaciones.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702053"
---
#  <a name="service-windows-for-site-servers"></a>Ventanas de servicio para servidores de sitio

*Se aplica a: Configuration Manager (rama actual)*

Puede configurar ventanas de servicio en sitios de administración central y sitios principales para controlar cuándo se pueden instalar las actualizaciones en la consola.  Puede configurar varias ventanas, con la ventana permitida para la instalación de actualizaciones determinada por una combinación de todas las ventanas de servicio para ese servidor del sitio.

Cuándo no se configura una ventana de servicio:
- **En el sitio de nivel superior** (un sitio de administración central o sitio primario independiente), elige cuándo iniciar la instalación de la actualización.
- **En un sitio secundario**, la actualización se instala automáticamente después de que la actualización complete la instalación en el sitio de administración central.
- **En un sitio secundario**, las actualizaciones nunca se inician automáticamente. En su lugar, debe iniciar manualmente la instalación de la actualización desde dentro de la consola, después de que el sitio primario principal haya instalado la actualización.

Cuándo se configura una ventana de servicio:
- **En el sitio de nivel superior**, no podrá iniciar la instalación de una nueva actualización desde dentro de la consola de Configuration Manager. Incluso con una ventana de servicio configurada, el sitio descarga automáticamente actualizaciones para que estén preparadas para instalarse.  
- **En un sitio primario secundario**, las actualizaciones instaladas en un sitio de administración central se descargan en el sitio primario, pero no se inician automáticamente. No puede iniciar manualmente la instalación de una actualización en el momento que se bloquea mediante el uso de una ventana de servicio. En el momento en el que las ventanas de servicio dejan de bloquear la instalación de la actualización, se inicia automáticamente la instalación de la actualización.
- Los **sitios secundarios** no son compatibles con las ventanas de servicio y no instalan actualizaciones automáticamente. Después de que el sitio primario principal de un sitio secundario instale una actualización, puede iniciar la actualización del sitio secundario desde dentro de la consola.

## <a name="to-configure-a-service-window"></a>Para configurar una ventana de servicio

1.  En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio** > **Sitios** y seleccione el servidor de sitio en el que quiere configurar un periodo para tareas administrativas.  

2.  A continuación, modifique las **Propiedades** de los servidores de sitio y seleccione la pestaña **Ventana de servicio** , donde puede establecer una o varias ventanas de servicio para ese servidor de sitio.  
