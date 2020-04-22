---
title: Procedimientos recomendados para la implementación de clientes
titleSuffix: Configuration Manager
description: Conozca los procedimientos recomendados para implementar clientes en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693883"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Procedimientos recomendados para la implementación de clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilice la instalación de clientes basada en actualizaciones de software para equipos de Active Directory  
 Este método de implementación de clientes usa tecnologías de Windows existentes, se integra con la infraestructura de Active Directory, requiere una configuración mínima en Configuration Manager, es el más fácil de configurar para los firewalls y es el más seguro. Al usar los grupos de seguridad y el filtrado WMI para la configuración de la directiva de grupo, dispone también de una gran flexibilidad para controlar en qué equipos se instala el cliente de Configuration Manager.  

 Para más información, vea [How to Install Configuration Manager Clients by Using Software Update-Based Installation (Cómo instalar clientes de Configuration Manager mediante una instalación basada en software)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Extienda el esquema de Active Directory y publique el sitio para que pueda ejecutar CCMSetup sin opciones de línea de comandos  
 Cuando extiende el esquema de Active Directory para Configuration Manager y el sitio se publica en Active Directory Domain Services, muchas propiedades de instalación de cliente se publican en Active Directory Domain Services. Si un equipo puede ubicar estas propiedades de instalación de cliente, puede usarlas durante la implementación de cliente de Configuration Manager. Dado que esta información se genera automáticamente, se elimina el riesgo de error humano asociado con escribir manualmente las propiedades de la instalación.  

 Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Usar una implementación por fases para administrar el uso de CPU  
 Minimice el efecto de los requisitos de procesamiento de la CPU en el servidor del sitio mediante una implementación por fases de los clientes. Implemente los clientes fuera del horario comercial, para que otros servicios dispongan de más ancho de banda durante el día y los usuarios no se vean afectados si su equipo se ralentiza o necesita reiniciarse.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Habilite la actualización automática una vez finalizada la implementación principal de clientes  
 [Las actualizaciones automáticas de cliente](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) son útiles cuando quiere actualizar un número reducido de equipos cliente que es posible que su método de instalación principal de cliente haya omitido porque estaban sin conexión. 

> [!NOTE]  
>  Las mejoras de rendimiento de Configuration Manager permiten usar las actualizaciones automáticas como método principal de actualización de clientes. Sin embargo, el rendimiento dependerá de la infraestructura de la jerarquía como, por ejemplo, el número de clientes.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Utilice SMSMP y FSP si instala el cliente con propiedades de client.msi  
 La propiedad SMSMP especifica el punto de administración inicial con el que el cliente se comunica y elimina la dependencia de soluciones de ubicación de servicios como Servicios de dominio de Active Directory, DNS o WINS.  

 Utilice la propiedad FSP e instale un punto de estado de reserva, de modo que pueda supervisar la instalación y asignación del cliente, e identificar los problemas de comunicación.  

 Para más información sobre estas opciones, vea [Acerca de las propiedades de instalación de clientes](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Instalar paquetes de idioma del cliente antes de instalar los clientes  
Se recomienda que instale los paquetes de idioma de cliente antes de implementar el cliente. Si instala los [paquetes de idioma de cliente](../../../../core/servers/deploy/install/language-packs.md) (para habilitar idiomas adicionales) en un sitio después de instalar los clientes, debe volver a instalar los clientes para poder usar esos idiomas. Para los clientes de dispositivos móviles, debe borrar el dispositivo móvil e inscribirlo otra vez.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Preparar los certificados PKI necesarios por adelantado  
 Para administrar dispositivos en Internet, dispositivos móviles inscritos y equipos Mac, debe tener los certificados PKI en sistemas del sitio (puntos de administración y distribución) y los dispositivos cliente. En redes de producción, es posible que necesite aprobación de administración de cambios para utilizar los nuevos certificados y reiniciar los servidores del sistema de sitio, o los usuarios tendrán que cerrar e iniciar sesión para la nueva pertenencia a grupos. Además, tendría que dejar tiempo suficiente para la replicación de los permisos de seguridad y las nuevas plantillas de certificado.  

 Para más información sobre los certificados PKI, vea [Requisitos de certificados PKI para Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Antes de instalar clientes, configure las opciones de cliente y las ventanas de mantenimiento requeridas  
 Aunque puede [configurar los ajustes del cliente](../../../../core/clients/deploy/configure-client-settings.md) y las ventanas de mantenimiento antes o después de instalar los clientes, es recomendable configurar los ajustes necesarios antes de instalar los clientes para que estos valores se empleen tan pronto como el cliente esté instalado. 

 Configure ventanas de mantenimiento para servidores y dispositivos de Windows Embedded, a fin de garantizar la continuidad empresarial de los dispositivos críticos. Las ventanas de mantenimiento garantizan que las actualizaciones de software y el software antimalware requeridos no reinician el equipo durante el horario comercial.  

> [!IMPORTANT]  
>  Para equipos de Windows 10 que se van a proteger con el filtro de escritura unificado (UWF), debe configurar el dispositivo para UWF antes de instalar el cliente. Esto permite a Configuration Manager instalar el cliente con un proveedor de credenciales personalizadas que evita que los usuarios con pocos derechos inicien sesión en el dispositivo durante el modo de mantenimiento.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planear la experiencia de inscripción de usuario para dispositivos móviles y equipos Mac   
 Si los usuarios inscriben sus propios equipos y dispositivos móviles Mac mediante Configuration Manager, planee la experiencia del usuario. Por ejemplo, es posible que cree un script para el proceso de instalación e inscripción mediante el uso de una página web para que los usuarios especifiquen la cantidad mínima de información necesaria, y enviar las instrucciones con un vínculo por correo electrónico.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Usar filtros de escritura basados en archivo para dispositivos de Windows Embedded 
 Los dispositivos incrustados que utilizan filtros de escritura mejorados (EWF) son propensos a experimentar resincronizaciones de mensaje de estado. Si tiene pocos dispositivos incrustados que utilizan filtros de escritura mejorados, es posible que no perciba este comportamiento. Sin embargo, si cuenta con una gran cantidad de dispositivos incrustados que resincronizan su información, tales como el envío del inventario completo del lugar de un inventario diferencial, esto puede generar un incremento notable en los paquetes de red y un mayor procesamiento de la CPU en el servidor de sitio.  

 Si puede elegir qué tipo de filtro de escritura habilitar, elija los filtros de escritura basados ​​en archivo y configure excepciones para conservar el estado del cliente y los datos de inventario entre los reinicios del dispositivo por motivos de eficiencia de la red y la CPU en el cliente de Configuration Manager. Para más información sobre los filtros de escritura, vea [Planeación de implementación de cliente en dispositivos de Windows Embedded en Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Para más información sobre el número máximo de clientes de Windows Embedded que un sitio primario puede admitir, vea [Supported operating systems for clients and devices (Sistemas operativos compatibles con clientes y dispositivos)](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
