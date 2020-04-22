---
title: Publicación y el esquema de Active Directory
titleSuffix: Configuration Manager
description: Extienda el esquema de Active Directory para Configuration Manager para simplificar el proceso de implementación y configuración de clientes.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701553"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Preparar Active Directory para la publicación de sitios

*Se aplica a: Configuration Manager (rama actual)*

Al extender el esquema de Active Directory para Configuration Manager, introducirá nuevas estructuras en Active Directory que los sitios de Configuration Manager pueden usar para publicar información de claves en una ubicación segura a la que pueden acceder fácilmente los clientes.  

Le recomendamos que use Configuration Manager con un esquema de Active Directory extendido al administrar los clientes locales. Un esquema extendido puede simplificar el proceso de implementación y configuración de clientes. Un esquema extendido también permite a los clientes buscar recursos de manera eficiente, como servidores de contenido y servicios adicionales proporcionados por los diferentes roles de sistema de sitio de Configuration Manager.  

-   Si no está familiarizado con lo que el esquema extendido permite realizar en una implementación de Configuration Manager, vea [Extensiones de esquema para Configuration Manager](../../../core/plan-design/network/schema-extensions.md) para que le resulte más fácil tomar esta decisión.  

-   Si no usa un esquema extendido, puede configurar otros métodos (como DNS y WINS) para ubicar los servicios y los servidores de sistema de sitio. Estos métodos de ubicación del servicio requieren configuraciones adicionales y no son el método preferido para la ubicación del servicio de los clientes. Para más información, vea [Comprender cómo los clientes buscan servicios y recursos de sitio para Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Si su esquema de Active Directory se ha extendido para Configuration Manager 2007 o System Center 2012 Configuration Manager, no necesita hacer nada más. Las extensiones de esquema no se modificarán y ya estarán en su lugar.  

La extensión del esquema es una acción que se realiza una sola vez para cada bosque. Siga estos pasos para extender el esquema de Active Directory y usar el esquema extendido:  

## <a name="step-1-extend-the-schema"></a>Paso 1. Extender el esquema  
Para extender el esquema para Configuration Manager:  

-   Use una cuenta que pertenezca al grupo de seguridad Administradores de esquema.  

-   Inicie sesión en el controlador de dominio del maestro de esquema.  

-   Ejecute la herramienta **Extadsch.exe** o use la utilidad de línea de comandos LDIFDE con el archivo **ConfigMgr_ad_schema.ldf** . La herramienta y el archivo se encuentran en la carpeta **SMSSETUP\BIN\X64** en los medios de instalación de Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opción A: usar Extadsch.exe  

1.  Ejecute **extadsch.exe** para agregar las clases y los atributos nuevos al esquema de Active Directory.  

    > [!TIP]  
    >  Ejecute esta herramienta desde una línea de comandos para ver los comentarios mientras se ejecuta.  

2.  Para comprobar que la extensión de esquema se ha completado correctamente, revise el archivo extadsch.log en la raíz de la unidad del sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opción B: usar el archivo LDIF  

1.  Edite el archivo **ConfigMgr_ad_schema.ldf** para definir el dominio raíz de Active Directory que quiere extender:  

    -   Cambie todas las instancias del texto **DC=x** del archivo por el nombre completo del dominio que quiera extender.  

    -   Por ejemplo, si el nombre completo del dominio que se va a extender es widgets.microsoft.com, cambie todas las instancias de DC=x del archivo a **DC=widgets, DC=microsoft, DC=com**.  

2.  Use la utilidad de línea de comandos LDIFDE para importar el contenido del archivo **ConfigMgr_ad_schema.ldf** en Active Directory Domain Services:  

    -   Por ejemplo, la siguiente línea de comandos importará las extensiones de esquema en Active Directory Domain Services, activará el registro detallado y creará un archivo de registro durante el proceso de importación: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;ubicación donde se almacenará el archivo de registro\>** .  

3.  Para comprobar que la extensión de esquema se ha completado correctamente, revise el archivo de registro creado por la línea de comandos del paso anterior.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Paso 2.  Crear el contenedor System Management y conceder permisos de sitios al contenedor  
 Después de extender el esquema, necesita crear un contenedor denominado **System Management** en Active Directory Domain Services (AD DS):  

-   Cree este contenedor una vez en cada dominio que tenga un sitio primario o secundario que vaya a publicar datos en Active Directory.  

-   Por cada contenedor, conceda permisos a la cuenta de equipo de cada servidor de sitio primario y secundario que vaya a publicar datos en ese dominio. Cada cuenta necesita permisos de **Control total** en el contenedor, con el permiso avanzado **Aplicar en** igual a **Este objeto y todos los descendientes**.  

#### <a name="to-add-the-container"></a>Para agregar el contenedor  

1.  Use una cuenta que tenga el permiso **Crear todos los objetos secundarios** en el contenedor **System** en Servicios de dominio de Active Directory.  

2.  Ejecute **ADSI Edit** (adsiedit.msc) y conéctese al dominio del servidor de sitio.  

3.  Cree el contenedor:  

    -   Expanda **Dominio** &lt;nombre de dominio completo del equipo\>, expanda &lt;nombre distintivo\>, haga clic con el botón derecho en **CN=System**, seleccione **Nuevo** y, después, haga clic en **Objeto**.  

    -   En el cuadro de diálogo **Crear objetos**, seleccione **Contenedor** y, después, **Siguiente**.  

    -   En el cuadro **Valor**, escriba **System Management** y, después, seleccione **Siguiente**.  

4.  Asignar permisos:  

    > [!NOTE]  
    >  Si lo prefiere, puede utilizar otras herramientas como la herramienta administrativa Usuarios y equipos de Active Directory (dsa.msc) para agregar permisos al contenedor.  

    -   Haga clic con el botón derecho en **CN=System Management** y, después, haga clic en **Propiedades**.  

    -   Seleccione la pestaña **Seguridad**, haga clic en **Agregar** y, después, agregue la cuenta de equipo del servidor de sitio con el permiso **Control total**.  

    -   Haga clic en **Avanzadas**, seleccione la cuenta de equipo del servidor del sitio y, después, haga clic en **Editar**.  

    -   En la lista **Aplicar en**, seleccione **Este objeto y todos los descendientes**.  

5.  Haga clic en **Aceptar** para cerrar la consola y guardar la configuración.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Paso 3. Configurar sitios para la publicación en Active Directory Domain Services  
 Después de configurar el contenedor, conceder los permisos e instalar un sitio primario de Configuration Manager, puede configurar el sitio para la publicación de datos en Active Directory.  

 Para más información sobre la publicación, vea [Publicar datos de sitio para Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
