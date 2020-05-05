---
title: Inscribir dispositivos en MDM local
titleSuffix: Configuration Manager
description: Obtenga información acerca de los métodos para inscribir dispositivos para la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724609"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Inscripción de dispositivos para MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para administrar dispositivos con Configuration Manager la administración de dispositivos móviles (MDM) local, primero debe inscribirlos. A continuación, Configuration Manager puede comunicarse con los dispositivos para las tareas de administración. Configuration Manager proporciona dos métodos para inscribir dispositivos:

- **Inscripción de usuario**: los usuarios inician el proceso de inscripción en su dispositivo. Para que la inscripción de usuario se realice correctamente, instale el certificado raíz de confianza en el dispositivo y aprovisione el usuario para la inscripción en la configuración de cliente. Para inscribir un dispositivo, el usuario solo tiene que escribir sus credenciales.

    Para obtener más información, consulte [Cómo inscriben los usuarios los dispositivos](user-enroll-devices-on-premises-mdm.md).

- **Inscripción masiva**: el usuario del dispositivo no inicia la inscripción. Puede crear un paquete de inscripción masiva en Configuration Manager. Al abrirlo en el dispositivo, el paquete proporciona la información necesaria para inscribir el dispositivo.

    Para obtener más información, consulte el apartado sobre [la inscripción masiva de dispositivos](bulk-enroll-devices-on-premises-mdm.md).

Para obtener más información sobre las versiones del sistema operativo que Configuration Manager admiten para la inscripción de dispositivos en MDM local, consulte [configuraciones admitidas](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
