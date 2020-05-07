---
title: Usar plantillas para dispositivos Windows 10 en Microsoft Intune - Azure | Microsoft Docs
description: Use plantillas administrativas de Microsoft Intune y el Administrador de puntos de conexión para crear grupos de valores de configuración para dispositivos Windows 10. Use estos valores en un perfil de configuración de dispositivo para controlar programas de Office, Microsoft Edge, proteger características de Internet Explorer, controlar el acceso a OneDrive, usar características de escritorio remoto, habilitar la reproducción automática, establecer la configuración de administración de energía, usar la impresión a través de HTTP, usar otras opciones de inicio de sesión de usuario y controlar el tamaño del registro de eventos.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f609ec62259deffb220c8ee935d0f10a98ae77b5
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254901"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Usar plantillas de Windows 10 para configurar opciones de directiva de grupo en Microsoft Intune

Al administrar dispositivos en una organización, el objetivo es crear grupos de valores de configuración que se apliquen a otros grupos de dispositivos. Por ejemplo, hay varios grupos de dispositivos. Para el grupo A, se quiere asignar un conjunto concreto de valores configuración. Para el grupo B, se quiere asignar otro conjunto de valores configuración. También se quiere obtener una vista sencilla de los valores que se pueden configurar.

Esta tarea se puede realizar con **Plantillas administrativas** de Microsoft Intune. Las plantillas administrativas incluyen cientos de valores que controlan características de la versión 77 Microsoft Edge y posteriores, Internet Explorer, programas de Microsoft Office, el escritorio remoto, OneDrive, contraseñas y PIN, y mucho más. Esta configuración permite a los administradores de grupo administrar las directivas de grupo mediante la nube.

Esta característica se aplica a:

- Windows 10 y versiones posteriores

