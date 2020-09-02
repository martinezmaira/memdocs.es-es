---
title: Solucionar problemas de Exchange Connector
titleSuffix: Microsoft Intune
description: Solucione los problemas relacionados con Intune On-Premises Exchange Connector.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57a7b232b7391d6b8716d4c2a56d69b44f6c07ee
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914759"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Solución de problemas de Intune Exchange Connector

En este artículo se describe cómo solucionar los problemas relacionados con Intune Exchange Connector.

> [!IMPORTANT]
>
> A partir de julio de 2020, el soporte técnico para Exchange Connector queda en desuso y se reemplaza por la [autenticación moderna híbrida (HMA)](/office365/enterprise/hybrid-modern-auth-overview) de Exchange. Además, se quita la capacidad de agregar Exchange Connector a Intune.
>
> Los clientes que previamente configuraron Exchange Connector y lo usan tienen soporte técnico continuado para el conector.


## <a name="before-you-start"></a>Antes de empezar

Antes de empezar a solucionar problemas de un Conector de Exchange en Intune, recopile información básica para trabajar sobre una base sólida. Este enfoque puede ayudarle a comprender mejor la naturaleza del problema y resolverlo más rápidamente.

- Compruebe que el proceso cumple los requisitos de instalación. Vea [Configuración de Intune Exchange Connector local](exchange-connector-install.md).
- Compruebe que la cuenta tenga permisos de administrador de Exchange y de Intune.
- Tenga en cuenta el texto del mensaje de error completo y exacto, los detalles y el lugar en el que se muestra el mensaje.
- Determine cuándo comenzó el problema: 
  - ¿Está configurando el conector por primera vez? 
  - ¿El conector funcionaba correctamente y, después, se produjo un error?
  - Si funcionaba, ¿qué cambios se produjeron en el entorno de Intune, en el entorno de Exchange o en el equipo que ejecuta el software del conector?
- ¿Qué es la entidad de MDM?
- ¿Qué versión de Exchange usa?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Uso de PowerShell para obtener más datos acerca de problemas de Exchange Connector

- Para obtener una lista de todos los dispositivos móviles para un buzón de correo, use `Get-ActiveSyncDeviceStatistics -mailbox mbx`.
- Para obtener una lista de todas las direcciones de SMTP para un buzón de correo, use `Get-Mailbox -Identity user | select emailaddresses | fl`.
- Para información detallada sobre el estado del acceso de un dispositivo, use `Get-CASMailbox <upn> | fl`.

## <a name="review-the-connector-configuration"></a>Revisión de la configuración del conector

Revise los [requisitos del conector de Exchange local](exchange-connector-install.md#intune-exchange-connector-requirements) para asegurarse de que el entorno y el conector están configurados correctamente. 

### <a name="general-considerations-for-the-connector"></a>Consideraciones generales sobre el conector

- Asegúrese de que el firewall y los servidores proxy permiten la comunicación entre el servidor que hospeda Intune Exchange Connector y el servicio Intune.

- El equipo que hospeda Intune Exchange Connector y el servidor de acceso de cliente (CAS) de Exchange deben estar unidos a un dominio y en la misma LAN. Asegúrese de que se han agregado los permisos necesarios para la cuenta que usa Intune Exchange Connector.

- La cuenta de notificación se usa para recuperar la configuración de *detección automática*. Para obtener más información sobre la detección automática en Exchange, vea [Servicio de detección automática en Exchange Server](/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Intune Exchange Connector envía una solicitud a la dirección URL de EWS mediante el uso de las credenciales de la cuenta de notificación para enviar mensajes de correo electrónico de notificación junto con el *vínculo para inscribirse en Intune*. El uso del *vínculo para inscribirse* es un requisito para dispositivos Android que no son Knox. De lo contrario, estos dispositivos se bloquearán por el acceso condicional.

### <a name="common-issues-for-connector-configurations"></a>Problemas comunes de las configuraciones de conectores

- **Permisos de cuenta**: En el cuadro de diálogo de Microsoft Intune Exchange Connector, asegúrese de que ha especificado una cuenta de usuario que tiene los permisos adecuados para ejecutar los [cmdlets de Windows PowerShell Exchange requeridos](exchange-connector-install.md#exchange-cmdlet-requirements).
- **Mensajes de correo electrónico de notificación**: Habilite las notificaciones y especifique una cuenta de notificación.
- **Sincronización de servidor de acceso de cliente**: Al configurar Exchange Connector, especifique un CAS que tenga la menor latencia de red posible al servidor que hospeda Exchange Connector. La latencia de comunicación entre las entidades de certificación y Exchange Connector puede provocar retrasos de detección del dispositivo, especialmente cuando se utiliza Exchange Online dedicado.
- **Programación de sincronización**: El acceso de un usuario con un dispositivo recién inscrito podría retrasarse hasta que el conector de Exchange se sincronice con el CAS de Exchange. Una sincronización completa se lleva a cabo una vez al día y una sincronización diferencial (rápida) se realiza varias veces al día. También puede [forzar manualmente una sincronización rápida o una sincronización completa](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync) para minimizar los retrasos.

## <a name="next-steps"></a>Pasos siguientes
Los siguientes artículos pueden ayudarle a resolver problemas comunes y errores específicos:

- [Resolución de problemas comunes de Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).
- [Resolución de errores comunes de Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Busque asistencia del soporte técnico o de la comunidad de Intune:

- Vea [Obtener soporte técnico](../fundamentals/get-support.md) para usar la consola de Intune con el fin de ayudarle a solucionar el problema o abrir un caso de soporte técnico con Microsoft. 
- Publique su problema en los [foros de Microsoft Intune](/answers/products/mem).  
