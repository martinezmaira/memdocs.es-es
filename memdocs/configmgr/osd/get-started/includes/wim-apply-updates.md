---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708883"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a> Aplicar las actualizaciones de software a una imagen

> [!Note]  
> Esta sección se aplica a las **imágenes de sistema operativo** y a los **paquetes de actualización del sistema operativo**. Utiliza el término general "imagen" para hacer referencia al archivo de imagen de Windows (WIM). Estos dos objetos tienen un archivo WIM, que contiene los archivos de instalación de Windows. Las actualizaciones de software son aplicables a estos archivos en los dos objetos. El comportamiento de este proceso es el mismo en los dos objetos.  

Todos los meses hay nuevas actualizaciones de software aplicables a la imagen. Para poder aplicar las actualizaciones de software, necesita los siguientes requisitos previos:

- Infraestructura de actualizaciones de software  
- Actualizaciones de software sincronizadas correctamente  
- Actualizaciones de software descargadas a la biblioteca de contenido en el servidor del sitio  

Para obtener más información, consulte [Deploy software updates](../../../sum/deploy-use/deploy-software-updates.md) (Implementación de actualizaciones de software).  

Aplique las actualizaciones de software pertinentes a una imagen según una programación especificada. Este proceso se conoce como *instalación sin conexión*. En esta programación, Configuration Manager aplica las actualizaciones de software seleccionadas a la imagen. Después, también puede redistribuir la imagen actualizada a los puntos de distribución.

> [!Important]  
> Aunque puede seleccionar cualquier actualización de software aplicable a la imagen según la versión, DISM solo puede aplicar ciertos tipos de actualizaciones a la imagen. En el archivo **OfflineServicingMgr.log** se muestra la siguiente entrada: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

La base de datos del sitio almacena información sobre la imagen, incluyendo las actualizaciones de software que se aplicaron en el momento de la importación. Las actualizaciones de software que aplique a la imagen desde que se agregó inicialmente también se almacenan en la base de datos del sitio. Al iniciar el asistente para aplicar las actualizaciones de software, se recuperará la lista de actualizaciones de software aplicables que el sitio aún no haya aplicado a la imagen. Configuration Manager copiará las actualizaciones de software que seleccione en la biblioteca de contenido del servidor de sitio. Después aplica las actualizaciones de software a la imagen.  

### <a name="servicing-process"></a>Proceso de mantenimiento

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después seleccione **Imágenes de sistema operativo** o **Paquetes de actualización del sistema operativo**.  

2. Seleccione el objeto al que va a aplicar las actualizaciones de software.  

3. En la cinta de opciones, haga clic en **Programar actualizaciones** para iniciar el asistente.  

4. En la página **Elegir actualizaciones**, seleccione las actualizaciones de software que quiera aplicar a la imagen. La lista de actualizaciones puede tardar un rato en aparecer en el asistente. Use el **filtro** para buscar cadenas en los metadatos. Use la lista desplegable **Arquitectura del sistema** para filtrar por **X86**, **X64** o **Todas**. Puede seleccionar una actualización de la lista, muchas o todas. Cuando haya terminado de seleccionar las actualizaciones, haga clic en **Siguiente**.  

5. En la página **Establecer programación** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    1. **Programación**: especifique la programación para cuando el sitio aplique las actualizaciones de software a la imagen.  

    2. **Continuar después de un error**: seleccione esta opción para continuar con la aplicación de las actualizaciones de software a la imagen incluso cuando se produzca un error.  

    3. **Actualizar los puntos de distribución con la imagen**: seleccione esta opción para actualizar la imagen en los puntos de distribución después de que el sitio aplique las actualizaciones de software.  

6. Finalice el asistente para programar actualizaciones.  

> [!NOTE]  
> Para minimizar el tamaño de carga, el mantenimiento de los paquetes de actualización del sistema operativo y de imágenes del sistema operativo quita la versión anterior.  

### <a name="servicing-operations"></a>Operaciones de mantenimiento

En el nodo **Imágenes de sistema operativo** o **Paquetes de actualización del sistema operativo** de la consola de Configuration Manager, agregue las siguientes columnas a la vista:

- **Fecha de actualizaciones programada**: esta propiedad muestra la siguiente programación que haya definido.  
- **Estado de las actualizaciones programadas**: esta propiedad muestra el estado. Por ejemplo, **Correcto** o **En proceso**.  

