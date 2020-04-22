---
title: Supervisar el uso de aplicaciones a través de la medición de software
titleSuffix: Configuration Manager
description: Conozca las operaciones que están disponibles en la medición de software de Configuration Manager.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689253"
---
# <a name="software-metering-in-configuration-manager"></a>Medición de software de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este tema contiene una referencia a todas las operaciones que puede realizar al usar la medición de software de Configuration Manager.

> [!IMPORTANT]
>  La medición de software se usa para supervisar aplicaciones de escritorio de PC Windows con un nombre de archivo que terminan en **.exe**. La medición de software no supervisa las aplicaciones modernas de Windows (como las que usa Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Requisitos previos para la medición de software
La medición de software no tiene dependencias externas, solo dependencias dentro del producto.

|Dependencia|Más información|
|----------------|----------------------|
|Configuración de cliente para la medición de software.|Para usar la medición de software, la configuración de cliente **Habilitar disponibilidad de software en clientes** debe estar habilitada e implementada en los equipos. Puede implementar la configuración de la medición de software en todos los equipos de la jerarquía, o puede implementar configuraciones personalizadas en grupos de equipos. Consulte **Configurar la medición de software** en este tema.|
|El punto de servicios de informes.|Debe configurar un punto de servicios de informes antes de poder ver los informes de medición de software. Para obtener más información, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Configurar la medición de software
 En este procedimiento se define la configuración predeterminada de cliente para la medición de software y se aplica a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada e impleméntela en una recopilación que contenga los equipos en los que quiere usar la medición de software. Para obtener más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración del cliente](../../core/clients/deploy/configure-client-settings.md).

1. En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.

2. En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.

3. En el cuadro de diálogo **Configuración predeterminada** , haga clic en **Disponibilidad de software**.

4. En la lista **Configuración de dispositivo** , configure lo siguiente:

   -   **Habilitar disponibilidad de software en clientes**: seleccione **Verdadero** para habilitar la medición de software.

   -   **Programar la recopilación de datos**: configure con qué frecuencia se recopilan datos de medición de software de los equipos cliente. Use el valor predeterminado de cada **7 días** o haga clic en **Programación** para especificar una programación personalizada.

5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración predeterminada** .

   Los equipos cliente se configuran con estas opciones la próxima vez que descargan directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a>Crear reglas de medición de software
 Use el Asistente para crear regla de disponibilidad de software para crear una nueva regla de disponibilidad de software para su sitio de Configuration Manager.

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Medición de software**.

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear regla de disponibilidad de software**.

