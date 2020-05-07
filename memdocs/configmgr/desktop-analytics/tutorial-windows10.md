---
title: 'Tutorial: Implementación de Windows 10'
titleSuffix: Configuration Manager
description: Un tutorial sobre el uso de Análisis de escritorio y Configuration Manager para implementar Windows 10 en un grupo piloto.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2456f530444fa5d9514247edd77cbe7b02f62c38
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126014"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutorial: Implementación de Windows 10 en el piloto

En este tutorial se usa Análisis de escritorio y Configuration Manager para implementar Windows 10 en un grupo piloto. Resalta la integración del servicio en la nube para proporcionar información sobre la implementación de Windows con el producto local. Use Análisis de escritorio para determinar cuáles son los mejores dispositivos para colocar en un grupo piloto. A continuación, use Configuration Manager para mantenerse actualizado con Windows.

En este tutorial, aprenderá a:  

> [!div class="checklist"]  
> * Configurar Análisis de escritorio en Azure Portal  
> * Conectar Configuration Manager y configurar las opciones del dispositivo  
> * Crear un plan de implementación de Análisis de escritorio para Windows 10  
> * Usar Configuration Manager para implementar Windows 10 en el grupo piloto  

Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free) antes de empezar. Cuando se configura correctamente, el uso de Análisis de escritorio no implica ningún costo de Azure.

Análisis de escritorio usa un *área de trabajo de Log Analytics* en su suscripción de Azure. Un área de trabajo es básicamente un contenedor que incluye información de la cuenta e información de configuración sencilla para la cuenta. Para más información, vea [Administración del acceso a los datos de registro y las áreas de trabajo](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Requisitos previos

Antes de empezar este tutorial, asegúrese de que se cumplen los siguientes requisitos previos:  

- Una suscripción de Azure activa, con permisos de [**administrador global**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions).  

    Para obtener más información, consulte [Requisitos previos de Análisis de escritorio](overview.md#prerequisites).

- Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571), o posterior, con el rol **Administrador total**.  

- Soporte de instalación para la versión más reciente de Windows 10.

- Al menos un dispositivo Windows 10 con las siguientes configuraciones:  

    - Windows 10, versión 1709 o posterior, pero inferior a la versión del soporte de instalación que piensa usar.

    - La actualización acumulativa más reciente de Windows 10.  

    - Cliente de Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571), o posterior.  

- Aprobación empresarial para configurar el nivel de datos de diagnóstico de Windows en **Mejorado (limitado)** en los dispositivos piloto.  

    Para más información, consulte [Privacidad de Análisis de escritorio](privacy.md).

