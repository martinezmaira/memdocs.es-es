---
title: Uso de directivas de Intune con dispositivos de Configuration Manager con asociación de inquilinos | Microsoft Docs
description: Configure la asociación de inquilinos de dispositivos de Configuration Manager al centro de administración de Microsoft Endpoint Manager para que pueda implementar directivas admitidas de Microsoft Intune en esos dispositivos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d56b06b49846201d6198c1abc81185bf74765ae3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823530"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Configuración de la asociación de inquilinos para admitir directivas de seguridad de punto de conexión de Intune

Cuando se usa el escenario de asociación de inquilinos de Configuration Manager, se pueden implementar directivas de seguridad de punto de conexión de Intune en los dispositivos que se administran con Configuration Manager. Para usar este escenario, primero debe configurar la asociación de inquilinos para Configuration Manager y habilitar colecciones de dispositivos de Configuration Manager para su uso con Intune. Una vez que las colecciones están habilitadas para su uso, se usa el centro de administración de Microsoft Endpoint Manager para crear e implementar las directivas.

Los siguientes tipos de directivas se admiten en los dispositivos de Configuration Manager que tienen asociación de inquilinos:

- Directiva de antivirus de seguridad de punto de conexión
- Directiva de detección y respuesta de seguridad del punto de conexión

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Requisitos para usar la directiva de Intune para la asociación de inquilinos

