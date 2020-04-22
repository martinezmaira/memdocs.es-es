---
title: Administración de puntos de distribución
titleSuffix: Configuration Manager
description: Use puntos de distribución para hospedar el contenido que implemente en dispositivos y usuarios.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1cc931bd0e02be66f608db11e0052fde571a427
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701683"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Instalar y configurar puntos de distribución en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Instale puntos de distribución de Configuration Manager para hospedar el contenido que se implementa en dispositivos y usuarios. Cree grupos de puntos de distribución para simplificar cómo se administran los puntos de distribución y cómo se distribuye el contenido en los puntos de distribución.  

Para *instalar un nuevo punto de distribución*, use el asistente para instalación. Para obtener más información, vea [Instalar un punto de distribución](#bkmk_install). Para *administrar las propiedades de un punto de distribución existente*, edite las propiedades del punto de distribución. Para obtener más información, vea [Configuración de puntos de distribución](#bkmk_configs).

Configure la mayoría de las opciones del punto de distribución con uno de los métodos. Algunas opciones de configuración solo están disponibles cuando se instala o se edita, pero no en ambos casos:  

- Opciones que solo están disponibles cuando se instala un punto de distribución:  

    - **Permitir que Configuration Manager instale IIS en el equipo del punto de distribución**

    - **Configurar el espacio de la unidad para el punto de distribución**  

- Pasos de configuración que solo están disponibles cuando se editan las propiedades de un punto de distribución:  

    - **Administrar relaciones de grupo de puntos de distribución**  

    - **Ver el contenido implementado en el punto de distribución**  

    - **Configurar los límites de frecuencia de las transferencias de datos a los puntos de distribución**  

    - **Configurar las programaciones de las transferencias de datos a los puntos de distribución**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a> Instalar un punto de distribución  

Seleccione un servidor de sistema de sitio como un punto de distribución antes de que el contenido esté disponible para los equipos cliente. Asigne un punto de distribución al menos a un [grupo de límites](boundary-groups.md#distribution-points) antes de que los equipos cliente locales puedan usar ese punto de distribución como ubicación de origen del contenido. Agregue el rol de punto de distribución a un nuevo servidor de sistema de sitio, o bien agréguelo a un servidor de sistema de sitio existente.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a> Requisitos previos

Cuando instala un nuevo punto de distribución, usa un asistente de instalación que le guía a través de la configuración disponible. Antes de comenzar, tenga en cuenta los requisitos previos siguientes:  

- Debe tener los siguientes permisos de seguridad para crear y configurar un punto de distribución:  

    - **Leer** en el objeto **Punto de distribución**  

    - **Copiar en punto de distribución** en el objeto **Punto de distribución**  

    - **Modificar** en el objeto **Sitio**  

    - **Administrar certificados para implementación de sistema operativo** en el objeto **Sitio**  

- Instale Internet Information Services (IIS) en el servidor de Windows donde se hospede el punto de distribución. O bien, al instalar el rol de sistema de sitio, Configuration Manager puede instalar y configurar IIS automáticamente.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a> Procedimiento para instalar un punto de distribución  

Siga este procedimiento para agregar un nuevo punto de distribución. Para cambiar la configuración de un punto de distribución existente, vea la sección [Configurar un punto de distribución](#bkmk_configs).  

Empiece con el procedimiento general para [Instalar roles de sistema de sitio](install-site-system-roles.md). Seleccione el rol de **punto de distribución** en la página **Selección de rol del sistema** del Asistente para crear servidor de sistema de sitio. Esta acción agregará las páginas siguientes al asistente:  

- [Punto de distribución](#bkmk_config-general)
- [Comunicación](#bkmk_config-comm)
- [Configuración de la unidad](#bkmk_config-drive)
- [Punto de distribución de extracción](#bkmk_config-pull)
- [Configuración de PXE](#bkmk_config-pxe)
- [Multidifusión](#bkmk_config-multicast)
- [Validación de contenido](#bkmk_config-valid)
- [Grupos de límites](#bkmk_config-boundary)

> [!Important]  
> Las siguientes opciones de configuración solo están disponibles al instalar un punto de distribución:  
>
> - **Permitir que Configuration Manager instale IIS en el equipo del punto de distribución**  
>
> - **Configurar el espacio de la unidad para el punto de distribución**  

Para obtener más información sobre las páginas del asistente específicas del rol de punto de distribución, vea la sección [Configurar un punto de distribución](#bkmk_configs). Por ejemplo, para instalar el punto de distribución como un [punto de distribución de extracción](#bkmk_config-pull), seleccione la opción **Habilitar este punto de distribución para extraer contenido desde otros puntos de distribución**. Después, realice las configuraciones adicionales necesarias para los puntos de distribución de extracción.  

Cuando complete el Asistente para crear servidor de sistema de sitio, el sitio agregará el rol de punto de distribución al servidor de sistema de sitio.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Administrar grupos de puntos de distribución  

Los grupos de puntos de distribución proporcionan una agrupación lógica de los puntos de distribución para la distribución de contenido. Use estos grupos para administrar y supervisar contenido desde una ubicación central para los puntos de distribución que abarcan varios sitios. Tenga en cuenta lo siguiente:

- Agregue uno o más puntos de distribución de cualquier sitio en la jerarquía a un grupo de puntos de distribución.  

- Agregue un punto de distribución a más de un grupo de puntos de distribución.  

- Al distribuir contenido a un grupo de puntos de distribución, Configuration Manager distribuye el contenido a todos los puntos de distribución que pertenezcan al grupo.  

- Si agrega un punto de distribución al grupo después de una distribución de contenido inicial, Configuration Manager distribuye automáticamente el contenido al nuevo miembro del punto de distribución.  

- Asocie una colección a un grupo de puntos de distribución. Al distribuir contenido a esa colección, Configuration Manager determina qué grupos se asocian a la colección. Después, distribuye el contenido a todos los puntos de distribución que sean miembros de esos grupos.  

    > [!NOTE]  
    > Si, después de distribuir contenido a una colección, asocia la colección a otro grupo de puntos de distribución, debe redistribuir el contenido a la colección antes de distribuirlo al nuevo grupo de puntos de distribución.  

En las secciones siguientes, se muestran los procedimientos de acciones siguientes para administrar grupos de puntos de distribución:  

- [Crear y configurar un grupo de puntos de distribución](#bkmk_dpgroup-create)
- [Modificar un grupo de puntos de distribución existente](#bkmk_dpgroup-modify)
- [Agregar puntos de distribución seleccionados a grupos de puntos de distribución existentes](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a> Procedimiento para crear y configurar un grupo de puntos de distribución  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Grupos de puntos de distribución**.  

2. En la cinta de opciones, seleccione **Crear grupo**.  

3. En la ventana Crear nuevo grupo de puntos de distribución, escriba el **Nombre** y, de manera opcional, una **Descripción** del grupo.  

4. En la pestaña **Miembros**, seleccione **Agregar**.  

5. En la ventana Agregar puntos de distribución, seleccione uno o más puntos de distribución para agregarlos como miembros del grupo. Después, haga clic en **Aceptar**.  

6. Si es necesario, cambie a la pestaña **Colecciones** de la ventana Crear nuevo grupo de puntos de distribución y seleccione **Agregar**.  

7. En la ventana Seleccionar colecciones, seleccione las colecciones que quiera asociar al grupo de puntos de distribución y, después, seleccione **Aceptar**.  

8. En la ventana Crear nuevo grupo de puntos de distribución, seleccione **Aceptar** para crear el grupo.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Crear un grupo a partir de un punto de distribución existente

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**. Seleccione uno o más puntos de distribución para agregarlos a un nuevo grupo de puntos de distribución.  

2. En la cinta de opciones, seleccione **Agregar elementos seleccionados** y, después, seleccione **Agregar elementos seleccionados a grupo de puntos de distribución nuevo**.  

Este proceso rellena automáticamente la pestaña **Miembros** de la ventana “Crear nuevo grupo de puntos de distribución” con los servidores seleccionados.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a> Procedimiento para modificar un grupo de puntos de distribución existente  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Grupos de puntos de distribución**.  

2. Seleccione un grupo de puntos de distribución existente que quiera modificar. En la cinta, seleccione **Propiedades**.  

3. Para asociar nuevas colecciones a este grupo, vaya a la pestaña **Colecciones** y elija **Agregar**. Seleccione las colecciones y, después, elija **Aceptar**.  

4. Para agregar nuevos puntos de distribución a este grupo, vaya a la pestaña **Miembros** y elija **Agregar**. Seleccione los puntos de distribución y, luego, elija **Aceptar**.  

5. Elija **Aceptar** para guardar los cambios en el grupo de puntos de distribución.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a> Procedimiento para agregar puntos de distribución seleccionados a grupos de puntos de distribución existentes  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**. Seleccione uno o más puntos de distribución para agregarlos a un grupo existente.  

2. En la cinta de opciones, seleccione **Agregar elementos seleccionados** y, después, seleccione **Agregar elementos seleccionados a grupos de puntos de distribución existentes**.  

3. En **Grupos de puntos de distribución disponibles**, seleccione los grupos a los que quiera agregar los puntos de distribución seleccionados como miembros. Después, haga clic en **Aceptar**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a> Reasignar un punto de distribución

<!-- 1306937 -->

Muchos clientes tienen grandes infraestructuras de Configuration Manager y reducen los sitios primarios o secundarios para simplificar su entorno. Tienen que conservar los puntos de distribución en las ubicaciones de las sucursales para entregar el contenido a los clientes administrados. Estos puntos de distribución a menudo contienen varios terabytes o más de contenido. Este contenido es costoso en términos de tiempo y ancho de banda de red para distribuirlo entre estos servidores remotos.

Esta característica permite volver a asignar un punto de distribución a otro sitio primario sin redistribuir el contenido. Esta acción actualiza la asignación del sistema de sitio mientras se conserva todo el contenido en el servidor. Si necesita reasignar varios puntos de distribución, primero ejecute esta acción en un único punto de distribución. Después, continúe con otros servidores, de uno en uno.

> [!IMPORTANT]  
> El servidor de destino solo puede hospedar el rol de punto de distribución. Si el servidor de sistema de sitio hospeda otro rol de servidor de Configuration Manager, como el punto de migración de estado, el punto de distribución no se puede reasignar. No se puede reasignar un punto de distribución de nube.

Antes de reasignar un punto de distribución, agregue la cuenta de equipo del servidor del sitio de destino al grupo de administradores locales en el servidor de punto de distribución de destino.

Siga estos pasos para volver a asignar un punto de distribución:

1. En la consola de Configuration Manager, conéctese al sitio de administración central.  

2. Vaya al área de trabajo **Administración** y haga clic en el nodo **Puntos de distribución**.  

3. Haga clic con el botón derecho en el punto de distribución de destino y seleccione **Reasignar punto de distribución**.  

4. Seleccione el servidor de sitio de destino y el código de sitio al que quiera reasignar este punto de distribución.  

Supervise la reasignación del mismo modo que cuando se agrega un rol nuevo. El método más sencillo consiste en actualizar la vista de consola después de varios minutos. Agregue la columna de código de sitio a la vista. Este valor cambia cuando Configuration Manager reasigna el servidor. Si se intenta realizar otra acción en el servidor de destino antes de actualizar la vista de consola, se produce un error "objeto no encontrado". Asegúrese de que el proceso ha terminado y actualice la vista de consola antes de iniciar otras acciones en el servidor.

Después de reasignar un punto de distribución, actualice el certificado del servidor. El servidor de sitio nuevo debe volver a cifrar este certificado con la clave pública y almacenarlo en la base de datos del sitio. Para obtener más información, vea la opción **Crear un certificado autofirmado o importar un certificado de cliente PKI para el punto de distribución** en la pestaña [General](#bkmk_config-general) de las propiedades del punto de distribución.

- Para los certificados PKI, no es necesario crear un certificado. Importe el mismo archivo .PFX y escriba la contraseña.  

- Para los certificados autofirmados, ajuste la fecha u hora de expiración para actualizarlos.  

- Si no actualiza el certificado, el punto de distribución seguirá sirviendo contenido, pero las funciones siguientes producirán errores:  

    - Mensajes de validación de contenido (el archivo distmgr.log muestra que no puede descifrar el certificado).  

    - Compatibilidad de PXE para clientes.  

### <a name="tips"></a>Sugerencias

- Realice esta acción desde el sitio de administración central. Esta práctica ayuda con la replicación en los sitios primarios.  

- No distribuya contenido en el servidor de destino y después intente volver a asignarlo. Se puede producir un error en la distribución de las tareas de contenido que están en curso durante el proceso de reasignación, pero se vuelve a intentar de manera normal.  

- Si el servidor también es un cliente de Configuration Manager, asegúrese de reasignar el cliente al sitio primario nuevo. Este paso es especialmente importante para los puntos de distribución de extracción, en los que se usan componentes de cliente para descargar el contenido.  

- Este proceso elimina el punto de distribución de grupo de límites predeterminado del sitio antiguo. Si es necesario, tendrá que agregarlo manualmente al grupo de límites predeterminado del sitio nuevo. Todas las demás asignaciones de grupos de límites se mantienen igual.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a> Modo de mantenimiento

<!--3555754-->

A partir de la versión 1902, puede establecer un punto de distribución en modo de mantenimiento. Habilite el modo de mantenimiento cuando vaya a instalar actualizaciones de software o realizar cambios de hardware en el servidor.

Mientras el punto de distribución está en modo de mantenimiento, presenta estos comportamientos:

- El sitio no distribuye contenido a este punto de distribución.  

- Los puntos de administración no devuelvan la ubicación de este punto de distribución a los clientes.

- Cuando se actualiza el sitio, todavía se actualiza un punto de distribución en modo de mantenimiento.

- Las propiedades del punto de distribución son de solo lectura. Por ejemplo, no se puede cambiar el certificado ni agregar grupos de límites.  

- Cualquier tarea programada, como la validación de contenido, se sigue ejecutando en la misma programación.

Tenga cuidado con habilitar el modo de mantenimiento en más de un punto de distribución. Si lo hace, podría afectar al rendimiento en los otros puntos de distribución. En función de las configuraciones de grupo de límites, es posible que los clientes hayan aumentado los tiempos de descarga o no puedan descargar contenido.

El modo de mantenimiento no debe ser un estado a largo plazo en ningún punto de distribución. En el caso de las acciones de larga duración, considere la posibilidad de quitar primero el rol de punto de distribución.

> [!NOTE]
> Mientras un punto de distribución esté en modo de mantenimiento, no realice ninguna de las siguientes acciones:<!-- SCCMDocs-pr #4699 -->
>
> - Quitar un rol
> - Reasignación del punto de distribución

### <a name="enable-maintenance-mode"></a>Habilitación del modo de mantenimiento

Para poner un punto de distribución en modo de mantenimiento, la cuenta de usuario requiere el permiso de **modificación** en la clase the **Site**. Por ejemplo, los roles integrados **Administrador de infraestructura** y **Administrador total** tienen este permiso.<!-- SCCMDocs-pr issue #3407 -->

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**.  

2. Seleccione el nodo **Puntos de distribución**.  

3. Seleccione el punto de distribución de destino y elija **Habilitar el modo de mantenimiento** en la cinta de opciones.  

Para ver el estado actual de los puntos de distribución, agregue la columna de "Modo de mantenimiento" al nodo **Puntos de distribución** en la consola.

Para más información sobre cómo automatizar este proceso con el SDK de Configuration Manager, consulte artículo sobre el [método SetDPMaintenanceMode en la clase SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a> Configurar un punto de distribución  

Los puntos de distribución individuales admiten varias configuraciones. Sin embargo, no todos los tipos de puntos de distribución son compatibles con todas las configuraciones. Por ejemplo, los puntos de distribución de nube no admiten implementaciones habilitadas para PXE o multidifusión. Para obtener más información sobre las limitaciones específicas, vea los artículos siguientes:  

- [Usar un punto de distribución basado en la nube](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Usar un punto de distribución de extracción](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

En las secciones siguientes, se describen las configuraciones de puntos de distribución al [instalar uno nuevo](#bkmk_install-procedure) o [editar uno existente](#bkmk_change-procedure):  

- [Configuración general](#bkmk_config-general)
- [Comunicación](#bkmk_config-comm)
- [Configuración de la unidad](#bkmk_config-drive)
- [Configuración del firewall](#bkmk_firewall)
- [Punto de distribución de extracción](#bkmk_config-pull)
- [Configuración de PXE](#bkmk_config-pxe)
- [Multidifusión](#bkmk_config-multicast)
- [Validación de contenido](#bkmk_config-valid)
- [Grupos de límites](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a> Procedimiento para cambiar un punto de distribución

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**.  

2. Seleccione el punto de distribución que quiera configurar. En la cinta, haga clic en **Propiedades**.  

3. Use la información de las secciones siguientes al editar las propiedades del punto de distribución.  

4. Después de realizar los cambios que prefiera, seleccione **Aceptar** para guardar la configuración y cerrar las propiedades del punto de distribución.  

### <a name="general"></a><a name="bkmk_config-general"></a> General  

> [!Note]  
> En la versión 1902 y anteriores, esta página tiene una configuración adicional para HTTP/HTTPS y los certificados. A partir de la versión 1906, esta configuración se encuentra ahora en la página [Comunicación](#bkmk_config-comm).

Las opciones siguientes se encuentran en la página **Punto de distribución** del Asistente para crear servidor de sistema de sitio y en la pestaña **General** de la ventana Propiedades de punto de distribución:  

- **Descripción**: descripción opcional para este rol de punto de distribución.  

- **Instalar y configurar IIS si lo requiere Configuration Manager**: si IIS todavía no está instalado en el servidor, Configuration Manager lo instala y lo configura. Para usar Configuration Manager, es necesario instalar IIS en todos los puntos de distribución. Si no selecciona esta opción e IIS no está instalado en el servidor, primero instale IIS antes de que Configuration Manager pueda instalar correctamente el punto de distribución.  

    > [!NOTE]  
    > Esta opción solo se encuentra en la página **Punto de distribución** del Asistente para crear servidor de sistema de sitio. Solo está disponible al [instalar un nuevo punto de distribución](#bkmk_install-procedure).  

- **Habilitar y configurar BranchCache para este punto de distribución**: elija esta opción para permitir que Configuration Manager configure Windows BranchCache en el servidor de punto de distribución. Para obtener más información, vea [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Ajustar la velocidad de descarga para usar el ancho de banda de red no utilizado (Windows LEDBAT)**<!--1358112-->: a partir de la versión 1806, habilite los puntos de distribución para usar el control de congestión de red. Para obtener más información, vea [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Requisitos mínimos para la compatibilidad con LEDBAT:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager, versión 1806 (versión general)  

        - Windows Server, versión 1709 o posterior  

    - Configuration Manager, versión 1806 con el paquete acumulativo de actualizaciones (4462978), o posterior  

        - Windows Server, versión 1709 o posterior
        - Windows Server 2016 con las actualizaciones KB4132216 y KB4284833

    - Configuration Manager, versión 1810 o posterior:

        - Windows Server, versión 1709 o posterior
        - Windows Server 2016 con las actualizaciones KB4132216 y KB4284833
        - Windows Server 2019  

- **Habilitar este punto de distribución para contenido preconfigurado**: esta opción permite agregar contenido al servidor antes de distribuir software. Como los archivos de contenido ya se encuentran en la biblioteca de contenido, no se transfieren a través de la red al distribuir el software. Para obtener más información, vea [Contenido preconfigurado](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).  

- **Habilitar este punto de distribución para usarlo como servidor de caché con conexión de Microsoft**: a partir de la versión 1906, puede instalar un servidor de caché con conexión de Microsoft en los puntos de distribución. Al almacenar en caché este contenido de forma local, los clientes pueden beneficiarse de la característica de Optimización de entrega y, además, puede ayudar a proteger los vínculos WAN. Para más información, incluidas descripciones de las configuraciones adicionales, vea [Caché con conexión de Microsoft en Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a> Comunicación

> [!Note]  
> A partir de la versión 1906, la siguiente configuración se encuentra en la pestaña **Comunicación**. En la versión 1902 y versiones anteriores, esta configuración está en la pestaña [General](#bkmk_config-general).

Las opciones siguientes se encuentran en la página **Comunicación** del Asistente para crear servidor de sistema de sitio y en la ventana Propiedades de punto de distribución:  

- **Configure cómo se comunican los dispositivos cliente con el punto de distribución**: el uso de **HTTP** o **HTTPS** presenta ventajas e inconvenientes. Para obtener más información, consulte [Prácticas recomendadas de seguridad para la administración de contenido](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

- **Permitir a los clientes conectarse de forma anónima**: esta opción permite especificar si el punto de distribución permite conexiones anónimas de los clientes de Configuration Manager con la biblioteca de contenido.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Crear un certificado autofirmado o importar un certificado de cliente PKI**: Configuration Manager usa este certificado para los siguientes fines:  

    - Autentica el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado.  

    - Al activar la opción **Habilitar compatibilidad de PXE para clientes** de la página **Configuración de PXE**, el punto de distribución lo envía a los equipos con arranque PXE. Después, estos equipos lo usarán para conectarse a un punto de administración durante el proceso de implementación del SO.  

    Al configurar todos los puntos de administración del sitio para HTTP, seleccione la opción **Crear certificado autofirmado**. Al configurar los puntos de administración para HTTPS, use la opción **Importar certificado** desde PKI.  

    Para importar el certificado, busque un archivo PKCS #12 (Public Key Cryptography Standards) válido. El archivo PFX o CER tiene el certificado PKI con los requisitos siguientes de Configuration Manager:  

    - En el uso previsto, se incluye la autenticación de cliente.  

    - Habilitar la exportación de la clave privada  

    > [!TIP]  
    > No existen requisitos específicos para el sujeto del certificado ni el nombre alternativo del firmante (SAN). Si es necesario, use el mismo certificado para varios puntos de distribución.  

    Para obtener más información sobre los requisitos de certificado, vea [Requisitos de certificados PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    Para obtener un ejemplo de implementación de este certificado, vea [Implementar el certificado de cliente para puntos de distribución](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a> Configuración de la unidad  

> [!NOTE]  
> Estas opciones solo están disponibles cuando se instala un nuevo punto de distribución.  

Especifique la configuración de unidad para el punto de distribución. Configure hasta dos unidades de disco para la biblioteca de contenido y dos discos de unidad para el recurso compartido de paquete. Configuration Manager puede usar otras unidades cuando las dos primeras alcancen la reserva de espacio de unidad configurada. La página **Configuración de unidad** permite configurar la prioridad de las unidades de disco y la cantidad de espacio libre en disco que debe quedar en cada unidad de disco.  

- **Reserva de espacio de unidad (MB)** : este valor determina la cantidad de espacio disponible en una unidad antes de que Configuration Manager seleccione otra unidad y continúe con el proceso de copia en esa unidad. Los archivos de contenido pueden ocupar varias unidades.  

- **Ubicaciones de contenido**: especifique las ubicaciones de la biblioteca de contenido y el recurso compartido de paquete en este punto de distribución. De forma predeterminada, todas las ubicaciones de contenido se establecen en **Automático**. Configuration Manager copia el contenido en la ubicación primaria de contenido hasta que la cantidad de espacio libre alcance el valor especificado en **Reserva de espacio de unidad (MB)** . Al seleccionar **Automático**, Configuration Manager establece las ubicaciones de contenido primarias en la unidad de disco con la mayor cantidad de espacio en disco disponible en el momento de la instalación. Establece las ubicaciones secundarias en la unidad de disco con la segunda mayor cantidad de espacio disponible en disco. Cuando las ubicaciones primaria y secundaria alcanzan la reserva de espacio de unidad, Configuration Manager seleccionará otra unidad disponible que tenga la mayor cantidad de espacio disponible en disco para continuar con el proceso de copia.  

> [!Tip]  
> Para evitar que Configuration Manager se instale en una unidad específica, cree un archivo vacío llamado **no_sms_on_drive.sms** y cópielo en la carpeta raíz de la unidad antes de instalar el punto de distribución.  

Para obtener más información, vea [La biblioteca de contenido](../../../plan-design/hierarchy/the-content-library.md).

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a> Configuración del firewall

El punto de distribución debe tener las siguientes reglas de entrada configuradas en el firewall de Windows:

- Instrumental de administración de Windows (DCOM-In)
- Instrumental de administración de Windows (WMI-In)

Sin estas reglas, los clientes obtendrán el error 0x801901F4 en DataTransferService.log al intentar descargar el contenido.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a> Punto de distribución de extracción  

Al activar la opción **Habilitar este punto de distribución para extraer contenido desde otros puntos de distribución**, se convierte en un punto de distribución de extracción. Puede cambiar la forma en que el punto de distribución obtiene el contenido que distribuya a este. Para más información, vea [Usar un punto de distribución de extracción con System Center Configuration Manager](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

Por cada punto de distribución de extracción que configure, especifique uno o más puntos de distribución de origen desde donde se obtiene el contenido:  

- Elija **Agregar** y, después, seleccione uno o más puntos de distribución disponibles para que sean orígenes.  

- Use los botones de flecha para ajustar la prioridad. Cuando el punto de distribución de extracción intenta transferir el contenido, la prioridad se corresponde con el orden en que establecerá contacto con los puntos de distribución de origen. Primero, establece contacto con los puntos de distribución con el valor más bajo.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a> PXE  

Especifique si desea habilitar PXE en el punto de distribución. Use PXE para iniciar implementaciones del sistema operativo en clientes. Para obtener más información sobre cómo usar PXE en Configuration Manager, vea [Usar PXE para implementar Windows a través de la red](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

Cuando se habilita PXE, Configuration Manager instala Servicios de implementación de Windows (WDS) en el servidor, si es necesario. WDS es el servicio que realiza el arranque PXE para instalar sistemas operativos. Después de finalizar el asistente para crear el punto de distribución, Configuration Manager instala un proveedor en WDS que usa las funciones de arranque PXE.

A partir de la versión 1806, puede habilitar PXE en un punto de distribución sin WDS.

Seleccione la opción **Habilitar compatibilidad de PXE para clientes** y, después, configure las opciones siguientes:  

> [!Note]  
> Seleccione **Sí** en el cuadro de diálogo **Revisar los puertos necesarios para PXE** para confirmar que quiere habilitar PXE. Configuration Manager configura automáticamente los puertos predeterminados en el firewall de Windows. Si usa otro firewall, configure los puertos de forma manual.  
>
> Si instala WDS y DHCP en el mismo servidor, configure WDS para escuchar en otro puerto. De forma predeterminada, DHCP escucha en el mismo puerto. Para obtener más información, consulte [Considerations when you have WDS and DHCP on the same server](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP) (Consideraciones si se tiene WDS y DHCP en el mismo servidor).  

- **Permitir que este punto de distribución responda a solicitudes de PXE entrantes**: especifique si quiere habilitar WDS para responder a solicitudes de servicio PXE. Use esta opción para habilitar o deshabilitar el servicio sin quitar la función de PXE del punto de distribución.  

- **Habilitar compatibilidad de equipos desconocida**: especifique si quiere habilitar la compatibilidad con equipos no administrados por Configuration Manager. Para obtener más información, consulte [Prepare for unknown computer deployments](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos).  

- **Habilitar un respondedor PXE sin Servicios de implementación de Windows**: a partir de la versión 1806, esta opción habilita un respondedor PXE en el punto de distribución que no requiere WDS (Servicios de implementación de Windows). El respondedor PXE es compatible con redes IPv6. Si habilita esta opción en un punto de distribución que ya sea compatible con PXE, Configuration Manager suspenderá el servicio WDS. Si deshabilita esta opción, pero activa la opción **Habilitar compatibilidad de PXE para clientes**, el punto de distribución volverá a habilitar WDS.<!--1357580-->  

    > [!Note]  
    > En la versión 1810 y anterior, no se permite usar el respondedor del entorno PXE sin WDS en servidores que también ejecutan un servidor DHCP.
    >
    > A partir de la versión 1902, cuando se habilita un respondedor del entorno PXE en un punto de distribución sin Servicio de implementación de Windows, ahora puede estar en el mismo servidor que el servicio DHCP. <!--3734270-->  

- **Requerir una contraseña cuando los equipos usen PXE**: para proporcionar seguridad adicional para sus implementaciones del entorno PXE, especifique una contraseña segura.  

- **Afinidad entre usuario y dispositivo**: especifique cómo desea que el punto de distribución asocie usuarios al equipo de destino para las implementaciones del entorno PXE. Elija una de las siguientes opciones:  

  - **Permitir afinidad de dispositivo de usuario con autoaprobación**: seleccione esta opción para asociar automáticamente los usuarios al equipo de destino sin tener que esperar aprobación.  

  - **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador**: seleccione esta opción para esperar aprobación por parte de un usuario administrativo antes de asociar usuarios al equipo de destino.  

  - **No permitir afinidad de dispositivo de usuario**: seleccione esta opción para especificar que los usuarios no están asociados al equipo de destino. Esta configuración es la predeterminada.  

    Para más información sobre la afinidad entre usuario y dispositivo, vea [Link users and devices with user device affinity (Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo)](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

- **Interfaces de red**: especifique que el punto de distribución responda a las solicitudes PXE desde todas las interfaces de red o desde interfaces de red específicas. Si el punto de distribución responde a interfaces de red específicas, especifique la dirección MAC de cada interfaz de red.  

    > [!Note]  
    > Al cambiar la interfaz de red, reinicie el servicio WDS para asegurarse de que guarde correctamente la configuración. A partir de la versión 1806, al usar el servicio del respondedor del entorno PXE, reinicie el **Servicio del respondedor PXE de Configuration Manager** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Especificar retraso en la respuesta del servidor PXE (segundos)** : al usar varios servidores PXE, especifique cuánto tiempo tiene que esperar este punto de distribución compatible con PXE antes de que responda a solicitudes de equipos. De forma predeterminada, el punto de distribución compatible con PXE de Configuration Manager responde de inmediato.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a> Multidifusión  

Especifique si desea habilitar la multidifusión en el punto de distribución. Las implementaciones de multidifusión conservan el ancho de banda de red al enviar de forma simultánea datos a varios clientes de Configuration Manager. Sin multidifusión, el servidor envía una copia de los datos a cada cliente con una conexión distinta. Para obtener más información sobre cómo usar la multidifusión para implementaciones de SO, vea [Usar multidifusión para implementar Windows a través de la red](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

Cuando se habilita la multidifusión, Configuration Manager instala Servicios de implementación de Windows (WDS) en el servidor, si es necesario.  

Seleccione la opción **Habilitar multidifusión para enviar datos simultáneamente a varios clientes** y, después, configure las opciones siguientes:  

- **Cuenta de conexión de multidifusión**: especifique la cuenta que se debe usar al configurar conexiones de base de datos de Configuration Manager para la multidifusión. Para obtener más información, vea [Cuenta de conexión de multidifusión](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Configuración de dirección de multidifusión**: especifique las direcciones IP para enviar datos a los equipos de destino. De forma predeterminada, obtiene la dirección IP de un servidor DHCP habilitado para distribuir direcciones de multidifusión. Según el entorno de red, puede especificar un intervalo de direcciones IP entre 239.0.0.0 y 239.255.255.255.  

    > [!IMPORTANT]  
    > Las direcciones IP que configure tienen que ser accesibles por los equipos de destino que soliciten la imagen del SO. Asegúrese de que los enrutadores y firewalls permitan el tráfico de multidifusión entre el equipo de destino y el punto de distribución.  

- **Intervalo de puertos UDP para multidifusión**: especifique el intervalo de puertos UDP que se usan para enviar datos a los equipos de destino.  

    > [!IMPORTANT]  
    > Los puertos UDP tienen que ser accesibles por los equipos de destino que soliciten la imagen del SO. Compruebe que los enrutadores y firewalls permiten tráfico de multidifusión entre el equipo de destino y el servidor del sitio.  

- **Número máximo de clientes**: especifique el número máximo de equipos de destino que pueden descargar la imagen del SO desde este punto de distribución.  

- **Habilitar multidifusión programada**: especifique de qué manera controla Configuration Manager cuándo se debe iniciar la implementación de sistemas operativos en los equipos de destino. Configure las siguientes opciones:  

    - **Retraso de inicio de sesión (minutos)** : especifique el número de minutos que Configuration Manager espera antes de responder a la primera solicitud de implementación.  

    - **Tamaño de sesión mínimo (clientes)** : especifique cuántas solicitudes deben recibirse para que Configuration Manager inicie la implementación del sistema operativo.  

> [!IMPORTANT]  
> A partir de la versión 1806, para habilitar y configurar la multidifusión en la pestaña **Multidifusión** de las propiedades del punto de distribución, el punto de distribución tiene que usar el Servicio de implementación de Windows.  
>
> - Si activa las opciones **Habilitar compatibilidad de PXE para clientes** y **Habilitar multidifusión para enviar datos simultáneamente a varios clientes**, no podrá activar la opción **Habilitar un respondedor PXE sin el Servicio de implementación de Windows**.  
>
> - Si activa las opciones **Habilitar compatibilidad de PXE para clientes** y **Habilitar un respondedor PXE sin el Servicio de implementación de Windows**, no podrá activar la opción **Habilitar multidifusión para enviar datos simultáneamente a varios clientes**.  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a> Relaciones de grupo  

> [!NOTE]  
> Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  

Administre los grupos de puntos de distribución de los que es miembro este punto de distribución.  

Para agregar este punto de distribución como miembro a un grupo de puntos de distribución existente, elija **Agregar**. En la ventana Agregar a grupos de puntos de distribución, seleccione un grupo existente y, después, elija **Aceptar**.  

Para quitar este punto de distribución de un grupo de puntos de distribución, seleccione el grupo en la lista y, después, elija **Quitar**. La eliminación del punto de distribución de un grupo de puntos de distribución no elimina ningún contenido del punto de distribución.

### <a name="content"></a><a name="bkmk_config-content"></a> Contenido  

> [!NOTE]  
> Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  

Administre el contenido que ha distribuido al punto de distribución. Realice una selección en la lista de paquetes de implementación y realice las acciones siguientes:  

- **Validar**: inicie el proceso para validar la integridad de los archivos de contenido del software. Para ver los resultados del proceso de validación de contenido, en el área de trabajo **Supervisión**, expanda **Estado de distribución** y luego elija el nodo **Estado de contenido**. Para obtener más información, vea [Validar contenido](deploy-and-manage-content.md#validate-content).  

- **Redistribuir**: copia todos los archivos de contenido del software seleccionado al punto de distribución y sobrescribe los archivos existentes. Normalmente, esta acción se usa para reparar archivos de contenido. Para obtener más información, vea [Redistribuir contenido](deploy-and-manage-content.md#redistribute-content).  

- **Quitar**: quita los archivos de contenido del software del punto de distribución. Para obtener más información, vea [Quitar contenido](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a> Validación de contenido  

Establezca una programación para validar la integridad de los archivos de contenido en el punto de distribución. Al habilitar la validación de contenido en una programación, Configuration Manager inicia el proceso en la hora programada. Verifica todo el contenido del punto de distribución en función de la clase de SCCMDP local SMS_PackagesInContLib. También puede configurar la prioridad de la validación de contenido. De forma predeterminada, la prioridad está establecida en **La más baja**. Al aumentar la prioridad, puede incrementarse el uso del disco y el procesador en el servidor durante el proceso de validación, pero se completará más rápido.

Para ver los resultados del proceso de validación de contenido, en el área de trabajo **Supervisión**, expanda **Estado de distribución** y luego elija el nodo **Estado de contenido**. Muestra el contenido de cada tipo de software (por ejemplo, aplicación, paquete de actualización de software e imagen de arranque).  

> [!WARNING]  
> Aunque la programación de la validación de contenido se especifica mediante la hora local del equipo, la programación se muestra en la consola de Configuration Manager en hora UTC.  

Para obtener más información, vea [Validar contenido](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a> Boundary groups  

Administre los grupos de límites a los que asigne este punto de distribución. Agregue el punto de distribución como mínimo a un grupo de límites. Durante la implementación del contenido, los clientes deben estar en un grupo de límites que esté asociado con un punto de distribución para usar ese punto de distribución como ubicación de origen del contenido.

Configure *relaciones* de grupo de límites que definan cuándo y a qué grupos de límites puede revertir un cliente para buscar contenido. Para obtener más información, consulte [Boundary groups (Grupos de límites)](boundary-groups.md).

Elija **Agregar** y seleccione un grupo de límites existente de la lista.

Para crear un grupo de límites para este punto de distribución, elija **Crear**. Para obtener más información sobre cómo crear y configurar un grupo de límites, vea [Procedimientos para grupos de límites](boundary-group-procedures.md).

Al editar las propiedades de un punto de distribución instalado anteriormente, administre la opción **Habilitar para distribución a petición**. Esta opción permite a Configuration Manager distribuir contenido automáticamente a este servidor cuando un cliente lo solicite. Para obtener más información, vea [Distribución de contenido a petición](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="schedule"></a><a name="bkmk_config-sched"></a> Programación  

> [!NOTE]  
> Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.
>
> Esta pestaña solo está disponible al editar las propiedades de un punto de distribución remoto en relación con el servidor de sitio.  

Configure una programación que restrinja cuándo Configuration Manager puede transferir datos al punto de distribución. Puede restringir los datos por prioridad, o bien puede cerrar la conexión en los períodos de tiempo seleccionados.

Para restringir los datos, seleccione el período de tiempo de la cuadrícula y, después, seleccione una de las siguientes opciones de **Disponibilidad**:  

- **Abrir para todas las prioridades**: Configuration Manager envía datos al punto de distribución sin restricciones. Esta opción es el valor predeterminado para todos los períodos de tiempo.  

- **Permitir alta y media prioridad**: Configuration Manager solo envía datos de prioridad alta y media al punto de distribución.  

- **Permitir solo prioridad alta**: Configuration Manager solo envía datos de prioridad alta al punto de distribución.  

- **Cerrado**: Configuration Manager no envía ningún dato al punto de distribución.  

Configure la **Prioridad de distribución** de software en la pestaña **Configuración de distribución** de las propiedades del software.

> [!IMPORTANT]  
> La programación se basa en la zona horaria del sitio de envío, no del punto de distribución.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a> Límites de frecuencia  

> [!NOTE]  
> Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  
>
> Esta pestaña solo está disponible al editar las propiedades de un punto de distribución remoto en relación con el servidor de sitio.  

Configure los límites de frecuencia para controlar el ancho de banda de red que Configuration Manager usa para transferir contenido al punto de distribución. Elija entre las siguientes opciones:  

- **Ilimitado en los envíos a este destino**: Configuration Manager envía contenido al punto de distribución sin restricciones de velocidad. Esta configuración es la predeterminada.  

- **Modo por pulsos**: esta opción especifica el tamaño de los bloques de datos que el servidor de sitio envía al punto de distribución. También puede especificar un retraso de tiempo entre el envío de cada bloque de datos. Utilice esta opción cuando tenga que enviar datos a través de una conexión de red con un ancho de banda muy bajo al punto de distribución. Por ejemplo, tiene restricciones para enviar 1 KB de datos cada cinco segundos, independientemente de la velocidad del vínculo o de su uso en un momento específico.  

- **Limitado al máximo especificado de velocidades de transferencia por hora**: especifique esta opción para que un sitio envíe datos a un punto de distribución usando solo el porcentaje de tiempo que configure. Al usar esta opción, Configuration Manager no identifica el ancho de banda disponible de la red. En su lugar, divide el tiempo en que puede enviar datos. El servidor envía datos durante un breve período de tiempo, seguido de períodos de tiempo en los que no se envían datos. Por ejemplo, si establece la opción **Limitar ancho de banda disponible** en **50 %** , Configuration Manager transmite datos durante un período de tiempo, seguido de un período de tiempo de la misma duración en el que no se envían datos. La cantidad de datos reales (o el tamaño del bloque de datos) no se administra. Solo se administra la cantidad de tiempo durante el que se envían datos.  
