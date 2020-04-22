---
title: Instalar roles de sistema de sitio
titleSuffix: Configuration Manager
description: Agregue roles de sistema de sitio en un servidor de sistema de sitio nuevo o existente en el sitio.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 102d07f29b9addd1f2c37dd741db09e972cd5802
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701663"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Instalación de roles de sistema de sitio para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Hay dos métodos en la consola de Configuration Manager para instalar roles de sistema de sitio:

- **Agregar roles de sistema de sitio**: Agregue roles de sistema de sitio en un servidor de sistema de sitio existente en el sitio.

- **Crear servidor del sistema de sitio**: Especifique un nuevo servidor como servidor de sistema de sitio y, después, instale uno o varios roles. Este método es el mismo que **Agregar roles de sistema de sitio**, excepto la primera página. En primer lugar, especifique el nombre del servidor y el sitio en el que quiere instalarlo.

> [!TIP]
> Al instalar un rol en un equipo remoto, Configuration Manager agrega la cuenta de equipo del equipo remoto a un grupo local en el servidor de sitio.
>
> Cuando se instala el sitio en un controlador de dominio, el grupo del servidor de sitio es un grupo de dominio, en lugar de un grupo local. En este caso, el rol de sistema de sitio remoto no funciona inmediatamente. El servidor de sistema de sitio debe reiniciarse o el usuario debe actualizar el ticket de Kerberos para la cuenta de equipo del servidor remoto. Para más información, vea [Cuentas que se usan](../../../plan-design/hierarchy/accounts.md).

Antes de instalar el rol de sistema de sitio, Configuration Manager comprueba el equipo de destino para asegurarse de que cumple los requisitos previos para los roles seleccionados.

De manera predeterminada, cuando Configuration Manager instala un rol de sistema de sitio, instala los archivos en la primera unidad de disco con formato NTFS disponible que tenga el mayor espacio disponible en disco. Para evitar que Configuration Manager se instale en unidades concretas, antes de instalar el servidor de sistema de sitio, cree un archivo vacío denominado **no_sms_on_drive.sms** en la carpeta raíz de la unidad.

Configuration Manager usa la **cuenta de instalación del sistema de sitio** para instalar roles. La cuenta se especifica al instalar el rol. De forma predeterminada, esta cuenta es la cuenta de sistema local del equipo de servidor de sitio. Puede especificar una cuenta de usuario de dominio como cuenta de instalación del sistema de sitio. Para obtener más información, vea [Cuentas: cuenta de instalación del sistema de sitio](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Instalar roles en un servidor de sistema de sitio existente

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y, después, seleccione el nodo **Servidores y roles del sistema de sitios**. Seleccione el servidor de sistema de sitio existente en el que quiere instalar los nuevos roles de sistema de sitio.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Servidor**, seleccione **Agregar rol de sistema de sitio**.

1. En la página **General**, revise la configuración.

    > [!TIP]
    >  Para acceder al rol de sistema de sitio desde Internet, asegúrese de especificar un nombre de dominio completo (FQDN) de Internet.

1. En la página **Proxy**, si los roles de este servidor requieren un proxy de Internet, especifique la configuración de un servidor proxy. Para obtener más información, vea [Compatibilidad de servidor proxy](../../../plan-design/network/proxy-server-support.md).

1. En la página **Selección de rol del sistema**, seleccione los roles de sistema de sitio que quiera agregar.

1. Complete el asistente. Pueden aparecer páginas adicionales para roles específicos. Para obtener más información, vea [Opciones de configuración para roles de sistema de sitio](configuration-options-for-site-system-roles.md).

> [!TIP]
> El cmdlet de Windows PowerShell, **New-CMSiteSystemServer**, realiza la misma función que este procedimiento. Para obtener más información, vea [New-CMSiteSystemServer](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Instalar roles en un servidor de sistema de sitio nuevo

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y, después, seleccione el nodo **Servidores y roles del sistema de sitios**.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear servidor del sistema de sitio**.

1. En la página **General**, especifique la configuración general para el sistema de sitio.

    > [!TIP]
    > Para acceder al nuevo rol de sistema de sitio desde Internet, asegúrese de especificar un FQDN de Internet.

1. En la página **Proxy**, si los roles de este servidor requieren un proxy de Internet, especifique la configuración de un servidor proxy. Para obtener más información, vea [Compatibilidad de servidor proxy](../../../plan-design/network/proxy-server-support.md).

1. En la página **Selección de rol del sistema**, seleccione los roles de sistema de sitio que quiera agregar.

1. Complete el asistente. Pueden aparecer páginas adicionales para roles específicos. Para obtener más información, vea [Opciones de configuración para roles de sistema de sitio](configuration-options-for-site-system-roles.md).

> [!TIP]
> El cmdlet de Windows PowerShell, **New-CMSiteSystemServer**, realiza la misma función que este procedimiento. Para obtener más información, vea [New-CMSiteSystemServer](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="next-steps"></a>Pasos siguientes

- [Opciones de configuración para roles de sistema de sitio](configuration-options-for-site-system-roles.md)

- [Quitar un rol](../install/uninstall-sites-and-hierarchies.md#bkmk_role)
