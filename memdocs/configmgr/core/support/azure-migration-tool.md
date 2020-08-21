---
title: Extensión y migración de un sitio local a Microsoft Azure
titleSuffix: Configuration Manager
description: Aprenda a usar la herramienta de migración para crear máquinas virtuales de Azure para Configuration Manager mediante programación.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d5f0c9127cc5c5819368eb0454d7bc63546ccc1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699507"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Extensión y migración de un sitio local a Microsoft Azure

*Se aplica a: Configuration Manager (rama actual)*


Esta herramienta, incluida en la versión 1910, ayuda a crear máquinas virtuales (VM) de Azure para Configuration Manager mediante programación. <!--3556022--> Se puede instalar con roles de sitio de configuración predeterminados, como un servidor de sitio pasivo, puntos de administración y puntos de distribución. Una vez validados los nuevos roles, úselos como sistemas de sitio adicionales para lograr alta disponibilidad. También puede quitar el rol de sistema de sitio local y mantener solo el rol de máquina virtual de Azure.

## <a name="prerequisites"></a>Requisitos previos

- Una suscripción de Azure.

- Red virtual de Azure con puerta de enlace de ExpressRoute.

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Su cuenta de usuario debe ser **Administrador total** de Configuration Manager y debe tener derechos de administrador en el servidor de sitio principal.

