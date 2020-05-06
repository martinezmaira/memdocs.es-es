---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre el Administrador de conversión de paquetes para convertir paquetes en aplicaciones en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689013"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1357861-->

A partir de la versión 1806, el Administrador de conversión de paquetes ayuda a convertir paquetes heredados de Configuration Manager en aplicaciones. Las aplicaciones tienen ventajas adicionales, como las dependencias, las reglas de requisitos, los métodos de detección y la afinidad entre usuario y dispositivo.

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión 1806 como una [característica de versión preliminar](../../core/servers/manage/pre-release-features.md). A partir de la versión 1810, ya no es una característica de versión preliminar.  


Una aplicación de Configuration Manager contiene los archivos y programas que se implementan en dispositivos cliente. Sin embargo, a diferencia de los paquetes y programas heredados, una aplicación proporciona funciones adicionales centradas en el usuario. Por ejemplo, una aplicación podría contener tipos de implementación para una instalación local de un paquete de software, un paquete de aplicación virtual o una versión de la aplicación para dispositivos móviles.

Vea los siguientes artículos para más información: 
- [Introducción a la administración de aplicaciones](../understand/introduction-to-application-management.md)  
- [Paquetes y programas](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Si tiene instalada una versión anterior de Package Conversion Manager, desinstálela antes de actualizar el sitio. Esta versión integrada no requiere la instalación, pero puede entrar en conflicto con las versiones existentes.  

Esta versión integrada del Administrador de conversión de paquetes funciona en los paquetes del sitio de la rama actual de Configuration Manager. No es una herramienta independiente. Si tiene paquetes y programas en una versión anterior de Configuration Manager, primero migre los paquetes al sitio de la rama actual. Para más información, vea [Migración de datos entre jerarquías](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
La versión 1902 de Configuration Manager incluye las mejoras siguientes:
- Análisis de paquetes programado que se ejecuta cada 7 días de forma predeterminada
- Cmdlets de PowerShell para analizar y convertir paquetes
- Mejoras y correcciones de errores generales



## <a name="planning"></a>Planeación

Antes de comenzar la conversión de paquetes en las aplicaciones, primero desarrolle un plan. El proceso siguiente es un plan de ejemplo:

- [Definir un plan detallado de conversión de paquetes](#bkmk_define)  

- [Seleccionar y preparar los paquetes para la conversión](#bkmk_prepare)  

- [Seleccionar los paquetes de prueba](#bkmk_test)  

- [Analizar, investigar y convertir paquetes](#bkmk_analyze)  

- [Probar e implementar las aplicaciones](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a> Definir un plan detallado de conversión de paquetes

En esta sección se describen dos planes de conversión de paquetes de ejemplo:  

- [Un entorno de prueba de muchos recursos](#bkmk_define-high): tiene un entorno de prueba con los recursos, permisos y arquitectura para replicar por completo el entorno de producción.  

- [Un entorno de prueba con recursos limitados](#bkmk_define-limited): no tiene un entorno de prueba que replique por completo el entorno de producción.  

Ajuste estos planes según sea necesario para otros problemas específicos de su entorno.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a> Plan de ejemplo para un entorno de prueba de muchos recursos

El entorno de prueba tiene los recursos, permisos y una arquitectura similar a su entorno de producción. Use el entorno de prueba para analizar y convertir todos los paquetes de forma eficaz y, a continuación, pruebe todas las aplicaciones de Configuration Manager. Después de completar ese trabajo, transfiéralo al entorno de producción. 

El plan de conversión de paquetes podría ser similar a los siguientes pasos:  

1.  Seleccionar los paquetes que desea convertir.  

2.  Migrar los paquetes de conversión en el entorno de prueba.  

3.  Preparar los paquetes para la conversión.  

4.  Seleccionar los paquetes de prueba.  

5.  Analizar, investigar y convertir los paquetes de prueba.  

6.  Probar las aplicaciones convertidas.  

7.  Analizar y convertir el resto de los paquetes (los que no sean de prueba).  

8.  Exportar las aplicaciones desde el entorno de prueba. Importarlas en el entorno de producción.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a> Plan de ejemplo para un entorno de prueba de recursos limitados

El entorno de prueba no tiene los recursos, permisos y una arquitectura similar a su entorno de producción. No puede analizar, probar ni convertir todos los paquetes. En este escenario, solo se analizan, investigan, convierten y prueban los paquetes de prueba. A continuación, migre los paquetes restantes en el entorno de producción para analizarlos y convertirlos. 

El plan de conversión de paquetes podría ser similar a los siguientes pasos:

1.  Seleccionar los paquetes que desea convertir.  

2.  Seleccionar los paquetes de prueba.  

3.  Migrar los paquetes de prueba en el entorno de prueba.  

4.  Preparar los paquetes de prueba para la conversión.  

5.  Analizar, investigar y convertir los paquetes de prueba.  

6.  Probar las aplicaciones convertidas.  

7.  Exportar las aplicaciones de prueba desde el entorno de prueba. Importarlas después en el entorno de producción.  

8.  Migrar los paquetes restantes en el entorno de producción y prepararlos para la conversión.  

9.  Analizar, investigar y convertir los paquetes restantes en el entorno de producción.  

10. Liberar las aplicaciones restantes en el entorno de producción.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a> Seleccionar y preparar los paquetes para la conversión

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a> Seleccionar los paquetes que desea convertir

No todos los paquetes se pueden convertir en aplicaciones. Antes de comenzar a convertir paquetes, identifique los paquetes que no se van a convertir. 

Los mejores tipos de paquetes para conversión en aplicaciones son aquellos que contienen software a nivel de usuario, por ejemplo:  

- Archivos de Windows Installer (.msi y .msu)  

- Programas de Microsoft Application Virtualization (App-V)  

- Archivos ejecutables de Windows (.exe)  

Entre los tipos de paquetes que se conservan mejor como paquetes y no se convierten en aplicaciones se incluyen:

- Herramientas de mantenimiento del sistema. Por ejemplo, scripts o utilidades de copia de seguridad.  

- Paquetes de software que están fuera de soporte técnico.

> [!Tip]  
> Tras identificar los paquetes que no se pueden convertir en aplicaciones, muévalos a una carpeta independiente en la consola de Configuration Manager. Para crear una carpeta de paquete en la consola de Configuration Manager:  
> - Haga clic en el nodo **Paquetes**.  
> - Seleccione **Carpetas** y luego **Crear carpeta**.  
> - Escriba el nombre de la carpeta, por ejemplo, `Not Converted`.  
> - Haga clic en **Aceptar**.  

#### <a name="prepare-the-packages-for-conversion"></a>Preparar los paquetes para la conversión

Para cada paquete que desea convertir, asegúrese de que se ajustan a las condiciones siguientes:  

- La ubicación de los archivos de origen es una ruta de acceso UNC completa, por ejemplo `\\Server\Share\File`.  

- Los archivos de Windows Installer utilizan solo un código de producto único.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a> Seleccionar los paquetes de prueba

Si es posible, el grupo de paquetes de prueba debe incluir paquetes que cumplan los criterios siguientes:  

- Al menos un paquete de prueba con el estado de disponibilidad **Automático**.  

- Al menos un paquete de prueba con el estado de disponibilidad **Manual**.  

Idealmente, los paquetes de prueba deberían ser paquetes principales, por ejemplo:  

- Los paquetes que conoce bien.  

- Los paquetes que son los más importantes para su organización.  

- Los paquetes que se pueden probar más fácilmente.  

Identifique los paquetes que son adecuados para las pruebas. Muévalos después a una carpeta independiente en la consola de Configuration Manager.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a> Analizar, investigar y convertir paquetes

#### <a name="analyze-packages"></a>Analizar paquetes

Para analizar un paquete individual o un grupo pequeño, utilice el Administrador de conversión de paquetes integrado en la consola de Configuration Manager. Para más información, vea [Cómo analizar y convertir paquetes](how-to-analyze-and-convert.md).  

> [!NOTE]  
> Consulte el nodo **Estado de conversión del paquete** del área de trabajo **Supervisión**. Muestra información de resumen sobre los procesos de análisis y conversión.  

#### <a name="investigate-analysis-results"></a>Investigar los resultados del análisis

Tras analizar los paquetes de prueba, investigue los paquetes con un estado de preparación de **Manual** o **Error**. Determine los motivos por los que tienen dicho estado. Algunas de las razones comunes de un estado de preparación **Manual** o **Error** incluyen:

- El paquete no contiene la información necesaria para crear un método de detección en un tipo de implementación de la aplicación.  

- El paquete no contiene la información necesaria para convertir las colecciones en requisitos y condiciones globales.  

- El paquete contiene más de un programa.  

- El paquete depende de otro paquete que no se ha convertido en una aplicación.  

Para más información, vea los siguientes recursos:  

- Revise los mensajes de error y las correcciones en [Referencia técnica de mensajes de error del Administrador de conversión de paquetes](error-messages.md)  

- Revise el archivo de registro **PCMTrace.log**  

- [Solución de problemas del Administrador de conversión de paquetes](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>Convertir los paquetes

Para más información sobre cómo convertir paquetes, vea [Cómo analizar y convertir paquetes](how-to-analyze-and-convert.md).

> [!NOTE]  
> Consulte el nodo **Estado de conversión del paquete** del área de trabajo **Supervisión**. Muestra información de resumen sobre los procesos de análisis y conversión.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a> Probar e implementar las aplicaciones

Pruebe las aplicaciones, ya sea en el entorno de prueba o el entorno de producción, según el plan detallado de conversión del paquete.



## <a name="recommendations"></a>Recomendaciones

- Use el nodo **Estado de conversión del paquete** del área de trabajo **Supervisión**. Muestra información de resumen sobre los procesos de análisis y conversión.  

- Investigue los programas en los paquetes (conocidos como contenedores). Use el complemento del Administrador de conversión de paquetes para convertir sus funciones en la funcionalidad equivalente de Configuration Manager.  

- Asegúrese de probar exhaustivamente cada aplicación convertida antes de implementarla en un entorno de producción.  



## <a name="next-steps"></a>Pasos siguientes

[Cómo analizar y convertir paquetes](how-to-analyze-and-convert.md)
