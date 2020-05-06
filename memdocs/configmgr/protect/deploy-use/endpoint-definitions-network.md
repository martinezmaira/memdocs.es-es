---
title: Descarga de definiciones desde un recurso compartido de red
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo descargar manualmente las últimas actualizaciones de definiciones de Microsoft y, luego, configurar los clientes para que descarguen estas definiciones.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697233"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Permitir que las definiciones de malware de Endpoint Protection se descarguen de un recurso compartido de red

*Se aplica a: Configuration Manager (rama actual)*

 Puede descargar manualmente las últimas actualizaciones de definiciones de Microsoft y luego configurar los clientes para que descarguen estas definiciones desde una carpeta compartida en la red. Los usuarios también pueden iniciar las actualizaciones de definiciones si se usa este origen de actualización.

> [!NOTE]
>  Los clientes deben tener acceso de lectura a la carpeta compartida para poder descargar actualizaciones de definiciones.

 Para obtener más información sobre cómo descargar las actualizaciones de definiciones y motores para su almacenamiento en el recurso compartido de archivos, consulte [Install the latest Microsoft antimalware and antispyware software](https://www.microsoft.com/wdsi/definitions) (Instalar el software antimalware y antispyware más reciente de Microsoft).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Para configurar las descargas de definiciones desde un recurso compartido de archivos

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Endpoint Protection**y haga clic en **Directivas antimalware**.

3.  Abra la página de propiedades de la **Directiva antimalware predeterminada** o cree una nueva. Para más información sobre cómo crear directivas antimalware, consulte [Crear e implementar directivas antimalware para Endpoint Protection](endpoint-antimalware-policies.md).

4.  En la sección **Actualizaciones de inteligencia de seguridad** del cuadro de diálogo de propiedades de antimalware, haga clic en **Establecer origen**.
    - Se ha cambiado el nombre de la sección **Actualizaciones de definiciones** a **Actualizaciones de inteligencia de seguridad** a partir de Configuration Manager, versión 1902.

5.  En el cuadro de diálogo **Configurar orígenes de actualización de definiciones** , seleccione **Actualizaciones desde recursos compartidos de archivos UNC**.

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar orígenes de actualización de definiciones** .

7.  Haga clic en **Rutas de acceso**. A continuación, en el cuadro de diálogo **Configurar rutas de acceso UNC de actualización de definiciones** , agregue una o varias rutas de acceso UNC a la ubicación de los archivos de actualizaciones de definiciones en un recurso compartido de red.

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar rutas de acceso UNC de actualización de definiciones** .


> [!div class="button"]
> [Paso siguiente >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Atrás >](endpoint-configure-alerts.md)