Seleccione un objeto de imagen específico y después cambie a la pestaña **Estado de actualización** en el panel de detalles. En esta pestaña se muestra la lista de actualizaciones de la imagen.

Seleccione un objeto de imagen específico y haga clic en **Propiedades** en la cinta de opciones. En la pestaña **Actualizaciones instaladas** se muestra la lista de actualizaciones de la imagen. La pestaña **Mantenimiento** es una vista de solo lectura de la programación de mantenimiento actual y de las actualizaciones programadas para aplicarse.

Cuando el estado es **En proceso**, puede seleccionar **Cancelar actualizaciones programadas** en la cinta de opciones. Esta acción cancela el proceso de mantenimiento activo.

Para solucionar este proceso, vea los archivos **OfflineServicingMgr.log** y **dism.log** en el servidor de sitio. Para obtener más información, vea [Archivos de registro](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a> Especificación de la unidad para la instalación sin conexión de imágenes de SO

<!--1358924-->

A partir de la versión 1810, especifique la unidad que Configuration Manager usa durante la instalación sin conexión de imágenes de SO. Este proceso puede consumir una gran cantidad de espacio en disco con los archivos temporales. Esta opción le ofrece la flexibilidad de seleccionar la unidad que se va a usar.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Implementación de sistema operativo**.  

2. En la pestaña **Instalación sin conexión**, especifique la opción para **Una unidad local que se usará en la instalación de imágenes sin conexión**.  

De manera predeterminada, esta configuración es **Automática**. Con este valor, Configuration Manager selecciona la unidad donde está instalado.

Si selecciona una unidad que no existe en el servidor de sitio, Configuration Manager se comportará igual que si selecciona **Automática**.

Durante la instalación sin conexión, Configuration Manager almacena los archivos temporales en la carpeta, `<drive>:\ConfigMgr_OfflineImageServicing`. También monta la imagen del SO en esta carpeta.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a> Servicio de imágenes optimizado

<!--3555951-->

A partir de la versión 1902, al aplicar actualizaciones de software a una imagen de sistema operativo, puede usar una nueva opción para optimizar los resultados que consiste en quitar cualquier actualización reemplazada. La optimización de la instalación sin conexión solo se aplica a imágenes con un índice único.

Al programar el sitio para aplicar actualizaciones de software a una imagen de sistema operativo, se usa la herramienta de línea de comandos DISM (Administración y mantenimiento de imágenes de implementación) de Windows. Durante el proceso de mantenimiento, este cambio introduce estos dos pasos adicionales:  

- Ejecuta DISM en la imagen montada sin conexión con los parámetros `/Cleanup-Image /StartComponentCleanup /ResetBase`. Si se produce un error en este comando, se produce un error en el proceso de mantenimiento actual. No se confirman los cambios en la imagen.  

- Después de que Configuration Manager confirme los cambios en la imagen y la desmonte del sistema de archivos, la imagen se exporta a otro archivo. Este paso usa el parámetro `/Export-Image` de DISM. Quita los archivos innecesarios de la imagen, lo que reduce el tamaño.  

Microsoft recomienda que aplique periódicamente las actualizaciones a las imágenes sin conexión. No tiene que usar esta opción cada vez que se realiza el mantenimiento de una imagen. Cuando se realiza este proceso cada mes, resulta más ventajoso usar esta nueva opción con el paso del tiempo. Para obtener más información, vea el [paso Recomendaciones de Instalar actualizaciones de software](../../understand/install-software-updates.md#recommendations).

Aunque con esta opción se reduce el tamaño total de la imagen en mantenimiento, se tarda más tiempo en completar el proceso. Use el asistente para programar la realización del mantenimiento en el momento más adecuado. También se necesita almacenamiento adicional en el servidor de sitio. Puede personalizar el sitio para que use una ubicación alternativa. Para más información, vea [Especificación de la unidad para el mantenimiento sin conexión de imágenes de SO](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Proceso para optimizar el mantenimiento de imágenes

1. Inicie el [proceso de mantenimiento](#servicing-process).  

2. En la página **Establecer programación**, seleccione la opción **Quitar las actualizaciones reemplazadas después de actualizar la imagen**. Esta opción no está habilitada automáticamente. Si la imagen tiene más de un índice, no puede usar esta opción.  

3. Para programar el mantenimiento de imágenes, siga todos los pasos del asistente.  

Valide y supervise el proceso mediante el archivo **OfflineServicing.log**.
