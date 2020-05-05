---
title: Instalación de roles para MDM local
titleSuffix: Configuration Manager
description: Instale los roles de sistema de sitio necesarios para la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724709"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Instalar roles de sistema de sitio para MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager la administración de dispositivos móviles (MDM) local requiere los siguientes roles de sistema de sitio en el sitio de Configuration Manager:

- Punto de inscripción

- Punto de proxy de inscripción

- Punto de distribución

- Punto de administración de dispositivos, que es un punto de administración que permite dispositivos móviles

## <a name="requirements-and-limitations"></a>Requisitos y limitaciones

- MDM local requiere que se habiliten los roles de sistema de sitio para las comunicaciones HTTPS. Para obtener más información, consulte [configuración de certificados para comunicaciones de confianza en MDM local](set-up-certificates-on-premises-mdm.md).

- La rama actual de Configuration Manager solo admite conexiones de *intranet* desde dispositivos a los puntos de distribución y puntos de administración de dispositivos para MDM local. Sin embargo, si también administra equipos macOS, dichos clientes requieren conexiones de *Internet* a esos mismos roles. Al configurar el punto de distribución y el punto de administración de dispositivos, use la opción para **permitir conexiones de intranet e Internet**.

- Los puntos de distribución que se configuran para las conexiones de intranet requieren que se configuren límites de sitio para ellos. Configuration Manager solo admite límites de intervalo IPv4 para MDM local. Para obtener más información, vea [Definir los límites del sitio y los grupos de límites](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Si usa [réplicas de base de datos](../../core/servers/deploy/configure/database-replicas-for-management-points.md) con el punto de administración de dispositivos, los dispositivos recién inscritos no podrán conectarse inicialmente. Este error de conexión se produce porque la réplica de base de datos no tiene la información sobre el dispositivo recién inscrito que se necesita para una conexión correcta. Las réplicas se sincronizan cada cinco minutos. Los dispositivos no se podrán conectar durante los primeros cinco minutos después de la inscripción, que suele ser dos intentos de conexión. Después, los dispositivos se conectarán correctamente.

## <a name="add-roles"></a>Agregar roles

Si va a agregar MDM local a un sitio que tiene la mayoría de los dispositivos administrados con el cliente de Configuration Manager, es posible que ya tenga algunos de estos roles instalados en el sitio. Por ejemplo, el punto de distribución es un rol común y el punto de administración de dispositivos es necesario para administrar los dispositivos macOS.

Para obtener más información sobre cómo agregar roles al sitio, vea [Agregar roles de sistema de sitio](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Configurar funciones

Configurar roles nuevos o existentes para administrar dispositivos móviles. Siga los pasos que se indican a continuación para configurar el punto de distribución y el punto de administración de dispositivos para que funcionen correctamente para MDM local:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**.

1. Seleccione el servidor de sistema de sitio con el punto de distribución o el punto de administración de dispositivos que desea configurar. Seleccione el servidor en la lista y, a continuación, seleccione el rol de **sistema de sitio** en el panel de detalles roles del sistema de sitio. En la cinta de opciones, en la pestaña **rol de sitio** , seleccione **propiedades**.

    > [!TIP]
    > En un sitio de gran tamaño, puede limitar la vista para mostrar solo los servidores con roles específicos. Al seleccionar el nodo **servidores y roles del sistema de sitio** , en la cinta de opciones, en la etiqueta Inicio, seleccione **servidores con rol**. A continuación, seleccione el rol que desee en la lista de roles disponibles actualmente en el sitio.

    En la pestaña **General** de las **propiedades del sistema de sitio**, asegúrese de que el **nombre** es un nombre de dominio completo (FQDN). Cierre las propiedades.

1. En la lista de la consola, seleccione un servidor con un rol de punto de distribución local. Seleccione el rol de **punto de distribución** en el panel de detalles roles del sistema de sitio. En la cinta de opciones, en la pestaña **rol de sitio** , seleccione **propiedades**. En la pestaña **comunicación** de las **propiedades del punto de distribución**:

    1. Seleccione **https**y seleccione **permitir solo conexiones de intranet**.

        > [!IMPORTANT]
        > Si también está administrando equipos macOS con el cliente Configuration Manager, use **permitir conexiones de intranet e Internet** en su lugar.

    1. Habilite la opción para **permitir que los dispositivos móviles se conecten a este punto de distribución**y, a continuación, cierre las propiedades.

1. Abra propiedades para el rol de sistema de sitio de **punto de administración** .

    1. En la pestaña **General** , seleccione **https**y seleccione **permitir solo conexiones de intranet**.

        > [!IMPORTANT]
        > Si también está administrando equipos macOS con el cliente Configuration Manager, use **permitir conexiones de intranet e Internet** en su lugar.

    1. Habilite la opción para **permitir que los dispositivos móviles y el equipo Mac usen este punto de administración**y, a continuación, cierre las propiedades.

        > [!NOTE]
        > Esta opción convierte eficazmente el punto de administración en un punto de administración de *dispositivos* .  

## <a name="next-step"></a>Paso siguiente

Después de agregar y configurar los roles para administrar dispositivos móviles, configure los servidores como puntos de conexión de confianza. Esta confianza permite que los roles se comuniquen con los dispositivos administrados y los inscriban.

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
