---
title: Actualizar clientes.
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo actualizar clientes en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076686"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Actualización de clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede usar varios métodos para actualizar el software cliente de Configuration Manager en equipos Windows, servidores UNIX y Linux, y equipos Mac. Aquí se muestran las ventajas y desventajas de cada método.  

> [!TIP]  
>  Si va a actualizar su infraestructura desde una versión anterior de Configuration Manager \(como Configuration Manager 2007 o System Center 2012 Configuration Manager\), se recomienda que realice las actualizaciones de servidor, incluida la instalación de todas las actualizaciones de la rama actual, antes de actualizar los clientes Configuration Manager. De esta manera, también tendrá la versión más reciente del software cliente.  

## <a name="group-policy-installation"></a>Instalación de directiva de grupo  
 **Plataforma de cliente admitida:** Windows  

#### <a name="advantages"></a>Ventajas  

- No requiere la detección previa de equipos para actualizar el cliente.  

- Se puede utilizar para nuevas instalaciones o actualizaciones de cliente.  

- Los equipos pueden leer las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory.  

- No requiere la configuración y el mantenimiento de una cuenta de instalación para el equipo cliente especificado.  

#### <a name="disadvantages"></a>Desventajas  

- Puede provocar mucho tráfico de red si está actualizando muchos clientes.  

- Si el esquema de Active Directory no se extiende para Configuration Manager, debe usar la [configuración de directiva de grupo](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) para agregar propiedades de instalación de cliente a los equipos del sitio.  


## <a name="logon-script-installation"></a>Instalación de script de inicio de sesión  
 **Plataforma de cliente admitida:** Windows  

#### <a name="advantages"></a>Ventajas  

- No requiere la detección de equipos para instalar el cliente.  

- Se puede utilizar para nuevas instalaciones o actualizaciones de cliente.  

- Admite el uso de propiedades de línea de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desventajas  

- Puede provocar mucho tráfico de red si está actualizando muchos clientes en un corto período de tiempo.  

- Puede tardar bastante tiempo en actualizar todos los equipos cliente si los usuarios no inician sesión en la red con frecuencia.  

  Para obtener más información, consulte [Instalación de clientes de Configuration Manager mediante scripts de inicio de sesión](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Instalación manual  
 **Plataforma de cliente admitida:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Ventajas  

- No requiere la detección previa de equipos para actualizar el cliente.  

- Puede ser útil para realizar pruebas.  

- Admite el uso de propiedades de línea de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desventajas  

- Carece de automatización y es, por lo tanto, un proceso lento.  

  Para obtener más información, consulte los temas siguientes:  

- [Instalación manual de clientes de Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Cómo actualizar clientes para servidores Linux y UNIX](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Cómo actualizar clientes en equipos Mac](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Instalación de la actualización (administración de aplicaciones)  
 **Plataforma de cliente admitida:** Windows  

> [!NOTE]  
>  No puede actualizar clientes de Configuration Manager 2007 con este método. En este escenario, puede implementar el cliente de Configuration Manager como un paquete desde el sitio de Configuration Manager 2007 o bien puede usar la actualización automática del cliente que crea e implementa de forma automática un paquete que contiene la última versión del cliente.  

#### <a name="advantages"></a>Ventajas  

- Admite el uso de propiedades de línea de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desventajas  

- Puede causar mucho tráfico de red si distribuye el cliente en grandes recopilaciones.  

- Solo puede utilizarse para actualizar el software cliente en equipos detectados y asignados al sitio.  

  Para obtener más información, consulte [Cómo instalar clientes de Configuration Manager mediante un paquete y un programa](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Actualización de cliente automática  

> [!NOTE]  
> Se puede usar para actualizar los clientes de Configuration Manager 2007 a clientes de la rama actual de Configuration Manager. Un cliente de Configuration Manager 2007 se puede asignar a un sitio de Configuration Manager, pero no puede realizar ninguna acción diferente de la actualización de cliente automática.  

 **Plataforma de cliente admitida:** Windows  

#### <a name="advantages"></a>Ventajas  

- Debido a la selección aleatoria durante el período especificado, solo la actualización automática es adecuada para las actualizaciones de clientes a gran escala. El resto de métodos son demasiado lentos para usarlos a gran escala, o bien no incluyen la selección aleatoria. 

    > [!Note]
    > El uso piloto de los clientes no es adecuado para su utilización a gran escala, ya que no incluye ningún tipo de selección aleatoria.  
- Se puede utilizar para mantener automáticamente la versión más reciente para los clientes en su sitio.  

- Requiere una administración mínima.  

#### <a name="disadvantages"></a>Desventajas  

- Solo se puede utilizar para actualizar el software cliente y no se puede utilizar para instalar un nuevo cliente.  

- Se aplica a todos los clientes en la jerarquía asignados a un sitio. No se puede limitar por recopilación.  

- Opciones de programación limitadas.  

  Para obtener más información, consulte [How to upgrade clients for Windows computers (Cómo actualizar clientes para equipos Windows)](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Pruebas de cliente  
 **Plataforma de cliente admitida:** Windows  

#### <a name="advantages"></a>Ventajas  

- Puede usarse para probar nuevas versiones de cliente de una recopilación de preproducción menor.  

- Cuando se completa la prueba, los clientes de preproducción se promueven a producción y se actualizan de manera automática en el sitio de Configuration Manager.  

#### <a name="disadvantages"></a>Desventajas  

- Solo se puede utilizar para actualizar el software cliente y no se puede utilizar para instalar un nuevo cliente.  

  [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
