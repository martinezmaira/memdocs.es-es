---
title: Actualización del canal de mantenimiento a largo plazo a la rama actual
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo convertir un sitio de canal de mantenimiento a largo plazo (LTSB) en un sitio de rama actual.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707233"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Actualizar la rama de mantenimiento a largo plazo a la rama actual

*Se aplica a: System Center Configuration Manager (Rama de mantenimiento a largo plazo)*

Use este tema para aprender a actualizar (convertir) un sitio y la jerarquía que ejecuta la rama mantenimiento a largo plazo (LTSB) de Configuration Manager a la rama actual.

Si cuenta con un acuerdo Software Assurance actual (o derechos de licencia similares) que le concede derechos de uso de la rama actual, puede convertir la instalación de la LTSB a la rama actual.  Esta es una conversión unidireccional, ya que no se puede convertir un sitio de Rama actual a la LTSB.

Si tiene varios sitios, basta con convertir el sitio de nivel superior de la jerarquía. Una vez convertido el sitio de nivel superior:
- Se convierten automáticamente los sitios primarios secundarios.
- Debe actualizar manualmente los sitios secundarios desde la consola de Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Ejecutar el programa de instalación para convertir la Rama de mantenimiento a largo plazo
En el sitio de nivel superior de la jerarquía puede ejecutar el programa de instalación de Configuration Manager desde el medio de línea base correspondiente y seleccionar **Mantenimiento del sitio**.  Después, cuando aparezca la página de licencias, seleccione la opción de la Rama actual y complete el asistente.

Después de convertir el sitio a la Rama actual, podrán usarse las funciones y características que antes no estaban disponibles.

> [!NOTE]  
> El medio de línea base aplicable es un medio que tiene una versión igual o posterior a la instalación de LTSB.

Por ejemplo, dado que la LTSB se basa en la versión 1606, no puede usar el medio 1511 de línea base para convertir a la rama actual. En su lugar, ejecute el programa de instalación desde el mismo medio de línea base de la versión 1606 usado para instalar el sitio de LTSB y seleccione la opción de licencia de la Rama actual.  Como alternativa, si se ha publicado una línea base posterior de la Rama actual, puede ejecutar el programa de instalación desde ese medio de línea base.

Para obtener una lista de las versiones de línea base, vea **Baseline and update versions** (Versiones de línea base y actualización) en [Updates for System Center Configuration Manager](../servers/manage/updates.md) (Actualizaciones para System Center Configuration Manager).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Usar la consola de Configuration Manager para convertir la rama de mantenimiento a largo plazo
Si el sitio ejecuta la LTSB, puede usar la siguiente opción de la consola de Configuration Manager para convertir a la rama actual:

 1. En la consola, vaya a **Administración** > **Configuración del sitio** > **Sitios** y, después, abra **Configuración de jerarquía**.  

 2. En **Configuración de jerarquía**, cambie a la pestaña **Licencias**. Seleccione la opción **Convertir a la rama actual** y, después, haga clic en **Aplicar**.  

Después de convertir el sitio a la Rama actual, podrán usarse las funciones y características que antes no estaban disponibles.
