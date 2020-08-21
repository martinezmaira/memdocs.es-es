---
title: Configuración del análisis de escritorio
titleSuffix: Configuration Manager
description: Guía paso a paso para la configuración de Análisis de escritorio y la incorporación al servicio
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: facfb2be1972933524c7ad632537fc8306939c1c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700759"
---
# <a name="how-to-set-up-desktop-analytics"></a>Configuración de Análisis de escritorio

Use este procedimiento para iniciar sesión en Análisis de escritorio y configurarlo en su suscripción. Este es un procedimiento único para configurar Análisis de escritorio para su organización.  

> [!Important]  
> Para obtener más información sobre los requisitos previos generales para usar Análisis de escritorio con Configuration Manager, consulte [Requisitos previos](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>Incorporación inicial

1. Abra el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) en Administración de dispositivos de Microsoft 365 con un usuario que tenga el rol de **administrador global**. Seleccione **Inicio**. Alternativamente, en la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, seleccione el nodo **Servicio de Análisis de escritorio** y seleccione **Planear implementaciones**.

2. En la página **Aceptar el acuerdo de servicio**, revise el acuerdo de servicio y seleccione **Aceptar**.  

3. En la página **Confirmar la suscripción**, revise la lista de licencias aptas requeridas. Cambie el valor a **Sí** junto a **¿Tiene alguna de las suscripciones admitidas o superiores?** y, a continuación, seleccione **Siguiente**.  

4. En la página para **permitir el acceso de los usuarios**:

    - **Permita que Análisis de escritorio administre los roles de directorio en su nombre**: Análisis de escritorio asigna automáticamente a los **propietarios del área de trabajo** el rol de **administrador de Análisis de escritorio**. Si esos grupos ya son **administradores globales**, no se producirá ningún cambio.

        Aunque no seleccione esta opción, Análisis de escritorio agregará usuarios como miembros del grupo de seguridad. Un **administrador global** debe asignar manualmente el rol de **administrador de Análisis de escritorio** para los usuarios.

        Para obtener más información sobre la asignación de permisos de rol de administrador en Azure Active Directory y los permisos asignados a **administradores de Análisis de escritorio**, consulte [Permisos de roles de administrador en Azure Active Directory](/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análisis de escritorio preconfigura el grupo de seguridad de **propietarios del área de trabajo** en Azure Active Directory para crear y administrar áreas de trabajo y planes de implementación.

        Para agregar un usuario al grupo, escriba su nombre o dirección de correo electrónico en la sección **Escriba un nombre o una dirección de correo electrónico**. Cuando termine, seleccione **Siguiente**.

5. En la página **Configurar el área de trabajo**:  

    > [!NOTE]  
    > Para completar este paso, el usuario necesita permisos de **propietario del área de trabajo** y acceso adicional a la suscripción y al grupo de recursos de Azure. Para más información, consulte los [requisitos previos](overview.md#prerequisites).  

    - Para usar un área de trabajo existente para Análisis de escritorio, selecciónela y continúe con el siguiente paso.  

        > [!TIP]  
        > Solo puede tener un área de trabajo de Análisis de escritorio por inquilino de Azure AD. Los dispositivos solo pueden enviar datos de diagnóstico a un área de trabajo.  

    - Para crear un área de trabajo para Análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre de área de trabajo** globalmente único.

        2. Seleccione la lista desplegable para **seleccionar el nombre de la suscripción de Azure para esta área de trabajo** y elija la suscripción de Azure para esta área de trabajo.  

        3. **Cree un nuevo** grupo de recursos o **use uno existente**.

        4. Seleccione la **región** en la lista y, a continuación, seleccione **Agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **Set as Desktop Analytics workspace** (Establecer como área de trabajo de Análisis de escritorio).  A continuación, seleccione **Continuar** en el cuadro de diálogo **Confirmar y conceder acceso**.  

7. En la pestaña del nuevo explorador, seleccione una cuenta para iniciar sesión. Seleccione la opción **Consentimiento en nombre de la organización** y seleccione **Aceptar**.  

    > [!Note]  
    > Este consentimiento es para asignar a la aplicación MALogAnalyticsReader el rol de lector Log Analytics para el área de trabajo. Análisis de escritorio requiere este rol de aplicación. Para obtener más información, consulte [Rol de aplicación MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. De vuelta en la página **Configurar el área de trabajo**, seleccione **Siguiente**.  

9. En la página **Últimos pasos**, seleccione **Ir a Análisis de escritorio**.

Azure Portal muestra la página **Inicio** de Análisis de escritorio.

## <a name="next-steps"></a>Pasos siguientes

Siga con el artículo siguiente para conectar Configuration Manager con Análisis de escritorio.
> [!div class="nextstepaction"]  
> [Conexión de Configuration Manager](connect-configmgr.md)