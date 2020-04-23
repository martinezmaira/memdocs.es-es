---
title: Seguridad y privacidad de perfiles de certificados
titleSuffix: Configuration Manager
description: Conozca los procedimientos recomendados de seguridad para administrar perfiles de certificado de usuarios y dispositivos en Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4b7db4537965b17cd56cc4d996eec576c2b18965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706053"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Seguridad y privacidad de perfiles de certificados en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Recomendaciones de seguridad para perfiles de certificado  
 Siga las siguientes recomendaciones de seguridad al administrar perfiles de certificado para usuarios y dispositivos.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Identifique y siga todas las recomendaciones de seguridad para el Servicio de inscripción de dispositivos de red, como la configuración del sitio web de Servicio de inscripción de dispositivos de red en Internet Information Services (IIS) para que requiera SSL y omita certificados de cliente.|Consulte [Network Device Enrollment Service Guidance (Guía del Servicio de inscripción de dispositivos de red)](https://go.microsoft.com/fwlink/p/?LinkId=309016) en la biblioteca de Servicios de certificados de Active Directory de TechNet.|  
|Al configurar los perfiles de certificado SCEP, elija las opciones más seguras que puedan admitir los dispositivos y la infraestructura.|Identifique, implemente y siga las recomendaciones de seguridad indicadas para los dispositivos y la infraestructura.|  
|Especifique manualmente la afinidad de dispositivo del usuario en lugar de permitir a los usuarios identificar su dispositivo primario. Además, no habilite la configuración basada en el uso.|Si hace clic en **Permitir la inscripción de certificados solo en el dispositivo primario de los usuarios** en un perfil de certificado de SCEP, no considere la información recopilada de los usuarios ni del dispositivo como relevante. Si implementa perfiles de certificado de SCEP con esta configuración y un usuario administrativo confiable no especifica la afinidad de dispositivo de usuario, es posible que se conceda a usuarios no autorizados certificados de autenticación y privilegios elevados.<br /><br /> **Nota:** Si habilita la configuración basada en el uso, esta información se recopila mediante mensajes de estado que no están protegidos por Configuration Manager. Para mitigar esta amenaza, utilice la firma SMB o IPsec entre equipos cliente y el punto de administración.|  
|No agregue permisos de lectura ni de inscripción para los usuarios a las plantillas de certificado ni configure el punto de Registro de certificado para omitir la comprobación de la plantilla de certificado.|Aunque Configuration Manager admita la comprobación adicional si agrega los permisos de seguridad de Leer e Inscribir para los usuarios, y usted pueda configurar el punto de registro de certificados para que omita esta comprobación si no es posible la autenticación, no se recomienda ninguna de estas configuraciones. Para más información, consulte [Planificación de permisos de plantilla de certificado para perfiles de certificado en System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Información de privacidad de los perfiles de certificado  
 Puede utilizar perfiles de certificado para implementar certificados de cliente y de entidad de certificación (CA) raíz, y evaluar si dichos dispositivos son compatibles tras la aplicación de los perfiles. El punto de administración envía información de cumplimiento al servidor de sitio y Configuration Manager almacena la información en la base de datos del sitio. La información de cumplimiento incluye propiedades del certificado como el nombre del firmante y la huella digital. La información se cifra cuando los dispositivos la envían al punto de administración, pero no se almacena en formato cifrado en la base de datos del sitio. La base de datos guarda la información hasta que la tarea de mantenimiento **Eliminar datos antiguos de administración de configuración** del sitio la elimina después de un intervalo predeterminado de 90 días. Puede configurar el intervalo de eliminación. La información de compatibilidad no se envía a Microsoft.  

 Los perfiles de certificado usan la información que recopila Configuration Manager mediante la detección. Para más información sobre la información de privacidad de la detección, consulte la sección **Información de privacidad de la detección** del tema [Seguridad y privacidad en System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Los certificados emitidos para usuarios o dispositivos pueden permitir el acceso a información confidencial.  

 De manera predeterminada, los dispositivos no evalúan perfiles de certificado. Además, debe configurar los perfiles de certificado y luego implementarlos en usuarios o dispositivos.  

 Antes de configurar los perfiles de certificado, tenga en cuenta sus requisitos de privacidad.  