La configuración de Windows es similar a la configuración de la directiva de grupo (GPO) en Active Directory (AD). Estas configuraciones están integradas en Windows y son [configuraciones con respaldo de ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) en las que se usa XML. La configuración de Office y Microsoft Edge está probada por ADMX y utiliza la configuración de ADMX en los [archivos de plantillas administrativas de Office](https://www.microsoft.com/download/details.aspx?id=49030) y los [archivos de plantillas administrativas de Microsoft Edge](https://www.microsoftedgeinsider.com/enterprise). Y las plantillas de Intune están totalmente basadas en la nube. Ofrecen una manera simple y sencilla de configurar y de buscar la configuración deseada.

Las **plantillas administrativas** están integradas en Intune y no requieren personalizaciones, ni siquiera el uso de OMA-URI. Como parte de la solución de administración de dispositivos móviles (MDM), use estos valores de plantilla como centro único para administrar los dispositivos Windows 10.

En este artículo se enumeran los pasos para crear una plantilla para dispositivos Windows 10 y se muestra cómo filtrar todas las opciones disponibles en Intune. Cuando se crea la plantilla, se crea un perfil de configuración de dispositivo. Luego se puede asignar o implementar este perfil en los dispositivos Windows 10 de la organización.

## <a name="before-you-begin"></a>Antes de comenzar

- Algunos de estos ajustes están disponibles a partir de la versión 1709 de Windows 10 (RS2/compilación 15063). Algunas opciones de configuración no se incluyen en todas las ediciones de Windows. Para obtener la mejor experiencia, se recomienda usar Windows 10 Enterprise versión 1903 (19H1/compilación 18362) y posteriores.

- La configuración de Windows usa los [CSP de directivas de Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). El CSP funciona en diferentes ediciones de Windows, como por ejemplo, Home, Professional, Enterprise, etcétera. Para ver si un CSP funciona en una edición específica, vaya a [CSP de directivas de Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Crear la plantilla

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
    - **Perfil**: seleccione **Plantillas administrativas**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es **Plantilla de administración: Plantilla de administración de Windows 10 que configura los valores XYZ en Microsoft Edge**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En **Opciones de configuración**, configure las opciones que se aplican al dispositivo (**Configuración del equipo**) y la configuración que se aplica a los usuarios (**Configuración del usuario**):

    > [!div class="mx-imgBorder"]
    > ![Aplicación de la configuración de la plantilla de ADMX a usuarios y dispositivos en el Administrador de puntos de conexión de Microsoft Intune](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Al seleccionar **Configuración del equipo**, se muestran las categorías de configuración. Puede seleccionar cualquier categoría para ver la configuración disponible.

    Por ejemplo, seleccione **Configuración del equipo** > **Componentes de Windows** > **Internet Explorer** para ver la configuración del dispositivo que se aplica a Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Vea toda configuración de dispositivos que se aplica a Internet Explorer en el Administrador de puntos de conexión de Microsoft Intune](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png).

9. También puede seleccionar **Todos los valores** para ver todas las opciones de configuración del dispositivo. Desplácese hacia abajo para usar las flechas anterior y siguiente para ver más opciones de configuración:

    > [!div class="mx-imgBorder"]
    > ![Lista de ejemplo de valores y uso de los botones Anterior y Siguiente](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Seleccione cualquier valor. Por ejemplo, filtre por **Office** y seleccione **Activar exploración restringida**. Se muestra una descripción detallada del valor. Elija **Habilitado**, **Deshabilitado** o bien deje el valor como **Sin configurar** (valor predeterminado). La descripción detallada también explica lo que sucede cuando se elige **Habilitado**, **Deshabilitado** o **Sin configurar**.

    > [!TIP]
    > La configuración de Windows en Intune se correlaciona con la ruta de acceso de la directiva de grupo local que ve en el Editor de directivas de grupo local (`gpedit`).

11. Haga clic en **Aceptar** para guardar los cambios.

    Siga examinando la lista de valores y configure los que quiera en el entorno. Estos son algunos ejemplos:

    - Use el valor **Configuración de notificaciones para macros de VBA** para controlar las macros de VBA en diferentes programas de Microsoft Office, incluidos Word y Excel.
    - Use el valor **Permitir la descarga de archivos** para permitir o evitar las descargas desde Internet Explorer.
    - Use **Requerir una contraseña al activar el equipo (conectado)** para solicitar una contraseña a los usuarios cuando los dispositivos se activan del modo de suspensión.
    - Use el valor **Descargar los controles ActiveX no firmados** para evitar que los usuarios descarguen controles ActiveX no firmados de Internet Explorer.
    - Use el valor **Desactivar Restaurar sistema** para permitir o evitar que los usuarios ejecuten una restauración del sistema en el dispositivo.
    - Use la opción de **permitir la importación de favoritos** para permitir o impedir que los usuarios importen favoritos de otro explorador en Microsoft Edge.
    - Y mucho más...

12. Seleccione **Siguiente**.
13. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](..//fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

14. En **Asignaciones**, seleccione el usuario o los grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Si el perfil se asigna a grupos de usuarios, las opciones configuradas de ADMX se aplican a cualquier dispositivo al que el usuario se inscriba e inicie sesión. Si el perfil se asigna a grupos de dispositivos, las opciones configuradas de ADMX se aplican a cualquier usuario que inicie sesión en ese dispositivo. Esta asignación se produce si el valor de ADMX es una configuración de equipo (`HKEY_LOCAL_MACHINE`) o una configuración de usuario (`HKEY_CURRENT_USER`). Con algunas opciones, una configuración de equipo asignada a un usuario también puede afectar a la experiencia de otros usuarios en ese dispositivo.
    
    Para obtener más información, vea [Grupos de usuarios frente a grupos de dispositivos](device-profile-assign.md#user-groups-vs-device-groups).

    Seleccione **Siguiente**.

15. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

La siguiente vez que el dispositivo busca actualizaciones de configuración, se aplican los valores que configuró.

## <a name="find-some-settings"></a>Buscar algunos valores

Hay cientos de valores disponibles en estas plantillas. Para que sea más fácil encontrar un valor concreto, use las características integradas:

- En la plantilla, seleccione las columnas **Configuración**, **Estado**, **Tipo de configuración** o **Ruta** para ordenar la lista. Por ejemplo, seleccione la columna **Ruta de acceso** y use la flecha siguiente para ver la configuración en la ruta de acceso `Microsoft Excel`:

- En la plantilla, use el cuadro **Buscar** para buscar valores específicos. Puede buscar por configuración o por la ruta de acceso. Por ejemplo, busque `copy`. Aparecen todos los valores con `copy`:

  > [!div class="mx-imgBorder"]
  > ![Búsqueda de copia para mostrar las configuraciones del dispositivo en las plantillas administrativas de Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  En otro ejemplo, busque `microsoft word`. Aparecen los valores que puede establecer para el programa Microsoft Word. Busque `explorer` para ver los valores de Internet Explorer que puede agregar a la plantilla.

## <a name="next-steps"></a>Pasos siguientes

Se crea la plantilla, pero quizá no haga nada todavía. A continuación, [asigne la plantilla (también denominada perfil)](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Actualice [Office 365 mediante las plantillas administrativas](administrative-templates-update-office.md).

[Tutorial: Usar la nube para configurar una directiva de grupo en dispositivos de Windows 10 con plantillas ADMX y Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
