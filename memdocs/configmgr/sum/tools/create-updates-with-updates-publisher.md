---
title: Creación de actualizaciones
titleSuffix: Configuration Manager
description: Crear y agrupar actualizaciones de software con System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708703"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Crear actualizaciones de software y actualizar agrupaciones con Updates Publisher

*Se aplica a: System Center Updates Publisher*

Con Updates Publisher puede usar el asistente para **crear actualizaciones** para crear sus propias actualizaciones y el asistente para **crear agrupaciones** para crear agrupaciones de actualizaciones.

Dado que estos dos asistentes tienen un flujo de trabajo similar, el procedimiento para crear un paquete de actualización hace referencia al procedimiento para crear actualizaciones, con solo las diferencias más relevantes detalladas.

## <a name="use-the-create-update-wizard"></a>Usar el asistente para crear actualizaciones
1. En la consola, vaya a **Updates Workspace** (Área de trabajo Actualizaciones) y luego, en el panel **Introducción**, elija **Actualizar** en la pestaña **Inicio** de la cinta de opciones. Se abrirá el asistente para **crear actualizaciones**.

2. En la página **Paquete**, use la información siguiente como ayuda para configurar la actualización:

   -   Elija **Examinar** para buscar el paquete de actualización de software que va a usar como origen del paquete. Entre los orígenes válidos se incluyen archivos .MSI, .MSP o .EXE. Updates Publisher requiere acceso al archivo para crear un hash de archivo. El nombre de archivo y de hash se usan después en los metadatos de actualización de la actualización que se va a crear.

   -   Especifique la ubicación de origen del contenido de esta actualización. Normalmente, se trata de la ubicación desde donde se descargarán los archivos binarios de actualización durante la publicación en un servidor WSUS.  Si está seleccionada la opción **Use a local source to publish software update content** (Utilizar un origen local para publicar contenido de la actualización de software), la ruta de acceso no es necesaria.

       Más adelante, cuando la actualización se publique en un servidor WSUS, Updates Publisher descarga los archivos binarios de la actualización de la ubicación de origen indicada.  Si no se proporciona ninguna ruta de acceso, Update Publisher buscará la [ruta de acceso de publicación de origen local](updates-publisher-options.md#advanced) para los archivos binarios de actualización.

   -   Especifique el **Binary language** (Lenguaje binario) de la actualización de software.

   -   Especifique **Success return codes** (Códigos de retorno correctos) y **Success pending reboot codes** (Códigos de reinicio pendiente correctos) para la actualización. Separe varios códigos de retorno con una coma. Puede usar códigos de retorno para determinar cuándo la instalación de actualización se realizó correctamente y cuando era necesario reiniciar el equipo.

       -   Los archivos y las revisiones (archivos .MSI y .MSP) de Windows Installer establecen automáticamente estos valores, que no pueden modificarse.

       -   Para actualizaciones de .EXE, se usan los códigos predeterminados definidos por el archivo .EXE si no se especifica ningún código de retorno.

   -   Especifique los argumentos de línea de comandos necesarios para instalar la actualización de software.

       -   Los archivos y las revisiones (archivos .MSI y .MSP) de Windows Installer establecen automáticamente estos valores. Para estos tipos de archivos, los argumentos deben especificarse como **\[nombre\]=\[valor\]** . Además, todas las opciones que empiezan por un **/** (como **/qn**) no son compatibles con actualizaciones de software de .MSI o .MSP.

       -   Para actualizaciones de .EXE, son válidos todos los argumentos.

