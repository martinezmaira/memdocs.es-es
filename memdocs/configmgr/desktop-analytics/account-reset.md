---
title: Restablecimiento de la cuenta
titleSuffix: Configuration Manager
description: Aprenda a restablecer la cuenta de Análisis de escritorio.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ece2d2725b8485f55fdce7761098577485bc2d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706573"
---
# <a name="how-to-reset-your-account"></a>Restablecimiento de la cuenta

<!-- 3733897 -->

Si configuró Análisis de escritorio en el entorno, pero desea empezar de nuevo con la incorporación y la inscripción, use este proceso para restablecer la cuenta.

## <a name="prerequisites"></a>Requisitos previos

Solo un **administrador global** puede restablecer la cuenta en Azure Portal.

## <a name="behaviors"></a>Comportamientos

- Este proceso no cambia ningún usuario, aplicación o permiso existentes Azure AD

- Si decide agregar una nueva área de trabajo, no se conserva ninguna de las siguientes entradas de usuario en los recursos:
    - Importancia
    - Propietario
    - Decisión de actualización
    - Notas de corrección

## <a name="process"></a>Proceso

1. Abra el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) en Administración de dispositivos de Microsoft 365 con un usuario que tenga el rol **administrador global**.

1. En el menú **Configuración global**, seleccione **Servicios conectados**. En la sección Inscribir dispositivos, seleccione la opción **Restablecer**.

1. Si decide continuar, se restablecerá la cuenta. Deberá volver a configurar Análisis de escritorio.

## <a name="next-steps"></a>Pasos siguientes

Después del restablecimiento, actualice la página y vuelva a ejecutar el proceso de incorporación. Para más información, consulte [Configuración de Análisis de escritorio](set-up.md).

Si tiene algún problema durante este proceso, póngase en contacto con el servicio de soporte técnico de Microsoft para recibir ayuda adicional.
