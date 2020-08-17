---
title: Uso de la inscripción directa para dispositivos macOS
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo inscribir dispositivos macOS mediante la inscripción directa.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819977"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>Uso de la inscripción directa para dispositivos macOS

Intune admite la inscripción de dispositivos macOS mediante la inscripción directa (DE) para dispositivos corporativos. La inscripción directa no borra el dispositivo. Lo inscribe a través de la configuración de macOS. Este método solo admite dispositivos **sin afinidad de usuario**.

## <a name="prerequisites"></a>Requisitos previos

- Acceso físico a dispositivos macOS
- [Configurar entidad de MDM](../fundamentals/mdm-authority-set.md)
- [Un certificado push MDM de Apple](apple-mdm-push-certificate-get.md)
 - Derechos de administrador en los dispositivos macOS que se van a inscribir

## <a name="create-an-apple-configurator-profile-for-devices"></a>Creación de un perfil de Apple Configurator para los dispositivos

Un perfil de inscripción de dispositivo define la configuración que se aplica durante la inscripción. Esta configuración se aplica una sola vez. Siga estos pasos para crear un perfil de inscripción para inscribir dispositivos macOS con Inscripción directa.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **Inscripción de dispositivos** > **Inscripción de Apple** > **Apple Configurator**.

2. Seleccione **Perfiles** > **Crear**.

3. En **Crear perfil de inscripción**, escriba un **nombre** y una **descripción** para el perfil con fines administrativos. Los usuarios no ven estos detalles. Puede usar este campo de nombre para crear un grupo dinámico en Azure Active Directory. Use el nombre de perfil para definir el parámetro enrollmentProfileName para asignar dispositivos con este perfil de inscripción. Obtenga más información sobre los grupos dinámicos de Azure Active Directory.

4. En **Afinidad de usuario**, elija **Inscribir sin afinidad de usuario**; seleccione esta opción para dispositivos no afiliados con un usuario único. Use esta opción para dispositivos que realizan tareas sin tener acceso a datos de usuario local. Las aplicaciones que requieren la afiliación de un usuario no funcionarán, incluida la aplicación Portal de empresa cuando se usa para instalar aplicaciones de línea de negocio. Es obligatorio para la inscripción directa.

     > [!NOTE]
     > **Inscribir con afinidad de usuario** no se admite en macOS cuando se usa Inscripción directa. En los dispositivos que necesitan afinidad de usuario, use Inscripción de dispositivo automatizada.

6. Elija **Crear** para guardar el perfil.

## <a name="direct-enrollment"></a>Inscripción directa
Como Inscripción directa solo admite la inscripción sin afinidad de usuario, no se puede usar el portal de empresa para instalar las aplicaciones disponibles.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Exportación del perfil e instalación en dispositivos macOS

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **Inscripción de dispositivos** > **Inscripción de Apple** > **Apple Configurator** > **Perfiles** > elija el perfil que se va a exportar > **Exportar perfil**.
2. En **Inscripción directa**, elija **Descargar perfil** y guarde el archivo. 

     > [!NOTE]
     > Un perfil de inscripción descargado es válido durante dos semanas después de la descarga. Mediante este vínculo puede descargar tantos perfiles de inscripción como necesite. La descarga de un perfil nuevo no anula el anterior, pero tampoco extiende el tiempo de expiración del archivo descargado antes.
         
3. Transfiera el archivo a un equipo macOS para instalarlo directamente.
4. Haga doble clic en el archivo **.mobileconfig** que ha guardado para abrirlo en Perfiles.
5. Cuando se le pida que instale el perfil de administración, seleccione **Instalar**.
6. En el mensaje siguiente, seleccione **Instalar** para confirmar que quiere instalar el perfil de administración.
7. Escriba las credenciales de una cuenta de administrador en el dispositivo macOS y haga clic en **Aceptar**.
8. Ahora el dispositivo macOS se inscribe y administra en Intune, y se empezarán a descargar los perfiles de destino.

## <a name="next-steps"></a>Pasos siguientes

Después de inscribir dispositivos macOS, puede empezar a [administrarlos](../remote-actions/device-management.md).