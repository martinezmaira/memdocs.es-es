---
title: Cómo inscriben dispositivos los usuarios
titleSuffix: Configuration Manager
description: Comprenda cómo los usuarios inscriben dispositivos con la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724889"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Cómo inscriben los usuarios dispositivos con MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Con Configuration Manager la administración de dispositivos móviles (MDM) local, los usuarios pueden inscribir sus dispositivos. Hay dos requisitos previos:

- Con la configuración de cliente, conceda al usuario permiso para inscribirse.

- Instale el certificado raíz de confianza necesario en el dispositivo.

Para obtener más información sobre cómo configurar la inscripción, consulte [configuración de la inscripción de dispositivos para MDM local](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Inscripción de Windows 10

1. En un equipo Windows 10, vaya a **Configuración**.

1. Seleccione **cuentas**y, a continuación, seleccione **acceso profesional o educativo**.

1. Seleccione **conectar**, escriba su nombre principal de usuario (UPN) y seleccione **Continue (continuar**). El UPN puede ser el mismo que su dirección de correo electrónico, por jdoe@contoso.comejemplo,.

1. Escriba el nombre de dominio completo (FQDN) del punto de proxy de inscripción y seleccione **continuar**.

1. Escriba la contraseña y seleccione **iniciar sesión**.

1. Windows no necesita recordar la información de inicio de sesión para esta acción, por lo que debe seleccionar **omitir**.

Tras un breve período de tiempo, el dispositivo se inscribe con Configuration Manager.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Inscribir Windows 10 Mobile

1. En un dispositivo Windows 10 Mobile, vaya a **Configuración**.

1. Seleccione **cuentas**y, a continuación, seleccione **acceso al trabajo**.

1. Seleccione **Conectar**.

1. Escriba el UPN y el FQDN del punto de proxy de inscripción. Después, seleccione **conectar**.

1. En la siguiente pantalla, escriba su UPN y contraseña y, a continuación, seleccione **Inicio de sesión**.

Tras un breve período de tiempo, el dispositivo se inscribe con Configuration Manager. Seleccione **Listo**.

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Comprobar la inscripción

Use la consola de Configuration Manager para comprobar que los dispositivos están inscritos correctamente. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione **Dispositivos**. Examine o busque el dispositivo inscrito en la lista de dispositivos.
