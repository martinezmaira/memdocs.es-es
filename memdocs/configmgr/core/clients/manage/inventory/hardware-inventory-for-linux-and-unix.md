---
title: Inventario de hardware para Linux y UNIX
titleSuffix: Configuration Manager
description: Aprenda a usar inventario de hardware para Linux y UNIX en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1bdfb8c6d528c12581f05f86111a1a76d2259faa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695433"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Inventario de hardware para Linux y UNIX en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

El cliente de Configuration Manager para Linux y UNIX admite el inventario de hardware. Después de recopilar el inventario de hardware, puede ejecutar y ver el inventario en el Explorador de recursos o informes de Configuration Manager y usar esta información para crear consultas y recopilaciones que permiten las siguientes operaciones:  

- Implementación de software  

- Aplicar ventanas de mantenimiento  

- Implementar configuraciones personalizadas de cliente  

El inventario de hardware para servidores Linux y UNIX utiliza un servidor de Modelo de información común (CIM) basado en estándares. El servidor CIM se ejecuta como un servicio de software (o daemon) y proporciona una infraestructura de administración que se basa en estándares del grupo de trabajo de administración distribuida (DMTF). El servidor CIM proporciona una funcionalidad similar a las capacidades de CIM de la infraestructura de administración de Windows (WMI) que están disponibles en equipos basados en Windows.  

A partir de la actualización acumulativa 1, el cliente para Linux y UNIX usa la versión 1.0.6 de **omiserver** de código abierto de **The Open Group**. (Antes de la actualización acumulativa 1, el cliente utilizaba **nanowbem** como servidor CIM).  

