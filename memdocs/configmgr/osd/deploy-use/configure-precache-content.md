---
title: Configuración del contenido de la caché previa
titleSuffix: Configuration Manager
description: Conozca cómo pueden los clientes descargar el contenido de la implementación del sistema operativo antes de que un usuario instale la secuencia de tareas.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 184bdc58ac6dc0e311875cc1ddab8c605d8eec32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704213"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Configuración del contenido de la caché previa para secuencias de tareas

*Se aplica a: Configuration Manager (rama actual)*

<!--1021244-->
La característica de caché previa para las implementaciones disponibles de secuencias de tareas permite que los clientes descarguen el contenido pertinente antes de que un usuario instale la secuencia de tareas. El cliente puede almacenar en la caché el contenido de las secuencias de tareas antes de [actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) o [instalar una imagen de sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

> [!Note]  
> En la versión 1910, Configuration Manager habilita esta característica opcional de forma predeterminada, mientras que en la versión 1906 o anteriores no lo hace. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Por ejemplo, solo quiere una secuencia de tareas de actualización en contexto para todos los usuarios y tiene muchas arquitecturas y lenguajes. En versiones anteriores, el contenido se comienza a descargar cuando el usuario instala una implementación de secuencia de tareas disponible desde el Centro de software. Este retraso agrega tiempo adicional antes de que la instalación esté lista para iniciarse. Se descarga todo el contenido al que se hace referencia en la secuencia de tareas. Este contenido incluye el paquete de actualización de sistema operativo para todos los lenguajes y arquitecturas. Si cada paquete de actualización tiene aproximadamente 3 GB de tamaño, el contenido total es muy grande.

El contenido de caché previa proporciona la opción al cliente de descargar solo el contenido aplicable y otro contenido al que se haga referencia, tan pronto como reciba la implementación. Cuando el usuario hace clic en **Instalar** en el Centro de software, el contenido está listo. La instalación se inicia rápidamente porque el contenido está en el disco duro local.

En Configuration Manager, versión 1902 y anteriores, este comportamiento solo se aplica al *paquete de actualización del sistema operativo*. Ese paquete es el único contenido en el que se especifica la arquitectura o el idioma correspondiente. Por ejemplo, si la secuencia de tareas también hace referencia a varios paquetes de controladores, el cliente los descarga todos. El motor de secuencia de tareas evalúa las condiciones en los pasos cuando se ejecuta la secuencia de tareas, no con antelación. El cliente usa las etiquetas de las propiedades del paquete para determinar qué contenido se almacena en la caché previa.

A partir de la versión 1906,<!--4224642--> puede usar el almacenamiento en caché previo para reducir el consumo de ancho de banda de los siguientes tipos de contenido:

- Paquetes de actualización del sistema operativo
- Imágenes de SO
- Paquetes de controladores
- Paquetes

## <a name="configure-pre-caching"></a>Configuración del almacenamiento en caché previo

Hay tres pasos para configurar la característica de caché previa:

1. [Crear y configurar los paquetes](#bkmk_createpkg)
2. [Crear una secuencia de tareas con pasos condicionales](#bkmk_createts)
3. [Implementar la secuencia de tareas y habilitar el almacenamiento en caché previo](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a> 1. Crear y configurar los paquetes

El cliente evalúa los atributos de los paquetes para determinar qué contenido se descarga durante el almacenamiento en caché previo.  

#### <a name="os-upgrade-package"></a>Paquete de actualización del sistema operativo

Cree [paquetes de actualización del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) para arquitecturas e idiomas específicos. Especifique la **Arquitectura** y el **Idioma** en la pestaña **Origen de datos** de sus propiedades.

#### <a name="os-image"></a>Imagen del sistema operativo

Cree [imágenes del sistema operativo](../get-started/manage-operating-system-images.md) para idiomas y arquitecturas específicos. Especifique la **Arquitectura** y el **Idioma** en la pestaña **Origen de datos** de sus propiedades.

#### <a name="driver-package"></a>Paquete de controladores

Cree [paquetes de controladores](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) para los modelos de hardware específicos. Especifique el **Modelo** en la pestaña **General** de sus propiedades.

Para determinar qué paquete de controladores descarga durante el almacenamiento en la caché previa, el cliente evalúa el modelo en comparación con la propiedad **Nombre** de la clase de WMI **Win32_ComputerSystemProduct**.

> [!TIP]
> La consulta real usa una instrucción `LIKE` con caracteres comodín: `select * from win32_computersystemproduct where name like "%yourstring%"`. Por ejemplo, si especifica `Surface` como modelo, la consulta devuelve todos los modelos que incluyen esa cadena.<!-- 6315551 -->

#### <a name="package"></a>Paquete

Cree [paquetes](../../apps/deploy-use/packages-and-programs.md) para idiomas y arquitecturas específicos. Especifique la **Arquitectura** y el **Idioma** en la pestaña **General** de sus propiedades.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a> 2. Creación de una secuencia de tareas

Cree una secuencia de tareas con pasos condicionales para los diferentes idiomas y arquitecturas, o los distintos modelos de hardware de los paquetes del controlador.

|Content|Paso|
|---------|---------|
|Paquete de actualización del sistema operativo|[Actualizar el sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|Imagen del sistema operativo|[Aplicar imagen del sistema operativo](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Paquete de controladores|[Aplicar paquete de controladores](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Paquete|[Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Por ejemplo, en el siguiente paso de **actualización del sistema operativo** se usa la versión en inglés:  

![Editor de secuencia de tareas en el que se muestran varios pasos de actualización del sistema operativo para ENU, DEU y JPN](../media/precacheproperties2.png)

![Pestaña Opciones del editor de secuencia de tareas, en la que se muestra la consulta WQL de WMI para la Configuración regional y OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> La siguiente consulta de WMI se recomienda para el sistema operativo Inglés (Estados Unidos) y la arquitectura de 64 bits:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Primero agregue el idioma al seleccionar la condición **Idioma del sistema operativo**. Luego edite la consulta de WMI para incluir la cláusula de arquitectura.


### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a> 3. Implementar la secuencia de tareas

[Implemente la secuencia de tareas](deploy-a-task-sequence.md). Para la característica de caché previa, configure las opciones siguientes:  

- En la pestaña **General**, seleccione **Descargar contenido previamente para esta secuencia de tareas**.  

- En la pestaña **Configuración de implementación**, configure la secuencia de tareas como **Disponible**.  

- En la pestaña **Programación**, elija la hora seleccionada actualmente para la opción **Programar cuándo estará disponible esta implementación**. El cliente inicia el almacenamiento del contenido en la caché previa a la hora de disponibilidad de la implementación. Cuando un cliente de destino recibe esta directiva, la hora disponible se encuentra en el pasado, por lo que la descarga en la caché previa se inicia inmediatamente. Si el cliente recibe esta directiva pero la hora disponible está en el futuro, el cliente no inicia el almacenamiento del contenido en la caché previa hasta la hora disponible.  

- En la pestaña **Puntos de distribución**, configure los valores **Opciones de implementación**. Si el contenido no se ha almacenado previamente en la caché antes de que un usuario inicie la instalación, el cliente usa esta configuración.  

    > [!Important]  
    > En una secuencia de tareas que instala una imagen de sistema operativo, no use la opción de implementación **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**. Cuando la secuencia de tareas borra el disco antes de aplicar la imagen del sistema operativo, quita la caché cliente. Puesto que el contenido ya no está, se produce un error en la secuencia de tareas.<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>Experiencia del usuario

- Cuando el cliente recibe la directiva de implementación, inicia el almacenamiento del contenido en la caché previa después de la hora disponible de la implementación. Este contenido incluye todos los paquetes a los que se hace referencia, pero solo el paquete de actualización del sistema operativo que coincide con los atributos de idioma y arquitectura del paquete.  

- Cuando el cliente pone la implementación a disposición de los usuarios, se muestra una notificación para informarles sobre la nueva implementación. Ahora la secuencia de tareas es visible en el Centro de software. El usuario puede ir al Centro de software y hacer clic en **Instalar** para iniciar la instalación.  

- Si el cliente no ha almacenado previamente en la caché el contenido cuando el usuario instala la secuencia de tareas, el cliente usa la configuración que se especifique en la pestaña **Opción de implementación** de la implementación.  


## <a name="see-also"></a>Vea también

- [Creación de una secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Escenario para actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)
