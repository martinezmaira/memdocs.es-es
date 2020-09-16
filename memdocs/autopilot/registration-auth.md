---
title: Consentimiento de cliente de Windows AutoPilot
description: Obtenga información sobre cómo un asociado de proveedor de servicios en la nube (CSP) o un OEM puede obtener autorización del cliente para registrar dispositivos Windows AutoPilot en el nombre del cliente.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: db2dc86b4f7cb514f3ceca4d37bf387db31c13f4
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568557"
---
# <a name="windows-autopilot-customer-consent"></a>Consentimiento de cliente de Windows AutoPilot

**Se aplica a: Windows 10**

En este artículo se describe cómo un asociado de proveedor de servicios en la nube (CSP) (factura directa, proveedor indirecto o revendedor indirecto) o un OEM puede obtener autorización del cliente para registrar dispositivos Windows AutoPilot en el nombre del cliente.

## <a name="csp-authorization"></a>Autorización de CSP

Los asociados de CSP pueden obtener autorización del cliente para registrar dispositivos Windows AutoPilot en el nombre del cliente según las restricciones siguientes:

<table>
<tr><td>CSP directo<td>Obtiene la autorización directa del cliente para registrar dispositivos.
<tr><td>Proveedor CSP indirecto<td>Obtiene el permiso implícito para registrar los dispositivos a través de la relación que tiene su asociado de revendedor de CSP con el cliente. Los proveedores de CSP indirectos registran dispositivos a través del centro de Partners de Microsoft.
<tr><td>Revendedor de CSP indirecto<td>Obtiene la autorización directa del cliente para registrar dispositivos. Al mismo tiempo, su asociado de proveedor CSP indirecto también obtiene la autorización, lo que significa que el proveedor indirecto o el revendedor indirecto pueden registrar los dispositivos del cliente. Sin embargo, el revendedor de CSP indirecto debe registrar los dispositivos a través de la interfaz de usuario de MPC (carga manual del archivo CSV). El proveedor CSP indirecto puede registrar dispositivos mediante las API de MPC.
</table>

### <a name="steps"></a>Pasos

Para que un CSP registre dispositivos Windows AutoPilot para un cliente, el cliente primero debe conceder el permiso de asociado de CSP mediante el siguiente proceso:

1. El CSP envía un vínculo a la solicitud de autorización/consentimiento del cliente para registrar o administrar dispositivos en su nombre. Para ello:
    1. CSP inicia sesión en el centro de Partners de Microsoft.
    2. Haga clic en **Panel** en el menú superior.
    3. En el menú del lado, haga clic en **cliente** .
    4. Haga clic en el vínculo **solicitar una relación de reseller** :

        ![Solicitar una relación de revendedor](images/csp1.png)
 
    5. Active la casilla que indica si desea derechos de administrador delegado:
 
        ![Derechos delegados](images/csp2.png)

        > [!NOTE]
        > En función de su asociado, pueden solicitar permisos de administrador delegado (DAP) al solicitar este consentimiento. Si es posible, es mejor usar el proceso sin uso de DAP más reciente (que se muestra en este documento). Si no es así, puede quitar fácilmente su estado de DAP en el centro de administración de Microsoft o en el portal de administración de Microsoft 365: https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    6. Envíe la plantilla anterior al cliente por correo electrónico.

2. Cliente con privilegios de administrador global en el centro de administración de Microsoft hace clic en el vínculo de correo electrónico. El vínculo los lleva a la siguiente página del centro de administración de Microsoft 365:

    ![Captura de aceptación del contrato y autorización de la página del asociado: derechos de administrador delegado](images/csp3a.png)

    La imagen anterior es lo que el cliente verá si solicitó derechos de administrador delegado (DAP). En la página se indica qué roles de administración se están solicitando. Si el cliente no solicitó derechos de administración delegados, verá la siguiente página:

    ![Captura de la página aceptar contrato y autorizar asociado](images/csp3b.png) 

    > [!NOTE]
    > Un usuario sin privilegios de administrador global que haga clic en el vínculo verá un mensaje similar al siguiente:

    ![Captura página de permisos](images/csp4.png)

3. El cliente selecciona la casilla **sí** y, después, el botón **Aceptar** . La autorización se produce de forma instantánea.
4. Para comprobar que la solicitud de autorización se ha completado, el CSP puede comprobar la lista de **clientes** en su cuenta de MPC. Si el cliente está en la lista, la solicitud se ha completado. Por ejemplo:

    ![Clientes](images/csp5.png)

## <a name="oem-authorization"></a>Autorización OEM

Cada OEM tiene un vínculo único para proporcionar a sus clientes respectivos, que el OEM puede solicitar a Microsoft a través de msoemops@microsoft.com .

1. Los correos electrónicos de OEM se vinculan a su cliente.
2. Cliente con privilegios de administrador global de Microsoft Store para empresas (MSfB) haga clic en el vínculo del correo electrónico, que lo lleva directamente a la siguiente página de MSfB:

    ![Captura página de aceptación de invitación de socio comercial](images/csp6.png)

    > [!NOTE]
    > Un usuario sin privilegios de administrador global que haga clic en el vínculo verá un mensaje similar al siguiente:

    ![Captura de MSfB página necesaria de permiso](images/csp7.png)

3. El cliente selecciona la casilla **sí** , seguida del botón **Aceptar** y está listo. La autorización se produce de forma instantánea.

    > [!NOTE]
    > Una vez completado este proceso, actualmente no es posible que un administrador Quite un OEM. Para quitar un OEM o revocar sus permisos, envíe una solicitud a msoemops@microsoft.com

4. El OEM puede usar la API de datos de envío de dispositivo de validación para comprobar que se ha completado el consentimiento. Esta API se describe en la versión más reciente de las notas del producto de la API, p. 14ff [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) . **Nota**: este vínculo solo es accesible para asociados de Microsoft Device. Como se describe en este artículo, se recomienda que los asociados de OEM ejecuten la comprobación de la API para confirmar que han recibido el consentimiento del cliente antes de intentar registrar los dispositivos. Esta comprobación puede ayudar a evitar errores en el proceso de registro.

    > [!NOTE]
    > Durante el proceso de registro de autorización OEM, no se conceden permisos de administrador delegado al OEM.

## <a name="summary"></a>Resumen

En esta fase del proceso, Microsoft ya no participa; el intercambio de consentimiento se produce directamente entre el OEM y el cliente. Y todo se produce de forma instantánea, tan pronto como se hace clic en los botones.