- Conectividad de red desde el dispositivo a los siguientes puntos de conexión de Internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (solo en el rol de servidor de Configuration Manager)
    - `https://*.manage.microsoft.com` (solo en el rol de servidor de Configuration Manager)

    Para obtener más información, consulte [Habilitación del uso compartido de datos en Análisis de escritorio](enable-data-sharing.md#endpoints).  

> [!Important]  
> Estos requisitos previos son para los fines de este tutorial. Para obtener más información sobre los requisitos previos generales para usar Análisis de escritorio con Configuration Manager, consulte [Requisitos previos](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configuración del análisis de escritorio

Use este procedimiento para iniciar sesión en Análisis de escritorio y configurarlo en su suscripción. Este es un procedimiento único para configurar Análisis de escritorio para su organización.  

1. Abra el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) en Administración de dispositivos de Microsoft 365 con un usuario que tenga permisos de **administrador global**. Seleccione **Inicio**.  

2. En la página **Aceptar el acuerdo de servicio**, revise el acuerdo de servicio y seleccione **Aceptar**.  

3. En la página **Confirmar la suscripción**, la lista de licencias requeridas se aplica a las características de mantenimiento de dispositivos de Windows de Análisis de escritorio. Seleccione **Siguiente** para continuar.  

4. En la página para **permitir el acceso de los usuarios**:

    - **Permita que Análisis de escritorio administre los roles de directorio en su nombre**: Análisis de escritorio asigna automáticamente a los **propietarios del área de trabajo** el rol de **administrador de Análisis de escritorio**. Si esos grupos ya son **administradores globales**, no se producirá ningún cambio.  

        Aunque no seleccione esta opción, Análisis de escritorio agregará usuarios como miembros del grupo de seguridad. Un **administrador global** debe asignar manualmente el rol de **administrador de Análisis de escritorio** para los usuarios.  

        Para obtener más información sobre la asignación de permisos de rol de administrador en Azure Active Directory y los permisos asignados a **administradores de Análisis de escritorio**, consulte [Permisos de roles de administrador en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análisis de escritorio preconfigura el grupo de seguridad de **propietarios del área de trabajo** en Azure Active Directory para crear y administrar áreas de trabajo y planes de implementación. 

        Para agregar un usuario al grupo, escriba su nombre o dirección de correo electrónico en la sección **Escriba un nombre o una dirección de correo electrónico**. Cuando termine, seleccione **Siguiente**.

5. En la página **Configurar el área de trabajo**:  

    > [!Note]  
    > Para completar este paso, el usuario necesita permisos de **propietario del área de trabajo** y acceso adicional a la suscripción y al grupo de recursos de Azure. Para más información, consulte los [requisitos previos](overview.md#prerequisites).  

    - Seleccione la suscripción a Azure.  

    - Para usar un área de trabajo existente para Análisis de escritorio, selecciónela y continúe con el siguiente paso.  

    - Para crear un área de trabajo para Análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre del área de trabajo**.  

        2. Seleccione la lista desplegable para **seleccionar el nombre de la suscripción de Azure para esta área de trabajo** y elija la suscripción de Azure para esta área de trabajo.  

        3. **Cree un nuevo** grupo de recursos o **use uno existente**.  

        4. Seleccione la **región** en la lista y, a continuación, seleccione **Agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **Set as Desktop Analytics workspace** (Establecer como área de trabajo de Análisis de escritorio).  A continuación, seleccione **Continuar** en el cuadro de diálogo **Confirmar y conceder acceso**.  

7. En la pestaña del nuevo explorador, seleccione una cuenta para iniciar sesión. Seleccione la opción **Consentimiento en nombre de la organización** y seleccione **Aceptar**.  


    > [!Note]  
    > Este consentimiento es para asignar a la aplicación MALogAnalyticsReader el rol de lector Log Analytics para el área de trabajo. Análisis de escritorio requiere este rol de aplicación. Para obtener más información, consulte [Rol de aplicación MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. De vuelta en la página **Configurar el área de trabajo**, seleccione **Siguiente**.  

9. En la página **Últimos pasos**, seleccione **Ir a Análisis de escritorio**. Azure Portal muestra la página **Inicio** de Análisis de escritorio.  



## <a name="connect-configuration-manager"></a>Conexión de Configuration Manager

Use este procedimiento para actualizar Configuration Manager, conectarlo a Análisis de escritorio y configurar los valores del dispositivo. Este procedimiento se realiza una sola vez para asociar la jerarquía al servicio en la nube.  

### <a name="update-configuration-manager"></a>Actualizar Configuration Manager

Instale el paquete acumulativo de actualizaciones de la versión 1902 (4500571) de Configuration Manager para admitir la integración con Análisis de escritorio. Para más información sobre esta actualización, consulte [Paquete acumulativo de la rama actual de Configuration Manager, versión 1902](https://support.microsoft.com/help/4500571).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](../core/servers/manage/install-in-console-updates.md).  

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Conexión al servicio

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **Configurar servicios de Azure** en la cinta de opciones.  

2. En la página **Servicios de Azure** del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **Nombre** para el objeto en Configuration Manager.  

    - Especifique una **Descripción** opcional para ayudar a identificar el servicio.  

    - Seleccione **Análisis de escritorio** en la lista de servicios disponibles.  
  
   Seleccione **Siguiente**.  

3. En la página **Aplicación**, seleccione el **entorno de Azure** adecuado. Luego, seleccione **Examinar** para la aplicación web.

4. Seleccione **Crear** para agregar fácilmente una aplicación Azure AD para la conexión de Análisis de escritorio.

5. En la ventana **Crear aplicación de servidor**, configure las siguientes opciones:  

    - **Nombre de aplicación**: un nombre descriptivo para la aplicación en Azure AD.

    - **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. Se encuentra en el token de acceso que usa el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **Período de validez de clave secreta**: elija **1 año** o **2 años** en la lista desplegable. El valor predeterminado es un año.  

    Haga clic en **Iniciar sesión**. Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.

    > [!Note]  
    > Complete este paso como **administrador global**. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure.  

    Haga clic en **Aceptar** para crear la aplicación web en Azure AD y cerrar el cuadro de diálogo Crear aplicación de servidor. En el cuadro de diálogo Aplicación de servidor, seleccione **Aceptar**. A continuación, seleccione **Siguiente** en la página Aplicación del Asistente para servicios de Azure.  

6. En la página **Datos de diagnóstico**, configure las siguientes opciones:  

    - **Id. comercial**: este valor se debe rellenar automáticamente con el identificador de la organización.  

    - **Nivel de datos de diagnóstico de Windows 10**: seleccione al menos **Mejorado (limitado)** .  

    - **Permitir nombre del dispositivo en los datos de diagnóstico**: seleccione **Habilitar**.  
  
   Seleccione **Siguiente**. En la página **Funcionalidad disponible** se muestra la funcionalidad de Análisis de escritorio que está disponible con la configuración de datos de diagnóstico de la página anterior. Seleccione **Siguiente**.  

7. En la página **Recopilaciones**, configure las siguientes opciones:  

    - **Nombre para mostrar**: el portal de Análisis de escritorio muestra esta conexión de Configuration Manager con este nombre. Úselo para diferenciar entre distintas jerarquías. Por ejemplo, *laboratorio de prueba* o *producción*.  

    - **Recopilación de destino**: esta recopilación incluye todos los dispositivos que configura Configuration Manager con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que conecta Configuration Manager al servicio Análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usan un proxy autenticado por el usuario para las comunicaciones salientes**: de forma predeterminada, este valor es **No**. Si es necesario en su entorno, establézcalo en **Sí**.  

    - **Seleccione recopilaciones específicas para sincronizarlas con Análisis de escritorio**: seleccione **Agregar** para incluir colecciones adicionales. Estas recopilaciones están disponibles en el portal de Análisis de escritorio para agruparlas con los planes de implementación. Asegúrese de incluir recopilaciones piloto y de exclusión piloto.  

        Estas recopilaciones se siguen sincronizando a medida que cambia su pertenencia. Por ejemplo, el plan de implementación usa una recopilación con una regla de pertenencia de Windows 7. A medida que esos dispositivos se actualizan a Windows 10 y Configuration Manager evalúa la pertenencia de la recopilación, dichos dispositivos abandonan la colección y el plan de implementación.  

8. Complete el asistente.  

Configuration Manager crea una directiva de configuración para configurar los dispositivos de la recopilación de destino. Esta directiva incluye la configuración de datos de diagnóstico para permitir que los dispositivos envíen datos a Microsoft. De forma predeterminada, los clientes actualizan la directiva cada hora. Después de recibir la nueva configuración, pueden pasar varias horas antes de que los datos estén disponibles en Análisis de escritorio.

> [!Note]  
> Para obtener más información acerca de estos valores de configuración, consulte [Configuración de Windows](enroll-devices.md#windows-settings).  

Supervise la configuración de los dispositivos de Análisis de escritorio. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda el nodo **Servicio de Análisis de escritorio** y seleccione el panel **Mantenimiento de la conexión**.  

Configuration Manager sincroniza las recopilaciones en los 60 minutos siguientes a la creación de la conexión. En el portal de Análisis de escritorio, vaya a **Piloto global** y vea las recopilaciones de dispositivos de Configuration Manager. El resto del portal puede tardar entre dos y tres días en mostrar datos completos. Para más información, consulte [Latencia de datos](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Crear un plan de implementación de Análisis de escritorio

Use este procedimiento para crear un plan de implementación en Análisis de escritorio.

1. Abra el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics). Use credenciales que tengan al menos permisos de **colaboradores del área de trabajo**.  

2. Seleccione **Planes de implementación** en el grupo Administrar.  

3. En el panel **Planes de implementación**, seleccione **Crear**.  

4. En el panel **Crear plan de implementación**, configure las siguientes opciones:  

    - **Nombre**: un nombre exclusivo para el plan de implementación, como `Windows 10 pilot`.  

    - **Productos y versiones**: seleccione el producto de **Windows** y la versión recomendada más reciente disponible. Por ejemplo, **Windows 10, versión 1809 (recomendado)** .  

    - **Grupos de dispositivos**: seleccione uno o varios grupos en la pestaña Configuration Manager y, a continuación, seleccione **Establecer como grupos de objetivo**. Estos grupos son recopilaciones sincronizadas desde Configuration Manager.  

    - **Reglas de preparación**: estas reglas ayudan a determinar qué dispositivos son aptos para la actualización. Seleccione **SO Windows** y configure las siguientes opciones:  

        - **Mis equipos obtienen automáticamente los controladores desde Windows Update**: la configuración predeterminada es **Desactivado**, que se recomienda al implementar con Configuration Manager.  

        - **Defina un umbral de recuento de instalación bajo para sus aplicaciones**: el valor predeterminado es `2%`. Las aplicaciones por debajo de este umbral se establecen automáticamente en *Recuento de instalaciones bajo*. Análisis de escritorio no valida estos complementos durante el piloto.  

            Si una aplicación se instala en un porcentaje superior de equipos a este umbral, el plan de implementación marca la aplicación como *Destacada*. Luego, puede decidir su importancia para probarla durante la fase piloto.  

    - **Fecha de finalización**: elija la fecha en que Windows debe implementarse completamente en todos los dispositivos de destino.  

5. Seleccione **Crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Para acelerar este proceso, solicite una actualización de datos a petición. Para más información, consulte [Preguntas frecuentes sobre Análisis de escritorio](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Abra el plan de implementación seleccionando su nombre.  

7. En el menú del plan de implementación, en el grupo **Preparar**, seleccione **Identificar importancia**.  

    1. En la pestaña **Aplicaciones**, seleccione que se muestren solo los recursos **no revisados**.  

    2. Seleccione cada aplicación y, a continuación, seleccione **Editar**. Puede seleccionar más de una aplicación para editarla al mismo tiempo.  

    3. Elija un nivel de importancia en la lista **Importancia**. Si quiere que Análisis de escritorio valide la aplicación durante la prueba piloto, seleccione **Crítico** o **Importante**. No valida las aplicaciones marcadas como **No importante**. Evalúe su [compatibilidad](compat-assessment.md) y otra información del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Haga clic en **Guardar** cuando haya terminado.  

8. En el menú del plan de implementación, en el grupo **Preparar**, seleccione **Identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **Agregar a piloto**. Si no está de acuerdo con la recomendación, seleccione **Reemplazar**.  

        Para obtener más información sobre cómo realiza estas recomendaciones Análisis de escritorio, seleccione el icono de información en la esquina superior derecha del panel **Identificar piloto**.



## <a name="deploy-windows-10-in-configuration-manager"></a>Implementación de Windows 10 en Configuration Manager

Use este procedimiento para implementar Windows 10 en Configuration Manager en el grupo piloto.

- Si aún no tiene uno, primero [cree un paquete de actualización del sistema operativo para Windows 10](#bkmk_create-package).  

- Si aún no tiene una, [cree una secuencia de tareas de actualización del sistema operativo para Windows 10](#bkmk_create-ts).  

- [Implemente la secuencia de tareas](#bkmk_deploy-ts) mediante el plan de implementación de Análisis de escritorio.  

- [Instale la secuencia de tareas](#bkmk_install-ts) desde el Centro de Software en un dispositivo de destino.  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> Creación de un paquete de actualización del sistema operativo para Windows 10

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Paquetes de actualización del sistema operativo**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Agregar paquete de actualización de sistema operativo**. Esta acción inicia el asistente para agregar una actualización del sistema operativo.  

3. En la página **Origen de datos**, especifique la **ruta de acceso** de red a los archivos de origen de instalación del paquete de actualización de sistema operativo. Por ejemplo, `\\server\share\path`.  

    > [!NOTE]  
    > Los archivos de origen de instalación contienen setup.exe y otros archivos y carpetas para instalar el sistema operativo.  

4. En la página **General**, especifique un **nombre** único para el paquete de actualización del sistema operativo.  

5. Complete el Asistente para agregar paquete de actualización de sistema operativo.  

#### <a name="distribute-content"></a>Distribución de contenido

A continuación, distribuya el paquete de actualización del sistema operativo a puntos de distribución.  

1. Seleccione el paquete de actualización del sistema operativo en la lista. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Distribuir contenido**. Se abre el Asistente para distribuir contenido.  

2. En la página **General**, compruebe que el contenido que aparece es el contenido que desea distribuir y, a continuación, haga clic en **Siguiente**.  

3. En la página **Destino del contenido**, elija **Agregar** y seleccione el **punto de distribución**. Seleccione un punto de distribución existente y, después, haga clic en **Aceptar**. Cuando termine de agregar los destinos del contenido, haga clic en **Siguiente**.  

4. Complete el Asistente para distribuir contenido.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a> Creación de una secuencia de tareas de actualización de SO para Windows 10

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear secuencia de tareas**.  

3. En la página **Crear nueva secuencia de tareas** del Asistente para creación de secuencia de tareas, seleccione **Actualizar un sistema operativo desde un paquete de actualización** y luego elija **Siguiente**.  

4. En la página **Información de secuencia de tareas**, especifique un **nombre para la secuencia de tareas** que identifique la secuencia de tareas.  

5. En la página **Actualizar el sistema operativo de Windows**, especifique la siguiente configuración y luego haga clic en **Siguiente**:  

    - **Paquete de actualización**: especifique el paquete de actualización que contenga los archivos de origen de actualización del sistema operativo.  

    - **Índice de ediciones**: si hay varios índices de edición del sistema operativo disponibles en el paquete, seleccione el índice de la edición deseada. De forma predeterminada, el asistente selecciona el primer índice.  

    - **Clave de producto**: especifique la clave de producto de Windows para el sistema operativo que quiera instalar. Puede especificar claves de licencia por volumen codificadas o claves de producto estándar. Si usa una clave de producto estándar, separe cada grupo de cinco caracteres por un guion (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Si se trata de una actualización de una edición de licencia por volumen, la clave de producto puede no ser necesaria.  

        > [!Note]  
        > Esta clave de producto puede ser una clave de activación múltiple (CAM) o una clave de licencias por volumen genérica (CLVG). Las CLVG también se conocen como claves de configuración de cliente del servicio de administración de claves (SAC). Para obtener más información, consulte [Plan para la activación por volumen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obtener una lista de claves de configuración de cliente KMS, consulte el [Apéndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) de la Guía de activación de Windows Server.

6. En la página **Incluir actualizaciones**, seleccione **Siguiente** para no instalar ninguna actualización de software.  

7. En la página **Instalar aplicaciones**, seleccione **Siguiente** para no instalar ninguna aplicación.

8. Complete el Asistente para crear secuencia de tareas.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> Implementación de secuencia de tareas mediante el plan de implementación de Análisis de escritorio.

1. En la consola de Configuration Manager, vaya a **Biblioteca de software**, expanda **Servicio Análisis de escritorio** y seleccione el nodo **Planes de implementación**.  

2. Seleccione el plan de implementación de Windows 10 y, luego, seleccione **Detalles del plan de implementación** en la cinta de opciones.  

3. En el icono **Estado piloto**, elija **Secuencia de tareas** en la lista desplegable y, a continuación, seleccione **Implementar**.  

4. En la página **General** del Asistente para implementar software, seleccione **Examinar** junto al campo **Software**. Seleccione la secuencia de tareas de la actualización local de Windows 10 y seleccione **Siguiente**.  

    > [!Note]  
    > Con la integración de Análisis de escritorio, Configuration Manager crea automáticamente recopilaciones piloto y de producción para el plan de implementación. Antes de poder usarlas, puede que estas recopilaciones tarden en sincronizarse. Para más información, consulte [Solución de problemas: latencia de datos](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Esta recopilación está reservada para los dispositivos del plan de implementación de Análisis de escritorio. No se admiten cambios manuales en esta recopilación.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. En la página **Contenido**, seleccione **Agregar** y luego elija el **punto de distribución**. Seleccione un punto de distribución disponible para hospedar el contenido de instalación y seleccione **Aceptar**. A continuación, seleccione **Siguiente**.  

6. En la página **Configuración de la implementación**, seleccione **Siguiente** para aceptar la configuración predeterminada. (Una instalación disponible).  

7. En la página **Programación**, seleccione **Siguiente** para aceptar la configuración predeterminada. (Disponible lo antes posible).  

8. En la página **Experiencia del usuario**, elija **Siguiente** para aceptar los valores predeterminados. (Mostrar en el Centro de software y mostrar solo las notificaciones para reinicios del sistema).  

9. En la página **Alertas**, elija **Siguiente** para aceptar los valores predeterminados.  

10. Complete el asistente.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> Instalación de la secuencia de tareas desde el Centro de software

1. Inicie sesión en un dispositivo que forme parte del plan de implementación piloto.  

2. Abra **Centro de software** e instale el sistema operativo disponible para Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para obtener más información sobre los planes de implementación de Análisis de escritorio.
> [!div class="nextstepaction"]  
> [Planes de implementación](about-deployment-plans.md)
