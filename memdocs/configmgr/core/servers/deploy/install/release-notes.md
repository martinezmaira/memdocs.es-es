---
title: Notas de la versión
titleSuffix: Configuration Manager
description: Obtenga información sobre problemas urgentes que todavía no se han corregido en el producto o no se han tratado en un artículo de Knowledge Base del soporte técnico de Microsoft.
ms.date: 05/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 131b6104d5724c8a4eeb0bb68c4afd9a5319abb7
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823969"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de la versión de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Con Configuration Manager, las notas de la versión del producto se limitan a cuestiones urgentes. Estos problemas todavía no se han corregido en el producto o no se han tratado en detalle en un artículo de Knowledge Base del soporte técnico de Microsoft.  

La documentación específica de características incluye información acerca de los problemas conocidos que afectan a escenarios básicos.  

Este artículo contiene notas de la versión de la rama actual de Configuration Manager. Para obtener más información sobre la rama Technical Preview, vea [Technical Preview](../../../get-started/technical-preview.md)  

Para obtener información sobre las características que presentan las distintas versiones, consulte los siguientes artículos:

- [Novedades de la versión 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Novedades de la versión 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Novedades de la versión 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [Novedades de la versión 1902](../../../plan-design/changes/whats-new-in-version-1902.md)

Para obtener información sobre las nuevas características de Análisis de escritorio, consulte [Novedades de Análisis de escritorio](../../../../desktop-analytics/whats-new.md).

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Configuración y actualización  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>La actualización automática del cliente se produce inmediatamente en todos los clientes.

<!-- 6040412 -->

*Se aplica a la versión 1910*

Si el sitio usa la [actualización automática del cliente](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade), cuando actualice el sitio a la versión 1910, todos los clientes se actualizarán inmediatamente después de que el sitio se actualice correctamente. La única aleatoriedad es cuando los clientes reciben la directiva, que de forma predeterminada es cada hora. Para un sitio grande con muchos clientes, este comportamiento puede consumir una cantidad significativa de tráfico de red y puntos de distribución de esfuerzo.

Para más información sobre las versiones afectadas, consulte [Actualización de cliente para la rama actual de Configuration Manager, versión 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>El servidor de sitio en modo pasivo no actualiza configuration.mof

<!-- 5787848 -->

*Se aplica a la versión 1910*

Si el sitio incluye un [servidor de sitio en modo pasivo](../configure/site-server-high-availability.md), puede que, al actualizar el sitio, se pierdan las personalizaciones de inventario. Actualmente, el sitio no sincroniza configuration.mof al conmutar por error los servidores de sitio.

Para solucionar este problema, haga una copia de seguridad de configuration.mof y restáurelo manualmente.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Configuración de la advertencia de requisitos previos en el nivel funcional del dominio en Server 2019

<!-- 4904376 -->

*Se aplica a la versión 1906*

Al instalar la actualización de la versión 1906 en un entorno con controladores de dominio que ejecutan Windows Server 2019, la comprobación de requisitos previos para el nivel funcional del dominio devuelve la siguiente advertencia:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Para solucionar esta incidencia, omita la advertencia.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>La detección de usuarios de Azure AD y la sincronización del grupo de colecciones no funcionan después de la expansión del sitio

<!-- 4797313 -->
*Se aplica a la versión 1906*

Después de configurar cualquiera de las siguientes características:

- Detección de grupos de usuarios de Azure Active Directory
- Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure Active Directory

Si, a continuación, expande un sitio primario independiente a una jerarquía con un sitio de administración central, verá el siguiente error en SMS_AZUREAD_DISCOVERY_AGENT.log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Para solucionar esta incidencia, renueve la clave asociada al registro de la aplicación en Azure AD. Para más información, vea [Renovar clave secreta](../configure/azure-services-wizard.md#bkmk_renew).

## <a name="role-based-administration"></a>Administración basada en roles

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Los ámbitos de seguridad de determinadas carpetas no se replican de CAS a los sitios primarios
<!--6306759-->
*Se aplica a la versión 1910*

Después de actualizar a la versión 1910, los [ámbitos de seguridad para las carpetas](../configure/configure-role-based-administration.md#bkmk_config-folder) en las recopilaciones de usuarios y las recopilaciones de dispositivos no se replican de CAS a los sitios primarios.

## <a name="application-management"></a>Administración de aplicaciones

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>No se puede obtener el certificado correspondiente al error de PowerShell al implementar Microsoft Edge, versión 77 y posteriores
<!--5769384-->
*Se aplica a: versión 1910 de Configuration Manager*

Si está ejecutando la consola de Configuration Manager en un sistema operativo donde el idioma es sueco, húngaro o japonés, recibirá el siguiente error al implementar Microsoft Edge, versión 77 y posteriores:

`Unable to get certificate for Powershell`

Este error se produce porque no hay una carpeta `scripts` en el directorio `AdminConsole\bin` de los idiomas sueco, húngaro o japonés. La carpeta scripts se localiza en estos idiomas de sistema operativo.

Para solucionar esta incidencia, cree una carpeta llamada `scripts` en el directorio `AdminConsole\bin`. Copie los archivos de la carpeta localizada en la carpeta `scripts` recién creada. Una vez copiados los archivos, implemente Microsoft Edge, versión 77 y posteriores.

## <a name="os-deployment"></a>Implementación del sistema operativo

### <a name="task-sequences-cant-run-over-cmg"></a>No se pueden ejecutar secuencias de tareas a través de CMG

*Se aplica a: Configuration Manager, versión 2002*

Hay dos casos en los que no se pueden ejecutar secuencias de tareas en un dispositivo que se comunica a través de una instancia de Cloud Management Gateway (CMG):

- Ha configurado el sitio para HTTP mejorado y el punto de administración es HTTP.<!-- 6358851 -->

    Para solucionar esta incidencia, configure el punto de administración para HTTPS.

- Ha instalado y registrado el cliente con un token de registro en masa para la autenticación.<!-- 6377921 -->

    Para solucionar esta incidencia, use uno de los métodos de autenticación siguientes:

  - Registro previo del dispositivo en la red interna
  - Configuración del dispositivo con un certificado de autenticación del cliente
  - Unión del dispositivo a Azure AD

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Tras promover el servidor de sitio pasivo, los paquetes de imágenes de arranque predeterminadas todavía tendrán el paquete de origen en el servidor activo anterior.

<!--3453224, SCCMDocs-pr issue 3097-->
*Se aplica a: Configuration Manager, versión 1810*

Si tiene un servidor de sitio en modo pasivo (servidor B), cuando lo promueva a activo, la ubicación del contenido para las imágenes de arranque predeterminadas continuará haciendo referencia al servidor activo anterior (servidor A). Si el servidor A tiene un error de hardware, no podrá actualizar ni cambiar las imágenes de arranque predeterminadas.

No hay ninguna solución para este problema.

## <a name="software-updates"></a>Actualizaciones de software

### <a name="security-roles-are-missing-for-phased-deployments"></a>Roles de seguridad que faltan para las implementaciones por fases

<!--3479337, SCCMDocs-pr issue 3095-->
*Se aplica a: Configuration Manager, versiones 1810, 1902*

El rol de seguridad integrado **Administrador de implementaciones del sistema operativo** tiene permisos para las [implementaciones por fases](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). En los roles siguientes faltan estos permisos:  

- **Administrador de aplicaciones**  
- **Administrador de implementación de aplicaciones**  
- **Administrador de actualizaciones de software**  

El rol **Autor de la aplicación** puede parecer que tiene algunos permisos para las implementaciones por fases, pero no debería ser capaz de crear implementaciones.

Un usuario con uno de estos roles puede iniciar el asistente Crear una implementación por fases y puede ver las implementaciones por fases para una aplicación o actualización de software. No puede completar al asistente ni realizar cambios en una implementación existente.

Para solucionar esta incidencia, cree un rol de seguridad personalizado. Copie un rol de seguridad existente y agregue los permisos siguientes a la clase de objeto **Implementación por fases**:

- Crear  
- Eliminar  
- Modificar  
- Lectura  

Para obtener más información, vea [Crear roles de seguridad personalizados](../configure/configure-role-based-administration.md#BKMK_CreateSecRole).

## <a name="desktop-analytics"></a>Análisis de escritorio

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a> Una actualización de seguridad extendida para Windows 7 hace que aparezca como **No se puede inscribir**

<!-- 7283186 -->
_Se aplica a: Configuration Manager, versiones 1902, 1906, 1910 y 2002_

La actualización de seguridad extendida (ESU) de abril de 2020 para Windows 7 cambió la versión mínima requerida de diagtrack.dll de 10586 a 10240. Este cambio hace que los dispositivos de Windows 7 se muestren como **No se pueden inscribir** en el panel **Estado de conexión** de Análisis de escritorio. Al explorar en profundidad la vista de dispositivos para este estado, la propiedad **Configuración del servicio DiagTrack** muestra el estado siguiente: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

No se requiere ninguna solución alternativa para este problema. No desinstale la ESU de abril. Si, por lo contrario, está configurada correctamente, los dispositivos de Windows 7 siguen notificando los datos de diagnóstico al servicio Análisis de escritorio y dichos dispositivos se siguen mostrando en el portal.

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Si usa el inventario de hardware para las vistas distribuidas, no puede realizar incorporaciones al Análisis de escritorio

<!-- 4950335 -->
*Se aplica a: la versión 1902 de Configuration Manager con el paquete acumulativo de actualizaciones y a la versión 1906*

Si tiene una jerarquía y habilita los datos del sitio **Inventario de hardware** para las [vistas distribuidas](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) en cualquier vínculo de replicación del sitio, después de configurar la conexión del Análisis de escritorio en Configuration Manager, verá el siguiente error en M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Para solucionar esta incidencia, deshabilite los datos del sitio **Inventario de hardware** de las vistas distribuidas en cada vínculo de replicación del sitio.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>La consola se cerra inesperadamente al quitar colecciones

<!-- 4749443 -->
*Se aplica a: Versión 1902 de Configuration Manager con el paquete acumulativo de actualizaciones*

Después de conectar el sitio a [Análisis de escritorio](../../../../desktop-analytics/connect-configmgr.md), puede **seleccionar colecciones específicas para sincronizar con Análisis de escritorio**. Si quita una colección y aplica los cambios, agregar inmediatamente una colección nueva provoca una excepción no controlada. La consola se cierra inesperadamente.

Para solucionar esta incidencia, cuando quite una colección, seleccione **Aceptar** para cerrar la ventana de propiedades. Luego, vuelva a abrir las propiedades para agregar una colección nueva en la pestaña **Desktop Analytics Connection** (Conexión de Análisis de escritorio).

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>El icono Estado piloto muestra algunos dispositivos como "no definidos"

<!-- 4547783 -->
*Se aplica a: Versión 1902 de Configuration Manager con el paquete acumulativo de actualizaciones*

Al usar la consola de Configuration Manager para supervisar el estado de la implementación piloto, los dispositivos piloto actualizados en la versión de destino de Windows de ese plan de implementación se muestran como **no definidos** en el icono Estado piloto.  

Estos dispositivos **no definidos** están **actualizados** con la versión de destino del sistema operativo de ese plan de implementación. No es necesario realizar ninguna acción.

## <a name="cloud-services"></a>Servicios en la nube

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>El servicio de Azure para la nube de administración pública de EE. UU. se muestra como nube pública

<!-- 6036748 -->

*Se aplica a la versión 1910*

Si crea una conexión a un servicio de Azure y establece el **entorno de Azure** en la nube de administración pública, las propiedades de la conexión muestran el entorno como la nube pública de Azure. Este es solo un problema de visualización en la consola, porque el servicio está en la nube de administración pública. Para confirmar la configuración, ejecute la consulta SQL siguiente en la base de datos del sitio:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

En el caso de la nube de administración pública, el resultado de esta consulta es `2` para el inquilino específico.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>No se puede descargar contenido de una instancia de Cloud Management Gateway habilitada para TLS 1.2

<!-- 5771680 -->

*Se aplica a las versiones 1906 y 1910 del anillo de actualización temprana*

Si se habilita una instancia de Cloud Management Gateway (CMG) para que **funcione como punto de distribución de nube y sirva contenido desde Azure Storage**, y **se aplica TLS 1.2**, pueden producirse errores en las descargas de contenido.

Los siguientes errores aparecen reflejados en DataTransferService.log en el cliente:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Los siguientes errores aparecen reflejados en CMGContentService.log en el servidor:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Para evitar este problema:

- Actualice el sitio a la versión disponible globalmente (1910), publicada el 20 de diciembre de 2019 (si ya ha actualizado a la versión 1910 del anillo de actualización temprana, deberá actualizar a esta compilación cuando esté disponible).

- Otra opción consiste en usar un [punto de distribución de nube](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) tradicional. Ese rol no aplica TLS 1.2, pero es compatible con clientes que requieren TLS 1.2.

## <a name="protection"></a>Protección

### <a name="bitlocker-management-appears-in-version-1906"></a>La administración de BitLocker aparece en la versión 1906

*Se aplica a la versión 1906*

<!-- 5984688 -->

Después del 21 de noviembre de 2019, si actualiza a la versión 1906 de la versión 1902 o anterior, la característica de administración de BitLocker estará activada y disponible. Se trata de una característica opcional a partir de la versión 1910. No se admite en la versión 1906. Si intenta usarla en la versión 1906, puede recibir resultados inesperados. Si no la usa, no hay ningún impacto.

Para usar la [característica de administración de BitLocker](../../../../protect/plan-design/bitlocker-management.md), actualice a la versión 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
