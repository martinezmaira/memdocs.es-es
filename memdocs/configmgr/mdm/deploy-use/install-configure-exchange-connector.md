---
title: Instalar Exchange Connector
titleSuffix: Configuration Manager
description: Instale y Configure Exchange Connector para Configuration Manager para administrar dispositivos móviles a través de ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d854e4b70a59a364b8611947feea89d4678e7e6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724849"
---
# <a name="install-and-configure-the-exchange-connector"></a>Instalación y configuración de Exchange Connector

*Se aplica a: Configuration Manager (rama actual)*

Utilice este procedimiento para instalar y configurar un conector de Exchange Server para administrar dispositivos móviles. Configuration Manager solo admite un conector en una organización de Exchange.

Antes de instalar el conector de Exchange Server para Configuration Manager, asegúrese de que tiene los permisos y versiones necesarios. Para obtener más información, consulte [Administración de dispositivos con Exchange y Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Cuenta de conexión de Exchange

Decida qué cuenta se conectará al servidor de acceso de cliente Exchange para administrar los dispositivos móviles. La cuenta puede ser la cuenta de equipo del servidor de sitio o una cuenta de usuario de Windows.

A continuación, configure esta cuenta en un grupo de roles de Exchange para ejecutar los siguientes cmdlets de Exchange Server:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-User**  

- **Set-ActiveSyncOrganizationSettings**  

Los siguientes roles de administración de Exchange Server incluyen estos cmdlets:

- Administración de destinatarios
- Administración de la organización de solo vista
- Servidor de administración

Para obtener más información, consulte Descripción de los [grupos de roles de administración](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help) en la documentación de Exchange Server 2013.

> [!TIP]  
> Si intenta instalar o usar el conector de Exchange Server sin los cmdlets necesarios, verá el siguiente error en el archivo EasDisc. log en el equipo de servidor de sitio: `Invoking cmdlet <cmdlet> failed`.

## <a name="install-the-connector"></a>Instalación del conector

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** , expanda **configuración de jerarquía**y, a continuación, seleccione **conectores de Exchange Server**.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **crear** , seleccione **Agregar servidor de Exchange**.

1. En la página **General** del Asistente para agregar servidor de Exchange, seleccione uno de los entornos de Exchange Server:

    - **Exchange Server local**: especifique un solo servidor o una matriz de servidores de acceso de cliente para cada sitio de Active Directory.

        Si el servidor o la matriz están desconectados, Configuration Manager intentará detectar un servidor de acceso de cliente para usarlo. Si esta opción no produce el resultado esperado, Configuration Manager recurrirá al uso de un servidor de buzones de correo para realizar una conexión con el servidor de acceso de cliente. Cuando vuelve a intentar la conexión, registra las siguientes advertencias en el archivo EasDisc. log en el equipo de servidor de sitio `Failed to open runspace for site <site_name>`:.

    - **Hosted Exchange Server**: especifique la dirección del servidor de su entorno de Exchange Online.

    A continuación, seleccione el sitio primario para ejecutar el conector de Exchange Server.

1. En la página **cuenta** , especifique la cuenta para conectarse al servidor de Exchange. Para obtener más información, vea [cuenta de conexión de Exchange](#exchange-connection-account).

1. En la página **detección** , configure la programación de sincronización y las reglas para buscar dispositivos.

1. En la página **configuración** , configure las opciones del dispositivo móvil en los grupos siguientes:

    - **General**
    - **Contraseña**
    - **Administración de correo electrónico**
    - **Seguridad**
    - **Aplicación**

    Para obtener más información, consulte [configuración de Exchange Connector](manage-mobile-devices-with-exchange-activesync.md#policies).

    Si también inscribe dispositivos móviles mediante Configuration Manager [MDM local](../understand/manage-mobile-devices-with-on-premises-infrastructure.md), habilite la opción para **permitir la administración externa de dispositivos móviles**. Esta configuración permite que estos dispositivos móviles sigan recibiendo correo electrónico de Exchange después de que Configuration Manager los inscriba.

1. Complete el asistente.

## <a name="verify-and-monitor"></a>Comprobar y supervisar

Compruebe la instalación del conector de Exchange Server con mensajes de estado y archivos de registro:

- Confirme que Administrador de componentes de sitio instalado correctamente el conector de Exchange Server. Busque el ID. de estado de mensaje **1015** del componente **SMS_EXCHANGE_CONNECTOR** .

    Se puede producir un error en la instalación si el servidor de acceso de cliente especificado está sin conexión. Si Configuration Manager no puede instalar correctamente el conector, Configuration Manager reintenta la instalación cada 60 minutos. Continúa intentándolo hasta que la instalación se realiza correctamente o se quita el conector de Exchange Server.

- En el equipo de servidor de sitio, revise **SiteComp. log** para obtener la `Component SMS_EXCHANGE_CONNECTOR flagged for installation`siguiente entrada:. Después, registra la instalación correcta con el siguiente texto: `STATMSG: ID=1015`.

Después de completar la instalación, supervise los dispositivos móviles encontrados y administrados por el conector. Ver las recopilaciones de dispositivos móviles y utilizar los informes para dispositivos móviles.

> [!NOTE]  
> Configuration Manager genera nombres para los dispositivos móviles que encuentra. Usa el formato *nombre de usuario*_*dispositivo tipo*. Por ejemplo, **jdoe_WindowsPhone**. Si un usuario tiene más de un dispositivo móvil con el mismo tipo de dispositivo, Configuration Manager muestra el mismo nombre para estos dispositivos móviles en la consola y en los informes.  

## <a name="see-also"></a>Consulte también

- [Puertos utilizados por los clientes de configuración y los sistemas de sitio](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Compatibilidad de servidor proxy](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Recomendaciones de seguridad para dispositivos móviles](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Información de privacidad para dispositivos móviles que se administran con el conector de Exchange Server](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)