4.  En la página **General** del Asistente para crear regla de disponibilidad de software, especifique la información siguiente:

    -   **Nombre** : el nombre de la regla de medición de software. Debe ser único y descriptivo.

        > [!NOTE]
        >  Las reglas de medición de software pueden compartir el mismo nombre si el nombre de archivo contenido en las reglas es diferente.

    -   **Nombre de archivo** : el nombre del archivo del programa que quiere medir. Puede hacer clic en **Examinar** para mostrar el cuadro de diálogo **Abrir** , en el que puede seleccionar el archivo de programa que quiere usar.

        > [!NOTE]
        >  Si escribe el nombre del archivo ejecutable en el cuadro **Nombre de archivo** , no se efectúan comprobaciones para determinar si existe el archivo o si contiene la información de encabezado necesaria. Cuando sea posible, haga clic en **Examinar** y seleccione el archivo ejecutable que se debe medir.
        >
        >  No se permiten caracteres comodín en el nombre de archivo.
        >
        >  Este cuadro es opcional si se especifica un valor para **Nombre original del archivo** .

    -   **Nombre original del archivo** : el nombre del archivo ejecutable que quiere medir. Este nombre coincide con la información en el encabezado del archivo, no con el propio nombre de archivo, por lo que puede ser útil en los casos en que ha cambiado el nombre del archivo ejecutable que quiere medirlo por el nombre original.

        > [!NOTE]
        >  No se permiten caracteres comodín en el nombre original del archivo.
        >
        >  Este cuadro es opcional si se especifica un valor para **Nombre de archivo** .

    -   **Versión** : la versión del archivo ejecutable que quiere medir. Puede usar el carácter comodín ( &#42; ) para representar cualquier cadena de caracteres o el carácter comodín ( ? ) para representar un solo carácter. Si quiere medir todas las versiones de un archivo ejecutable, use el valor predeterminado ( &#42; ).

    -   **Idioma** : el idioma del archivo ejecutable que se va a medir. El valor predeterminado es la configuración regional actual del sistema operativo que está usando. Si selecciona un archivo ejecutable para la medición haciendo clic en el botón **Examinar** , este cuadro se rellena automáticamente si la información del idioma está presente en el encabezado del archivo. Para medir todas las versiones de idioma de un archivo, seleccione **Cualquiera** en la lista desplegable.

    -   **Descripción** : una descripción opcional para la regla de medición de software.

    -   **Aplicar esta regla de disponibilidad de software a los clientes siguientes** : seleccione si quiere aplicar la regla de medición de software a todos los clientes en la jerarquía o a los clientes que están asignados al sitio especificado en la lista **Sitio** .

5.  Para continuar, haga clic en **Siguiente**.

6.  Revise y confirme la configuración y, a continuación, complete el asistente para crear regla de medición de software. La nueva regla de medición de software se muestra en el nodo **Disponibilidad de software** en el área de trabajo **Activos y compatibilidad** .

##  <a name="configure-automatic-software-metering-rules"></a>Configurar reglas de medición de software automáticas
 Puede configurar la medición de software en Configuration Manager para generar automáticamente reglas de medición de software deshabilitadas a partir de los datos de inventario de uso reciente en la base de datos del sitio. Puede configurar estos datos de inventario para que únicamente se creen reglas de medición para aplicaciones que se usan en un porcentaje especificado de equipos. También puede especificar el número máximo de reglas de medición de software generadas automáticamente que se permiten en el sitio.

> [!NOTE]
>  De forma predeterminada, las reglas de medición de software que se crean automáticamente están deshabilitadas. Antes de que pueda empezar a recopilar datos de uso con estas reglas, debe habilitarlas.

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Medición de software** y, luego, en la pestaña **Inicio** del grupo **Configuración**, haga clic en **Propiedades de disponibilidad de software**.

3.  En el cuadro de diálogo **Propiedades de disponibilidad de software** , configure lo siguiente:

    -   **Retención de datos (en días)** : especifica la cantidad de tiempo que se conserva los datos generados por las reglas de medición de software en la base de datos del sitio. El valor predeterminado es **90** días.

    -   Habilite la opción **Crear automáticamente reglas de disponibilidad deshabilitada a partir de datos de inventario de uso reciente**.

    -   **Especificar el porcentaje de equipos de la jerarquía que debe usar un programa antes de que se cree automáticamente una regla de disponibilidad de software** : el valor predeterminado es **10** por ciento.

    -   **Especifique el número de reglas de disponibilidad de software que debe superarse en la jerarquía antes de que se deshabilite la creación automática de reglas** : el valor predeterminado es **100** reglas.

4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de disponibilidad de software** .

##  <a name="manage-software-metering-rules"></a>Administrar reglas de medición de software
 En el área de trabajo **Activos y compatibilidad** , seleccione **Disponibilidad de software**, seleccione la regla de medición de software que quiere administrar y, a continuación, seleccione una tarea de administración.

 Utilice la tabla siguiente para obtener más información acerca de las tareas de administración que pueden requerir información para poder seleccionarlas.

|Tarea de administración|Detalles|
|---------------------|-------------|
|**Habilitar**<br /><br /> **Deshabilitar**|Habilita o deshabilita una regla de medición de software. Esta configuración se descarga en los equipos cliente según el **Intervalo de sondeo de directiva de cliente** de la sección **Directiva de cliente** de la configuración de cliente (de forma predeterminada, cada 60 minutos).<br /><br /> Vea [Configure client settings](../../core/clients/deploy/configure-client-settings.md) (Configuración de las opciones del cliente).|

##  <a name="monitor-software-metering"></a>Supervisión de la medición de software
 La medición de software en Configuration Manager incluye una serie de informes integrados que permiten supervisar información sobre operaciones de medición de software. Estos informes tienen la categoría de informe **Disponibilidad de software**.

 Para obtener más información sobre cómo configurar informes en Configuration Manager, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).

 Además, puede crear consultas y recopilaciones basadas en los datos almacenados en la base de datos de Configuration Manager por la medición de software.

 Para obtener más información acerca de las recopilaciones, consulte [Introduction to collections](../../core/clients/manage/collections/introduction-to-collections.md) (Introducción a recopilaciones).

 Para obtener más información acerca de las consultas, consulte [Introduction to queries](../../core/servers/manage/introduction-to-queries.md) (Introducción a las consultas).

##  <a name="security-and-privacy-for-software-metering"></a>Seguridad y privacidad de la medición de software

