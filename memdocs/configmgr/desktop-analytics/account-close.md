---
title: Cierre de la cuenta
titleSuffix: Configuration Manager
description: Eliminación de Análisis de escritorio de la cuenta de Azure
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706613"
---
# <a name="how-to-close-your-account"></a>Cierre de la cuenta

Si configuró Análisis de escritorio en el entorno y luego decide que debe quitarlo, use este proceso para cerrar la cuenta.

## <a name="prerequisites"></a>Requisitos previos

Solo un **administrador global** puede cerrar o volver a activar la cuenta en Azure Portal.

## <a name="process-to-offboard"></a>Proceso de anulación de incorporación

1. Abra el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) en Administración de dispositivos de Microsoft 365 con un usuario que tenga el rol **administrador global**.

1. En el menú **Configuración global**, seleccione **Servicios conectados**. En la sección Inscribir dispositivos, seleccione la opción **Offboard** (Anular incorporación).

1. Si decide continuar, la cuenta se cierra.

> [!Important]
> Continúe únicamente con el resto de este artículo después de 90 días o si no la va a reactivar.
>
> Si quiere cerrar completamente la cuenta sin esperar 90 días, primero [restablezca](account-reset.md) la cuenta.

## <a name="reactivate"></a>Reactivación

Durante los próximos 90 días, cualquier administrador de la organización que acceda al portal de Análisis de escritorio verá el aviso de que ha optado por anular la incorporación.

Un administrador global puede reactivar la cuenta en un plazo de 90 días. Para restaurar Análisis de escritorio de su organización, seleccione la opción **Devolverme**.

## <a name="delete-the-solution"></a>Eliminación de la solución

> [!Warning]
> Continúe únicamente con el resto de este artículo después de 90 días o si no la va a reactivar. Si elimina y desconecta estos otros componentes, no intente reactivarla.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) como usuario con el rol **Administrador global**.

1. Busque en **Todos los recursos** por el nombre del área de trabajo de Análisis de escritorio. Este es el nombre que creó al suscribirse al servicio.

1. Elimine `Microsoft365Analytics(YourWorkspaceName)` de tipo **Solución**.

Los datos de Análisis de escritorio caducan de acuerdo con la directiva de retención de datos del área de trabajo. Puede seguir usando cualquier otra solución en la misma área de trabajo.

> [!Important]  
> Si usa el área de trabajo de Log Analytics con otras soluciones, no la elimine.

## <a name="remove-user-and-app-access"></a>Eliminación del acceso de usuarios y aplicaciones

1. Inicie sesión en [Azure Portal](https://portal.azure.com) como usuario con el rol **Administrador global**. Vaya a **Azure Active Directory**.

1. En **Roles y administradores**, busque el rol **Administrador de Análisis de escritorio**. Quite sus miembros.

1. En **Grupos**, quite los miembros de los siguientes grupos:

    - **Administradores de clientes de Analytics M365 (propietarios de Log Analytics)**
    - **Administradores de clientes de M365 Analytics (colaboradores de Log Analytics)**

1. En **Aplicaciones empresariales**, elimine o revoque los permisos de acceso para las siguientes aplicaciones:

    - `MaLogAnalyticsReader`

    - Aplicación Configuration Manager. Para encontrar el nombre de esta aplicación, vaya a la consola de Configuration Manager. En el área de trabajo **Administración**, expanda **Servicios de nube** y seleccione el nodo **Servicios de Azure**. Abra las propiedades del servicio **Análisis de escritorio** y cambie a la pestaña **Aplicaciones**. La **aplicación web** es esta aplicación de Azure.

        > [!Important]  
        > Antes de realizar cambios en esta aplicación en Azure AD, asegúrese de que no la usa de nuevo con otro servicio en Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Desconexión de Configuration Manager

1. Abra la consola de Configuration Manager como usuario con el rol **Administrador total**.

1. Vaya a al área de trabajo **Administración**, expanda **Servicios de nube** y seleccione el nodo **Servicios de Azure**.

1. Elimine el servicio Análisis de escritorio.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Eliminación de recopilaciones de las implementaciones piloto y de producción

1. En la consola de Configuration Manager, seleccione **Recopilaciones de dispositivos** en el área de trabajo **Activos y compatibilidad**.

1. Elimine todas las recopilaciones que ya no use. De forma predeterminada, las recopilaciones se encuentran en la carpeta **Planes de implementación**.  

## <a name="reconfigure-clients"></a>Reconfiguración de los clientes

### <a name="unenroll-devices"></a>Anulación de la inscripción de dispositivos

En los dispositivos inscritos, quite el valor CommercialID de las siguientes claves del Registro de Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuración de los datos de diagnóstico de Windows

Si no quiere que los dispositivos sigan enviando datos de diagnóstico, siga estos pasos:

- Windows 10: establezca el nivel de datos de diagnóstico en **Seguridad**
- Windows 7 SP1 o 8.1: deshabilite la **clave de participación en los datos comerciales**.

Establezca estos valores con uno de los métodos siguientes:

- Directiva de grupo: en **Configuración del equipo** > **Plantillas administrativas** > **Componentes de Windows** > **Recopilación de datos y versiones preliminares**
- Administración de dispositivos móviles (MDM), como [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Al aplicar estos cambios, los dispositivos dejan de enviar datos de diagnóstico inmediatamente. Microsoft puede tardar entre 24 y 48 horas en detener el procesamiento de las conclusiones del área de trabajo. Microsoft elimina estos datos de sus servicios en la nube en un plazo de 30 días como máximo.
