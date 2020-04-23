---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1709.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3cefbbb9824266fd5fa057a7625332e85ec0ab32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705123"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Funciones de Technical Preview 1709 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1709 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conocidos de esta Technical Preview:**
- **Error al actualizar a la versión preliminar 1709 cuando hay un servidor de sitio en modo pasivo**. Si ejecuta la versión preliminar 1706, 1707 o 1708 y tiene un [servidor de sitio principal en modo pasivo](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), debe desinstalar el servidor de sitio en modo pasivo para poder actualizar correctamente el sitio en versión preliminar a la versión 1709. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio ejecute la versión 1709.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiencia mejorada del perfil VPN en la consola de Configuration Manager
<!-- 1313282 -->
Con esta versión hemos actualizado las páginas de propiedades y el asistente de perfiles VPN para mostrar una configuración más adecuada para la plataforma seleccionada. De manera específica:

- Cada plataforma tiene su propio flujo de trabajo, lo que significa que los nuevos perfiles VPN contienen únicamente la configuración compatible con la plataforma.
- Las páginas **Plataformas admitidas** ahora aparecen después de la página **General**.  Ahora se elige primero la plataforma antes de establecer los valores de propiedad.
- Cuando la plataforma se establece en **Android**, **Android for Work** o **Windows Phone 8.1**, la página **Plataformas admitidas** no es necesaria y no se muestra.
- El flujo de trabajo basado en el cliente de Configuration Manager se ha combinado con los flujos de trabajo de Windows 10 basados en el cliente de dispositivos móviles híbridos (MDM). Ambos admiten la misma configuración.
- Cada flujo de trabajo de la plataforma incluye únicamente las opciones adecuadas para ese flujo de trabajo.  Por ejemplo, el flujo de trabajo de Android contiene configuraciones adecuadas para Android; las configuraciones adecuadas para iOS o Windows 10 Mobile ya no aparecen en el flujo de trabajo de Android.
- Para los dispositivos con Windows 8.1, la configuración administrada por Configuration Manager está claramente marcada.
- La página VPN automática está obsoleta y se ha quitado.

Estos cambios se aplican a los nuevos perfiles VPN.  

Para minimizar el riesgo de compatibilidad, los perfiles VPN existentes no se modifican.  Al editar un perfil existente, la configuración aparece igual que cuando se creó el perfil.  

### <a name="try-it-out"></a>Haga la prueba

Cree un perfil VPN siguiendo el proceso habitual. Tenga en cuenta que la primera página de las opciones del asistente de perfiles VPN ha cambiado.

1. Vaya a **Activos y compatibilidad** > **Introducción** > **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de VPN** y elija **Crear perfil de VPN**.
2. Escriba un nombre en la página **General** y elija una de las opciones siguientes en **Especifique el tipo de perfil VPN que desea crear**:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS y macOS  
    - Android  
    - Android for Work  

3. Si elige **Windows 8.1**, también tiene la opción de **crear un perfil** o de **importar uno desde un archivo**.
4. Siga los pasos del asistente para acabar de crear el perfil.

A medida que seleccione distintas plataformas, observe que solo se muestran las opciones relevantes para la plataforma seleccionada.

## <a name="co-management-for-windows-10-devices"></a>Administración conjunta para dispositivos de Windows 10    
<!-- 1350871 -->
Muchos clientes quieren administrar dispositivos de Windows 10 de la misma manera que administran dispositivos móviles mediante una solución simplificada, basada en la nube y de costo inferior, pero llevar a cabo la transición de la administración tradicional a una administración moderna puede resultar complicado. A partir de Windows 10, versión 1607 (también conocida como la Actualización de aniversario), puede unir un dispositivo Windows 10 a Active Directory (AD) local y a Azure AD basado en la nube al mismo tiempo (Azure AD híbrido). La administración conjunta aprovecha esta mejora y le permite administrar dispositivos Windows 10 de forma simultánea mediante Configuration Manager e Intune. Se trata de una solución que sirve de puente entre la administración tradicional y moderna, y proporciona un camino para realizar la transición con un enfoque por fases. 

