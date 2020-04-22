---
title: Configuración de la administración de energía
titleSuffix: Configuration Manager
description: Configure la administración de energía en Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696603"
---
# <a name="configure-power-management-in-configuration-manager"></a>Configuración de la administración de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se explica cómo configurar la administración de energía en Configuration Manager.

## <a name="enable-and-configure-client-settings"></a>Habilitación y configuración del cliente

En este procedimiento se establece la *configuración del cliente predeterminada* para la administración de energía. Se aplica a todos los equipos de la jerarquía.

Si solo quiere aplicar esta configuración a algunos clientes, cree una *configuración de cliente de dispositivo personalizada*. Después, asígnela a una recopilación que contenga los equipos para la administración de energía. Para obtener más información, vea [Cómo configurar el cliente](../../deploy/configure-client-settings.md).  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, seleccione el nodo **Configuración de cliente** y después **Configuración de cliente predeterminada**.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.  

1. Seleccione el grupo **Administración de energía**.  

1. Habilite la opción de cliente **Permitir la administración de energía de dispositivos**.

1. Configure las opciones de cliente adicionales que necesite. Para más información, vea [Acerca de la configuración de cliente: Administración de energía](../../deploy/about-client-settings.md#power-management).  

Los clientes configurarán estas opciones la próxima vez que descarguen la directiva de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../manage-clients.md#BKMK_PolicyRetrieval).  

## <a name="exclude-computers"></a>Exclusión de equipos

Puede impedir que las recopilaciones de equipos reciban la configuración de administración de energía. Si un equipo es miembro de *cualquier* recopilación que se excluye de la configuración de administración de energía, ese equipo no aplica la configuración de administración de energía. Este comportamiento se aplica incluso si es miembro de otra recopilación que aplica la configuración de administración de energía.  

Es posible que quiera excluir equipos de la administración de energía por los siguientes motivos:  

- Existe un requisito empresarial de que los equipos estén encendidos en todo momento.  

- Tiene una recopilación de control de equipos en los que no quiere aplicar la configuración de administración de energía.  

- Algunos de los equipos no tienen la capacidad para aplicar la configuración de administración de energía.  

- Quiere excluir los equipos que ejecutan Windows Server de la administración de energía.  

> [!NOTE]  
> Si establece la configuración de cliente en **Permitir a los usuarios excluir su dispositivo de la administración de energía**, los usuarios pueden excluir sus propios equipos de la administración de energía mediante el Centro de software.  

Para averiguar qué equipos se excluyen de la administración de energía, ejecute el informe **Equipos excluidos**. Para más información sobre este informe, vea [Cómo supervisar y planear la administración de energía](monitor-and-plan-for-power-management.md#BKMK_Excluded).  

> [!IMPORTANT]  
> La exclusión de un equipo de la administración de energía hace que toda la configuración de energía revierta a sus valores originales. No puede revertir una configuración de energía individual a sus valores originales.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Procedimientos para excluir una recopilación de equipos de la administración de energía  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**.  

1. Seleccione la recopilación que quiera excluir de la administración de energía. En la pestaña **Inicio** de la cinta, en el grupo **Propiedades**, seleccione **Propiedades**.  

1. Cambie a la pestaña **Administración de energía** y seleccione **No aplicar nunca la configuración de administración de energía en equipos de esta recopilación**.  

## <a name="next-steps"></a>Pasos siguientes

[Cómo crear y aplicar planes de energía](create-and-apply-power-plans.md)

[Cómo supervisar y planear la administración de energía](monitor-and-plan-for-power-management.md)
