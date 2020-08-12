---
title: Directivas de configuración para aplicaciones administradas sin inscripción de dispositivos
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo configurar directivas para aplicaciones administradas sin inscripción de dispositivos.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 42547885c5f791749517415b325c8c785ec52c13
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051410"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>Agregar directivas de configuración para aplicaciones administradas sin inscripción de dispositivos

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Puede usar directivas de configuración de aplicaciones con aplicaciones administradas que admiten Intune App SDK incluso en los dispositivos que no están inscritos. 

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Elija **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Aplicaciones administradas**.
3. En la página **Aspectos básicos**, establezca los detalles siguientes:
    - **Nombre**: Nombre del perfil que aparecerá en Azure Portal.
    - **Descripción**: Descripción del perfil que aparecerá en Azure Portal.
    - **Tipo de inscripción del dispositivo**: está seleccionada la opción Aplicaciones administradas.
4. Elija **Seleccionar aplicaciones públicas** o **Seleccionar aplicaciones personalizadas** para seleccionar la aplicación que va a capturar. Seleccione la aplicación en la lista de aplicaciones que ha aprobado y sincronizado con Intune.
5. Haga clic en **Siguiente** para abrir la página **Configuración**.
6. En la **página Configuración** se ofrecen opciones que se muestran en función de la aplicación que se esté configurando:

    - **Opciones de configuración generales**: para cada opción de configuración que la aplicación admita, escriba los datos de **Nombre** y **Valor**. 
 
        Las aplicaciones habilitadas para Intune App SDK admiten configuraciones en pares de clave y valor. Para obtener más información sobre qué configuraciones de clave y valor se admiten, consulte la documentación de cada aplicación. Tenga en cuenta que puede usar tokens que se rellenarán de forma dinámica con datos generados por la aplicación. Para eliminar una opción de configuración general, elija el menú de puntos suspensivos ( **...** ) y seleccione **Eliminar**. Para más información, consulte [Valores de configuración para usar tokens](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens). 

    - **Valores de configuración de Outlook**: Outlook para iOS y Android ofrece a los administradores la posibilidad de personalizar la configuración predeterminada para varias opciones de configuración de la aplicación. Para más información, consulte [Outlook para iOS y Android: Escenarios generales de configuración de aplicaciones](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios).
   
    - **S/MIME**: extensiones seguras multipropósito al correo de Internet (S/MIME) es una especificación que permite a los usuarios enviar y recibir mensajes de correo electrónico firmados y cifrados digitalmente.
        - **Habilitar S/MIME**: especifique si los controles S/MIME se habilitan o no al redactar un correo electrónico. Valor predeterminado: **No configurado**.
        - **Permitir que el usuario cambie la configuración**: especifique si el usuario tiene permiso para cambiar la configuración. S/MIME debe estar habilitada. Valor predeterminado: **Sí**.
        
    Para más información sobre las opciones de las directivas de configuración de aplicaciones de Outlook, consulte [Implementación de las opciones de configuración de la aplicación de Outlook para iOS y Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

7. Haga clic en **Siguiente** para abrir la página **Asignaciones**.
8. Haga clic en **Seleccionar grupos para incluir**.
9. Seleccione un grupo en el panel **Seleccionar grupos para incluir** y haga clic en **Seleccionar**.
10. Haga clic en **Seleccionar grupos para excluir** para mostrar el panel relacionado.
11. Seleccione los grupos que quiera excluir y después haga clic en **Seleccionar**.

    >[!NOTE]
    >Al agregar un grupo, si ya se ha incluido otro a un tipo de asignación determinado, este se preselecciona y no se puede cambiar por otros tipos de asignación de inclusión. Por lo tanto, ese grupo que se ha usado no se puede usar como un grupo de exclusión.

12. Elija **Siguiente** para mostrar la página **Revisar y crear**.
13. Haga clic en **Crear** para agregar la Ddrectiva de configuración de aplicaciones a Intune.

## <a name="configuration-values-for-using-tokens"></a>Valores de configuración para usar tokens

Intune puede generar ciertos tokens y enviarlos a la aplicación administrada. Por ejemplo, si la configuración de la aplicación incluye una opción de correo electrónico, puede usar un token para agregar un correo electrónico dinámico. Escriba el nombre esperado por la aplicación en el campo **Nombre** y luego escriba `{{mail}}` en el campo **Valor**.

Intune admite los siguientes tipos de token en las opciones de configuración. No se admiten otros pares clave/valor personalizados.

- \{\{userprincipalname\}\}. Por ejemplo, John@contoso.com
- \{\{mail\}\}. Por ejemplo, John@contoso.com
- \{\{partialupn\}\}. Por ejemplo, John
- \{\{accountid\}\}. Por ejemplo, fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\}. Por ejemplo, 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\}. Por ejemplo, John Doe
- \{\{PrimarySMTPAddress\}\}. Por ejemplo, testuser@ad.domain.com

> [!Note]  
> Los caracteres \{\{ y \}\} solo se usan para los tipos de token y no deben usarse para otros fines.

## <a name="next-steps"></a>Pasos siguientes

Siga [asignando](apps-deploy.md) y [supervisando](apps-monitor.md) la aplicación como de costumbre.
