---
title: La biblioteca de contenido
titleSuffix: Configuration Manager
description: Obtenga información sobre la biblioteca de contenido que usa Configuration Manager para reducir el tamaño total del contenido distribuido.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d7432b3522d5292e2c2afc1dac6b8db3382cca12
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343174"
---
# <a name="the-content-library-in-configuration-manager"></a>La biblioteca de contenido en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La biblioteca de contenido es un almacén de instancia única del contenido en Configuration Manager. El sitio la usa para reducir el tamaño total del cuerpo combinado del contenido que se distribuye. En la biblioteca de contenido se almacenan todos los archivos de contenido de las implementaciones de software, por ejemplo las actualizaciones de software, las aplicaciones y las implementaciones de sistema operativo.  

- El sitio crea y mantiene automáticamente una copia de la biblioteca de contenido en todos los servidores de sitio y puntos de distribución.  

- Antes de que Configuration Manager agregue archivos de contenido al servidor de sitio o copie los archivos en los puntos de distribución, comprueba si cada uno de los archivos de contenido ya está en la biblioteca de contenido.  

- Si el archivo de contenido está disponible, Configuration Manager no lo copia. En su lugar, asocia el archivo de contenido existente con la aplicación o paquete.  

En los servidores de punto de distribución, configure las opciones siguientes:

- Una o varias unidades de disco en las que quiera crear la biblioteca de contenido.  

- Una prioridad para cada unidad que use.  

Configuration Manager copia los archivos de contenido en la unidad con la prioridad más alta hasta que esa unidad contenga menos de una cantidad mínima de espacio disponible especificado.  

- Las unidades se configuran durante la instalación del punto de distribución.  

- No se pueden configurar las opciones de unidad en las propiedades del punto de distribución una vez finalizada la instalación.  

