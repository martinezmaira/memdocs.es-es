---
title: Desinstalación de sitios
titleSuffix: Configuration Manager
description: Una guía para quitar roles y desinstalar sitios y jerarquías
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700533"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Desinstalar roles, sitios y jerarquías en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use este artículo como guía para desinstalar un sitio, una jerarquía o un rol de sistema de sitio de Configuration Manager.

A partir de la versión 2002, también puede quitar el sitio de administración central (CAS) de una jerarquía, pero mantener el sitio primario.

## <a name="site-system-role"></a><a name="bkmk_role"></a> Rol de sistema de sitio

Es posible que quiera quitar un rol de un servidor de sistema de sitio por las siguientes razones:

- Un cambio de infraestructura más amplio, como la red o las ubicaciones físicas
- Retirar el servidor subyacente
- Consolidar roles para reducir los costes y la complejidad
- Volver a configurar o rediseñar los roles de sitio
- Dejar de usar la característica que admite el rol

Cuando decida que necesita quitar un rol, primero tenga en cuenta las respuestas a las siguientes preguntas:

- ¿Todavía necesita el rol en el sitio? Si es así, ¿hay algún otro sistema de sitio que ya tenga el rol?

- ¿Los sistemas de sitio con este rol tienen el tamaño adecuado para satisfacer los requisitos empresariales de rendimiento y disponibilidad?

- ¿Todos los clientes ya se han reconfigurado para usar otro rol? ¿Dependerá de los comportamientos de cliente predeterminados para revertir o detectar otro servidor?

### <a name="procedure-to-remove-a-site-system-role"></a>Procedimiento para quitar un rol de sistema de sitio

Use el siguiente procedimiento para quitar un rol:

1. En la consola de **Configuration Manager**, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y, después, haga clic en el nodo **Servidores y roles del sistema de sitios**.

1. Seleccione el servidor de sistema de sitio con el rol que se va a quitar. En el panel de detalles **Roles de sistema de sitio**, seleccione el rol de destino.

1. En la pestaña **Rol del sitio** de la cinta de opciones, en el grupo **Rol del sitio**, seleccione en **Quitar rol**. Confirme que quiere quitar el rol.

### <a name="additional-information-for-specific-roles"></a>Más información para roles específicos

Algunos roles pueden tener pasos y consideraciones adicionales.

#### <a name="software-update-point"></a>Punto de actualización de software

Después de quitar el punto de actualización de software, Configuration Manager actualiza la directiva de cliente para quitar el punto de actualización de software de la lista. Cuando quite el último punto de actualización de software del sitio, la lista de puntos de actualización de software no contiene ningún punto de actualización de software. Sin roles disponibles, la administración de actualizaciones de software está deshabilitada en el sitio.

Si tiene más de un punto de actualización de software en un sitio primario y quita el punto de actualización de software que es el origen de sincronización, elija otro punto de actualización de software en el sitio para que sea el nuevo origen de sincronización.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a> Sitio secundario  