El servidor CIM se instala como parte del cliente para Linux y UNIX. El cliente para Linux y UNIX se comunica directamente con el servidor CIM y no utiliza la interfaz de WS-MAN del servidor CIM. El puerto de WS-MAN en el servidor CIM está deshabilitado cuando se instala el cliente. Microsoft desarrolló el servidor CIM que ahora está disponible como código abierto a través del proyecto Open Management Infrastructure (OMI). Para obtener más información sobre el proyecto Open Management Infrastructure, consulte el sitio web de [The Open Group](https://www.opengroup.org/) .  

El inventario de hardware en servidores Linux y UNIX funciona mediante la asignación de clases y propiedades de WMI de Win32 existentes a clases y propiedades equivalentes para servidores Linux y UNIX. Esta asignación uno a uno de clases y propiedades permite que el inventario de hardware de Linux y UNIX se integre en Configuration Manager. Los datos de inventario de servidores Linux y UNIX se muestran junto con el inventario de equipos basados en Windows en la consola y los informes de Configuration Manager. Este comportamiento proporciona una experiencia de administración coherente y heterogénea.  

> [!TIP]  
>  Puede usar el valor **Título** para la clase **Sistema operativo** a fin de identificar los diferentes sistemas operativos Linux y UNIX en consultas y recopilaciones.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Configurar el inventario de hardware para servidores Linux y UNIX  
 Puede utilizar la configuración de cliente predeterminada o crear configuraciones de dispositivo cliente personalizadas para configurar el inventario de hardware. Cuando se utiliza la configuración de dispositivos cliente personalizada, puede configurar las clases y las propiedades que quiera recopilar únicamente de los servidores Linux y UNIX. También puede especificar las programaciones personalizadas para cuándo recopilar inventarios completos y diferenciales de los servidores Linux y UNIX.  

 El cliente para Linux y UNIX admite las siguientes clases de inventario de hardware que están disponibles en servidores Linux y UNIX:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

No todas las propiedades para estas clases de inventario están habilitadas para equipos UNIX y Linux en Configuration Manager.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Operaciones del inventario de hardware  
 Después de recopilar el inventario de hardware de los servidores Linux y UNIX, puede ver y utilizar esta información de la misma manera que ve el inventario que recopila de otros equipos:  

- Utilizar el Explorador de recursos para ver información detallada sobre el inventario de hardware de servidores Linux y UNIX.  

- Crear consultas basadas en configuraciones de hardware específicas.  

- Crear recopilaciones basadas en consultas en función de configuraciones de hardware específicas.  

- Ejecutar informes que muestran detalles específicos sobre las configuraciones de hardware.  

El inventario de hardware en un servidor Linux o UNIX se ejecuta según la programación configurada en la configuración del cliente. De forma predeterminada, esta programación tiene lugar cada siete días. El cliente para Linux y UNIX admite tanto ciclos de inventario completo como ciclos de inventario diferencial.  

También puede forzar al cliente en un servidor Linux o UNIX para que ejecute el inventario de hardware de inmediato. Para ejecutar el inventario de hardware, en un cliente use las credenciales **raíz** para ejecutar el siguiente comando para iniciar un ciclo de inventario de hardware: `/opt/microsoft/configmgr/bin/ccmexec -rs hinv`.  

Las acciones del inventario de hardware se especifican en el archivo de registro de cliente, **scxcm.log**.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Cómo utilizar Open Management Infrastructure para crear un inventario de hardware personalizado  
 El cliente para Linux y UNIX admite el inventario de hardware personalizado que puede crear utilizando Open Management Infrastructure (OMI). Para ello, siga estos pasos:  

1.  Cree un proveedor de inventario personalizado mediante el origen OMI.  

2.  Configure equipos para que usen el nuevo proveedor para informar el inventario.  

3.  Habilitar Configuration Manager para admitir el nuevo proveedor  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Cree un proveedor de  inventario de hardware personalizado para equipos UNIX y Linux:  
 Para crear un proveedor de inventario de hardware personalizado para el cliente de Configuration Manager para Linux y UNIX, use **OMI Source - v.1.0.6** y siga las instrucciones de la Guía de introducción de OMI. Este proceso incluye la creación de un archivo Managed Object Format (MOF) que define el esquema del nuevo proveedor. Después, importe el archivo MOF en Configuration Manager para habilitar la compatibilidad de la nueva clase de inventario personalizado.  

 Tanto OMI Source - v.1.0.6 como la Guía de introducción de OMI están disponibles para descargar desde el sitio web de [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . Puede encontrar estas descargas en la pestaña **Documentos** en la siguiente página web en el sitio web de OpenGroup.org: [Open Management Infrastructure (OMI)](https://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Configure cada equipo que ejecute Linux o UNIX con el proveedor de inventario de hardware personalizado:  
 Después de crear un proveedor de inventario personalizado, debe copiar y, a continuación, registrar el archivo de la biblioteca del proveedor en cada equipo que tiene el inventario que desea recopilar.  

1.  Copie la biblioteca del proveedor en cada equipo Linux y UNIX del que desea recopilar el inventario. El nombre de la biblioteca del proveedor es similar al siguiente: **XYZ_MyProvider.SO**  

2.  A continuación, en cada equipo Linux y UNIX, registre la biblioteca del proveedor en el servidor OMI. El servidor OMI se instala en el equipo al instalar el cliente de Configuration Manager para Linux y UNIX, pero debe registrar manualmente los proveedores personalizados. Utilice la siguiente línea de comandos para registrar el proveedor: `/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`.  

3.  Después de registrar el nuevo proveedor, pruebe el proveedor mediante la herramienta **omicli** . La herramienta de **omicli** se instala en cada equipo Linux y UNIX al instalar el cliente de Configuration Manager para Linux y UNIX. Por ejemplo, donde **XYZ_MyProvider** es el nombre del proveedor que creó, ejecute el siguiente comando en el equipo: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Para obtener información acerca de **omicli** y probar los proveedores personalizados, consulte la Guía de introducción de OMI.  

> [!TIP]  
>  Utilice la distribución de software para implementar proveedores personalizados y registrar proveedores personalizados en cada equipo cliente Linux y UNIX.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Habilite la nueva clase de inventario en Configuration Manager:  
 Para que Configuration Manager pueda informar sobre el inventario que notifica el nuevo proveedor en equipos Linux y UNIX, debe importar el archivo Managed Object Format (MOF) que define el esquema del proveedor personalizado.  

 Para importar un archivo MOF personalizado en Configuration Manager, vea [Cómo configurar el inventario de hardware](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
