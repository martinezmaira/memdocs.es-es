---
title: Funcionalidades de Technical Preview 1511
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 475cb4e9a4c6c3b90582210b0ebf4a7f69e9f643
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694293"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Funciones de Technical Preview 1511 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1511 de Technical Preview de Configuration Manager. Esta versión es una instalación de línea base de la Technical Preview que puede usar para instalar un nuevo sitio de Technical Preview o para actualizar desde una versión anterior de la Technical Preview.   Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

Estas son las nuevas características que puede probar con esta versión.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Integración con Windows Update for Business en Windows 10  
 Configuration Manager tiene ahora la capacidad de diferenciar entre un equipo de Windows 10 que esté directamente conectado a través de Windows Update for Business (WUfB) y aquellos equipos conectados a WSUS para obtener actualizaciones de Windows 10.  Aquellos equipos conectados a través de WUfB pueden administrar las actualizaciones en la cadencia establecida por un usuario administrador a través de las directivas de grupo o las directivas de MDM; asimismo, estas actualizaciones se pueden instalar directamente desde WUfB.    
Configuration Manager no podrá informar sobre el estado de cumplimiento (incluyendo actualizaciones de Windows o de definiciones) de los equipos conectados a través de WUfB. Asimismo, Configuration Manager no podrá implementar actualizaciones de Microsoft o de terceros en estos equipos.  

 **Requisitos previos para este escenario:**  

-   Versión 1511 o posterior de Windows 10 Desktop Pro o Windows 10 Enterprise Edition  

-   Equipos que serán administrados a través de [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx).  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar la siguiente tarea y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo ha funcionado:  

1.  Si lo tiene habilitado, deshabilite el agente de Windows Update para que no examine nada con WSUS.   
    La clave del registro **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** se puede establecer para indicar si el equipo está realizando algún análisis con WSUS o Windows Update.  Cuando el valor es 2, no se realiza el análisis con WSUS.  

2.  Tome nota del nuevo atributo **UseWUServer**que se encuentra en el nodo **Windows Update** del Explorador de recursos de Configuration Manager.  

3.  Cree una colección basada en el atributo **UseWUServer** para todos los equipos que estén conectados a través de WUfB para conseguir actualizaciones.  

4.  Cree una configuración de agente cliente para deshabilitar el flujo de trabajo de la actualización de software e implementar la configuración en la colección de equipos que están conectados directamente a WUfB.  

5.  Los equipos que se administran a través de WUfB, mostrarán el valor **Desconocido** en el estado de cumplimiento y no se tendrán en cuenta como parte del porcentaje total de cumplimiento.  

##  <a name="managing-office-365-proplus-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Administración de la actualización de cliente de Office 365 ProPlus a través de Configuration Manager  
 Configuration Manager tiene ahora la capacidad de administrar actualizaciones de cliente para equipos de escritorio de Office 365 mediante el flujo de trabajo de administración de actualizaciones de software de Configuration Manager.    
Cuando Microsoft publica una nueva actualización de cliente para equipos de escritorio de Office 365 para Windows Server Updates Services (WSUS), Configuration Manager puede sincronizar la actualización con su catálogo si la actualización de Office 365 está configurada para ser parte de la sincronización del catálogo.  El servidor de sitio de Configuration Manager descarga las actualizaciones de cliente de Office 365 y distribuye el paquete a los puntos de distribución de Configuration Manager.  Luego, el cliente de Configuration Manager informa a los clientes para equipos de escritorio de Office 365 de dónde obtener las actualizaciones y de cuándo iniciar el proceso de instalación de las mismas.  

**Requisitos previos para este escenario:**  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar la siguiente tarea y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo ha funcionado:  

1. Puede sincronizar actualizaciones de Office 365 con el servidor de sitio de Configuration Manager y verlas desde la consola de Configuration Manager.  

2. Puede aprobar e implementar correctamente actualizaciones de Office 365.  

3. Puede descargar correctamente las actualizaciones de Office 365 para los clientes.  

