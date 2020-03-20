---
title: Obtención de una clave de recuperación para un dispositivo macOS desde el sitio web de Portal de empresa de Intune
description: Consulte la clave de recuperación de un dispositivo macOS inscrito y administrado.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5a15f3a05f96333eba19cf69c5778e6c8bd04f59
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79336763"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>Obtención de una clave de recuperación para un dispositivo macOS

Use el sitio web de Portal de empresa para obtener una clave de recuperación para el dispositivo macOS bloqueado. Si olvida la contraseña del dispositivo, puede iniciar sesión en Portal de empresa desde otro dispositivo para recuperar la clave.  

## <a name="get-recovery-key-from-company-portal-website"></a>Obtención de una clave de recuperación desde el sitio web de Portal de empresa

Esta opción está disponible para los dispositivos cifrados por su organización mediante FileVault. No está disponible para los dispositivos que ha cifrado personalmente.

1. En cualquier dispositivo, inicie sesión en el [sitio web de Portal de empresa](https://portal.manage.microsoft.com) y haga clic en el botón **Menú** > **Dispositivos**.  
2. Seleccione el dispositivo macOS cifrado.  
3. Seleccione **Obtener clave de recuperación**.  

    ![Captura de pantalla del sitio web de Portal de empresa, con la sección Obtener clave de recuperación resaltada.](./media/1907-recovery2-cpweb-intune.PNG)  

4. Aparecerá la clave de recuperación.

    ![Captura de pantalla del sitio web de Portal de empresa en la que se muestra la clave de recuperación.](./media/1907-recovery-cpweb-intune.PNG)  

    Por motivos de seguridad, la clave desaparecerá después de cinco minutos. Para volver a ver la clave, seleccione **Obtener clave de recuperación**.

Si no se encuentra una clave, pero el dispositivo está correctamente cifrado, póngase en contacto con el personal de soporte técnico de su organización. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>Obtención de una clave de recuperación desde la aplicación Portal de empresa para iOS

Puede recuperar su clave de recuperación personal (clave de FileVault) mediante la aplicación Portal de empresa para iOS. El dispositivo que tiene la clave de recuperación personal debe inscribirse en Intune y cifrarse con FileVault a través de Intune. Esta opción no está disponible para los dispositivos que ha cifrado personalmente. 

Con la aplicación Portal de empresa, puede abrir la vista web de Safari y obtener su clave de recuperación personal. 

1. Abra Portal de empresa.
2. Seleccione **Obtener clave de recuperación**.

    ![Captura de pantalla de la aplicación Portal de empresa para iOS en la que se muestra la clave de recuperación](./media/get-recovery-key-cpweb-02.png)  

El sitio web de Portal de empresa se abre en la vista web de Safari y muestra la clave. 

## <a name="it-pro-support"></a>Soporte para profesionales de TI

Si forma parte del personal soporte técnico de TI y quiere configurar y administrar el cifrado de FileVault para dispositivos macOS, vea [Uso del cifrado de dispositivos con Intune](/intune/protect/encrypt-devices).

## <a name="next-steps"></a>Pasos siguientes

Descubra qué más puede hacer desde el sitio web de Portal de empresa. Vea [Uso del sitio web de Portal de empresa de Intune](using-the-intune-company-portal-website.md) para obtener la lista de acciones.  

¿Aún necesita ayuda? Póngase en contacto con el personal de soporte técnico de TI. Para averiguar su información de contacto, vaya al [sitio web del portal de empresa](https://go.microsoft.com/fwlink/?linkid=2010980).  
