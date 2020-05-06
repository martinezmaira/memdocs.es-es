---
title: Implementación de perfiles de acceso a los recursos
titleSuffix: Configuration Manager
description: Aprenda a implementar perfiles de certificado, Wi-Fi y VPN en Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709463"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Implementación de perfiles de acceso a recursos en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de crear uno de los perfiles de acceso de recursos siguientes, impleméntelo en una o varias recopilaciones:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certificado](create-certificate-profiles.md)

Cuando se implementan estos perfiles, se especifica la colección de destino y la frecuencia con la que el cliente evalúa el cumplimiento del perfil.  

## <a name="deploy-a-profile"></a>Implementación de un perfil

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento**, **Acceso a los recursos de la empresa** y, a continuación, elija el nodo de perfil adecuado. Por ejemplo, **Perfiles de Wi-Fi**.

1. En la lista de perfiles, seleccione el perfil que quiere implementar. Luego, en la pestaña **Inicio** de la cinta, en el grupo **Implementación**, seleccione **Implementar**.  

1. En la ventana de implementación de perfil, especifique la información siguiente:  

    - **Colección**: seleccione la colección en la que quiere implementar el perfil.

    - **Generar una alerta**: habilite esta opción para configurar una alerta. El sitio genera esta alerta si el cumplimiento del perfil es menor que el porcentaje especificado en la fecha y hora especificadas. También puede seleccionar si quiere que se envíe una alerta a System Center Operations Manager.

    - **Retraso aleatorio (horas)** : en perfiles de certificado que contengan la configuración Protocolo de inscripción de certificados simple (SCEP), especifique una ventana de retraso para evitar un procesamiento excesivo en el Servicio de inscripción de dispositivos de red (NDES). El valor predeterminado es `64` horas.  

    - **Especifique la programación de evaluación de compatibilidad de este perfil de...:** : especifique la frecuencia con la que el cliente evalúa la compatibilidad de este perfil. Seleccione una **Programación sencilla** o configure una **Programación personalizada**. De manera predeterminada, la programación sencilla es cada `12` horas.

1. Seleccione **Aceptar** para cerrar la ventana y crear la implementación.

## <a name="delete-a-deployment"></a>Eliminación de una implementación

Si desea eliminar una implementación, selecciónela en la lista. En el panel de detalles, cambie a la pestaña **Implementaciones**. Seleccione la implementación y, después, en la pestaña **Implementación** de la cinta, seleccione **Eliminar**.

> [!IMPORTANT]
> Cuando se quita una implementación de perfil de VPN, Configuration Manager no quita el perfil de VPN de Windows. Si quiere quitar el perfil de dispositivos, hágalo de forma manual.

## <a name="next-steps"></a>Pasos siguientes

[Supervisión de perfiles de Wi-Fi y VPN](monitor-wifi-email-vpn-profiles.md)

[Supervisar perfiles de certificado](monitor-certificate-profiles.md)
