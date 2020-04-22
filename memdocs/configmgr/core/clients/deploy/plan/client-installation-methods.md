---
title: Métodos de instalación de cliente
titleSuffix: Configuration Manager
description: Obtenga información sobre los métodos de instalación del cliente de Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693843"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Métodos de instalación de cliente en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede usar diferentes métodos para instalar el software cliente de Configuration Manager. Use un método o una combinación de ellos. En este artículo se describe cada método, para que sepa cuál es el más adecuado para la organización.  

## <a name="client-push-installation"></a>Instalación de inserción de cliente  

**Plataforma de cliente admitida**: Windows  

#### <a name="advantages"></a>Ventajas  

-   Se puede utilizar para instalar el cliente en un solo equipo, en una recopilación de equipos o en los resultados de una consulta.  

-   Se puede utilizar para instalar automáticamente el cliente en todos los equipos detectados.  

-   Usa automáticamente las propiedades de instalación de cliente definidas en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente**.  

#### <a name="disadvantages"></a>Desventajas  

-   Puede causar mucho tráfico de red si se realiza la inserción en recopilaciones de gran volumen.  

-   Solo se puede usar en equipos detectados por Configuration Manager.  

-   No se puede usar para instalar clientes en un grupo de trabajo.  

-   Debe especificar una cuenta de instalación de inserción de cliente que tenga derechos administrativos en el equipo cliente especificado.  

-   Firewall de Windows se debe configurar con excepciones en los equipos cliente.   

-   La instalación de inserción de cliente no se puede cancelar. Configuration Manager intenta instalar el cliente en todos los recursos detectados. Reintentará las instalaciones en las que se produzca un error durante un máximo de siete días.  

Para obtener más información, vea [Cómo instalar clientes con inserción de cliente](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Instalación basada en el punto de actualización de software  

**Plataforma de cliente admitida**: Windows  

#### <a name="advantages"></a>Ventajas  

-   Puede utilizar la infraestructura existente de actualizaciones de software para administrar el software cliente.  

-   Si se configuran correctamente las opciones de Windows Server Update Services (WSUS) y de directiva de grupo en Active Directory Domain Services, se puede instalar automáticamente el software cliente en equipos nuevos.  

-   No requiere la detección de equipos para instalar el cliente.  

-   Los equipos pueden leer las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory.  

-   Si se quita el cliente, este método vuelve a instalarlo.  

-   No requiere la configuración y el mantenimiento de una cuenta de instalación para el equipo cliente especificado.  

#### <a name="disadvantages"></a>Desventajas  

-   Requiere una infraestructura de actualizaciones de software operativa como requisito previo.  

-   Debe usar el mismo servidor para la instalación de cliente y las actualizaciones de software. Este servidor debe residir en un sitio primario.  

-   Para instalar clientes nuevos, debe configurar un objeto de directiva de grupo en Active Directory Domain Services con el puerto y el punto de actualización de software activo del cliente.  

-   Si el esquema de Active Directory no se extiende para Configuration Manager, debe usar la configuración de directiva de grupo para aprovisionar equipos con propiedades de instalación de cliente.  

Para obtener más información, vea [Cómo instalar clientes con la instalación basada en actualizaciones de software](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Instalación de directiva de grupo  

**Plataforma de cliente admitida**: Windows  

#### <a name="advantages"></a>Ventajas  

-   No requiere la detección de equipos para instalar el cliente.  

-   Se puede utilizar para nuevas instalaciones o actualizaciones de cliente.  

-   Los equipos pueden leer las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory.  

-   No requiere la configuración y el mantenimiento de una cuenta de instalación para el equipo cliente especificado.  

#### <a name="disadvantages"></a>Desventajas  

-   Si se instala un gran número de clientes, puede causar mucho tráfico de red.  

-   Si el esquema de Active Directory no se extiende para Configuration Manager, debe usar la configuración de directiva de grupo para agregar propiedades de instalación de cliente a los equipos del sitio.  

Para obtener más información, vea [Cómo instalar clientes con directiva de grupo](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Instalación de script de inicio de sesión  

**Plataforma de cliente admitida**: Windows  

#### <a name="advantages"></a>Ventajas  

-   No requiere la detección de equipos para instalar el cliente.  

-   Admite el uso de propiedades de línea de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desventajas  

-   Si se instala un gran número de clientes en un breve período de tiempo, puede causar mucho tráfico de red.  

-   Si los usuarios no inician sesión en la red con frecuencia, puede llevar bastante tiempo realizar la instalación en todos los equipos cliente.  

Para obtener más información, vea [Cómo instalar clientes con scripts de inicio de sesión](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Instalación manual  

**Plataforma de cliente admitida**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Ventajas  

-   No requiere la detección de equipos para instalar el cliente.  

-   Puede ser útil para realizar pruebas.  

-   Admite el uso de propiedades de línea de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desventajas  

-   Carece de automatización y es, por lo tanto, un proceso lento.  

Para obtener más información sobre cómo instalar manualmente el cliente en cada plataforma, vea los artículos siguientes:  

-   [Implementar clientes en equipos Windows](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Implementar clientes en servidores UNIX y Linux](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Cómo implementar clientes en equipos Mac](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Instalación de MDM de Microsoft Intune

**Plataformas de cliente admitidas**: Windows 10

#### <a name="advantages"></a>Ventajas  

-   No requiere la detección de equipos para instalar el cliente.  

-   No requiere la configuración y el mantenimiento de una cuenta de instalación para el equipo cliente especificado.  

-   Puede usar la autenticación moderna con Azure Active Directory.  

-   Puede instalar y asignar equipos en Internet.  

-   Se puede automatizar con Windows AutoPilot y Microsoft Intune para la administración conjunta.  

#### <a name="disadvantages"></a>Desventajas  

-   Requiere tecnologías adicionales fuera de Configuration Manager.  

-   Requiere que el dispositivo tenga acceso a Internet, incluso si no está basado en Internet.  

Vea los siguientes artículos para más información:  

-   [Cómo instalar clientes en dispositivos Windows administrados por MDM con Intune](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](../deploy-clients-cmg-azure.md)  

