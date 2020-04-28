---
title: Planeamiento de permisos de plantilla de certificado
titleSuffix: Configuration Manager
description: Aprenda a planear los permisos que necesita para configurar las plantillas de certificado que usa Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 075d371a334f26a788c656fe85ec01ae2338eb26
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074833"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Planeamiento de los permisos de plantilla de certificado para perfiles de certificado en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


La siguiente información puede ayudarle a planear la configuración de permisos de las plantillas de certificado que Configuration Manager usa cuando se implementan perfiles de certificado.  

## <a name="default-security-permissions-and-considerations"></a>Consideraciones y permisos de seguridad predeterminados  
 Los permisos de seguridad predeterminados necesarios para las plantillas de certificado que usará Configuration Manager para solicitar certificados para usuarios y dispositivos son los siguientes:  

- Lectura e Inscripción para la cuenta que el grupo de aplicaciones Servicio de inscripción de dispositivos de red usa  

- Lectura para la cuenta que ejecuta la consola de Configuration Manager  

  Para más información sobre estos permisos de seguridad, vea [Infraestructura de certificados](../deploy-use/certificate-infrastructure.md).  

  Cuando se usa esta configuración predeterminada, los usuarios y los dispositivos no pueden solicitar directamente certificados de las plantillas de certificado. El Servicio de inscripción de dispositivos de red debe iniciar todas las solicitudes. Esta restricción es sumamente importante, ya que las plantillas de certificado deben configurarse con **Proporcionado por el solicitante** para el sujeto del certificado, lo que implica un riesgo de suplantación si un usuario no autorizado o un dispositivo comprometido solicitan un certificado. En la configuración predeterminada, el Servicio de inscripción de dispositivos de red debe iniciar la solicitud. Sin embargo, el riesgo de suplantación continúa si el servicio que ejecuta el Servicio de inscripción de dispositivos de red se ve comprometido. Para evitar este riesgo, siga todas las recomendaciones de seguridad para el Servicio de inscripción de dispositivos de red y el equipo que ejecuta este servicio de rol.  

  Si los permisos de seguridad predeterminados no satisfacen sus requisitos empresariales, tiene otra opción para configurar los permisos de seguridad en las plantillas de certificado: Puede agregar permisos de lectura e inscripción para usuarios y equipos.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Agregar permisos de lectura e inscripción para usuarios y equipos  
 Agregar permisos de lectura e inscripción para usuarios y equipos puede ser la opción adecuada si un equipo distinto administra el equipo de infraestructura de entidad de certificación (CA), y dicho equipo quiere que Configuration Manager compruebe que los usuarios tienen una cuenta válida de Servicios de dominio de Active Directory antes de enviarles un perfil de certificado para solicitar un certificado de usuario. Para esta configuración, debe especificar uno o varios grupos de seguridad que contienen los usuarios y, a continuación, otorgar a los grupos permisos de lectura e inscripción en las plantillas de certificado. En este escenario, el administrador de CA administra el control de seguridad.  

 De forma similar, puede especificar uno o varios grupos de seguridad que contienen cuentas de equipo y conceder a los grupos permisos de lectura e inscripción en las plantillas de certificado. Si implementa un perfil de certificado de equipo en un equipo que es miembro de un dominio, deben concederse permisos de lectura e inscripción a la cuenta de equipo del equipo. Estos permisos no son necesarios si el equipo no es miembro de un dominio; por ejemplo, si es un equipo de grupo de trabajo o un dispositivo móvil personal.  

 Aunque esta configuración utiliza un control de seguridad adicional, no se recomienda. El motivo es que los usuarios o propietarios especificados de los dispositivos podrían solicitar certificados al margen de Configuration Manager, y suministrar valores para el sujeto del certificado que podrían usarse para suplantar a otro usuario o dispositivo.  

 Además, si especifica cuentas que no se pueden autenticar cuando se realiza la solicitud de certificado, se producirá un error de solicitud de certificado de forma predeterminada. Por ejemplo, se producirá un error de solicitud de certificado si el servidor que ejecuta el Servicio de inscripción de dispositivos de red está en un bosque de Active Directory que no es de confianza para el bosque que contiene el servidor del sistema de sitios de punto de registro de certificado. Puede configurar el punto de registro de certificado para continuar si no se puede autenticar una cuenta porque no se recibe ninguna respuesta de un controlador de dominio. Sin embargo, no es una práctica de seguridad recomendada.  

 Tenga en cuenta que si el punto de registro de certificado se configura para comprobar los permisos de la cuenta y un controlador de dominio está disponible y rechaza la solicitud de autenticación (por ejemplo, porque la cuenta está bloqueada o se ha eliminado), se producirá un error de solicitud de inscripción de certificado.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Para comprobar los permisos de lectura e inscripción de los usuarios y los equipos que son miembros de un dominio  

1.  En el servidor del sistema de sitio que hospeda el punto de registro del certificado, cree la siguiente clave DWORD del Registro con un valor de 0: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Si una cuenta no se puede autenticar porque no hay ninguna respuesta de un controlador de dominio y desea omitir la comprobación de permisos:  

    -   En el servidor del sistema de sitio que hospeda el punto de registro del certificado, cree la siguiente clave DWORD del Registro con un valor de 1: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  En la CA emisora, en la ficha **Seguridad** en las propiedades de la plantilla de certificado, agregue uno o varios grupos de seguridad para conceder permisos de lectura e inscripción a las cuentas de usuario o dispositivo.  
