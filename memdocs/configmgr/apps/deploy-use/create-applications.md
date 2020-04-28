---
title: Crear aplicaciones
titleSuffix: Configuration Manager
description: Cree aplicaciones con tipos de implementación, métodos de detección y requisitos para instalar el software.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 33a95ae78fdc80c6c08b59cfe5ec5b2e88485a8f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074663"
---
# <a name="create-applications-in-configuration-manager"></a>Crear aplicaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Una aplicación de Configuration Manager define los metadatos sobre la aplicación. Una aplicación tiene uno o varios tipos de implementación. Estos tipos de implementación incluyen la información y los archivos de instalación necesarios para instalar el software en los dispositivos. Un tipo de implementación también tiene reglas, como los requisitos y los métodos de detección. Estas reglas especifican cuándo y cómo el cliente instala el software.  

Cree aplicaciones mediante los métodos siguientes:  

- Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación:  
  - [Crear una aplicación](#bkmk_create) y [detectar automáticamente](#bkmk_auto-app) la información de la aplicación
  - [Crear un tipo de implementación](#bkmk_create-dt) e [identificar automáticamente](#bkmk_auto-dt) la información de tipo de implementación

- Crear manualmente la aplicación y después agregar los tipos de implementación más adelante:  
  - [Crear una aplicación](#bkmk_create) y [especificar manualmente](#bkmk_manual-app) la información de la aplicación
  - [Crear un tipo de implementación](#bkmk_create-dt) e [especificar manualmente](#bkmk_manual-dt) la información de tipo de implementación

- [Importar una aplicación](#bkmk_import) desde un archivo  

Este artículo también incluye la información siguiente para configurar un tipo de implementación:  

- [Contenido](#bkmk_dt-content)
- [Secuencia de tareas](#bkmk_dt-ts)
- [Método de detección](#bkmk_dt-detect)
- [Experiencia del usuario](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Códigos de retorno](#bkmk_dt-return)
- [Dependencias](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a> Crear una aplicación  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear aplicación**.  

Después, detecte automáticamente o especifique manualmente la información de la aplicación:  

- [Detecte automáticamente](#bkmk_auto-app) la información de la aplicación para crear una aplicación básica con un solo tipo de implementación. Por ejemplo, un archivo de Windows Installer que no tiene dependencias ni requisitos. Después de crear una aplicación mediante el uso de este procedimiento, edítela según sea necesario. Puede agregar o cambiar los tipos de implementación y agregar métodos de detección, dependencias o requisitos.  

- [Especifique manualmente](#bkmk_manual-app) la información de la aplicación para crear aplicaciones más complejas. Defina más de un tipo de implementación, dependencias, métodos de detección o requisitos.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a> Detectar automáticamente la información de la aplicación  

1. En la página **General** del Asistente para crear aplicaciones, seleccione **Detectar automáticamente la información sobre esta aplicación a partir de archivos de instalación**.  

2. En la lista desplegable **Tipo** , seleccione el tipo de archivo de instalación de aplicación que desea utilizar para detectar información de la aplicación. Para obtener más información sobre los tipos de instalación disponibles, vea [Tipos de implementación que admite Configuration Manager](create-applications.md#bkmk_deploy-types).  

3. En el cuadro **Ubicación**, especifique el archivo de instalación de la aplicación que quiera utilizar para detectar información de la aplicación. Esta ubicación es una ruta de acceso de red (`\\server\share\filename`) o un vínculo de la tienda. Debe tener acceso a la ruta de acceso de red y a todas las subcarpetas que incluyen el contenido de la aplicación.  

    > [!IMPORTANT]  
    > Si selecciona **Windows Installer (archivo \*.msi)** como tipo de aplicación, el sitio importa todos los archivos de la carpeta especificada. Después envía estos archivos a los puntos de distribución. Asegúrese de que la carpeta especificada solo contenga los archivos necesarios para instalar la aplicación. Microsoft prueba Configuration Manager para que admita hasta 20 000 archivos en el paquete de la aplicación. Si la aplicación tiene más archivos, considere la posibilidad de crear varias aplicaciones con menos archivos.  

4. En la página **Importar información** del Asistente para crear aplicaciones, revise la información y después seleccione **Siguiente**. Si es necesario, seleccione **Anterior** para volver atrás y corregir los errores.  

5. En la página **Información general** del Asistente para crear aplicaciones, especifique la siguiente información:  

    > [!NOTE]  
    > Si Configuration Manager detecta automáticamente esta información en los archivos de instalación de la aplicación, ya está rellenada aquí. Además, las opciones mostradas pueden ser diferentes según el tipo de aplicación que cree.  

    - Información general sobre la aplicación, como **Nombre**, **Comentarios de administrador**, **Editor** y **Versión de software**. Para ayudar a encontrar la aplicación en la consola de Configuration Manager, especifique una **Referencia opcional** o seleccione **Categorías administrativas**.  

    - **Programa de instalación**: especifique el programa de instalación y las propiedades necesarias para instalar este tipo de implementación de aplicaciones.  

        > [!TIP]  
        > Si el programa de instalación no aparece, haga clic en **Examinar** y busque la ubicación del programa de instalación.  

    - **Comportamiento de instalación**: seleccione una de las tres opciones para cómo instala Configuration Manager este tipo de implementación. Para obtener más información sobre estas opciones, vea [Experiencia de usuario](#bkmk_dt-ux).  

    - **Usar una conexión VPN automática (si está configurada)** : si ha implementado un perfil de VPN en el dispositivo en el que el usuario inicia la aplicación, la VPN se conectará cuando se inicie. Esta opción es solo para Windows 8.1 y Windows Phone 8.1. En dispositivos Windows Phone 8.1, las conexiones VPN automáticas no se admiten si se ha implementado más de un perfil de VPN en el dispositivo. Para obtener más información, vea [Perfiles de VPN](../../protect/deploy-use/vpn-profiles.md).  

    - **Aprovisionar esta aplicación para todos los usuarios del dispositivo**:<!--1358310-->: Aprovisione una aplicación con un paquete de la aplicación de Windows para todos los usuarios del dispositivo. Para obtener más información, vea [Creación de aplicaciones Windows](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Si va a modificar una aplicación existente, esta opción está en la pestaña de **Experiencia del usuario** de las propiedades del tipo de implementación del paquete de la aplicación de Windows.  

6. Seleccione **Siguiente**, revise la información de la aplicación en la página **Resumen** y, después, finalice el Asistente para crear aplicaciones.  

La nueva aplicación ahora aparece en el nodo **Aplicaciones** de la consola de Configuration Manager. Ha terminado de crear una aplicación.

Para agregar más tipos de implementación o configurar otras opciones, vea [Crear tipos de implementación para la aplicación](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a> Especificar manualmente la información de la aplicación  

1. En la página **General** del Asistente para crear aplicaciones, seleccione **Especificar manualmente la información de la aplicación** y, después, seleccione **Siguiente**.  

2. Especificar **Información general** sobre la aplicación:  

    - El **nombre** de la aplicación es necesario y debe tener menos de 256 caracteres.  

    - **Comentarios del administrador**, **Editor** y **Versión del software** son metadatos adicionales para describir aún más la aplicación.  

    - Para ayudar a encontrar la aplicación en la consola de Configuration Manager, especifique una **Referencia opcional** o seleccione **Categorías administrativas**.  

    - **Fecha de publicación**  

    - Seleccione usuarios o grupos que son responsables de esta aplicación, como **Propietarios** y **Contactos de soporte técnico**. De forma predeterminada, estos valores se establecen en el nombre de usuario.  

3. En la página **Centro de software** del Asistente para crear aplicaciones, especifique la siguiente información:  

    > [!Note]  
    > En la versión 1902 y anteriores, esta página se llamaba **Catálogo de aplicaciones**.

    - **Idioma seleccionado**: en la lista desplegable, seleccione la versión de idioma de la aplicación que quiere configurar. Seleccione **Agregar o quitar** para configurar más idiomas para esta aplicación.  

    - **Nombre de aplicación localizado**: especifique el nombre de la aplicación en el idioma que ha seleccionado.  

        > [!IMPORTANT]  
        > Es necesario un nombre de aplicación localizado para cada versión de idioma que configure.  

    - **Categorías de usuario**: haga clic en **Editar** para especificar categorías de la aplicación en el idioma que ha seleccionado. Los usuarios del Centro se software usan estas categorías como ayuda para filtrar y ordenar las aplicaciones.  

        > [!Note]  
        > En la versión 1902 y anteriores, las categorías de usuario solo se aplican a las implementaciones disponibles en las recopilaciones de usuarios. Si una aplicación se implementa en una recopilación de equipos, se omiten las categorías de usuario.
        >
        > A partir de la versión 1906, las categorías de usuario para las implementaciones de aplicaciones destinadas a dispositivos se muestran como filtros en el Centro de software. Estas implementaciones pueden estar disponibles o ser obligatorias.
        >
        > <!-- 4726793 -->Cambiar el nombre o eliminar una categoría no se aplica automáticamente a las aplicaciones con esta categoría. Estos cambios se aplican en la siguiente revisión de la aplicación. Para solucionar este problema con el fin de cambiar el nombre o eliminar:
        >
        > - En primer lugar, desactive la casilla de la categoría en cualquier aplicación que haga referencia a ella. A continuación, aplique ese cambio, lo que revisa la aplicación.
        >     - En lugar de la acción para cambiar nombre, cree una categoría con el nombre nuevo y agregue la categoría nueva a las aplicaciones correspondientes.
        >     - Puede eliminar la categoría después de revisar las aplicaciones.

    - **Documentación de usuario**: especifique la ubicación de un archivo con el que los usuarios del Centro de software pueden obtener más información sobre esta aplicación. Esta ubicación es una dirección de sitio web o un nombre de archivo y de ruta de acceso de red. Asegúrese de que los usuarios tengan acceso a esta ubicación.  

    - **Texto del vínculo**: especifique el texto que aparece en lugar de "Información adicional" cuando se especifica la documentación del usuario.  

    - **Dirección URL de privacidad**: especifique una dirección de sitio web vinculada a la declaración de privacidad de la aplicación.  

    - **Descripción localizada**: especifique una descripción para esta aplicación en el idioma que ha seleccionado.  

    - **Palabras clave**: escriba una lista de palabras clave en el idioma seleccionado. Estas palabras clave ayudan a los usuarios del Centro de software a buscar la aplicación.  

    - **Icono**: seleccione **Examinar** para seleccionar un icono para esta aplicación. Si no se especifica un icono, Configuration Manager usa un icono predeterminado. Los iconos pueden tener dimensiones de hasta 512 x 512 píxeles.  

4. En la página **Tipos de implementación** del Asistente para crear aplicaciones, seleccione **Agregar** para crear un tipo de implementación nuevo. Para obtener más información, consulte [Crear tipos de implementación de la aplicación](#bkmk_create-dt).  

5. Seleccione **Siguiente**, revise la información de la aplicación en la página **Resumen** y, después, finalice el Asistente para crear aplicaciones.  

La nueva aplicación ahora aparece en el nodo **Aplicaciones** de la consola de Configuration Manager.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a> Crear tipos de implementación de la aplicación  

Si se [detecta automáticamente la información de la aplicación](#bkmk_auto-app), es posible que no sea necesario finalizar algunos de los pasos de esta sección.  

> [!Note]  
> Al ver las propiedades de un tipo de implementación existente, las secciones siguientes se corresponden con las pestañas de la ventana de propiedades del tipo de implementación:  
>
> - [Contenido](#bkmk_dt-content)
> - [Secuencia de tareas](#bkmk_dt-ts)
> - [Método de detección](#bkmk_dt-detect)
> - [Experiencia del usuario](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Códigos de retorno](#bkmk_dt-return)
> - [Dependencias](#bkmk_dt-depend)
>  
> Para obtener información sobre la pestaña **Comportamiento de instalación** de las propiedades de un tipo de implementación, vea [Comprobación de archivos ejecutables en ejecución](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Iniciar el Asistente para crear tipos de implementación  

Hay tres formas de iniciar el Asistente para crear tipos de implementación:

- **En el nodo Aplicaciones**: En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**. Seleccione una aplicación y después elija **Crear un tipo de implementación** en la cinta de opciones.  

- **Al crear una aplicación**: cuando seleccione [Especificar manualmente la información de la aplicación](#bkmk_manual-app) en el Asistente para crear aplicaciones, haga clic en **Agregar** en la página Tipos de implementación.  

- **Desde las propiedades de la aplicación**: seleccione una aplicación existente en el nodo **Aplicaciones** y seleccione **Propiedades**. Cambie a la pestaña **Tipos de implementación** y seleccione **Agregar**.

Después use uno de los procedimientos siguientes para [detectar automáticamente](#bkmk_auto-dt) o [configurar manualmente](#bkmk_manual-dt) la información de tipo de implementación.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a> Identificar automáticamente la información de tipo de implementación  

1. En la página **General** del Asistente para crear tipos de implementación:  

    1. Seleccione el **Tipo** de archivo de instalación de aplicación para detectar información del tipo de implementación.  

    2. Seleccione **Identificar automáticamente la información sobre este tipo de implementación a partir de los archivos de instalación**.  

    3. En el cuadro **Ubicación**, especifique el archivo de instalación de aplicación que quiere usar para detectar información del tipo de implementación. Esta ubicación es una ruta de acceso de red (`\\server\share\filename`) o un vínculo de la tienda. Debe tener acceso a la ruta de acceso de red y a todas las subcarpetas que incluyen el contenido de la aplicación.  

2. En la página **Importar información** del Asistente para crear tipos de implementación, revise la información y después seleccione **Siguiente**. Si es necesario, seleccione **Anterior** para volver atrás y corregir los errores.  

3. En la página **Información general** del Asistente para crear tipos de implementación, especifique la información siguiente:  

    > [!NOTE]  
    > Es posible que parte de la información del tipo de implementación ya esté presente si se obtuvo de los archivos de instalación de la aplicación. Además, es posible que las opciones que se muestran difieran, según el tipo de implementación que se va a crear.  

    - **Información general** sobre el tipo de implementación:  
        - El **Nombre** es obligatorio  

        - **Comentarios del administrador** para ampliar la descripción  

        - **Idiomas** que están disponibles para él  

    - **Programa de instalación**: especifique el programa de instalación y las propiedades que se requieren para instalar al tipo de implementación.  

    - **Comportamiento de instalación**: seleccione una de las tres opciones para cómo instala Configuration Manager este tipo de implementación. Para obtener más información sobre estas opciones, vea [Experiencia de usuario](#bkmk_dt-ux).  

    - **Usar una conexión VPN automática (si está configurada)** : si ha implementado un perfil de VPN en el dispositivo en el que el usuario inicia la aplicación, la VPN se conectará cuando se inicie. Esta opción es solo para Windows 8.1 y Windows Phone 8.1. En dispositivos Windows Phone 8.1, las conexiones VPN automáticas no se admiten si se ha implementado más de un perfil de VPN en el dispositivo. Para obtener más información, vea [Perfiles de VPN](../../protect/deploy-use/vpn-profiles.md).  

4. Seleccione **Siguiente** y continúe con [Opciones de contenido de tipo de implementación](#bkmk_dt-content).  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a> Especificar manualmente la información del tipo de implementación  

1. En la página **General** del Asistente para crear tipos de implementación, en la lista desplegable **Tipo**, elija el tipo de archivo de instalación de aplicación para este tipo de implementación.

2. Seleccione **Especificar manualmente la información del tipo de implementación** y después elija **Siguiente**.

3. En la página **Información general** del Asistente para crear tipos de implementación, especifique un **Nombre** para el tipo de implementación. Opcionalmente, especifique **Comentarios del administrador**, seleccione los **Idiomas** para este tipo de implementación y después elija **Siguiente**.  

4. Continúe con las [Opciones de contenido de tipo de implementación](#bkmk_dt-content).  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a> Opciones de **contenido** de tipo de implementación  

En la página **Contenido**, especifique la siguiente información:  

> [!Note]  
> Al ver las propiedades de un tipo de implementación existente, algunas de estas opciones aparecen en la pestaña **Contenido** y otras en la pestaña **Programas**.  

- **Ubicación del contenido**: especifique la ubicación del contenido para este tipo de implementación, o haga clic en **Examinar** para seleccionar la carpeta de contenido del tipo de implementación.  

    > [!IMPORTANT]  
    > La cuenta del sistema del equipo del servidor de sitio debe tener permisos para la ubicación del contenido que especifique.  

  - **Conservar contenido en la caché del cliente**: el cliente de Configuration Manager mantiene indefinidamente en su caché el contenido del tipo de implementación. El cliente mantiene el contenido incluso si la aplicación ya está instalada. Esta opción es útil en algunas implementaciones, como el software basado en Windows Installer. Windows Installer necesita una copia local del contenido de origen para aplicar las actualizaciones. Esta opción reduce el espacio de caché disponible. Si se selecciona esta opción, podría posteriormente causar un error de una implementación de gran tamaño si la memoria caché no tiene espacio disponible suficiente.  

- **Programa de instalación**: especifique el nombre del programa de instalación y los parámetros de instalación necesarios.  

  - **Inicio de instalación en**: opcionalmente, especifique la carpeta que contiene el programa de instalación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente, o una ruta de acceso a la carpeta del punto de distribución que contiene los archivos de instalación.  

- **Programa de desinstalación**: opcionalmente, especifique el nombre del programa de desinstalación y los parámetros necesarios.  

  - **Inicio de desinstalación en**: opcionalmente, especifique la carpeta que contiene el programa de desinstalación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente. También puede ser una ruta de acceso relativa en un punto de distribución de la carpeta que contiene el paquete.  

- **Reparar el programa**: especifique opcionalmente el nombre del programa de reparación y los parámetros necesarios para los tipos de implementación de Windows Installer y el instalador de scripts.<!--1357866-->  

  - **Inicio de la reparación en**: opcionalmente, especifique la carpeta que contiene el programa de reparación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente. También puede ser una ruta de acceso relativa en un punto de distribución de la carpeta que contiene el paquete.  

- **Ejecutar programa de instalación y desinstalación como proceso de 32 bits en clientes de 64 bits**: use las ubicaciones del Registro y de archivos de 32 bits en equipos basados en Windows para ejecutar el programa de instalación del tipo de implementación.  

#### <a name="deployment-type-properties-content-options"></a>Opciones de **contenido** de propiedades de tipo de implementación

Al ver las propiedades de un tipo de implementación, las siguientes opciones solo aparecen en la pestaña **Contenido**:

- **Configuración del contenido de desinstalación**:  

  - **Igual que el contenido de instalación**: seleccione esta opción si el contenido de instalación y desinstalación es el mismo. Esta opción es el valor predeterminado.  

  - **Ningún contenido de desinstalación**: seleccione esta opción si la aplicación no necesita contenido para la desinstalación.  

  - **Diferente del contenido de instalación**: seleccione esta opción si el contenido de desinstalación es diferente al de instalación.  

    - **Ubicación del contenido de desinstalación**: especifique la ruta de acceso de red para el contenido que se usa para desinstalar la aplicación.  

- **Permitir que los clientes usen puntos de distribución del grupo de límite del sitio predeterminado**: especifique si los clientes deben descargar e instalar el software desde un punto de distribución del grupo de límites predeterminado del sitio, cuando el contenido no esté disponible desde un punto de distribución del grupo actual o de los grupos de límites vecinos.  

- **Opciones de implementación**: especifique si los clientes deben descargar la aplicación al usar un punto de distribución desde un grupo vecino o los grupos de límites predeterminados del sitio.  

- **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si desea habilitar el uso de BranchCache para descargas de contenido. Para obtener más información, vea [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). BranchCache siempre está habilitado en los clientes. Esta configuración se eliminó en la versión 1802, ya que los clientes usan BranchCache si el punto de distribución lo admite.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a> Opciones del tipo de implementación de la **secuencia de tareas**

<!--3555953-->

Para obtener más información sobre el tipo de implementación de la secuencia de tareas a partir de la versión 2002, consulte [Tipo de implementación de la secuencia de tareas](../get-started/creating-windows-applications.md#bkmk_tsdt).

En la página **Secuencia de tareas**, especifique la información siguiente:

- **Secuencia de tareas de instalación**: seleccione una secuencia de tareas que ejecute el proceso de instalación de esta aplicación.

- **Secuencia de tareas de desinstalación** (opcional): seleccione una secuencia de tareas que quite esta aplicación.

> [!TIP]  
> Si la secuencia de tareas no aparece en la lista, compruebe que no se incluye ningún paso de implementación o actualización del sistema operativo. Confirme también que no esté marcada como una secuencia de tareas de gran impacto. Para obtener más información, revise los requisitos previos para el [Tipo de implementación de la secuencia de tareas](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a> Opciones de **método de detección** de tipo de implementación

Este procedimiento configura un método de detección que indica la presencia del tipo implementación. En otras palabras, si el dispositivo de Windows ya tiene instalada la aplicación. Use uno de los dos métodos siguientes para crear un método de detección:

- [Configurar reglas para detectar la presencia de este tipo de implementación](#bkmk_detect-rule)
- [Usar un script personalizado para detectar la presencia de este tipo de implementación](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a> Configurar reglas para detectar la presencia de este tipo de implementación

1. En la página **Método de detección**, la opción de **Configurar reglas para detectar la presencia de este tipo de implementación** está activada de forma predeterminada. Haga clic en **Agregar cláusula**.  

2. En el cuadro de diálogo **Regla de detección**, seleccione un **Tipo de configuración** para detectar la presencia del tipo de implementación:  

    - **Sistema de archivos**: detecte si una carpeta o archivo especificado existe en un dispositivo. Esta detección indica que la aplicación está instalada. Especifique la siguiente información adicional:  

        - **Tipo**: seleccione si es un archivo o carpeta.  

        - **Ruta de acceso** (obligatorio): escriba o busque la ruta de acceso local en el dispositivo que incluye el archivo o carpeta. Por ejemplo, `C:\Program Files`. No se puede especificar una ruta de acceso de red compartida. Si selecciona **Examinar**, examinará el sistema de archivos local o se conectará a un cliente representativo para examinar.  

        - **Nombre de archivo o carpeta** (obligatorio): especifique el nombre de archivo o carpeta específico para detectar en la ruta de acceso anterior. Si el cliente detecta este archivo o carpeta en el dispositivo, considera la aplicación como instalada en el dispositivo.  

        - **Este archivo o carpeta está asociado a una aplicación de 32 bits en sistemas de 64 bits**: Esta opción está seleccionada de forma predeterminada. En primer lugar, el cliente comprueba las ubicaciones de archivos de 32 bits para la carpeta o archivo especificado. Si no se encuentra el archivo o la carpeta, el cliente busca en ubicaciones de 64 bits.  

    - **Registro**: detecte si existe una clave del Registro especificada o un valor del Registro en un dispositivo cliente. Esta detección indica que la aplicación está instalada. Especifique la siguiente información adicional:  

        - **Subárbol** (obligatorio): elija un subárbol del Registro en la lista desplegable. Por ejemplo, `HKEY_LOCAL_MACHINE`.  

        - **Clave** (obligatorio): especifique la clave del Registro para buscar en la sección anterior. Por ejemplo, `SOFTWARE\Microsoft\Office`.  

        - **Valor** (opcional): escriba un valor concreto para detectar en la clave anterior. Si quiere que el cliente detecte el valor (predeterminado), habilite la opción para **Usar valor de clave del Registro (predeterminado) para la detección**. Cuando escriba un valor o habilite esta opción, es preciso que seleccione un **tipo de datos**.  

        - **Esta clave del Registro está asociada con una aplicación de 32 bits en sistemas de 64 bits**: seleccione esta opción para buscar primero en las ubicaciones del Registro de 32 bits la clave del Registro especificada. Si no se encuentra la clave del registro, el cliente busca las ubicaciones de 64 bits.  

    - **Windows Installer**: detecte si un archivo de Windows Installer especificado existe en un dispositivo cliente. Esta detección indica que la aplicación está instalada. Especifique el **código de producto** MSI para detectar en el cliente. Si selecciona **Examinar**, elija el archivo MSI desde el que se va a leer el código de producto.

3. En la parte inferior de la ventana de la regla de detección, especifique si el elemento debe existir o cumplir una regla. Por ejemplo, si detecta un archivo, la opción siguiente se selecciona de forma predeterminada: **La configuración del sistema de archivos debe existir en el sistema de destino para indicar la presencia de esta aplicación**. Seleccione la otra opción para crear una regla de detección en función de las propiedades de archivo o carpeta. Estas propiedades incluyen la fecha de modificación, la fecha de creación, la versión o el tamaño. Estos criterios de regla son diferentes para cada tipo de configuración.  

4. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Regla de detección**.  

Cuando cree más de un método de detección para un tipo de implementación, puede crear una lógica más compleja mediante la agrupación de las cláusulas.  

#### <a name="group-detection-clauses-optional"></a>Agrupación de cláusulas de detección *(opcional)*

1. Cree tres o más cláusulas del método de detección en un tipo de implementación.  

2. Seleccione dos o más cláusulas consecutivas y, a continuación, elija **Grupo**. Verá los paréntesis agregados a las columnas asociadas, que mostrarán dónde empieza y acaba el grupo.  

    Ejemplo:

    | Conector  |  ( | Cláusula           |  )  |
    |------------|----|------------------|-----|
    |            |    | Código de producto de MSI |     |
    | \- O bien -         | (  | file1.text existe|     |
    | And        |    | file2.txt existe | )   |

3. Para quitar el grupo, seleccione las cláusulas agrupadas y, a continuación, Elija **Desagrupar**.  

*Continúe* con la siguiente sección sobre el uso de un script personalizado como método de detección. También puede *saltar* a las opciones de [Experiencia del usuario](#bkmk_dt-ux) para el tipo de implementación.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a> Usar un script personalizado para determinar la presencia de un tipo de implementación  

1. En la página **Método de detección**, seleccione el cuadro **Usar un script personalizado para detectar la presencia de este tipo de implementación**. Después, seleccione **Editar**.  

2. En el cuadro de diálogo **Editor de scripts**, seleccione un **tipo de script** para detectar el tipo de implementación: PowerShell, VBScript o JScript.  

    > [!Note]  
    > Cuando un script de Windows PowerShell se ejecuta como un método de detección de aplicaciones, el cliente de Configuration Manager llama a PowerShell con el parámetro `-NoProfile`. Esta opción inicia PowerShell sin perfiles. Un perfil de PowerShell es un script que se ejecuta cuando se inicia PowerShell. <!--3607762-->  

3. En el cuadro **Contenido del script**, escriba el script que quiera usar o pegue el contenido de un script existente. Elija **Abrir** para ir a un script existente guardado. Seleccione **Borrar** para quitar el texto en el campo de contenido del script. Si es necesario, habilite la opción **Ejecutar el script como proceso de 32 bits en clientes de 64 bits**.  

    > [!NOTE]  
    > El tamaño máximo para un script es 32 KB.  

4. Seleccione **Aceptar** para guardar el script y cerrar el cuadro de diálogo **Editor de script**. En el Asistente para crear tipos de implementación, los campos **Tipo de script** y **Longitud del script** se actualizan con detalles sobre el script.

#### <a name="about-custom-script-detection-methods"></a>Sobre los métodos de detección de scripts personalizados  

Configuration Manager comprueba los resultados del script. Lee los valores escritos por el script en la secuencia de salida estándar (STDOUT), la secuencia de error estándar (STDERR) y el código de salida. Si el script sale con un valor distinto de cero, se produce un error en el script y el estado de detección de la aplicación es *Desconocido*. Si el código de salida es cero y STDOUT contiene datos, el estado de detección de la aplicación es *Instalada*.

> [!TIP]
> Al escribir un script de detección, si devuelve un código de salida cero, pero no devuelve resultados (datos en STDOUT), la aplicación no se detectará como instalada. Para obtener más información, vea los ejemplos siguientes.

Use las siguientes tablas para comprobar a partir de la salida de un script si una aplicación está instalada:  

##### <a name="zero-exit-code"></a>Código de salida cero

|STDOUT|STDERR|Resultado del script|Estado de detección de la aplicación|
|---------|---------|---------|---------|
|Vacío|Vacío|Correcto|Sin instalar|
|Vacío|No está vacío|Error|Unknown|
|No está vacío|Vacío|Correcto|Instalado|
|No está vacío|No está vacío|Correcto|Instalado|

##### <a name="non-zero-exit-code"></a>Código de salida que no es cero

|STDOUT|STDERR|Resultado del script|Estado de detección de la aplicación|
|---------|---------|---------|---------|
|Vacío|Vacío|Error|Unknown|
|Vacío|No está vacío|Error|Unknown|
|No está vacío|Vacío|Error|Unknown|
|No está vacío|No está vacío|Error|Unknown|

##### <a name="examples"></a>Ejemplos

Use los siguientes ejemplos de PowerShell/VBScript para escribir sus propios scripts de detección de aplicaciones:  

**Ejemplo 1**: el script devuelve un código de salida que no es cero. Este código indica que el script no se pudo ejecutar correctamente. En este caso, el estado de detección de la aplicación es desconocido.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Ejemplo 2:** : el script devuelve un código de salida de cero, pero el valor de STDERR no está vacío. Este resultado indica que el script no se pudo ejecutar correctamente. En este caso, el estado de detección de la aplicación es desconocido.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Ejemplo 3**: el script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. En cambio, el valor de STDOUT está vacío, lo que indica que la aplicación no está instalada.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Ejemplo 4**: el script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. El valor de STDOUT está vacío, lo que indica que la aplicación no está instalada.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Ejemplo 5**: el script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. Los valores de STDOUT y STDERR no están vacíos, lo que indica que la aplicación está instalada.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a> Opciones de **experiencia del usuario** para el tipo de implementación

Esta configuración especifica cómo instala el cliente la aplicación en los dispositivos y lo que el usuario ve.  

En la página **Experiencia del usuario** , especifique la siguiente información:  

- **Comportamiento de instalación**: en la lista desplegable, seleccione una de las opciones siguientes:  

  - **Instalar para el usuario**: el cliente solo instala la aplicación para el usuario para el que se implementa la aplicación.  

  - **Instalar para el sistema**: el cliente instala la aplicación una sola vez. Está disponible para todos los usuarios.  

  - **Instalar para el sistema si el recurso es el dispositivo; de lo contrario, instalar para el usuario**: si implementa la aplicación para un usuario, el cliente solo la instala para ese usuario. Si implementa la aplicación para un usuario, el cliente solo la instala para ese usuario.  

- **Requisito de inicio de sesión**: Seleccione una de las siguientes opciones:  

  - **Solo cuando un usuario haya iniciado sesión**  

  - **Tanto si un usuario ha iniciado sesión como si no**  

  - **Solo cuando ningún usuario haya iniciado sesión**  

    > [!NOTE]  
    > El valor predeterminado de esta opción es **Solo cuando un usuario haya iniciado sesión**. Si se selecciona **Instalar para el usuario** en la lista desplegable **Comportamiento de la instalación**, esta opción no se puede cambiar.  

- **Visibilidad del programa de instalación**: especifica el modo en el que el tipo de implementación se ejecuta en los dispositivos cliente. Seleccione una de las siguientes opciones:  

  - **Maximizado**: el tipo de implementación se ejecuta en modo maximizado en los dispositivos cliente. Los usuarios ven toda la actividad de instalación.  

  - **Normal**: el tipo de implementación se ejecuta en modo normal en función de los valores predeterminados del programa y del sistema. Este es el modo predeterminado.  

  - **Minimizado**: el tipo de implementación se ejecuta en modo minimizado en los dispositivos cliente. Los usuarios pueden ver la actividad de instalación en el área de notificación o en la barra de tareas.  

  - **Oculto**: el tipo de implementación se ejecuta en modo oculto en los dispositivos cliente. Los usuarios no ven ninguna actividad de instalación.  

- **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**: especifique si un usuario puede interactuar con la instalación del tipo de implementación para configurar las opciones de instalación.  

    Si se seleccionó la opción **Instalar para el usuario** en la lista desplegable **Comportamiento de instalación**, esta opción está habilitada de forma predeterminada.  

    > [!IMPORTANT]  
    > Este valor es opcional cuando se selecciona el comportamiento **Instalar para el sistema**. Este cambio es principalmente para permitir que un usuario final interactúe con la instalación durante una secuencia de tareas. Por ejemplo, para ejecutar un proceso de instalación que solicite varias opciones al usuario final. En algunos instaladores de aplicaciones no se pueden silenciar los mensajes, o bien el proceso de instalación puede requerir valores de configuración específicos que solo conoce el usuario. <!--1356976-->  
    >  
    > Instalar en el contexto de sistema y permitir a los usuarios interactuar con la instalación no es una configuración segura. Para obtener más información, vea [Seguridad y privacidad de la administración de aplicaciones](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **Duración máxima permitida de la ejecución (minutos)** : especifique la duración máxima en minutos que espera que se ejecute el tipo de implementación en el equipo cliente. Especifique esta configuración como un número entero mayor que cero. El valor predeterminado es 120 minutos (dos horas).  

    Se puede usar este valor para las siguientes acciones:  

  - Para supervisar los resultados a partir del tipo de implementación.  

  - Comprobar si un tipo de implementación está instalado al definir ventanas de mantenimiento en los dispositivos cliente. Cuando se programa una ventana de mantenimiento, el tipo de implementación solo se inicia si hay suficiente tiempo disponible en la ventana de mantenimiento según el parámetro **Tiempo de ejecución máximo permitido**.  

    > [!IMPORTANT]  
    > Se puede producir un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el usuario configura el tiempo de ejecución máximo en un periodo superior a la duración de las ventanas de mantenimiento disponibles, ese tipo de implementación no se ejecuta.  

- **Tiempo de instalación estimado (minutos):** : especifique la duración estimada de la instalación del tipo de implementación. Los usuarios ven este tiempo en el Centro de Software.  

#### <a name="deployment-type-properties-user-experience-options"></a>Opciones de **experiencia del usuario** para propiedades del tipo de implementación

Al ver las propiedades de un tipo de implementación, las siguientes opciones solo aparecen en la pestaña **Experiencia del usuario**:

Aplicar un comportamiento específico posterior a la instalación. Seleccione una de las siguientes opciones:  

- **Determinar comportamiento en función de códigos de retorno**: controle los reinicios en función de los códigos configurados en la pestaña [Códigos de retorno](#bkmk_dt-return). En el Centro de software se muestra **Puede ser necesario reiniciar**. Si un usuario ha iniciado sesión durante la instalación, se le solicita según la configuración de la experiencia de usuario de la *implementación*.  

- **Ninguna acción específica**: no es necesario reiniciar después de la instalación. El Centro de software notifica que no es necesario reiniciar.  

- **El programa de instalación de software puede forzar un reinicio del dispositivo**: Configuration Manager no controla ni inicia un reinicio, pero es posible que la instalación real lo haga sin previo aviso. Use esta opción para impedir que Configuration Manager notifique el error de instalación cuando el programa de instalación inicia un reinicio. En el Centro de software se muestra **Puede ser necesario reiniciar**.  

- **El cliente de Configuration Manager forzará un reinicio obligatorio del dispositivo**: Configuration Manager fuerza un reinicio del dispositivo tras una instalación correcta. El Centro de software notifica que es necesario reiniciar. Si un usuario ha iniciado sesión durante la instalación, se le solicita según la configuración de la experiencia de usuario de la *implementación*.  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Requisitos** de tipos de implementación

Configuration Manager comprueba estos requisitos en los dispositivos antes de instalar el tipo de implementación. Utilice los requisitos para restringir y controlar los dispositivos o usuarios que reciben esta aplicación. Por ejemplo, si implementa la aplicación para una colección de usuarios, debe especificar aquí los requisitos de hardware de la aplicación.

1. En la página **Requisitos**, seleccione **Agregar** para abrir el cuadro de diálogo **Crear requisito**.  

2. En la lista desplegable **Categoría**, seleccione si este requisito es para un **dispositivo** o un **usuario**.  

    Seleccione **Personalizada** para usar una condición global creada previamente. Si elige **Personalizada**, también puede seleccionar **Crear** para crear una nueva condición global. Para obtener más información sobre las condiciones globales, consulte [Cómo crear condiciones globales](create-global-conditions.md).  

    > [!IMPORTANT]  
    > Si la aplicación se implementa en una recopilación de dispositivos, el cliente omite todos los requisitos con la categoría **Usuario** y la condición **Dispositivo primario**.  

3. En la lista desplegable **Condición**, seleccione la condición para evaluar si el usuario o el dispositivo cumplen los requisitos de instalación. El contenido de esta lista varía según la categoría seleccionada.  

4. En la lista desplegable **Operador**, seleccione el operador que se va a usar. Este operador compara la condición seleccionada con el valor especificado. Evalúa si el usuario o el dispositivo cumplen los requisitos de instalación. Los operadores disponibles varían según la condición seleccionada.  

    > [!Note]  
    > Los requisitos disponibles varían en función del tipo de dispositivo que use el tipo de implementación.  

5. En el cuadro **Valor**, especifique los valores que se van a usar para comparar. Estos valores, junto con la condición y el operador seleccionados, evalúan si el usuario o el dispositivo cumplen los requisitos de instalación. Los valores disponibles varían según la condición y el operador seleccionados.  

6. Seleccione **Aceptar** para guardar los requisitos y cierre el cuadro de diálogo **Crear requisito**.  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>**Dependencias** del tipo de implementación  

Las dependencias definen uno o más tipos de implementación de otra aplicación que el cliente debe instalar antes de instalar este tipo de implementación.

> [!IMPORTANT]  
> En algunos casos, un tipo de implementación depende de un tipo de implementación que también tiene dependencias. El número máximo de dependencias admitidas en la cadena es cinco.  

1. En la página **dependencias**, seleccione **Agregar**.  

2. En la ventana Agregar dependencia, escriba el **nombre del grupo de dependencias**. Este nombre hace referencia a este grupo de dependencias de aplicaciones.  

3. En la ventana Agregar dependencia, seleccione **Agregar**.  

4. En la ventana **Especificar aplicación requerida**, seleccione una aplicación disponible y al menos uno de sus tipos de implementación para utilizarlo como una dependencia.  

    > [!TIP]  
    > Seleccione **Ver** para mostrar las propiedades de la aplicación o del tipo de implementación seleccionado.  

5. Seleccione **Aceptar** para cerrar la ventana **Especificar aplicación requerida**.  

6. Si quiere que el cliente instale automáticamente la aplicación dependiente, seleccione **Instalación automática** junto a la dependencia.  

    > [!NOTE]  
    > No es necesario implementar una aplicación dependiente para que el cliente la instale automáticamente.  

7. Si agrega más de una dependencia, haga clic en los botones **Aumentar prioridad** y **Reducir prioridad**. Estas acciones cambian el orden en que el cliente evalúa cada dependencia.  

8. Seleccione **Aceptar** para cerrar la ventana **Agregar dependencia**.  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>**Códigos de retorno** del tipo de implementación

> [!Note]  
> Esta página no está en el Asistente para crear tipos de implementación. Solo es una pestaña en las propiedades de un tipo de implementación existente.  

Especifique los códigos de retorno para controlar los comportamientos al finalizar el tipo de implementación. Por ejemplo, indique que se requiere un reinicio, la instalación se ha completado.

1. En la pestaña **Códigos de retorno** de la ventana de propiedades del tipo de implementación, haga clic en **Agregar**.  

2. En la ventana Agregar código de retorno, especifique el **valor del código de retorno** esperado de este tipo de implementación. Este valor es un entero positivo o negativo comprendido entre `-2147483648` y `2147483647`.  

3. Seleccione una **tipo de código** de la lista desplegable. Esta configuración define cómo Configuration Manager interpreta el código de retorno especificado de este tipo de implementación. Los tipos disponibles varían en función de la tecnología de tipo de implementación.  

    - **Correcto (sin reinicio)** : el tipo de implementación se instaló correctamente y no es necesario reiniciar.  

    - **Error (sin reinicio)** : no se pudo instalar el tipo de implementación.  

    - **Reinicio en frío**: el tipo de implementación se instaló correctamente, pero requiere reiniciar el dispositivo. Nada se puede instalar hasta que se reinicie el dispositivo.  

    - **Reinicio parcial**: el tipo de implementación se instaló correctamente, pero requiere reiniciar el dispositivo. Pueden realizarse otras instalaciones antes de que el dispositivo se reinicie.  

    - **Reintento rápido**: otra instalación ya está en curso en el dispositivo. El cliente lo reintenta cada dos horas, hasta un total de 10 veces.  

4. Opcionalmente, especifique un **nombre** y una **descripción** para este código de retorno.

5. Seleccione **Aceptar** para cerrar la ventana Agregar código de retorno.  

#### <a name="example-non-zero-success"></a>Ejemplo: correcto distinto de cero

Va a implementar una aplicación que devuelve un código de salida de `1` cuando se instala correctamente. De forma predeterminada, Configuration Manager detecta este código de retorno distinto de cero como un error. Especifique el valor de código de retorno de `1` y seleccione el tipo de código **correcto (sin reinicio)** . Ahora Configuration Manager interpreta ese código de retorno como una operación correcta para este tipo de implementación.

#### <a name="default-return-codes"></a>Códigos de retorno predeterminados

Al crear algunos tipos de implementación, Configuration Manager agrega automáticamente los siguientes códigos de retorno que son comunes a esa tecnología:  

##### <a name="windows-installer-msi-file"></a>Windows Installer (archivo \*.msi)

|Valor    |Tipo de código|
|---------|---------|
|0        |Correcto (sin reinicio)|
|1707     |Correcto (sin reinicio)|
|3010     |Reinicio parcial|
|1641     |Reinicio en frío|
|1618     |Reintento rápido|

##### <a name="script-installer"></a>Instalador de scripts

|Valor    |Tipo de código|
|---------|---------|
|0        |Correcto (sin reinicio)|
|1641     |Reinicio en frío|
|3010     |Reinicio parcial|
|1618     |Reintento rápido|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Paquete de aplicación de Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)

|Valor    |Tipo de código|
|---------|---------|
|15605    |Reintento rápido|
|15618    |Reintento rápido|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a> Opciones adicionales de los tipos de implementación de App-V  

Configure opciones adicionales únicas para los tipos de implementación para aplicaciones virtuales (App-V).  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a> Opciones de **contenido** de tipo de implementación de App-V  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2. Seleccione una aplicación con un tipo de implementación de App-V y elija **Propiedades**.  

3. En las propiedades de la aplicación, cambie a la pestaña **Tipos de implementación**. Seleccione el tipo de implementación de App-V y elija **Editar**.  

4. En las propiedades del tipo de implementación, cambie a la pestaña **Contenido**. Configure las siguientes opciones según sea necesario:  

    - **Conservar contenido en la caché del cliente**: el cliente de Configuration Manager no eliminará de su caché el contenido de este tipo de implementación.  

    - **Cargar contenido en la memoria caché de App-V antes del inicio**: antes de iniciar la aplicación, el cliente de Configuration Manager carga en la caché de App-V todo el contenido de este tipo de implementación. El cliente no ancla el contenido en la memoria caché. Elimina el contenido según sea necesario.  

5. Seleccione **Aceptar** para cerrar las propiedades del tipo de implementación. Después, seleccione **Aceptar** para cerrar las propiedades de la aplicación.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a> Opciones de **publicación** del tipo de implementación de App-V

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2. Seleccione una aplicación con un tipo de implementación de App-V y elija **Propiedades**.  

3. En las propiedades de la aplicación, cambie a la pestaña **Tipos de implementación**. Seleccione el tipo de implementación de App-V y elija **Editar**.  

4. En las propiedades del tipo de implementación, cambie a la pestaña **Publicar**. Seleccione los elementos de la aplicación virtual que quiera publicar.  

5. Seleccione **Aceptar** para cerrar las propiedades del tipo de implementación. Después, seleccione **Aceptar** para cerrar las propiedades de la aplicación.  

## <a name="import-an-application"></a><a name="bkmk_import"></a> Importar una aplicación  

Use el siguiente procedimiento para importar una aplicación en Configuration Manager:

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2. En la cinta de opciones, en la pestaña **Inicio** y en el grupo **Crear**, seleccione **Importar aplicación**.  

3. En la página **General** del Asistente para importar aplicaciones, especifique la ruta de acceso de red al **archivo** que se importará. Por ejemplo, `\\server\share\file.zip`. Este archivo es un archivo comprimido válido (formato ZIP) de una aplicación de Configuration Manager exportada.  

4. En la página **Contenido del archivo**, seleccione la acción que se va a realizar si esta aplicación es un duplicado de una existente. Cree una aplicación u omita el duplicado y agregue una nueva revisión de la aplicación existente.  

5. En la página **Resumen**, revise las acciones y después finalice el asistente.  

La nueva aplicación se muestra en el nodo **Aplicaciones** .  

> [!TIP]  
> El cmdlet de Windows PowerShell **Import-CMApplication** realiza la misma función que este procedimiento. Para obtener más información, vea [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Para obtener más información sobre cómo exportar una aplicación, consulte [Tareas de administración para aplicaciones](management-tasks-applications.md).

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a> Tipos de implementación compatibles  

Configuration Manager admite los siguientes tipos de implementación para aplicaciones:

| Nombre de tipo de implementación | Descripción |
|--------------------------|----------------------|  
| **Windows Installer (archivo \*.msi)** | Un archivo de Windows Installer. |  
| **Paquete de aplicación de Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** | Un archivo de paquete de aplicación de Windows (.appx), un paquete de lote de aplicaciones de Windows (.appxbundle), un paquete de aplicación de Windows 10 (.msix) o un lote de aplicaciones de Windows 10 (.msixbundle).<!--1357427--> |  
| **Paquete de aplicación de Windows (en la Tienda Windows)** | Especifique un vínculo a la aplicación en Microsoft Store o busque en la tienda para seleccionar la aplicación.<sup>[Nota 1](#bkmk_note1)</sup> |  
| **Instalador de scripts** | Especifique un script o programa que se ejecuta en los clientes de Windows para instalar contenido o llevar a cabo una acción. Use este tipo de implementación para los instaladores setup.exe o los contenedores de scripts. |  
| **Microsoft Application Virtualization 4** | Un manifiesto de Microsoft App-V v4. |  
| **Microsoft Application Virtualization 5** | Un archivo de paquete de Microsoft App-V v5. |  
| **Paquete de aplicación de Windows Phone (archivo \*.xap)** | Un archivo de paquete de aplicación de Windows Phone. |  
| **Paquete de aplicación de Windows Phone (en la Tienda de Windows Phone)** | Especifique un vínculo a la aplicación en la Tienda Windows. |  
| **Mac OS X** | Para equipos Mac que ejecutan el cliente de Configuration Manager. Cree un archivo .cmmac con la herramienta **CMAppUtil**. |  
| **Aplicación web** | Especifique un vínculo a una aplicación web. Este tipo de implementación instala un acceso directo a la aplicación web en el dispositivo del usuario. |  
| **Windows Installer a través de MDM (\*.msi)** | Cree e implemente aplicaciones basadas en Windows Installer en dispositivos Windows 10. Para obtener más información, vea [Implementar aplicaciones de Windows Installer en equipos de Windows 10 inscritos con MDM](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Secuencia de tareas** | A partir de la versión 2002, instale o desinstale aplicaciones complejas mediante secuencias de tareas. Para obtener más información, consulte [Tipo de implementación de la secuencia de tareas](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> La consola de Configuration Manager puede mostrar otros tipos de implementación, pero para las plataformas que ya no se admiten. Para más información, consulte [¿Qué ha ocurrido con la MDM híbrida?](../../mdm/understand/what-happened-to-hybrid.md)

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a> Nota 1: Paquete de aplicación de Windows (en la Tienda Windows)

Para implementar la aplicación como un vínculo a Microsoft Store, establezca la directiva de grupo **Desactivar la aplicación Tienda**. Establézcala en **Deshabilitado** o **No configurado**. Si habilita esta opción, los clientes no pueden conectarse a la Tienda Windows para descargar e instalar aplicaciones.

Los clientes de Windows siempre evalúan los tipos de implementación que usan un vínculo a una tienda antes de otros tipos de implementación. Después, el cliente evalúa los tipos de implementación por prioridad.

> [!TIP]
> Algunos vínculos de la tienda pueden generar el error siguiente en el Asistente para crear aplicaciones: "vínculo de aplicación no válido". Por ejemplo, algunas *aplicaciones destacadas* de la tienda pueden generar este error. De todos modos puede seleccionar **Siguiente** en la página **General** del Asistente. Configuration Manager crea correctamente la aplicación y puede implementarla sin problemas.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Pasos siguientes

Después de crear una aplicación en Configuration Manager, el paso siguiente consiste en [implementar la aplicación](deploy-applications.md).

A partir de la versión 1906, cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación. Para más información, consulte [Crear grupos de aplicaciones](create-app-groups.md).

Para obtener más información sobre cómo crear aplicaciones en distintas plataformas de sistema operativo, consulte los siguientes artículos:  

- [Crear aplicaciones de Windows](../get-started/creating-windows-applications.md)
- [Crear aplicaciones de Mac](../get-started/creating-mac-computer-applications.md)
- [Crear aplicaciones de servidor de UNIX y Linux](../get-started/creating-linux-and-unix-server-applications.md)
- [Crear aplicaciones de Windows Embedded](../get-started/creating-windows-embedded-applications.md)
