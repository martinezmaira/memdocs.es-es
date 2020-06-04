---
title: 'Incorporación o definición de configuración de educación en Microsoft Intune: Azure | Microsoft Docs'
description: Use la aplicación Hacer un examen en un perfil de configuración de dispositivo en Windows 10 y dispositivos posteriores en Microsoft Intune. Cree un perfil de configuración mediante la configuración de educación y escriba una dirección URL de aplicación de examen, elija cómo los usuarios inician sesión, supervise la pantalla durante el examen y permita o evite sugerencias de texto durante el examen.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52eae65e6735ad655c2e8db53e34383ccc5e3b30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988387"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Uso de la aplicación Hacer un examen en dispositivos Windows 10 en Microsoft Intune

Los perfiles de educación en Intune están diseñados para que los alumnos realicen una prueba o un examen en dispositivos. Esta característica incluye la aplicación **Hacer un examen** y la configuración para agregar una dirección URL de examen, elegir cómo los usuarios finales inician sesión en el examen, etc. Esta característica es compatible con la siguiente plataforma:

- Windows 10 y versiones posteriores

Cuando el usuario inicia sesión, la aplicación Hacer un examen se abre automáticamente con el examen especificado. No se pueden ejecutar otras aplicaciones en el dispositivo mientras el examen está en curso. [Hacer exámenes en Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) proporciona más detalles sobre la aplicación Hacer un examen.

En este artículo se enumeran los pasos para crear un perfil de configuración de dispositivos en Microsoft Intune. También incluye información para leer y obtener información sobre la configuración de educación disponible para los dispositivos Windows 10.

## <a name="create-a-device-profile"></a>Creación del perfil de un dispositivo

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
    - **Perfil**: Seleccione **Evaluación segura (Educación)** .

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración**, especifique las opciones que quiera configurar:

    - [Windows 10 y versiones posteriores](education-settings-windows.md)

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione los usuarios o el grupo de usuarios que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

La próxima vez que cada dispositivo se registre, se aplicará la directiva.

## <a name="next-steps"></a>Pasos siguientes

Consulte una lista de las [configuraciones de educación de Windows 10](education-settings-windows.md) y sus descripciones.

Una vez [asignado el perfil](device-profile-assign.md), [supervise su estado](device-profile-monitor.md).