3. En la página **Información**, especifique detalles de la actualización que se incluyan cuando la actualización se publique o exporte. Entre los detalles se incluyen propiedades localizadas tales como el nombre (título) y la descripción de las actualizaciones. Luego, puede especificar detalles más generales, como, por ejemplo, la clasificación, el proveedor, el producto y dónde obtener más información sobre la actualización.

    __Propiedades localizadas:__

   - **Idioma**: seleccione un idioma y luego especifique un título y una descripción. Después puede seleccionar idiomas adicionales, uno a uno, donde cada idioma admite su propio título y descripción.

   - **Título**: escriba el nombre de la actualización. Este nombre se muestra en el área de trabajo Actualizaciones de la consola de Updates Publisher.

   - **Descripción**: descripción detallada de la actualización. Puede incluir lo que instala la actualización, además de cómo y cuándo se debe usar.

   **Clasificación**: estas son algunas descripciones frecuentes para las distintas clasificaciones.

   - **Actualización**: actualización de una aplicación o un archivo que está instalado actualmente.

   - **Crítica**: actualización de amplia distribución para un problema específico que resuelve un error crítico no relacionado con la seguridad.

   - **Feature Pack**: nuevas características de producto que se distribuyen fuera de una versión del producto y que normalmente se incluyen en la siguiente versión completa del producto.

   - **Seguridad**: actualización de amplia distribución para un problema específico del producto, relacionado con la seguridad.

   - **Paquete acumulativo de actualizaciones**: conjunto acumulativo de revisiones que se recopilan para facilitar la implementación. Estas revisiones pueden incluir actualizaciones de seguridad, actualizaciones críticas, actualizaciones, etc. Un paquete acumulativo de revisiones suele relacionarse, por lo general, con un área específica; por ejemplo, una característica del producto o de la seguridad.

   - **Service Pack**. conjunto acumulativo de revisiones correspondientes a una aplicación. Estas revisiones pueden incluir actualizaciones de seguridad, actualizaciones críticas, actualizaciones de software, etc.

   - **Herramienta**: especifica una herramienta o característica que ayuda a realizar una o varias tareas.

   - **Controlador**: actualización del software de controlador.

   **Proveedor**: especifica un proveedor para actualización. Puede usar la lista desplegable para usar valores de actualizaciones que se encuentran en el repositorio. Cuando especifique un proveedor, el asistente crea una carpeta con el nombre del proveedor en **Todas las actualizaciones de software** en el **área de trabajo Actualizaciones** si esa carpeta no existe ya. Los siguientes son nombres reservados de Windows Server Update Services (WSUS) que no se pueden especificar para actualizaciones creadas por el usuario:
   - Microsoft Corporation
   - Microsoft
   - Actualizar
   - Actualización de software
   - Herramientas
   - Herramienta
   - Crítica
   - Actualizaciones críticas
   - Seguridad
   - Actualizaciones de seguridad
   - Feature Pack
   - Paquete acumulativo de actualizaciones
   - Service Pack
   - Controlador
   - Actualización de controlador
   - Agrupación
   - Actualización de agrupación

   **Producto**: especifique el tipo de producto al que se destina la actualización. Puede usar la lista desplegable para usar valores de actualizaciones que se encuentran en el repositorio. La misma lista de nombres reservados de WSUS que no se pueden usar con **Proveedor**, tampoco se pueden usar con **Producto**.

   **URL de información adicional**: especifique la dirección URL donde se encuentra más información sobre esta actualización. Debe usar letras minúsculas en **https** o **http** al escribir esta dirección URL.

