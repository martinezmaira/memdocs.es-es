---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1705.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 99a053800971642b1c771329c2ff9b3a29ce7912
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607888"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Funciones de Technical Preview 1705 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1705 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.    

**Problemas conocidos de esta Technical Preview:**
-   **El conector de Operations Management Suite no se actualiza**. Cuando se actualiza desde una versión anterior de Technical Preview que tenía configurado el conector de OMS, este conector no se actualiza y deja de estar disponible en la consola. Después de la actualización, debe [usar el Asistente para servicios de Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) y restablecer la conexión con el área de trabajo de OMS.
-   **Los controladores de Surface no se sincronizan correctamente**. Aunque la compatibilidad para los controladores de Surface se incluye en la sección **Novedades** de la consola de Configuration Manager para la versión preliminar técnica, esta característica aún no funciona según lo previsto.
-   **No se pueden crear directivas de aplazamiento de Windows Update para empresas**. Aunque la posibilidad de configurar directivas de aplazamiento se incluye en la sección **Novedades** de la consola de Configuration Manager para la versión preliminar técnica, el asistente no se abre y no es posible configurar ninguna directiva.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Herramienta de restablecimiento de actualizaciones  
Puede usar la Herramienta de restablecimiento de actualizaciones de Configuration Manager, **CMUpdateReset.exe**, para solucionar los problemas de descarga o replicación de las actualizaciones en la consola. Esta herramienta se incluye con la versión 1705 de Technical Preview. Puede encontrarla en el servidor de sitio del sitio de la versión preliminar técnica tras la instalación de esta, en la carpeta ***\cd.latest\SMSSETUP\TOOLS***.

Esta herramienta se puede utilizar a partir de la versión 1606 de Technical Preview. Se proporciona esta compatibilidad con versiones anteriores a fin de que la herramienta pueda utilizarse en diferentes escenarios de actualización de versiones preliminares técnicas, y sin tener que esperar hasta el lanzamiento de la siguiente versión preliminar técnica.

Se puede utilizar esta herramienta en aquellos casos en que no se haya instalado aún una actualización en consola y esta se encuentre en un estado de error. Un estado de error puede significar que la descarga de la actualización está en curso pero se ha quedado bloqueada y tarda demasiado tiempo, quizá más horas de las que suelen durar los paquetes de actualizaciones de tamaño similar. También puede implicar un error de replicación de la actualización en sitios primarios secundarios.  

Al ejecutar la herramienta, esta se ejecuta con la actualización que especifique. De forma predeterminada, la herramienta no elimina las actualizaciones instaladas o descargadas correctamente.  

