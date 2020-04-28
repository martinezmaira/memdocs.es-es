---
title: Uso de Intune en entornos sin Google Mobile Services
titleSuffix: Microsoft Intune
description: Aprenda a usar Intune en entornos sin Google Mobile Services.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5aa91a84b2fe5d8870afc93022ab5a468b30e0db
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074799"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Uso de Intune en entornos sin Google Mobile Services

Microsoft Intune usa Google Mobile Services (GMS) para comunicarse con el Portal de empresa de Microsoft Intune al administrar dispositivos Android. En algunos casos, los dispositivos pueden no tener acceso a GMS de forma temporal o permanente. Por ejemplo, es posible que un dispositivo se distribuya sin GMS o que el dispositivo se conecte a una red cerrada en la que no está disponible GMS. En este documento se resumen las diferencias y limitaciones que puede observar al instalar y usar Intune para administrar dispositivos Android sin GMS.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Instalación de la aplicación Portal de empresa de Intune sin acceso a Google Play Store 

### <a name="for-users-outside-of-mainland-china"></a>Para usuarios fuera de la China continental 

Si Google Play no está disponible, los dispositivos Android pueden descargar el  [Portal de empresa de Microsoft Intune para Android](https://www.microsoft.com/en-us/download/details.aspx?id=49140) y transferir localmente la aplicación. Cuando se instala este modo, la aplicación no recibe las actualizaciones o correcciones automáticamente. Debe asegurarse de actualizar y aplicar revisiones periódicamente a la aplicación de forma manual. 

### <a name="for-users-in-mainland-china"></a>Para usuarios de la China continental 

Como Google Play Store no está disponible actualmente en la China continental, los dispositivos Android deben obtener aplicaciones de mercados de aplicaciones chinos. Para obtener más información, consulte [Instalación de la aplicación Portal de empresa en la China continental](../user-help/install-company-portal-android-china.md).

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Limitaciones de administración para los administradores de dispositivos de Intune cuando GMS no está disponible 

### <a name="unavailable-intune-features"></a>Características no disponibles de Intune

Algunas características de Intune dependen de los componentes de GMS, como Google Play Store o Google Play Services. Dado que estos componentes no están disponibles en entornos sin GMS, puede que las siguientes características de la consola del Administrador del servicio Intune no estén disponibles.  

| Escenario  | Funciones  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Directivas de cumplimiento de dispositivos  | Al crear o editar directivas de cumplimiento para el administrador de dispositivos Android, ninguna de las opciones que se muestran en **Google Play Protect** está disponible.  |
| Directivas de protección de aplicaciones (inicio condicional)  | Las condiciones de dispositivo **Atestación de dispositivo SafetyNet** y **Requerir examen de amenazas en las aplicaciones** no se pueden usar para el inicio condicional.  |
| Aplicaciones cliente  | Las aplicaciones de tipo **Android** no están disponibles. Use **Aplicación de línea de negocio** en su lugar para implementar y administrar aplicaciones.  |
| Mobile Threat Defense  | Trabaje con su proveedor de MTD para saber si su solución está integrada con Intune, si está disponible en la región que le interesa y si se basa en GMS.  |

### <a name="some-tasks-may-be-delayed"></a>Posible retraso de algunas tareas 

En entornos en los que está disponible GMS, Intune se basa en las notificaciones push para acelerar la finalización de las tareas. Por ejemplo, si intenta borrar el dispositivo de forma remota, las notificaciones suelen llegar al dispositivo en segundos. En condiciones en las que no GMS no está disponible, las notificaciones push también pueden no estar disponibles. Por lo tanto, Intune debe esperar al siguiente momento de sincronización de dispositivos para completar las tareas.  

Los dispositivos Android inscritos emiten notificaciones a Intune cada 8 horas. Por ejemplo, si un dispositivo notifica a Intune a la 1 p.m. y las tareas remotas se emiten a las 1:05 p.m., Intune contactará con el dispositivo a las 9 p.m. para completar las tareas. 

Las siguientes tareas pueden tardar hasta 8 horas en completarse: 

**Consola de Intune**:
- Eliminación completa
- Borrado selectivo
- Implementaciones de la aplicación nuevas o actualizadas
- Bloqueo remoto
- Restablecimiento de la contraseña

**Aplicación Portal de empresa de Intune para Android**:
- Eliminación remota de dispositivos
- Restablecimiento del dispositivo
- Instalación de aplicaciones de línea de negocio disponibles

**Sitio web del Portal de empresa de Intune**:
- Eliminación de dispositivos (local y remota)
- Restablecimiento del dispositivo
- Restablecimiento del código de acceso del dispositivo

Si el dispositivo se ha inscrito recientemente, la comprobación de cumplimiento, no cumplimiento y configuración se ejecuta con más frecuencia. Para obtener más información acerca de las sincronizaciones de dispositivo, consulte [Preguntas comunes, problemas y su solución con perfiles y directivas de dispositivos en Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Pasos siguientes

- [Asignación de aplicaciones a grupos con Microsoft Intune](../apps/apps-deploy.md)
