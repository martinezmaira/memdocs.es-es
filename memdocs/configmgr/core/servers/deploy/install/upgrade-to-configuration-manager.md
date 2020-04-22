---
title: Actualización a la rama actual
titleSuffix: Configuration Manager
description: Obtenga información sobre qué pasos seguir para ejecutar correctamente una actualización local desde un sitio y jerarquía que ejecutan System Center 2012 Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700413"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Actualización a la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Realice una actualización local en la rama actual de Configuration Manager desde un sitio y la jerarquía que ejecuta System Center 2012 Configuration Manager. Antes de actualizar System Center 2012 Configuration Manager, debe preparar los sitios. Para esta preparación, es necesario quitar configuraciones específicas que puedan impedir una actualización correcta. A continuación, siga la secuencia de actualización cuando intervenga más de un sitio.  

> [!TIP]  
> Al administrar el sitio de Configuration Manager y la infraestructura de la jerarquía, los términos *mejorar*, *actualizar* e *instalar* se utilizan para describir los tres conceptos diferentes. Para obtener información sobre cómo se usa cada término, vea [Acerca de la actualización e instalación](../../../understand/upgrade-update-install.md).

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a> Rutas de actualización local  

Las siguientes opciones son las rutas de actualización local admitidas actualmente:

### <a name="upgrade-to-version-2002"></a>Actualizar a la versión 2002

Los siguientes productos se pueden actualizar a una versión con *licencia completa* de la rama actual de Configuration Manager, versión 2002:

- Una instalación de *evaluación* de la rama actual de Configuration Manager, versión 2002
- System Center 2012 Configuration Manager con Service Pack 1
- System Center 2012 Configuration Manager con Service Pack 2
- Administrador de configuración de System Center 2012 R2
- System Center 2012 R2 Configuration Manager con Service Pack 1

Para más información, consulte [Preguntas más frecuentes sobre las licencias y ramas de Configuration Manager](../../../understand/product-and-licensing-faq.md).

