---
title: Instalación de informes de ejemplo de Power BI
titleSuffix: Configuration Manager
description: Aprenda a instalar los informes de ejemplo de Power BI en Configuration Manager.
ms.date: 08/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 450c76617cf12a3201aa990c90843cb2e0f0edee
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179441"
---
# <a name="install-power-bi-sample-reports"></a>Instalación de informes de ejemplo de Power BI
<!--5679791-->
*Se aplica a: Configuration Manager (rama actual)*

A partir de la versión 2002, puede integrar [Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) con los informes de Configuration Manager. Existen informes de ejemplo para descarga que puede instalar en Configuration Manager. En este artículo se explica cómo instalar los informes de ejemplo de Power BI en Configuration Manager.

## <a name="prerequisites"></a>Requisitos previos

- Punto de servicios de informes de Configuration Manager con [Power BI Report Server integrado](powerbi-report-server.md)

- [Microsoft Power BI Desktop (optimizado para Power BI Report Server de septiembre de 2019)](https://www.microsoft.com/download/details.aspx?id=57271), o posterior.

- Se recomienda el [paquete acumulativo de actualizaciones (4560496) para la versión 2002](https://support.microsoft.com/help/4560496), pero no es necesario.

    > [!IMPORTANT]
    > Use solo las versiones de Power BI Desktop del [centro de descarga de Microsoft](https://www.microsoft.com/download/). No use una versión de Microsoft Store.
    >
    > Use solo una versión de Power BI Desktop [optimizada para Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>Descarga de los informes de ejemplo

Para descargar los informes de ejemplo:

1. Descargue los informes de ejemplo de Power BI del [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=101452).

1. Guarde el archivo `ConfigMgrSamplePowerBIReports.exe`.

1. Mueva el archivo a un equipo con Microsoft Power BI Desktop (optimizado para Power BI Report Server) instalado si lo descargó desde otro dispositivo.

1. Ejecute el archivo `ConfigMgrSamplePowerBIReports.exe` para extraer los archivos .pbit.

## <a name="install-the-sample-reports"></a>Instalación de los informes de ejemplo

Para instalar los informes de ejemplo:

1. En Power BI Report Server, cree una carpeta llamada `Sample Reports` en la carpeta raíz de informes de Configuration Manager.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Creación de la carpeta de informes de ejemplo en la carpeta raíz de informes de Configuration Manager desde " lightbox="media/create-sample-reports-folder.png":::

1. Inicie Microsoft Power BI Desktop (optimizado para Power BI Report Server).

1. Seleccione **Archivo**, luego **Abrir** y vaya al lugar donde guardó los archivos .pbit extraídos.

1. Seleccione uno de los archivos .pbit extraídos del archivo `ConfigMgrSamplePowerBIReports.exe`.

1. Especifique el nombre de la base de datos de Configuration Manager y el nombre del servidor de bases de datos cuando se le solicite y, luego, seleccione **Cargar**.

    Al cargar o aplicar el modelo de datos, omita los errores que surjan.

    :::image type="content" source="media/sample-report-database.png" alt-text="Especificación de la base de datos y el nombre del servidor de bases de datos" lightbox="media/sample-report-database.png":::

1. Cuando se carguen los datos del informe, seleccione **Archivo** > **Guardar como** y, luego, elija **Power BI Report Server**.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Guardar como Power BI Report Server" lightbox="media/save-powerbi-report-server.png":::

1. Guarde el informe en la carpeta `Sample Reports` que creó en el punto de notificación.

    :::image type="content" source="media/save-sample-report.png" alt-text="Guardar en la carpeta de informes de ejemplo" lightbox="media/save-sample-report.png":::

1. Repita los pasos con otros informes de ejemplo. Cuando termine, cierre Microsoft Power BI Desktop (optimizado para Power BI Report Server).

1. En la consola de Configuration Manager, vaya a **Supervisión** > **Informes de Power BI** > **Informes de ejemplo**.

1. Haga clic con el botón derecho en uno de los informes y seleccione **Ejecutar en explorador** para iniciar el informe.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Ejecución del informe de ejemplo desde la consola de Configuration Manager" lightbox="media/view-powerbi-report.png":::
