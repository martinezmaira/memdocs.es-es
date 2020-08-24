---
title: Conexión de Configuration Manager
titleSuffix: Configuration Manager
description: Guía de procedimientos para conectar Configuration Manager con Análisis de escritorio.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7015ab4c180ed56b00149ffbff99c9e5a8112e95
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126008"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Conexión de Configuration Manager con Análisis de escritorio

Análisis de escritorio está fuertemente integrado con Configuration Manager. En primer lugar, asegúrese de que el sitio está actualizado para admitir las características más recientes. A continuación, cree la conexión de Análisis de escritorio en Configuration Manager. Por último, supervise el estado de la conexión.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a> Actualización del sitio

En primer lugar, asegúrese de que el sitio de Configuration Manager ejecute al menos la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](../core/servers/manage/install-in-console-updates.md).

También debe instalar el paquete acumulativo de actualizaciones de la versión 1902 (4500571) para admitir la integración con Análisis de escritorio. Para más información sobre esta actualización, consulte [Paquete acumulativo de la rama actual de Configuration Manager, versión 1902](https://support.microsoft.com/help/4500571).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](../core/servers/manage/install-in-console-updates.md).

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a> Conexión al servicio

> [!TIP]
> Antes de iniciar el asistente, cree la colección de destino mencionada en el paso 8, ya que no la podrá seleccionar fuera del asistente una vez que lo haya iniciado.

Use este procedimiento para conectar Configuration Manager a Análisis de escritorio y configurar los valores del dispositivo. Este procedimiento es un proceso de una sola vez para asociar la jerarquía al servicio en la nube.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **Configurar servicios de Azure** en la cinta de opciones.

    > [!TIP]
    > Conéctese al servicio directamente desde el nodo **Servicio Análisis de escritorio**. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y seleccione el nodo **Servicio Análisis de escritorio**. En el cuadro *¿Es nuevo en Análisis de escritorio?* , seleccione el segundo vinculo a *Conectar Configuration Manager con el servicio Análisis de escritorio*.

2. En la página **Servicios de Azure** del Asistente para servicios de Azure, configure las siguientes opciones:

    - Especifique un **Nombre** para el objeto en Configuration Manager.

    - Especifique una **Descripción** opcional para ayudar a identificar el servicio.

    - Seleccione **Análisis de escritorio** en la lista de servicios disponibles.

   Seleccione **Siguiente**.

3. En la página **Aplicación**, seleccione el **entorno de Azure** adecuado. Luego, seleccione **Examinar** para la aplicación web.

4. Si tiene una aplicación que quiere reutilizar para este servicio, elíjala de la lista y seleccione **Aceptar**.

5. En la mayoría de los casos, puede crear una aplicación para la conexión de Análisis de escritorio con este asistente. Seleccione **Crear**.<!-- 3572123 -->

    > [!TIP]
    > Si no puede crear la aplicación desde este asistente, puede hacerlo manualmente en Azure AD y, luego, importarla en Configuration Manager. Para más información, consulte [Creación e importación de una aplicación para Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. En la ventana **Crear aplicación de servidor**, configure las siguientes opciones:

    - **Nombre de aplicación**: un nombre descriptivo para la aplicación en Azure AD.

    - **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.

    - **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. Se encuentra en el token de acceso que usa el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.

    - **Período de validez de clave secreta**: elija **1 año** o **2 años** en la lista desplegable. El valor predeterminado es un año.

    Seleccione **Iniciar sesión**. Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.

    > [!NOTE]
    > Complete este paso como **administrador global**. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure.

    Haga clic en **Aceptar** para crear la aplicación web en Azure AD y cerrar el cuadro de diálogo Crear aplicación de servidor. En el cuadro de diálogo Aplicación de servidor, seleccione **Aceptar**. A continuación, seleccione **Siguiente** en la página Aplicación del Asistente para servicios de Azure.

7. En la página **Datos de diagnóstico**, configure las siguientes opciones:

    - **Id. comercial**: este valor se debe rellenar automáticamente con el identificador de la organización. Si no es así, asegúrese de que el servidor proxy esté configurado para permitir todos los [puntos de conexión](enable-data-sharing.md#endpoints) necesarios antes de continuar. También puede recuperar el identificador comercial manualmente desde el [portal de Análisis de escritorio](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Nivel de datos de diagnóstico de Windows 10**: seleccione al menos **Requerido**. para más información, consulte [Niveles de datos de diagnóstico](enable-data-sharing.md#diagnostic-data-levels).

        > [!TIP]
        > En Configuration Manager versión 2002 y versiones anteriores, este valor se llamaba **Básico**.<!-- 7363467 -->

    - **Permitir nombre del dispositivo en los datos de diagnóstico**: seleccione **Habilitar**.

        > [!NOTE]
        > A partir de la versión 1803 de Windows 10, el nombre del dispositivo no se envía a Microsoft de forma predeterminada. Si no envía el nombre del dispositivo, aparece en Análisis de escritorio como "desconocido". Este comportamiento puede dificultar la identificación y la evaluación de los dispositivos.

   Seleccione **Siguiente**. En la página **Funcionalidad disponible** se muestra la funcionalidad de Análisis de escritorio que está disponible con la configuración de datos de diagnóstico de la página anterior. Seleccione **Siguiente** para continuar o **Anterior** para realizar cambios.

    ![Ejemplo de la página Funcionalidad disponible en el Asistente para servicios de Azure](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. En la página **Recopilaciones**, configure las siguientes opciones:

    - **Nombre para mostrar**: el portal de Análisis de escritorio muestra esta conexión de Configuration Manager con este nombre. Úselo para diferenciar entre diferentes jerarquías e identificar colecciones de jerarquías independientes. Use los términos para distinguir fácilmente varias jerarquías en su entorno, por ejemplo: *laboratorio de pruebas* o de *producción*.

    - **Recopilación de destino**: esta recopilación incluye todos los dispositivos que configura Configuration Manager con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que conecta Configuration Manager al servicio Análisis de escritorio.

    - **Los dispositivos de la recopilación de destino usan un proxy autenticado por el usuario para las comunicaciones salientes**: de forma predeterminada, este valor es **No**. Si es necesario en su entorno, establézcalo en **Sí**.

    - **Seleccione recopilaciones específicas para sincronizarlas con Análisis de escritorio**: seleccione **Agregar** para incluir recopilaciones adicionales de la jerarquía **Recopilación de destino**. Estas recopilaciones están disponibles en el portal de Análisis de escritorio para agruparlas con los planes de implementación. Asegúrese de incluir recopilaciones piloto y de exclusión piloto.  <!-- 4097528 -->

        > [!TIP]
        > La ventana Seleccionar recopilaciones muestra solo las recopilaciones que están limitadas por la **recopilación de destino**.
        >
        > En el ejemplo siguiente, se selecciona RecopilaciónA como recopilación de destino. Luego, verá RecopilaciónA, RecopilaciónB y RecopilaciónC al agregar más recopilaciones. No puede agregar RecopilaciónD.
        >
        > - RecopilaciónA: está limitada por la recopilación **Todos los sistemas**
        >     - RecopilaciónB: está limitada por la RecopilaciónA.
        >         - RecopilaciónC: está limitada por la RecopilaciónB.
        > - RecopilaciónD: está limitada por la recopilación **Todos los sistemas**
        >
        > Para administrar las colecciones disponibles en el portal Análisis de escritorio para agrupar con planes de implementación, en la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Servicios de Azure**. Seleccione la entrada asociada al servicio de Azure **Análisis de escritorio** y actualice la configuración en la página **Desktop Analytics Collection** (Colección de Análisis de escritorio).

        > [!IMPORTANT]
        > Estas recopilaciones se siguen sincronizando a medida que cambia su pertenencia. Por ejemplo, la colección de destino usa una recopilación con una regla de pertenencia de Windows 7. A medida que esos dispositivos se actualizan a Windows 10 y Configuration Manager evalúa la pertenencia de la recopilación, dichos dispositivos abandonan la recopilación y Análisis de escritorio.

9. Complete el asistente.

Configuration Manager crea una directiva de configuración para configurar los dispositivos de la recopilación de destino. Esta directiva incluye la configuración de datos de diagnóstico para permitir que los dispositivos envíen datos a Microsoft. De forma predeterminada, los clientes actualizan la directiva cada hora. Después de recibir la nueva configuración, pueden pasar varias horas antes de que los datos estén disponibles en Análisis de escritorio.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a> Supervisión del estado de la conexión

Supervise la configuración de los dispositivos de Análisis de escritorio. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda el nodo **Servicio de Análisis de escritorio** y seleccione el panel **Mantenimiento de la conexión**.

Para más información, consulte [Supervisión del estado de conexión](monitor-connection-health.md).

Configuration Manager sincroniza las recopilaciones en los 60 minutos siguientes a la creación de la conexión. En el portal de Análisis de escritorio, vaya a **Piloto global** y consulte las recopilaciones de dispositivos de Configuration Manager.

> [!NOTE]
> La conexión de Configuration Manager con Análisis de escritorio se basa en el punto de conexión de servicio. Cualquier cambio que se realice en este rol de sistema de sitio pueden afectar a la sincronización con el servicio en la nube. Para obtener más información, consulte [About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move) (Sobre el punto de conexión del servicio).

## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para inscribir los dispositivos en Análisis de escritorio.
> [!div class="nextstepaction"]
> [Inscripción de dispositivos](enroll-devices.md)
