---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1801.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074221"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Funciones de Technical Preview 1801 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1801 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. 

Repase [Technical Preview de Configuration Manager](technical-preview.md) antes de instalar esta versión de Technical Preview. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


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
  <!--sms 489412-->


**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Creación de implementaciones por fases
<!-- 1357405 -->
Las implementaciones por fases automatizan una implementación coordinada y secuencial de software sin necesidad de crear varias implementaciones. En esta versión Technical Preview, se puede completar el Asistente para la implementación por fases para secuencias de tareas en la consola de administración. Pero las implementaciones no se crean. 

### <a name="try-it-out"></a>Haga la prueba  
  Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.
 
**Creación de una implementación por fases para una secuencia de tareas** </br>
1. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.
2. Haga clic con el botón derecho en una secuencia de tareas existente y seleccione **Create Phased Deployment** (Crear implementación por fases). 
3. En la pestaña **General** asigne un nombre y una descripción (opcional), a la implementación por fases y seleccione **Automatically create default pilot and production phases** (Crear automáticamente las fases de prueba y de producción predeterminadas). 
4. Rellene los campos **Recopilación piloto** y **Recopilación de producción**. Seleccione **Siguiente**.
5. En la pestaña **Configuración**, elija una opción para cada una de las opciones de programación y haga clic en **Siguiente** cuando haya terminado. 
6. En la pestaña **Fases**, modifique cualquiera de las fases si es necesario y después haga clic en **Siguiente**.
7. Confirme las selecciones en la pestaña **Resumen** y después haga clic en **Siguiente** para continuar.

## <a name="co-management-reporting"></a>Informes de administración conjunta
<!-- 1356648 -->
Si usa las funcionalidades de [administración conjunta](../../comanage/overview.md), ahora puede ver un panel con información sobre la administración conjunta en su entorno. En la consola de Configuration Manager, navegue hasta el área de trabajo **Supervisión**, expanda **Upgrade Readiness** y seleccione el panel **Administración conjunta**. En el panel se incluyen los iconos siguientes:
- **Dispositivos administrados conjuntamente**: el porcentaje de dispositivos en el entorno que se han habilitado para la administración conjunta.
- **Distribución del sistema operativo**: el desglose de los sistemas operativos (SO) por versión. En este gráfico se usan las siguientes agrupaciones:
  - Windows 7 y 8.x
  - Windows 10 anterior a la versión 1709
  - Windows 10 1709 y versiones posteriores
    > [!NOTE] 
    > Windows 10, versión 1709 y versiones posteriores, es un requisito previo para la administración conjunta
- **Co-management status** (Estado de la administración conjunta): el desglose de los dispositivos que se ejecutan correctamente o con error en las siguientes categorías:
   - Se ejecuta correctamente, Unidos a Azure AD híbrido
   - Se ejecuta correctamente, Unido a Azure AD
   - Error: Error de inscripción automática
- **Workload transition** (Transición de la carga de trabajo): un gráfico de barras en el que se muestra el número de dispositivos que se han pasado a Microsoft Intune para las tres cargas de trabajo disponibles: 
   - Directivas de cumplimiento
   - Acceso a los recursos
   - Windows Update para empresas

### <a name="prerequisites"></a>Requisitos previos
- En el equipo que ejecuta la consola de Configuration Manager se necesita Internet Explorer 9 o una versión posterior.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Mejoras en la programación de evaluación de reglas de implementación automática
<!-- 1357133 -->
En función de los [comentarios de UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), ahora puede programar la evaluación de reglas de implementación automática (ADR) para que se desplacen con respecto a un día base. Por ejemplo, un desplazamiento de dos días después del segundo martes del mes se evalúa como la regla del jueves. 

### <a name="try-it-out"></a>Haga la prueba  
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado. <br/>

**Creación de una programación personalizada para la evaluación y desplazamiento de ADR desde un día base** </br>
1.  En el área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y haga clic en **Reglas de implementación automática**.
2. Haga clic con el botón derecho en **Reglas de implementación automática** y elija **Crear regla de implementación automática**. 
3. Siga las indicaciones para completar las pestañas **General**, **Configuración de implementación** y **Actualizaciones de software**. 
4. En la pestaña **Programación de evaluación**, haga clic en **Ejecutar la regla en una programación** y **Personalizar**.
5. Para la programación personalizada, seleccione **Mensual** y un día base, por ejemplo, el segundo martes. 
6. Active **Desplazamiento (días)** y el número de días para el desplazamiento, y después haga clic en **Aceptar** cuando termine.  
7. Complete el resto del **Asistente para crear regla de implementación automática**. 



## <a name="reassign-distribution-point"></a>Reasignación del punto de distribución
<!-- 1306937 -->
Muchos clientes tienen grandes infraestructuras de Configuration Manager y reducen los sitios primarios o secundarios para simplificar su entorno. Tienen que conservar los puntos de distribución en las ubicaciones de las sucursales para entregar el contenido a los clientes administrados. Estos puntos de distribución a menudo contienen varios terabytes o más de contenido. Este contenido es costoso en términos de tiempo y ancho de banda de red para distribuirlo entre estos servidores remotos. 

