---
title: Eliminación del CAS
titleSuffix: Configuration Manager
description: Quite el sitio de administración central (CAS) para simplificar la infraestructura de Configuration Manager a un único sitio primario independiente.
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 237c326c4420aec13ad6c9ca9b07d9f5304b6945
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84613969"
---
# <a name="remove-the-central-administration-site"></a>Quitar el sitio de administración central

*Se aplica a: Configuration Manager (rama actual)*

<!-- 3607277 -->

A partir de la versión 2002, si la jerarquía consta del sitio de administración central (CAS) y de un único sitio primario secundario, puede quitar el CAS. Esta acción simplifica la infraestructura de Configuration Manager a un único sitio primario independiente. Elimina las complejidades de la replicación de sitio a sitio y centra sus tareas de administración en un único sitio.

> [!IMPORTANT]
> En esta versión de Configuration Manager, esta característica se encuentra en versión preliminar y no está habilitada de forma predeterminada. Actualmente, está disponible para los clientes del soporte técnico Premier de Microsoft Azure.
>
> Para habilitar esta característica, póngase en contacto con su responsable técnico de cuentas para obtener ayuda:
>
> - El responsable abrirá un caso de asesoría, que usará las horas del soporte técnico Premier de Microsoft Azure.
> - No se puede cambiar la gravedad del caso.
> - El soporte técnico de Microsoft ayudará en estos casos de consulta durante el horario laboral normal entre semana.

## <a name="plan"></a>Plan

