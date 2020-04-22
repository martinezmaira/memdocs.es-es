---
title: Servidores de sistema de sitio admitidos
titleSuffix: Configuration Manager
description: Obtenga información sobre qué versiones de Windows puede usar para hospedar un sitio o rol de sistema de sitio de Configuration Manager.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc58ae7f7b5629319d239f9c48b5c6572fb28116
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691383"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Sistemas operativos compatibles con servidores de sistema de sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo, se detallan las versiones de Windows que puede usar para hospedar un sitio o un rol de sistema de sitio de Configuration Manager.

Use la información de este artículo con la información de los artículos siguientes:

- [Hardware recomendado para Configuration Manager](recommended-hardware.md)
- [Sitio y requisitos previos de sistema de sitio para Configuration Manager](site-and-site-system-prerequisites.md)
- [Números de tamaño y escala para Configuration Manager](size-and-scale-numbers.md)

## <a name="windows-server-2019"></a><a name="bkmk_2019"></a> Windows Server 2019

*Se aplica a Windows Server 2019: Standard y Datacenter* 

A partir de la versión 1810, se admite esta versión de sistema operativo en los siguientes roles:

#### <a name="site-servers"></a>Servidores de sitio

- Sitio de administración central  
- Sitio primario  
- Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

- Punto de servicio web del catálogo de aplicaciones  
- Punto de sitios web del catálogo de aplicaciones  
- Punto de sincronización de Asset Intelligence  
- Punto de registro de certificados  
- Punto de conexión de Cloud Management Gateway  
- Punto de servicio de almacenamiento de datos  
- Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto de Endpoint Protection  
- Punto de inscripción  
- Punto de proxy de inscripción  
- Punto de estado de reserva  
- Punto de administración
- Punto de servicios de informes  
- Punto de conexión de servicio  
- Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Punto de actualización de software  
- Punto de migración de estado

## <a name="windows-server-2016"></a><a name="bkmk_2016"></a> Windows Server 2016

*Se aplica a Windows Server 2016: Standard y Datacenter*

Esta versión de sistema operativo se admite en los siguientes roles:

#### <a name="site-servers"></a>Servidores de sitio

- Sitio de administración central  
- Sitio primario  
- Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

- Punto de servicio web del catálogo de aplicaciones  
- Punto de sitios web del catálogo de aplicaciones  
- Punto de sincronización de Asset Intelligence  
- Punto de registro de certificados  
- Punto de conexión de Cloud Management Gateway  
- Punto de servicio de almacenamiento de datos  
- Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto de Endpoint Protection  
- Punto de inscripción  
- Punto de proxy de inscripción  
- Punto de estado de reserva  
- Punto de administración
- Punto de servicios de informes  
- Punto de conexión de servicio  
- Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Punto de actualización de software  
- Punto de migración de estado

## <a name="windows-storage-server-2016"></a><a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>Servidor de sistema de sitio

- Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  

## <a name="windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Windows Server 2012 R2

*Se aplica a Windows Server 2012 R2: Standard y Datacenter*

#### <a name="site-servers"></a>Servidores de sitio

- Sitio de administración central  
- Sitio primario  
- Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

- Punto de servicio web del catálogo de aplicaciones  
- Punto de sitios web del catálogo de aplicaciones  
- Punto de sincronización de Asset Intelligence  
- Punto de registro de certificados  
- Punto de conexión de Cloud Management Gateway  
- Punto de servicio de almacenamiento de datos  
- Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto de Endpoint Protection  
- Punto de inscripción  
- Punto de proxy de inscripción  
- Punto de estado de reserva  
- Punto de administración
- Punto de servicios de informes  
- Punto de conexión de servicio  
- Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Punto de actualización de software  
- Punto de migración de estado  

## <a name="windows-server-2012"></a><a name="bkmk_2012"></a> Windows Server 2012  

*Se aplica a Windows Server 2012: Standard y Datacenter*

#### <a name="site-servers"></a>Servidores de sitio

- Sitio de administración central  
- Sitio primario  
- Sitio secundario  

#### <a name="site-system-servers"></a>Servidores de sistema de sitio

- Punto de servicio web del catálogo de aplicaciones  
- Punto de sitios web del catálogo de aplicaciones  
- Punto de sincronización de Asset Intelligence  
- Punto de registro de certificados  
- Punto de conexión de Cloud Management Gateway  
- Punto de servicio de almacenamiento de datos  
- Punto de distribución <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto de Endpoint Protection  
- Punto de inscripción  
- Punto de proxy de inscripción  
- Punto de estado de reserva  
- Punto de administración
- Punto de servicios de informes  
- Punto de conexión de servicio  
- Servidor de base de datos del sitio <sup>[Nota 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Punto de actualización de software  
- Punto de migración de estado  

## <a name="client-os-versions"></a><a name="bkmk_client"></a> Versiones de sistema operativo del cliente

Las siguientes versiones de sistema operativo de cliente se pueden usar como **punto de distribución** <sup>[Nota 1](#bkmk_note1)</sup>:  

- Windows 10 (x86, x64): Pro y Enterprise

    Para más información sobre las versiones de compilación compatibles, vea [Compatibilidad con Windows 10](support-for-windows-10.md).

- Windows 8.1 (x86, x64): Professional y Enterprise

Esta compatibilidad tiene las siguientes limitaciones:  

- Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

## <a name="server-core-installations"></a><a name="bkmk_core"></a> Instalaciones de Server Core

La instalación de Server Core de las siguientes versiones de sistema operativo de servidor se puede usar como **punto de distribución**:

- Windows Server 2019 (a partir de la versión 1810 de Configuration Manager)  
- Windows Server, versión 1809 (a partir de la versión 1810 de Configuration Manager)  
- Windows Server, versión 1803 (a partir de la versión 1802 de Configuration Manager)  
- Windows Server, versión 1709 (a partir de la versión 1710 de Configuration Manager)  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

Esta compatibilidad tiene las siguientes limitaciones:  

- Los puntos de distribución de este sistema operativo no admiten el entorno PXE ni multidifusión con los Servicios de implementación de Windows predeterminados. A partir de la versión 1806, puede habilitar para el entorno PXE un punto de distribución de este sistema operativo con la opción **Habilitar un respondedor PXE sin Servicios de implementación de Windows**. Para obtener más información, vea [Instalación y configuración de puntos de distribución](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

## <a name="general-notes"></a>Notas generales

### <a name="note-1-distribution-points"></a><a name="bkmk_note1"></a> Nota 1: Puntos de distribución

Los puntos de distribución admiten varias configuraciones diferentes y cada uno tiene requisitos diferentes. En algunos casos, estas configuraciones admiten la instalación no solo en los servidores sino también en sistemas operativos de clientes. Para obtener más información, consulte [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido).  

### <a name="note-2-site-database-servers"></a><a name="bkmk_note2"></a> Nota 2: Servidores de bases de datos del sitio

Los servidores de base de datos de sitio no se admiten en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte el artículo de Soporte técnico de Microsoft: [Puede encontrar problemas al instalar SQL Server en un controlador de dominio](https://support.microsoft.com/help/2032911). 

Además, los servidores de sitio secundario no se admiten en ningún controlador de dominio.  
