---
title: Actualizar clientes de Linux y UNIX
titleSuffix: Configuration Manager
description: Actualice un cliente en un servidor Linux o UNIX en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696823"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Cómo actualizar clientes para servidores Linux y UNIX en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

Puede actualizar la versión del cliente para Linux y UNIX en un equipo a una versión más reciente del cliente sin desinstalar primero el cliente actual. Para ello, instale el nuevo paquete de instalación de cliente en el equipo mientras usa la propiedad de línea de comandos **-keepdb**. Cuando se instala el cliente para Linux y UNIX, sobrescribe los datos de cliente existentes con los nuevos archivos de cliente. En cambio, la propiedad de línea de comandos **-keepdb** dirige el proceso de instalación para conservar el identificador único de cliente (GUID), la base de datos local de información y el almacén de certificados. La nueva instalación de cliente usará entonces esta información.  

 Por ejemplo, tiene un equipo RHEL5 x64 que ejecuta el cliente desde la versión original del cliente de Configuration Manager para Linux y UNIX. Para actualizar este cliente a la versión de cliente de la actualización acumulativa 1, ejecute de forma manual el script **install** para instalar el paquete de cliente correspondiente de la actualización acumulativa 1, con la adición del conmutador de línea de comandos **-keepdb**. Vea la siguiente línea de comandos de ejemplo:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Cómo usar una implementación de software para actualizar el cliente en servidores Linux y UNIX  
 Puede usar una implementación de software para actualizar el cliente para Linux y UNIX a una nueva versión de cliente. En cambio, el cliente de Configuration Manager no puede ejecutar directamente el script de instalación para instalar el cliente nuevo porque la instalación de un nuevo cliente exige desinstalar primero el cliente actual. Esta acción finalizaría el proceso de cliente de Configuration Manager que ejecuta el script de instalación antes de empezar la instalación del nuevo cliente. Para usar correctamente una implementación de software para instalar el cliente nuevo, debe programar la instalación para que se inicie en un momento futuro mediante las capacidades de programación integradas del sistema operativo.  

 Use una implementación de software para copiar primero los archivos para el nuevo paquete de instalación de cliente en el equipo cliente. Después, implemente y ejecute un script para programar el proceso de instalación de cliente. El script usa el comando **at** integrado del sistema operativo para retrasar su inicio. Cuando se ejecuta el script, es el sistema operativo cliente el que administra su funcionamiento y no el cliente de Configuration Manager en el equipo. Esto permite que la línea de comandos a la que llama el script desinstale primero el cliente de Configuration Manager y luego instale el nuevo cliente. Estas acciones completan el proceso de actualización de cliente en el equipo Linux o UNIX. Cuando se completa la actualización, Configuration Manager sigue administrando el cliente actualizado.  

 Use el procedimiento siguiente para configurar más fácilmente una implementación de software destinada a actualizar el cliente para Linux y UNIX. En los siguientes pasos y ejemplos se actualiza un equipo RHEL5 x64 que ejecuta la versión inicial del cliente a la versión de cliente de actualización acumulativa 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Uso de una implementación de software para actualizar el cliente en servidores Linux y UNIX  

1. Copie el nuevo archivo de paquete de instalación de cliente en el equipo que ejecuta el cliente de Configuration Manager que se va a actualizar.  

    Por ejemplo, coloque el paquete de instalación del cliente e instale el script de actualización acumulativa 1 en la siguiente ubicación en el equipo cliente: **/tmp/PATCH**  

2. Cree un script para administrar la actualización del cliente de Configuration Manager. Después, coloque una copia del script en la misma carpeta del equipo cliente que los archivos de instalación del cliente del paso 1.  

    El script no requiere un nombre específico, sino que debe contener líneas de comandos suficientes para usar los archivos de instalación del cliente desde una carpeta local en el equipo cliente y para instalar el paquete de instalación del cliente mediante la propiedad de línea de comandos **-keepdb**. Use la propiedad de línea de comandos **-keepdb** para mantener el identificador único del cliente actual para que pueda usarlo el nuevo cliente que está instalando.  

    Por ejemplo, cree un script denominado **upgrade.sh** que contenga las siguientes líneas:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Después, cópielo en la carpeta **/tmp/PATCH** en el equipo cliente.

3. Use la implementación de software para que cada cliente emplee el comando **at** integrado de los equipos para ejecutar el script **upgrade.sh** con un breve retraso antes de que se ejecute el script.  

    Por ejemplo, use la siguiente línea de comandos para ejecutar el script: **at -f /tmp/upgrade.sh -m now + 5 minutes**  

   Una vez que el cliente programe correctamente el script **upgrade.sh** que se va a ejecutar, el cliente enviará un mensaje de estado para indicar que la implementación de software se completó correctamente. Sin embargo, la instalación de cliente real la administra el equipo después del retraso. Una vez finalizada la actualización del cliente, revise el archivo **/var/opt/microsoft/scxcm.log** en el equipo cliente para validar la instalación. Confirme que el cliente está instalado y se comunica con el sitio. Para ello, vea los detalles del cliente en el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad** en la consola de Configuration Manager.  
