---
title: Introducción a la administración de aplicaciones
titleSuffix: Configuration Manager
description: Obtenga la información básica que necesitará para administrar e implementar las aplicaciones de Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b2fc0dfe37ad51ce1a549545c3eaa716395438d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347119"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Introducción a la administración de aplicaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo, aprenderá los conceptos básicos antes de empezar a trabajar con aplicaciones de Configuration Manager.  

> [!TIP]  
> Si ya está familiarizado con la forma de administrar aplicaciones en Configuration Manager, omita este artículo. Continúe con la creación de una aplicación de ejemplo: [Crear e implementar una aplicación](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>¿Qué es una aplicación?

Aunque *aplicación* o *app* es un término ampliamente usado en informática, en Configuration Manager significa algo específico. Piense en una aplicación como en una caja. Dicha caja contiene uno o varios conjuntos de archivos de instalación de un paquete de software (conocidos como *tipo de implementación*) más instrucciones acerca de la implementación del software.  

Cuando la aplicación se implementa en dispositivos, los **requisitos** deciden qué tipo de implementación instala Configuration Manager en el dispositivo.  

Puede hacer muchas más cosas con una aplicación. Obtendrá información sobre ellas a medida que avance por esta guía. En las secciones siguientes se presentan algunos conceptos que debe saber antes de empezar a investigar un poco más:  

### <a name="deployment-type"></a>Tipo de implementación

Si la *aplicación* es la caja, el *tipo de implementación* es el conjunto de contenido que hay en la caja. Una aplicación necesita al menos un tipo de implementación, dado que determina cómo se instala la aplicación. Use más de un tipo de implementación para configurar otro contenido y programa de instalación para la misma aplicación.

Por ejemplo, su empresa tiene una aplicación de línea de negocio denominada Astoria. Los desarrolladores de la aplicación proporcionan las siguientes maneras de instalar la aplicación:

- Paquete de Windows Installer para una funcionalidad completa en dispositivos Windows 10
- Un paquete de App-V para su uso en la granja de servidores de Terminal Server
- Una aplicación web para usuarios de dispositivos móviles  

Cree una única aplicación para Astoria en Configuration Manager. La aplicación define los metadatos generales sobre la aplicación que son comunes en todas las plataformas y métodos de instalación. Después, se crean tres tipos de implementación para los métodos de instalación disponibles y se implementa la aplicación en todos los usuarios. Según los requisitos y otras configuraciones de los tipos de implementación, Configuration Manager determina el método adecuado en cada caso de uso.

Para obtener más información, consulte [Crear tipos de implementación de la aplicación](../deploy-use/create-applications.md#bkmk_create-dt).

### <a name="requirements"></a>Requisitos

En versiones anteriores de Configuration Manager, se creaba una colección de dispositivos para implementar en una aplicación. Aunque todavía puede crear una colección, use los *requisitos* para especificar criterios más detallados para la implementación de una aplicación.

Por ejemplo, especifique que una aplicación solo se puede instalar en dispositivos que ejecutan Windows 10. Al implementar la aplicación en todos los dispositivos, solo se instala en los que ejecuten Windows 10.

Configuration Manager evalúa los requisitos para determinar si instala una aplicación y cualquiera de sus tipos de implementación. A continuación, determina el tipo de implementación correcto mediante el que debe instalarse una aplicación. De forma predeterminada, el cliente de Configuration Manager vuelve a evaluar las reglas de requisitos cada siete días para determinar su cumplimiento conforme a la configuración de cliente **Programar la reevaluación para implementaciones**.

Para obtener más información, vea [Crear e implementar una aplicación](../get-started/create-and-deploy-an-application.md) y [Especificar requisitos para el tipo de implementación](../deploy-use/create-applications.md#bkmk_dt-require).

### <a name="global-conditions"></a>Condiciones globales

Aunque los requisitos se usan con un tipo de implementación específico en una única aplicación, también se pueden crear *condiciones globales*. Estas condiciones son una biblioteca de requisitos predefinidos que se puede usar con cualquier aplicación y tipo de implementación. Configuration Manager incluye un conjunto de condiciones globales integradas, o bien puede crear las suyas propias.

Para obtener más información, vea [Creación de condiciones globales](../deploy-use/create-global-conditions.md).

### <a name="simulated-deployment"></a>Implementación simulada

Una *implementación simulada* evalúa los requisitos, el método de detección y las dependencias de una aplicación. Un cliente informa de los resultados sin instalar realmente la aplicación.

Para obtener más información, consulte el artículo sobre [simular implementaciones de aplicaciones ](../deploy-use/simulate-application-deployments.md).  

### <a name="deployment-action"></a>Acción de implementación

Una *acción de implementación* especifica si se quiere instalar o desinstalar la aplicación que se va a implementar. No todos los tipos de implementación admiten la acción de desinstalación.

Para obtener más información, consulte [Deploy applications](../deploy-use/deploy-applications.md) (Implementar aplicaciones).  

### <a name="deployment-purpose"></a>Propósito de implementación

El *propósito de implementación* especifica si la aplicación de implementación tiene el estado **Requerido** o **Disponible**:  

- El cliente instala automáticamente una implementación *requerida* según la programación que se establezca. Si la aplicación no está oculta, un usuario puede realizar el seguimiento de su estado de implementación. También puede usar el Centro de software para instalar la aplicación antes de la fecha límite.  

- Si la aplicación se implementa en un usuario como *disponible*, la verá en el Centro de software y podrá solicitarla a petición.  

Para obtener más información, consulte [Deploy applications](../deploy-use/deploy-applications.md) (Implementar aplicaciones).  

### <a name="revisions"></a>Revisiones

Si se hacen *revisiones* en una aplicación o un tipo de implementación, Configuration Manager crea una versión nueva de la aplicación. Realice las acciones siguientes en la consola de Configuration Manager:

- Mostrar el historial de cada revisión de aplicación
- Ver sus propiedades
- Restaurar una versión anterior de una aplicación
- Eliminar una versión anterior

Para más información, consulte [Revisar aplicaciones](../deploy-use/revise-and-supersede-applications.md#application-revisions).  

### <a name="detection-method"></a>Método de detección

Los *métodos de detección* se usan para detectar si un dispositivo ya ha instalado una aplicación. Si el método de detección indica que la aplicación está instalada, Configuration Manager no intenta instalarla de nuevo.

Para obtener más información, vea las [opciones de método de detección del tipo de implementación](../deploy-use/create-applications.md#bkmk_dt-detect).

### <a name="dependencies"></a>Dependencias

Las *dependencias* definen uno o más tipos de implementación de otra aplicación que el cliente debe instalar antes de instalar este tipo de implementación.

Para obtener más información, vea [Especificar dependencias para el tipo de implementación](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Sustitución

Configuration Manager permite actualizar o reemplazar las aplicaciones existentes mediante una relación de *sustitución*. Cuando se sustituye una aplicación, se puede especificar un tipo de implementación nuevo para reemplazar el de la aplicación sustituida. También se puede decidir si se quiere actualizar o desinstalar la aplicación sustituida antes de que el cliente instale la de sustitución.

Para obtener más información, consulte [Sustitución de la aplicación](../deploy-use/revise-and-supersede-applications.md#application-supersedence).  

### <a name="user-centric-management"></a>Administración centrada en el usuario

Las aplicaciones de Configuration Manager admiten la *administración centrada en el usuario*, que permite asociar usuarios específicos con dispositivos concretos. En lugar de tener que recordar el nombre del dispositivo de un usuario, las aplicaciones se implementan en el usuario y el dispositivo. Esta funcionalidad ayuda a asegurarse de que las aplicaciones más importantes siempre estén disponibles en todos los dispositivos del usuario. Si un usuario adquiere un equipo nuevo, Configuration Manager instala de forma automática las aplicaciones en el dispositivo antes de que el usuario inicie sesión.

Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  

### <a name="application-group"></a>Grupo de aplicaciones

A partir de la versión 1906, cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación. Los metadatos que especifique sobre el grupo de aplicaciones se ven en el Centro de software como una sola entidad. Puede ordenar las aplicaciones en el grupo para que el cliente las instale en un orden específico.

Para más información, consulte [Crear grupos de aplicaciones](../deploy-use/create-app-groups.md).

## <a name="what-application-types-can-you-deploy"></a>¿Qué tipos de aplicación puede implementar?

Configuration Manager le permite implementar los siguientes tipos de aplicaciones:  

- Windows Installer (msi)  

- Paquete de aplicación de Windows y paquetes de aplicaciones (appx, appxbundle, msix, msixbundle)  

- Paquete de aplicación de Windows en Microsoft Store  

- Instalador de scripts para instaladores de terceros y contenedores de scripts

- Microsoft App-V v4 y v5  

- macOS  

- Una secuencia de tareas de implementación que no es de sistema operativo para aplicaciones complejas

Además, al administrar dispositivos mediante la [administración de dispositivos locales](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) de Configuration Manager, administre estos tipos de aplicación adicionales:  

- Paquete de aplicación de Windows Phone (xap)  

- Paquete de aplicación de Windows Phone en Microsoft Store  

- Windows Installer a través de MDM (msi)  

- Aplicación web

## <a name="state-based-applications"></a>Aplicaciones basadas en estado  

Las aplicaciones de Configuration Manager usan la supervisión basada en estado. Se puede realizar el seguimiento del último estado de implementación de la aplicación para usuarios y dispositivos. Los mensajes de estado muestran información acerca de dispositivos individuales. Por ejemplo, si una aplicación se implementa en una colección de usuarios, puede ver el estado de cumplimiento de la implementación y el propósito de la implementación en la consola de Configuration Manager. Supervise la implementación de todo el software desde el área de trabajo **Supervisión** de la consola de Configuration Manager. Para obtener más información, consulte [Supervisión de aplicaciones](../deploy-use/monitor-applications-from-the-console.md).  

El cliente de Configuration Manager vuelve a evaluar las implementaciones de aplicaciones de manera periódica. Por ejemplo:  

- Un usuario desinstala una aplicación implementada. En el siguiente ciclo de evaluación, Configuration Manager detecta que la aplicación no está presente. Después, el cliente reinstala la aplicación de forma automática.  

- Configuration Manager no instaló una aplicación en un dispositivo porque no cumplía los requisitos. Posteriormente, se realiza un cambio en el dispositivo y cumple los requisitos. Configuration Manager detecta este cambio y el cliente instala la aplicación.  

Puede establecer el intervalo de reevaluación para las implementaciones de aplicaciones. Use la configuración de cliente **Programar la reevaluación para implementaciones** del grupo **Implementación de software**. Para más información, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md#software-deployment).  

## <a name="get-started-creating-an-application"></a>Empezar a crear una aplicación  

Si quiere comenzar de inmediato y crear una aplicación, encontrará un tutorial en el artículo [Crear e implementar una aplicación](../get-started/create-and-deploy-an-application.md).  

Si está familiarizado con los aspectos básicos y quiere obtener más información de referencia sobre todas las opciones disponibles, empiece por [Crear aplicaciones](../deploy-use/create-applications.md).  

## <a name="software-center"></a>Centro de software  

El Centro de software es una aplicación de Windows que se instala con el cliente de Configuration Manager. Se puede usar para las acciones siguientes:  

- Buscar y solicitar las aplicaciones implementadas en el dispositivo o el usuario
- Instalar y programar las instalaciones de software
- Ver el estado de instalación de las aplicaciones, actualizaciones de software y sistemas operativos
- Configurar opciones de control remoto
- Configurar la administración de energía

Vea los siguientes artículos para más información:  

- [Planear y configurar la administración de aplicaciones en Configuration Manager](../plan-design/plan-for-and-configure-application-management.md)
- [Planeamiento del centro de software](../plan-design/plan-for-software-center.md)
- [Manual del usuario del Centro de software](../../core/understand/software-center.md)

> [!Note]  
> La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, consulte [Eliminación del catálogo de aplicaciones](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Paquetes y programas  

Configuration Manager mantiene la compatibilidad de los paquetes y programas usados en versiones anteriores del producto.

Para obtener más información, consulte [Paquetes y programas](../deploy-use/packages-and-programs.md).  

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende los conceptos básicos de administración de aplicaciones en Configuration Manager, continúe con los artículos siguientes:

- [Crear e implementar una aplicación de ejemplo](../get-started/create-and-deploy-an-application.md)
- [Planear y configurar la administración de aplicaciones en Configuration Manager](../plan-design/plan-for-and-configure-application-management.md)
- [Crear aplicaciones](../deploy-use/create-applications.md)