4. En la página **Información opcional**, puede configurar detalles que ofrezcan información adicional sobre la actualización.

   -   **Id. de boletín**: los identificadores de boletín suelen proporcionarlos los proveedores de actualización, aunque no siempre.

   -   **Id. de artículo**: si hay un articulo de actualización de software disponible, este identificador puede resultar útil para quienes busquen información adicional sobre la actualización.

   -   **CVE IDs** (Id de CVE): muestra uno o varios identificadores de Common Vulnerabilities and Exposures (Vulnerabilidades y exposiciones comunes, CVE) que ofrecen información de seguridad sobre la actualización o la agrupación de actualizaciones. Cuando muestre más de uno, use punto y coma para separar los identificadores de CVE; por ejemplo: *CVE1;CVE2.*

   -   **Dirección URL de soporte**: muestra la dirección URL que contiene información de soporte técnico para esta actualización, si está disponible. Debe usar letras minúsculas en **https** o **http** al escribir esta dirección URL.

   -   **Gravedad**: establezca el nivel de gravedad de esta actualización.

   -   **Impacto**: pueden usarse las siguientes opciones para especificar el impacto:
       -   **Normal** : use esta opción para indicar que la actualización requiere procedimientos de instalación típica.
       -   **Menor**: use esta opción para indicar que la actualización requiere procedimientos de instalación mínima.
       -   **Requires exclusive handling** (Requiere manipulación exclusiva): use esta opción para indicar que la actualización debe instalarse automáticamente, excluyente de otras actualizaciones.   <br /><br />

   -   **Comportamiento de reinicio**: use esta opción para proporcionar información sobre el comportamiento de reinicio de las actualizaciones. Esta opción no afecta al comportamiento real de la instalación de actualización.

       -   **Never reboots** (No se reinicia nunca): el equipo no realiza nunca un reinicio del sistema después de instalar la actualización de software.
       -   **Always requires reboot** (Siempre requiere reinicio): el equipo realiza siempre un reinicio del sistema después de instalar la actualización de software.
       -   **Can request reboot** (Puede solicitar reinicio): después de instalar la actualización de software, el equipo solicita un reinicio del sistema solo en caso necesario. El usuario tiene la posibilidad de posponer el reinicio. Es el valor predeterminado. <br /><br />

5. En la página **Requisitos previos**, especifique los requisitos previos que deben instalarse en un equipo para poder instalar esta actualización. Los requisitos previos pueden ser **detectoids** u otras actualizaciones. Los detectoids son reglas de alto nivel como, por ejemplo, una que requiera que la CPU de los equipos sea un procesador de 64 bit. Los detectoids también pueden especificar actualizaciones que deben instalarse para poder instalar esta actualización.

   -   Para mejorar el rendimiento, use detectoids en lugar de crear reglas *instalables* e *instaladas* que realicen la misma comprobación o acción.

   Use la opción de búsqueda de **Available software updates and detectoids** (Actualizaciones de software y detectoids disponibles) para que le ayude a encontrar determinadas actualizaciones o detectoids. Por ejemplo, realice una búsqueda sobre **CPU** para encontrar los detectoids que le permiten limitar la instalación en función de una determinada arquitectura de CPU.

   Puede seleccionar uno o varios elementos a la vez para agregarlos como requisitos previos. Al agregar requisitos previos, los detectoids seleccionados se agregan como uno o varios grupos. Para optar a la instalación, un equipo debe cumplir el requisito de un miembro al menos de cada grupo que se configure:

   -   Al hacer clic en **Add Prerequisite** (Agregar requisito previo), todos los detectoids que ha seleccionado se agregan a los distintos grupos individuales. Para optar a esta instalación, un equipo debe cumplir el requisito previo de este grupo y pasar los requisitos de los grupos adicionales que están configurados.

   -   Al hacer clic en **Agregar grupo**, todos los elementos que ha seleccionado se agregan a un solo grupo. Para optar a esta instalación, un equipo debe cumplir al menos uno de los requisitos previos de este grupo y pasar los requisitos de los grupos adicionales que están configurados.

6. En la página **Sustitución**, especifique las actualizaciones que se reemplazan (sustituyen) por esta actualización. Cuando esta actualización se publique, Configuration Manager marcará cada actualización que se ha sustituido como **Caducada**. Los clientes instalarán luego esta actualización en lugar de las actualizaciones sustituidas.