- La jerarquía debe estar formada por el sitio de administración central (CAS) y un único sitio primario secundario. El sitio primario puede tener sitios secundarios. Para quitar otros sitios primarios secundarios de la jerarquía, revise los pasos de planificación y los requisitos previos para [desinstalar un sitio primario](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Asegúrese de que el sitio primario secundario cumple los requisitos de tamaño y escala de un [sitio primario independiente](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Mueva o quite los roles del CAS, excepto el punto de conexión de servicio y el punto de actualización de software. El programa de instalación de Configuration Manager controla estos dos roles al quitar el sitio de administración central.

  Los siguientes roles son los más comunes en el sitio de administración central y debe quitarlos o pasarlos al sitio primario:

  - Punto de sincronización de Asset Intelligence
  - Punto de Endpoint Protection
  - Punto de servicios de informes
  - Punto de servicio de almacenamiento de datos
  - Cloud Management Gateway (CMG)

    > [!NOTE]
    > Si ha habilitado CMG para el contenido, planee redistribuir el contenido después de volver a crear la instancia de CMG en el sitio primario.<!-- 6608659 -->

- Desactive las vistas distribuidas.

- Configuration Manager controla automáticamente las ubicaciones de origen del paquete para los paquetes integrados, como el cliente de Configuration Manager. Revise el resto de ubicaciones de origen del contenido para asegurarse de que no usan un recurso compartido en el sitio de administración central.

- Detenga todos los trabajos de migración activos y quite todas las configuraciones de migración. Para obtener más información, consulte la sección [Detención de la migración activa desde otra jerarquía](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Si usa reglas de implementación automática para las actualizaciones de software, vuelva a crearlas en el sitio primario secundario.

- Si usa Configuration Manager o System Center Updates Publisher para administrar las [actualizaciones de software de terceros](../../../../sum/deploy-use/third-party-software-updates.md), exporte el certificado de firma de WSUS desde el punto de actualización de software del CAS.

  - Antes de eliminar el CAS, espere a que pase la fecha límite de cualquier implementación de actualizaciones de software de terceros necesaria. Los clientes descargan previamente el contenido de las implementaciones necesarias y, al cambiar el punto de actualización de software, el hash de contenido cambia con la *publicación local* de las actualizaciones de software. (Este comportamiento no afecta a otros tipos de contenido, solo a la publicación local de actualizaciones de software de terceros). Si quita el sitio de administración central con estas implementaciones necesarias todavía en curso, se producirá un error de coincidencia de hash en los clientes.

- Revise cualquier software de terceros que pueda tener una dependencia en el sitio de administración central.

## <a name="prerequisites"></a>Requisitos previos

- El usuario administrativo que ejecuta el programa de instalación de Configuration Manager debe tener los siguientes derechos de seguridad:

  - Derechos de **administrador** local en el servidor del CAS.

  - Derechos de **administrador** local en el servidor de base de datos de sitio remoto para el CAS, si el servidor de bases de datos de CAS es remoto desde el servidor de sitio.

  - Derechos de **administrador del sistema** en la base de datos de sitio de administración central (CAS).

  - Derechos de **administrador** local en el servidor de sitio primario.

  - Derechos de **administrador** local en el servidor de base de datos de sitio remoto para el sitio primario, si el servidor de bases de datos de sitio primario es remoto con respecto al servidor del sitio primario.

  - Derechos de **administrador del sistema** en la base de datos del sitio primario.

  - Rol de seguridad **Administrador de infraestructura** o **Administrador total** en el CAS y en el sitio primario.

- Solo un sitio primario secundario en la jerarquía. Para obtener más información, consulte la sección [Desinstalar un sitio primario](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Proceso

1. Inicie el programa de instalación de Configuration Manager en el servidor del CAS mediante uno de los métodos siguientes:

    - En el menú **Inicio**, seleccione **Programa de instalación de Configuration Manager**.

    - En el directorio de *medios de instalación* de Configuration Manager, abra `\SMSSETUP\BIN\X64\setup.exe`. Asegúrese de que esta versión sea la misma que la versión del sitio.

    - En el directorio en el que está *instalado* Configuration Manager, abra `\BIN\X64\setup.exe`.

1. Revise la información de la página **Antes de comenzar**.

1. En la página **Primeros pasos**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio**.

1. En la página **Mantenimiento del sitio**, seleccione **Quitar el sitio de administración central**. <!-- or is it still "delete"? -->

1. En la página **Reconfiguración de los roles existentes de sistema de sitio**:

    - **Punto de conexión de servicio**: escriba el nombre de dominio completo del sistema de sitio en el sitio primario para hospedar este rol obligatorio. Para obtener más información, consulte [About the service connection point](../configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).

    - **Punto de actualización de software**: seleccione un punto de actualización de software existente en el sitio primario. El programa de instalación configura este punto de actualización de software para que se sincronice igual que la configuración del CAS.

    El programa de instalación comprueba que los servidores especificados cumplan los requisitos previos. Seleccione **Empezar la instalación** cuando esté listo para continuar.

Si el programa de instalación encuentra un problema, use el asistente para volver a intentar el proceso.

Una vez finalizada la instalación, se restablece el sitio primario. Para obtener más información, vea [Ejecutar un restablecimiento de sitio](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>Supervisión y comprobación

Revise los siguientes registros durante el proceso de instalación:

- `C:\ConfigMgrSetup.log` en el servidor del CAS

- **hman.log** en el directorio de registros de Configuration Manager del servidor del sitio primario

Use el nodo **Jerarquía del sitio** en el área de trabajo **Supervisión** para visualizar los cambios en la jerarquía. Por ejemplo, en el gráfico siguiente se muestra la comparación del antes y el después del sitio de administración central **SHY**, el sitio primario **HAW** y el sitio secundario **VWT**:

| Antes  | Después   |
|---------|---------|
|![Ejemplo de la vista de jerarquía de un sitio de administración central, un sitio primario y un sitio secundario](media/3607277-cas-primary-secondary.png)|![Ejemplo de la vista de jerarquía de un sitio primario y un sitio secundario](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Tareas posteriores a la instalación

Después de quitar el CAS, revise los pasos siguientes según se apliquen a su entorno.

- Quite manualmente la cuenta de equipo del servidor del CAS de los grupos locales del sitio primario.

- La clave raíz confiable ha cambiado, lo que puede requerir acciones adicionales:

  - Actualice las imágenes de arranque de la implementación del sistema operativo para incluir los archivos binarios más recientes de Configuration Manager.

  - Vuelva a crear [medios de implementación de sistemas operativos](../../../../osd/deploy-use/create-task-sequence-media.md).

- Si conecta Configuration Manager con [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context), debe restablecer la conexión. El primer paso para resolver cualquier problema es [renovar la clave secreta](../configure/azure-services-wizard.md#bkmk_renew). Si esto no resuelve el problema, vuelva a crear la conexión.<!-- 5584635 -->

- En la versión 2002, si habilita la sincronización de controladores de Surface, vuelva a configurar esta característica después de quitar el sitio de administración central. Para más información, consulte el artículo sobre [actualizaciones de firmware y controladores de Microsoft Surface](../../../../sum/deploy-use/surface-drivers.md).<!-- 5728727 -->

- Si administra actualizaciones de software de terceros:

  1. Exporte el certificado de firma de WSUS desde el punto de actualización de software del CAS, si no lo ha hecho ya.

  1. Antes de crear nuevas implementaciones, quite la actualización de las implementaciones existentes y de los paquetes de actualización de software.

  1. Para restaurar los metadatos de las actualizaciones de software a un estado operativo, vuelva a sincronizar los catálogos suscritos. También puede esperar a que Configuration Manager se vuelva a sincronizar automáticamente.

  1. Espere a que un proceso de sincronización de actualizaciones de software normal actualice Configuration Manager con el estado actual de WSUS o inícielo usted. Opcionalmente, puede usar los cmdlets de PowerShell de SCUP o WSUS para eliminar y leer actualizaciones.

  1. Vuelva a publicar el contenido para las actualizaciones que necesita implementar.