- Para agregar un servidor pasivo, el sitio principal debe cumplir los [requisitos de alta disponibilidad de servidor de sitio](../servers/deploy/configure/site-server-high-availability.md#prerequisites). Por ejemplo, requiere una [biblioteca de contenido remota](../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="required-azure-permissions"></a>Permisos de Azure necesarios

Necesitará los siguientes permisos en Azure al ejecutar la herramienta:
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


Para más información sobre los permisos y la asignación de roles, vea [Administración del acceso a los recursos de Azure mediante RBAC](/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Ejecutar la herramienta

1. Inicie sesión en el servidor de sitio principal y ejecute la herramienta siguiente en el directorio de instalación de Configuration Manager: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Revise la información en la pestaña **General** y, luego, cambie a la pestaña **Información de Azure**.

1. En la pestaña **Información de Azure**, elija el **Entorno de Azure** y, luego, **inicie sesión**.

    > [!TIP]
    > Es posible que tenga que agregar `https://*.microsoft.com` a la lista de sitios web de confianza para iniciar sesión correctamente.

    [ ![Pestaña Información de Azure en la herramienta de extensión y migración](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Después de iniciar sesión, seleccione el **Id. de suscripción** y la **Red virtual**. La herramienta solo muestra las redes con una puerta de enlace de ExpressRoute.

## <a name="site-server-high-availability"></a>Alta disponibilidad de servidor de sitio

1. En la pestaña **Alta disponibilidad de servidor de sitio**, seleccione **Check** (Comprobar) para evaluar la preparación del sitio.

    Si se produce un error en alguna de las comprobaciones, seleccione **Más detalles** para determinar cómo solucionar el problema. Para más información sobre estos requisitos previos, consulte [Alta disponibilidad de servidor de sitio](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Si quiere extender o migrar el servidor de sitio a Azure, seleccione **Create a site server in Azure** (Crear un servidor de sitio en Azure). Luego, rellene los campos siguientes:

    |Nombre|Descripción|
    |---|---|
    |**Suscripción**|Solo lectura. Muestra el nombre y el identificador de la suscripción.|
    |**Grupo de recursos**| Enumera los grupos de recursos disponibles. Si necesita crear un grupo de recursos nuevo, use [Azure Portal](https://portal.azure.com) y, luego, vuelva a ejecutar esta herramienta.|
    |**Ubicación**| Solo lectura. Determinada por la ubicación de la red virtual.|
    |**Tamaño de VM**|Elija un tamaño que se ajuste a la carga de trabajo. Microsoft recomienda **Standard_DS3_v2**.|
    |**Sistema operativo**|Solo lectura. La herramienta usa Windows Server 2019.|
    |**Tipo de disco**|Solo lectura. La herramienta usa SSD Premium para obtener el mejor rendimiento.|
    |**Red virtual**|Solo lectura.|
    |**Subred**|Seleccione la subred que se va a usar. Si necesita crear una subred, use [Azure Portal](https://portal.azure.com).|
    |**Nombre de la máquina**|Escriba el nombre de la máquina virtual del servidor de sitio pasivo en Azure. Es el mismo nombre que se muestra en [Azure Portal](https://portal.azure.com).|
    |**Nombre de usuario de administrador local**|Escriba el nombre del usuario administrativo local que la máquina virtual crea antes de unirse al dominio.|
    |**Contraseña de administrador local**|La contraseña del usuario administrativo local. Para proteger la contraseña durante la implementación de Azure, almacene la contraseña como secreto en [Azure Key Vault](/azure/key-vault/key-vault-overview). A continuación, use la referencia que aparece aquí. Si es necesario, cree una nueva en [Azure Portal](https://portal.azure.com).|
    |**FQDN del dominio**|El nombre de dominio completo del dominio de Active Directory que se va a combinar. De manera predeterminada, la herramienta obtiene este valor de la máquina actual.|
    |**Nombre de usuario de dominio**|El nombre del usuario de dominio que tiene permiso para unirse al dominio. De manera predeterminada, la herramienta usa el nombre del usuario que ha iniciado sesión actualmente.|
    |**Contraseña de dominio**|La contraseña del usuario de dominio que se va a unir al dominio. La herramienta lo comprueba después de que selecciona **Iniciar**. Para proteger la contraseña durante la implementación de Azure, almacene la contraseña como secreto en [Azure Key Vault](/azure/key-vault/key-vault-overview). A continuación, use la referencia que aparece aquí. Si es necesario, cree una nueva en [Azure Portal](https://portal.azure.com).|
    |**Dirección IP de DNS de dominio**|Se usa para unirse al dominio. De manera predeterminada, la herramienta usa el DNS actual de la máquina actual.|
    |**Tipo**|Solo lectura. Muestra *Servidor de sitio pasivo* como el tipo.|

    > [!IMPORTANT]
    > De forma predeterminada, las máquinas virtuales se establecen en **No** para **Usar la licencia de Windows Server existente**. Si desea usar sus licencias de Windows Server locales con Software Assurance, configure esta opción en [Azure Portal](https://portal.azure.com) después de aprovisionar las máquinas virtuales. Para obtener más información, vea [Ventaja para uso híbrido de Azure para Windows Server](/windows-server/get-started/azure-hybrid-benefit).

1. Para iniciar el aprovisionamiento de la máquina virtual de Azure, seleccione **Iniciar**. Para supervisar el estado de la implementación, cambie a la pestaña **Implementaciones en Azure** de la herramienta. Para ver el estado más reciente, seleccione **Refresh deployment status** (Actualizar el estado de la implementación).

    > [!TIP]
    > También puede usar [Azure Portal](https://portal.azure.com) para comprobar el estado, buscar errores y determinar posibles correcciones.

1. Cuando finalice la implementación, vaya a los servidores SQL Server y conceda permisos para la nueva máquina virtual de Azure. Para más información, consulte [Alta disponibilidad de servidor de sitio: requisitos previos](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Para agregar la máquina virtual de Azure como servidor de sitio en modo pasivo, seleccione **Add site server in passive mode** (Agregar servidor de sitio en modo pasivo).

1. Una vez que el sitio agrega el servidor de sitio en modo pasivo, la pestaña **Alta disponibilidad de servidor de sitio** muestra el estado.

   [![Servidor de sitio pasivo agregado a la pestaña Alta disponibilidad de servidor de sitio](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Luego, vaya a la pestaña [Implementaciones en Azure](#bkmk_deploy-azure) para finalizar la implementación.

## <a name="site-database"></a>Base de datos del sitio

Actualmente, la herramienta no tiene ninguna tarea para migrar la base de datos del entorno local a Azure. Puede optar por migrar la base de datos de una instancia de SQL Server local a una máquina virtual de Azure SQL Server. La herramienta enumera los artículos siguientes en la pestaña **Base de datos del sitio** para ayudar:

- [Copia de seguridad y restauración de la base de datos](../servers/manage/backup-and-recovery.md)
- [Configuración de SQL Always On y autorización para que los datos se repliquen](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Migración de una base de datos SQL a una máquina virtual de Azure SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Roles de sistema de sitio

1. Cambie a la pestaña **Roles de sistema de sitio**. Para aprovisionar un rol de sistema de sitio nuevo con la configuración siguiente, seleccione **Create new** (Crear nuevo). Puede aprovisionar roles como el punto de administración, el punto de distribución y el punto de actualización de software. No todos los roles están disponibles actualmente en la herramienta.

    [![Pestaña Roles de sistema de sitio en la herramienta de extensión y migración](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. En la ventana de aprovisionamiento, rellene los campos para aprovisionar la VM del rol de sitio en Azure. Estos detalles son similares a la lista anterior para el servidor de sitio.

1. Para iniciar el aprovisionamiento de la máquina virtual de Azure, seleccione **Iniciar**. Para supervisar el estado de la implementación, cambie a la pestaña **Implementaciones en Azure** de la herramienta. Para ver el estado más reciente, seleccione **Refresh deployment status** (Actualizar el estado de la implementación).

    > [!TIP]
    > También puede usar [Azure Portal](https://portal.azure.com) para comprobar el estado, buscar errores y determinar posibles correcciones.

1. Repita este proceso para agregar más roles de sistema de sitio.

1. Luego, vaya a la pestaña [Implementaciones en Azure](#bkmk_deploy-azure) para finalizar la implementación.

1. Cuando finalice la implementación, vaya a la consola de Configuration Manager para realizar cambios adicionales en el rol de sitio.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Implementaciones en Azure

1. Una vez que Azure cree la VM, cambie a la pestaña **Implementaciones en Azure** en la herramienta. Seleccione **Deploy** (Implementar) para configurar el rol con la configuración siguiente.

1. Seleccione **Run** (Ejecutar) para iniciar el script de PowerShell.

    [![Implementación de roles de sitio mediante la ejecución del script generado de PowerShell](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Repita este proceso para configurar más roles.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> Adición de roles de sitio a una implementación de máquina virtual existente
<!--5665775, 6307931-->
A partir de la versión 2002 de Configuration Manager, la herramienta Extensión y migración de un sitio local a Microsoft Azure permite aprovisionar varios roles de sistema de sitio en una sola máquina virtual de Azure. Puede agregar roles de sistema de sitio después de que se haya completado la implementación inicial de la máquina virtual de Azure. Para agregar un nuevo rol a una máquina virtual existente, realice los pasos siguientes:
1. En la pestaña **Implementaciones en Azure**, haga clic en una implementación de máquina virtual que tenga un estado **Completado**.
1. Haga clic en el botón **Crear nuevo** para agregar un rol adicional a la máquina virtual.


## <a name="next-steps"></a>Pasos siguientes

Revisar los cambios en [Azure Portal](https://portal.azure.com)