> [!TIP]  
> Al realizar la actualización desde una versión de System Center 2012 Configuration Manager a la rama actual, es posible simplificar el proceso de actualización. Para obtener más información, consulte:  
>
> - [Versiones de línea de base y versiones de actualización](../../manage/updates.md#bkmk_Baselines)  
> - [La carpeta CD.Latest](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Rutas de acceso no admitidas

No se admiten las siguientes rutas de acceso:

- No se admite la actualización de una rama de versión preliminar técnica a una instalación con licencia completa. Una versión de Technical Preview solo se puede actualizar a una versión posterior de la versión de Technical Preview correspondiente.  

- No se admite la migración de una versión preliminar técnica a una versión con licencia completa.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> Lista de comprobación de actualización  

Las listas de comprobación siguientes pueden ayudarle a planear una actualización correcta a Configuration Manager.  

### <a name="before-you-upgrade"></a>Antes de realizar la actualización  

Revise estos pasos antes de actualizar a Configuration Manager.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Revisar el entorno de System Center 2012 Configuration Manager

Resolver los problemas como se detalla en el siguiente artículo del servicio de soporte técnico de Microsoft: [Los clientes de Configuration Manager se reinstalan cada cinco horas debido a una tarea periódica de reintento y puede provocar una actualización de cliente involuntaria](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Asegurarse de que su entorno cumpla las configuraciones admitidas

- Revise la versión de sistema operativo de servidor en uso para hospedar roles de sistema de sitio:  

  - Algunos sistemas operativos anteriores compatibles con System Center 2012 Configuration Manager no se admiten en la rama actual de Configuration Manager. Antes de la actualización, quite los roles de sistema de sitio de esas versiones del sistema operativo. Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - El comprobador de requisitos previos de Configuration Manager no comprueba los requisitos previos de los roles de sistema de sitio en el servidor de sitio ni en los sistemas de sitio remotos.  

- Revise los requisitos previos requeridos para cada equipo que hospeda un rol de sistema de sitio. Por ejemplo, para implementar un sistema operativo, Configuration Manager usa Assessment and Deployment Kit (Windows ADK) para Windows 10. Antes de ejecutar el programa de instalación, debe descargar e instalar Windows 10 ADK en el servidor del sitio y en cada uno de los equipos que ejecutan una instancia del proveedor de SMS.  

Para más información sobre las plataformas admitidas y las configuraciones de los requisitos previos, consulte [Configuraciones admitidas](../../../plan-design/configs/supported-configurations.md).  

Para más información sobre el uso del ADK de Windows con Configuration Manager, consulte [Requisitos de infraestructura para la implementación de SO](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Revisar el estado del sitio y de la jerarquía y comprobar que no hay problemas sin resolver

Antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor del sitio, el servidor de base de datos del sitio y los roles del sistema de sitio instalados en los equipos remotos. La actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Instalar todas las actualizaciones críticas aplicables de los sistemas operativos en los equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto

Antes de actualizar un sitio, instale las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización del Service Pack.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Desinstalar los roles de sistema de sitio no compatibles con Configuration Manager

Los siguientes roles de sistema de sitio ya no se usan en Configuration Manager. Desinstálelas antes de actualizar System Center 2012 Configuration Manager:  

- Punto de administración fuera de banda  

- Punto de Validador de mantenimiento del sistema  

- Punto de sitios web del catálogo de aplicaciones y punto de servicio web

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Deshabilite las réplicas de la base de datos para los puntos de administración en los sitios primarios

Configuration Manager no puede actualizar correctamente un sitio primario que tenga una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de:  

- Crear una copia de seguridad de la base de datos del sitio para probar la actualización de la base de datos.  

- Actualizar el sitio de producción a la rama actual de Configuration Manager.  

Vea los siguientes artículos para más información:  

- System Center 2012 Configuration Manager: [Configuración de réplicas de base de datos para puntos de administración](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager, rama actual: [Réplicas de bases de datos para puntos de administración](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Volver a configurar los puntos de actualización de software que usan NLB

Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.  

Si utiliza clústeres NLB para puntos de actualización de software, use PowerShell para quitar el clúster NLB. (A partir de System Center 2012 Configuration Manager SP1, no hay ninguna opción en la consola de Configuration Manager para configurar un clúster NLB).  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Deshabilitar todas las tareas de mantenimiento del sitio en cada sitio mientras dure la actualización del sitio

Antes de actualizar a Configuration Manager, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización esté activo. Esta lista incluye, entre otras, las siguientes tareas:  

- Copia de seguridad del servidor del sitio  
- Eliminar operaciones cliente antiguas  
- Eliminar datos de detección antiguos  

Si se ejecuta una tarea de mantenimiento de base de datos durante el proceso de actualización, se puede producir un error en la actualización del sitio.  

Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de finalizar la actualización del sitio.

Para más información sobre las tareas de mantenimiento del sitio, consulte los siguientes artículos:  

- System Center 2012 Configuration Manager: [Planeamiento de las operaciones del sitio](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, rama actual: [Referencia de las tareas de mantenimiento](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Ejecutar el comprobador de requisitos previos del programa de instalación

Antes de actualizar un sitio, ejecute el **comprobador de requisitos previos** independientemente del programa de instalación para validar que el sitio cumple los requisitos previos. Después, cuando actualice el sitio, el comprobador de requisitos previos se ejecuta otra vez.  

La comprobación de requisitos previos independiente evalúa si el sitio está preparado para la actualización a la rama actual y a la rama de mantenimiento a largo plazo (LTSB) de Configuration Manager. Dado que la rama de mantenimiento a largo plazo no admite algunas características, podría ver entradas en **ConfigMgrPrereq.log** parecidas a los ejemplos siguientes:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Si tiene previsto actualizar a la rama actual, puede pasar por alto sin problema los errores relacionados con la edición LTSB. Solo se aplican si tiene previsto actualizar a LTSB.

Más adelante, cuando se ejecuta el programa de instalación de Configuration Manager para realizar la actualización, la comprobación de requisitos previos se ejecuta de nuevo. El sitio se evalúa según la rama de Configuration Manager que decida instalar (rama actual o LTSB). Si decide actualizar a la rama actual, no se ejecutará la comprobación de características que no sean compatibles con LTSB.

Para más información, consulte [Comprobador de requisitos previos](prerequisite-checker.md) y [Lista de comprobaciones de requisitos previos](list-of-prerequisite-checks.md).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Descargar los archivos de requisitos previos y los archivos redistribuibles de Configuration Manager

Use el **descargador del programa de instalación** para descargar los archivos redistribuibles de requisitos previos, los paquetes de idioma y las actualizaciones más recientes del producto de Configuration Manager.  

Para obtener información, consulte [Descargador del programa de instalación](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Planear la administración de los idiomas de los servidores y los clientes

Cuando se actualiza un sitio, la actualización del sitio instala solo las versiones del paquete de idioma que se seleccionan durante la actualización.  

- El programa de instalación revisa la configuración actual de idioma de su sitio. Luego, identifica los paquetes de idioma que están disponibles en la carpeta donde se almacenan los archivos de requisitos previos descargados previamente.  

- Puede confirmar la selección actual de los paquetes de idioma de servidor y cliente, o bien cambiar las selecciones para agregar o quitar compatibilidad con determinados idiomas.  

- Solo se pueden seleccionar los paquetes de idioma que están disponibles al ejecutar el programa de instalación.  

> [!NOTE]  
> No puede usar los paquetes de idioma de System Center 2012 Configuration Manager para habilitar idiomas para un sitio de la rama actual de Configuration Manager.  

Para más información sobre los paquetes de idioma, consulte [Paquetes de idioma](language-packs.md).  

#### <a name="review-considerations-for-site-upgrades"></a>Revisar las consideraciones para las actualizaciones de sitio

Al actualizar un sitio, algunas características y configuraciones restablecen su configuración predeterminada. Para ayudarle a prepararse para estos cambios y otros relacionados, consulte [Consideraciones sobre la actualización](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Crear una copia de seguridad de la base de datos del sitio en el sitio de administración central y los sitios primarios

Antes de actualizar un sitio, haga una copia de seguridad de la base de datos del sitio para asegurarse de que dispone de una copia de seguridad preparada para una recuperación ante desastres.  

Para obtener más información, vea [Copia de seguridad y recuperación](../../manage/backup-and-recovery.md).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Hacer una copia de seguridad de un archivo configuration.mof personalizado

Si usa un archivo configuration.mof personalizado para definir clases de datos que se usan con el inventario de hardware, cree una copia de seguridad de este archivo. Tras la actualización, restaure este archivo en el sitio. Para obtener más información, vea [Cómo ampliar el inventario de hardware](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Probar el proceso de actualización de la base de datos en una copia de la última copia de seguridad de la base de datos del sitio

Antes de actualizar un sitio primario o un sitio de administración central de Configuration Manager, pruebe la el proceso de actualización de la base de datos del sitio en una copia de la base de datos del sitio.  

- Pruebe el proceso de actualización de la base de datos del sitio. Cuando actualiza un sitio, la base de datos de sitio podría estar modificada.  

- Aunque no es necesario probar la actualización de la base de datos de prueba, puede ayudarle a identificar problemas de la actualización antes de que la base de datos de producción se vea afectada.  

- Una actualización incorrecta de la base de datos del sitio podría inutilizar la base de datos del sitio, en cuyo caso podría ser necesaria una recuperación del sitio para restaurar la funcionalidad.  

- Aunque se trate de una base de datos de sitio compartida entre varios sitios de una jerarquía, planee la prueba de la base de datos en cada uno de los sitios correspondientes antes de actualizar el sitio.  

- Si usa réplicas de base de datos para puntos de administración en un sitio primario, deshabilite la replicación antes de crear la copia de seguridad de la base de datos del sitio.  

Configuration Manager no admite la copia de seguridad de sitios secundarios ni la actualización de prueba de una base de datos de un sitio secundario.  

No se puede ejecutar una actualización de prueba en la base de datos del sitio de producción. Esta acción actualiza la base de datos del sitio y podría inutilizar el sitio.  

Para obtener más información, vea [Probar la actualización de la base de datos del sitio](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Reiniciar el servidor de sitio y todos los equipos que hospedan un rol de sistema de sitio

Realice esta acción para asegurarse de que no hay ninguna acción pendiente de una instalación reciente de actualizaciones o de requisitos previos.  

#### <a name="upgrade-sites"></a>Actualizar sitios

En el sitio de primer nivel de la jerarquía, ejecute Setup.exe desde el medio de origen de Configuration Manager.  

A continuación, puede comenzar la actualización de los sitios secundarios. No comience la actualización de un sitio hasta que finalice la anterior.  

Hasta que todos los sitios de la jerarquía se actualicen a Configuration Manager, la jerarquía funciona en modo de versión mixta.  

Para obtener información sobre cómo ejecutar la actualización, consulte [Actualizar sitios](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Después de realizar la actualización  

Revise estos pasos después de actualizar a Configuration Manager.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Actualizar las consolas independientes de Configuration Manager

De manera predeterminada, cuando se actualiza un sitio de administración central o un sitio primario, también se actualiza la consola de Configuration Manager instalada en el servidor de sitio. Actualice manualmente cada una de las consolas que esté instalada en un equipo distinto del servidor de sitio.  

> [!TIP]  
> Cierre todas las consolas abiertas antes de iniciar la actualización.  

Para obtener más información, consulte [Instalar la consola de System Center Configuration Manager](install-consoles.md).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Volver a configurar réplicas de base de datos para los puntos de administración de los sitios primarios

Si usa réplicas de base de datos con puntos de administración en sitios primarios, necesita desinstalar las réplicas de base de datos antes de actualizar el sitio. Después de actualizar un sitio primario, vuelva a configurar la réplica de base de datos de los puntos de administración.

Para obtener más información, vea [Réplicas de bases de datos para puntos de administración ](../configure/database-replicas-for-management-points.md).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Volver a configurar todas las tareas de mantenimiento de la base de datos que haya deshabilitado antes de la actualización

Si deshabilitó [tareas de mantenimiento](../../manage/reference-for-maintenance-tasks.md) de la base de datos en un sitio antes de la actualización, vuelva a configurar esas tareas en el sitio con los mismos valores que había antes de la actualización.  

#### <a name="upgrade-clients"></a>Actualizar clientes.

Después de actualizar todos los sitios a Configuration Manager, planee la actualización de los clientes.  

Cuando se actualiza un cliente, se desinstala el software cliente actual y se instala la nueva versión de software cliente. Para actualizar clientes, puede usar cualquier método admitido por Configuration Manager.  

> [!TIP]  
> Al actualizar el sitio de primer nivel de una jerarquía, también se actualiza el paquete de instalación de cliente en cada punto de distribución de la jerarquía. Cuando se actualiza un sitio primario, se actualiza el paquete de actualización de cliente que está disponible en ese sitio primario.  

Para obtener más información, consulte [How to upgrade clients for Windows computers (Cómo actualizar clientes para equipos Windows)](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a> Consideraciones sobre la actualización  

### <a name="automatic-actions"></a>Acciones automáticas

Cuando se realiza la actualización a Configuration Manager, se producen de forma automática las siguientes acciones:  

- Un restablecimiento del sitio. Esta acción incluye una reinstalación de todos los roles de sistema de sitio.  

- Si el sitio es el sitio de nivel superior de una jerarquía, actualiza el paquete de instalación de cliente en cada punto de distribución en la jerarquía. El sitio también actualiza las imágenes de arranque predeterminadas para que usen la nueva versión de Windows PE incluida en Windows Assessment and Deployment Kit para Windows 10. Sin embargo, la actualización no actualiza el medio existente para usar con la implementación de la imagen.  

- Si el sitio es un sitio primario, actualiza el paquete de actualización de cliente para ese sitio.  

### <a name="manual-actions-after-an-upgrade"></a>Acciones manuales después de una actualización

Después de actualizar un sitio, asegúrese de realizar las siguientes acciones:  

- Asegúrese de que los clientes asignados a cada sitio primario se actualizan e instalan la nueva versión del cliente  

- Actualice cada consola de Configuration Manager que se conecta al sitio y que se ejecuta en un equipo remoto con respecto al servidor de sitio.  

- En los sitios primarios en los que usa réplicas de base de datos para puntos de administración, vuelva a configurar las réplicas de base de datos.  

- Después de actualizar el sitio, actualice manualmente los medios físicos, como archivos ISO de CD, DVD o unidades flash USB. La actualización debe incluir también los medios preconfigurados proporcionados a los proveedores de hardware. La actualización del sitio actualiza las imágenes de arranque predeterminadas, no puede actualizar estos dispositivos o archivos de medios usados de forma externa a Configuration Manager.  

- Planee la actualización de las imágenes de arranque personalizadas cuando no necesite la versión anterior de Windows PE.  

### <a name="actions-that-affect-configurations-and-settings"></a>Acciones que afectan a la configuración

Cuando un sitio se actualiza a Configuration Manager, algunas configuraciones no se conservan después de la actualización. Algunas configuraciones se establecen en un nuevo valor predeterminado. En la lista siguiente se incluyen algunos valores de configuración que no se conservan o que cambian:  

- **Centro de software**  
    Se restablecen los valores predeterminados de los siguientes elementos del Centro de software:  

  - **Información del trabajo**: se restablece un horario comercial de **5:00 a.m.** a **10:00 p.m.** , de lunes a viernes.  

  - El valor de **Mantenimiento del equipo** se configura como **Suspender las actividades del Centro de software si el equipo está en modo Presentación**.  

  - El valor de **Control remoto** se configura según el valor en la configuración de cliente asignada al equipo.  

- **Programaciones de resumen de actualización de software**: Las programaciones de resumen personalizadas para actualizaciones de software o grupos de actualizaciones de software se restablecen al valor predeterminado de 1 hora. Al finalizar la actualización, restablezca los valores personalizados de resumen según la frecuencia necesaria.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> Probar la actualización de la base de datos del sitio  

La siguiente información solo se aplica cuando se actualiza una versión anterior como System Center 2012 Configuration Manager a la rama actual de Configuration Manager.

Antes de actualizar un sitio, pruebe una copia de la base de datos de ese sitio para la actualización.  

Para comprobar que la base de datos esté preparada para una actualización, primero debe restaurar una copia de la base de datos del sitio en una instancia de SQL Server que no hospede un sitio de Configuration Manager. La versión de SQL Server que use para hospedar la copia de base de datos debe ser una versión de SQL Server que admita Configuration Manager.  

Después de restaurar la base de datos del sitio, en el equipo de SQL Server, ejecute el programa de instalación de Configuration Manager desde la carpeta de medios de origen de Configuration Manager. Use la opción de la línea de comandos `/TESTDBUPGRADE`.  

Vea los siguientes artículos para más información:

- [Hacer una copia de seguridad de un sitio de Configuration Manager](../../manage/backup-and-recovery.md)  

- [Opciones de la línea de comandos para la instalación](command-line-options-for-setup.md#bkmk_setup)  

- [Compatibilidad con versiones de SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Si integra Microsoft Intune con Configuration Manager:  
>
> al ejecutar una actualización de base de datos de prueba en la copia de la base de datos del sitio de 5 o más días de antigüedad, es posible que reciba un mensaje similar a los siguientes:  
>
> - ADVERTENCIA: La actualización forzará la sincronización completa en la nube.  
> - ERROR: La actualización de la base de datos forzará la sincronización completa en la nube.  
>
> Ambos pueden omitirse de forma segura durante las pruebas de una actualización de la base de datos. No indican un error o problema con la actualización de prueba. En su lugar, indican que, durante la actualización real, los datos del grupo de replicación de base de datos en la **nube** pueden sincronizarse con Microsoft Intune.  

### <a name="test-a-site-database-for-upgrade"></a>Probar que una base de datos del sitio está preparada para la actualización  

Use el siguiente procedimiento en cada sitio de administración central y sitio primario que tenga previsto actualizar:  

1. Realice una copia de la base de datos del sitio. Luego, restaure dicha copia en una instancia de SQL Server que use la misma edición que la base de datos de su sitio y que no hospede un sitio de Configuration Manager. Por ejemplo, si la base de datos del sitio se ejecuta en una instancia de la edición Enterprise de SQL Server, asegúrese de que restaure la base de datos a una instancia de SQL Server que también ejecute la edición Enterprise.  

2. Tras restaurar la copia de la base de datos, ejecute el programa de instalación desde el medio de origen de la rama actual de Configuration Manager. Cuando ejecute el programa de instalación, use la opción de línea de comandos `/TESTDBUPGRADE`. Si la instancia de SQL Server que hospeda la copia de la base de datos no es la instancia predeterminada, proporcione también los argumentos de la línea de comandos para identificar la instancia que hospeda la copia de la base de datos del sitio.  

    Por ejemplo, tiene previsto actualizar una base de datos de sitio con el nombre SMS_ABC. Restaura una copia de esta base de datos del sitio a una instancia compatible de SQL Server con el nombre de instancia DBTest. Para probar una actualización de esta copia de la base de datos del sitio, use la siguiente línea de comandos: `Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup.exe se encuentra en la siguiente ubicación en el medio de origen de Configuration Manager: `SMSSETUP\BIN\X64`  

3. En la instancia de SQL Server donde se ejecuta la actualización de la base de datos de prueba, supervise el archivo ConfigMgrSetup.log en la raíz de la unidad del sistema para ver el progreso y el éxito:  

    - En caso de que se produzca un error en la actualización de prueba, resuelva los problemas relacionados con dicho error. A continuación, cree una nueva copia de seguridad de la base de datos del sitio y pruebe la actualización de esta nueva copia.  

    - Una vez completado el proceso correctamente, puede eliminar la copia de la base de datos.  

        > [!NOTE]  
        > La copia de la base de datos del sitio que se utiliza para probar la actualización de prueba no se puede restaurar para usarla como una base de datos de sitio en cualquier sitio.  

Después de actualizar correctamente una copia de la base de datos del sitio, continúe con la actualización del sitio de Configuration Manager y su base de datos del sitio.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a> Actualizar sitios  

Después de realizar las siguientes tareas, estará listo para actualizar el sitio de Configuration Manager:

- Configuraciones previas a la actualización del sitio
- Prueba de la actualización de la base de datos del sitio en una copia de la base de datos
- Descarga de archivos de requisitos previos y paquetes de idioma para la versión que planea instalar

Cuando se actualiza un sitio en una jerarquía, primero debe actualizar el sitio de nivel superior de la jerarquía. Este sitio de nivel superior es un sitio de administración central o un sitio primario independiente. Una vez completada la actualización de un sitio de administración central, puede actualizar los sitios primarios y secundarios en el orden que desee. Después de actualizar un sitio primario, puede actualizar sus sitios secundarios. También tiene la opción de actualizar sitios primarios adicionales antes de actualizar cualquier sitio secundario.  

Para actualizar un sitio de administración central o un sitio primario, ejecute el programa de instalación desde el medio de origen de Configuration Manager. No ejecute el programa de instalación para actualizar los sitios secundarios. En su lugar, se usa la consola de Configuration Manager para actualizar un sitio secundario después de completar la actualización de su sitio primario.  

Antes de actualizar un sitio, cierre la consola de Configuration Manager del servidor de sitio hasta que finalice la actualización del sitio. También debe cerrar cada consola de Configuration Manager que se ejecute en equipos que no sean el servidor de sitio. Puede volver a conectar la consola una vez completada la actualización del sitio. En cambio, hasta que actualice una consola de Configuration Manager a la nueva versión de Configuration Manager, esa consola no podrá mostrar algunos objetos ni información que estén disponibles en la nueva versión de Configuration Manager.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Actualizar un sitio de administración central o un sitio primario  

1. Compruebe que el usuario que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    - Derechos de **administrador** local en el servidor de sitio  

    - Si el servidor de base de datos del sitio es remoto desde el servidor de sitio, se necesitan en él derechos de **administrador** local.  

2. En el servidor de sitio, abra el siguiente programa: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Esta acción abre al Asistente para instalación de Configuration Manager.  

3. Lea la información de la página **Antes de comenzar** y, luego, seleccione **Siguiente**.  

4. En la página **Introducción**, seleccione **Actualizar este sitio de Configuration Manager** y, a continuación, seleccione **Siguiente**.  

5. En la página **Clave de producto**:  

    Si instaló anteriormente la evaluación de Configuration Manager, puede seleccionar **Install the licensed edition of this product** (Instalar la edición con licencia de este producto). A continuación, escriba la clave de producto correspondiente a la instalación completa de Configuration Manager. Esta acción cambia el sitio a la versión completa.  

    También puede especificar la **fecha de expiración de Software Assurance** de su contrato de licencia como un práctico recordatorio de esa fecha. Si no especifica este valor durante la instalación, puede hacerlo más adelante desde la consola de Configuration Manager.  

    > [!NOTE]  
    > Microsoft no valida la fecha de expiración especificada y no la usará para la validación de la licencia. pero usted puede usarla como un recordatorio de la fecha de expiración. Configuration Manager busca de forma periódica nuevas actualizaciones de software que se ofrecen en línea y el estado de su licencia de Software Assurance debe ser actual para que pueda usar estas actualizaciones adicionales.

    Para obtener más información, vea [Licencias y ramas](../../../understand/learn-more-editions.md).

6. En la página **Términos de licencia del software de Microsoft**, lea y acepte los términos de licencia y, después, seleccione **Siguiente**.  

7. En la página **Licencias de requisitos previos**, lea y acepte los términos de licencia del software necesario y seleccione **Siguiente**. El programa de instalación descarga e instala automáticamente el software en los sistemas de sitio o los clientes cuando sea necesario. Para poder continuar a la página siguiente, acepte todos los términos.  

8. En la página **Descargas de requisitos previos**, especifique si el programa de instalación descarga el contenido más reciente de Internet o use los archivos descargados previamente. Este contenido incluye archivos redistribuibles necesarios, paquetes de idioma y las actualizaciones más recientes del producto. Si previamente descargó los archivos con el descargador del programa de instalación, seleccione **Usar archivos descargados anteriormente** y especifique la carpeta de descarga. Para obtener más información, consulte [Descargador del programa de instalación](setup-downloader.md).  

    > [!NOTE]  
    > Cuando se utilizan archivos descargados anteriormente, compruebe que la ruta de acceso a la carpeta de descarga contiene la versión más reciente de los archivos.  

9. En la página **Selección de idioma de servidor** , vea la lista de idiomas instalados actualmente para el sitio. Seleccione idiomas adicionales que estén disponibles en este sitio para la consola de Configuration Manager y para los informes. También puede borrar los idiomas que ya no quiera permitir en este sitio. El idioma predeterminado es el inglés y no se puede quitar.  

    > [!IMPORTANT]  
    > Las versiones de Configuration Manager no pueden usar paquetes de idioma de una versión anterior de Configuration Manager. Para habilitar la compatibilidad con un idioma en un sitio de Configuration Manager que actualice, debe usar la versión del paquete de idioma para esa nueva versión. Por ejemplo, durante la actualización de System Center 2012 Configuration Manager a la rama actual de Configuration Manager, si la versión de la rama actual de un paquete de idioma no está disponible con los archivos de requisitos previos descargados, no podrá instalar la compatibilidad con ese idioma.  

10. En la página **Selección de idioma de cliente** , vea la lista de idiomas instalados actualmente para el sitio. Seleccione los idiomas adicionales que están disponibles en este sitio para los equipos cliente o borre los idiomas que ya no desee admitir en este sitio. Especifique si desea habilitar todos los idiomas de cliente para clientes de dispositivos móviles y, a continuación, haga clic en **Siguiente**. El idioma predeterminado es el inglés y no se puede quitar.  

11. En la página **Resumen de configuración**, revise las opciones de configuración. Cuando esté listo, seleccione **Siguiente** para iniciar el comprobador de requisitos previos y confirmar la preparación del servidor para la actualización del sitio.  

12. En la página **Comprobación de requisitos previos de la instalación**, si no aparece ningún problema, seleccione **Siguiente** para actualizar el sitio y los roles de sistema de sitio.

    Cuando el comprobador de requisitos previos encuentre un problema, seleccione un elemento de la lista para obtener más información acerca de cómo resolver el problema. Resuelva todos los elementos de la lista que tengan un estado de **Error** antes de continuar el programa de instalación. Después de resolver el problema, haga clic en **Ejecutar comprobación** para reiniciar la comprobación de requisitos previos. También puede abrir el archivo ConfigMgrPrereq.log en la raíz de la unidad del sistema para revisar los resultados del comprobador de requisitos previos. El archivo de registro puede contener información adicional que no se muestra en la interfaz de usuario. Para obtener una lista de reglas de requisitos previos de instalación y descripciones, consulte [Comprobador de requisitos previos](list-of-prerequisite-checks.md).

En la página **Actualización** , el programa de instalación muestra el estado del progreso general. Una vez completada la instalación del servidor de sitio principal y del sistema de sitio, puede cerrar el asistente. La configuración del sitio continúa en segundo plano.  

### <a name="upgrade-a-secondary-site"></a>Actualizar un sitio secundario  

1. Compruebe que el usuario administrativo que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    - Derechos de **administrador** local en el servidor de sitio secundario  

    - Rol de seguridad **Administrador de infraestructuras** o **Administrador total** en el sitio primario principal  

    - Derechos de administrador de sistema (**SA**) en la base de datos del sitio secundario  

2. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y después haga clic en el nodo **Sitios**.  

3. Seleccione el sitio secundario que quiere actualizar. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Sitio**, seleccione **Actualizar**.  

4. Seleccione **Sí** para confirmar la decisión y para iniciar la actualización del sitio secundario.  

La actualización del sitio secundario se ejecuta en segundo plano. Una vez finalizada, puede confirmar el estado en la consola de Configuration Manager. Seleccione el servidor de sitio secundario y, luego, en la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Sitio** y seleccione **Mostrar estado de instalación**.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a> Tareas posteriores a la actualización  

Después de actualizar un sitio, es posible que tenga que realizar tareas adicionales para finalizar la actualización o volver a configurar el sitio. Estas tareas pueden incluir los siguientes elementos:

- Actualizar los clientes de Configuration Manager
- Actualizar las consolas de Configuration Manager
- Volver a habilitar las réplicas de base de datos de los puntos de administración
- Restaurar la configuración de la funcionalidad de Configuration Manager que use y que no se conserva después de la actualización  
