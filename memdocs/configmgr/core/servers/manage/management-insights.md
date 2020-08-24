---
title: Información de administración
titleSuffix: Configuration Manager
description: Obtenga información sobre la funcionalidad Información de administración disponible en la consola de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700521"
---
# <a name="management-insights-in-configuration-manager"></a>Información de administración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Información de administración de Configuration Manager proporciona información sobre el estado actual del entorno. La información se basa en el análisis de los datos de la base de datos del sitio. Esta información le ayuda a entender mejor el entorno y tomar medidas en consecuencia. <!--1353967-->

## <a name="review-management-insights"></a>Revisar información de administración

Para ver la información, la cuenta necesita el permiso **Lectura** en el objeto **Sitio**.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Información de administración** y seleccione **Todas las conclusiones**.

    > [!NOTE]
    > Al seleccionar el nodo **Información de administración**, se muestra el [Panel Información de administración](#bkmk_insights).

1. Abra el grupo de información de administración que quiera revisar.

1. En la cinta de opciones, seleccione **Mostrar conclusiones**.

Las siguientes cuatro pestañas están disponibles para su revisión:

- **Todas las reglas**: proporciona la lista completa de información del grupo elegido.

- **Completa**:  enumera la información en la que no se necesita ninguna acción.

- **En curso**: muestra la información en la que algunos requisitos previos están completos, pero no todos.

- **Acción necesaria**: en esta pestaña se enumera la información en la que es necesario realizar alguna acción. Seleccione **Más detalles** para mostrar los elementos específicos en los que se necesita una acción.

En el panel **Requisitos previos** se muestran todos los elementos necesarios para ejecutar la información seleccionada.

Por ejemplo, en la siguiente captura de pantalla, se muestra un ejemplo de la pestaña **Todas las reglas** para el grupo **Cloud Services**:

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Información de administración: todas las reglas y requisitos previos para el grupo Cloud Services":::

Para ver los detalles, seleccione una información y, después, seleccione **Más detalles**.

## <a name="operations"></a>Operaciones

El sitio vuelve a evaluar la aplicabilidad de la información de administración según una programación semanal. Para volver a evaluar una información manualmente, haga clic con el botón derecho en ella y seleccione **Volver a evaluar**.

El archivo de registro para información de administración es **SMS_DataEngine.log** en el servidor de sitio.

<!--1357930-->
Alguna información le permite realizar acciones. Seleccione una información y haga clic en **Más detalles**. Después, si está disponible, seleccione **Realizar acción**. En función de la información, esta acción muestra uno de los siguientes comportamientos:

- Navegar automáticamente por la consola hasta el nodo donde se puede realizar una acción. Por ejemplo, si la información de administración recomienda cambiar una configuración de cliente, al llevar a cabo la acción navegará hasta el nodo **Configuración de cliente**. Después realice otra acción modificando los valores predeterminados o un objeto de configuración de cliente personalizado.

- Navegar a una vista filtrada basándose en una consulta. Por ejemplo, al realizar alguna acción en la información de recopilaciones vacías, se muestran solo estas recopilaciones en la lista de recopilaciones. Después puede realizar otra acción, como eliminar una recopilación o modificar sus reglas de pertenencia.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Panel de información de administración

<!--1357979-->

Seleccione el nodo **Información de administración** para mostrar un panel gráfico. Este panel muestra información general de los estados de la información, con lo que le resultará más fácil mostrar el progreso.

Use los siguientes filtros en la parte superior del panel para ajustar la vista:

- Mostrar completadas
- Opcional
- Recomendado
- Crítica

En el panel se incluyen los iconos siguientes:  

- **Índice de Información de administración**: realiza el seguimiento del progreso general de la información de administración. El índice es un promedio ponderado. La información crítica vale más. Este índice proporciona el menor peso a la información opcional.

- **Grupos de Información de administración**: muestra el porcentaje de información en cada grupo, teniendo en cuenta los filtros. Seleccione un grupo para explorar en profundidad la información específica de este grupo.

- **Prioridad de Información de administración**: muestra el porcentaje de información por prioridad, teniendo en cuenta los filtros.

- **Diez reglas principales de información aplicable**: una tabla de información, incluida la prioridad y el estado. Use el campo **Filtro** situado en la parte superior de la tabla para emparejar las cadenas de cualquiera de las columnas disponibles. El panel ordena la tabla en el orden siguiente:

  - Estado: acción necesaria, completado, desconocido  
  - Prioridad: crítica, recomendada, opcional  
  - Último cambio: fechas más antiguas en la parte superior  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Captura de pantalla del panel de información de administración" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Grupos e información

La información se organiza en los siguientes grupos de información de administración:

- [Aplicaciones](#applications)
- [Servicios en la nube](#cloud-services)
- [Recopilaciones](#collections)
- [Configuration Manager Assessment](#configuration-manager-assessment)
- [Optimización para trabajos remotos](#optimize-for-remote-workers)
- [Mantenimiento proactivo](#proactive-maintenance)
- [Seguridad](#security)
- [Administración simplificada](#simplified-management)
- [Centro de software](#software-center)
- [Actualizaciones de software](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> Es posible que el sitio no muestre todos los grupos e información siguientes. Algunos detalles no aparecen cuando ya ha configurado el sitio para la recomendación.

### <a name="applications"></a>Aplicaciones

Conclusiones de administración de la aplicación.

- **Aplicaciones sin implementaciones ni referencias**: enumera las aplicaciones del entorno sin implementaciones ni referencias activas. Las referencias incluyen dependencias, secuencias de tareas y entornos virtuales. Esta información ayuda a encontrar y eliminar las aplicaciones sin usar para simplificar la lista de aplicaciones que se muestran en la consola. Para obtener más información, consulte [Deploy applications](../../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Servicios en la nube

Ayuda a integrar con muchos servicios en la nube, lo que permite la administración moderna de los dispositivos.

- **Evaluar la preparación de la administración conjunta**: ayuda a comprender qué pasos son necesarios para habilitar la administración conjunta. Esta información tiene requisitos previos. Para obtener más información, vea [Información general sobre la administración conjunta](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Dispositivos no cargados en Azure AD**: a partir de la versión 2002, esta información enumera los dispositivos que el sitio no ha cargado en Azure Active Directory (Azure AD) porque no se ha configurado para HTTPS.<!--6268489--> Configure [HTTP mejorado](../../plan-design/hierarchy/enhanced-http.md) o habilite al menos un punto de administración para HTTPS. Si ya ha configurado el sitio para la comunicación HTTPS, esta información no aparece.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Habilitar Cloud Management Gateway**: Cloud Management Gateway (CMG) proporciona una manera sencilla de administrar clientes de Configuration Manager a través de Internet. Al implementar CMG como un servicio en la nube de Microsoft Azure, puede continuar administrando y sirviendo contenido a los clientes que navegan por Internet. Con CMG, no necesita ninguna infraestructura local adicional expuesta a Internet. Para obtener más información, vea [Planear para Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Habilitar dispositivos para que sean híbridos unidos a Azure Active Directory**: los dispositivos unidos a Azure AD permiten a los usuarios iniciar sesión con sus credenciales de dominio y asegurarse de que los dispositivos cumplen los estándares de seguridad y cumplimiento de la organización. Para obtener más información, vea [Consideraciones de diseño de identidad híbrida de Azure Active Directory](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Sitios que no tienen una configuración correcta de HTTPS**: A partir de la versión 2002, esta información enumera los sitios de la jerarquía que no están correctamente configurados para HTTPS. Esta configuración evita que el sitio realice una [Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure AD](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Puede hacer que la sincronización de Azure AD no cargue todos los dispositivos. Es posible que la administración de estos clientes no funcione correctamente.<!--6268489--> Configure [HTTP mejorado](../../plan-design/hierarchy/enhanced-http.md) o habilite al menos un punto de administración para HTTPS. Si ya ha configurado el sitio para la comunicación HTTPS, esta información no aparece.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Actualización de clientes a la versión más reciente de Windows 10**: Windows 10, versión 1709 o superior, mejora y moderniza la experiencia informática de los usuarios. Para obtener más información, vea [Artículos clave sobre la adopción de Windows como servicio](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Recopilaciones

Información que ayuda a simplificar la administración mediante la limpieza y reconfiguración de las colecciones.

- **Colecciones vacías**: enumera las colecciones del entorno que no tienen miembros. Para obtener más información, vea [Cómo administrar colecciones](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Colecciones con ninguna regla de consulta y ningún miembro directo**: elimine estas colecciones para simplificar la lista de colecciones de la jerarquía.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Colecciones con la misma hora de inicio de reevaluación**: estas colecciones tienen la misma hora de reevaluación que otras colecciones. Modifique la hora de reevaluación para que no entren en conflicto.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Recopilaciones con un tiempo de consulta superior a cinco minutos**: revise las reglas de consulta de esta colección. Considere la posibilidad de modificar o eliminar la colección.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- La información siguiente incluye configuraciones que podrían ocasionar una carga innecesaria en el sitio. Revise estas colecciones y elimínelas o deshabilite la evaluación de la regla de recopilación:

  - **Colecciones sin reglas de consulta y actualizaciones incrementales habilitadas**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Recopilaciones sin reglas de consulta y habilitadas para cualquier programación**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Colecciones sin reglas de consulta y con una evaluación completa programada seleccionada**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Configuration Manager Assessment

<!--3607758-->

A partir de la versión 2002, este grupo es cortesía de Ingeniería del campo de soporte técnico Premier de Microsoft. Esa información es un ejemplo de las muchas comprobaciones más que proporciona el soporte técnico Premier de Microsoft Azure en el [centro de servicios](/services-hub/health/getting_started_with_on_demand_assessments).

- **La detección de grupos de seguridad de Active Directory está configurada para ejecutarse con demasiada frecuencia**: normalmente no es necesario configurar que Detección de grupos de seguridad de Active Directory se produzca con más frecuencia que cada tres horas. Una configuración más frecuente puede tener un impacto negativo en el rendimiento de Active Directory, la red y Configuration Manager. Habilite la sincronización incremental, en lugar de usar una programación de sincronización completa. Para obtener más información, vea [Detección de grupos de Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **La detección de sistemas de Active Directory está configurada para ejecutarse con demasiada frecuencia**: normalmente no es necesario configurar que Detección de sistemas de Active Directory se produzca con más frecuencia que cada tres horas. Una configuración más frecuente puede tener un impacto negativo en el rendimiento de Active Directory, la red y Configuration Manager. Habilite la sincronización incremental, en lugar de usar una programación de sincronización completa. Para obtener más información, vea [Detección de sistemas de Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **La detección de usuarios de Active Directory está configurada para ejecutarse con demasiada frecuencia**: normalmente no es necesario configurar que la detección de usuarios de Active Directory se produzca con más frecuencia que cada tres horas. Una configuración más frecuente puede tener un impacto negativo en el rendimiento de Active Directory, la red y Configuration Manager. Habilite la sincronización incremental, en lugar de usar una programación de sincronización completa. Para obtener más información, vea [Detección de usuario de Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Recopilaciones limitadas a Todos los sistemas o Todos los usuarios**: revise todas las recopilaciones en las que se use **Todos los sistemas** o **Todos los usuarios** como recopilación de restricción. Configuration Manager actualiza la pertenencia de estas recopilaciones predeterminadas con datos de los métodos de detección de Active Directory. Es posible que estos datos no sean información válida para los clientes de Configuration Manager.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **La detección de latidos está deshabilitada**: la detección de latidos requiere la instalación del cliente de Configuration Manager en los dispositivos. Es el único método de detección que los clientes inician. Todos los demás métodos se producen en servidores de sitios. La detección de latidos es esencial para mantener actualizado el estado de actividad del cliente. Esto garantiza que el sitio no haga que los registros de recursos de la base de datos del sitio venzan accidentalmente. Para obtener más información, vea [Heartbeat Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat) (Detección de latidos).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Consultas de recopilaciones de larga duración habilitadas para las actualizaciones incrementales**: las recopilaciones cuyo último tiempo de actualización incremental es superior a 30 segundos usan los recursos del servidor de sitio y de la base de datos, lo que puede afectar al rendimiento global de Configuration Manager. Para obtener más información, vea [Procedimientos recomendados para recopilaciones](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Reducción del número de aplicaciones y paquetes en los puntos de distribución**: De forma oficial, Microsoft admite un total combinado de hasta 10 000 paquetes y aplicaciones en un punto de distribución. Si se supera este total, se pueden producir problemas de funcionamiento. Para obtener más información, vea [Números de tamaño y escala: punto de distribución](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **Problemas de instalación del sitio secundario**: el estado de la instalación de algunos sitios secundarios es **Pendiente** o **Con error**. Estos estados significan que la instalación se ha iniciado, pero que no se ha completado correctamente. Hasta que finalice la instalación del sitio secundario, es posible que los clientes no se comuniquen de forma correcta con el sitio principal. Compruebe el área de trabajo **Supervisión** y vuelva a intentar realizar la instalación. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](install-in-console-updates.md#bkmk_retry).<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Actualización de todos los sitios a la misma versión**: use la misma versión de Configuration Manager en una jerarquía. Esta configuración garantiza que todos los sitios proporcionen la misma funcionalidad. Los sitios con otras versiones en la misma jerarquía presentan escenarios de interoperabilidad. Las versiones posteriores de Configuration Manager incluyen características nuevas y resuelven problemas conocidos. Para obtener más información, vea [Interoperabilidad entre diferentes versiones](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Para obtener más detalles sobre esta información, vea [Pasos de corrección de la información de administración de Configuration Manager](/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Si ya es un cliente de Microsoft Unified o Microsoft Premier, inicie sesión en [Services Hub](https://serviceshub.microsoft.com/assessments/) para obtener más evaluaciones a petición.
>
> Para obtener más información sobre los servicios de Microsoft, vea [Soluciones de soporte técnico](https://www.microsoft.com/enterprise/services/support).

### <a name="operating-system-deployment"></a>Implementación de sistema operativo

<!--6982275-->

A partir de la versión 2006, la información de administración siguiente le ayudará a administrar el tamaño de la directiva de las secuencias de tareas. Cuando el tamaño de la directiva de secuencia de tareas supera los 32 MB, el cliente no puede procesar la directiva de gran tamaño. En consecuencia, el cliente no puede ejecutar la implementación de la secuencia de tareas.

- **Las secuencias de tareas de gran tamaño pueden contribuir a superar el tamaño máximo de la directiva**: si implementa estas secuencias de tareas, es posible que los clientes no puedan procesar los objetos de directiva de gran tamaño. Reduzca el tamaño de la directiva de la secuencia de tareas para evitar posibles problemas de procesamiento de las directivas.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **El tamaño total de la directiva para las secuencias de tareas supera el límite de la Directiva**: los clientes no pueden procesar la directiva para estas secuencias de tareas porque es demasiado grande. Reduzca el tamaño de la directiva de secuencia de tareas para permitir que la implementación se ejecute en los clientes.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Para más información, vea [Reducción del tamaño de la directiva de secuencia de tareas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

En la versión 2006, la siguiente información se ha migrado a este grupo desde el grupo **Mantenimiento proactivo**:

- **Imágenes de arranque no utilizadas**: imágenes de arranque a las que no hay ninguna referencia para el uso de la secuencia de tareas o del arranque PXE. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../../../osd/get-started/manage-boot-images.md).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Optimización para trabajos remotos

<!--6982226-->

A partir de la versión 2006, la información siguiente lo ayudará a crear experiencias mejores para los trabajadores remotos y reducir la carga en su infraestructura:

- **Configurar preferencia por orígenes de contenido en la nube de los clientes conectados a VPN**: para reducir el tráfico en la VPN, habilite la opción de grupo de límites **Prefer cloud based sources over on-premises sources** (Preferir los orígenes basados en la nube frente a los orígenes locales). Esta opción permite a los clientes descargar contenido desde Internet en lugar de puntos de distribución a través de la VPN. Para obtener más información, consulte las [opciones de grupo de límites](../deploy/configure/boundary-groups.md#bkmk_bgoptions4).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **Definir grupos de límites de VPN**: cree un límite de VPN y asócielo a un grupo de límites. Asocie sistemas de sitio específicos de VPN al grupo y configure las opciones del entorno. Esta información comprueba al menos un grupo de límites con al menos un límite de VPN. En las propiedades de esta información, seleccione **Revisar acciones** para ir al nodo **Grupos de límites**. Para obtener más información, consulte [Tipo de límite de VPN](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Deshabilitar el uso compartido de contenido punto a punto para clientes conectados VPN**: para evitar el tráfico punto a punto innecesario que probablemente no beneficie a los clientes remotos, deshabilite la opción de grupo de límites **Permitir descargas del mismo nivel en este grupo de límites**. Para obtener más información, consulte las [opciones de grupo de límites](../deploy/configure/boundary-groups.md#bkmk_bgoptions1).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Mantenimiento proactivo

<!--1352184-->
La información de este grupo resalta posibles problemas de configuración que se pueden evitar mediante el mantenimiento de los objetos de Configuration Manager.

- **Grupos de límites sin sistemas de sitio asignados**: sin los sistemas de sitio asignados, los grupos de límites solo pueden usarse para la asignación de sitio. Para obtener más información, vea [Configuración de grupos de límites](../deploy/configure/boundary-groups.md).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Grupos de límites sin miembros**: los grupos de límites no son aplicables a la asignación de sitio ni a la búsqueda de contenido si no tienen ningún miembro. Para obtener más información, vea [Configuración de grupos de límites](../deploy/configure/boundary-groups.md).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Puntos de distribución que no proporcionan contenido a los clientes**: puntos de distribución que no han proporcionado contenido a los clientes en los treinta últimos días. Estos datos se basan en los informes de los clientes de su historial de descargas. Para obtener más información, vea [Instalación y configuración de puntos de distribución](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **Habilitar la limpieza WSUS**: comprueba que haya habilitado la opción para ejecutar la limpieza WSUS en las propiedades de componente de punto de actualización de software. Esta opción ayuda a mejorar el rendimiento de WSUS. Para obtener más información, vea [Mantenimiento de las actualizaciones de software](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Elementos de configuración no utilizados**: elementos de configuración que no forman parte de una línea base de configuración y tienen más de 30 días. Para obtener más información, consulte [Crear una línea base de configuración](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Actualizar los orígenes de caché del mismo nivel a la última versión del cliente de Configuration Manager**:<!--1358008--> indentifique a los clientes que actúan como origen de caché del mismo nivel, pero no se ha actualizado desde una versión del cliente anterior a la 1806. Los clientes de la versión anterior a la 1806 no pueden usarse como un origen de caché del mismo nivel para clientes que ejecutan la versión 1806 o alguna posterior. Seleccione **Realizar acción** para abrir una vista de dispositivo que muestre la lista de clientes.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> En la versión 2006, la información sobre las **Imágenes de arranque no utilizadas** se movió al nuevo grupo [Implementación del sistema operativo](#operating-system-deployment).

### <a name="security"></a>Seguridad

Conclusiones para mejorar la seguridad de su infraestructura y dispositivos.

- **La reserva de NTLM está habilitada**:<!--4572953--> a partir de la versión 1906, esta información detecta si habilitó el método de reserva de autenticación NTLM menos seguro para el sitio. Cuando se usa el método de inserción de cliente para la instalación del cliente de Configuration Manager, el sitio puede requerir la autenticación mutua Kerberos. Esta mejora ayuda a proteger la comunicación entre el servidor y el cliente. Para obtener más información, vea [Cómo instalar clientes con inserción de cliente](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Versiones del cliente antimalware no admitidas**: Más del 10 % de los clientes ejecutan versiones de System Center Endpoint Protection que no son compatibles. Para obtener más información, vea [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Administración simplificada

Conclusiones que le ayudarán a simplificar la administración diaria de su entorno.

- **Conecte el sitio a la nube de Microsoft para obtener actualizaciones de Configuration Manager**: esta información garantiza que el punto de conexión de servicio de Configuration Manager se ha conectado a la nube de Microsoft en los últimos siete días. Esta conexión consiste en descargar contenido para las actualizaciones periódicas. Revise DMPDownloader.log y hman.log. Para más información, consulte los [requisitos de acceso a Internet](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Versiones de cliente diferentes de CB**: enumera todos los clientes cuyas versiones no son una compilación de la rama actual (CB). Para obtener más información, vea [Actualizar clientes](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Actualizar clientes a una versión de Windows 10 admitida**:<!--3897268--> esta información ofrece detalles sobre los clientes que ejecutan una versión de Windows 10 que ya no se admite. También incluye a los clientes con una versión de Windows 10 que se acerca al final del servicio (tres meses).<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Centro de software

Conclusiones para la administración del Centro de software.

- **Dirigir a los usuarios al Centro de software en lugar de al catálogo de aplicaciones**: compruebe si los usuarios han instalado o solicitado aplicaciones del catálogo de aplicaciones en los últimos 14 días. La funcionalidad principal del Catálogo de aplicaciones ahora se incluye en el Centro de software. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, vea [Deprecated Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features) (Características en desuso).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Uso de la nueva versión del Centro de software**: La versión anterior del Centro de software ya no se admite. Configure los clientes para que usen el nuevo Centro de software. Para ello, habilite la opción de cliente **Usar nuevo Centro de software** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#use-new-software-center).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Actualizaciones de software

- **La configuración de cliente no permite que los clientes descarguen contenido diferencial**: Algunas las actualizaciones de software sincronizadas en su entorno incluyen contenido diferencial. Habilite la configuración del cliente, **Permitir que los clientes descarguen contenido diferencial cuando esté disponible**. Si no habilita esta opción, cuando implemente estas actualizaciones, el cliente descargará innecesariamente más contenido del que necesita. Para más información, vea la [Configuración del cliente - Actualizaciones de software](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Habilitar la categoría de producto de actualizaciones de software para Windows 10, versión 1903 y posteriores**: hay una nueva categoría de producto de actualizaciones de software para Windows 10, versión 1903 y posteriores. Si sincroniza las actualizaciones de Windows 10 y tiene los clientes de Windows 10, versión 1903 o versiones posteriores, seleccione la categoría de producto **Windows 10, versión 1903 y versiones posteriores** en las propiedades de componente de punto de actualización de software. Para más información, vea [Configurar las clasificaciones y los productos que va a sincronizar](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Conclusiones relacionadas con la implementación y el mantenimiento de Windows 10. El grupo de información de administración de Windows 10 está solo disponible cuando más de la mitad de los clientes ejecutan Windows 7, Windows 8 o Windows 8.1.

- **Configurar los datos de diagnóstico y la clave de id. comercial de Windows**: Para usar datos de Análisis de escritorio, configure los dispositivos con una clave de id. comercial y habilite la recopilación de datos de diagnóstico. Establezca los dispositivos Windows 10 en el nivel **Mejorado (limitado)** o en un nivel superior. Para obtener más información, consulte [Habilitación del uso compartido de datos en Análisis de escritorio](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->