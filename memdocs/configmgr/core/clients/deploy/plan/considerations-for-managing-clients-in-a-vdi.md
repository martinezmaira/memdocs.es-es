---
title: Administrar clientes VDI
titleSuffix: Configuration Manager
description: Administre clientes de Configuration Manager en una infraestructura de escritorio virtual (VDI).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693863"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Administración de clientes de Configuration Manager en una infraestructura de escritorio virtual (VDI)

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite la instalación del cliente de Configuration Manager en los siguientes escenarios de infraestructura de escritorio virtual (VDI):  

- **Máquinas virtuales personales**: las máquinas virtuales personales se suelen usar cuando se quiere garantizar que los datos y la configuración de usuario se mantienen en la máquina virtual entre sesiones.  

- **Sesiones de Servicios de Escritorio Remoto**: Servicios de Escritorio Remoto permite a un servidor hospedar varias sesiones de cliente simultáneas. Los usuarios pueden conectarse a una sesión y, a continuación, ejecutar aplicaciones en ese servidor.  

- **Máquinas virtuales agrupadas**: las máquinas virtuales agrupadas no se conservan entre sesiones. Cuando se cierra una sesión, se descartan todos los datos y configuraciones. Las máquinas virtuales agrupadas son útiles cuando no se puede utilizar Servicios de Escritorio Remoto debido a que una aplicación empresarial requerida no se puede ejecutar en el servidor Windows Server que hospeda las sesiones de cliente.  

  En la tabla siguiente se incluyen consideraciones para la administración del cliente de Configuration Manager en una infraestructura de escritorio virtual.  

|Tipo de máquina virtual|Consideraciones|  
|--------------------------|--------------------|  
|Máquinas virtuales personales|Configuration Manager trata a las máquinas virtuales personales de forma idéntica a un equipo físico. El cliente de Configuration Manager se puede instalar previamente en la imagen de máquina virtual o implementar después de aprovisionar la máquina virtual.|  
|Servicios de Escritorio Remoto|El cliente de Configuration Manager no está instalado para sesiones de Escritorio Remoto individuales. En su lugar, el cliente sólo se instala una vez en el servidor de Servicios de Escritorio Remoto. Todas las características de Configuration Manager pueden usarse en el servidor de Servicios de Escritorio Remoto.|  
|Máquinas virtuales agrupadas|Cuando se retira una máquina virtual agrupada, cualquier cambio realizado mediante Configuration Manager se pierde.<br /><br /> Es posible que los datos devueltos de características de Configuration Manager como el inventario de hardware, el inventario de software y la disponibilidad de software no sean relevantes para sus necesidades, ya que la máquina virtual podría estar operativa solo durante un breve periodo de tiempo. Considere la posibilidad de excluir a las máquinas virtuales agrupadas de las tareas de inventario.|  

 Debido a que la virtualización admite la ejecución de varios clientes de Configuration Manager en el mismo equipo físico, muchas operaciones de cliente tienen un retraso aleatorio integrado para acciones programadas como el inventario de hardware y software, los exámenes antimalware, las instalaciones de software y los exámenes de actualizaciones de software. Este retraso ayuda a distribuir el procesamiento de la CPU y la transferencia de datos de un equipo que tiene varias máquinas virtuales que ejecutan el cliente de Configuration Manager.  

> [!NOTE]  
>  Con la excepción de los clientes de Windows Embedded que están en modo de mantenimiento, los clientes de Configuration Manager que no se están ejecutando en entornos virtualizados también usan este retraso aleatorio. Cuando se tienen muchos clientes implementados, este comportamiento ayuda a evitar que se produzcan picos de uso del ancho de banda de red y reduce el requisito de procesamiento de la CPU en los sistemas de sitio de Configuration Manager, como el punto de administración y el servidor de sitio. El intervalo de retraso varía según la capacidad de Configuration Manager.  
>   
>  El retraso de selección aleatoria está deshabilitado de forma predeterminada para las actualizaciones de software requeridas mediante la siguiente configuración de cliente: **Agente de equipo**: **Deshabilitar selección aleatoria de fecha límite**.