7. En la página **Aplicabilidad**, use el **Editor de reglas** para definir un conjunto de reglas que determinen si un dispositivo necesita esta actualización. (Esta página es similar a la página **Instalado** que la sigue).

   Para agregar una nueva regla, haga clic en ![Nueva regla](media/newrule.png). Se abrirá la página Applicability Rule (Regla de aplicabilidad), donde puede configurar reglas.

   Entre los tipos de reglas que puede crear se incluyen:

   -   **Archivo**: use esta regla para exigir que un dispositivo tenga un archivo con propiedades que cumplan uno o más criterios que se especifiquen para poder aplicar esta actualización.

   -   **Registro**: use este tipo para especificar detalles del Registro que deben estar presentes para que un dispositivo cumpla los requisitos para instalar esta actualización.

   -   **Sistema**: esta regla usa detalles del sistema para determinar la aplicabilidad. Puede elegir entre definir una versión de Windows, un idioma de Windows o la arquitectura del procesador, o especificar una consulta WMI que identifique el sistema operativo de los dispositivos.

   -   **Windows Installer**: use este tipo de regla para determinar la aplicabilidad en función de un .MSI instalado o una revisión de Windows Installer (.MSP). También puede determinar si determinados componentes o características se instalan como parte del requisito.

       > [!IMPORTANT]  
       > En dispositivos administrados, el nuevo Agente de Windows Update no puede detectar paquetes de instalación de Windows instalados por usuario. Cuando use este tipo de regla, configure reglas de aplicabilidad adicionales, como versiones de archivo o valores de la clave del Registro, para que el paquete de Windows Installer pueda detectarse adecuadamente independientemente del criterio, por usuario o por sistema.

   -   **Saved rule** (Regla guardada): esta opción le permite buscar y usar reglas que haya *creado en el área de trabajo Reglas*.

       Después de crear una regla, puede usar otros iconos para modificar la regla y, si hay varias reglas, para definir relaciones entre esas reglas.

   Cuando haya terminado de crear y agregar reglas, haga clic en **Aceptar** en el cuadro de diálogo **Create Rule Set** (Crear conjunto de reglas) para guardar ese conjunto. Luego puede crear una **nueva** regla y agregarla también al conjunto.

   Cuando tiene varias reglas o varios conjuntos de reglas que agregar a una actualización, puede usar los operadores lógicos en el **Editor de reglas** para determinar las condiciones entre las reglas y el orden en que se procesan.

8. En la página **Instalado**, use el **Editor de reglas** para definir un conjunto de reglas que determinen si un dispositivo tiene ya instalada la actualización que está configurando. (Esta página es similar a la página **Aplicabilidad** que la precede).

   Esta página del asistente admite la configuración de reglas con las mismas opciones y criterios que la página **Aplicabilidad**.

   Cuando el asistente termine, la nueva actualización se agrega a un nodo en el **área de trabajo Actualizaciones** que se identifica con el nombre del **Proveedor** y el **Producto** que se use para la actualización.

## <a name="use-the-create-bundle-wizard"></a>Usar el asistente para crear agrupaciones
Puesto que este asistente usa el mismo flujo de trabajo que el asistente para [crear actualizaciones](#use-the-create-update-wizard), use ese flujo de trabajo, pero tenga en cuenta la siguiente diferencia de las agrupaciones:

1.  Para iniciar el asistente, vaya a **Updates Workspace** (Área de trabajo Actualizaciones) en la consola y luego seleccione **Agrupación** en la pestaña **Inicio** de la cinta de opciones.

2.  A diferencia del asistente para crear actualizaciones, no hay ninguna página Paquete cuando se crea una agrupación.

3.  En la página **Información**, especifique detalles de la agrupación de actualizaciones que se incluyan cuando la actualización se publique o exporte.

4.  En la página **Información opcional**, puede configurar detalles que ofrezcan información adicional sobre la agrupación de actualizaciones. Las opciones disponibles son las mismas que para crear una actualización. Pero las opciones Impacto y Comportamiento de reinicio no están disponibles ya que no se aplican a agrupaciones.

5.  En la página **Requisitos previos**, especifique los requisitos previos que deben instalarse en un equipo para poder instalar esta agrupación. Estas reglas son las mismas vistas en el caso de actualizaciones individuales.

6.  En la página **Sustitución**, especifique las actualizaciones que se reemplazan (sustituyen) por esta agrupación. Estas reglas son las mismas vistas en el caso de actualizaciones individuales.

7.  En la página **Miembros**, seleccione actualizaciones para agregarlas a la agrupación de actualizaciones. Solo están disponibles las actualizaciones que ha creado o importado a Updates Publisher.

Cuando el asistente termine, la nueva agrupación de actualizaciones se agrega a un nodo en el **área de trabajo Actualizaciones** que se identifica con el nombre del **Proveedor** que se use para la agrupación de actualizaciones.
