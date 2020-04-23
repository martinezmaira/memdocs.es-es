---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Use Deployment Monitoring Tool para solucionar problemas de implementaciones de software en un cliente de Configuration Manager.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707833"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*Se aplica a: Configuration Manager (rama actual)*

Deployment Monitoring Tool es una de las [herramientas de Configuration Manager](tools.md). Es una interfaz gráfica de usuario diseñada para ayudar a solucionar problemas de implementaciones de línea de base de configuración, actualizaciones de software y aplicaciones en un cliente de Configuration Manager. La herramienta es de solo lectura y no cambia ningún estado en el cliente. Puede usarla con seguridad para diagnosticar los escenarios comunes de implementación.


## <a name="features"></a>Funciones

- Ejecútela como administrador para solucionar problemas de implementación en un cliente local.  

- Solucione problemas de implementaciones de un cliente remoto. Inicie la herramienta y conéctese a un equipo remoto como administrador.  

- Exporte a XML todos los datos recopilados en la herramienta. Comparta el archivo XML con otros usuarios y utilícelo como una plataforma común para hablar sobre cómo solucionar problemas de implementaciones.  

- Importe datos exportados previamente a un equipo diferente y utilícelos para ejecutar la herramienta en modo sin conexión.   


## <a name="usage"></a>Uso

La herramienta de supervisión de la implementación admite solo la interfaz gráfica de usuario. Para iniciar la herramienta, ejecute **DeploymentMonitoringTool.exe** como administrador. Hay tres vistas:  

- **Propiedades del cliente**: una lista de atributos útiles sobre el dispositivo y el cliente de Configuration Manager. Esta es la visa predeterminada.   

- **Implementaciones**: vea todas las implementaciones de destino actuales. Seleccione una implementación en el panel de resultados para ver más información en el panel de detalles.  

- **Todas las actualizaciones**: vea todas las actualizaciones de software y su estado.  

Para copiar datos en cualquier vista, seleccione una celda y presione **CTRL** + **C**.


### <a name="actions-menu"></a>Menú Acciones

Las acciones siguientes están disponibles en el menú **Acciones**:  

- **Conectarse a equipo remoto**: seleccione un equipo al que quiera conectarse. Cuando no se especifica un nombre de usuario y contraseña, utilice las credenciales actuales. Haga clic en **Guardar** para conectarse a un equipo remoto.  

- **Exportar datos**: seleccione el archivo en el que quiera escribir los datos y haga clic en **Guardar**. Use el archivo XML exportado para solucionar problemas de forma remota en un equipo diferente.  

- **Importar datos**: seleccione un archivo para importarlo a la herramienta.  

- **Ver registro**: se abre un archivo de registro asociado, según la vista:  
    - Propiedades del cliente: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Implementaciones: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Todas las actualizaciones: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Vea también

- [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md)
- [Implementar actualizaciones de software](../../sum/deploy-use/deploy-software-updates.md)
- [Implementar líneas base de configuración](../../compliance/deploy-use/deploy-configuration-baselines.md)
