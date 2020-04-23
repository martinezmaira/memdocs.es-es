---
title: Creación de planes de implementación
titleSuffix: Configuration Manager
description: Guía paso a paso para crear planes de implementación en Análisis de escritorio.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c42576f35d285fc7285466c4208d7ccaf370daa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708303"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Creación de planes de implementación en Análisis de escritorio

En este artículo se proporcionan los pasos para crear un plan de implementación en Análisis de escritorio. Antes de empezar, [obtenga información sobre los planes de implementación](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Creación de un plan para Windows 10

Siga los pasos de esta sección para usar Análisis de escritorio con el fin de crear un plan para implementar Windows 10.

1. Abra el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics). Use credenciales que tengan al menos permisos de **colaboradores del área de trabajo**.  

2. Seleccione **Planes de implementación** en el grupo Administrar.  

3. En el panel **Planes de implementación**, seleccione **Crear**.  

4. En el panel **Crear plan de implementación**, configure las siguientes opciones:  

    - **Nombre**: un nombre exclusivo para el plan de implementación.  

    - **Productos y versiones**: elija la versión de Windows 10 que se va a implementar. Microsoft recomienda crear planes de implementación que usen la versión más reciente.  

    - **Grupos de dispositivos**: seleccione uno o más grupos de la misma jerarquía. Estos grupos son [colecciones de dispositivos](connect-configmgr.md#bkmk_Collections) sincronizados desde Configuration Manager.

        Si conecta varias jerarquías de Configuration Manager a la misma instancia de Análisis de escritorio, un nombre para mostrar de la jerarquía prefijará el nombre de la colección en la configuración piloto global. Este nombre es la propiedad **nombre para mostrar** de la conexión de Análisis de escritorio en la consola de Configuration Manager.<!-- 4814075 -->

        > [!NOTE]
        > La compatibilidad con varias jerarquías requiere la versión 1910 o posterior de Configuration Manager.
        >
        > Si selecciona recopilaciones para varias jerarquías, el portal muestra una advertencia. No se puede crear el plan de implementación con recopilaciones de varias jerarquías.<!-- 4814075 -->

    - **Reglas de preparación**: estas reglas ayudan a determinar qué dispositivos son aptos para la actualización. Para más información, consulte [Reglas de preparación](#readiness-rules).  

    - **Fecha de finalización**: elija la fecha en que Windows debe implementarse completamente en todos los dispositivos de destino.  

5. Seleccione **Crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Para acelerar este proceso, solicite una actualización de datos a petición. Para más información, consulte [Preguntas frecuentes sobre Análisis de escritorio](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Abra el plan de implementación seleccionando su nombre.  

7. En el menú del plan de implementación, en el grupo **Preparar**, seleccione **Identificar importancia**.  

    1. En la pestaña **Aplicaciones**, seleccione que se muestren solo los recursos **no revisados**.  

    2. Seleccione cada aplicación y, a continuación, seleccione **Editar**. Puede seleccionar más de una aplicación para editarla al mismo tiempo.  

    3. Elija un nivel de importancia en la lista **Importancia**. Si quiere que Análisis de escritorio valide la aplicación durante la prueba piloto, seleccione **Crítico** o **Importante**. No valida las aplicaciones marcadas como **No importante**. Evalúe su [compatibilidad](compat-assessment.md) y otra información del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Haga clic en **Guardar** cuando haya terminado.  

8. En el menú del plan de implementación, en el grupo **Preparar**, seleccione **Identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **Agregar a piloto**. Si no está de acuerdo con la recomendación, seleccione **Reemplazar**.  

        Para obtener más información sobre cómo realiza estas recomendaciones Análisis de escritorio, seleccione el icono de información en la esquina superior derecha del panel **Identificar piloto**.

## <a name="readiness-rules"></a>Reglas de preparación

Estas reglas ayudan a determinar qué dispositivos son aptos para la actualización local. Puede establecer estas reglas al crear el plan de implementación o editarlas más adelante.

Para cambiar las reglas de preparación:

1. En el portal de Análisis de escritorio, seleccione el plan de implementación.
1. Junto al nombre, seleccione **Editar**.
1. Seleccione **Reglas de preparación**.
1. Seleccione **SO Windows**.
1. Realice los cambios necesarios y seleccione **Guardar**.

Para las actualizaciones del **SO Windows**, hay dos reglas disponibles: controladores de dispositivo y aplicaciones Windows.

### <a name="device-drivers"></a>Controladores de dispositivo

Configure si los dispositivos reciben controladores de Windows Update. De forma predeterminada, este valor está **desactivado**. Habilite esta regla cuando use Windows Update para empresas para administrar las actualizaciones, incluidos los controladores. Si usa Configuration Manager para administrar las actualizaciones de software, establezca esta regla en **Desactivado**.

### <a name="windows-applications"></a>Aplicaciones Windows

Las aplicaciones que Análisis de escritorio muestra como *destacadas* se basan en el umbral de recuento de instalaciones. Establezca este umbral en las reglas de preparación para el plan de implementación. De forma predeterminada, este umbral es de **2,0 %** . En caso necesario, puede cambiar el valor de `0.0` a `10.0`.


## <a name="next-steps"></a>Pasos siguientes

Continúe con el siguiente artículo para implementar en dispositivos piloto.
> [!div class="nextstepaction"]  
> [Cómo realizar una implementación piloto](deploy-pilot.md)  
