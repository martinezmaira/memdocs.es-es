---
title: Publicar datos del sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo publicar sitios de Configuration Manager en Servicios de dominio de Active Directory.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700983"
---
# <a name="publish-site-data-for-configuration-manager"></a>Publicar datos de sitio para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de extender el esquema de Active Directory para Configuration Manager, podrá publicar sitios de Configuration Manager en Active Directory Domain Services (AD DS). Esto permite a los equipos de Active Directory recuperar de forma segura la información del sitio desde una fuente de confianza. Aunque no es necesario publicar la información del sitio en AD DS para obtener las funciones básicas de Configuration Manager, esto puede reducir la sobrecarga de trabajo administrativo.  

-   **Cuando hay un sitio configurado para publicar en AD DS**, los clientes de Configuration Manager pueden buscar automáticamente puntos de administración con la publicación de Active Directory. Para hacerlo, realizan una consulta LDAP en un servidor de catálogo global.  

-   **Cuando un sitio no publica en AD DS**, los clientes deben tener un mecanismo alternativo para buscar su punto de administración predeterminado.  

Para más información sobre cómo los clientes pueden buscar un punto de administración, vea [Comprender cómo los clientes buscan servicios y recursos de sitio para Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurar sitios para publicar en AD DS  
 Estos son los pasos generales:  

-   Es necesario [extender el esquema de Active Directory para Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) en todos los bosques donde se vayan a publicar datos del sitio. Además, asegúrese de que el contenedor **System Management** esté presente.  

-   Necesita conceder a la cuenta de equipo de cada sitio primario que publicará datos los permisos de **control total** en el contenedor **System Management** y en todos sus objetos secundarios.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Para permitir que un sitio de Configuration Manager publique información del sitio en el bosque de Active Directory

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y haga clic en **Sitios**. Seleccione el sitio para el que quiera publicar sus datos de sitio. Después, en la pestaña **Inicio**, en el grupo **Propiedades**, haga clic en **Propiedades**.  

3.  En la pestaña **Publicación** de las propiedades del sitio, seleccione los bosques donde el sitio publicará los datos.  

4.  Haga clic en **Aceptar** para guardar la configuración.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Para configurar los bosques de Active Directory para la publicación  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Configuración de jerarquía** y, después, haga clic en **Bosques de Active Directory**. Si previamente ejecutó la detección de bosques de Active Directory, verá cada bosque detectado en el panel de resultados. El bosque local y todos los bosques de confianza se detectan cuando se ejecuta la detección de bosques de Active Directory. Sólo deben agregarse manualmente los bosques que no son de confianza.  

    -   Para configurar un bosque detectado anteriormente, seleccione el bosque en el panel de resultados. En la pestaña **Inicio**, en el grupo **Propiedades**, haga clic en **Propiedades** para abrir las propiedades del bosque. Continúe con el paso 3.  

    -   Para configurar un bosque nuevo que no se muestra en la lista, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Agregar bosque** para abrir el cuadro de diálogo **Agregar bosques**. Continúe con el paso 3.  

3.  En la pestaña **General**, complete las configuraciones del bosque que quiera detectar y especifique la **Cuenta de bosque de Active Directory**.  

    > [!NOTE]  
    >  La detección de bosques de Active Directory requiere una cuenta global para detectar bosques que no son de confianza y publicar en ellos. Si no utiliza la cuenta de equipo del servidor de sitio, solo se puede seleccionar una cuenta global.  

4.  Si planea permitir que los sitios publiquen datos del sitio en este bosque, en la pestaña **Publicación** , realice las configuraciones necesarias para publicar en este bosque.  

    > [!NOTE]  
    >  Si permite a los sitios publicar en un bosque, tendrá que extender el esquema de Active Directory de ese bosque para Configuration Manager. Es necesario que la cuenta del bosque de Active Directory tenga permisos de control total en el contenedor del sistema de ese bosque.  

5.  Cuando termine la configuración de este bosque para utilizarlo con la detección de bosques de Active Directory, haga clic en **OK** para guardar la configuración.  
