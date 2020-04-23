---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1712.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705083"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Funciones de Technical Preview 1712 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1712 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. 

Repase [Technical Preview de Configuration Manager](technical-preview.md) antes de instalar esta versión de Technical Preview. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problemas conocidos de esta Technical Preview:**
- **La actualización a una nueva versión preliminar no se puede realizar cuando hay un servidor de sitio en modo pasivo**. Si tiene un [servidor de sitio primario en modo pasivo](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), debe desinstalarlo antes de actualizar a esta nueva versión preliminar. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio finalice la actualización.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola de Configuration Manager vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms489412-->


**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>No actualizar automáticamente las aplicaciones reemplazadas
<!-- 1351266 -->
En función de sus [comentarios de User Voice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), en esta versión tiene la opción de configurar una implementación de aplicación para no actualizar automáticamente ninguna versión reemplazada. Ahora, al crear la implementación, en la página **Configuración de implementación** del **Asistente para implementar software**, para cada propósito de instalación **Disponible** o **Requerido**, puede habilitar o deshabilitar la opción **Actualizar automáticamente cualquier versión reemplazada de esta aplicación**.


## <a name="install-multiple-applications-in-software-center"></a>Instalar varias aplicaciones en el Centro de software
<!-- 1357126 -->
Si un usuario final o técnico de escritorio necesita instalar varias aplicaciones en un dispositivo, ahora en el Centro de software se admite la instalación de varias aplicaciones seleccionadas. Esto permite que el usuario sea más eficaz, al no tener que esperar a que finalice una instalación antes de iniciar la siguiente.

Al usar el modo de selección múltiple en la pestaña **Aplicaciones**, los criterios siguientes determinan qué aplicaciones del Centro de software permiten la selección múltiple:
- La aplicación es visible para el usuario
- La aplicación ya no está instalada
- La aprobación del administrador no es necesaria o ya se ha concedido
- El estado de la aplicación está disponible (por ejemplo, todavía no descarga contenido)

### <a name="try-it-out"></a>Haga la prueba
**En la consola de Configuration Manager:** implemente varias aplicaciones en un dispositivo o usuario para la instalación, como disponibles o requeridas (con la fecha límite en el futuro). No se requiere la aprobación del administrador. Para obtener más información, consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).

**En el Centro de software:**
 1. La pestaña **Aplicaciones** se debe abrir de forma predeterminada. 
 2. Para entrar en modo de selección múltiple en la vista de lista, haga clic en el nuevo icono ![Icono de selección múltiple del Centro de software](media/software-center-multi-select-apps.png) en la esquina superior derecha.
 3. Seleccione dos o más aplicaciones para instalar activando la casilla situada la izquierda de las aplicaciones en la lista.
 4. Haga clic en el botón **Instalar seleccionadas**.

Las aplicaciones se instalan como de costumbre, pero ahora de forma sucesiva.


## <a name="client-based-pxe-responder-service"></a>Servicio del respondedor PXE basado en cliente
<!-- 1357148 -->
Un reto común para los clientes es proporcionar servicios PXE en oficinas remotas o sucursales con poca o ninguna infraestructura de servidor. El rol de punto de distribución admite los sistemas operativos de cliente, pero no se puede habilitar para PXE debido a la dependencia de los Servicios de implementación de Windows.

La configuración de cliente nueva ahora está disponible para habilitar un servicio del respondedor PXE en los clientes de Configuration Manager. Una imagen de arranque habilitada para PXE debe residir en la memoria caché del cliente del respondedor PXE.

### <a name="try-it-out"></a>Haga la prueba
Asegúrese de que no haya ningún punto de distribución habilitado para PXE existente u otros servidores PXE en el entorno de prueba que puedan entrar en conflicto con este respondedor PXE de cliente.

En la consola de Configuration Manager:
1. En el área de trabajo **Biblioteca de software** bajo **Sistemas operativos**, **Secuencias de tareas**: cree una secuencia de tareas mediante la plantilla personalizada.
   1. Haga clic en **Agregar**, seleccione **General** y, después, el paso **Configurar variable de secuencia de tareas**. Escriba **SMSTSPersistContent** como la variable de secuencia de tareas y el valor **TRUE**.
   1. Haga clic en **Agregar**, seleccione **Software** y, después, el paso **Descargar contenido de paquete**. Haga clic en el asterisco dorado y seleccione una imagen de arranque habilitada con PXE. Incluya imágenes de arranque x86 y x64. Configure el paso para colocarlo en la **memoria caché del cliente de Configuration Manager**.
   1. Haga clic en **Agregar**, seleccione **General** y, después, el paso **Configurar variable de secuencia de tareas**. Escriba **SMSTSPreserveContent** como la variable de secuencia de tareas y el valor **TRUE**.
