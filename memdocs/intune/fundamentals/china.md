---
title: Intune ofrecido por 21Vianet en China
titleSuffix: ''
description: Intune ofrecido por 21Vianet en China
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: f82664cbc9f6970d494945cfdf6fc72e8d95ae8b
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022354"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune ofrecido por 21Vianet en China  

Intune ofrecido por 21Vianet está diseñado para satisfacer las necesidades de servicios en la nube seguros, confiables y escalables en China. Intune como servicio se basa en Microsoft Azure. Microsoft Azure ofrecido por 21Vianet es una instancia físicamente separada los servicios en la nube ubicados en China. Se ofrece y se realiza de forma independiente con 21Vianet. Este servicio se basa en la tecnología que Microsoft ha autorizado a 21Vianet.

Microsoft no ofrece con el propio servicio. 21Vianet ofrece, proporciona y administra la entrega del servicio. 21Vianet es un proveedor de servicios de centro de datos de Internet en China. Proporciona servicios de hospedaje, servicios de red administrados e infraestructura de informática en la nube. Gracias a las tecnologías de licencias de Microsoft, 21Vianet funciona en los centros de datos locales para ofrecer la posibilidad de usar el servicio de Intune al tiempo que mantiene los datos en China. 21Vianet también proporciona servicios de suscripción, facturación y soporte técnico.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>Diferencias de características en Intune ofrecido por 21Vianet

Dado que los servicios de China operan en un partner de dentro de China, hay algunas diferencias de características con Intune. 

- Intune ofrecido por 21Vianet solo admite implementaciones independientes. La compatibilidad de la administración conjunta con System Center Configuration Manager está actualmente en desarrollo.
- No se admiten migraciones de nubes públicas a nubes independientes. Los clientes interesados en pasar a Intune ofrecido por 21Vianet deben migrar manualmente.
- Actualmente no se admite la característica de asociación de inquilinos (la sincronización de dispositivos a Intune sin inscripción para admitir escenarios de la consola en la nube).
- Intune ofrecido por 21Vianet no admite el agente de Intune y, por tanto, no admite la administración de equipos heredada.
- Se admite la administración de Windows 10 mediante el canal de MDM moderno.
- Intune ofrecido por 21Vianet no admite el conector de Exchange local.
- Las características de Windows Autopilot y de la Tienda para empresas no están disponibles actualmente.
- Dado que Google Mobile Services no está disponible en China, los clientes de Intune ofrecidos por 21Vianet no pueden usar características que requieran los servicios de Google para móviles. Estas características incluyen:
  - Funcionalidades de Google Play Protect como certificación de dispositivo SafetyNet
  - Administración de aplicaciones desde Google Play Store
  - Funcionalidades de Android Enterprise Para más información, consulte la [documentación de Google](https://support.google.com/work/android/answer/6270910?hl=en).
- La aplicación Portal de empresa de Intune para Android utiliza los servicios de Google para móviles para comunicarse con el servicio Microsoft Intune. Como los servicios de Google Play no están disponible en China, algunas tareas pueden tardar hasta ocho horas en completarse. Para más información, consulte este [artículo](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable). 
- Para seguir las regulaciones locales y proporcionar una funcionalidad mejorada, la experiencia del cliente de Intune (aplicación Portal de empresa) puede diferir en China.
- Las barreras no están disponibles.
- La disponibilidad de administración de aplicaciones móviles (MAM) depende de las aplicaciones que están disponibles en la República Popular China.

## <a name="you-control-customer-data"></a>Control de los datos de los clientes

En Microsoft Azure, Intune, Office 365 y Power BI ofrecido por 21Vianet, usted tiene el control total de los datos:
- Sabe dónde se encuentran los datos del cliente.
- Puede controlar el acceso a los datos del cliente.
- Puede controlar los datos de los clientes si deja el servicio.
- Tiene opciones para controlar la seguridad de los datos de los clientes.

Con Microsoft Azure, Intune, Office 365 y Power BI ofrecido por 21Vianet, usted es el propietario de los datos:
- 21Vianet no utiliza los datos de clientes para publicidad.
- Usted controla quién tiene acceso a los datos del cliente.
- Usamos el aislamiento lógico para separar los datos de cada cliente.
- Proporcionamos directivas de uso de datos sencillas y transparentes y obtenemos auditorías independientes.
- Nuestros subcontratistas están bajo contrato para cumplir con nuestros requisitos de privacidad.

## <a name="data-subject-requests"></a>Solicitudes de los titulares de los datos

El rol Administrador de inquilinos para Intune ofrecido por 21Vianet puede solicitar datos para los titulares de las siguientes maneras:

- Mediante el centro de administración de Azure Active Directory, un administrador de inquilinos puede eliminar de forma permanente un titular de los datos de Azure Active Directory y servicios relacionados. Para más información, consulte la sección Paso 5: Eliminar de [Solicitudes de titulares de los datos de Azure para el RGPD y la CCPA](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- Los administradores de inquilinos pueden exportar los registros generados por el sistema para los servicios de Microsoft ofrecidos por 21Vianet mediante la exportación del registro de datos. Para más información, consulte la sección Paso 6: Exportar de [Solicitudes de titulares de los datos de Azure para el RGPD y la CCPA](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export).

## <a name="next-steps"></a>Pasos siguientes

[Más información sobre los dispositivos compatibles con Intune](supported-devices-browsers.md).