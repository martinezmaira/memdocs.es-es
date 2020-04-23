---
title: Inicio rápido del Centro de soporte técnico
titleSuffix: Configuration Manager
description: Capture rápidamente el estado de un cliente de Configuration Manager para solucionar problemas.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707463"
---
# <a name="support-center-quickstart-guide"></a>Guía de inicio rápido del Centro de soporte técnico

*Se aplica a: Configuration Manager (rama actual)*

El Centro de soporte técnico dispone de eficaces características, como la solución de problemas y la visualización de registros en tiempo real. También puede usarse para capturar en cuestión de minutos el estado de un equipo cliente de Configuration Manager. Esta capacidad incluye el acceso a clientes remotos.

Cree un completo archivo de *paquete de solución de problemas* (.zip) que capture el estado del cliente. El paquete no solo contiene archivos de registro. Puede incluir otros tipos de datos, como la configuración del Registro y configuraciones de cliente. Proporcione el paquete a un técnico de soporte técnico que use el Visor del Centro de soporte.



## <a name="prerequisites"></a>Requisitos previos

- Derechos administrativos locales para un cliente de Configuration Manager.  

- Instalador del Centro de soporte técnico. Este archivo se encuentra en el servidor de sitio en `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Para obtener más información, vea [Centro de soporte técnico: Instalación](support-center.md#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Paso 1: crear un paquete de datos en un cliente local

1.  Instale el Centro de soporte técnico en el cliente de Configuration Manager.  

2.  Vaya al menú **Iniciar** del grupo **Microsoft System Center** y seleccione **Support Center**.  

3.  En la pestaña Inicio de la cinta, seleccione **Recopilar datos seleccionados**. De forma predeterminada, el Centro de soporte técnico solo recopila el conjunto de datos mínimo: archivos de registro, configuración del cliente y sistema operativo.  

4.  Guarde el archivo de paquete de solución de problemas (.zip) en una carpeta en el equipo. De forma predeterminada, el nombre de archivo es similar al ejemplo siguiente: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Paso 2: ver el paquete de datos mediante el Visor del Centro de soporte técnico

1.  Inicie el **Visor del Centro de soporte técnico**. Esta acción puede realizarse en cualquier equipo en el que instale el Centro de soporte técnico.  

2.  Seleccione **Abrir paquete**, vaya al archivo de paquete y haga clic en **Abrir**.  

3.  Una vez que el Visor del Centro de soporte técnico procese el archivo, cambie a cada pestaña disponible. Vea los tipos de datos que el Centro de soporte técnico recopila de forma predeterminada:  

    - **Configuración**  

        - Configuración del cliente de Configuration Manager  

        - Sistema operativo  

        - Equipo  

        - Servicios  

        - Adaptadores de red  

    - **Registros**: seleccione una o más entradas de la lista y haga clic en **Abrir**. Esta acción abre los archivos de registro seleccionados en el visor de registros. Use esta característica para buscar códigos de error y use los filtros avanzados para analizar más rápidamente archivos de registro.  



## <a name="collect-more-data"></a>Recopilar más datos

Aparte de estas capacidades básicas, el Centro de soporte técnico también puede recabar otra información de estado de cliente de muy diversa índole. Abra **Support Center** y seleccione **Recopilar todos los datos**. Este proceso normalmente dura varios minutos, incluso en los equipos más modernos. El Centro de soporte técnico recopila los siguientes datos adicionales:

- **Directiva**: configuraciones de directiva de Configuration Manager, incluida la configuración de directiva solicitada y la configuración de directiva real.  

- **Certificados**: información de clave pública de los certificados de cliente. El Centro de soporte técnico no recopila claves privadas de certificados.  

- **Registro del cliente**: recopila información de configuración del cliente del Registro. El Centro de soporte técnico solo recopila información del Registro de Configuration Manager.  

- **WMI de cliente**: información de configuración del cliente de WMI. El Centro de soporte técnico no recopila la directiva del cliente.  

- **Solución de problemas**: datos de solución de problemas en tiempo real para ayudar a diagnosticar problemas comunes de cliente relativos a Active Directory, puntos de administración, redes, asignaciones de directivas y registro.  

- **Volcados de depuración**: realiza el volcado de depuración del cliente y procesos relacionados. Los volcados de depuración pueden ser de gran tamaño. Habilite esta opción solo cuando solucione problemas de rendimiento del cliente.  