Aparte de cuando se [retira una jerarquía](#bkmk_hierarchy), la razón principal para quitar un sitio secundario es un cambio de infraestructura más amplio, como la red o las ubicaciones físicas. Revise también las razones para [elegir un sitio secundario](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

Cuando decida que necesita quitar un sitio secundario, tenga en cuenta primero las respuestas a las siguientes preguntas:

- ¿Se quitaron todos los roles de sistema de sitio del servidor de sitio?

- ¿Hay límites o grupos de límites asociados al sitio secundario? Vuelva a configurar los límites antes de quitar el sitio.

- ¿Todavía queda algún cliente en la ubicación?

- ¿Ha configurado otras opciones de administración de contenido, como la [caché de sistemas de mismo nivel](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)?

### <a name="options-to-delete-secondary-sites"></a>Opciones para eliminar sitios secundarios

No se puede cambiar o volver a asignar un sitio secundario a otro sitio primario. Al quitar un sitio secundario de su sitio primario directo, elija si quiere desinstalarlo o quitarlo.

#### <a name="uninstall-the-secondary-site"></a>Desinstalar el sitio secundario

Utilice esta opción para quitar un sitio secundario funcional que sea accesible desde la red. Esta opción desinstala Configuration Manager del servidor de sitio secundario. Después, elimina toda la información sobre el sitio y sus recursos del sitio de Configuration Manager.

Si Configuration Manager instaló SQL Server Express para el sitio secundario, Configuration Manager desinstala también SQL Express. Si ha instalado SQL Server Express antes de instalar el sitio secundario, Configuration Manager no desinstala SQL Server Express.

#### <a name="delete-the-secondary-site"></a>Eliminar el sitio secundario

Utilice esta opción en las siguientes situaciones:

- No se pudo instalar

- El sitio secundario continua mostrándose en la consola de Configuration Manager después de desinstalarlo

    Esta opción elimina toda la información sobre el sitio y los recursos de la jerarquía de Configuration Manager, pero no realiza ningún cambio en el servidor de sitio.

    > [!TIP]
    >  También puede usar la herramienta de mantenimiento de jerarquía con la opción **/DELSITE** para eliminar un sitio secundario. Para más información, vea [Herramienta de mantenimiento de jerarquía (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>Requisitos previos para eliminar un sitio secundario

El usuario administrativo que ejecuta el programa de instalación de Configuration Manager debe tener los siguientes derechos de seguridad:

- Derechos de **administrador** local en el servidor de sitio secundario

- Derechos de **administrador** local en el servidor de base de datos de sitio remoto para el sitio primario, si el servidor de bases de datos de sitio primario es remoto con respecto al servidor del sitio primario.

- Rol de seguridad **Administrador de infraestructuras** o **Administrador total** en el sitio primario principal

- Derechos de **administrador del sistema** en la base de datos de sitio secundario

### <a name="procedure-to-delete-a-secondary-site"></a>Procedimiento para eliminar un sitio secundario

Utilice el procedimiento siguiente para desinstalar o eliminar un sitio secundario:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y después haga clic en el nodo **Sitios**.

1. Seleccione el servidor de sitio secundario que quiera quitar. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Sitio**, seleccione **Eliminar**.

1. En la página **General**, seleccione si quiere desinstalar o eliminar el sitio secundario.

1.  Complete el asistente.

## <a name="primary-site"></a><a name="bkmk_primary"></a> Sitio primario  

Es posible que quiera desinstalar un sitio primario de la jerarquía por las siguientes razones:

- Consolidar sitios para reducir los costes y la complejidad
- Volver a configurar o rediseñar los sitios de la jerarquía

Antes de desinstalar un sitio primario secundario que utilice [vistas distribuidas](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) activadas para su vínculo de replicación del sitio de administración central (CAS), debe desactivar las vistas distribuidas en su jerarquía. Para obtener más información, consulte [Desinstalar un sitio primario configurado con vistas distribuidas](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a> Planear la desinstalación de un sitio primario

Antes de desinstalar un sitio primario, revise las siguientes tareas:

- Revise los límites, los grupos de límites y las relaciones de reserva. Si asigna clientes a un nuevo sitio, pero no cambia los límites, pueden tener en cuenta la itinerancia. Para obtener más información, vea [Definir los límites del sitio y los grupos de límites](../configure/define-site-boundaries-and-boundary-groups.md).

- Asegúrese de que todos los clientes activos se reasignan a otro sitio primario en la jerarquía. De lo contrario, los clientes no se administrarán después de desinstalar el sitio. Para obtener más información, vea [Cómo asignar clientes a un sitio](../../../clients/deploy/assign-clients-to-a-site.md).

  - Revise la lista de roles de sitio para asegurarse de que el nuevo sitio proporciona el mismo nivel de servicio.

  - Asegúrese de que ha ajustado correctamente el resto de sistemas de sitio con este rol en el otro sitio. Deberán cumplir los requisitos empresariales para el rendimiento y la disponibilidad con los clientes adicionales.

  - Si este sitio tiene muchos clientes, reasígnelos en fases. Supervise la replicación de base de datos a medida que los clientes actualizan el inventario completo y otros datos específicos del sitio. Si administra actualizaciones de software, los clientes se asignarán a un nuevo punto de actualización de software. Este comportamiento provoca un examen completo del cumplimiento de las actualizaciones.

  - La reasignación de clientes puede afectar a los informes y las consultas que se basan en los datos de inventario y el cumplimiento basado en el estado. Tenga en cuenta la posibilidad de ajustar temporalmente cualquier ciclo de cliente durante la transición.

  - Revise todos los métodos de asignación de clientes para asegurarse de que ninguno hace referencia a este sitio primario.

- Compruebe si alguno de los objetos utilizados activamente en la jerarquía tiene referencias estáticas al código de sitio. Por ejemplo, consultas de colección, secuencias de tareas o scripts administrativos.

- Si la jerarquía usa un [sitio de reserva](../configure/boundary-group-procedures.md#bkmk_site-fallback) para la asignación de sitio automática, asegúrese de que no hace referencia a este sitio primario.

- Vuelva a configurar los [métodos de instalación de cliente](../../../clients/deploy/plan/client-installation-methods.md) que pueden hacer referencia a un código de sitio estático.

- Si este sitio primario tiene servicios conectados a la nube específicos del sitio, asegúrese de quitarlos. Si sigue necesitando los recursos en la nube, muévalos a otro sitio primario en la jerarquía. Quítelos del sitio primario que va a desinstalar y agréguelos a otro sitio primario.

- Si este sitio primario tiene [métodos de detección](../configure/run-discovery.md) para la jerarquía, muévalos a otro sitio.

- Retire todos los [medios de implementación de sistema operativo](../../../../osd/deploy-use/create-task-sequence-media.md) basados en sitios.

- Desinstale todos los roles de sistema de sitio del sitio y el servidor de sitio. Para obtener más información, vea [Desinstalar roles de sistema de sitio](#bkmk_role). Aunque este paso de preparación no es necesario, ayuda a identificar las dependencias adicionales antes de desinstalar el sitio.

- Desinstale los sitios secundarios de este sitio primario. Para obtener más información, vea la sección [Sitio secundario](#bkmk_secondary).

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a> Requisitos previos para desinstalar un sitio primario

El usuario administrativo que ejecuta el programa de instalación de Configuration Manager debe tener los siguientes derechos de seguridad:

- Derechos de **administrador** local en el servidor del CAS.

- Derechos de **administrador** local en el servidor de base de datos de sitio remoto para el CAS, si el servidor de bases de datos de CAS es remoto desde el servidor de sitio.

- Derechos de **administrador del sistema** en la base de datos de sitio de administración central (CAS).

- Derechos de **administrador** local en el servidor de sitio primario.

- Derechos de **administrador** local en el servidor de base de datos de sitio remoto para el sitio primario, si el servidor de bases de datos de sitio primario es remoto con respecto al servidor del sitio primario.

- Rol de seguridad **Administrador de infraestructuras** o **Administrador total** en el CAS

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a> Procedimiento para desinstalar un sitio primario

Ejecute el programa de instalación de Configuration Manager para desinstalar un sitio primario que no tiene un sitio secundario asociado. Utilice el procedimiento siguiente para desinstalar un sitio primario:

> [!TIP]
> Si el servidor de sitio primario ya no está disponible, utilice la herramienta de mantenimiento de jerarquía en el sitio de administración central (CAS) para eliminar el sitio primario de la base de datos de sitio. Para más información, vea [Herramienta de mantenimiento de jerarquía (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Inicie el programa de instalación de Configuration Manager en el servidor de sitio primario mediante uno de los métodos siguientes:

    - En el menú **Inicio**, seleccione **Programa de instalación de Configuration Manager**.

    - En el directorio de *medios de instalación* de Configuration Manager, abra `\SMSSETUP\BIN\X64\setup.exe`. Asegúrese de que esta versión sea la misma que la versión del sitio.

    - En el directorio en el que está *instalado* Configuration Manager, abra `\BIN\X64\setup.exe`.

1. Revise la información de la página **Antes de comenzar**.

1. En la página **Introducción**, seleccione **Desinstalar un sitio de Configuration Manager**.

    > [!IMPORTANT]  
    >  Si un sitio secundario se adjunta al sitio primario, debe quitar el sitio secundario para desinstalar el sitio primario.  

1. En la página **Desinstalar el sitio de Configuration Manager**, las dos opciones siguientes están habilitadas de forma predeterminada:

    - Quitar la base de datos de sitio del servidor de sitio primario
    - Quitar la consola de Configuration Manager

1. Seleccione **Sí** para confirmar la desinstalación del sitio primario de Configuration Manager.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a> Desinstalar un sitio primario que utilice vistas distribuidas

1. Antes de desinstalar un sitio primario secundario, desactive las vistas distribuidas en cada vínculo de la jerarquía entre el sitio de administración central (CAS) y el sitio primario.

1. Después de desactivar las vistas distribuidas en cada vínculo, confirme que los datos del sitio primario acaban de reinicializarse en el CAS. Para supervisar la inicialización de datos, vea [Supervisar la replicación](../../manage/monitor-replication.md).

1. Después de reinicializar correctamente los datos con el CAS, [desinstale el sitio primario](#bkmk_pri-process).

1. Después de desinstalar completamente el sitio primario, puede volver a configurar las vistas distribuidas en los vínculos del CAS a otros sitios primarios.

    > [!IMPORTANT]
    > Si desinstala el sitio primario antes de desactivar las vistas distribuidas de cada sitio o antes de que los datos del sitio primario se reinicialicen correctamente en el CAS, es posible que se produzca un error en la replicación de datos.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a> Retirada de una jerarquía

Algunas organizaciones tienen varias jerarquías debido a fusiones, adquisiciones, entornos de prueba u otros requisitos empresariales. Si consolida la administración en una sola jerarquía, esta acción puede ayudar a reducir los costes y la complejidad. Otro motivo para retirar la jerarquía es que va a migrar a un servicio de administración solo en la nube, como Microsoft Intune, y que está listo para quitar su infraestructura local.

Para retirar una jerarquía con varios sitios, la secuencia de eliminación es importante. Empiece desinstalando los sitios de la parte inferior de la jerarquía y luego continúe hacia arriba:

1. Quite los sitios secundarios conectados a sitios primarios.
2. Desinstale los sitios primarios.
3. Después de desinstalar todos los sitios primarios, puede desinstalar el CAS.

Para obtener más información, consulte las secciones siguientes:

- [Quitar un sitio secundario](#bkmk_secondary)
- [Desinstalar un sitio primario](#bkmk_primary)
- [Desinstalar el CAS](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a> Desinstalar el CAS

El último paso para retirar una jerarquía es desinstalar el CAS. Ejecute el programa de instalación de Configuration Manager para desinstalar el CAS que no tiene sitios primarios secundarios.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Requisitos previos para desinstalar el CAS

Compruebe que el usuario administrativo que ejecuta el programa de instalación de Configuration Manager tenga los siguientes derechos de seguridad:

- Derechos de **administrador** local en el servidor del CAS.

- Derechos de **administrador** local en el servidor de base de datos de sitio remoto para el CAS, si el servidor de bases de datos de CAS es remoto desde el servidor de sitio.

#### <a name="procedure-to-uninstall-the-cas"></a>Procedimiento para desinstalar el CAS

1. Inicie el programa de instalación de Configuration Manager en el servidor del CAS mediante uno de los métodos siguientes:

    - En el menú **Inicio**, seleccione **Programa de instalación de Configuration Manager**.

    - En el directorio de *medios de instalación* de Configuration Manager, abra `\SMSSETUP\BIN\X64\setup.exe`. Asegúrese de que esta versión sea la misma que la versión del sitio.

    - En el directorio en el que está *instalado* Configuration Manager, abra `\BIN\X64\setup.exe`.

1. Revise la información de la página **Antes de comenzar**.

1. En la página **Introducción**, seleccione **Desinstalar un sitio de Configuration Manager**.

    > [!IMPORTANT]  
    >  Quite todos los sitios primarios secundarios para poder desinstalar el CAS.  

1. En la página **Desinstalar el sitio de Configuration Manager**, las dos opciones siguientes están habilitadas de forma predeterminada:

    - Quitar la base de datos de sitio del servidor CAS
    - Quitar la consola de Configuration Manager

1. Seleccione **Sí** para confirmar la desinstalación del sitio de administración central (CAS) de Configuration Manager.

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a> Eliminación del CAS

<!-- 3607277 -->

A partir de la versión 2002, si la jerarquía consta del sitio de administración central (CAS) y de un único sitio primario secundario, puede quitar el CAS. Esta acción simplifica la infraestructura de Configuration Manager a un único sitio primario independiente. Elimina las complejidades de la replicación de sitio a sitio y centra sus tareas de administración en un único sitio.

Para obtener más información, vea [Eliminación del CAS](remove-central-administration-site.md).