Para obtener más información sobre cómo configurar la unidad para el punto de distribución, vea [Administración del contenido y de la infraestructura de contenido](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Para mover la biblioteca de contenido a otra ubicación en un punto de distribución después de la instalación, use la **herramienta de transferencia de biblioteca de contenido** de las herramientas de Configuration Manager. Para obtener más información, vea [Content Library Transfer tool](../../support/content-library-transfer.md) (Herramienta de transferencia de biblioteca de contenido).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Acerca de la biblioteca de contenido en el sitio de administración central

De manera predeterminada, Configuration Manager crea una biblioteca de contenido en el sitio de administración central cuando se instala el sitio. La biblioteca de contenido se ubica en la unidad del servidor de sitio que dispone de más espacio libre. Como no se puede instalar un punto de distribución en el sitio de administración central, no se puede priorizar el uso de las unidades en la biblioteca de contenido. Al igual que la biblioteca de contenido en otros servidores de sitio y en puntos de distribución, cuando la unidad que contiene la biblioteca de contenido se queda sin espacio disponible en disco, la biblioteca de contenido se distribuye a la siguiente unidad disponible.  

Configuration Manager usa la biblioteca de contenido en el sitio de administración central en los siguientes escenarios:  

- Se crea contenido en el sitio de administración central.  

- Se migra el contenido desde otro sitio de Configuration Manager y se asigna el sitio de administración central como el sitio que administra ese contenido.  

> [!NOTE]  
> Cuando se crea contenido en un sitio primario y después se distribuye a otro sitio primario o a uno secundario de otro sitio primario, el sitio de administración central almacena temporalmente ese contenido en la bandeja de entrada del programador del sitio de administración central, pero no lo agrega a su biblioteca de contenido.  

Utilice las siguientes opciones para administrar la biblioteca de contenido en el sitio de administración central:  

- Para evitar que la biblioteca de contenido se instale en una unidad específica, cree un archivo vacío llamado **no_sms_on_drive.sms**. Cópielo en la raíz de la unidad antes de crear la biblioteca de contenido.  

- Después de crear la biblioteca de contenido, use la **herramienta de transferencia de biblioteca de contenido** de las herramientas de Configuration Manager para administrar la ubicación de la biblioteca de contenido. Para obtener más información, vea [Content Library Transfer tool](../../support/content-library-transfer.md) (Herramienta de transferencia de biblioteca de contenido).  

> [!Note]  
> Los puntos de distribución de nube no usan el almacenamiento de instancia única. El sitio cifra los paquetes antes de enviarlos a Azure, y cada paquete tiene una clave cifrada única. Incluso si dos archivos fueran idénticos, las versiones cifradas no serían iguales.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a> Configuración de una biblioteca de contenido remota para el servidor de sitio

<!--1357525-->
A partir de la versión 1806, para configurar la [alta disponibilidad del servidor de sitio](../../servers/deploy/configure/site-server-high-availability.md) o para liberar espacio de disco duro en los servidores de sitio primario o de administración central, reubique la biblioteca de contenido en otra ubicación de almacenamiento. Mueva la biblioteca de contenido a otra unidad del servidor de sitio, un servidor independiente o discos tolerantes a errores de una red de área de almacenamiento (SAN). Se recomienda una SAN, ya que tiene alta disponibilidad y proporciona almacenamiento elástico que aumenta o disminuye con el tiempo para satisfacer los requisitos variables del contenido. Para obtener más información, vea [High availability options](../../servers/deploy/configure/site-server-high-availability.md) (Opciones de alta disponibilidad).

Una biblioteca de contenido remota es un requisito previo para la [alta disponibilidad del servidor de sitio](../../servers/deploy/configure/site-server-high-availability.md).

> [!Note]  
> Esta acción solo mueve la biblioteca de contenido en el servidor de sitio. No afecta a la ubicación de la biblioteca de contenido en los puntos de distribución. 

> [!Tip]  
> Planee también la administración de contenido de origen del paquete, que es externo a la biblioteca de contenido. Todos los objetos de software de Configuration Manager tienen un origen del paquete en un recurso compartido de red. Considere la posibilidad de centralizar todos los orígenes en un mismo recurso compartido, pero asegúrese de que esta ubicación es redundante y de alta disponibilidad.
>
> Si mueve la biblioteca de contenido al mismo volumen de almacenamiento que los orígenes de paquete, no puede marcar este volumen para la desduplicación de datos. Aunque la biblioteca de contenido es compatible con la desduplicación de datos, el volumen de los orígenes del paquete no lo admite. Para obtener más información, vea [Introducción a la desduplicación de datos](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Requisitos previos  

- La cuenta de equipo del servidor de sitio necesita permisos de **control total** para la ruta de acceso de red a la que se va a mover la biblioteca de contenido. Este permiso se aplica al recurso compartido y al sistema de archivos. No se instala ningún componente en el sistema remoto.

- El servidor de sitio no puede tener el rol de punto de distribución. El punto de distribución también usa la biblioteca de contenido, y este rol no admite una biblioteca de contenido remota. Después de mover la biblioteca de contenido, no se puede agregar el rol de punto de distribución al servidor de sitio.  

- El sistema remoto de la biblioteca de contenido ha de estar en un dominio de confianza.

> [!Important]  
> No reutilice una ubicación de red compartida entre varios sitios. Por ejemplo, no use la misma ruta de acceso para un sitio de administración central y un sitio primario secundario. Esta configuración tiene el potencial de dañar la biblioteca de contenido y tendrá que volver a generarla.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Proceso para administrar la biblioteca de contenido

1. Cree una carpeta en un recurso compartido de red como destino para la biblioteca de contenido. Por ejemplo, `\\server\share\folder`.  

    > [!Warning]  
    > No reutilice una carpeta existente con contenido. Por ejemplo, no use la misma carpeta que sus orígenes de paquete. Antes de copiar la biblioteca de contenido, Configuration Manager quita todo el contenido de la ubicación que especifique.  

2. En la consola de Configuration Manager, cambie al área de trabajo **Administración**. Expanda **Configuración del sitio**, haga clic en el nodo **Sitios** y seleccione el sitio. En la pestaña **Resumen** de la parte inferior del panel de detalles, observará una nueva columna **Biblioteca de contenido**.  

3. Seleccione **Administrar la biblioteca de contenido** en la cinta de opciones.  

4. En la ventana Administrar la biblioteca de contenido, en el campo **Ubicación actual** se muestra la unidad local y la ruta de acceso. Escriba una ruta de acceso de red válida para **Nueva ubicación**. Esta ruta de acceso es la ubicación a la que el sitio mueve la biblioteca de contenido. Debe incluir un nombre de carpeta que ya exista en el recurso compartido, por ejemplo, `\\server\share\folder`. Seleccione **Aceptar**.  

5. Observe el valor **Estado** de la columna Biblioteca de contenido en la pestaña Resumen del panel de detalles. Se actualiza para mostrar el progreso del sitio cuando se mueve la biblioteca de contenido.  

   - Mientras está **En curso**, el valor **Progreso de movimiento (%)** muestra el porcentaje completado.  

        > [!Note]  
        > Si tiene una gran biblioteca de contenido, es posible que vea el progreso `0%` en la consola durante un tiempo. Por ejemplo, con una biblioteca de 1 TB, debe copiar 10 GB antes de mostrar `1%`. Consulte **distmgr.log**, que muestra el número de bytes y archivos copiados. A partir de la versión 1810, el archivo de registro también muestra un tiempo estimado restante.

   - Si se produce un estado de error, el estado muestra el error. Errores comunes incluyen **acceso denegado** o **disco lleno**.  

   - Cuando finaliza, se muestra **Completado**.  

     Consulte **distmgr.log** para más información. Para más información, consulte [Registros de servidor de sistema de sitio y servidor de sitio](log-files.md#BKMK_SiteSiteServerLog).  

Para obtener más información sobre este proceso, vea [Flowchart - Manage content library](manage-content-library-flowchart.md) (Diagrama de flujo: administración de la biblioteca de contenido).

El sitio *copia* en realidad los archivos de biblioteca de contenido en la ubicación remota. Este proceso no elimina los archivos de biblioteca de contenido en la ubicación original en el servidor de sitio. Para liberar espacio, un administrador debe eliminar manualmente estos archivos originales.

Si la biblioteca de contenido original abarca dos unidades, se combina en una sola carpeta en el nuevo destino.

A partir de la versión 1810, durante el proceso de copia, los componentes del **procesador de paquetes** y del **administrador de distribución** no procesan los nuevos paquetes. Esta acción garantiza que el contenido no se agregue a la biblioteca mientras se está eliminando. Programe en cualquier caso este cambio durante un mantenimiento del sistema.

Si tiene que devolver la biblioteca de contenido al servidor de sitio, repita este proceso, pero escriba una unidad y ruta de acceso locales para **Nueva ubicación**. Debe incluir un nombre de carpeta que ya exista en la unidad, por ejemplo, `D:\SCCMContentLib`. Cuando el contenido original todavía existe, el proceso mueve rápidamente la configuración a la ubicación local en el servidor de sitio.

> [!Tip]  
> Para mover el contenido a otra unidad en el servidor de sitio, use la herramienta **Content Library Transfer**. Para obtener más información, vea [Content Library Transfer tool](../../support/content-library-transfer.md) (Herramienta de transferencia de biblioteca de contenido).  


## <a name="inside-the-content-library"></a>Dentro de la biblioteca de contenido

> [!Warning]  
> La sección siguiente se proporciona únicamente con fines informativos. No modifique, agregue o quite ningún archivo ni carpeta de la biblioteca de contenido. Si lo hace, podría dañar los paquetes, el contenido o la biblioteca de contenido en su totalidad. Si sospecha que faltan datos o que hay datos dañados o no válidos, use la característica de validación en la consola de Configuration Manager para detectar estos problemas. Después, redistribuya el contenido afectado para corregir los problemas.

De forma predeterminada, la biblioteca de contenido se almacena en la raíz de una unidad en una carpeta denominada **SCCMContentLib**. Esta carpeta se comparte de forma predeterminada como **SCCMContentLib$** . La carpeta y el recurso compartido tienen permisos restringidos para evitar daños accidentales. Todos los cambios se deben realizar desde la consola de Configuration Manager. En esta carpeta se encuentran los objetos siguientes:  

- La biblioteca de paquetes (carpeta **PkgLib**): información sobre qué paquetes están presentes en el punto de distribución.  

- La biblioteca de datos (carpeta **DataLib**): información sobre la estructura original de los paquetes.  

- La biblioteca de archivos (carpeta **FileLib**): archivos originales del paquete. Esta carpeta suele ser la que usa la mayor parte del almacenamiento.  

![Información general del diagrama de la biblioteca de contenido de Configuration Manager](media/content-library-overview.png)

> [!Tip]  
> Use la herramienta **Content Library Explorer** de las herramientas de Configuration Manager para examinar el contenido de la biblioteca de contenido. Esta herramienta no se puede usar para modificar el contenido. Proporciona información sobre lo que está presente, además de permitir la validación y redistribución. Para obtener más información, vea [Content Library Explorer](../../support/content-library-explorer.md) (Explorador de la biblioteca de contenido).  

### <a name="package-library"></a>Biblioteca de paquetes

En la carpeta de biblioteca de paquetes, **PkgLib**, se incluye un archivo para cada paquete que se distribuye al punto de distribución. El nombre de archivo es el identificador del paquete, por ejemplo, `ABC00001.INI`. En este archivo, en la sección `[Packages]`, hay una lista de identificadores de contenido que forman parte del paquete, así como otra información como la versión. Por ejemplo, **ABC00001** es un paquete heredado en la versión **1**. El identificador de contenido de este archivo es `ABC00001.1`.

### <a name="data-library"></a>Biblioteca de datos

En la carpeta de biblioteca de datos, **DataLib**, se incluye un archivo y una carpeta para el contenido de cada paquete. Por ejemplo, los nombres de este archivo y esta carpeta son `ABC00001.1.INI` y `ABC00001.1`, respectivamente. El archivo incluye información para la validación. La carpeta vuelve a crear la estructura de carpetas del paquete original.

Los archivos de la biblioteca de datos se reemplazan por archivos INI con el nombre del archivo original en el paquete. Por ejemplo, `MyFile.exe.INI`. Estos archivos incluyen información sobre el archivo original, como el tamaño, la hora de modificación y el código hash. Use los cuatro primeros caracteres del código hash para buscar el archivo original en la biblioteca de archivos. Por ejemplo, el código hash de MyFile.exe.INI es **DEF98765**, y los cuatro primeros caracteres son **DEF9**.

### <a name="file-library"></a>Biblioteca de archivos

Si la biblioteca de contenido abarca varias unidades, los archivos del paquete podrían estar en la carpeta de biblioteca de archivos, **FileLib**, en cualquiera de estas unidades.

Busque un archivo específico mediante los cuatro primeros caracteres del código hash encontrado en la biblioteca de datos. Dentro de la carpeta de biblioteca de archivos hay muchas carpetas, cada una con un nombre de cuatro caracteres. Busque la carpeta que coincida con los cuatro primeros caracteres del código hash. Una vez que encuentre esta carpeta, incluye uno o varios conjuntos de tres archivos. Estos archivos comparten el mismo nombre, pero uno tiene la extensión INI, otro tiene la extensión SIG y otro no tiene ninguna extensión de archivo. El archivo original es el que no tiene extensión cuyo nombre es igual que el código hash de la biblioteca de datos.

Por ejemplo, la carpeta **DEF9** incluye `DEF98765.INI`, `DEF98765.SIG` y `DEF98765`. `DEF98765` es el `MyFile.exe` original. El archivo INI incluye una lista de "usuarios" o identificadores de contenido que comparten el mismo archivo. El sitio no quita un archivo a menos que también se eliminen todos estos contenidos.

### <a name="drive-spanning"></a>Expansión de unidades

La biblioteca de contenido puede abarcar varias unidades. Puede elegir estas unidades al crear el punto de distribución. De forma predeterminada, Configuration Manager elige automáticamente las unidades cuando se expande la biblioteca de contenido.

Al elegir las unidades, seleccione una unidad principal y otra secundaria. El sitio almacena todos los metadatos en la unidad principal. Solo expande la biblioteca de archivos en la unidad secundaria. El nombre de recurso compartido de la carpeta para las unidades secundarias incluye la letra de unidad. Por ejemplo, si D: y E: son unidades secundarias para la biblioteca de contenido, los nombres de recurso compartido son **SCCMContentLibD$** y **SCCMContentLibE$** .

Si ha seleccionado la opción **Automático**, Configuration Manager selecciona la unidad con más espacio disponible como la unidad principal. Almacena todos los metadatos en esta unidad. El sitio solo expande la biblioteca de archivos en las unidades secundarias.

Especifique una cantidad de espacio de reserva durante la configuración. Configuration Manager intenta usar un disco secundario cuando el mejor disco disponible solo tiene libre esta cantidad de espacio de reserva. Cada vez que se selecciona una unidad nueva para su uso, se selecciona la unidad con el máximo espacio libre disponible.

No se puede especificar que un punto de distribución deba usar todas las unidades excepto para un conjunto específico. Para impedir este comportamiento, cree un archivo vacío en la raíz de la unidad, denominado `NO_SMS_ON_DRIVE.SMS`. Coloque este archivo antes de que Configuration Manager seleccione la unidad que se va a usar. Si Configuration Manager detecta este archivo en la raíz de la unidad, no use la unidad para la biblioteca de contenido.


## <a name="troubleshooting"></a>Solución de problemas

Las sugerencias siguientes pueden ayudar a solucionar problemas relacionados con la biblioteca de contenido:  

- Revise los registros en el servidor de sitio (**distmgr.log** y **PkgXferMgr.log**) y el punto de distribución (**smsdpprov.log**) para todos los punteros a los errores.  

- Use la herramienta [Content Library Explorer](../../support/content-library-explorer.md).  

- Busque bloqueos de archivo por otros procesos, como software antivirus. Excluya la biblioteca de contenido en todas las unidades de los análisis antivirus automáticos, así como el directorio de ensayo temporal, **SMS_DP$** , en cada unidad.  

- Para ver si hay diferencias en el código hash, valide el paquete desde la consola de Configuration Manager.  

- Como última opción, redistribuya el contenido. Con esta acción se debería resolver la mayoría de los problemas.  

Para obtener información más detallada, consulte [Descripción y solución de problemas de distribución de contenido en Configuration Manager](https://support.microsoft.com/help/4482728/understand-troubleshoot-content-distribution-in-configuration-manager).
