---
title: Solución de problemas de perfiles de correo electrónico en Microsoft Intune - Azure | Microsoft Docs
description: Consulte los problemas comunes con los perfiles de correo electrónico en Microsoft Intune y sus soluciones, incluidos los perfiles de correo electrónico duplicados y errores en dispositivos Samsung KNOX Standard con Android.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 717ad28625b5eac97c26bcd09a21ef34250a7d39
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565723"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Problemas comunes y resoluciones con perfiles de correo electrónico en Microsoft Intune

Revise algunos problemas comunes relacionados con los perfiles de correo electrónico y cómo se pueden solucionar.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Solicitud de escribir la contraseña en múltiples ocasiones

Es posible que se pida repetidas veces a los usuarios que escriban su contraseña en el perfil de correo electrónico. Si los certificados se usan para autenticar y autorizar al usuario, compruebe las asignaciones de todos los perfiles de certificado. Normalmente, estos perfiles de certificado se asignan a grupos de usuarios, no a grupos de dispositivos. Si uno de los certificados no está destinado a un usuario, Intune sigue intentando implementar el perfil de correo electrónico.

Si la cadena de perfiles de correo electrónico se asigna a grupos de usuarios, asegúrese de que los perfiles de certificado también se asignen a grupos de usuarios.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Errores y latencia en los perfiles implementados en grupos de dispositivos

Los perfiles de correo electrónico se asignan normalmente a grupos de usuarios. Puede haber algunos casos en los que se asignen a grupos de dispositivos.

- Por ejemplo, quiere implementar un perfil de correo electrónico basado en certificados solo en dispositivos Surface, no en otros de escritorio. En este escenario, los grupos de dispositivos pueden tener sentido. Sepa que es posible que estos dispositivos aparezcan como no compatibles, que devuelvan errores y que no se obtengan los perfiles de correo electrónico inmediatamente.

  En este ejemplo, se crea el perfil de correo electrónico y se asigna el perfil a grupos de dispositivos. El dispositivo se reinicia y hay un retraso antes de que un usuario inicie sesión. Durante este retraso, se implementa el perfil de certificado PKCS, que se asigna a los grupos de usuarios. Dado que todavía no hay ningún usuario, el perfil de certificado PKCS hace que el dispositivo no sea compatible. Puede que el Visor de eventos muestre errores en el dispositivo.

  Para que sea compatible, el usuario inicia sesión en el dispositivo y realiza la sincronización con Intune para recibir las directivas. Los usuarios pueden realizar una resincronización manual o esperar a la siguiente sincronización.

- Por ejemplo, se usan grupos dinámicos. Si Azure AD no actualiza los grupos dinámicos inmediatamente, estos dispositivos pueden aparecer como no compatibles.

En estos casos, decida si es más importante usar los grupos de dispositivos o mostrar todas las directivas como compatibles.

## <a name="device-already-has-an-email-profile-installed"></a>El dispositivo ya tiene instalado un perfil de correo electrónico

Si los usuarios crean un perfil de correo electrónico antes de inscribirse en Intune u Office 365 MDM, es posible que el perfil de correo electrónico implementado por Intune no funcione según lo previsto:

- **iOS/iPadOS**: Intune detecta un perfil de correo electrónico existente duplicado según el nombre de host y la dirección de correo electrónico. El perfil de correo electrónico creado por el usuario bloquea la implementación del perfil creado por Intune. Este es un problema común, ya que los usuarios de iOS/iPadOS suelen crear un perfil de correo electrónico y, luego, se inscriben. La aplicación Portal de empresa indica que el usuario no cumple con los requisitos y podría pedirle al usuario que quite el perfil de correo electrónico.

  El usuario debe quitar su perfil de correo electrónico para que el perfil de Intune pueda implementarse. Para evitar este problema, indique a los usuarios que realicen la inscripción y permita que Intune implemente el perfil de correo electrónico. Luego, los usuarios podrán crear su perfil de correo electrónico.

- **Windows**: Intune detecta un perfil de correo electrónico existente duplicado según el nombre de host y la dirección de correo electrónico. Intune sobrescribe el perfil de correo electrónico existente que ha creado el usuario.

- **Samsung KNOX Standard**: Intune identifica una cuenta de correo electrónico duplicada según la dirección de correo electrónico y la sobrescribe con el perfil de Intune. Si el usuario configura esa cuenta, el perfil de Intune la vuelve a sobrescribir. Este comportamiento puede confundir al usuario cuya configuración de cuenta se sobrescribe.

Samsung KNOX no usa el nombre de host para identificar el perfil. Le recomendamos que no cree varios perfiles de correo electrónico para implementar la misma dirección de correo electrónico en varios host, puesto que se sobrescribirán entre sí.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Error 0x87D1FDE8 para dispositivo KNOX Standard

**Problema**: después de crear e implementar un perfil de correo electrónico de Exchange Active Sync de Samsung KNOX Standard para distintos dispositivos Android, se notifica el error **0x87D1FDE8** o **error de corrección** en las propiedades del dispositivo > pestaña de directiva.

Revise la configuración de su perfil EAS de Samsung KNOX y la directiva de origen. Ya no se admite la opción de sincronización de notas de Samsung y no debe estar seleccionada en el perfil. Asegúrese de que los dispositivos tengan tiempo suficiente para procesar la directiva (hasta 24 horas).

## <a name="unable-to-send-images-from--email-account"></a>No se pueden enviar imágenes desde la cuenta de correo electrónico

Los usuarios que tienen cuentas de correo electrónico configuradas automáticamente no pueden enviar imágenes ni fotos desde sus dispositivos. Esto puede ocurrir si no está habilitada la opción **Allow e-mail to be sent from third-party applications** (Permitir que se envíe correo electrónico desde aplicaciones de terceros).

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración**.
3. Seleccione el perfil de correo electrónico > **Propiedades** > **Configuración**.
4. Establezca la opción **Allow e-mail to be sent from third-party applications** (Permitir que se envíe correo electrónico desde aplicaciones de terceros) en **Habilitar**.

## <a name="next-steps"></a>Pasos siguientes

Obtenga [ayuda de soporte técnico de Microsoft](../fundamentals/get-support.md) o use los [foros de la comunidad](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
