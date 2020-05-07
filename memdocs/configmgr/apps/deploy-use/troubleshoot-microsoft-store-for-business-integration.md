---
title: Solución de problemas de integración de MSfB
titleSuffix: Configuration Manager
description: Proporciona sugerencias para solucionar algunos de los problemas más comunes con la integración de Microsoft Store para Empresas y Educación.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149109"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Solución de problemas de integración de Microsoft Store para Empresas y Educación con Configuration Manager

En este artículo se proporcionan sugerencias y correcciones de solución de problemas para algunos de los principales problemas que puede tener con la integración de Microsoft Store para Empresas y Educación (MSfB) con Configuration Manager.

Para obtener más información sobre el uso de Microsoft Store para Empresas y Educación con Configuration Manager, vea [Administración de aplicaciones desde Microsoft Store para Empresas y Educación con Configuration Manager](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>Supervisión

### <a name="component-status"></a>Estado del componente

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y haga clic en el nodo **Estado del componente**. Supervise el estado de los siguientes componentes:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Estado de sincronización

En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**. Compruebe la columna **Último estado de sincronización**.

### <a name="view-synchronized-apps"></a>Visualización de aplicaciones sincronizadas

En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Información de licencia para las aplicaciones de la Tienda**.


## <a name="log-files"></a>Archivos de registro

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

Este archivo de registro se encuentra en el punto de conexión de servicio, en `\Logs` en el directorio de instalación de Configuration Manager. Registra información sobre la comunicación con el servicio en la nube. Esta información incluye metadatos, iconos, paquetes y recuperación del archivo de licencia.

Para cambiar el nivel de registro, cambie el valor `LoggingLevel` a `0` en la clave del Registro `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION`. Para obtener más información, vea [Configuración de opciones de registro](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

Este archivo de registro se encuentra en el punto de conexión de servicio, en `\Logs` en el directorio de instalación de Configuration Manager. Si el servicio WSfBSyncWorker no se inicia, o bien se inicia y se detiene repetidamente, revise las entradas de este archivo de registro.

> [!NOTE]
> Este archivo de registro se comparte con otras características.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

Este archivo de registro se encuentra en el servidor de sitio para el sitio de nivel superior de la jerarquía. Se encuentra en `\Logs` en el directorio de instalación de Configuration Manager. Registra información sobre los procesos siguientes:

- Inserción de la información de metadatos sincronizada por el componente BusinessAppProcessWorker en la base de datos
- Procesamiento de archivos en `\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log

Este archivo de registro se encuentra en el servidor de sitio para el sitio de nivel superior de la jerarquía. Se encuentra en `\Logs` en el directorio de instalación de Configuration Manager. Si el servicio BusinessAppProcessWorker no se inicia, o bien se inicia y se detiene repetidamente, revise las entradas de este archivo de registro.



## <a name="last-sync-failed"></a>Error de la última sincronización

Cuando el último estado de sincronización es *con error*, empiece por revisar los siguientes [archivos de registro](#log-files) para identificar el síntoma:

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Después, examine una de las secciones siguientes para ver los problemas comunes:

- [Error de autorización](#bkmk_fail-symptom1)
- [La clave secreta no es válida](#bkmk_fail-symptom2)
- [Error al obtener el token de aplicación](#bkmk_fail-symptom3)
- [La ubicación del contenido no existe o tiene permisos incorrectos](#bkmk_fail-symptom4)
- [Error al hacer que la solicitud HTTP llame al método "GET"](#bkmk_fail-symptom5)
- [No se pueden escribir más bytes en el búfer](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a> Error de autorización

#### <a name="cause"></a>Causa

Este problema se puede producir si la aplicación Azure Active Directory (Azure AD) configurada no tiene permisos para administrar Microsoft Store para Empresas y Educación para este inquilino.

#### <a name="workaround"></a>Solución alternativa

1. Inicie sesión como administrador en el portal de Microsoft Store para Empresas o Educación.
1. Vaya a **Configuración** y seleccione **Herramientas de administración**.
1. Si la aplicación no aparece en la lista, seleccione **Agregar una herramienta de administración**. Después, busque por nombre y seleccione la aplicación Azure AD asociada con el mismo id. de cliente que Configuration Manager.
1. Si el estado no se muestra como **Activo**, seleccione **Activar** en la sección **Acción**.
1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**. Realice la sincronización con la tienda, o bien espere a que se produzca el siguiente intervalo de sincronización.

> [!Tip]
> Para buscar el valor ClientID en Configuration Manager:
>
> 1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Inquilinos de Azure Active Directory**.
> 1. Seleccione el inquilino que use para la integración de Microsoft Store para Empresas y Educación.
> 1. En el panel de resultados, busque la aplicación coincidente y examine la columna **Id. de cliente**.

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a> La clave secreta no es válida

#### <a name="cause"></a>Causa

Este problema se puede producir si la clave secreta ha expirado en la aplicación Azure AD para la configuración de Microsoft Store para Empresas y Educación.

#### <a name="resolution"></a>Solución

Renueve la clave secreta de la aplicación Azure AD. Para más información, vea [Renovar clave secreta](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a> Error al obtener el token de aplicación

#### <a name="cause"></a>Causa

Este problema se puede producir si la aplicación conectada ya no existe en Azure AD.

#### <a name="resolution"></a>Solución

Elimine y vuelva a crear la conexión a Microsoft Store para Empresas y Educación.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**.
1. Seleccione la conexión existente.
1. Seleccione **Eliminar** en la cinta.

A continuación, vuelva a crear la conexión. Vea los siguientes artículos para más información:

- [Configuración de los Servicios de Azure](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Configuración de la sincronización de Microsoft Store para Empresas y Educación](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a> La ubicación del contenido no existe o tiene permisos incorrectos

#### <a name="cause"></a>Causa

Al configurar la conexión a Microsoft Store para Empresas y Educación, se especifica un recurso compartido de red para almacenar el contenido sincronizado. Este problema se puede producir si este recurso compartido no existe o tiene permisos incorrectos. La cuenta de equipo para el punto de conexión de servicio debe ser el propietario de este directorio y todos los subdirectorios.<!-- memdocs#146 --> Si no es así, verá un error similar al siguiente:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Para ver la ubicación que ha configurado:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**.

1. Seleccione la cuenta y abra sus **Propiedades**.

1. Cambie a la pestaña **Configuración**. La configuración de **Ubicación** muestra la ruta de acceso de red para almacenar el contenido de la aplicación descargado del Microsoft Store para empresas y educación.

#### <a name="workaround"></a>Solución alternativa

1. Si todavía no existe, cree el recurso compartido.

1. Compruebe los permisos NTFS en la carpeta y los permisos en el recurso compartido de red. Conceda a la cuenta de equipo del punto de conexión de servicio permisos de **Lectura** y **Escritura**.

Si quiere reconfigurar la ubicación, elimine y vuelva a crear la conexión con la nueva ubicación de contenido.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a> Error al hacer que la solicitud HTTP llame al método "GET"

#### <a name="cause"></a>Causa

Este problema se puede producir si la sincronización de aplicaciones desde la tienda ha tardado tanto que la dirección URL del contenido ha expirado.

#### <a name="workaround"></a>Solución alternativa

Vuelva a intentar el proceso de sincronización

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**.
1. Seleccione la de conexión. En la cinta, seleccione **Sincronizar desde Microsoft Store para Empresas**.

Cada vez, debe avanzar más allá. Puede necesitar varios reintentos en función de los factores siguientes:

- El número de aplicaciones sin conexión
- El tamaño de los paquetes
- Velocidad de la red

Con cada intento, debería ver el error menos veces. Si el número de errores no se reduce, hay otro problema.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a> No se pueden escribir más bytes en el búfer

#### <a name="cause"></a>Causa

Este problema se puede producir si el paquete de la aplicación es mayor de 500 MB. Configuration Manager solo admite la sincronización automática de aplicaciones sin conexión con paquetes de menos de 500 MB.

#### <a name="workaround"></a>Solución alternativa

Estas aplicaciones no se pueden sincronizar de forma automática, pero puede descargar el contenido y crear la aplicación manualmente:

1. Obtenga el id. de aplicación con error de la siguiente línea en **WSfbSynWorker.log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Inicie sesión como administrador en el portal de Microsoft Store para Empresas o Educación. Busque la página de esta aplicación.

    > [!Tip]
    > La dirección URL de la página es similar a la siguiente: `https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Seleccione **Sin conexión** si no está ya seleccionado. Después, seleccione **Administrar**.

    1. Cree una carpeta independiente en el recurso compartido de contenido de la aplicación para todas las plataformas compatibles.

    1. Descargue el paquete en la carpeta del paquete.

    1. Descargue el archivo de licencia codificado como un archivo `.bin` en la carpeta del paquete.

    1. Descargue todos los marcos necesarios en la carpeta del paquete.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.

1. [Cree una aplicación](create-applications.md) y especifique manualmente la información de la aplicación.

    1. Cree un tipo de implementación para cada plataforma admitida que haya descargado antes.

    1. Tipo: **Paquete de aplicación de Windows (\*.appx, \*.appxbundle)**

    1. Especifique appx/appxbundle para el paquete de aplicación real, no un paquete de dependencias necesario.

Confirme los detalles siguientes en la última página de **Importar información**:

- **Archivo de licencia:** especifica el archivo `.bin`. Este archivo de licencia es necesario para las aplicaciones sin conexión.
- **Dependencias de aplicaciones de Windows:** compruebe que se han descargado todas las dependencias necesarias para este paquete.


## <a name="sync-doesnt-run"></a>La sincronización no se ejecuta

En esta sección se describen los problemas de sincronización siguientes:

- El proceso de sincronización se inicia manualmente, pero no se ejecuta
- El sitio no se sincroniza automáticamente cada día

Empiece por revisar los siguientes [archivos de registro](#log-files) para identificar el síntoma:

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER. log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Después, examine una de las secciones siguientes para ver los problemas comunes:

- [La sincronización manual no se inicia](#bkmk_sync-symptom1)
- [La sincronización diaria automática no se ejecuta y aparece el error "cerrando # trabajos" en SMS_BUSINESS_APP_PROCESS_MANAGER.log](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a> La sincronización manual no se inicia

#### <a name="cause"></a>Causa

Este problema se puede producir si se inicia una sincronización menos de 10 minutos después de la anterior. No se puede sincronizar con una frecuencia inferior a 10 minutos.

#### <a name="resolution"></a>Solución

Espere al menos 10 minutos antes de iniciar otra sincronización.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a> La sincronización diaria automática no se ejecuta y aparece el error "cerrando # trabajos" en SMS_BUSINESS_APP_PROCESS_MANAGER.log

#### <a name="cause"></a>Causa

Este problema se puede producir si el componente SMS_BUSINESS_APP_PROCESS_MANAGER detiene el subproceso WsfbSyncWorker. El error puede especificar `2` o `4` trabajos.

#### <a name="workaround"></a>Solución alternativa

Reinicie el servicio **SMS_EXECUTIVE**.

Si no puede reiniciar el servicio principal, detenga los dos componentes con trabajos de MSfB y, después, inícielos:

1. Abra el Registro de Windows en el servidor que ejecuta el punto de conexión de servicio.

1. Vaya a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Establezca la operación solicitada en **Detener**.

    1. Actualice para comprobar que Estado actual = **Detenido**.

1. Vaya a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Establezca la operación solicitada en **Detener**.

    1. Actualice para comprobar que Estado actual = **Detenido**.

1. En **SMS_CLOUDCONNECTION**, establezca Operación solicitada en **Iniciar**.

1. En **SMS_BUSINESS_APP_PROCESS_MANAGER**, establezca Operación solicitada en **Iniciar**.


## <a name="language-related-issues"></a>Problemas relacionados con el idioma

En esta sección se incluyen los problemas comunes siguientes:

- [No se aplican los cambios de selección de idioma](#bkmk_lang-symptom1)
- [No todos los idiomas seleccionados están presentes para toda la información de licencia](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a> No se aplican los cambios de selección de idioma

#### <a name="cause"></a>Causa

Este problema se puede producir si la selección de idioma se almacena en caché y no se borra después de cambiar los valores de propiedad.

#### <a name="workaround"></a>Solución alternativa

Para resolver este problema, reinicie el servicio **SMS_Executive**.

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a> No todos los idiomas seleccionados están presentes para toda la información de licencia

#### <a name="cause"></a>Causa

Este problema se puede producir si la información de licencia de la aplicación Microsoft Store para Empresas y Educación no contiene datos localizados para el idioma especificado.

#### <a name="workaround"></a>Solución alternativa

Agregue manualmente los idiomas que faltan para las aplicaciones creadas.


## <a name="offline-applications"></a>Aplicaciones sin conexión

En esta sección se incluyen los problemas comunes siguientes:

- [No se pudo crear la aplicación sin conexión porque no se puede comprobar el contenido](#bkmk_off-symptom1)
- [No se pudo instalar la aplicación creada a partir de la información de la licencia sin conexión](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a> No se pudo crear la aplicación sin conexión porque no se puede comprobar el contenido

#### <a name="cause"></a>Causa

Este problema se puede producir si el contenido sincronizado para la aplicación sin conexión está dañado o se ha modificado.

#### <a name="workaround"></a>Solución alternativa

Inicie una nueva sincronización. Cuando se complete la sincronización, debe comprobar y descargar los archivos de contenido incorrectos.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a> No se pudo instalar la aplicación creada a partir de la información de la licencia sin conexión

#### <a name="cause"></a>Causa

Este problema se puede producir si implementa la aplicación en un cliente que ejecuta una versión de Windows 10 anterior a la versión 1511. Las aplicaciones con licencia sin conexión de Microsoft Store para Empresas y Educación solo se admiten en la versión 1511 y posteriores de Windows 10.

#### <a name="resolution"></a>Solución

Instale la versión más reciente de Windows 10.


## <a name="next-steps"></a>Pasos siguientes

Para buscar ayuda adicional, vea [Búsqueda de ayuda para usar Configuration Manager](../../core/understand/find-help.md).
