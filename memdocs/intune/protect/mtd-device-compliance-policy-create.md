---
title: Creación de directiva de cumplimiento de dispositivos de Mobile Threat Defense (MTD) con Microsoft Intune
titleSuffix: Microsoft Intune
description: Cree una directiva de cumplimiento de dispositivo de Intune que utilice sus niveles de amenazas de partners MTD asociados para determinar si un dispositivo móvil puede tener acceso a recursos de la empresa.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88f8a2ff04f536370f613341170e7fae0a808ff6
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365532"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Creación de directiva de cumplimiento de dispositivos de Mobile Threat Defense (MTD) con Intune

Intune con MTD le ayuda a detectar amenazas y a evaluar el riesgo en dispositivos móviles. Puede crear una regla de directivas de cumplimiento de dispositivos de Intune que evalúe el riesgo para determinar si el dispositivo cumple con la directiva o no lo hace. Luego puede usar una [directiva de acceso condicional](create-conditional-access-intune.md) para bloquear el acceso a servicios en función del cumplimiento del dispositivo.

> [!NOTE]
> Este tema se aplica a todos los partners de Mobile Threat Defense.

## <a name="before-you-begin"></a>Antes de comenzar

Como parte de la configuración de MTD, en la consola del partner de MTD se crea una directiva que clasifica las distintas amenazas como alta, media y baja. A continuación, verá el nivel de Mobile Threat Defense en la directiva de cumplimiento de dispositivos de Intune.

Requisitos previos de la directiva de cumplimiento de dispositivos con MTD:

- Configuración de la integración de MTD con Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>Creación de una directiva de cumplimiento de dispositivos de MTD

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión** > **Cumplimiento de dispositivos** > **Crear directiva**.

3. Seleccione **Plataforma** y, luego **Crear**.

4. En **Conceptos básicos**, especifique un **Nombre** y una **Descripción** (opcional) de la directiva de cumplimiento del dispositivo. Seleccione **Siguiente** para continuar.


5. En **Configuración de cumplimiento**, expanda y configure **Estado del dispositivo**. Elija el nivel de Mobile Threat en la lista desplegable **Requerir que el dispositivo tenga el nivel de amenaza del dispositivo**.

   - **Protegido**: este nivel es el más seguro. El dispositivo no puede tener ninguna amenaza presente y aún puede tener acceso a los recursos de la empresa. Si se encuentra alguna amenaza, el dispositivo se clasificará como no conforme.

   - **Bajo**: el dispositivo se evalúa como compatible si solo hay amenazas de nivel bajo. Cualquier valor por encima coloca al dispositivo en un estado de no conformidad.

   - **Media**: el dispositivo se evalúa como compatible si las amenazas que se encuentran en él son de nivel bajo o medio. Si se detectan amenazas de nivel alto, se determinará que el dispositivo no es compatible.

   - **Alta**: este nivel de amenaza es el menos seguro, ya que permite todos los niveles de amenaza y usa Mobile Threat Defense solo con fines informativos. Los dispositivos deben tener activada la aplicación MTD con esta configuración.

6. Seleccione **Siguiente** para pasar a **Asignaciones**. Seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

   Seleccione **Siguiente**.

7. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

> [!IMPORTANT]
> Si crea directivas de acceso condicional para Office 365 u otros servicios, se efectuará esta evaluación de cumplimiento de dispositivo y se bloqueará el acceso de los dispositivos no conformes a los recursos corporativos hasta que se resuelva la amenaza en el dispositivo.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Asignación de una directiva de cumplimiento de dispositivos de MTD

Para asignar o cambiar la asignación de una directiva de cumplimiento de dispositivos a los usuarios:

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión** > **Cumplimiento de dispositivos**.

3. Seleccione la directiva que quiere asignar a los usuarios y, luego, seleccione **Propiedades**.

4. Seleccione **Editar** para las asignaciones y, a continuación, use las opciones disponibles para *incluir* y *excluir* grupos de la recepción de esta directiva.  

5. Seleccione **Revisar y guardar** para completar la asignación. Al guardar la asignación, la directiva se implementa en los usuarios seleccionados y se evalúa el cumplimiento de sus dispositivos.

## <a name="next-steps"></a>Pasos siguientes

[Habilitar MTD con Intune](mtd-connector-enable.md)