2. En el área de trabajo **Administración** bajo **Configuración de cliente**: cree una directiva de configuración de dispositivos de cliente personalizada.
   1. Seleccione el grupo **Configuración de caché de cliente**.
   1. Establezca la opción **Habilitar el cliente de Configuration Manager en el SO completo para compartir contenido** en **Sí**.
   1. Establezca la opción **Habilitar servicio del respondedor PXE** en **Sí**.
   1. Para la opción **Crear un certificado autofirmado o importar un certificado de cliente PKI**, haga clic en **Proporcionar un certificado**. Seleccione **Importar certificado** si el entorno de prueba tiene PKI; en caso contrario, haga clic en **Aceptar** para crear un certificado autofirmado. 
   1. Configure las opciones restantes según sea necesario para el entorno de prueba. (La configuración predeterminada debería funcionar a menos que haya requisitos específicos de red o de seguridad).
3. Implemente la secuencia de tareas y la configuración de cliente personalizada en una colección de los clientes de destino como respondedores PXE. Espere a que se apliquen las directivas y se ejecute la secuencia de tareas.
4. Inicie otro cliente en la misma subred para el arranque normal de PXE o de la red.

### <a name="known-issues"></a>Problemas conocidos
- El editor de secuencia de tareas muestra un icono de error de color rojo para el paso **Descargar contenido de paquete** al agregar una imagen de arranque, pero la secuencia de tareas se guarda correctamente. Al volver a abrir esta secuencia de tareas en el editor también se muestra una advertencia inofensiva sobre objetos a los que se hace referencia que no se encuentran. <!-- sms427542 -->
- La imagen de arranque del paso Descargar contenido de paquete no se muestra en la lista de referencias de la secuencia de tareas personalizada. Tampoco está disponible la acción **Distribuir contenido**. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Cambio en la instalación del cliente de Configuration Manager  
Como resultado de los comentarios de User Voice, [Silverlight ya no se instala automáticamente en los clientes.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Cambio en el panel de dispositivos Surface
Ahora, en el panel de Surface se muestran las versiones de firmware para los dispositivos Surface en lugar de la versión del sistema operativo. En la consola, vaya a **Supervisión** > **Dispositivos Surface**. Puede ver los elementos siguientes:
- El porcentaje de dispositivos Surface
- El porcentaje de modelos Surface
- Las primeras cinco versiones de firmware
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Mejoras en el panel de administración de clientes de Office 365 
Ahora, en el panel de administración de clientes de Office 365 se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico. En la consola, vaya a **Biblioteca de software** >**Información general** >**Administración de clientes de Office 365**. El panel se muestra en la parte derecha. Al seleccionar criterios en el gráfico se muestra una lista de dispositivos.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Mejoras en la consola de Configuration Manager 
Se han realizado las siguientes mejoras en la consola de Configuration Manager, que son consecuencia de los comentarios de User Voice.

- [En la lista de dispositivos se muestra el usuario primario](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): En las listas de dispositivos bajo Activos y compatibilidad, Dispositivos, ahora se muestra el usuario primario de forma predeterminada. También se puede agregar el último usuario que inició sesión como columna opcional. <!-- 1357280 -->
- [Las recopilaciones que se han cambiado de nombre se muestran en las reglas de pertenencia de recopilación existentes](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Si una recopilación es miembro de otra y se cambia de nombre, el nuevo nombre se actualiza en las reglas de pertenencia.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Mejoras en la implementación de sistema operativo
Se han realizado las siguientes mejoras en la implementación del sistema operativo, algunas de las cuales son el resultado de los comentarios de los usuarios.
- [Visor de registros predeterminado en la imagen de arranque](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): En Windows PE, al iniciar cmtrace.exe, ya no se le solicita que elija si este programa se debe establecer como el visor predeterminado para los archivos de registro. <!-- SMS 500897 -->
- Paso Descargar contenido de paquete: ahora se pueden agregar imágenes de arranque a este paso de secuencia de tareas.


## <a name="windows-10-feedback-hub-app-integration"></a>Integración de la aplicación Centro de opiniones de Windows 10

Nos gusta tanto recibir comentarios que ahora se permiten a través de la [aplicación Centro de opiniones](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) integrada en Windows 10. Cuando **agregue nuevos comentarios**, no olvide seleccionar la categoría **Enterprise Management** y, después, elija una de las subcategorías siguientes:
- Cliente de Configuration Manager
- Consola de Configuration Manager
- Implementación del sistema operativo de Configuration Manager
- Servidor de Configuration Manager

Siga usando nuestra [página User Voice](https://configurationmanager.uservoice.com/) para votar nuevas ideas de características en Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
