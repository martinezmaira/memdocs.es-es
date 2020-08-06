---
title: Solución de problemas de inscripción automática de Windows 10 en Intune
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo solucionar problemas con la inscripción automática.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 968aa9b2f7127e9b7f092f36a99b491a75f0b78c
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546873"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Solución de problemas de inscripción automática basada en directivas de grupo de Windows 10 en Intune

Se puede usar la directiva de grupo para desencadenar la inscripción automática en MDM para dispositivos unidos a un dominio de Active Directory (AD). Para obtener información sobre esta característica, vea [Inscripción automática de un dispositivo Windows 10 con directiva de grupo](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

## <a name="verify-the-configuration"></a>Comprobación de la configuración

Antes de empezar a solucionar problemas, es mejor comprobar que todo está configurado correctamente. Si la incidencia no se puede solucionar durante la comprobación, puede seguir solucionando problemas mediante la comprobación de algunos archivos de registro importantes.

- Compruebe que hay una licencia válida de Intune asignada al usuario que está intentando inscribir el dispositivo.

   ![Comprobación de la licencia de Intune](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Compruebe que la inscripción automática está habilitada para todos los usuarios que inscribirán los dispositivos en Intune. Para obtener más información, vea [Azure AD y Microsoft Intune: Inscripción automática de MDM en el portal nuevo](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal).

   ![Comprobación de la inscripción automática](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Compruebe que la opción **Ámbito de usuario de MDM** está establecida en **Todos** para permitir que todos los usuarios inscriban un dispositivo en Intune.
   - Compruebe que la opción **Ámbito de usuario de MDM** está establecida en **Ninguno**. De lo contrario, este valor tendrá prioridad sobre el ámbito de MDM y provocará incidencias.
   - Compruebe que la opción **Dirección URL de descubrimiento de MDM** está establecida en **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** .

- Compruebe que el dispositivo ejecuta Windows 10, versión 1709 o una versión posterior.

- Compruebe que los dispositivos estén establecidos en  **unido a Azure AD híbrido**. Esta configuración significa que los dispositivos están unidos a un dominio y a Azure AD.

   Para comprobar la configuración, ejecute **dsregcmd /status** en la línea de comandos. Después, compruebe los valores de estado siguientes en la salida:

   - Estado del dispositivo
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - Estado de SSO

     ```asciidoc
     AzureAdPrt: YES
     ```

   Se puede encontrar esta misma información en la lista de dispositivos unidos a Azure AD:

   ![Lista de dispositivos unidos a Azure AD](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- Tanto **Microsoft Intune** como **Inscripción en Microsoft Intune** se pueden mostrar en **Movilidad (MDM y MAM)**  en la hoja de Azure AD. Si están los dos, asegúrese de configurar las opciones de inscripción automática en **Microsoft Intune**.

- Compruebe que la siguiente configuración de directiva de grupo se ha implementado correctamente en todos los dispositivos que deben inscribirse en Intune:

   **Configuración del equipo** > **Directivas** > **Plantillas administrativas** > **Componentes de Windows** > **MDM** > **Habilitar la inscripción automática de MDM con credenciales de Azure AD predeterminadas**

   Puede ponerse en contacto con los administradores del dominio para comprobar que la configuración de la directiva de grupo se ha implementado correctamente.

- Asegúrese de que el dispositivo no esté inscrito en Intune mediante el agente de PC clásico.
- Compruebe la configuración siguiente en Azure AD e Intune:

   **En la configuración del dispositivo de Azure AD:**

   ![Configuración del dispositivo de Azure AD](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - La opción **Los usuarios pueden inscribir dispositivos en Azure AD** está establecida en **Todos**.
   - El número de dispositivos que tiene un usuario en Azure AD no supera la cuota de **número máximo de dispositivos por usuario**.
   
   **En las restricciones de inscripción en Intune:**

   - Se permite la inscripción de dispositivos Windows.

     ![Inscripción permitida de dispositivos Windows](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Solución de problemas

Si la incidencia persiste, examine los registros de MDM en el dispositivo en la ubicación siguiente de Visor de eventos:

**Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Administración**

Busque el id. de evento 75 (mensaje de evento "Inscripción automática de MDM: correcta"). Este evento indica que la inscripción automática se ha realizado correctamente.

El id. de evento 75 no se registra en las situaciones siguientes:

- Se produce un error en la inscripción.

  Para comprobar este error, busque el id. de evento 76 (mensaje de evento: Inscripción automática de MDM: error (código de error de Win32 desconocido: 0x8018002b)). Este evento indica que se ha producido una inscripción automática con errores.

  Para obtener una resolución de este error, vea [Solución de problemas con la inscripción de dispositivos Windows en Microsoft Intune](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors).

- La inscripción no se ha desencadenado en absoluto. En este caso, los id. de evento 75 y 76 no se registran.
  
  El proceso de inscripción automática se desencadena con la tarea "**Programación creada por el cliente de inscripción para inscribirse automáticamente en MDM desde AAD**" que se encuentra en el Programador de tareas, en **Microsoft** > **Windows** > **EnterpriseMgmt**.

  ![La inscripción no se ha desencadenado.](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Esta tarea se crea cuando la configuración de directiva de grupo **Habilitar la inscripción automática de MDM con las credenciales de Azure AD predeterminadas** se implementa correctamente en el dispositivo de destino. La tarea está programada para ejecutarse cada 5 minutos durante 1 día.

  Para comprobar que la tarea se ha iniciado, compruebe los registros de eventos del Programador de tareas en la ubicación siguiente del Visor de eventos:

  **Registros de aplicaciones y servicios > Microsoft > Windows > Programador de tareas > Operativo**

  Cuando la tarea se desencadena en el programador, se registra el id. de evento 107.

  Una vez completada la tarea, se registra el id. de evento 102. El evento se registra independientemente de si la inscripción automática se realiza correctamente.

  > [!NOTE]
  > Puede usar el registro del Programador de tareas para comprobar si se desencadena la inscripción automática. Sin embargo, no puede utilizar el registro para determinar si la inscripción automática se ha realizado correctamente.

  La situación siguiente puede provocar que la programación que crea el cliente de inscripción se inscriba automáticamente en MDM desde la tarea de AAD para que no se inicie:

  - El dispositivo ya está inscrito en otra solución de MDM. En este caso, el id. de evento 7016 junto con el código de error 2149056522 se registra en el registro de evento **Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **Programador de tareas** > **Operativo**.

    Para corregir esta incidencia, anule la inscripción del dispositivo de MDM.

  - Existe una incidencia de directiva de grupo. En este caso, fuerce una actualización de la configuración de la directiva de grupo ejecutando el comando siguiente:

    **gpupdate /force**

    Si la incidencia persiste, realice solución de problemas adicionales en Active Directory.

## <a name="next-steps"></a>Pasos siguientes
[Solución de problemas de inscripción de dispositivos Windows](troubleshoot-windows-enrollment-errors.md)