---
title: Configurar la detección
titleSuffix: Configuration Manager
description: Configure métodos de detección para buscar recursos para administrar desde la red, Active Directory y Azure Active Directory.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cfda27df7df537ededb1f103afdd6107354af786
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347294"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configurar métodos de detección para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configure métodos de detección para buscar recursos para administrar desde la red, Active Directory y Azure Active Directory (Azure AD). Primero habilite y luego configure cada método que quiera usar para realizar búsquedas en el entorno. También se puede deshabilitar un método con el mismo procedimiento que se use para habilitarlo. Las únicas excepciones a este proceso son la detección de latidos y la detección de servidores:  

- De forma predeterminada, la **detección de latidos** ya está habilitada cuando se instala un sitio primario de Configuration Manager. Se configura para ejecutarse de acuerdo a una programación básica. Mantenga habilitada la detección de latidos. Garantiza que los registros de datos de detección (DDR) para los dispositivos están actualizados. Para obtener más información sobre la detección de latidos, vea [Acerca de la detección de latidos](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Detección de servidores** es un método de detección automática. Busca los equipos que se usan como sistemas de sitio. No se puede configurar ni deshabilitar.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Detección de bosques de Active Directory  

Para finalizar la configuración de detección de bosques de Active Directory, configure los ajustes de las ubicaciones siguientes de la consola de Configuration Manager:  

- En el nodo **Métodos de detección**, puede:

  - Habilitar este método de detección.  

  - Establecer una programación de sondeo.  

  - Seleccione si la detección crea automáticamente límites para los sitios y subredes de Active Directory que detecta.  

- En el nodo **Bosques de Active Directory**, puede:

  - Agregar bosques que quiere detectar.  

  - Habilitar la detección sitios y subredes de Active Directory en el bosque.  

  - Configurar opciones que habiliten sitios de Configuration Manager para publicar la información del sitio en el bosque.  

  - Asignar una cuenta para utilizarla como la cuenta de bosque de Active Directory de cada bosque.  

Utilice los procedimientos siguientes para habilitar la detección de bosques de Active Directory y configurar bosques individuales a fin de utilizarlos con la detección de bosques de Active Directory.  

### <a name="configure-active-directory-forest-discovery"></a>Configuración de la detección de bosques de Active Directory  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Métodos de detección**.  

2. Seleccione el método Detección de bosques de Active Directory para el sitio donde desea configurar la detección.  

3. En la pestaña **Inicio** de la cinta de opciones, seleccione **Propiedades**.  

4. En la pestaña **General** de las propiedades, configure la siguientes opciones:  

    - Habilite el método de detección.

    - Especifique opciones para crear los límites de sitio para las ubicaciones detectadas.  

    - Especifique una programación de ejecución de la detección.  

5. Seleccione **Aceptar** para guardar la configuración.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Configuración de un bosque para la detección de bosques de Active Directory  

1. En el área de trabajo **Administración**, expanda **Configuración de jerarquía** y luego haga clic en **Bosques de Active Directory**. Si previamente ejecutó la detección de bosques de Active Directory, verá cada bosque detectado en el panel de resultados. Cuando este método de detección se ejecuta, detecta el bosque local y todos los bosques de confianza. Agregue manualmente los bosques que no son de confianza.  

    - Para configurar un bosque detectado anteriormente, seleccione el bosque en el panel de resultados. En la cinta de opciones, seleccione **Propiedades** para abrir las propiedades del bosque.

    - Para configurar un nuevo bosque que no se muestra, en la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Agregar bosque**. Esta acción abre el cuadro de diálogo **Agregar bosques**.

2. En la pestaña **General**, finalice las configuraciones del bosque que desea detectar y especifique la **cuenta de bosque de Active Directory**. Para más información sobre esta cuenta, vea [Cuentas](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > La detección de bosques de Active Directory requiere una cuenta global para detectar bosques que no son de confianza y publicar en ellos. Si no utiliza la cuenta del equipo del servidor del sitio, solo se puede seleccionar una cuenta global.  

3. Si piensa permitir que los sitios publiquen datos del sitio en este bosque, finalice las configuraciones necesarias para publicar en este bosque en la pestaña **Publicación**.  

    > [!NOTE]  
    > Si permite que los sitios publiquen en un bosque, extienda el esquema de Active Directory del bosque para Configuration Manager. Es necesario que la cuenta del bosque de Active Directory tenga permisos de control total en el contenedor del sistema de ese bosque.  

4. Seleccione **Aceptar** para guardar la configuración.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Detección de Active Directory para equipos, usuarios o grupos  

Para configurar la detección de equipos, usuarios o grupos, comience con estos pasos comunes:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Métodos de detección**.  

2. Seleccione el método para el sitio donde desea configurar la detección.  

3. En la pestaña **Inicio** de la cinta de opciones, seleccione **Propiedades**.  

4. En la pestaña **General** de las propiedades, seleccione la casilla para habilitar la detección. También puede configurar ahora la detección y volver después para habilitarla.  

Después, utilice la información de las siguientes secciones para configurar los métodos de detección específicos:  

- [Detección de grupos de Active Directory](#bkmk_config-adgd)  

- [Detección de sistemas de Active Directory](#bkmk_config-adgd)  

- [Detección de usuarios de Active Directory](#bkmk_config-adud)  

> [!NOTE]  
> La información de esta sección no se aplica a la detección de bosques de Active Directory.  

Si bien cada uno de estos métodos de detección es independiente del resto, comparten opciones similares. Para más información sobre estas opciones de configuración, vea [Características comunes de la detección de grupos, detección de sistemas y detección de usuarios de Active Directory](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> El sondeo de Active Directory de cada uno de estos métodos de detección puede generar un tráfico de red elevado. Considere la posibilidad de programar los métodos de detección para que se ejecuten cuando este tráfico de red no afecte negativamente a los usos de negocio de la red.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a> Configuración de la detección de grupos de Active Directory  

1. En la pestaña **General** de la ventana Propiedades de Detección de grupos de Active Directory, seleccione **Agregar** para configurar un ámbito de detección. Seleccione **Grupos** o **Ubicación**. Después, finalice las configuraciones siguientes en los cuadros de diálogo **Agregar grupos** o **Agregar ubicación de Active Directory**:  

    1. Especifique un **Nombre** para este ámbito de detección.  

    2. Especifique un **Dominio de Active Directory** o una **Ubicación** para buscar:  

        - Si selecciona **Grupos**, especifique uno o varios grupos de Active Directory para su detección.  

        - Si elige **Ubicación**, especifique un contenedor de Active Directory como ubicación que se deba detectar. También puede habilitar una búsqueda recursiva de los contenedores secundarios de Active Directory para esta ubicación.  

    3. Especifique la **Cuenta de detección de grupos de Active Directory** que el sitio usa para buscar este ámbito de detección. Para más información, vea [Cuentas](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Seleccione **Aceptar** para guardar la configuración del ámbito de detección.  

2. Repita los pasos anteriores para cada ámbito de detección adicional que desee definir.  

3. En la pestaña **Programación de sondeo** , configure la programación de sondeo de detección completa y la detección de diferencias.

4. En la pestaña **Opciones**, configure las opciones para filtrar o excluir de la detección los registros de equipos obsoletos. Configure también la detección de la pertenencia a grupos de distribución.  

    > [!NOTE]  
    > De forma predeterminada, la detección de grupos de Active Directory detecta únicamente la pertenencia a grupos de seguridad.  

5. Seleccione **Aceptar** para guardar la configuración.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a> Configuración de la detección de sistemas de Active Directory  

1. En la pestaña **General** de la ventana Propiedades de Detección de sistemas de Active Directory, seleccione el icono **Nuevo**![Icono Nuevo](media/Disc_new_Icon.gif) para especificar un nuevo contenedor de Active Directory. En el cuadro de diálogo **Contenedor de Active Directory**, finalice las configuraciones siguientes:  

    1. Escriba o busque una ubicación para la **ruta de acceso**. Este valor es una ruta de acceso LDAP válida a un contenedor o unidad organizativa (OU). El sitio consulta esta ruta de acceso para los recursos. Por ejemplo, `LDAP://CN=Computers,DC=contoso,DC=com`.  

    2. Especifique las opciones que modifican el comportamiento de búsqueda:  

        - **Detectar objetos dentro de grupos de Active Directory**: el sitio también busca las pertenencias de grupos en esta ruta de acceso.  

        - **Buscar recursivamente contenedores secundarios de Active Directory**: si habilita esta opción, el sitio buscará contenedores adicionales o unidades organizativas en la ruta de acceso anterior. Si deshabilita esta opción, el sitio solo busca recursos en la ruta de acceso específica.  

          A partir de la versión 1806, seleccione los subcontenedores que se excluirán de esta búsqueda recursiva. Esta opción ayuda a reducir el número de objetos detectados. Seleccione **Agregar** para elegir los contenedores en la ruta de acceso anterior. En el cuadro de diálogo Seleccionar nuevo contenedor, seleccione un contenedor secundario para excluir. Seleccione **Aceptar** para cerrar el cuadro de diálogo Seleccionar nuevo contenedor.<!--1358143-->

          > [!Tip]  
          > La lista de contenedores de Active Directory de la ventana Propiedades de Detección de sistemas de Active Directory incluye una columna **Tiene exclusiones**. Al seleccionar contenedores para excluir, este valor es **Sí**.  

    3. Para cada ubicación, especifique la cuenta para utilizarla como la **Cuenta de detección de Active Directory**. Para más información, vea [Cuentas](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Para cada ubicación especificada, se puede configurar un conjunto de opciones de detección y una única cuenta de detección de Active Directory.  

    4. Seleccione **Aceptar** para guardar la configuración del contenedor de Active Directory.  

2. En la pestaña **Programación de sondeo** , configure la programación de sondeo de detección completa y la detección de diferencias.  

3. En la pestaña **Atributos de Active Directory**, configure atributos adicionales de Active Directory para los equipos que desea detectar. En esta pestaña también se enumeran los atributos predeterminados del objeto.  

    > [!Tip]  
    > Por ejemplo, la organización usa el atributo **Descripción** en la cuenta de equipo de Active Directory. Seleccione **Personalizar** y agregue `Description` como un atributo personalizado. Después de que se ejecute este método de detección, este atributo se muestra en la pestaña Propiedades del dispositivo de la consola de Configuration Manager.<!--513948-->  

4. En la pestaña **Opciones**, configure las opciones para filtrar o excluir de la detección los registros de equipos obsoletos.  

5. Seleccione **Aceptar** para guardar la configuración.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a> Configuración de la detección de usuarios de Active Directory  

1. En la pestaña **General** de la ventana Propiedades de Detección de usuarios de Active Directory, seleccione el icono **Nuevo**![Icono Nuevo](media/Disc_new_Icon.gif) para especificar un nuevo contenedor de Active Directory. En el cuadro de diálogo **Contenedor de Active Directory**, finalice las configuraciones siguientes:  

    1. Especifique una o varias ubicaciones de búsqueda.  

    2. Para cada ubicación, especifique las opciones que modifican el comportamiento de búsqueda.  

    3. Para cada ubicación, especifique la cuenta para utilizarla como la **Cuenta de detección de Active Directory**. Para más información, vea [Cuentas](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Para cada ubicación especificada, se puede configurar un único conjunto de opciones de detección y una única cuenta de detección de Active Directory.  

    4. Seleccione **Aceptar** para guardar la configuración del contenedor de Active Directory.  

2. En la pestaña **Programación de sondeo** , configure la programación de sondeo de detección completa y la detección de diferencias.  

3. En la pestaña **Atributos de Active Directory**, configure atributos adicionales de Active Directory para los equipos que desea detectar. En esta pestaña también se enumeran los atributos predeterminados del objeto.  

4. Seleccione **Aceptar** para guardar la configuración.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a> Detección de usuarios de Azure AD

La detección de usuarios de Azure AD no se habilita ni configura igual que otros métodos de detección. Configúrela al incorporar el sitio de Configuration Manager a Azure AD.

Para obtener más información, vea [Detección de usuarios de Azure AD](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Requisitos previos

Para habilitar y configurar este método de detección, [Configure los servicios de Azure](azure-services-wizard.md) para la **Administración en la nube**.

Si usa Configuration Manager para *crear* la aplicación de Azure, la configurará con los permisos necesarios.

Si primero crea la aplicación en Azure y luego la *importa* en Configuration Manager, necesita configurarla manualmente. Esta configuración incluye la concesión del permiso a la aplicación del servidor para que lea los datos del directorio.

1. Abra [Azure Portal](https://portal.azure.com) como un usuario con permisos de *Administrador global*. Vaya a **Azure Active Directory** y seleccione **Registros de aplicaciones**. Cambie a **Todas las aplicaciones** si es necesario.

1. Seleccione la aplicación de destino.

1. En el menú **Administrar**, seleccione **Permisos de API**.  

    1. En el panel **Permisos de API**, seleccione **Agregar un permiso**.  

    2. En el panel **Solicitud de permisos de API**, cambie a **API usadas en mi organización**.  

    3. Busque y seleccione la API de **Microsoft Graph**.  

        > [!Tip]
        > En la versión 1810 y versiones anteriores, use la API **Azure Active Directory Graph**.

    4. Seleccione el grupo **Permisos de la aplicación**. Expanda **Directorio** y seleccione **Directory.Read.All**.  

    5. Seleccione **Agregar permisos**.  

1. En el panel **Permisos de API**, en la sección **Otorgar consentimiento**, seleccione **Conceder consentimiento de administrador...** Seleccione **Sí**.  

### <a name="configure-azure-ad-user-discovery"></a>Configuración de la detección de usuarios de Azure AD

Al configurar el servicio **Cloud Management** de Azure:

- En la página **Detección** del asistente, seleccione la opción **Habilitar la detección de usuarios de Azure Active Directory**.
- Seleccione **Configuración**.
- En el cuadro de diálogo Configuración de detección de usuarios de Azure AD, configure una programación para cuando se produce la detección. También se puede habilitar la detección de diferencias, que busca únicamente las cuentas nuevas o modificadas en Azure AD.

> [!Note]  
> Si el usuario es una identidad federada o sincronizada, debe usar la [detección de usuarios de Active Directory](about-discovery-methods.md#bkmk_aboutUser) de Configuration Manager, así como la detección de usuarios de Azure AD. Para más información sobre las identidades híbridas, vea [Definición de una estrategia de adopción de identidad híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Detección de grupos de usuarios de Azure AD

<!--3611956-->
> [!Tip]  
> Esta característica se introdujo por primera vez en la versión 1906 como una [característica de versión preliminar](../../manage/pre-release-features.md). A partir de la versión 2002, ya no es de versión preliminar.  

Puede descubrir grupos de usuarios y miembros de esos grupos desde Azure AD. Cuando el sitio encuentra usuarios en los grupos de Azure AD que no ha detectado anteriormente, los agrega como nuevos recursos de usuario en Configuration Manager. Cuando el grupo es un grupo de seguridad, se crea un registro de recurso de grupo de usuarios.

### <a name="prerequisites"></a>Requisitos previos

- [Servicio Azure](azure-services-wizard.md) de administración en la nube
- Permiso de lectura y búsqueda en grupos de Azure AD

### <a name="limitations"></a>Limitaciones

La detección delta de grupos de usuarios de Azure AD está deshabilitada en la versión 1906. Puede habilitarla a partir de la versión 1910 de Configuration Manager.

### <a name="log-files"></a>Archivos de registro

Use SMS_AZUREAD_DISCOVERY_AGENT.log para la solución de problemas. Este registro también se comparte con la detección de usuarios de Azure AD. Para obtener más información, vea [Archivos de registro](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Habilitar al detección de grupos de usuarios de Azure AD

Para habilitar la detección en un servicio existente de **Administración en la nube** de Azure:

1. Vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y luego seleccione el nodo **Servicios de Azure**.
1. Seleccione uno de los servicios de Azure y luego seleccione **Propiedades** en la cinta de opciones.
1. En la pestaña **Detección**, active la casilla **Habilitar la detección de grupos de Azure Active Directory** y, después, seleccione **Configuración**.
1. Seleccione **Agregar** en la pestaña **Ámbitos de detección**.
    - Puede modificar la **Programación de sondeo** en la otra pestaña.
1. Seleccione uno o varios grupos de usuarios. También puede **buscar** por nombre y elegir si quiere ver **solo los grupos de seguridad**.
    - La primera vez que seleccione **Buscar** se le pedirá que inicie sesión en Azure.
1. Seleccione **Aceptar** cuando termine de seleccionar los grupos.
1. Cuando finalice la detección, puede examinar los grupos de usuarios de Azure AD en el nodo **Usuarios**.

Para habilitar la detección al configurar un nuevo servicio de Azure de **Administración en la nube**:

- En la página **Detección** del asistente, seleccione la opción **Habilitar la detección de grupos de Azure Active Directory**.
- Seleccione **Configuración**.
- En el cuadro de diálogo Configuración de detección de grupos de Azure AD, configure el ámbito de detección y una programación para cuando se produce la detección.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Detección de latidos

Configuration Manager habilita el método de detección de latidos al instalar un sitio primario. Si desea usar la programación predeterminada para cada siete días, no hay que configurar nada más. De lo contrario, solo tiene que configurar la programación de la frecuencia con que los clientes envían el registro de datos de detección de latidos a un punto de administración.  

> [!NOTE]  
> Si habilita la instalación de inserción de cliente y la tarea de mantenimiento del sitio **Borrar marca de instalación** en el mismo sitio, establezca la programación de la detección de latidos para que sea inferior al **Periodo de nueva detección de cliente** de la tarea de mantenimiento del sitio **Borrar marca de instalación**. Para más información sobre las tareas de mantenimiento del sitio, vea [Tareas de mantenimiento](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Configuración de la programación de la detección de latidos  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Métodos de detección**.  

2. Seleccione el método **Detección de latidos** para el sitio donde desea configurar la detección de latidos.  

3. En la pestaña **Inicio** de la cinta de opciones, seleccione **Propiedades**.  

4. Configure la frecuencia con la que los clientes envían registros de datos de detección de latidos. Después, seleccione **Aceptar** para guardar la configuración.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Detección de redes  

Antes de configurar Detección de redes, debe entender los temas siguientes:  

- Niveles disponibles de la detección de redes  

- Opciones de detección de redes disponibles  

- Limitar la detección de redes en la red  

Para obtener más información, vea la sección [Acerca de la detección de redes](about-discovery-methods.md#bkmk_aboutNetwork).  

En las secciones siguientes se proporciona información sobre configuraciones comunes para la detección de redes. Puede aplicar una o varias de estas configuraciones para utilizarlas durante la misma ejecución de la detección. Si utiliza varias configuraciones, planee las interacciones que pueden afectar a los resultados de la detección.  

Por ejemplo, detecta todos los dispositivos de Protocolo simple de administración de redes (SNMP) que utilizan un nombre de comunidad SNMP específico. Para la misma ejecución de la detección, deshabilite la detección en una subred específica. Cuando se ejecuta la detección, la detección de redes no detecta los dispositivos SNMP con el nombre de comunidad especificado en la subred que se ha deshabilitado.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Determinación de la topología de red  

Puede utilizar una detección solo de topología para asignar unidades de red. Este tipo de detección no detecta posibles clientes. La detección de redes solo de topología se basa en SNMP.  

Al asignar la topología de red, configure el **Número máximo de saltos** en la pestaña **SNMP** del cuadro de diálogo **Propiedades de detección de redes**. Unos pocos saltos pueden ayudarle a controlar el ancho de banda de red que se utiliza cuando se ejecuta la detección. Conforme aumenta el número de elementos detectados en su red, incremente el número de saltos para obtener una mejor comprensión de la topología de red.  

Una vez que comprenda la topología de red, configure propiedades adicionales para la Detección de redes. Estas propiedades ayudan a detectar clientes potenciales y sus sistemas operativos. Configure también la Detección de redes para limitar los segmentos de red que puede buscar.  

Para más información, vea [Determinación de la topología de red](#bkmk_proc-top).

### <a name="network-discovery-search-options"></a>Opciones de búsqueda de Detección de redes

Configuration Manager admite los siguientes métodos de búsqueda de red:

- [Limitación de búsquedas mediante el uso de subredes](#BKMK_LimitBySubnet)
- [Búsqueda en un dominio específico](#BKMK_SearchByDomain)
- [Limitación de búsquedas mediante el uso de nombres de comunidad SNMP](#BKMK_LimitBySNMPname)
- [Búsqueda en un servidor DHCP específico](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Limitación de búsquedas mediante el uso de subredes  

Puede configurar Detección de redes para buscar subredes específicas durante la ejecución de la detección. De forma predeterminada, Detección de redes busca la subred del servidor que ejecuta la detección. Las subredes adicionales que se pueden configurar y habilitar solo se aplican a las opciones de búsqueda de SNMP y DHCP. Cuando Detección de redes busca dominios, no está limitada por las configuraciones para subredes.  

Si especifica una o más subredes en la pestaña **Subredes** del cuadro de diálogo **Propiedades de detección de redes**, solo se buscarán las subredes marcadas como **Habilitada**.  

Cuando se deshabilita una subred, el sitio la excluye de la detección y se aplican las condiciones siguientes:  

- Las consultas basadas en SNMP no se ejecutan en la subred.  

- Los servidores DHCP no responden con una lista de recursos ubicados en la subred.  

- Las consultas basadas en dominio pueden detectar recursos ubicados en la subred.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Búsqueda en un dominio específico  

Puede configurar Detección de redes para buscar un dominio específico o un conjunto de dominios durante la ejecución de la detección. De forma predeterminada, Detección de redes busca el dominio local del servidor que ejecuta la detección.  

Si especifica uno o más dominios en la pestaña **Dominios** del cuadro de diálogo **Propiedades de detección de redes**, solo se buscarán los dominios marcados como **Habilitado**.  

Cuando se deshabilita un dominio, el sitio lo excluye de la detección y se aplican las condiciones siguientes:  

- Detección de redes no consulta a los controladores de dominio de ese dominio.  

- Las consultas basadas en SNMP pueden continuar ejecutándose en subredes del dominio.  

- Los servidores DHCP pueden responder todavía con una lista de recursos ubicados en el dominio.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Limitación de búsquedas mediante el uso de nombres de comunidad SNMP  

Configure Detección de redes para buscar una comunidad SNMP específica o un conjunto de comunidades durante la ejecución de la detección. De forma predeterminada, el método configura el nombre de comunidad **público**.  

Detección de redes utiliza nombres de comunidad para tener acceso a los enrutadores que son dispositivos SNMP. Un enrutador puede proporcionar Detección de redes con información acerca de otros enrutadores y subredes que están vinculados al primer enrutador.  

> [!NOTE]  
> Los nombres de comunidad SNMP son similares a las contraseñas. Detección de redes puede obtener la información solo de un dispositivo SNMP para el que se ha especificado un nombre de comunidad. Cada dispositivo SNMP puede tener su propio nombre de comunidad, pero a menudo el mismo nombre de comunidad se comparte entre varios dispositivos. Además, la mayoría de los dispositivos SNMP tienen el nombre de comunidad predeterminado **public**. Pero algunas organizaciones eliminan el nombre de comunidad **public** de sus dispositivos como precaución de seguridad.  

Si incluye más de una comunidad SNMP en la pestaña **SNMP** del cuadro de diálogo **Propiedades de detección de redes**, las busca en el orden en el que se muestran. Asegúrese de que los nombres usados con más frecuencia aparecen en la parte superior de la lista. Esta configuración ayuda a minimizar el tráfico de red que el sitio genera cuando intenta ponerse en contacto con un dispositivo mediante el uso de nombres diferentes.

> [!NOTE]  
> Además de usar el nombre de comunidad SNMP, se puede especificar la dirección IP o el nombre que se pueda resolver de un dispositivo SNMP específico. Esta acción se realiza en la pestaña **Dispositivos SNMP** del cuadro de diálogo **Propiedades de detección de redes**.  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Búsqueda en un servidor DHCP específico  

Puede configurar Detección de redes para utilizar un servidor DHCP específico o varios servidores para detectar clientes DHCP durante la ejecución de la detección.  

Detección de redes busca todos los servidores DHCP especificados en la pestaña **DHCP** del cuadro de diálogo **Propiedades de detección de redes** . Si al servidor que ejecuta la detección se le ha concedido la dirección IP desde un servidor DHCP, puede configurar la detección para buscar en ese servidor DHCP. Habilite este comportamiento con la opción **Incluir el servidor DHCP configurado para que el servidor de sitio lo utilice**.  

> [!NOTE]  
> Para configurar correctamente un servidor DHCP en Detección de redes, el entorno debe ser compatible con IPv4. No se puede configurar Detección de redes para usar un servidor DHCP en un entorno nativo de IPv6.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Cómo configurar la detección de redes  

Use los procedimientos siguientes para detectar en primer lugar solo la topología de red y, a continuación, configurar Detección de redes para detectar clientes potenciales mediante una o más de las opciones de Detección de redes disponibles.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a> Determinación de la topología de red  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Métodos de detección**.  

2. Seleccione el método **Detección de redes** para el sitio donde desea detectar recursos de red.  

3. En la pestaña **Inicio** de la cinta de opciones, seleccione **Propiedades**.  

    - En la pestaña **General**, seleccione la opción para **Habilitar la detección de redes**. Luego seleccione **Topología** en las opciones del **Tipo de detección**.  

    - En la pestaña **Subredes**, seleccione la opción **Buscar subredes locales**.  

      > [!TIP]  
      > Si conoce las subredes específicas que componen la red, desactive la casilla **Buscar subredes locales**. Después, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif) y agregue las subredes específicas que se quieren buscar. Para redes grandes, busque solo una o dos subredes al mismo tiempo para minimizar el uso de ancho de banda de red.  

    - En la pestaña **Dominios**, seleccione la opción para **Buscar dominio local**.  

    - En la pestaña **SNMP**, seleccione una opción de la lista desplegable **Número máximo de saltos**. Esta opción especifica cuántos saltos de enrutador puede tardar la Detección de redes en asignar la topología.  

      > [!TIP]  
      > Cuando asigne por primera vez la topología de red, configure pocos saltos del enrutador para minimizar el uso de ancho de banda de red.  

4. En la pestaña **Programación**, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif) y defina una programación para la ejecución de la detección.  

    > [!NOTE]  
    > No se puede asignar una configuración de detección diferente a programaciones de Detección de redes independientes. Cada vez que se ejecuta Detección de redes, utiliza la configuración de detección actual.  

5. Seleccione **Aceptar** para aceptar las configuraciones. Detección de redes se ejecuta a la hora programada.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a> Cómo configurar la detección de redes  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Métodos de detección**.  

2. Seleccione el método **Detección de redes** para el sitio donde desea detectar recursos de red.  

3. En la pestaña **Inicio** de la cinta de opciones, seleccione **Propiedades**.  

4. En la pestaña **General**, seleccione la opción para **Habilitar la detección de redes**.  

    - En las opciones de **Tipo de detección**, seleccione el tipo de detección que desea ejecutar.  

    - Habilite la opción **Red lenta** para que Configuration Manager realice ajustes automáticos de las redes de ancho de banda bajo.  

5. Para configurar la detección para buscar subredes, cambie a la pestaña **Subredes**. Luego configure una o varias de las siguientes opciones:  

    - Para ejecutar la detección de subredes locales en el equipo que ejecuta la detección, habilite la opción para **Buscar subredes locales**.  

    - Para buscar una subred específica, la subred debe aparecer en **Subred a buscar** y tener un valor de **Búsqueda** de **Habilitada**:  

      1. Si la subred no aparece, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Nueva asignación de subred**, escriba la información **Subred** y **Máscara** y luego seleccione **Aceptar**. De forma predeterminada, se habilita una nueva subred para la búsqueda.  

      2. Para cambiar el valor de **búsqueda** de una subred mostrada, selecciónela en la lista. Después, seleccione el icono **Alternar** para cambiar el valor entre **Deshabilitado** y **Habilitado**.  

6. Para configurar la detección para buscar dominios, cambie a la pestaña **Dominios**. Luego configure una o varias de las siguientes opciones:  

    - Para ejecutar la detección en el dominio del equipo que ejecuta la detección, habilite la opción **Buscar dominio local**.  

    - Para buscar un dominio concreto, el dominio debe aparecer en **Dominios** y tener un valor de **Búsqueda** de **Habilitada**:  

      1. Si el dominio no aparece, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Propiedades del dominio**, escriba la información de **Dominio** y seleccione **Aceptar**. De forma predeterminada, se habilita un nuevo dominio para la búsqueda.  

      2. Para cambiar el valor de **búsqueda** de un dominio mostrado, selecciónelo en la lista. Después, seleccione el icono **Alternar** para cambiar el valor entre **Deshabilitado** y **Habilitado**.  

7. Para configurar la detección para buscar nombres de comunidad SNMP específicos para dispositivos SNMP, cambie a la pestaña **SNMP**. Luego configure una o varias de las siguientes opciones:  

    - Para agregar un nombre de comunidad SNMP a la lista **Nombres de comunidades SNMP**, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Nombre de comunidad SNMP nuevo**, especifique el **Nombre** de la comunidad SNMP y luego seleccione **Aceptar**.  

    - Para quitar un nombre de comunidad SNMP, seleccione el nombre de comunidad y luego seleccione el icono **Eliminar**![icono Eliminar](media/Disc_delete_Icon.gif).  

    - Para ajustar el orden de búsqueda de nombres de comunidad SNMP, seleccione un nombre de comunidad de la lista. Luego seleccione el icono **Subir elemento**![icono de mover hacia arriba](media/Disc_moveUp_Icon.gif) o el icono **Bajar elemento**![icono de mover hacia abajo](media/Disc_moveDown_Icon.gif). Cuando se ejecuta la detección, los nombres de comunidad se buscan de arriba a abajo. 

    - Para configurar el número máximo de saltos de enrutador en las búsquedas de SNMP, seleccione el número de saltos en la lista desplegable **Número máximo de saltos**.  

8. Para configurar un dispositivo SNMP, cambie a la pestaña **Dispositivos SNMP**. Si el dispositivo no aparece, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Nuevo dispositivo SNMP**, especifique la dirección IP o el nombre del dispositivo SNMP y luego seleccione **Aceptar**.  

    > [!NOTE]  
    > Si especifica un nombre de dispositivo, Configuration Manager debe ser capaz de resolver el nombre NetBIOS en una dirección IP.  

9. Para configurar la detección para consultar servidores DHCP específicos, cambie a la pestaña **DHCP**. Luego configure una o varias de las siguientes opciones:  

    - Para consultar el servidor DHCP en el equipo que ejecuta la detección, habilite la opción **Always use the site server's DHCP server** (Usar siempre el servidor DHCP del servidor de sitio).  

      > [!NOTE]  
      > Para usar esta opción, el servidor debe conceder su dirección IP desde un servidor DHCP y no puede usar una dirección IP estática.  

    - Para consultar un servidor DHCP específico, seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Servidor DHCP nuevo**, especifique la dirección IP o el nombre del servidor y luego seleccione **Aceptar**.  

      > [!NOTE]  
      > Si especifica un nombre de servidor, Configuration Manager debe ser capaz de resolver el nombre NetBIOS en una dirección IP.  

10. Para configurar cuándo se ejecuta la detección, cambie a la pestaña **Programación**. Seleccione el icono **Nuevo**![icono Nuevo](media/Disc_new_Icon.gif) para configurar una programación para la ejecución de la Detección de redes. Puede configurar varias programaciones periódicas y programaciones sin ninguna periodicidad.  

    > [!NOTE]  
    > Si en la pestaña **Programación** aparece más de una programación al mismo tiempo, la Detección de redes se ejecuta para todas las programaciones conforme a la configuración y a la hora indicada en la programación. Este comportamiento también se aplica a las programaciones periódicas.  

11. Seleccione **Aceptar** para guardar las configuraciones.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Cómo comprobar que se ha completado la detección de redes  

El tiempo necesario para que finalice Detección de redes puede variar en función de uno o varios de los factores siguientes:  

- El tamaño de la red  

- La topología de la red  

- El número máximo de saltos que están configurados para buscar enrutadores en la red  

- El tipo de detección que se está ejecutando  

La Detección de redes no crea mensajes para avisarle cuando haya finalizado. Use el procedimiento siguiente para verificar cuándo ha finalizado la detección:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Expanda **Estado del sistema** y luego seleccione el nodo **Consultas de mensaje de estado**.  

2. Seleccione la consulta **Todos los mensajes de estado**.  

3. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Consultas de mensaje de estado**, seleccione **Mostrar mensajes**.  

4. En la ventana Todos los mensajes de estado, seleccione un valor de la lista desplegable **Seleccionar fecha y hora** que incluye cuánto tiempo hace que se inició la detección. Luego, seleccione **Aceptar** para abrir el **Visor de mensajes de estado de Configuration Manager**.  

    > [!TIP]  
    > También puede usar la opción **Especificar fecha y hora** para seleccionar la fecha y la hora de ejecución de la detección. Esta opción es útil cuando se ejecuta la detección de redes en una determinada fecha y desea recuperar los mensajes solo desde esa fecha.  

5. Para validar la finalización de la detección de redes, busque un mensaje de estado que tenga los siguientes detalles:  

    - Id. de mensaje: **502**  

    - Componente: **SMS_NETWORK_DISCOVERY**  

    - Descripción: **Este componente se ha detenido**  

    Si este mensaje de estado no aparece, Detección de redes no ha terminado.  

6. Para validar el inicio de la detección de redes, busque un mensaje de estado con los detalles siguientes:  

    - Id. de mensaje: **500**  

    - Componente: **SMS_NETWORK_DISCOVERY**  

    - Descripción: **Este componente se ha iniciado**  

    Esta información comprueba el inicio de la detección de redes. Si esta información no aparece, vuelva a programar Detección de redes.  