Para admitir el uso de directivas de seguridad de punto de conexión de Intune con dispositivos de Configuration Manager, se necesitan las siguientes configuraciones en el entorno de Configuration Manager. En este artículo se proporcionan [instrucciones de configuración](#set-up-configuration-manager-to-support-intune-policies):

### <a name="general-requirements-for-tenant-attach"></a>Requisitos generales para la asociación de inquilinos

- **Configuración de la asociación de inquilinos**: con el escenario de *asociación de inquilinos*, puede sincronizar colecciones de dispositivos de Configuration Manager con el centro de administración de Microsoft Endpoint Manager. Después, puede usar el centro de administración para implementar las directivas admitidas en esas colecciones.

  La asociación de inquilinos se configura a menudo con administración conjunta, pero puede hacerlo de forma independiente.

- **Sincronización de colecciones de Configuration Manager**: al configurar la asociación de inquilinos, puede seleccionar las colecciones de dispositivos de Configuration Manager que se van a sincronizar con el centro de administración de Microsoft Endpoint Manager. También puede volver después para modificar las colecciones de dispositivos que se sincronizan. Las directivas admitidas para dispositivos de Configuration Manager solo se pueden asignar a colecciones que haya sincronizado.

  Después de seleccionar las colecciones que se van a sincronizar, debe habilitarlas para su uso con las directivas de seguridad de punto de conexión de Intune.

- **Permisos para Azure AD**: para realizar la configuración de la asociación de inquilinos, necesitará una cuenta con permisos de administrador global para la suscripción de Azure.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Requisitos específicos para las directivas de seguridad de punto de conexión de Intune

- **Directiva de antivirus** (*versión preliminar*):

  - **Configuration Manager**: se admiten los siguientes entornos:

    - **Versión 2006 o posterior de la rama actual de Configuration Manager**: con esta versión de la rama actual, se ha agregado compatibilidad con directivas de antivirus de Intune.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Inquilino de Protección contra amenazas avanzada de Microsoft Defender**: el inquilino de ATP de Microsoft Defender se debe integrar con el de Microsoft Endpoint Manager (suscripción de Intune).  Vea [Uso de ATP de Microsoft Defender](advanced-threat-protection.md) en la documentación de Intune.

- **Directiva de detección de puntos de conexión y respuesta**:

  - **Configuration Manager**: se admiten los siguientes entornos:

    - **Technical Preview 2003 o posterior de Configuration Manager** : con la versión de Technical Preview 2003, se ha agregado compatibilidad con directivas de detección de puntos de conexión y respuesta de Intune.

    - **Versión 2002 o posterior de la rama actual de Configuration Manager**: si usa Configuration Manager con la versión 2002, debe instalar la actualización en la consola **Configuration Manager 2002 Hotfix (KB4563473)** . Esta actualización permite la compatibilidad en Configuration Manager 2002 con el uso de directivas de seguridad de punto de conexión.

  - **Inquilino de Protección contra amenazas avanzada de Microsoft Defender**: el inquilino de ATP de Microsoft Defender se debe integrar con el de Microsoft Endpoint Manager (suscripción de Intune).  Vea [Uso de ATP de Microsoft Defender](advanced-threat-protection.md) en la documentación de Intune.

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Configuración de Configuration Manager para la compatibilidad con directivas de Intune

Antes de implementar las directivas de Intune en dispositivos de Configuration Manager, realice las configuraciones que se detallan en las secciones siguientes. Estas configuraciones incorporan los dispositivos de Configuration Manager con ATP de Microsoft defender y les permiten trabajar con las directivas de Intune.

Las siguientes tareas se realizan en la consola de Configuration Manager. Si no está familiarizado con Configuration Manager, trabaje con un administrador de Configuration Manager para realizar estas tareas.

1. [Instalación de la actualización de Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Habilitación de la asociación de inquilinos](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Selección de las colecciones para sincronizar](#task-3-select-collections-to-synchronize)
4. [Habilitación de las colecciones para admitir directivas de Intune](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Para obtener más información sobre el uso de ATP de Microsoft Defender con Configuration Manager, vea los artículos siguientes en el contenido de la Configuration Manager:
>
> - [Incorporación de clientes de Configuration Manager a ATP de Microsoft Defender a través del Centro de administración de Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Tarea 1: Instalación de la actualización de Configuration Manager

Si usa la versión 2002 de la rama actual de Configuration Manager, instale la siguiente actualización en la consola que agrega compatibilidad con las directivas de seguridad de punto de conexión que se implementan desde el centro de administración de Microsoft Endpoint Manager.

**Detalles de la actualización**:

- **Revisión de Configuration Manager 2002 (KB4563473)**

Para instalar esta actualización, siga las instrucciones de [Instalación de actualizaciones en la consola](../../configmgr/core/servers/manage/install-in-console-updates.md) en la documentación de Configuration Manager.

Después de instalar la actualización, vuelva aquí para continuar con la configuración del entorno para admitir directivas de punto de conexión del centro de administración de Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Tarea 2: Configuración de la asociación de inquilinos y sincronización de colecciones

Con la asociación de inquilinos se especifican colecciones de dispositivos desde la implementación de Configuration Manager para la sincronización con el centro de administración de Microsoft Endpoint Manager. Después de sincronizar las colecciones, use el centro de administración para ver información sobre esos dispositivos e implementar en ellos la directiva de seguridad de punto de conexión.

Para más información sobre el escenario de asociación de inquilinos, consulte [Habilitación de la asociación de inquilinos](../../configmgr/tenant-attach/device-sync-actions.md) en el contenido de Configuration Manager.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Habilitación de la asociación de inquilinos cuando no se ha habilitado la administración conjunta

> [!TIP]
> El **Asistente para la configuración de administración conjunta** de la consola de Configuration Manager se usa para habilitar la asociación de inquilinos, pero no es necesario habilitar la administración conjunta.
>
> Si tiene previsto habilitar la administración conjunta, antes de continuar debe estar familiarizado con ella, sus requisitos previos y cómo se administran las cargas de trabajo. Vea [¿Qué es la administración conjunta?](../../configmgr/comanage/overview.md) en la documentación de Configuration Manager.

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).
2. En la cinta de opciones, haga clic en **Configure co-management** (Configurar la administración conjunta) para abrir el asistente.
3. En la página **Tenant onboarding** (Incorporación de inquilinos), seleccione **AzurePublicCloud** para el entorno. La nube de Azure Government no es compatible.
   1. Haga clic en **Iniciar sesión**. Use la cuenta de *administrador global* para iniciar sesión.

   2. Asegúrese de que la opción **Cargar en el centro de administración de Microsoft Endpoint Manager** esté seleccionada en la página **Incorporación de inquilinos**.

   3. Desactive la opción **Habilitar la inscripción automática de clientes para la administración conjunta**.

      Cuando está activada, el asistente presenta páginas adicionales para completar la configuración de la administración conjunta. Para obtener más información, vea [Habilitación de la administración conjunta](../../configmgr/comanage/how-to-enable.md) en el contenido de Configuration Manager.

     ![Configuración de la asociación de inquilinos](./media/tenant-attach-intune/tenant-onboarding.png)

4. Haga clic en **Siguiente** y luego en **Sí** para aceptar la notificación **Crear aplicación de AAD**. Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación de Azure AD para facilitar la sincronización de las colecciones con el centro de administración de Microsoft Endpoint Manager.

5. En la página **Configurar carga**, configure las colecciones que quiere sincronizar. Puede limitar la configuración a una o varias colecciones de dispositivos, o bien usar el valor de carga de dispositivos recomendado para **Todos los dispositivos administrados por Microsoft Endpoint Configuration Manager**.

   > [!TIP]
   > Puede omitir la selección de colecciones ahora y, luego, usar la información de la tarea siguiente (tarea 3) para configurar las colecciones que se van a sincronizar con el centro de administración de Microsoft Endpoint Manager.

6. Haga clic en **Resumen** para revisar la selección y luego en **Siguiente**.

7. Cuando el asistente esté completo, haga clic en **Cerrar**.

   La asociación de inquilinos ya está configurada y las colecciones seleccionadas se sincronizan con el centro de administración de Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Habilitación de la asociación de inquilinos cuando ya se usa la administración conjunta

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).

2. Haga clic con el botón derecho en la configuración de administración conjunta y seleccione **Propiedades**.

3. En la pestaña **Configure upload** (Configurar carga), seleccione **Upload to Microsoft Endpoint Manager admin center** (Cargar en el centro de administración de Microsoft Endpoint Manager). Haga clic en **Aplicar**.

   El valor predeterminado para la carga de dispositivos es **All my devices managed by Microsoft Endpoint Configuration Manager** (Todos los dispositivos administrados por Microsoft Endpoint Configuration Manager). También puede optar por limitar la configuración a una o varias colecciones de dispositivos.

   ![Visualización de la pestaña Propiedades de administración conjunta](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > Puede omitir la selección de colecciones ahora y, luego, usar la información de la tarea siguiente (tarea 3) para configurar las colecciones que se van a sincronizar con el centro de administración de Microsoft Endpoint Manager.

4. Inicie sesión con la cuenta de *administrador global* cuando se le pida.

5. Haga clic en **Sí** para aceptar la notificación **Crear aplicación de AAD**. Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación de Azure AD para facilitar la sincronización.

6. Haga clic en **Aceptar** para salir de las propiedades de administración conjunta una vez que haya terminado de realizar los cambios.

   La asociación de inquilinos ya está configurada y las colecciones seleccionadas se sincronizan con el centro de administración de Microsoft Endpoint Manager.

### <a name="task-3-select-collections-to-synchronize"></a>Tarea 3: Selección de las colecciones para sincronizar

Una vez que se ha configurado la asociación de inquilinos, puede seleccionar colecciones para sincronizarlas. Si todavía no ha sincronizado las colecciones o necesita volver a configurar las que sincroniza, puede editar las propiedades de la administración conjunta en la consola de Configuration Manager para hacerlo.

#### <a name="select-collections"></a>Selección de colecciones

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).

2. Haga clic con el botón derecho en la configuración de administración conjunta y seleccione **Propiedades**.

3. En la pestaña **Configure upload** (Configurar carga), seleccione **Upload to Microsoft Endpoint Manager admin center** (Cargar en el centro de administración de Microsoft Endpoint Manager). Haga clic en **Aplicar**.

   El valor predeterminado para la carga de dispositivos es **All my devices managed by Microsoft Endpoint Configuration Manager** (Todos los dispositivos administrados por Microsoft Endpoint Configuration Manager). También puede optar por limitar la configuración a una o varias colecciones de dispositivos.

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Tarea 4: Habilitación de colecciones para las directivas de seguridad de punto de conexión

Después de configurar las colecciones que se van a sincronizar con el centro de administración de Microsoft Endpoint Manager, habilítelas para que funcionen con las directivas de seguridad de punto de conexión. Cuando se habilitan las colecciones de dispositivos para que funcionen con las directivas de seguridad de punto de conexión de Intune, se configuran los dispositivos de esas colecciones para incorporarse a ATP de Microsoft Defender.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Habilitación de las colecciones que se van a usar con directivas de seguridad de punto de conexión

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Pasos siguientes

- [Configure directivas de seguridad de punto de conexión](endpoint-security-policy.md#create-an-endpoint-security-policy) para *antivirus* y *detección de puntos de conexión y respuesta*.

- Obtenga más información sobre [detección de puntos de conexión y respuesta](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) en la documentación de ATP de Microsoft Defender.
