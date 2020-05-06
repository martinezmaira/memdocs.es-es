---
title: Administración de actualizaciones rápidas de Windows 10
titleSuffix: Configuration Manager
description: Configuration Manager admite archivos de instalación rápida para Windows 10, que proporciona descargas más pequeñas y tiempos de instalación más rápidos en los clientes.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4093eafe9f8a337ce322165a529f630a759b365f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701383"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Administración de archivos de instalación rápida para actualizaciones de Windows 10

Configuration Manager admite archivos de instalación rápida para las actualizaciones de Windows 10. Configure el cliente para descargar solo los cambios entre la actualización acumulativa de calidad de Windows 10 del mes actual y la actualización del mes anterior. Sin los archivos de instalación rápida, los clientes de Configuration Manager descargan cada mes la actualización acumulativa completa de Windows 10, incluidas todas las actualizaciones de los meses anteriores. Usar los archivos de instalación rápida proporciona descargas más pequeñas y tiempos de instalación más rápidos en los clientes.

Para obtener información sobre cómo usar Configuration Manager para administrar el contenido de actualización para estar al día con Windows 10, consulte [Optimización de la distribución de actualizaciones de Windows 10](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> La compatibilidad con el cliente del sistema operativo está disponible en la versión 1607 de Windows 10, con una actualización del Agente de Windows Update. Esta actualización se incluye con las actualizaciones publicadas el 11 de abril de 2017. Para obtener más información sobre estas actualizaciones, vea el [artículo de soporte técnico 4015217](https://support.microsoft.com/kb/4015217). Las actualizaciones futuras se benefician de la instalación rápida para descargas más pequeñas. Las versiones anteriores de Windows 10 y la versión 1607 de Windows 10 sin esta actualización no admiten los archivos de instalación rápida.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Habilitar el sitio para descargar archivos de instalación rápida para las actualizaciones de Windows 10
Para iniciar la sincronización de los metadatos de los archivos de instalación rápida de Windows 10, habilítelos en las propiedades de punto de actualización de software.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el sitio de administración central o el sitio primario independiente.  

3. En la cinta de opciones, haga clic en **Configurar componentes de sitio** y después haga clic en **Punto de actualización de software**. Cambie a la pestaña **Archivos de actualización** y seleccione **Download both full files for all approved updates and express installation files for Windows 10** (Descargar archivos completos para todas las actualizaciones aprobadas y archivos de instalación rápida de Windows 10).

> [!NOTE]    
> El componente Punto de actualización de software no se puede configurar para descargar *solo* actualizaciones rápidas.  El sitio de descarga los archivos de instalación rápida además de los archivos completos. Esto aumenta la cantidad de contenido almacenado en la biblioteca de contenido y se distribuye y almacena en los puntos de distribución.

> [!Tip]  
> Para determinar el espacio real que el archivo va a ocupar en el disco, compruebe la propiedad **Size on disk** (Tamaño en disco) del archivo. La propiedad de tamaño en disco debe ser considerablemente inferior al valor de tamaño. Para más información, vea las [preguntas más frecuentes para optimizar la distribución de actualizaciones de Windows 10](optimize-windows-10-update-delivery.md#bkmk_faq).  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Habilitar los clientes para que descarguen e instalen archivos de instalación rápida
Para habilitar la compatibilidad de los archivos de instalación rápida en los clientes, habilite los archivos de instalación rápida en la sección **Actualizaciones de software** de la configuración de cliente. Esta configuración crea un agente de escucha HTTP que escucha las solicitudes para descargar los archivos de instalación rápida en el puerto que especifique.

> [!NOTE]    
> Se trata de un puerto local que los clientes usan para escuchar solicitudes de Optimización de distribución o Servicio de transferencia inteligente en segundo plano (BITS) para descargar contenido rápido desde el punto de distribución. No es necesario abrir este puerto en firewalls, pues todo el tráfico se encuentra en el equipo local.  

Una vez que implemente la configuración de cliente para habilitar esta característica en el cliente, intenta descargar la diferencia entre la actualización acumulativa de Windows 10 del mes actual y la actualización del mes anterior. Los clientes deben ejecutar una versión de Windows 10 que admita los archivos de instalación rápida.  

1. Habilite la compatibilidad para los archivos de instalación rápida en las propiedades de componente de punto de actualización de software (procedimiento anterior).  

2. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione **Configuración de cliente**.  

3. Seleccione la configuración de cliente adecuada y, después, haga clic en **Propiedades** en la cinta de opciones.  

4. Seleccione el grupo **Actualizaciones de software**. Establezca la configuración en **Sí** para **Enable installation of Express Updates on clients** (Habilitar la instalación de actualizaciones rápidas en clientes). Configure el puerto que ha usado el agente de escucha HTTP en el cliente en la opción **Port used to download content for Express Updates** (Puerto usado para descargar el contenido de las actualizaciones rápidas).
    - En la versión 1902, el **Puerto usado para descargar el contenido de las actualizaciones rápidas** ha cambiado al **Puerto que los clientes usan para recibir solicitudes para el contenido diferencial**.

## <a name="next-steps"></a>Pasos siguientes

[Implementar actualizaciones de software](deploy-software-updates.md)