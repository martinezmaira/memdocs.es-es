---
title: Requisitos de la infraestructura de OSD
titleSuffix: Configuration Manager
description: Obtenga información sobre las dependencias de producto externas y los requisitos para la implementación de SO en Configuration Manager
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9bb07bd2b82a9411bc527d04a9a64a0bb6e12f8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697677"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Requisitos de infraestructura para la implementación de SO en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La implementación de SO en Configuration Manager tiene dependencias externas y dependencias dentro del producto. Use este artículo para facilitar la preparación de la infraestructura de implementación de SO.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Dependencias externas a Configuration Manager  

En esta sección se proporciona información sobre herramientas externas, kits de instalación y versiones de sistema operativo necesarias para implementar sistemas operativos en Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  

Windows Assessment and Deployment Kit (ADK) es un conjunto de herramientas y documentación que admiten la configuración e implementación de Windows. Configuration Manager usa Windows ADK para automatizar acciones como la instalación de Windows, la captura de imágenes y la migración de datos y perfiles de usuario.  

Vea los siguientes artículos para más información:  

- [Escenarios de Windows ADK para Windows 10 para profesionales de TI](/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Descargar Windows ADK para Windows 10](/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Asegúrese de descargar **Windows ADK para Windows 10** y el **complemento de Windows PE para el ADK**.

- [Compatibilidad con Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Sistemas de sitio
Windows ADK es un requisito previo para estos servidores de sistemas de sitio:

- El servidor de sitio del sitio de nivel superior en la jerarquía  

- El servidor de sitio de cada sitio principal en la jerarquía  

- Cada instancia del proveedor de SMS  


> [!NOTE]  
> Instale manualmente Windows ADK en cada servidor de sitio antes de instalar el sitio de Configuration Manager.  

#### <a name="windows-adk-features"></a>Características de Windows ADK
Instale estas características de Windows ADK:  

-   Herramienta de migración de estado de usuario (USMT)  

    > [!Note]  
    > No se necesita USMT en el proveedor de SMS.

-   Herramientas de implementación de Windows  

-   Entorno de preinstalación de Windows (Windows PE)  

    > [!Important]  
    > A partir de Windows 10 versión 1809, Windows PE es un instalador independiente. Aparte de esto, no hay ninguna diferencia funcional.<!--SCCMDocs-pr issue 2908-->  

Para obtener una lista de las versiones de Windows 10 ADK que se pueden usar con otras versiones de Configuration Manager, vea [Compatibilidad con Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>Herramienta de migración de estado de usuario (USMT)  

Configuration Manager usa un paquete USMT que incluye los archivos de código fuente de USMT 10 para capturar y restaurar el estado de usuario como parte de la implementación de SO. El programa de instalación de Configuration Manager en el sitio de nivel superior crea automáticamente el paquete USMT. USMT 10 captura el estado de usuario de Windows 7, Windows 8, Windows 8.1 y Windows 10.  

Vea los siguientes artículos para más información:  

- [Escenarios de migración habituales para USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Administrar el estado de usuario](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE se usa para que las imágenes de arranque inicien un equipo. Es una versión de Windows con servicios limitados que se usa durante la preinstalación y la implementación de Windows. En la lista siguiente se incluyen las versiones admitidas de Windows ADK para Configuration Manager (Rama actual):  

#### <a name="windows-adk-version"></a>Versión de Windows ADK  
Windows ADK para Windows 10 Para obtener más información, vea [Compatibilidad con Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Versiones admitidas de Windows PE para imágenes de arranque que no se pueden personalizar desde la consola de Configuration Manager  
Windows PE 3.1<sup>1</sup> y Windows PE 5  

<sup>1</sup> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE 3.1. Instale el complemento de AIK de Windows para Windows 7 SP1 a fin de actualizar AIK de Windows para Windows 7 (basado en Windows PE 3) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Descargue el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

Por ejemplo, si tiene Configuration Manager, puede personalizar imágenes de arranque desde Windows ADK para Windows 10 (basado en Windows PE 10) mediante la consola de Configuration Manager. En cambio, aunque se admiten imágenes de arranque basadas en Windows PE 5, debe personalizarlas desde otro equipo y usar la versión de DISM instalada con Windows ADK para Windows 8. Después, agregue la imagen de arranque a la consola de Configuration Manager. Para obtener más información sobre los pasos para personalizar una imagen de arranque (agregar componentes y controladores adicionales), habilitar la compatibilidad con comandos en la imagen de arranque, agregar la imagen de arranque a la consola de Configuration Manager y actualizar los puntos de distribución con la imagen de arranque, consulte [Personalizar imágenes de arranque](../get-started/customize-boot-images.md). Para obtener más información sobre las imágenes de arranque, consulte [Administrar imágenes de arranque](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS es necesario para el punto de actualización de software, que es necesario para instalar las actualizaciones de software durante la implementación de SO. Para obtener más información, vea [Instalar y configurar un punto de actualización de software](../../sum/get-started/install-a-software-update-point.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) en los servidores de sistema de sitio  

Se necesita IIS para el punto de distribución, el punto de migración de estado y el punto de administración. Para obtener más información, consulte [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  


### <a name="windows-deployment-services-wds"></a>Servicios de implementación de Windows (WDS)  

En la versión 1802 y anteriores, WDS es necesario para las implementaciones de PXE. A partir de la versión 1806, puede habilitar PXE en un punto de distribución sin WDS. Para obtener más información, vea [Servicios de implementación de Windows](#BKMK_WDS) en este artículo. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo de configuración dinámica de host (DHCP)  

Se requiere DHCP para implementaciones de PXE. Debe tener un servidor DHCP en funcionamiento con un host activo para implementar sistemas operativos mediante PXE. Para obtener más información sobre las implementaciones de PXE, consulte [Usar PXE para implementar Windows a través de la red](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos y configuraciones de disco duro compatibles  

Para obtener más información sobre las versiones de SO y las configuraciones de disco duro compatibles con Configuration Manager al implementar sistemas operativos, vea [Sistemas operativos compatibles](#BKMK_SupportedOS) y [Configuraciones de disco compatibles](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Controladores de dispositivos de Windows  

Se pueden usar controladores de dispositivo de Windows cuando se instala el sistema operativo en el equipo de destino. También se usan cuando se ejecuta Windows PE en una imagen de arranque. Para obtener más información, consulte [Administrar controladores](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Dependencias de Configuration Manager  

En esta sección se proporciona información sobre los requisitos previos para la implementación de SO de Configuration Manager.  


### <a name="os-image"></a>Imagen del sistema operativo  

Las imágenes de SO en Configuration Manager se almacenan en el formato de archivo Windows Imaging (WIM). Representan una colección comprimida de carpetas y archivos de referencia. Estas imágenes son necesarias para instalar y configurar correctamente un sistema operativo en un equipo. Para más información, vea [Administrar imágenes de SO](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Catálogo de controladores  

Para implementar un controlador de dispositivo, impórtelo, habilítelo y establézcalo como disponible en un punto de distribución al que el cliente de Configuration Manager pueda tener acceso. Para obtener más información sobre el catálogo de controladores, consulte [Administrar controladores](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Punto de administración  

Los puntos de administración transfieren información entre los clientes y el sitio de Configuration Manager. El cliente usa un punto de administración para ejecutar la secuencia de tareas para completar la implementación de SO. Para obtener más información sobre las secuencias de tareas, consulte [Planeación de consideraciones para la automatización de tareas](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Punto de distribución  

Los puntos de distribución se usan en la mayoría de las implementaciones para almacenar los datos que se usan para implementar un sistema operativo, como los paquetes de imagen o controladores. Las secuencias de tareas normalmente recuperan datos de un punto de distribución para implementar el sistema operativo. Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).  


### <a name="pxe-enabled-distribution-point"></a>Punto de distribución habilitado con PXE  

Para realizar las implementaciones iniciadas con PXE, configure un punto de distribución que acepte las solicitudes de PXE de los clientes. Para obtener más información, vea [Configuración de puntos de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Punto de distribución habilitado con multidifusión  

Para optimizar las implementaciones de SO mediante multidifusión, configure un punto de distribución que admita multidifusión. Para obtener más información, vea [Configuración de puntos de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Punto de migración de estado  

Al capturar y restaurar datos de estado de usuario para las implementaciones en paralelo y de actualización, configure un punto de migración de estado para almacenar los datos de estado de usuario en otro equipo.  

Para obtener más información sobre cómo configurar el punto de migración de estado, consulte [Punto de migración de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

Para más información sobre cómo capturar y restaurar el estado de usuario, vea [Administrar el estado de usuario](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Punto de servicios de informes  

Para usar informes de Configuration Manager para las implementaciones de SO, instale y configure un punto de notificación. Para obtener más información, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Permisos de seguridad para las implementaciones de SO  

El rol de seguridad **Administrador de implementaciones de sistema operativo** es un rol integrado que no se puede cambiar. Sin embargo, puede copiar el rol, realizar cambios y, a continuación, guardar estos cambios como un nuevo rol de seguridad personalizado. Estos son algunos de los permisos que se aplican directamente a las implementaciones de SO:  

- **Paquete de imágenes de arranque**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

- **Controladores de dispositivo**: crear, eliminar, modificar, modificar carpeta, modificar informe, mover objeto, leer, ejecutar informe  

- **Paquete de controladores**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

- **Imagen del sistema operativo**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

- **Paquete de actualización del sistema operativo**: crear, eliminar, modificar, modificar carpeta, mover objeto, leer, establecer ámbito de seguridad  

- **Paquete de secuencia de tareas**: crear, crear medio de secuencia de tareas, eliminar, modificar, modificar carpeta, modificar informe, mover objeto, leer, ejecutar informe, establecer ámbito de seguridad  

Para obtener más información, vea [Crear roles de seguridad personalizados](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Ámbitos de seguridad para las implementaciones de SO  

Use ámbitos de seguridad para proporcionar a los usuarios administrativos acceso a los objetos protegibles que se usan en las implementaciones de SO, como las imágenes de SO y de arranque, los paquetes de controladores y los paquetes de secuencias de tareas. Para obtener más información, consulte [Ámbitos de seguridad](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Servicios de implementación de Windows  

En la versión 1802 y anteriores, para admitir PXE o multidifusión, Servicios de implementación de Windows (WDS) debe instalarse en el mismo servidor que los puntos de distribución que se configuran. WDS se incluye en el SO del servidor. En las implementaciones de PXE, WDS es el servicio que realiza el arranque de PXE. Si el punto de distribución se instala y se habilita para PXE, Configuration Manager instala un proveedor en WDS que emplea las funciones de arranque de PXE de WDS.  

A partir de la versión 1806, puede habilitar PXE en un punto de distribución sin WDS. Para obtener más información, consulte la opción **Habilitar un respondedor PXE sin servicios de implementación de Windows** en [Instalar y configurar puntos de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


> [!NOTE]  
>  Si el servidor requiere un reinicio, puede que la instalación de WDS no se realice correctamente. 


### <a name="wds-requirements"></a>Requisitos de WDS  

-   La instalación de WDS en el servidor requiere que el administrador sea miembro del grupo Administradores locales.  

-   El servidor de WDS debe ser miembro de un dominio de Active Directory o de un controlador de dominio para un dominio de Active Directory. Todas las configuraciones de dominio y de bosque de Windows son compatibles con WDS.  

-   Si el proveedor está instalado en un servidor remoto, instale WDS en el servidor de sitio y el proveedor remoto.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> Consideraciones si se tiene WDS y DHCP en el mismo servidor  

Si planea hospedar conjuntamente el punto de distribución en un servidor que ejecuta DHCP, tenga en cuenta las siguientes consideraciones sobre configuración:  

-   Debe tener un servidor DHCP en funcionamiento con un ámbito activo. WDS usa PXE, que requiere un servidor DHCP.  

-   Se necesita un servidor DNS para ejecutar WDS.  

-   Los siguientes puertos UDP deben estar abiertos en el servidor de WDS:  

    -   Puerto 67 (DHCP)  

    -   Puerto 69 (TFTP)  

    -   Puerto 4011 (PXE)  

    > [!NOTE]  
    >  Si se requiere autorización de DHCP en el servidor, será necesario que el puerto 68 del cliente DHCP esté abierto en el servidor.  

-   DHCP y WDS requieren el puerto número 67. Si WDS y DHCP se hospedan conjuntamente, se puede mover DHCP o el punto de distribución que esté configurado para PXE a otro servidor. O bien, puede usar el procedimiento siguiente para configurar el servidor de WDS para que escuche en otro puerto.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Para configurar el servidor de WDS para que escuche en otro puerto  

1.  Modifique la siguiente Clave del registro:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Establezca el valor del Registro **UseDHCPPorts** en **0**.  

3.  Para que la nueva configuración surta efecto, ejecute el siguiente comando en el servidor:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> En la versión 1810 y anterior, no se permite usar el respondedor del entorno PXE sin WDS en servidores que también ejecutan un servidor DHCP.
>
> A partir de la versión 1902, cuando se habilita un respondedor del entorno PXE en un punto de distribución sin Servicio de implementación de Windows, ahora puede estar en el mismo servidor que el servicio DHCP. Para más información, consulte [Configurar al menos un punto de distribución para aceptar solicitudes del entorno PXE](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> Sistemas operativos compatibles  

Todos los sistemas operativos de Windows enumerados como clientes compatibles en [Sistemas operativos compatibles con clientes y dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) se admiten en las implementaciones de SO.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> Configuraciones de disco compatibles  

Las combinaciones de configuración de disco duro en los equipos de referencia y de destino compatibles con la implementación de SO de Configuration Manager se muestran en la tabla siguiente:  

|Configuración de disco duro del equipo de referencia|Configuración de disco duro del equipo de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volumen simple en un disco dinámico|Volumen simple en un disco dinámico|  

Configuration Manager admite la captura de una imagen de SO solamente desde equipos que estén configurados con volúmenes simples. No hay soporte para las configuraciones de disco duro siguientes:  

-   Volúmenes distribuidos  

-   Volúmenes seccionados (RAID 0)  

-   Volúmenes reflejados (RAID 1)  

-   Volúmenes de paridad (RAID 5)  

En la tabla siguiente se muestra una configuración de disco duro adicional en los equipo de referencia y de destino que no se admite con la implementación de SO de Configuration Manager.  

|Configuración de disco duro del equipo de referencia|Configuración de disco duro del equipo de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinámico|  



## <a name="next-steps"></a>Pasos siguientes

- [Preparar los roles de sistema de sitio para la implementación de SO](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Preparar la implementación de SO](../get-started/prepare-for-operating-system-deployment.md)