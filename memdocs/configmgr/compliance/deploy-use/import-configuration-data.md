---
title: Importar datos de configuración
titleSuffix: Configuration Manager
description: Importe datos de configuración si se encuentran en formato de archivo contenedor y se ajustan al esquema de Lenguaje de modelado de servicios compatible.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 4f70a956051858fce5b4ba5f519c7e1035600793
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692413"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Importación de datos de configuración con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Además de crear líneas base de configuración y elementos de configuración en la consola de Configuration Manager, puede importar datos de configuración si se encuentran en formato de archivo contenedor (.cab) y se ajustan al esquema de Lenguaje de modelado de servicios (SML) compatible. Puede importar datos de configuración desde:  

- Datos de configuración de procedimiento recomendado (paquetes de configuración) que se han descargado de Microsoft o de otros sitios de proveedores de software.  

- Datos de configuración que se han exportado desde System Center 2012 Configuration Manager y versiones posteriores.  

- Datos de configuración que se crearon externamente y que se ajustan al esquema de (SML).  

  Para un ejemplo de paquete de configuración que le ayude a administrar el cumplimiento de los roles de servidor de sitio de System Center 2012 Configuration Manager, vea [System Center 2012 Configuration Manager Configuration Pack](https://www.microsoft.com/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Al importar una línea base de configuración, algunos o todos los elementos de configuración a los que se hace referencia en la línea de base de configuración pueden incluirse también en el archivo contenedor. Durante el proceso de importación, Configuration Manager comprueba que todos los elementos de configuración a los que se hace referencia en la línea de base de configuración también se incluyen en el archivo .cab o ya existen en el sitio de Configuration Manager. Se produce un error en el proceso de importación si intenta importar una línea de base de configuración que hace referencia a datos de configuración que Configuration Manager no puede encontrar.  

Otros escenarios donde puede producirse un error en el proceso de importación son los siguientes:  

-   Los datos de configuración hacen referencia a datos de configuración que Configuration Manager no puede encontrar en su base de datos o en el propio archivo .cab.  

-   Los datos de configuración ya están presentes en la base de datos de Configuration Manager con el mismo nombre y la misma versión de datos de configuración, pero distinta versión del contenido.  

-   Los datos de configuración ya están presentes en la base de datos de Configuration Manager con la misma versión de contenido, pero el cálculo hash los identifica como diferentes.  

-   Una versión más reciente de los datos de configuración con el mismo nombre ya está presente en la base de datos de Configuration Manager o se ha eliminado recientemente.  

-   En una jerarquía Configuration Manager de varios sitios, los datos de configuración se importaron originalmente de un sitio primario. Deben actualizarse desde el mismo sitio y no desde un sitio secundario.  

### <a name="import-configuration-data"></a>Importar datos de configuración  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Elementos de configuración** o **Líneas base de configuración**.
2.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Importar datos de configuración**.  
3.  En la página **Seleccionar archivos** del **Asistente para importar datos de configuración**, haga clic en **Agregar**y, a continuación, en el cuadro de diálogo **Abrir** , seleccione los archivos .cab que quiere importar.  
4.  Active la casilla **Crear una nueva copia de los elementos de configuración y líneas de base de configuración importados** si quiere que los datos de configuración importados sean editables en la consola de Configuration Manager.  
5.  En la página **Resumen**, revise las acciones que deberán realizarse y, después, complete el asistente.  

Los datos de configuración importados se muestran en el nodo **Configuración de cumplimiento** del área de trabajo **Activos y compatibilidad**.  
