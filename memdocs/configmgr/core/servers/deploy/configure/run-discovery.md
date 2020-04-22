---
title: Detección de recursos de usuario y dispositivo
titleSuffix: Configuration Manager
description: Lea la información general sobre el proceso de detección y los registros de datos de detección.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700993"
---
# <a name="run-discovery-for-configuration-manager"></a>Ejecución de la detección para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use uno o varios métodos de detección en Configuration Manager para encontrar recursos de usuarios y dispositivos que pueda administrar. También puede usar la detección para identificar la infraestructura de red en su entorno. Existen varios métodos de detección que puede usar para detectar elementos y cada método tiene su propia configuración y limitaciones.  

## <a name="overview-of-discovery"></a>Información general sobre la detección  
 La detección es el proceso mediante el cual Configuration Manager conoce los elementos que puede administrar. Estos son los métodos de detección disponibles:  

-   Detección de bosques de Active Directory  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

-   Detección de latidos  

-   Detección de redes  

-   detección de servidores  

> [!TIP]  
>  Encontrará más información sobre los métodos de detección individuales en [Acerca de los métodos de detección en Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Para obtener ayuda para seleccionar los métodos que va a usar y en qué sitios de la jerarquía, vea [Selección de los métodos de detección que se usarán en Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Para usar la mayoría de los métodos de detección necesita habilitar el método en un sitio y configurarlo para buscar ubicaciones específicas de red o de Active Directory. Cuando se ejecuta, consulta en la ubicación especificada información sobre los dispositivos o usuarios que Configuration Manager puede administrar. Cuando un método de detección encuentra información sobre un recurso, copia esa información en un archivo denominado registro de datos de detección (DDR). Después, un sitio de administración central o primario procesa el archivo. El procesamiento de un DDR crea un nuevo registro en la base de datos del sitio para los recursos recién detectados, o bien actualiza los registros existentes con la información nueva.  

 Algunos métodos de detección pueden generar un gran volumen de tráfico de red y los DDR generados pueden producir un uso significativo de recursos de CPU durante el procesamiento. Por lo tanto, le recomendamos que use solo los métodos de detección que necesite para cumplir sus objetivos. Podría comenzar usando solo uno o dos métodos de detección y luego más tarde habilitar métodos adicionales de una manera controlada para ampliar el nivel de detección en su entorno.  

 Después de agregar la información de detección a la base de datos del sitio, esta se replicará en todos los sitios de la jerarquía, independientemente del sitio donde se haya detectado o procesado. Por lo tanto, aunque se pueden configurar distintas programaciones y opciones para métodos de detección en diferentes sitios, solo se puede ejecutar un método de detección específico en un sitio. Esto reduce el uso del ancho de banda de red con acciones de detección duplicadas y reduce el procesamiento de datos de detección redundantes en varios sitios.  

 Puede usar los datos de detección para crear colecciones y consultas personalizadas que agrupen de forma lógica los recursos de las tareas de administración. Por ejemplo:  

-   Insertar instalaciones de clientes o actualizar.  

-   Puede implementar el contenido en usuarios o dispositivos.  

-   Puede implementar la configuración de cliente y las configuraciones relacionadas.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Acerca de los registros de datos de detección  
 Los DDR son archivos creados por un método de detección. Contienen información sobre un recurso que puede administrar en Configuration Manager, como equipos, usuarios y, en algunos casos, infraestructura de red. Estos se procesan en sitios primarios o en sitios de administración central. Después de agregar a la base de datos la información de recursos del DDR, se elimina el DDR y se replica la información como datos globales en todos los sitios de la jerarquía.  

 El sitio en que se procesa un DDR depende de la información que contiene:  

-   Los DDR de los nuevos recursos detectados que no se encuentran en la base de datos se procesan en el sitio de primer nivel de la jerarquía. El sitio de primer nivel crea un registro de recursos en la base de datos y le asigna un identificador único. Los DDR se transfieren mediante la replicación basada en archivos hasta que alcanzan el sitio de primer nivel.  

-   Los DDR de los objetos detectados anteriormente se procesan en sitios primarios. Los sitios primarios secundarios no transfieren DDR al sitio de administración central cuando el DDR contiene información sobre un recurso que ya está en la base de datos.  

-   Los sitios secundarios no procesan los DDR y siempre los transfieren al sitio primario principal con la replicación basada en archivos.  

Los archivos DDR se identifican por la extensión .ddr y tienen un tamaño típico de aproximadamente 1 kB.  

## <a name="get-started-with-discovery"></a>Introducción a la detección:  
 Antes de usar la consola de Configuration Manager para configurar la detección, es importante que comprenda las diferencias entre los métodos, lo que hacen y, en algunos casos, sus limitaciones.  

Los temas siguientes pueden servir como base para ayudarle a usar correctamente los métodos de detección:  

-   [Acerca de los métodos de detección en Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selección de los métodos de detección que se usarán en Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Después, cuando conozca los métodos que quiere usar, busque información para configurar cada método en [Configurar métodos de detección para Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