Esta característica permite volver a asignar un punto de distribución a otro sitio primario sin redistribuir el contenido. Esta acción actualiza la asignación del sistema de sitio mientras se conserva todo el contenido en el servidor. Si necesita volver a asignar varios puntos de distribución, en primer lugar realice esta acción en un único punto de distribución y, después, continúe con otros servidores de uno en uno.

> [!IMPORTANT]
> El servidor de sistema de sitio solo puede hospedar el rol de punto de distribución. Si el servidor de sistema de sitio hospeda otro rol de servidor de Configuration Manager, como el punto de migración de estado, el punto de distribución no se puede reasignar. No se puede reasignar un punto de distribución de nube. 

Esta opción no es funcional con esta versión debido al límite de Technical Preview de un solo sitio primario. Considere el escenario y, después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta, con respecto a las funcionalidades de esta acción.
1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**.
2. Haga clic con el botón derecho en el punto de distribución de destino y seleccione **Reasignar punto de distribución**. 
  ![Reasignación de un punto de distribución](media/1306937-reassign-dp.png)
3. Seleccione el servidor de sitio y el código de sitio al que quiera reasignar este punto de distribución. 
  ![Selección de un servidor de sitio](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Mejoras en el inventario de hardware
<!-- 1357389 -->
Para las clases recién agregadas, se pueden especificar longitudes de cadena mayores de 255 caracteres para las propiedades de inventario de hardware que no sean claves.

### <a name="try-it-out"></a>Haga la prueba  
Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.<br/>

1. En el área de trabajo **Administración**, haga clic en **Configuración de cliente**, resalte una configuración de dispositivo cliente para modificar, haga clic con el botón derecho y, después, seleccione **Propiedades**. 
2. Seleccione **Inventario de hardware**, después **Establecer clases** y haga clic en **Agregar**.
3. Haga clic en el botón **Conectar**.
4. Rellene **Nombre de equipo** y **Espacio de nombres WMI**, y seleccione **Recurrente** si es necesario. Proporcione las credenciales si es necesario para conectarse. Haga clic en **Conectar** para ver las clases del espacio de nombres.
5. Seleccione una clase nueva y después haga clic en **Editar**.
6. Cambie la **Longitud** de al menos una propiedad que sea una cadena, que no sea la clave, para que sea mayor de 255. Haga clic en **Aceptar**. 
7. Asegúrese de que esté seleccionada la propiedad modificada para **Agregar clase de inventario de hardware** y haga clic en **Aceptar**. 
8. Recopile el inventario de hardware con la clase recién agregada que contiene una propiedad de más de 255 caracteres de longitud. 



## <a name="improvements-to-client-settings-for-software-center"></a>Mejoras en la configuración de cliente para el Centro de software
<!-- 1351224 & 1355146 -->
En esta versión de Technical Preview, se han realizado mejoras para la personalización del Centro de software en la configuración del cliente. 

1. La configuración de cliente para el Centro de software ahora tiene un botón **Personalizar**.
2. Se ha agregado una vista previa para mostrar el aspecto del banner del Centro de software.<!--1351224-->
    - Si no se selecciona un logotipo, en la vista previa se muestra el texto del nombre y el color de empresa.
    - Si se selecciona un logotipo, en la vista previa se muestra el logotipo y el texto del nombre de la empresa.  
3.  **Ocultar las aplicaciones no aprobadas en el Centro de software** es una nueva configuración para el Centro de software. Cuando esta opción está habilitada, las aplicaciones disponibles para los usuarios que necesiten aprobación se ocultan en el Centro de software.<!--1355146-->

### <a name="try-it-out"></a>Haga la prueba  
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. En el área de trabajo **Administración**, haga clic en **Configuración de cliente**. Seleccione una configuración de dispositivo cliente para modificar. Haga clic con el botón derecho en ella, seleccione **Propiedades** y después **Centro de software**.
2.  Haga clic en el botón **Personalizar**. Pruebe las diferentes opciones de personalización, incluida la vista previa.
3. Habilite la opción **Ocultar aplicaciones no aprobadas en el Centro de software**. Observe los cambios en el Centro de software. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Nueva configuración de Protección de aplicaciones de Windows Defender
<!-- 1356256 -->
Para Windows 10 versión 1709 y dispositivos posteriores, hay dos nuevas opciones de interacción de host para [Protección de aplicaciones de Windows Defender](../../protect/deploy-use/create-deploy-application-guard-policy.md). 
1. A los sitios web se les puede conceder acceso al procesador de gráficos virtuales del host. 
2. Los archivos descargados en el contenedor se pueden conservar en el host. </br>



## <a name="improvements-to-run-scripts"></a>Mejoras para ejecutar scripts
<!-- 1236459 -->
Ahora la [característica **Ejecutar scripts**](../../apps/deploy-use/create-deploy-scripts.md) permite importar y ejecutar scripts de PowerShell firmados. 
- Para mantener la integridad de los scripts, los scripts firmados deben importarse en lugar de usar copiar y pegar. 
- Los scripts firmados importados no se pueden modificar después de la importación.
    
>[!IMPORTANT]
>En esta versión Technical Preview, hay dos limitaciones temporales.
>- Los scripts solo se pueden importar mediante la característica Ejecutar scripts y no se pueden modificar directamente desde la consola.
>- Es posible que los scripts que se importan con una codificación que no sea Unicode no se muestren correctamente en la consola. El script se ejecutará como se haya escrito originalmente.





## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
