---
title: Extensiones de esquema
titleSuffix: Configuration Manager
description: Extienda el esquema de Active Directory para admitir Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904083"
---
# <a name="schema-extensions-for-configuration-manager"></a>Extensiones de esquema para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede extender el esquema de Active Directory para admitir Configuration Manager. De este modo, se edita el esquema de Active Directory de un bosque para agregar un nuevo contenedor y varios atributos que los sitios de Configuration Manager usan para publicar información de claves en Active Directory a la que los clientes pueden acceder de forma segura. Esta información puede simplificar la implementación y configuración de clientes, y ayuda a los clientes a buscar los recursos del sitio, como servidores con contenido distribuido o que ofrezcan varios servicios a los clientes.  

-   Le recomendamos que extienda el esquema de Active Directory, aunque no es obligatorio.  

Antes de [extender el esquema de Active Directory](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema), debe estar familiarizado con los Servicios de dominio de Active Directory y sentirse cómodo con la [modificación del esquema de Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Consideraciones para extender el esquema de Active Directory para Configuration Manager  

-   Las extensiones de esquema de Active Directory para Configuration Manager son iguales que las que se usan en Configuration Manager 2007 y Configuration Manager 2012. Si extendió el esquema anteriormente para cualquiera de las versiones, no tiene que volver a hacerlo.  

-   La extensión del esquema es una única acción irreversible que afecta a todo el bosque.  

-   Solo un usuario que pertenezca al grupo Administradores de esquema o que tenga delegados permisos suficientes para cambiar el esquema puede extender el esquema.  

-   Aunque puede extender el esquema antes o después de ejecutar el programa de instalación de Configuration Manager, le recomendamos que extienda el esquema antes de empezar a configurar los sitios y la jerarquía. Esto puede simplificar muchos de los pasos de configuración posteriores.  

-   Después de extender el esquema, el catálogo global de Active Directory se replica en todo el bosque. Por tanto, planee extender el esquema cuando no esté previsto que el tráfico de replicación vaya a afectar negativamente a otros procesos que dependen de la red:  

    -   En los bosques de Windows 2000, la extensión del esquema produce una sincronización completa de todo el catálogo global.  

    -   A partir de bosques de Windows 2003, solo se replican los atributos agregados.  

**Dispositivos y clientes que no usan el esquema de Active Directory:**  

-   Dispositivos móviles que administra el conector de Exchange Server  

-   El cliente para equipos Mac  

-   El cliente para servidores Linux y UNIX  

-   Dispositivos móviles inscritos por Configuration Manager  

-   Dispositivos móviles que están inscritos por Microsoft Intune  

-   Clientes heredados de dispositivo móvil  

-   Clientes de Windows que están configurados para la administración de clientes solo de Internet  

-   Los clientes de Windows que Configuration Manager detecta que están en Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Capacidades que se benefician de la extensión del esquema  
**Asignación de sitio e instalación de equipo cliente:** cuando se instala un nuevo cliente en un equipo Windows, el cliente busca las propiedades de instalación en Active Directory Domain Services.  

-   **Soluciones alternativas:** si no extiende el esquema, use una de las opciones siguientes para ofrecer detalles de configuración que es necesario instalar en los equipos:  

    -   **Use la instalación de inserción de cliente**. Antes de usar el método de instalación de cliente, asegúrese de que se cumplen todos los requisitos previos. Para obtener más información, consulte la sección “Dependencias de los métodos de instalación” en [Requisitos previos para la implementación de clientes en equipos Windows con System Center Configuration Manager](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

    -   **Instale manualmente los clientes** y defina las propiedades de instalación de cliente mediante las propiedades de línea de comandos de instalación de CCMSetup. Esto debe incluir lo siguiente:  

        -   Especifique un punto de administración o ruta de acceso de origen desde donde el equipo puede descargar los archivos de instalación usando la propiedad de CCMSetup **/mp:=&lt;nombre de equipo de nombre de punto de administración\>** o **/source:&lt;ruta de acceso de los archivos de origen del cliente\>** en la línea de comandos de CCMSetup durante la instalación del cliente.  

        -   Especifique una lista de los puntos de administración iniciales que el cliente puede usar para asignarlos al sitio y, después, descargue la configuración del sitio y la directiva de cliente. Utilice la propiedad SMSMP de CCMSetup Client.msi para hacer esto.  

    -   **Publique el punto de administración en DNS o WINS** y configure los clientes para que usen este método de ubicación del servicio.  

**Configuración de puerto para la comunicación cliente a servidor**: cuando se instala un cliente, se configura con la información del puerto almacenada en Active Directory. Si posteriormente se cambia el puerto de comunicación entre cliente y servidor para un sitio, un cliente puede obtener esta nueva configuración de puerto de Active Directory Domain Services.  

-   **Soluciones alternativas:** si no extiende el esquema, use una de las opciones siguientes para proporcionar nuevas configuraciones de puerto para los clientes existentes:  

    -   **Reinstale los clientes** con las opciones que configuren el puerto nuevo.  

    -   **Implemente un script personalizado para los clientes que actualice la información de puerto**. Si los clientes no pueden comunicarse con un sitio debido a un cambio de puerto, no podrá usar Configuration Manager para implementar este script. Por ejemplo, podría utilizar una directiva de grupo.  

**Escenarios de implementación de contenido**: cuando crea contenido en un sitio y, a continuación, implementa ese contenido en otro sitio de la jerarquía, el sitio receptor debe poder verificar la firma de los datos del contenido firmado. Esto requiere acceso a la clave pública del sitio de origen en el que crea estos datos. Al extender el esquema de Active Directory para Configuration Manager, la clave pública de un sitio estará disponible para todos los sitios de la jerarquía.  

-   **Solución alternativa:** si no extiende el esquema, use la herramienta de mantenimiento de la jerarquía, **preinst.exe**, para intercambiar la información de clave segura entre sitios.  

     Por ejemplo, si tiene previsto crear contenido en un sitio primario e implementar ese contenido en un sitio secundario que esté por debajo de otro sitio primario, necesitará extender el esquema de Active Directory para permitir que el sitio secundario obtenga la clave pública del sitio primario de origen, o bien tendrá que usar preinst.exe para compartir las claves entre los dos sitios directamente.  

## <a name="active-directory-attributes-and-classes"></a>Atributos y clases de Active Directory  
Si extiende el esquema para Configuration Manager, las siguientes clases y atributos se agregarán al esquema y estarán disponibles para todos los sitios de Configuration Manager de ese bosque de Active Directory.  

-   Atributos:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        en  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Clases:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]
> 
>  Las extensiones de esquema podrían incluir atributos y clases que provienen de versiones anteriores del producto, pero que Configuration Manager no usa. Por ejemplo:  
> 
> 
> - Atributo: cn=MS-SMS-Site-Boundaries  
>   -   Clase: cn=MS-SMS-Server-Locator-Point  

Para asegurarse de que las listas anteriores están actualizadas, consulte el archivo **ConfigMgr_ad_schema.LDF** de la carpeta **\SMSSETUP\BIN\x64** del medio de instalación de Configuration Manager.  
