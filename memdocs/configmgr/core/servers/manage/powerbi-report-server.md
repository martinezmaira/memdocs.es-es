---
title: Integración con Power BI Report Server
titleSuffix: Configuration Manager
description: Integre Power BI Report Server con los informes de Configuration Manager para obtener una visualización moderna y un mejor rendimiento.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f4089f52d912491b3b1396906fe391c5c334e061
ms.sourcegitcommit: 02635469d684d233fef795d2a15615658e62db10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2020
ms.locfileid: "84814900"
---
# <a name="integrate-with-power-bi-report-server"></a>Integración con Power BI Report Server

*Se aplica a: Configuration Manager (rama actual)*

<!--3721603-->

A partir de la versión 2002, puede integrar [Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) con los informes de Configuration Manager. Esta integración proporciona una visualización moderna y un mejor rendimiento. Además, la consola admite informes de Power BI de manera similar a como ya ocurre con SQL Server Reporting Services.

Guarde archivos de informes de Power BI Desktop (.PBIX) e impleméntelos en el Power BI Report Server. Este proceso es similar al de los archivos de informes de SQL Server Reporting Services (.RDL). También puede iniciar los informes en el explorador directamente desde la consola de Configuration Manager.

## <a name="prerequisites"></a>Requisitos previos

- Licencia de Power BI Report Server. Para más información, vea [Licencias de Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Descargue [Microsoft Power BI Report Server de septiembre de 2019](https://www.microsoft.com/download/details.aspx?id=57270), o posterior.

    > [!NOTE]
    > No instale Power BI Report Server de inmediato. Para ver el proceso adecuado en función de su entorno, consulte la sección [Configuración del punto de servicios de informes](#configure-the-reporting-services-point).

- Descargue [Microsoft Power BI Desktop (optimizado para Power BI Report Server de septiembre de 2019)](https://www.microsoft.com/download/details.aspx?id=57271), o posterior.

    > [!IMPORTANT]
    > - Use solo las versiones de Power BI Desktop del [centro de descarga de Microsoft ](https://www.microsoft.com/download/), no use una versión de Microsoft Store.
    > - Use solo una versión de [Power BI Desktop que indique que se ha **optimizado para Power BI Report Server**](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

- La integración de Power BI usa la misma administración basada en roles para la generación de informes.
    > [!NOTE]
    > Power BI Report Server no admite informes habilitados para RBAC, por lo tanto, las personas que vean los informes verán los mismos resultados, con independencia de su ámbito asignado.

## <a name="configure-the-reporting-services-point"></a>Configuración del punto de servicios de informes

Este proceso varía en función de si ya tiene este rol en el sitio.

### <a name="you-have-a-reporting-services-point"></a>Tiene un punto de servicios de informes

Use este proceso solo si ya tiene un punto de servicios de informes en el sitio. Siga todos los pasos de este proceso en el mismo servidor:

1. En **Administrador de configuración del servidor de informes**, haga una copia de seguridad de las **Claves de cifrado**. Para obtener más información, vea [Claves de cifrado de SSRS: copia de seguridad y restauración de claves de cifrado](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Si omite este paso, perderá el acceso a los informes personalizados en SQL Server Reporting Services.

1. Quite el rol de punto de servicios de informes del sitio.

1. Desinstale SQL Server Reporting Services, pero mantenga la base de datos.

1. Instale Power BI Report Server.

1. Configuración de Power BI Report Server

    1. Use la base de datos del servidor de informes anterior.

    1. Use **Administrador de configuración del servidor de informes** para restaurar las **Claves de cifrado**.

1. Agregue el rol de punto de servicios de informes en Configuration Manager.

### <a name="you-dont-have-a-reporting-services-point"></a>No tiene un punto de servicios de informes

Use este proceso solo si aún no tiene un punto de servicios de informes en el sitio. Siga todos los pasos de este proceso en el mismo servidor:

1. Instale Power BI Report Server.

2. Agregue el rol de punto de servicios de informes en Configuration Manager. Para más información, consulte [Configuración de informes](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Configuración de la consola de Configuration Manager

1. En un equipo que tenga la consola de Configuration Manager, actualice la consola de Configuration Manager a la última versión.

1. Instale Power BI Desktop. Asegúrese de que el idioma sea el mismo.

1. Una vez instalado, inicie Power BI Desktop al menos una vez antes de abrir la consola de Configuration Manager.

## <a name="create-power-bi-reports"></a>Creación de informes de Power BI

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nuevo nodo **Informes de Power BI**.

1. En la cinta de opciones, seleccione **Crear informe**. Esta acción abre Power BI Desktop.

1. Cree un informe en Power BI Desktop.

    - En Power BI Desktop, al conectarse a un origen de datos, seleccione **DirectQuery** para la configuración de conexión.

    - Use solo vistas SQL compatibles en estos informes. Para obtener más información, consulte cómo [crear informes personalizados mediante vistas de SQL Server en Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Cuando el informe esté listo para ser guardado, vaya al menú **Archivo**, seleccione **Guardar como** y, después, seleccione **Power BI Report Server**.

1. En la ventana **Power BI Report Server Selection** (Selección de Power BI Report Server), escriba la dirección URL del punto de servicios de informes como **Nueva dirección de servidor de informes**. Por ejemplo, `https://rsp.contoso.com/Reports`.

En la consola de Configuration Manager, verá el informe nuevo en la lista de informes de Power BI.

## <a name="next-steps"></a>Pasos siguientes

Después de crear un informe, realice las acciones siguientes en la consola de Configuration Manager:

- **Ejecutar en explorador**: abre el informe de Power BI en el explorador web. Comparta esta dirección URL con otras personas, por ejemplo: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Solo puede ver estos informes en el explorador web.

- **Editar**: Modifique el informe en Power BI Desktop. En el caso de un informe existente, use la opción **Guardar** para guardar los cambios de nuevo en el servidor de informes.

Para obtener más información sobre los archivos de registro que se van a usar para los informes, vea [Referencia del archivo de registro: Informes](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
