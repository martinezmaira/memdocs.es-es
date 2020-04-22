---
title: Información de administración
titleSuffix: Configuration Manager
description: Obtenga información sobre la funcionalidad Información de administración disponible en la consola de Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694453"
---
# <a name="management-insights-in-configuration-manager"></a>Información de administración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Información de administración de Configuration Manager proporciona información sobre el estado actual del entorno. La información se basa en el análisis de los datos de la base de datos del sitio. Esta información le ayuda a entender mejor el entorno y tomar medidas en consecuencia. <!--1353967-->

## <a name="review-management-insights"></a>Revisar información de administración

Para ver las reglas, su cuenta debe tener el permiso **leer** en el objeto **sitio**.

1. Abra la consola de Configuration Manager.  

2. Vaya al área de trabajo **Administración**, expanda **Información de administración** y seleccione **Toda la información**.  

    > [!Note]  
    > Al seleccionar el nodo **Información de administración**, se muestra el [Panel Información de administración](#bkmk_insights).  

3. Abra el grupo de información de administración que quiera revisar. Haga clic en **Mostrar información** en la cinta de opciones.  

Las siguientes cuatro pestañas están disponibles para su revisión:

- **Todas las reglas**: proporciona la lista completa de las reglas para el grupo de información de administración elegido.  

- **Completa**:  enumera las reglas en las que no se necesita ninguna acción.  

- **En curso**: muestra las reglas en las que algunos requisitos previos están completos, pero no todos.  

- **Acción necesaria**: se enumeran las reglas en las que es necesario realizar acciones. Haga clic en **Más detalles** para recuperar los elementos específicos en los que se necesita una acción.  

El panel **Requisitos previos** muestra los elementos necesarios para ejecutar la regla.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Todas las reglas y requisitos previos para el grupo de servicios en la nube

![Información de administración: todas las reglas y requisitos previos para el grupo de servicios en la nube](./media/Management-insights-all-cloud-rules.png)

Seleccione una regla y después haga clic en **Más detalles** para ver los detalles de la regla.

## <a name="operations"></a>Operaciones

Las reglas de información de administración vuelven a evaluar su aplicabilidad de acuerdo a una programación semanal. Para volver a evaluar una regla a petición, haga clic con el botón derecho en la regla y seleccione **Reevaluar**.

El archivo de registro para reglas de información de administración es **SMS_DataEngine.log** en el servidor de sitio.

<!--1357930-->
Algunas reglas le permiten tomar medidas. Seleccione una regla y haga clic en **Más detalles**. Después, si está disponible, seleccione **Tomar medidas**.

En función de la regla, esta acción muestra uno de los siguientes comportamientos:  

- Navegar automáticamente por la consola hasta el nodo donde se puede realizar una acción. Por ejemplo, si la información de administración recomienda cambiar una configuración de cliente, al llevar a cabo la acción navegará hasta el nodo Configuración de cliente. Después realice otra acción modificando los valores predeterminados o un objeto de configuración de cliente personalizado.  

- Navegar a una vista filtrada basándose en una consulta. Por ejemplo, al actuar en la regla de recopilaciones vacías se muestran solo estas recopilaciones en la lista de recopilaciones. Después puede realizar otra acción, como eliminar una recopilación o modificar sus reglas de pertenencia.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Panel de información de administración

<!--1357979-->

El nodo **Información de administración** incluye un panel gráfico. Este panel muestra información general de los estados de la regla, con lo que le resultará más fácil mostrar el progreso.

Use los siguientes filtros en la parte superior del panel para ajustar la vista:

- Mostrar completadas
- Opcional
- Recomendado
- Crítica

En el panel se incluyen los iconos siguientes:  

- **Índice de Información de administración**: realiza el seguimiento del progreso general en las reglas de información de administración. El índice es un promedio ponderado. Las reglas críticas valen más. Este índice proporciona el menor peso a las reglas opcionales.  

- **Grupos de Información de administración**: muestra el porcentaje de las reglas en cada grupo, teniendo en cuenta los filtros. Seleccione un grupo para explorar en profundidad las reglas específicas de este grupo.  

- **Prioridad de Información de administración**: muestra el porcentaje de las reglas por prioridad, teniendo en cuenta los filtros.  

- **Toda la información**: una tabla de información, incluida la prioridad y el estado. Use el campo **Filtro** situado en la parte superior de la tabla para emparejar las cadenas de cualquiera de las columnas disponibles. El panel ordena la tabla en el orden siguiente:

  - Estado: acción necesaria, completado, desconocido  
  - Prioridad: crítica, recomendada, opcional  
  - Último cambio: fechas más antiguas en la parte superior  

![Captura de pantalla del panel de información de administración](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Reglas y grupos

Las reglas se organizan en los siguientes grupos de información de administración:

- [Aplicaciones](#applications)
- [Servicios en la nube](#cloud-services)
- [Recopilaciones](#collections)
- [Configuration Manager Assessment](#configuration-manager-assessment)
- [Mantenimiento proactivo](#proactive-maintenance)
- [Seguridad](#security)
- [Administración simplificada](#simplified-management)
- [Centro de software](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Aplicaciones

Conclusiones de administración de la aplicación.

- **Aplicaciones sin implementaciones**: enumera las aplicaciones del entorno sin implementaciones activas. Esta regla ayuda a encontrar y eliminar las aplicaciones sin usar para simplificar la lista de aplicaciones que se muestran en la consola. Para obtener más información, consulte [Deploy applications](../../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).  

### <a name="cloud-services"></a>Servicios en la nube

Ayuda a integrar con muchos servicios en la nube, lo que permite la administración moderna de los dispositivos.

- **Evaluar la preparación de la administración conjunta**: ayuda a comprender qué pasos son necesarios para habilitar la administración conjunta. Esta regla tiene requisitos previos. Para obtener más información, vea [Información general sobre la administración conjunta](../../../comanage/overview.md).  

- **Dispositivos no cargados en Azure AD**: A partir de la versión 2002, esta regla enumera los dispositivos que no se cargan en Azure AD porque el sitio no está correctamente configurado para HTTPS.<!--6268489--> Configure [HTTP mejorado](../../plan-design/hierarchy/enhanced-http.md) o habilite al menos un punto de administración para HTTPS. Si ya ha configurado el sitio para la comunicación HTTPS, esta regla no aparece.

- **Configuración de servicios de Azure para utilizarlos con Configuration Manager**: esta regla le ayuda a incorporar Configuration Manager a Azure AD, que permite a los clientes autenticarse en el sitio mediante Azure AD. Para obtener más información, vea [Configuración de servicios de Azure](../deploy/configure/azure-services-wizard.md).  

- **Habilitar dispositivos para que sean híbridos unidos a Azure Active Directory**: los dispositivos unidos a Azure AD permiten a los usuarios iniciar sesión con sus credenciales de dominio y también asegurarse de que los dispositivos cumplen los estándares de seguridad y cumplimiento de la organización. Para obtener más información, vea [Consideraciones de diseño de identidad híbrida de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Sitios que no tienen una configuración correcta de HTTPS**: A partir de la versión 2002, esta regla enumera los sitios de la jerarquía que no están correctamente configurados para HTTPS. Esta configuración evita que el sitio realice una [Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Puede hacer que la sincronización de Azure AD no cargue todos los dispositivos. Es posible que la administración de estos clientes no funcione correctamente.<!--6268489--> Configure [HTTP mejorado](../../plan-design/hierarchy/enhanced-http.md) o habilite al menos un punto de administración para HTTPS. Si ya ha configurado el sitio para la comunicación HTTPS, esta regla no aparece.

- **Actualización de clientes a la versión más reciente de Windows 10**: Windows 10, versión 1709 o superior, mejora y moderniza la experiencia informática de los usuarios. Para obtener más información, vea [Artículos clave sobre la adopción de Windows como servicio](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Recopilaciones

Información que ayuda a simplificar la administración mediante la limpieza y reconfiguración de las colecciones.

- **Colecciones vacías**: enumera las colecciones del entorno que no tienen miembros. Para obtener más información, vea [Cómo administrar colecciones](../../clients/manage/collections/manage-collections.md).  

A partir de la versión 1902, hay nuevas reglas con recomendaciones sobre la administración de colecciones.<!--3555752--> Use esta información para simplificar la administración y mejorar el rendimiento:

- **Colecciones con ninguna regla de consulta y ningún miembro directo**: elimine estas colecciones para simplificar la lista de colecciones de la jerarquía.  

- **Colecciones con la misma hora de inicio de reevaluación**: estas colecciones tienen la misma hora de reevaluación que otras colecciones. Modifique la hora de reevaluación para que no entren en conflicto.  

- **Colecciones con tiempo de consulta superior a dos segundos**: revise las reglas de consulta de esta colección. Considere la posibilidad de modificar o eliminar la colección.

- Estas reglas incluyen configuraciones que podrían ocasionar una carga innecesaria en el sitio. Revise estas colecciones y elimínelas o deshabilite la evaluación de regla:  

  - **Colecciones sin reglas de consulta y actualizaciones incrementales habilitadas**  

  - **Colecciones sin reglas de consulta y habilitadas para la evaluación incremental o programada**  

  - **Colecciones sin reglas de consulta y con una evaluación completa programada seleccionada**  

### <a name="configuration-manager-assessment"></a>Configuration Manager Assessment

<!--3607758-->

A partir de la versión 2002, este grupo es cortesía de Ingeniería del campo de soporte técnico Premier de Microsoft. Estas reglas son un ejemplo de las muchas comprobaciones más que proporciona Microsoft Premier en [Services Hub](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments).

- **La detección de grupos de seguridad de Active Directory está configurada para ejecutarse con demasiada frecuencia**: normalmente no es necesario configurar que Detección de grupos de seguridad de Active Directory se produzca con más frecuencia que cada tres horas. Una configuración más frecuente puede tener un impacto negativo en el rendimiento de Active Directory, la red y Configuration Manager. Habilite la sincronización incremental, en lugar de usar una programación de sincronización completa. Para obtener más información, vea [Detección de grupos de Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).

- **La detección de sistemas de Active Directory está configurada para ejecutarse con demasiada frecuencia**: normalmente no es necesario configurar que Detección de sistemas de Active Directory se produzca con más frecuencia que cada tres horas. Una configuración más frecuente puede tener un impacto negativo en el rendimiento de Active Directory, la red y Configuration Manager. Habilite la sincronización incremental, en lugar de usar una programación de sincronización completa. Para obtener más información, vea [Detección de sistemas de Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).

- **La detección de usuarios de Active Directory está configurada para ejecutarse con demasiada frecuencia**: normalmente no es necesario configurar que la detección de usuarios de Active Directory se produzca con más frecuencia que cada tres horas. Una configuración más frecuente puede tener un impacto negativo en el rendimiento de Active Directory, la red y Configuration Manager. Habilite la sincronización incremental, en lugar de usar una programación de sincronización completa. Para obtener más información, vea [Detección de usuario de Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

- **Recopilaciones limitadas a Todos los sistemas o Todos los usuarios**: revise todas las recopilaciones en las que se use **Todos los sistemas** o **Todos los usuarios** como recopilación de restricción. Configuration Manager actualiza la pertenencia de estas recopilaciones predeterminadas con datos de los métodos de detección de Active Directory. Es posible que estos datos no sean información válida para los clientes de Configuration Manager.

- **La detección de latidos está deshabilitada**: la detección de latidos requiere la instalación del cliente de Configuration Manager en los dispositivos. Es el único método de detección que los clientes inician. Todos los demás métodos se producen en servidores de sitios. La detección de latidos es esencial para mantener actualizado el estado de actividad del cliente. Esto garantiza que el sitio no haga que los registros de recursos de la base de datos del sitio venzan accidentalmente. Para obtener más información, vea [Heartbeat Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat) (Detección de latidos).

- **Consultas de recopilaciones de larga duración habilitadas para las actualizaciones incrementales**: las recopilaciones cuyo último tiempo de actualización incremental es superior a 30 segundos usan los recursos del servidor de sitio y de la base de datos, lo que puede afectar al rendimiento global de Configuration Manager. Para obtener más información, vea [Procedimientos recomendados para recopilaciones](../../clients/manage/collections/best-practices-for-collections.md).

- **Reducción del número de aplicaciones y paquetes en los puntos de distribución**: De forma oficial, Microsoft admite un total combinado de hasta 10 000 paquetes y aplicaciones en un punto de distribución. Si se supera este total, se pueden producir problemas de funcionamiento. Para obtener más información, vea [Números de tamaño y escala: punto de distribución](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **Problemas de instalación del sitio secundario**: el estado de la instalación de algunos sitios secundarios es **Pendiente** o **Con error**. Estos estados significan que la instalación se ha iniciado, pero que no se ha completado correctamente. Hasta que finalice la instalación del sitio secundario, es posible que los clientes no se comuniquen de forma correcta con el sitio principal. Compruebe el área de trabajo **Supervisión** y vuelva a intentar realizar la instalación. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](install-in-console-updates.md#bkmk_retry).

- **Actualización de todos los sitios a la misma versión**: use la misma versión de Configuration Manager en una jerarquía. Esta configuración garantiza que todos los sitios proporcionen la misma funcionalidad. Los sitios con otras versiones en la misma jerarquía presentan escenarios de interoperabilidad. Las versiones posteriores de Configuration Manager incluyen características nuevas y resuelven problemas conocidos. Para obtener más información, vea [Interoperabilidad entre diferentes versiones](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Para obtener más información sobre estas reglas, vea [Pasos de corrección para ConfigMgr Management Insights](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Si ya es un cliente de Microsoft Unified o Microsoft Premier, inicie sesión en [Services Hub](https://serviceshub.microsoft.com/assessments/) para obtener más evaluaciones a petición.
>
> Para obtener más información sobre los servicios de Microsoft, vea [Soluciones de soporte técnico](https://www.microsoft.com/enterprise/services/support).

### <a name="proactive-maintenance"></a>Mantenimiento proactivo

<!--1352184-->
Las reglas de este grupo resaltan posibles problemas de configuración que se pueden evitar mediante el mantenimiento de los objetos de Configuration Manager.

- **Grupos de límites sin sistemas de sitio asignados**: sin los sistemas de sitio asignados, los grupos de límites solo pueden usarse para la asignación de sitio. Para obtener más información, vea [Configuración de grupos de límites](../deploy/configure/boundary-groups.md).  

- **Grupos de límites sin miembros**: los grupos de límites no son aplicables a la asignación de sitio ni a la búsqueda de contenido si no tienen ningún miembro. Para obtener más información, vea [Configuración de grupos de límites](../deploy/configure/boundary-groups.md).  

- **Puntos de distribución que no proporcionan contenido a los clientes**: puntos de distribución que no han proporcionado contenido a los clientes en los treinta últimos días. Estos datos se basan en los informes de los clientes de su historial de descargas. Para obtener más información, vea [Instalación y configuración de puntos de distribución](../deploy/configure/install-and-configure-distribution-points.md).  

- **Habilitar la limpieza WSUS**: comprueba que haya habilitado la opción para ejecutar la limpieza WSUS en las propiedades de componente de punto de actualización de software. Esta opción ayuda a mejorar el rendimiento de WSUS. Para obtener más información, vea [Mantenimiento de las actualizaciones de software](../../../sum/deploy-use/software-updates-maintenance.md).  

- **Imágenes de arranque no utilizadas**: imágenes de arranque a las que no hay ninguna referencia para el uso de la secuencia de tareas o del arranque PXE. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../../../osd/get-started/manage-boot-images.md).  

- **Elementos de configuración no utilizados**: elementos de configuración que no forman parte de una línea base de configuración y tienen más de 30 días. Para obtener más información, consulte [Crear una línea base de configuración](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Actualizar los orígenes de caché del mismo nivel a la última versión del cliente de Configuration Manager**: indentifique a los clientes que actúan como origen de caché del mismo nivel, pero no se ha actualizado desde una versión del cliente anterior a la 1806. Los clientes de la versión anterior a la 1806 no pueden usarse como un origen de caché del mismo nivel para clientes que ejecutan la versión 1806 o alguna posterior. Seleccione **Realizar acción** para abrir una vista de dispositivo que muestre la lista de clientes.<!--1358008-->  

### <a name="security"></a>Seguridad

Conclusiones para mejorar la seguridad de su infraestructura y dispositivos.

- **La reserva de NTLM está habilitada**:<!--4572953--> a partir de la versión 1906, esta regla detecta si habilitó el método de reserva de autenticación NTLM menos seguro para el sitio. Cuando se usa el método de inserción de cliente para la instalación del cliente de Configuration Manager, el sitio puede requerir la autenticación mutua Kerberos. Esta mejora ayuda a proteger la comunicación entre el servidor y el cliente. Para obtener más información, vea [Cómo instalar clientes con inserción de cliente](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

- **Versiones del cliente antimalware no admitidas**: Más del 10 % de los clientes ejecutan versiones de System Center Endpoint Protection que no son compatibles. Para obtener más información, vea [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Administración simplificada

Conclusiones que le ayudarán a simplificar la administración diaria de su entorno.

- **Conecte el sitio a la nube de Microsoft para obtener actualizaciones de Configuration Manager**: Esta regla garantiza que el punto de conexión de servicio de Configuration Manager se ha conectado a la nube de Microsoft en los últimos siete días. Esta conexión consiste en descargar contenido para las actualizaciones periódicas. Revise DMPDownloader.log y hman.log. Para más información, consulte los [requisitos de acceso a Internet](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).

- **Versiones de cliente diferentes de CB**: enumera todos los clientes cuyas versiones no son una compilación de la rama actual (CB). Para obtener más información, vea [Actualizar clientes](../../clients/manage/upgrade/upgrade-clients.md).  

- **Actualizar clientes a una versión de Windows 10 admitida**: a partir de la versión 1902, esta regla informa sobre los clientes que ejecutan una versión de Windows 10 que ya no se admite. También incluye a los clientes con una versión de Windows 10 que se acerca al final del servicio (tres meses).<!--3897268-->  

### <a name="software-center"></a>Centro de software

Conclusiones para la administración del Centro de software.

- **Dirigir a los usuarios al Centro de software en lugar de al catálogo de aplicaciones**: compruebe si los usuarios han instalado o solicitado aplicaciones del catálogo de aplicaciones en los últimos 14 días. La funcionalidad principal del Catálogo de aplicaciones ahora se incluye en el Centro de software. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, vea [Deprecated Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features) (Características en desuso).  

- **Uso de la nueva versión del Centro de software**: La versión anterior del Centro de software ya no se admite. Configure los clientes para que usen el nuevo Centro de software. Para ello, habilite la opción de cliente **Usar nuevo Centro de software** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#use-new-software-center).  

### <a name="software-updates"></a>Actualizaciones de software

- **La configuración de cliente no permite que los clientes descarguen contenido diferencial**: Algunas las actualizaciones de software sincronizadas en su entorno incluyen contenido diferencial. Habilite la configuración del cliente, **Permitir que los clientes descarguen contenido diferencial cuando esté disponible**. Si no habilita esta opción, cuando implemente estas actualizaciones, el cliente descargará innecesariamente más contenido del que necesita. Para más información, vea la [Configuración del cliente - Actualizaciones de software](../../clients/deploy/about-client-settings.md#software-updates).

- **Habilitar la categoría de producto de actualizaciones de software para Windows 10, versión 1903 y posteriores**: hay una nueva categoría de producto de actualizaciones de software para Windows 10, versión 1903 y posteriores. Si sincroniza las actualizaciones de Windows 10 y tiene los clientes de Windows 10, versión 1903 o versiones posteriores, seleccione la categoría de producto **Windows 10, versión 1903 y versiones posteriores** en las propiedades de componente de punto de actualización de software. Para más información, vea [Configurar las clasificaciones y los productos que va a sincronizar](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Conclusiones relacionadas con la implementación y el mantenimiento de Windows 10. El grupo de información de administración de Windows 10 está solo disponible cuando más de la mitad de los clientes ejecutan Windows 7, Windows 8 o Windows 8.1.

- **Configurar los datos de diagnóstico y la clave de id. comercial de Windows**: Para usar datos de Análisis de escritorio, configure los dispositivos con una clave de id. comercial y habilite la recopilación de datos de diagnóstico. Establezca los dispositivos Windows 10 en el nivel **Mejorado (limitado)** o en un nivel superior. Para obtener más información, consulte [Habilitación del uso compartido de datos en Análisis de escritorio](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Reglas de información de administración de Windows 10

![Reglas de información de administración para Windows 10](./media/Windows-10-insights-group.png)