### <a name="security-issues-for-software-metering"></a>Problemas de seguridad de la medición de software
 Un atacante puede enviar información de medición de software no válida a Configuration Manager, que el punto de administración aceptará aunque la configuración de cliente de medición de software esté deshabilitada. Esto puede dar lugar a que un gran número de reglas de medición se repliquen a través de la jerarquía, provocando una denegación de servicio en la red y para los servidores de sitio de Configuration Manager.

 Puesto que un atacante puede crear datos de medición de software no válidos, no considere relevante la información de medición de software.

 Disponibilidad de software está habilitada de forma predeterminada como una configuración de cliente.

###  <a name="privacy-information-for-software-metering"></a>Información de privacidad de disponibilidad de Software
 Disponibilidad de software supervisa el uso de aplicaciones en equipos cliente. La medición de software está habilitada de forma predeterminada. Debe configurar las aplicaciones que se van a medir. La información de medición se almacena en la base de datos de Configuration Manager. La información se cifra durante la transferencia al punto de administración, pero no se almacena en formato cifrado en la base de datos de Configuration Manager.

 Esta información se guarda en la base de datos hasta que la eliminan las tareas de mantenimiento del sitio **Eliminar datos antiguos de disponibilidad de software** (cada cinco días) y **Eliminar datos antiguos de resumen de disponibilidad de software** (cada 270 días). Puede configurar el intervalo de eliminación. La información de medición no se envía a Microsoft.

 Antes de configurar la medición de software, tenga en cuenta los requisitos de privacidad.

## <a name="example-scenario-for-using-software-metering"></a>Escenario de ejemplo de uso de medición de software
 En esta sección, creará una regla de medición de software de ejemplo que puede ayudarlo a resolver los requisitos empresariales siguientes:

- Determinar el número de copias de una determinada aplicación en la compañía

- Detectar las copias de una aplicación que no se usan

- Determinar los usuarios que usan habitualmente una aplicación concreta

  Woodgrove Bank ha implementado Microsoft Office 2010 como su conjunto de aplicaciones de productividad de oficina estándar. Sin embargo, para admitir una aplicación heredada, es necesario que algunos equipos continúen ejecutando Microsoft Office Word 2003. El departamento de TI quiere reducir los costos de licencia y de soporte mediante la eliminación de estas copias de Word 2003 si ya no se usa la aplicación heredada. El departamento de soporte técnico también quiere identificar a los usuarios usan la aplicación heredada.

  El administrador de sistemas de TI de Woodgrove Bank usa la medición de software en Configuration Manager para lograr estos objetivos de negocio. El administrador realiza las siguientes acciones:

- Comprueba los requisitos previos para la medición de software y confirma que el punto de servicios de informes está instalado y en funcionamiento.
- Configura la configuración de cliente predeterminada para la medición de software:<br>El administrador habilita la medición de software y usa la programación predeterminada de recopilación de datos de una vez cada siete días.<br>El administrador configura el inventario de software para inventariar los archivos que tienen la extensión .exe mediante la configuración de la opción de cliente de inventario de software **Inventariar estos tipos de archivo**.<br>El administrador agrega un nueva regla de medición de software, denominada **woodgrove.exe**, para supervisar la aplicación heredada.
- Espera siete días y después los equipos cliente comienzan a notificar datos de uso sobre el archivo ejecutable **woodgrove.exe**.
- El administrador usa el informe de Configuration Manager denominado **Base de instalación para todos los programas de software medidos** para ver qué equipos tienen cargada la aplicación **woodgrove.exe**.
- Después de seis meses, el administrador ejecuta el informe **Equipos que tienen un programa medido instalado, pero que no han ejecutado el programa desde una fecha especificada**, al indicar la regla de medición de software y una fecha seis meses en el pasado. Este informe identifica 120 equipos que no han ejecutado el programa en los últimos seis meses.
- El administrador realiza algunas comprobaciones adicionales para confirmar que la aplicación heredada no es necesaria en los equipos identificados. A continuación, el administrador desinstala la aplicación heredada y la copia de Word 2003 de estos equipos.<br>El administrador ejecuta el informe **Usuarios que han ejecutado un programa de software medido específico** para proporcionar al departamento de soporte técnico una lista de usuarios que siguen usando la aplicación heredada.
- El administrador sigue comprobando los informes de medición de software semanalmente y toma medidas correctivas si es necesario.

  Como resultado de esta estrategia, los costos del departamento de TI en materia de soporte técnico y licencias se reducen mediante la eliminación de las aplicaciones que ya no son necesarias. Además, el departamento de soporte técnico tiene ahora la lista deseada que detalla los usuarios que ejecutan la aplicación heredada.
