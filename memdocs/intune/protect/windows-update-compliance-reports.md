---
title: Uso de informes de Update Compliance para actualizaciones de Windows en Microsoft Intune
titleSuffix: Microsoft Intune
description: Use Update Compliance de OMS para ver los datos del informe de Windows Update que implemente con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 297707da0afb03650eaab91b26abad9947c6a951
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286159"
---
# <a name="intune-compliance-reports-for-updates"></a>Informes de cumplimiento de Intune para las actualizaciones

Al usar Intune para implementar la actualización de Windows en dispositivos Windows 10, vea detalles sobre el cumplimiento de las actualizaciones mediante Intune o una solución gratuita llamada *Update Compliance*. Update Compliance forma parte de Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Uso de Intune

Para revisar un informe de directivas sobre el estado de implementación para los anillos de actualizaciones de Windows 10 que ha configurado, haga lo siguiente:

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Información general** > **Estado de actualización de software**. Puede ver información general sobre el estado de los círculos de actualizaciones que tenga asignados.

3. Para ver detalles adicionales, seleccione **Monitor**. Luego, en **Actualizaciones de software**, seleccione **Estado de implementación por anillo de actualización** y elija el anillo de implementación que se revisará.

   En la sección **Supervisar**, elija uno de los siguientes informes para ver información más detallada sobre el círculo de actualizaciones:

   - **Estado de dispositivo**: muestra el estado de configuración del dispositivo. Para más información, consulte [Actualizar deviceConfigurationDeviceStatus]( /graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Estado del usuario**: muestra el nombre del usuario, el estado y la fecha de último informe. Para más información, consulte [Enumerar deviceConfigurationUserStatuses](/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Estado de actualización del usuario final**: muestra el estado de actualización del dispositivo Windows. Para más información, vea [windowsUpdateState](/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Uso de Update Compliance

Puede supervisar las implementaciones de actualización de Windows 10 mediante [Update Compliance](/windows/deployment/update/update-compliance-monitor). Update Compliance se ofrece a través de Azure Portal y está disponible de forma gratuita para los dispositivos que cumplen los [requisitos previos](/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites).  

Cuando se utiliza esta solución, se implementa un identificador comercial en cualquiera de sus dispositivos Windows 10 administrados con Intune para el que quiera que se informe del cumplimiento de las actualizaciones.  

En Intune, puede usar la configuración OMA-URI de una directiva personalizada para configurar el identificador comercial. Consulte [Usar una configuración personalizada para dispositivos Windows 10 en Intune](../configuration/custom-settings-windows-10.md).

Ruta OMA-URI (distingue mayúsculas de minúsculas) para configurar el identificador comercial: *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*

Por ejemplo, puede usar los siguientes valores en **Agregar o editar configuración OMA-URI**:

- **Nombre de la configuración**: identificador comercial de Windows Analytics
- **Descripción de la configuración**: configuración del identificador comercial para soluciones de Windows Analytics
- **OMA-URI** (distingue mayúsculas de minúsculas): *./Vendor/MSFT/DMClient/Provider/ProviderID/CommercialID*
- **Tipo de datos**: String
- **Valor**: \<Use the GUID shown on the Windows Telemetry tab in your OMS workspace>

> [!NOTE]
> Para obtener más información sobre MS DM Server, vea [DMClient configuration service provider (CSP)]( /windows/client-management/mdm/dmclient-csp) (Proveedor de servicios de configuración (CSP) de DMClient).

## <a name="next-steps"></a>Pasos siguientes

[Administrar las actualizaciones de software en Intune](windows-update-for-business-configure.md)