### <a name="prerequisites"></a>Requisitos previos
Debe cumplir los siguientes requisitos previos para poder habilitar la administración conjunta. Existen requisitos previos generales y distintos requisitos previos para los clientes existentes de Configuration Manager y dispositivos que no son clientes.

### <a name="known-issues"></a>Problemas conocidos
Después de crear una directiva de administración conjunta, esta no se puede editar. Para cambiar la directiva, elimínela y vuelva a crearla con la configuración que necesite. 

#### <a name="general-prerequisites"></a>Requisitos previos generales
A continuación se indican los requisitos previos generales para poder habilitar la administración conjunta:  

- Technical Preview para la versión 1709 de Configuration Manager
- Azure AD 
- Licencia de EMS o de Intune para todos los usuarios
- Suscripción a Intune &#40;entidad de MDM en Intune establecida en **Intune**&#41;

   > [!Note]  
   > Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Requisitos previos adicionales para los clientes existentes de Configuration Manager
- Windows 10, versión 1709 (Fall Creators Update) y versiones posteriores
- Azure AD híbrido unido (unido a AD y a Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Requisitos previos adicionales para los nuevos dispositivos de Windows 10
- Windows 10, versión 1709 (Fall Creators Update) y versiones posteriores
- [Cloud Management Gateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) en Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabajo que puede pasar a Intune
Después de habilitar la administración conjunta, Configuration Manager sigue administrando todas las cargas de trabajo. Cuando decida que ya está listo, puede hacer que Intune empiece a administrar las cargas de trabajo disponibles. En esta versión puede hacer que Intune administre las siguientes cargas de trabajo.   

#### <a name="compliance-policies"></a>Directivas de cumplimiento
Las directivas de cumplimiento definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional.

#### <a name="windows-update-for-business-policies"></a>Directivas de Windows Update para empresas
Las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. Para obtener más información, vea [Configuración de directivas de aplazamiento de Windows Update para empresas](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Acciones remotas disponibles en Intune para Azure para los dispositivos administrados conjuntamente
Si un dispositivo de Windows 10 está habilitado para la administración conjunta, tiene a su disposición las siguientes acciones remotas de Intune en Azure:  
- [Restablecimiento de la configuración de fábrica](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Borrado selectivo](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Empezar de cero](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Preparar Intune para la administración conjunta
Antes de cambiar las cargas de trabajo de Configuration Manager a Intune, cree los perfiles y las directivas que necesite en Intune para asegurarse de que los dispositivos siguen estando protegidos.
Puede crear objetos en Intune a partir de los objetos que tiene en Configuration Manager. Como alternativa, si su estrategia actual se basa en una administración heredada o tradicional, puede retroceder un paso para reconsiderar qué directivas y perfiles necesita para la administración moderna. Use los siguientes recursos para crear directivas y perfiles.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Directivas de Windows Update para empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Perfiles de configuración de dispositivos](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Introducción a la arquitectura de la administración conjunta
En el siguiente diagrama se muestra una introducción a la arquitectura de la administración conjunta y cómo encaja en las infraestructuras existentes de Intune y de Configuration Manager.

![Diagrama de arquitectura de administración conjunta](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Escenarios para habilitar la administración conjunta  
Puede habilitar la administración conjunta para los dispositivos de Windows 10 inscritos en Microsoft Intune y para los clientes existentes de Configuration Manager que tienen Windows 10. En ambos escenarios, los dispositivos de Windows 10 se administran de forma simultánea con Intune y Configuration Manager, y se unen a AD y a Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Dispositivos inscritos en Intune  
Al inscribir dispositivos de Windows 10 en Intune, puede instalar en ellos el cliente de Configuration Manager (con un argumento de línea de comandos específico) para preparar los clientes para la administración conjunta. Luego podrá habilitar la administración conjunta desde la consola de Configuration Manager para empezar a trasladar cargas de trabajo específicas a Intune para dispositivos específicos de Windows 10.  

Para los dispositivos de Windows 10 que todavía no están inscritos en Intune, puede usar la inscripción automática en Azure para inscribirlos. Para los nuevos dispositivos de Windows 10, puede usar Windows AutoPilot para definir la configuración rápida (OOBE), que incluye la inscripción automática, que inscribe dispositivos en Intune.  

#### <a name="configuration-manager-clients"></a>Clientes de Configuration Manager
Si tiene dispositivos de Windows 10 que son clientes de Configuration Manager, puede inscribirlos y habilitar la administración conjunta desde la consola de Configuration Manager. Configuration Manager desencadena la inscripción automática en Intune en función de la información del inquilino de Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos de Windows 10 para la administración conjunta
Puede habilitar la administración conjunta en los dispositivos de Windows 10 que están unidos a AD y a Azure AD y que están inscritos en Intune y en un cliente en Configuration Manager. Para los nuevos dispositivos de Windows 10 y para los que ya estén inscritos en Intune, instale el cliente de Configuration Manager antes de administrarlos de forma conjunta. Para los dispositivos de Windows 10 que ya son clientes de Configuration Manager, puede inscribirlos en Intune y habilitar la administración conjunta en la consola de Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Línea de comandos para instalar el cliente de Configuration Manager
Cree una aplicación en Intune para los dispositivos de Windows 10 que aún no son clientes de Configuration Manager. Al crear la aplicación en las secciones siguientes, use la siguiente línea de comandos:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway*&#62;/ CCMHOSTNAME=&#60;*Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway*&#62; SMSSiteCode=&#60;*CódigoSitio*&#62; SMSMP=https:&#47;/&#60;*FQDN del MP*&#62; AADTENANTID=&#60;*Id. de inquilino de AAD*&#62; AADTENANTNAME=&#60;*Nombre del inquilino*&#62; AADCLIENTAPPID=&#60;*Id. de aplicación del servidor de integración de AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*Id. de recurso*&#62;”

Por ejemplo, si tuviera los siguientes valores:

- **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Use el valor **MutualAuthPath** en la vista SQL **vProxy_Roles** para el valor **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**.

- **FQDN del punto de administración (MP)** : sccmmp.corp.contoso.com    
- **CódigoDeSitio**: PS1    
- **Id. de inquilino de Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nombre del inquilino de Azure AD**: contoso    
- **Id. de aplicación cliente de Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI de id. de recurso de AAD**: ConfigMgrServer    

  > [!Note]    
  > Use el valor **IdentifierUri** que se encuentra en la vista SQL **vSMS_AAD_Application_Ex** para el valor **URI del Id. de recurso de AAD**.

Usaría la siguiente línea de comandos:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
>Encontrará los parámetros de la línea de comandos del sitio siguiendo estos pasos:     
> 1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).  
> 2. En la pestaña Inicio, en el grupo Administrar, elija **Configurar administración conjunta** para abrir el Asistente para la incorporación de la administración conjunta.    
> 3. En la página de suscripción, haga clic en **Iniciar sesión**, inicie sesión con su inquilino de Intune y haga clic en **Siguiente**.    
> 4. En la página de habilitación, haga clic en **Copiar** en la sección **Devices enrolled in Intune** (Dispositivos inscritos en Intune) para copiar la línea de comandos en el Portapapeles y, luego, guarde la línea de comandos para usarla en el procedimiento en el que se creará la aplicación.  
> 5. Haga clic en **Cancelar** para salir del asistente.

#### <a name="new-windows-10-devices"></a>Nuevos dispositivos de Windows 10
Para los nuevos dispositivos de Windows 10, puede usar el servicio AutoPilot para definir la configuración rápida (OOBE), que incluye la unión del dispositivo a AD y a Azure AD, así como la inscripción del dispositivo en Intune. Luego, cree una aplicación en Intune para implementar el cliente de Configuration Manager.  
1. Habilite AutoPilot para los nuevos dispositivos de Windows 10. Para más información, vea [Resumen de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure la inscripción automática en Azure AD para que los dispositivos se inscriban automáticamente en Intune. Para más información, vea  [Inscripción de dispositivos Windows para Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Cree una aplicación en Intune con el paquete del cliente de Configuration Manager e implemente la aplicación en los dispositivos de Windows 10 que quiera administrar de forma conjunta. Use la [línea de comandos para instalar el cliente de Configuration Manager](#command-line-to-install-configuration-manager-client) cuando siga los pasos para [instalar clientes desde Internet mediante Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos de Windows 10 no inscritos en Intune o en un cliente de Configuration Manager
Para los dispositivos de Windows 10 que no están inscritos en Intune o que tienen el cliente de Configuration Manager, puede usar la inscripción automática para inscribirlos en Intune. Luego, cree una aplicación en Intune para implementar el cliente de Configuration Manager.
1. Configure la inscripción automática en Azure AD para que los dispositivos se inscriban automáticamente en Intune. Para más información, vea  [Inscripción de dispositivos Windows para Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Cree una aplicación en Intune con el paquete del cliente de Configuration Manager e implemente la aplicación en los dispositivos de Windows 10 que quiera administrar de forma conjunta. Use la [línea de comandos para instalar el cliente de Configuration Manager](#command-line-to-install-configuration-manager-client) cuando siga los pasos para [instalar clientes desde Internet mediante Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos de Windows 10 inscritos en Intune
Para los dispositivos de Windows 10 que ya están inscritos en Intune, cree una aplicación en Intune para implementar el cliente de Configuration Manager. Use la [línea de comandos para instalar el cliente de Configuration Manager](#command-line-to-install-configuration-manager-client) cuando siga los pasos para [instalar clientes desde Internet mediante Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Cambiar las cargas de trabajo de Configuration Manager a Intune
En la sección anterior ha preparado dispositivos de Windows 10 para la administración conjunta. Estos dispositivos ahora están unidos a AD y a Azure AD, están inscritos en Intune y tienen el cliente de Configuration Manager. Es probable que aún tenga dispositivos de Windows 10 unidos a AD y que tenga el cliente de Configuration Manager, pero no que esté unido a Azure AD ni inscrito en Intune. En el siguiente procedimiento se proporcionan los pasos necesarios para habilitar la administración conjunta y preparar el resto de los dispositivos de Windows 10 (clientes de Configuration Manager sin la inscripción de Intune) para la administración conjunta. También podrá empezar a trasladar a Intune determinadas cargas de trabajo de Configuration Manager.

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).    
2. En la pestaña Inicio, en el grupo Administrar, elija **Configurar administración conjunta** para abrir el Asistente para la incorporación de la administración conjunta.    
3. En la página de suscripción, haga clic en **Iniciar sesión**, inicie sesión con su inquilino de Intune y haga clic en **Siguiente**.   
4. En la página de almacenamiento provisional, configure las opciones siguientes y haga clic en **Siguiente**:
    - **Grupo piloto**: el grupo piloto contiene una o varias colecciones que seleccione. Use este grupo como parte de la implementación por fases de la administración conjunta. Puede comenzar con un conjunto de prueba pequeños y, luego, agregar más colecciones al grupo piloto a medida que implemente la administración conjunta en más usuarios y dispositivos. Puede cambiar las colecciones del grupo piloto en cualquier momento desde las propiedades de la administración conjunta.
    - **Production**: al seleccionar esta opción, se habilitan todos los dispositivos Windows 10 compatibles para la administración conjunta. Configure el **grupo de exclusión** con una o varias colecciones. Los dispositivos que forman parte de cualquiera de las colecciones de este grupo se excluyen del uso de la administración conjunta. 
5. En la página de habilitación, elija **Piloto** o **Todo** (en función de los valores configurados en la página de almacenamiento provisional) para habilitar la inscripción automática en Intune y, luego, haga clic en **Siguiente**. Si elige **Piloto**, solo los clientes de Configuration Manager que sean miembros del grupo piloto se inscribirán automáticamente en Intune. De esta manera podrá habilitar la administración conjunta en un subconjunto de clientes para probarla inicialmente e implementarla con un enfoque por fases. 
6. En la página Cargas de trabajo, elija si quiere cambiar las cargas de trabajo de Configuration Manager para que las administre Intune. Luego, haga clic en **Siguiente**. Use los controles deslizantes para seleccionar si se debe cambiar la carga de trabajo al grupo piloto o para todos los clientes de Windows 10 (en función de los valores configurados en la página de almacenamiento provisional). 
7. Para habilitar la administración conjunta, siga los pasos del asistente.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Vea también
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md). 
