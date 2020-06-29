---
title: Administración de la configuración de detección y respuesta de puntos de conexión con directivas de seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas para los dispositivos administrados con la directiva de detección y respuesta de puntos de conexión en Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
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
ms.openlocfilehash: ae95fb48296f778fb98affa2270ba763d79fb766
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879667"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Directiva de detección y respuesta de puntos de conexión para la seguridad de puntos de conexión en Intune

Al integrar Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) con Intune, puede usar directivas de seguridad de punto de conexión para la detección de puntos de conexión y respuesta (EDR) a fin de administrar la configuración de EDR e incorporar dispositivos a ATP de Defender.

Las funciones de detección de puntos de conexión y respuesta de ATP de Microsoft Defender proporcionan detecciones de ataques avanzadas casi en tiempo real y procesables. Los analistas de seguridad pueden priorizar las alertas de forma eficaz, obtener visibilidad sobre el ámbito completo de una vulneración y tomar medidas de respuesta para corregir las amenazas.

Las directivas de EDR incluyen perfiles específicos de la plataforma para administrar la configuración de EDR. Los perfiles incluyen automáticamente un *paquete de incorporación* para ATP de Microsoft Defender. La incorporación de paquetes es la manera de configurar los dispositivos de modo que funcionen con ATP de Microsoft Defender. Una vez que se incorpora un dispositivo, puede empezar a usar los datos de amenazas de ese dispositivo.

Las directivas de EDR se implementan en grupos de dispositivos en Azure Active Directory (Azure AD) que se administran con Intune y en colecciones de dispositivos locales que se administran con Configuration Manager, incluidos los servidores de Windows. Las directivas de EDR para las distintas rutas de administración requieren otros paquetes de incorporación. Por tanto, creará directivas de EDR independientes para los diferentes tipos de dispositivos que administra.

> [!TIP]
> La compatibilidad con los dispositivos que administra con Configuration Manager está en *versión preliminar pública*.

