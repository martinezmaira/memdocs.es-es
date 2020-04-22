---
title: Administración de clientes Linux y UNIX
titleSuffix: Configuration Manager
description: Administre clientes en servidores Linux y UNIX en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690053"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Administración de clientes en servidores Linux y UNIX en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

Cuando administre servidores Linux y UNIX con Configuration Manager, puede configurar recopilaciones, ventanas de mantenimiento y configuraciones de cliente como ayuda en esta tarea. Además, aunque el cliente de Configuration Manager para Linux y UNIX no tiene una interfaz de usuario, puede forzarlo a sondear manualmente la directiva de cliente.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Colecciones de servidores Linux y UNIX  
 Use recopilaciones para administrar grupos de servidores Linux y UNIX de la misma forma que usa recopilaciones para administrar otros tipos de cliente. Las colecciones pueden ser de pertenencia directa o basadas en consultas. Estas últimas identifican los sistemas operativos cliente, las configuraciones de hardware u otros detalles sobre el cliente que se almacenan en la base de datos del sitio. Por ejemplo, puede usar colecciones que incluyan servidores Linux y UNIX para administrar la siguiente configuración:  

- Configuración de cliente  

- Implementaciones de software  

- Aplicar ventanas de mantenimiento  

  Antes de poder identificar un cliente Linux o UNIX por su sistema operativo o distribución, debe recopilar el [inventario de hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) desde el cliente.  

  La configuración de cliente predeterminada para el inventario de hardware incluye información sobre el sistema operativo del equipo de cliente. Puede usar la propiedad **Título** de la clase **Sistema operativo** para identificar el sistema operativo de un servidor Linux o UNIX.  

  Puede ver detalles sobre los equipos que ejecutan el cliente de Configuration Manager para Linux y UNIX en el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad** en la consola de Configuration Manager. En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, puede ver el nombre del sistema operativo de cada equipo en la columna **Sistema operativo**.  

  De forma predeterminada, los servidores Linux y UNIX son miembros de la recopilación **Todos los sistemas** . Le recomendamos crear recopilaciones personalizadas que incluyan solo servidores Linux y UNIX, o un subconjunto de ellos. Las colecciones personalizadas permiten administrar operaciones como la implementación de software o la asignación de la configuración de cliente a grupos de equipos similares, de manera que pueda medir con precisión el éxito de una implementación.   

  Cuando cree una recopilación personalizada para servidores Linux y UNIX, incluya consultas de regla de pertenencia que contengan el atributo de título para el atributo de sistema operativo. Para más información sobre cómo crear recopilaciones, vea [Cómo crear recopilaciones](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Ventanas de mantenimiento para servidores Linux y UNIX  
 El cliente de Configuration Manager para servidores de Linux y UNIX admite el uso de [ventanas de mantenimiento](../../../core/clients/manage/collections/use-maintenance-windows.md). Esta compatibilidad no se ha modificado para los clientes basados en Windows.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Configuración de cliente para servidores Linux y UNIX  
 Puede [configurar las opciones de cliente](../../../core/clients/deploy/configure-client-settings.md) que se aplican a servidores Linux y UNIX de la misma manera que configura las opciones para otros clientes.  

 De forma predeterminada, la **Configuración predeterminada del agente cliente** se aplica a servidores Linux y UNIX. También puede crear opciones de configuración de cliente personalizadas e implementarlas en recopilaciones de clientes específicos.  

 No hay ninguna configuración de cliente adicional que se aplique solo a los clientes de Linux y UNIX. Sin embargo, hay opciones de configuración de cliente predeterminadas que no se aplican a clientes de Linux y UNIX. El cliente para Linux y UNIX solo aplica opciones de configuración para funciones que admita.  

 Por ejemplo, una configuración de dispositivos cliente personalizada que permita y configure valores de control remoto se omitirá en los servidores Linux y UNIX, ya que el cliente de Linux y UNIX no admite control remoto.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Directiva de equipo para servidores Linux y UNIX  
 El cliente para servidores Linux y UNIX sondea periódicamente en su sitio la directiva de equipo para obtener información sobre las configuraciones solicitadas y para comprobar las implementaciones.  

 También puede forzar al cliente en un servidor Linux o UNIX para que sondee inmediatamente la directiva de equipo. Para hacer esto, use las credenciales **raíz** en el servidor para ejecutar el comando siguiente: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 Los detalles sobre el sondeo de la directiva de equipo se escriben en el archivo de registro de cliente compartido **scxcm.log**.  

> [!NOTE]  
>  El cliente de Configuration Manager para Linux y UNIX nunca solicita ni procesa la directiva de usuario.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> Cómo administrar certificados en el cliente para Linux y UNIX  
 Después de instalar el cliente para Linux y UNIX, puede usar la herramienta **certutil** para actualizar el cliente con un nuevo certificado PKI e importar una nueva lista de revocación de certificados (CRL). Al instalar el cliente para Linux y UNIX, esta herramienta se coloca en `/opt/microsoft/configmgr/bin/certutil`. 

 Para administrar certificados, en cada cliente ejecute certutil con una de las siguientes opciones:  

|Opción|Más información|  
|------------|----------------------|  
|`importPFX`|Use esta opción para especificar un certificado que reemplace el certificado que actualmente usa un cliente.<br /><br /> Cuando use `-importPFX`, también debe usar el parámetro de línea de comandos `-password` para proporcionar la contraseña asociada con el archivo PKCS #12.<br /><br /> Use `-rootcerts` para especificar más requisitos de certificado raíz.<br /><br /> Ejemplo: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Use esta opción para actualizar el servidor de sitio que firma el certificado que se encuentra en el servidor de administración.<br /><br /> Ejemplo: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Use esta opción para actualizar la CRL en el cliente con una o varias rutas de archivos CRL.<br /><br /> Ejemplo: `certutil -importcrl <comma separated CRL file paths>`|  