### <a name="prerequisites"></a>Requisitos previos
La cuenta que utilice para ejecutar la herramienta requiere los permisos siguientes:
-   Permisos de **lectura** y **escritura** para la base de datos de sitio del sitio de administración central y cada sitio primario de la jerarquía. Para establecer estos permisos, puede agregar la cuenta de usuario como miembro de los [roles fijos de base de datos](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** y **db_datareader** en la base de datos de Configuration Manager de cada sitio. La herramienta no interactúa con los sitios secundarios.
-   **Administrador local** en el sitio de primer nivel de la jerarquía.
-   **Administrador local** en el equipo que hospeda el punto de conexión de servicio.

Necesitará el GUID del paquete de actualización que desea restablecer. Para obtenerlo:
-   En la consola, vaya a **Administración** > **Actualizaciones y mantenimiento**; a continuación, en el panel de información, haga clic derecho en el encabezado de una de las columnas (como **Estado**) y seleccione **GUID de paquete**. Con esta acción se agrega la columna a la pantalla y esta muestra el GUID del paquete de actualización.

> [!TIP]  
> Para copiar el GUID, seleccione la fila del paquete de actualización que desea restablecer y cópiela con CTRL+C. Si pega la selección copiada en un editor de texto, podrá copiar únicamente el GUID para utilizarlo como un parámetro de la línea de comandos al ejecutar la herramienta.

### <a name="run-the-tool"></a>Ejecutar la herramienta    
La herramienta se debe ejecutar en el sitio de primer nivel de la jerarquía.

Al ejecutar la herramienta, se utilizan parámetros de la línea de comandos para especificar el servidor de SQL Server en el sitio de nivel superior de la jerarquía, el nombre de la base de datos de sitio y el GUID del paquete de actualización que desea restablecer. La herramienta entonces identifica los servidores adicionales a los que necesita obtener acceso en función del estado de las actualizaciones.   

Si el paquete de actualización está en un estado *posterior a la descarga*, la herramienta no limpiará el paquete. En ese caso, tiene la opción de forzar la eliminación de una actualización descargada correctamente mediante el parámetro correspondiente (vea los parámetros de la línea de comandos que se tratan más adelante en este mismo tema).

Después de ejecutar la herramienta:
-   Si se eliminó un paquete, reinicie el servicio SMS_Executive de sitios de nivel superior y, a continuación, busque actualizaciones para descargar el paquete de nuevo.
-   Si no se eliminó un paquete, no es necesario realizar ninguna acción, ya que la actualización se reiniciará y comenzará otra vez el proceso de replicación o instalación.

**Parámetros de la línea de comandos:**  


|                        Parámetro                         |                                                            Descripción                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;nombre de dominio completo del servidor de SQL Server de su sitio de nivel superior>** | *Requerido* <br> Debe especificar el nombre de dominio completo del servidor de SQL Server que hospeda la base de datos de sitio de nivel superior de la jerarquía. |
|                **-D &lt;nombre de base de datos >**                 |                             *Requerido* <br> Debe especificar el nombre de la base de datos de los sitios de nivel superior.                             |
|                 **-P &lt;GUID del paquete >**                 |                        *Requerido* <br> Debe especificar el GUID del paquete de actualización que desea restablecer.                        |
|           **-I &lt;nombre de instancia de SQL Server>**           |                   *Opcional* <br> Úselo para identificar la instancia de SQL Server que hospeda la base de datos de sitio.                   |
|                       **-FDELETE**                       |                      *Opcional* <br> Utilice esta opción para forzar la eliminación de un paquete de actualización descargado correctamente.                      |

 **Ejemplos:**  
 En un escenario habitual, querrá restablecer una actualización que tenga problemas de descarga. El nombre de dominio completo de los servidores de SQL Server es *server1.fabrikam.com*, la base de datos de sitio es *CM_XYZ* y el GUID del paquete es *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Ejecute lo siguiente: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 En un escenario más extremo, quizá desee forzar la eliminación del paquete de actualización problemático. El nombre de dominio completo de los servidores de SQL Server es *server1.fabrikam.com*, la base de datos de sitio es *CM_XYZ* y el GUID del paquete es *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Ejecute lo siguiente: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Prueba de la herramienta con Technical Preview  
Esta herramienta se puede utilizar a partir de la versión 1606 de Technical Preview. Se proporciona esta compatibilidad con versiones anteriores a fin de que la herramienta pueda utilizarse con un mayor número de escenarios de actualización de versiones preliminares técnicas, sin tener que esperar hasta el lanzamiento de la siguiente versión preliminar técnica.

Ejecute la herramienta en un paquete de actualización para una versión preliminar técnica antes que esa actualización complete su comprobación de requisitos previos. Cuando se haya completado el estado de comprobación de requisitos previos, el paquete tendrá alguno de los estados siguientes en **Administración** > **Actualizaciones y mantenimiento**:  
-   **Requisitos previos comprobados correctamente**
-   **Comprobación de requisito previo superada con advertencia**
-   **Comprobación de requisito previo no superada**


## <a name="high-dpi-console-support"></a>Compatibilidad de la consola con una configuración elevada de ppp

Con esta versión, los problemas relacionados con el modo en que la consola de Configuration Manager escala y muestra distintas partes de la interfaz de usuario cuando se ven en los dispositivos con una configuración elevada de ppp (como un libro de Surface) deben haberse corregido.


## <a name="peer-cache-improvements"></a>Mejoras de almacenamiento en caché del mismo nivel
A partir de esta versión preliminar técnica, la caché del mismo nivel [ya no utiliza la cuenta de acceso a la red](../plan-design/hierarchy/client-peer-cache.md) para autenticar las solicitudes de descarga de elementos del mismo nivel.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Mejoras de los grupos de disponibilidad AlwaysOn de SQL Server  
Con esta versión, ahora puede usar réplicas de confirmación asincrónica en los grupos de disponibilidad AlwaysOn de SQL Server que usa con Configuration Manager.  Esto significa que puede agregar réplicas adicionales a los grupos de disponibilidad con el fin de usarlas como copias de seguridad externas (remotas) y así utilizarlas en un escenario de recuperación ante desastres.  

- Configuration Manager admite el uso de la réplica de confirmación asincrónica para recuperar una réplica sincrónica.  Vea [las opciones de recuperación de la base de datos de sitio](../servers/manage/recover-sites.md#site-database-recovery-options) en el tema Copia de seguridad y recuperación para obtener información sobre cómo realizar esta tarea.

- Esta versión no admite la conmutación por error para usar la réplica de confirmación asincrónica como la base de datos de sitio.
  > [!CAUTION]  
  > Dado que Configuration Manager no valida el estado de la réplica de confirmación asincrónica para confirmar que está actualizada, y que [por cuestiones de diseño una réplica de este tipo puede no estar sincronizada](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server#AvailabilityModes), el uso de una réplica de confirmación asincrónica como la base de datos de sitio puede poner en peligro la integridad de los datos y del sitio.  

- Puede usar el mismo número y tipo de réplicas en un grupo de disponibilidad en la medida en que lo admita la versión de SQL Server que utilice.   (La compatibilidad anterior se limitaba a dos réplicas de confirmación sincrónica).

### <a name="configure-an-asynchronous-commit-replica"></a>Configuración de una réplica de confirmación asincrónica
Para agregar una réplica asincrónica a un [grupo de disponibilidad que utilice con Configuration Manager](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md), no es necesario ejecutar los scripts de configuración necesarios para configurar una réplica sincrónica. (El motivo es que no se admite el uso de esa réplica asincrónica como la base de datos de sitio). Para más información, vea [Adición de una réplica secundaria a un grupo de disponibilidad Always On](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Uso de la réplica asincrónica para la recuperación del sitio
Antes de usar una réplica asincrónica para recuperar la base de datos de sitio, debe detener el sitio primario activo para evitar escrituras adicionales en la base de datos de sitio. Una vez detenido el sitio, puede utilizar una réplica asincrónica en lugar de una [base de datos recuperada manualmente](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).

Para detener el sitio, puede usar la [herramienta de mantenimiento de jerarquía](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) si desea detener servicios clave en el servidor del sitio. Use la línea de comandos: **Preinst.exe /stopsite**   

Detener el sitio equivale a detener el servicio Administrador de componentes del sitio (sitecomp) seguido por el servicio SMS_Executive en el servidor del sitio.


## <a name="improved-user-notifications-for-microsoft-365-updates"></a>Mejora en las notificaciones de usuario para las actualizaciones de Microsoft 365
Se han hecho mejoras para aprovechar la experiencia de usuario Hacer clic y ejecutar de Office cuando un cliente instala una actualización de Microsoft 365. Esto incluye notificaciones emergentes y en la aplicación y una experiencia de cuenta atrás. Antes de esta versión, cuando se enviaba una actualización de Microsoft 365 a un cliente, las aplicaciones de Office que estaban abiertas se cerraban automáticamente sin previo aviso. Después de esta actualización, las aplicaciones de Office ya no se cerrarán inesperadamente.

### <a name="prerequisites"></a>Requisitos previos
Esta actualización se aplica a los clientes de Aplicaciones de Microsoft 365 para empresas.

### <a name="known-issues"></a>Problemas conocidos
Cuando un cliente evalúa por primera vez una asignación de actualización de Microsoft 365 y la actualización tiene un tiempo límite programado en el pasado, programado inmediatamente o programado para los siguientes 30 minutos, la experiencia del usuario de Microsoft 365 puede ser incoherente. Por ejemplo, es posible que el cliente reciba un cuadro de diálogo de cuenta atrás de 30 minutos para la actualización pero que su aplicación pueda iniciarse de manera efectiva antes del final de la cuenta atrás. Para evitar este comportamiento, tenga en cuenta lo siguiente:
- Implemente la actualización de Microsoft 365 con un tiempo límite de al menos 60 minutos con respecto a la hora actual.
- Configure una ventana de mantenimiento fuera del horario laboral en la recopilación o configure un período de gracia para la aplicación en la implementación.

### <a name="try-it-out"></a>Haga la prueba
Intente realizar las tareas siguientes y luego envíenos sus **comentarios** desde la pestaña **Inicio** de la cinta para comunicarnos si funcionó:
- Implemente en un cliente una actualización de Microsoft 365 con un tiempo límite de al menos 60 minutos después de la hora actual. Observe el nuevo comportamiento en el cliente.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender

[Protección de aplicaciones de Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) es una nueva característica de Windows que ayuda a proteger a los usuarios al abrir los sitios web que no sean de confianza en un contenedor aislado seguro al que no puedan tener acceso otras partes del sistema operativo. En esta versión preliminar técnica, ya se admite la configuración de esta característica mediante las opciones de conformidad de Configuration Manager que establezca para, posteriormente, implementarla en una recopilación.
Esta característica se publicará en la versión preliminar para la versión de 64 bits de Windows 10 Creators Update. Para probar esta característica ahora debe estar utilizando una versión preliminar de esta actualización.


### <a name="before-you-start"></a>Antes de empezar

Para crear e implementar directivas de Protección de aplicaciones de Windows Defender, los dispositivos de Windows 10 en los que implementa la directiva deben configurarse con una directiva de aislamiento de red. Para obtener más información, consulte la entrada de blog a la que se hace referencia más tarde.
Esta funcionalidad solo es aplicable a compilaciones de Windows 10 Insider actuales. Para probarla, los clientes deben ejecutar una compilación reciente de Windows 10 Insider.

### <a name="try-it-out"></a>Haga la prueba

Asegúrese de haber leído la entrada de blog para conocer los conceptos básicos sobre Protección de aplicaciones de Windows Defender.

Para crear una directiva y examinar la configuración disponible:

1.  En la consola de Configuration Manager, elija **Activos y compatibilidad**.
2.  En el área de trabajo **Activos y compatibilidad**, elija **Introducción** > **Endpoint Protection** > **Protección de aplicaciones de Windows Defender**.
3.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Protección de aplicaciones de Windows Defender**.
4.  Con la entrada de blog como referencia, puede examinar y configurar las opciones disponibles para probar la característica.
5.  Cuando haya terminado, complete el asistente e implemente la directiva en uno o varios dispositivos de Windows 10.

### <a name="further-reading"></a>Lectura adicional

Para obtener más información acerca de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Además, para obtener más información sobre el modo independiente de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Nuevas funcionalidades para Azure AD y administración en la nube

En esta versión, puede configurar los servicios en la nube para usar Azure AD a fin de admitir el escenario siguiente:

- Instalación manual del cliente Configuration Manager desde Internet y asignación a un sitio de Configuration Manager.
- Uso de Intune para implementar el cliente de Configuration Manager en dispositivos en Internet.

### <a name="advantages"></a>Ventajas

Con los servicios en la nube y Azure AD, se suprime la necesidad de usar certificados de autenticación del cliente.

Puede detectar usuarios de Azure AD en el sitio para usarlos en las recopilaciones y otras operaciones de Configuration Manager.

### <a name="before-you-start"></a>Antes de empezar

- Debe tener un inquilino de Azure AD.
- Los dispositivos deben ejecutar Windows 10 y estar unidos a Azure AD.  (Además de a Azure AD, los clientes también pueden estar unidos a un dominio).
- Además de los [requisitos previos existentes](../plan-design/configs/site-and-site-system-prerequisites.md) para el rol de sistema de sitio del punto de administración, debe asegurarse de que la plataforma **ASP.NET 4.5** esté habilitada en el equipo que hospeda este rol de sistema de sitio, así como cualquier otra opción que se seleccione automáticamente con esta.
- Para utilizar Microsoft Intune a fin de implementar el cliente de Configuration Manager:
    - Debe tener un inquilino de Intune en funcionamiento (no es necesario que Configuration Manager e Intune estén conectados).
    - En Intune, tiene que haber creado e implementado una aplicación que contenga el cliente de Configuration Manager. Para obtener información sobre este procedimiento, consulte Cómo instalar clientes en dispositivos Windows administrados por MDM con Intune.
- Para usar Configuration Manager para implementar el cliente:
    - Debe haber al menos un punto de administración configurado para el modo HTTPS.
    - Debe configurar una instancia de Cloud Management Gateway.


### <a name="set-up-the-cloud-management-gateway"></a>Configuración de Cloud Management Gateway

Configure Cloud Management Gateway para permitir que los clientes tengan acceso a su sitio de Configuration Manager en Internet sin utilizar certificados.

Encontrará ayuda para hacerlo en los temas siguientes:

- [Planificación de Cloud Management Gateway en Configuration Manager](../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Configurar puerta de enlace de administración en la nube para Configuration Manager](../clients/manage/cmg/setup-cloud-management-gateway.md)
- [Supervisar la puerta de enlace de administración en la nube en Configuration Manager](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md)

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configuración de la aplicación Servicios de Azure en Configuration Manager Cloud Services

Con esta acción se conecta el sitio de Configuration Manager con Azure AD, lo cual es un requisito previo para todas las demás operaciones de esta sección. Para realizar esta tarea:

1. En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Cloud Services** y luego haga clic en **Servicios de Azure**.
2. En la pestaña **Inicio**, en el grupo **Servicios de Azure**, haga clic en **Configurar servicios de Azure**.
3. En la página **Servicios de Azure** del Asistente para servicios de Azure, seleccione **Administración en la nube** para permitir que los clientes se autentiquen en la jerarquía mediante Azure AD.
4. En la página **General** del asistente, especifique un nombre y una descripción para el servicio de Azure.
5. En la página **Aplicación** del asistente, seleccione su entorno de Azure en la lista y, a continuación, haga clic en **Examinar** para seleccionar las aplicaciones de servidor y cliente que se usarán para configurar el servicio de Azure:
   - En la ventana **Aplicación del servidor**, seleccione la aplicación de servidor que quiera usar y, después, haga clic en **Aceptar**. Las aplicaciones de servidor son las aplicaciones web de Azure que contienen las configuraciones de la cuenta de Azure, incluidos el identificador de inquilino, el identificador de cliente y una clave secreta para los clientes. Si no tiene una aplicación de servidor disponible, use una de las siguientes:
       - **Crear**: para crear una aplicación de servidor, haga clic en **Crear**. Proporcione un nombre descriptivo para la aplicación y el inquilino. Después, una vez que inicie sesión en Azure, Configuration Manager crea automáticamente la aplicación web en Azure, incluidos el identificador de cliente y la clave secreta para su uso con la aplicación web. Podrá verlos más adelante desde Azure Portal.
       - **Importar**: para usar una aplicación web que ya existe en su suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el inquilino y, después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web que quiere que use Configuration Manager. Después de comprobar la información, haga clic en **Aceptar** para continuar. Esta opción no está disponible en esta versión Technical Preview.
   - Repita el mismo proceso para la aplicación cliente.

   Deberá conceder el permiso de aplicación *Leer datos de directorio* cuando utilice la importación de la aplicación para establecer los permisos correctos en el portal. Si utiliza la creación de la aplicación, los permisos se crearán automáticamente con la aplicación, pero aún será necesario que dé su consentimiento a la aplicación en Azure Portal.
6. En la página **Detección** del asistente, haga clic si lo desea en **Habilitar la detección de usuarios de Azure Active Directory** y, a continuación, en **Configuración**.
   En el cuadro de diálogo **Configuración de detección de usuarios de Azure AD**, configure una programación para cuando se produce la detección. También puede habilitar la detección de diferencias, que busca únicamente las cuentas nuevas o modificadas en Azure AD.
7. Complete el asistente.

En este momento, ya ha conectado el sitio de Configuration Manager con Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instalación del cliente de CM desde Internet

Antes de empezar, asegúrese de que los archivos de origen de la instalación del cliente están almacenados localmente en el dispositivo en el que desea instalar el cliente.
Después, siga las instrucciones de [Implementar clientes en equipos Windows](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) usando la siguiente línea de comandos de instalación (reemplace los valores del ejemplo por sus propios valores):

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=\<GUID> AADRESOURCEURI=<code>https://contososerver</code>**

- **/NoCrlCheck**: si el punto de administración o la instancia de Cloud Management Gateway usa un certificado de servidor no público, es posible que el cliente no pueda llegar a la ubicación de CRL.
- **/Source**: Carpeta local:   ubicación de los archivos de instalación del cliente.
- **CCMHOSTNAME**: nombre de su punto de administración de Internet. Puede encontrarlo mediante la ejecución de **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** desde un símbolo del sistema en un cliente administrado.
- **SMSMP**: nombre de su punto de administración de búsqueda (puede ser de la intranet).
- **SMSSiteCode**: código de sitio del sitio de Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: identificador y nombre del inquilino de Azure AD vinculados a Configuration Manager. Puede encontrarlos mediante la ejecución de dsregcmd.exe /status desde un símbolo del sistema en un dispositivo unido a Azure AD.
- **AADCLIENTAPPID**: identificador de aplicación de cliente de Azure AD. Para encontrarlo, consulte [Uso del portal para crear una aplicación de Azure Active Directory y una entidad de servicio con acceso a los recursos](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
- **AADResourceUri**: identificador URI de la aplicación de servidor de Azure AD incorporada.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Uso del Asistente para servicios de Azure para configurar una conexión a OMS
A partir de la versión preliminar técnica 1705, se puede usar el **Asistente para servicios de Azure** para configurar la conexión desde Configuration Manager hasta el servicio en la nube de Operations Management Suite (OMS). El asistente reemplaza los flujos de trabajo anteriores para configurar esta conexión.

-   El asistente se utiliza para configurar los servicios en la nube para Configuration Manager, como OMS, la Tienda Windows para empresas (WSfB) y Azure Active Directory (Azure AD).  

-   Configuration Manager se conecta a OMS para utilizar características como Log Analytics o Upgrade Readiness.

### <a name="prerequisites-for-the-oms-connector"></a>Requisitos previos para el conector de OMS
Los requisitos previos para configurar una conexión a OMS son iguales que los [documentados para la versión 1702 de Rama actual](/azure/azure-monitor/platform/collect-sccm). Esa información se repite aquí:  

-   Proporcionar el permiso de Configuration Manager para OMS.

-   El conector de OMS debe instalarse en el equipo que hospeda un [punto de conexión de servicio](../servers/deploy/configure/about-the-service-connection-point.md) en [modo en línea](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

-   Debe instalar Microsoft Monitoring Agent para OMS en el punto de conexión de servicio junto con el conector de OMS. El agente y el conector de OMS deben configurarse para usar el mismo **área de trabajo de OMS**. Para instalar el agente, vea [Descarga e instalación del agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) en la documentación de OMS.
-   Después de instalar el conector y el agente, debe configurar OMS para utilizar datos de Configuration Manager. Para ello, en el Portal de OMS, vea [Importación de recopilaciones de Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Uso del Asistente para servicios de Azure para configurar la conexión a OMS

1.  En la consola, vaya a **Administración** > **Introducción** > **Cloud Services** > **Servicios de Azure** y, después, elija **Configurar servicios de Azure** en la pestaña **Inicio** de la cinta de opciones para iniciar el **Asistente para servicios de Azure**.

2.  En la página **Servicios de Azure**, seleccione el servicio en la nube de Operation Management Suite. Proporcione un nombre descriptivo para el **Nombre del servicio de Azure** y una descripción opcional y, después, haga clic en **Siguiente**.

3.  En la página **Aplicación**, especifique el entorno de Azure (la versión preliminar técnica admite solo la nube pública). A continuación, haga clic en **Examinar** para abrir la ventana de la aplicación de servidor.

4.  Seleccione una aplicación web:

    -   **Importar**: para usar una aplicación web que ya existe en su suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el inquilino y, después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web que quiere que use Configuration Manager. Después de **Comprobar** la información, haga clic en **Aceptar** para continuar.   

    > [!NOTE]   
    > Si configura OMS con esta versión preliminar, OMS solo admite la función de *importación* para una aplicación web. No se admite la creación de una nueva aplicación web. Del mismo modo, no se puede reutilizar una aplicación existente para OMS.

5.  Si ha completado todos los demás procedimientos correctamente, aparecerá automáticamente en esta página la información de la pantalla **OMS Connection Configuration** (Configuración de la conexión de OMS). La información para la configuración de la conexión debería aparecer en **Suscripción de Azure**, **Grupo de recursos de Azure** y **Área de trabajo de Operations Management Suite**.

6.  El asistente se conecta al servicio de OMS con la información que ha especificado. Seleccione las recopilaciones de dispositivos que desea sincronizar con OMS y, a continuación, haga clic en **Agregar**.

7.  Compruebe la configuración de la conexión en la pantalla **Resumen** y luego seleccione **Siguiente**. En la pantalla **Progreso** se muestra el estado de la conexión; después debería seleccionar **Completar**.

8.  Cuando finalice el asistente, la consola de Configuration Manager muestra que ha configurado **Operation Management Suite** como un **Tipo de servicio de nube**.