4. Puede comprobar el funcionamiento de las actualizaciones de Office 365 supervisándolas o creando informes con la consola.  

   Para obtener los pasos detallados, vea [Administrar las actualizaciones de cliente de Office 365 con Configuration Manager Technical Preview](https://technet.microsoft.com/library/mt628083.aspx).  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> Compatibilidad con SQL Server AlwaysOn para bases de datos de alta disponibilidad  
 Configuration Manager ahora admite el uso de grupos de disponibilidad de SQL Server AlwaysOn para hospedar la base de datos del sitio.  Cuando instale un sitio nuevo, podrá indicar al programa de instalación que use el grupo de disponibilidad en lugar de una instancia normal de SQL Server.  

> [!NOTE]  
>  La configuración y el uso correctos de los grupos de disponibilidad requiere destreza en la configuración de grupos de disponibilidad de SQL Server y se basa en la documentación y los procedimientos proporcionados en la biblioteca de documentación de SQL Server.  

El proceso general de alto nivel necesario para configurar y usar grupos de disponibilidad incluye:  

1.  configurar el grupo de disponibilidad en SQL Server.  

2.  Instalar un nuevo sitio de Configuration Manager y, durante la instalación, indicarle que use el grupo de disponibilidad mediante la especificación del punto de conexión de los grupos.  

**Requisitos previos para este escenario:**  

-   Requiere una versión de SQL Server compatible con Configuration Manager Technical Preview.  

-   Debe crear y configurar el grupo de disponibilidad de SQL Server para instalar Configuration Manager  

-   El grupo de disponibilidad debe tener una réplica principal y tener hasta dos réplicas secundarias sincrónicas.  

-   El grupo de disponibilidad debe tener al menos un extremo.  

-   Debe tener una ubicación de red a la que puedan acceder todos los SQL Server del grupo de disponibilidad. Esta ubicación la usa el programa de instalación al configurar el grupo de disponibilidad y se puede quitar tras finalizar la instalación.  

**Problemas conocidos de esta versión:**  

-   No puede agregar correctamente un nuevo miembro de réplica a un grupo de disponibilidad que ya está en uso como una base de datos del sitio. En su lugar, debe volver a instalar el sitio después de agregar el nuevo miembro de réplica.  

-   Para este escenario, puede necesitar instalar el **cliente nativo de SQL Server 2012** ([desde SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065)) en el servidor de punto de administración. Esto evita los errores de conexión de SQL (que se registran en **mp_getauth.log** en el servidor de punto de administración).  

### <a name="try-it-out"></a>Haga la prueba  
Intente realizar las siguientes tareas y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo han funcionado:  

-   Puedo instalar un sitio primario que usa un servidor de bases de datos configurado para grupos de disponibilidad de SQL AlwaysOn.  

-   He logrado realizar la conmutación por error de mi grupo de disponibilidad de SQL AlwaysOn a una nueva réplica en el grupo y el sitio primario sigue funcionando.  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configuración de SQL Server AlwaysOn para Configuration Manager  
 Use los siguientes procedimientos para crear y configurar por primera vez el grupo de disponibilidad y, luego, instale un nuevo sitio de Configuration Manager que use el grupo de disponibilidad.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Para crear el grupo de disponibilidad de SQL Server AlwaysOn  
El proceso para [crear un grupo de disponibilidad de SQL Server](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) se documenta en la biblioteca de documentación de SQL Server.  Cuando cree el grupo de disponibilidad, asegúrese de que se cumplan los siguientes requisitos para poder usarlo con Configuration Manager:  

-   Un máximo de tres miembros:  

    -   Una réplica principal y hasta dos réplicas secundarias  

    -   Las réplicas secundarias deben ser sincrónicas.  

        > [!TIP]  
        >  Se recomienda configurar las réplicas secundarias para que sean de solo lectura. Esto le permite usar una réplica secundaria para funciones como la generación de informes al tiempo que mantiene el rendimiento de la réplica principal para las operaciones del sitio.  

-   Al menos un extremo. El nombre virtual de este punto de conexión se usará al instalar el sitio de Configuration Manager.  

    > [!TIP]  
    >  Aunque el grupo puede contener varios puntos de conexión, Configuration Manager solo puede usar uno.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Para instalar un sitio de Configuration Manager que usa el grupo de disponibilidad  
Para instalar un sitio que usa un grupo de disponibilidad de SQL Server:  

1.  Sustituya lo siguiente cuando se lo solicite el programa de instalación de Configuration Manager:  

    -   **Nombre de SQL Server**: escriba el nombre virtual del punto de conexión que configuró al crear el grupo de disponibilidad. El nombre virtual debe ser un nombre DNS completo, como **&lt;servidorPuntodeconexión\>.fabrikam.com**.  

    -   **Instancia**:  este valor debe permanecer en blanco. No hay ninguna instancia en esta configuración.  

    -   **Base de datos**: escriba el nombre de la base de datos que creó en la réplica principal del grupo de disponibilidad.  

2.  A continuación, debe proporcionar una ubicación de red a la que puedan acceder todos los SQL Server del grupo.  

    -   La cuenta de equipo y la cuenta de servicio de cada SQL Server requieren acceso con control total en esta ubicación.  

    -   Esta ubicación solo se usa durante la instalación y puede dejar de compartirla o eliminarla tras completar el programa de instalación, una vez está instalado el sitio.  

3.  Después de proporcionar esta información, complete la instalación con el proceso y las configuraciones normales.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> Servicio de un clúster de servidores  
Ahora puede crear una recopilación que contenga los servidores de un clúster y, a continuación, configurar las opciones del clúster que se usarán al implementar actualizaciones en el clúster. Puede controlar el porcentaje de los servidores que están en línea en cualquier momento, así como configurar scripts de PowerShell anteriores y posteriores a la implementación para ejecutar acciones personalizadas.  

**Problemas conocidos de esta versión:**  

-   No está disponible la generación de informes para comprobar el estado de la implementación de actualizaciones de software para servidores del clúster.  

-   La opción de secuencia de mantenimiento de la página **Configuración de clúster** está deshabilitada y no está disponible en esta versión.  

### <a name="try-it-out"></a>Haga la prueba  
Intente realizar la siguiente tarea y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo ha funcionado:  

-   Puedo crear una recopilación que representa un clúster de servidores. Para esta prueba puede configurar las reglas de pertenencia de la recopilación para tener 2 máquinas en esta recopilación.  

-   Puedo especificar que solo el 50% de los servidores del clúster pueden estar sin conexión en cualquier punto del mantenimiento del clúster. Use los scripts de ejemplo del procedimiento para especificar los scripts anteriores y posteriores a la implementación.  

-   Implemente una actualización en esta recopilación. Revise los archivos start.txt y end.txt en C:\temp y compruebe las horas de inicio y finalización de la implementación en los servidores del clúster. Revise el archivo UpdatesDeployment.log para obtener más información.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Para crear una recopilación para un clúster de servidores  

1.  [Cree una colección de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contenga los servidores del clúster.  

2.  En el área de trabajo **Activos y compatibilidad**, haga clic en **Colecciones de dispositivos**, haga clic con el botón derecho en la colección que contiene los servidores del clúster y, luego, haga clic en **Propiedades**.  

3.  En la pestaña **General**, seleccione **Todos los dispositivos forman parte del mismo grupo de servidores** y haga clic en **Configuración**.  

4.  En la página **Configuración del clúster**, seleccione el porcentaje de servidores que se pueden desconectar a la vez para instalar las actualizaciones de software. Un servidor de clúster se puede desconectar cada vez sin tener en cuenta el porcentaje que proporcione. Configuration Manager redondeará a la baja al seleccionar el número de servidores que se va a atender al mismo tiempo. Por ejemplo, si elige el 51 % y hay 4 servidores en el clúster, se desconectarán 2 servidores al mismo tiempo.  

5.  Especifique si quiere usar un script anterior a la implementación (purga de nodo) o posterior a la implementación (reanudación de nodo).  

    > [!TIP]  
    >  Los siguientes son ejemplos que puede usar en las pruebas para los scripts anteriores a la implementación y posteriores a la implementación que escriben la hora actual en un archivo de texto:  
    >   
    >  **Anterior a la implementación**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Posterior a la implementación**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Para implementar actualizaciones de software en el clúster de servidores  

1.  [Implemente actualizaciones de software](https://technet.microsoft.com/library/gg712304.aspx) en la colección del clúster de servidores.  

2.  [Supervise la implementación de la actualización de software](https://technet.microsoft.com/library/gg712304.aspx).  
