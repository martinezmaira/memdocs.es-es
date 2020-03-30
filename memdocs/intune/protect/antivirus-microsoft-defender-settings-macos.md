---
title: Configuración de la directiva antivirus de macOS para el antivirus de Microsoft Defender para Intune | Microsoft Docs
description: Vea una lista de los valores de configuración en el perfil del antivirus de Microsoft Defender para macOS. Este perfil forma parte de la directiva antivirus de seguridad de los puntos de conexión para macOS en Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: 9a0687b9e3938c93cfaebe0e064fd994077a92af
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086694"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Configuración de ATP de Microsoft defender para Mac en Microsoft Intune

Vea la configuración del perfil *antivirus* que puede configurar para ATP de Microsoft Defender para Mac en Microsoft Intune. Para obtener más información acerca de esta configuración, consulte [Advanced Threat Protection de Microsoft Defender para Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) en la documentación de Windows.

**ATP de Microsoft Defender**

- **Protección en tiempo real**  
  Requerir que Defender en dispositivos macOS usen la funcionalidad de supervisión en tiempo real. La supervisión en tiempo real ubica el malware e impide que se instale o se ejecute en su equipo. Puede desactivar esta opción durante un breve período de tiempo antes de que vuelva a activarse automáticamente.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **Habilitado**: forzar el uso de la supervisión en tiempo real. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Deshabilitado**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Protección que proporciona la nube**  
  De forma predeterminada, Defender envía información a Microsoft sobre los problemas que encuentre. Microsoft analiza esa información para obtener detalles sobre los problemas que le afectan a usted y a otros clientes a fin de ofrecer soluciones mejoradas. La protección funciona mejor cuando la opción *Envío automático de muestras* está activa.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **Habilitado**: la protección en la nube está activa. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Deshabilitado**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Envío automático de muestras**  
  Envía archivos de ejemplo a Microsoft para ayudar a proteger a los usuarios de dispositivos y a su organización ante posibles amenazas.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **Habilitado**: la protección en la nube está activa.  Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Deshabilitado**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Recopilación de datos de diagnóstico**

  Configure cómo se comparten los datos de uso y diagnóstico con Microsoft.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **Requerido**
  - **Opcional**

- **Carpetas excluidas del examen**  
  Seleccione **Agregar** y, a continuación, especifique las carpetas que se van a omitir durante un examen.

- **Archivos excluidos del examen**  
  Seleccione **Agregar** y, a continuación, especifique los archivos que se van a omitir durante un examen.

- **Tipos de archivo excluidos del examen**  
  Seleccione **Agregar** y, a continuación, especifique las extensiones de archivos que se van a omitir durante un examen.

- **Procesos excluidos del examen**  
  Seleccione **Agregar** y, a continuación, especifique los procesos que se van a omitir durante un examen.