Busque las directivas de seguridad de puntos de conexión para EDR en *Administrar*, en el nodo **Seguridad de los puntos de conexión** del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Vea [Configuración del perfil de respuesta y detección de puntos de conexión](endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Requisitos previos para las directivas de EDR

**General**:

- **Inquilino de Advanced Threat Protection de Microsoft Defender**: el inquilino de ATP de Microsoft Defender se debe integrar con el de Microsoft Endpoint Manager (suscripción de Intune) para poder crear directivas de EDR. Vea [Uso de ATP de Microsoft Defender](advanced-threat-protection.md) en la documentación de Intune.

**Para admitir dispositivos desde Configuration Manager**:

para admitir el uso de directivas de EDR con dispositivos de Configuration Manager, el entorno de Configuration Manager requiere las siguientes configuraciones adicionales. En este artículo se proporcionan [instrucciones de configuración](#set-up-configuration-manager-to-support-edr-policy):

- **Configuration Manager con la versión 2002 o posterior**: el sitio debe ejecutar Configuration Manager 2002 o posterior.

- **Instalación de la actualización de Configuration Manager**: para habilitar la compatibilidad en Configuration Manager 2002 a fin de usar la directiva de EDR que cree en el centro de administración de Microsoft Endpoint Manager, instale la actualización siguiente desde la consola de Configuration Manager:
  - **Revisión de Configuration Manager 2002 (KB4563473)**

- **Configuración de la asociación de inquilinos**: la asociación de inquilinos permite sincronizar colecciones de dispositivos desde Configuration Manager con el centro de administración de Microsoft Endpoint Manager. Después, puede usar el centro de administración para implementar las directivas de EDR en esas colecciones.

  La asociación de inquilinos se configura a menudo con administración conjunta, pero puede hacerlo de forma independiente.

- **Sincronización de colecciones de Configuration Manager**: al configurar la asociación de inquilinos, puede seleccionar las colecciones de dispositivos de Configuration Manager que se van a sincronizar con el centro de administración de Microsoft Endpoint Manager. También puede volver después para modificar las colecciones de dispositivos que se sincronizan. La directiva de EDR para los dispositivos de Configuration Manager solo se puede asignar a las colecciones que haya sincronizado.

  Después de seleccionar las colecciones que se van a sincronizar, debe habilitarlas para su uso con ATP de Microsoft Defender.

- **Permisos para Azure AD**: con el fin de completar la configuración de la asociación de inquilinos y configurar las colecciones de Configuration Manager que se van a sincronizar con el centro de administración de Microsoft Endpoint Manager, necesitará una cuenta con permisos de administrador global para la suscripción de Azure.

## <a name="edr-profiles"></a>Perfiles de EDR

[Vea las opciones](endpoint-security-edr-profile-settings.md) que puede configurar para las siguientes plataformas y perfiles.

**Intune**: los dispositivos que administra con Intune admiten lo siguiente:

- Plataforma: **Windows 10 y versiones posteriores**: Intune implementa la directiva en los dispositivos de los grupos de Azure AD.
- Perfil: **Detección y respuesta de puntos de conexión (MDM)**

**Configuration Manager** *(en versión preliminar)* : los dispositivos que administra con Configuration Manager admiten lo siguiente:

- Plataforma: **Windows 10 y Windows Server**: Configuration Manager implementa la directiva en los dispositivos de las colecciones de Configuration Manager.
- Perfil: **Detección de puntos de conexión y respuesta (ConfigMgr) (versión preliminar)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Configurar Configuration Manager para admitir la directiva de EDR

Antes de implementar las directivas de EDR en dispositivos de Configuration Manager, complete las configuraciones que se detallan en las secciones siguientes.

Estas configuraciones se realizan en la consola de Configuration Manager y en la implementación de Configuration Manager. Si no está familiarizado con Configuration Manager, planee trabajar con un administrador de Configuration Manager para completar estas tareas.  

En las secciones siguientes se tratan las tareas necesarias:

1. [Instalación de la actualización de Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Habilitación de la asociación de inquilinos](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Selección de las colecciones para sincronizar](#task-3-select-collections-to-synchronize)
4. [Habilitación de colecciones para ATP de Microsoft Defender](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> Para obtener más información sobre el uso de ATP de Microsoft Defender con Configuration Manager, vea los artículos siguientes en el contenido de la Configuration Manager:
>
> - [Incorporación de clientes de Configuration Manager a ATP de Microsoft Defender a través del Centro de administración de Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Tarea 1: Instalación de la actualización de Configuration Manager

La versión 2002 de Configuration Manager requiere una actualización para admitir el uso de las directivas de detección y respuesta de puntos de conexión que se implementan desde el centro de administración de Microsoft Endpoint Manager.

**Detalles de la actualización**:

- **Revisión de Configuration Manager 2002 (KB4563473)**

Encontrará esta actualización como *actualización en la consola* para Configuration Manager 2002.

Para instalar esta actualización, siga las instrucciones de [Instalación de actualizaciones en la consola](../../configmgr/core/servers/manage/install-in-console-updates.md) en la documentación de Configuration Manager.

Después de instalar la actualización, vuelva aquí para continuar con la configuración del entorno para admitir la directiva de EDR desde el centro de administración de Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Tarea 2: Configuración de la asociación de inquilinos y sincronización de colecciones

Si la administración conjunta estaba previamente habilitada, la asociación de inquilinos ya está configurada y puede ir directamente a la [Tarea 3](#task-3-select-collections-to-synchronize).

Con la asociación de inquilinos se especifican colecciones de dispositivos desde la implementación de Configuration Manager para la sincronización con el centro de administración de Microsoft Endpoint Manager. Después de sincronizar las colecciones, use el centro de administración para ver información sobre esos dispositivos e implementar en ellos la directiva de EDR desde Intune.  

Para obtener más información sobre el escenario de asociación de inquilinos, vea [Habilitación de la asociación de inquilinos](../../configmgr/tenant-attach/device-sync-actions.md) en el contenido de Configuration Manager.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Habilitación de la asociación de inquilinos cuando no se ha habilitado la administración conjunta

> [!TIP]
> El **Asistente para la configuración de administración conjunta** de la consola de Configuration Manager se usa para habilitar la asociación de inquilinos, pero no es necesario habilitar la administración conjunta.

Si tiene previsto habilitar la administración conjunta, antes de continuar debe estar familiarizado con la administración conjunta, sus requisitos previos y la administración de cargas de trabajo. Vea [¿Qué es la administración conjunta?](../../configmgr/comanage/overview.md) en la documentación de Configuration Manager.

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).
2. En la cinta de opciones, haga clic en **Configure co-management** (Configurar la administración conjunta) para abrir el asistente.
3. En la página **Tenant onboarding** (Incorporación de inquilinos), seleccione **AzurePublicCloud** para el entorno. La nube de Azure Government no es compatible.
   1. Haga clic en **Iniciar sesión**. Use la cuenta de *administrador global* para iniciar sesión.

   2. Asegúrese de que la opción **Cargar en el centro de administración de Microsoft Endpoint Manager** esté seleccionada en la página **Incorporación de inquilinos**.

   3. Desactive la opción **Habilitar la inscripción automática de clientes para la administración conjunta**.

      Cuando está activada, el asistente presenta páginas adicionales para completar la configuración de la administración conjunta. Para obtener más información, vea [Habilitación de la administración conjunta](../../configmgr/comanage/how-to-enable.md) en el contenido de Configuration Manager.

     ![Configuración de la asociación de inquilinos](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Haga clic en **Siguiente** y luego en **Sí** para aceptar la notificación **Crear aplicación de AAD**. Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación de Azure AD para facilitar la sincronización de las colecciones con el centro de administración de Microsoft Endpoint Manager.

5. En la página **Configurar carga**, configure las colecciones que quiere sincronizar. Puede limitar la configuración a una o varias colecciones de dispositivos, o bien usar el valor de carga de dispositivos recomendado para **Todos los dispositivos administrados por Microsoft Endpoint Configuration Manager**.

6. Haga clic en **Resumen** para revisar la selección y luego en **Siguiente**.

7. Cuando el asistente esté completo, haga clic en **Cerrar**.

   La asociación de inquilinos ya está configurada y las colecciones seleccionadas se sincronizan con el centro de administración de Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Habilitación de la asociación de inquilinos cuando se usa la administración conjunta

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).

2. Haga clic con el botón derecho en la configuración de administración conjunta y seleccione **Propiedades**.

3. En la pestaña **Configure upload** (Configurar carga), seleccione **Upload to Microsoft Endpoint Manager admin center** (Cargar en el centro de administración de Microsoft Endpoint Manager). Haga clic en **Aplicar**.
   - El valor predeterminado para la carga de dispositivos es **All my devices managed by Microsoft Endpoint Configuration Manager** (Todos los dispositivos administrados por Microsoft Endpoint Configuration Manager). También puede optar por limitar la configuración a una o varias colecciones de dispositivos.

     ![Visualización de la pestaña Propiedades de administración conjunta](media/endpoint-security-edr-policy/configure-upload.png)

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

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Tarea 4: Habilitación de colecciones para ATP de Microsoft Defender

Después de configurar las colecciones para sincronizar con el centro de administración de Microsoft Endpoint Manager, debe habilitarlas para que sean válidas para la incorporación y las directivas de ATP de Microsoft Defender.  Para ello, edite las propiedades de cada colección en la consola de Configuration Manager.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Habilitación de colecciones para usarlas con Advanced Threat Protection

1. Desde una consola de Configuration Manager conectada al sitio de nivel superior, haga clic con el botón derecho en una colección de dispositivos que sincronice con el centro de administración de Microsoft Endpoint Manager y seleccione **Propiedades**.

2. En la pestaña **Sincronización con la nube**, habilite la opción **Hacer que esta recopilación esté disponible para asignar directivas de ATP de Microsoft Defender en Intune**.

   - No se puede seleccionar esta opción si la jerarquía de Configuration Manager no está asociada al inquilino.
  
   ![Configuración de la sincronización en la nube](media/endpoint-security-edr-policy/cloud-sync.png)

3. Seleccione **Aceptar** para guardar la configuración.

   Ahora los dispositivos de esta colección pueden recibir la directiva de ATP de Microsoft Defender.

## <a name="create-and-deploy-edr-policies"></a>Creación e implementación de directivas de EDR

Cuando la suscripción de ATP de Microsoft Defender está integrada con Intune, puede crear e implementar directivas de EDR. Existen dos tipos distintos de directivas de EDR que se pueden crear. Uno es para los dispositivos que administra con Intune a través de MDM. El segundo tipo es para los dispositivos que administra con Configuration Manager.

Elegirá el tipo de directiva que creará al crear una directiva de EDR cuando seleccione la plataforma de la directiva.

Antes de implementar la directiva en los dispositivos administrados por Configuration Manager, [configure Configuration Manager para admitir la directiva de EDR](#set-up-configuration-manager-to-support-edr-policy) desde el centro de administración de Microsoft Endpoint Manager.

### <a name="create-edr-policies"></a>Creación de directivas de EDR

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión** > **Detección y respuesta de puntos de conexión** > **Crear directiva**.

3. Seleccione la plataforma y el perfil de la directiva. La siguiente información identifica las opciones:

   - Intune: Intune implementa la directiva en los dispositivos de los grupos de Azure AD. Al crear la directiva, seleccione lo siguiente:
     - Plataforma: **Windows 10 y versiones posteriores**
     - Perfil: **Detección y respuesta de puntos de conexión (MDM)**

   - Configuration Manager: Configuration Manager implementa la directiva en los dispositivos de las colecciones de Configuration Manager. Al crear la directiva, seleccione lo siguiente:
     - Plataforma: **Windows 10 y Windows Server**
     - Perfil: **Detección de puntos de conexión y respuesta (ConfigMgr) (versión preliminar)**

4. Seleccione **Crear**.

5. En la página **Datos básicos**, escriba un nombre y una descripción para el perfil y, después, elija **Siguiente**.

6. En la página **Opciones de configuración**, configure las opciones que quiera administrar con este perfil. El paquete de incorporación se incluye de forma automática y no se puede configurar.

   Cuando haya finalizado la configuración, seleccione **Siguiente**.

7. *Este paso solo se aplica al perfil **Detección de puntos de conexión y respuesta (MDM)***:  

   En la página **Etiquetas de ámbito**, seleccione **Seleccionar etiquetas de ámbito** para abrir el panel *Seleccionar etiquetas* a fin de asignar etiquetas de ámbito al perfil.
  
   Seleccione **Siguiente** para continuar.

8. En la página **Asignaciones**, seleccione los grupos o colecciones que recibirán esta directiva. La elección depende de la plataforma y el perfil que haya seleccionado:

   - Para Intune, seleccionará grupos de Azure AD.
   - Por Configuration Manager, seleccionará colecciones de Configuration Manager que haya sincronizado con el centro de administración de Microsoft Endpoint Manager y habilitado para la directiva de ATP de Microsoft Defender.

   En este momento, puede elegir no asignar grupos o colecciones y editar después la directiva para agregar una asignación.

   Cuando esté listo para continuar, seleccione **Siguiente**.

9. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**.

   El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

## <a name="edr-policy-reports"></a>Informes de directivas de EDR

Puede ver los detalles de las directivas de EDR que implemente en el centro de administración de Microsoft Endpoint Manager. Para ver los detalles, vaya a **Seguridad de los puntos de conexión** > **Implementación y respuesta de puntos de conexión**, y seleccione una directiva para la que quiera ver los detalles de cumplimiento:

- En el caso de las directivas que tienen como destino la plataforma **Windows 10 y versiones posteriores** (Intune), verá información general del cumplimiento de la directiva. También puede seleccionar el gráfico para ver una lista de los dispositivos que han recibido la directiva y profundizar en dispositivos individuales para obtener más detalles.

  En el gráfico **Dispositivos con sensor ATP** solo se muestran los dispositivos que se incorporan correctamente a ATP de Microsoft Defender mediante el uso del perfil **Windows 10 y versiones posteriores**. Para asegurarse de que tiene una representación completa de los dispositivos en este gráfico, implemente el perfil de incorporación en todos los dispositivos. Los dispositivos que se incorporan a ATP de Microsoft Defender por medios externos, como la directiva de grupo o PowerShell, se cuentan como **Dispositivos sin el sensor ATP**.

- En el caso de las directivas que tienen como destino la plataforma **Windows 10 y Windows Server** (Configuration Manager), verá información general sobre el cumplimiento de la directiva, pero no puede profundizar para ver detalles adicionales. La vista está limitada porque el centro de administración recibe detalles de estado limitados de Configuration Manager, que administra la implementación de la directiva en los dispositivos de Configuration Manager.


[Vea las opciones](endpoint-security-edr-profile-settings.md) que puede configurar para plataformas y perfiles.

## <a name="next-steps"></a>Pasos siguientes

- [Configuración de directivas de seguridad de puntos de conexión](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Obtenga más información sobre [detección de puntos de conexión y respuesta](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) en la documentación de ATP de Microsoft Defender.
