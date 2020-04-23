---
title: Herramienta de restablecimiento de actualizaciones
titleSuffix: Configuration Manager
description: Use la herramienta de restablecimiento de actualizaciones para actualizaciones en la consola para Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704333"
---
# <a name="update-reset-tool"></a>Herramienta de restablecimiento de actualizaciones

*Se aplica a: Configuration Manager (rama actual)*  


A partir de la versión 1706, los sitios primarios de Configuration Manager y los sitios de administración central incluyen la Herramienta de restablecimiento de actualizaciones de Configuration Manager, **CMUpdateReset.exe**. Utilice la herramienta para solucionar problemas cuando las actualizaciones en la consola tengan problemas al descargar o replicar. La herramienta se encuentra en la carpeta ***\cd.latest\SMSSETUP\TOOLS*** del servidor de sitio.

Puede usar esta herramienta con cualquier versión de la rama actual que permanece en el soporte técnico.

Utilice esta herramienta en aquellos casos en que no se haya instalado aún una [actualización en consola](install-in-console-updates.md) y esta se encuentre en un estado de error. Un estado de error significa que la descarga de actualización está en curso, pero bloqueada o tarda demasiado tiempo. Se considera demasiado tiempo cuando transcurren más horas que las expectativas históricas para los paquetes de actualización de tamaño similar. También puede implicar un error de replicación de la actualización en sitios primarios secundarios.  

Al ejecutar la herramienta, esta se ejecuta con la actualización que especifique. De forma predeterminada, la herramienta no elimina las actualizaciones instaladas o descargadas correctamente.  

### <a name="prerequisites"></a>Requisitos previos
La cuenta que utilice para ejecutar la herramienta requiere los permisos siguientes:
- Permisos de **lectura** y **escritura** para la base de datos de sitio del sitio de administración central y para cada sitio primario de la jerarquía. Para establecer estos permisos, puede agregar la cuenta de usuario como miembro de los [roles fijos de base de datos](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** y **db_datareader** en la base de datos de Configuration Manager de cada sitio. La herramienta no interactúa con los sitios secundarios.
- **Administrador local** en el sitio de primer nivel de la jerarquía.
- **Administrador local** en el equipo que hospeda el punto de conexión de servicio.

Necesita el GUID del paquete de actualización que desea restablecer. Para obtenerlo:
  1.   En la consola, vaya a **Administración** > **Actualizaciones y mantenimiento**.
  2.   En el panel de información, haga clic con el botón derecho en el encabezado de una de las columnas (como **Estado**) y seleccione **GUID de paquete** para agregar esa columna a la visualización.
  3.   Ahora, la columna muestra el GUID del paquete de actualización.

> [!TIP]  
> Para copiar el GUID, seleccione la fila del paquete de actualización que desea restablecer y cópiela con CTRL+C. Si pega la selección copiada en un editor de texto, podrá copiar únicamente el GUID para utilizarlo como un parámetro de la línea de comandos al ejecutar la herramienta.

### <a name="run-the-tool"></a>Ejecutar la herramienta    
La herramienta se debe ejecutar en el sitio de primer nivel de la jerarquía.

Al ejecutar la herramienta, utilice parámetros de línea de comandos para especificar:
- El servidor SQL Server en el sitio de nivel superior de la jerarquía.
- El nombre de la base de datos del sitio en el sitio de nivel superior.
- El GUID del paquete de actualización que desea restablecer.

En función del estado de la actualización, la herramienta identifica servidores adicionales a los que necesita acceder.   

Si el paquete de actualización está en un estado *posterior a la descarga*, la herramienta no limpiará el paquete. En ese caso, tiene la opción de exigir la eliminación de una actualización descargada correctamente mediante el parámetro correspondiente (vea los parámetros de la línea de comandos que se tratan más adelante en este mismo tema).

Después de ejecutar la herramienta:
- Si se eliminó un paquete, reinicie el servicio SMS_Executive en el sitio de nivel superior. A continuación, compruebe si hay actualizaciones, para poder descargar el paquete de nuevo.
- Si no se eliminó un paquete, no es necesario realizar ninguna acción. La actualización se reinicia y luego reinicia la replicación o instalación.

**Parámetros de línea de comandos:**  


|                        Parámetro                         |                                                       Descripción                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;nombre de dominio completo del servidor de SQL Server de su sitio de nivel superior>** | *Requerido* <br> Especifique el nombre de dominio completo del servidor de SQL Server que hospeda la base de datos de sitio de nivel superior de la jerarquía. |
|                **-D &lt;nombre de base de datos >**                 |                          *Requerido* <br> Especifique el nombre de la base de datos del sitio de nivel superior.                          |
|                 **-P &lt;GUID del paquete >**                 |                        *Requerido* <br> Especifique el GUID del paquete de actualización que desea restablecer.                        |
|           **-I &lt;nombre de instancia de SQL Server>**           |                    *Opcional* <br> Identifique la instancia de SQL Server que hospeda la base de datos de sitio.                     |
|                       **-FDELETE**                       |                       *Opcional* <br> Exija la eliminación de un paquete de actualización descargado correctamente.                        |

**Ejemplos:**  
En un escenario habitual, querrá restablecer una actualización que tenga problemas de descarga. El nombre de dominio completo de los servidores de SQL Server es *server1.fabrikam.com*, la base de datos de sitio es *CM_XYZ* y el GUID del paquete es *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Ejecute lo siguiente: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

En un escenario más extremo, quizá desee forzar la eliminación del paquete de actualización problemático. El nombre de dominio completo de los servidores de SQL Server es *server1.fabrikam.com*, la base de datos de sitio es *CM_XYZ* y el GUID del paquete es *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Ejecute lo siguiente: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
