---
title: Consentimiento de cliente de Windows AutoPilot
description: Obtenga información sobre cómo un asociado de proveedor de servicios en la nube (CSP) o un OEM puede obtener autorización del cliente para registrar dispositivos Windows AutoPilot en el nombre del cliente.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
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
ms.openlocfilehash: 16342550a30271afe20a85fb6cfabf1c0ad429da
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993809"
---
# <a name="windows-autopilot-customer-consent"></a>Consentimiento de cliente de Windows AutoPilot

**Se aplica a: Windows 10**

En este artículo se describe cómo un asociado de proveedor de servicios en la nube (CSP) (factura directa, proveedor indirecto o revendedor indirecto) o un OEM puede obtener autorización del cliente para registrar dispositivos Windows AutoPilot en el nombre del cliente.

## <a name="csp-authorization"></a>Autorización de CSP

Los asociados de CSP pueden obtener autorización del cliente para registrar dispositivos Windows AutoPilot en el nombre del cliente según las restricciones siguientes:

<table>
<tr><td>CSP directo<td>Obtiene la autorización directa del cliente para registrar dispositivos.
<tr><td>Proveedor CSP indirecto<td>Obtiene el permiso implícito para registrar los dispositivos a través de la relación que tiene su asociado de revendedor de CSP con el cliente.  Los proveedores de CSP indirectos registran dispositivos a través del centro de Partners de Microsoft.
<tr><td>Revendedor de CSP indirecto<td>Obtiene la autorización directa del cliente para registrar dispositivos.  Al mismo tiempo, su asociado de proveedor CSP indirecto también obtiene la autorización, lo que significa que el proveedor indirecto o el revendedor indirecto pueden registrar los dispositivos del cliente.  Sin embargo, el revendedor de CSP indirecto debe registrar los dispositivos a través de la interfaz de usuario de MPC (cargar manualmente el archivo CSV), mientras que el proveedor de CSP indirecto tiene la opción de registrar dispositivos mediante las API de MPC.
</table>

### <a name="steps"></a>Pasos

Para que un CSP registre dispositivos Windows AutoPilot en nombre de un cliente, el cliente primero debe conceder el permiso de asociado de CSP mediante el siguiente proceso:

1. El CSP envía un vínculo a la solicitud de autorización/consentimiento del cliente para registrar o administrar dispositivos en su nombre.  Para ello:
    - Registro de CSP en el centro de Partners de Microsoft
    - Haga clic en **Panel** en el menú superior.
    - Haga clic en **cliente** en el menú del lado
    - Haga clic en el vínculo **solicitar una relación de reseller** : ![ solicitar una relación de revendedor.](images/csp1.png)
    - Active la casilla que indica si desea o no derechos de administrador delegado: ![ derechos delegados](images/csp2.png)
    - Nota: en función de su asociado, pueden solicitar permisos de administrador delegado (DAP) al solicitar este consentimiento.  Si es posible, debe pedirles que usen el proceso sin uso de DAP más reciente (que se muestra en este documento). Si no es así, puede quitar fácilmente su estado de DAP en el centro de administración de Microsoft o en el portal de administración de Microsoft 365:  https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    - Envíe la plantilla anterior al cliente por correo electrónico.
2. Cliente con privilegios de administrador global en el centro de administración de Microsoft hace clic en el vínculo en el cuerpo del mensaje de correo electrónico una vez que lo reciba del CSP, que los lleva directamente a la siguiente página del centro de administración de Microsoft 365:

    ![Administrador global](images/csp3a.png)

    La imagen anterior es lo que el cliente verá si solicitó derechos de administrador delegado (DAP). Tenga en cuenta que la página indica qué roles de administración se están solicitando.  Si el cliente no solicitó derechos de administrador delegado, verán la siguiente página:

    ![Administrador global](images/csp3b.png)   

    > [!NOTE]
    > Un usuario sin privilegios de administrador global que haga clic en el vínculo verá un mensaje similar al siguiente:

    ![No administrador global](images/csp4.png)

3. El cliente selecciona la casilla **sí** y, después, el botón **Aceptar** . La autorización se produce de forma instantánea.
4. El CSP sabrá que se ha completado esta solicitud de consentimiento o autorización porque el cliente se mostrará en la cuenta MPC del CSP en la lista de **clientes** , por ejemplo:

![Clientes](images/csp5.png)

## <a name="oem-authorization"></a>Autorización OEM

Cada OEM tiene un vínculo único para proporcionar a sus clientes respectivos, que el OEM puede solicitar a Microsoft a través de msoemops@microsoft.com .

1. Los correos electrónicos de OEM se vinculan a su cliente.
2. Cliente con privilegios de administrador global en Microsoft Store para empresas (MSfB) haga clic en el vínculo después de recibirlo del OEM, que lo lleva directamente a la siguiente página de MSfB:

    ![Administrador global](images/csp6.png)

    > [!NOTE]
    > Un usuario sin privilegios de administrador global que haga clic en el vínculo verá un mensaje similar al siguiente:

    ![No administrador global](images/csp7.png)
3. El cliente selecciona la casilla **sí** , seguida del botón **Aceptar** y está listo.  La autorización se produce de forma instantánea.

    > [!NOTE]
    > Una vez completado este proceso, actualmente no es posible que un administrador Quite un OEM. Para quitar un OEM o revocar sus permisos, envíe una solicitud a msoemops@microsoft.com

4. El OEM puede usar la API de datos de envío de dispositivo de validación para comprobar que se ha completado el consentimiento.  Esta API se describe en la versión más reciente de las notas del producto de la API, p. 14ff [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) . **Nota**: este vínculo solo es accesible para asociados de Microsoft Device. Como se describe en estas notas del producto, se recomienda que los asociados OEM ejecuten la comprobación de la API para confirmar que han recibido el consentimiento del cliente antes de intentar registrar los dispositivos y, por lo tanto, evitar errores en el proceso de registro.

    > [!NOTE]
    > Durante el proceso de registro de autorización OEM, no se conceden permisos de administrador delegado al OEM.

## <a name="summary"></a>Resumen

En esta fase del proceso, Microsoft ya no participa; el intercambio de consentimiento se produce directamente entre el OEM y el cliente.  Y todo se produce de forma instantánea, tan pronto como se hace clic en los botones.
