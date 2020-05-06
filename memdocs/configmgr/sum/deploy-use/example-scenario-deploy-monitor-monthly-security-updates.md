---
title: Escenario de ejemplo para implementar y supervisar actualizaciones
titleSuffix: Configuration Manager
description: Cómo usar las actualizaciones de software en Configuration Manager para implementar y supervisar actualizaciones mensuales de software.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696133"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Escenario de ejemplo para implementar y supervisar las actualizaciones mensuales de software

*Se aplica a: Configuration Manager (rama actual)*

En este tema se proporciona un escenario de ejemplo sobre cómo se pueden usar las actualizaciones de software en Configuration Manager para implementar y supervisar las actualizaciones de software de seguridad que Microsoft emite mensualmente.  

 En este escenario, vamos a seguir las acciones del administrador de Configuration Manager en Woodgrove Bank. El administrador necesita crear una estrategia de implementación de actualizaciones de software con las siguientes condiciones y requisitos:  

- La implementación activa de actualizaciones de software se produce una semana después de que Microsoft publique las actualizaciones de software de seguridad el segundo martes de cada mes. Este evento se conoce habitualmente como Patch Tuesday (la revisión del martes).  

- Las actualizaciones de software se descargan y se configuran en puntos de distribución. A continuación, se prueba una implementación en un subconjunto de clientes antes de que el administrador de ConfigMgr implemente las actualizaciones de software en su entorno de producción.  

- El administrador debe ser capaz de supervisar el cumplimiento de las actualizaciones de software por mes o año.  

  En este escenario se supone que ya se ha implementado la infraestructura de punto de actualización de software. Use la información siguiente para planear y configurar las actualizaciones de software en Configuration Manager.  

|Proceso|Referencia|  
|-------------|---------------|  
|Revise los conceptos clave de las actualizaciones de software.|[Introducción a las actualizaciones de software](../understand/software-updates-introduction.md)|  
|Planee las actualizaciones de software. Esta información contribuye a planear las consideraciones de capacidad y determinar la infraestructura de puntos de actualización de software, la instalación de puntos de actualización de software, la configuración de sincronización y la configuración de cliente para las actualizaciones de software.|[Planear las actualizaciones de software](../plan-design/plan-for-software-updates.md)|  
|Configure las actualizaciones de software. Esta información contribuye a instalar y configurar puntos de actualización de software en la jerarquía y a configurar y sincronizar las actualizaciones de software.<br /><br /> En este escenario, nuestro administrador de ConfigMgr configura la programación de sincronización de actualizaciones de software para que se produzca el segundo miércoles de cada mes, con el fin de asegurarse de que obtienen las actualizaciones de software de seguridad de Microsoft más recientes.|[Sincronizar actualizaciones de software](../get-started/synchronize-software-updates.md)|  

 En las secciones siguientes de este tema se proporcionan ejemplos de pasos para implementar y supervisar las actualizaciones de software de seguridad de Configuration Manager en la organización.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a> Paso 1: Crear un grupo de actualizaciones de software de cumplimiento anual  
 El administrador de Configuration Manager crea un grupo de actualizaciones de software para supervisar el cumplimiento de todas las actualizaciones de software de seguridad publicadas en 2016. El administrador realiza los pasos de la tabla siguiente.  

|Proceso|Referencia|  
|-------------|---------------|  
|En el nodo **Todas las actualizaciones de software** de la consola de Configuration Manager, el administrador de Configuration Manager agrega criterios para mostrar solo las actualizaciones de software de seguridad publicadas o revisadas en el año 2015 que cumplen los criterios siguientes:<br /><br /><ul><li>**Criterios**: fecha de publicación o revisión</li><li>**Condición**: es mayor o igual que la fecha específica<br />**Valor**: 1/1/2015</li><li>**Criterios**: clasificación de actualizaciones<br />**Valor**: Actualizaciones de seguridad</li><li>**Criterios**: Expirado <br />**Valor**: No</li></ul>|Sin información adicional|
|El administrador de ConfigMgr agrega todas las actualizaciones de software filtradas a un nuevo grupo de actualizaciones de software con los siguientes requisitos:<br /><br /><ul><li>**Nombre**: Grupo de cumplimiento: actualizaciones de seguridad de Microsoft 2015</li><li>**Descripción**: Actualizaciones de software|[Agregar actualizaciones de software a un grupo de actualizaciones](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a> Paso 2: Crear una regla de implementación automática para el mes en curso  
 El administrador de Configuration Manager crea una regla de implementación automática para las actualizaciones de software de seguridad que Microsoft publica para el mes en curso. El administrador realiza los pasos de la tabla siguiente.  

|Proceso|Referencia|  
|-------------|---------------|  
|El administrador de ConfigMgr crea una regla de implementación automática con los siguientes requisitos:<br /><br /><ol><li>En la pestaña **General**, el administrador de ConfigMgr configura lo siguiente:<br /> <ul><li>Especifica **Actualizaciones de seguridad mensuales** como nombre.</li><li>Selecciona una recopilación de prueba con un número limitado de clientes.</li><li>Selecciona **Crear un nuevo grupo de actualizaciones de software**.</li><li>Comprueba que la opción **Habilitar la implementación después de ejecutar la regla** no está seleccionada.</li></ul></li><li>En la pestaña **Configuración de implementación**, el administrador de ConfigMgr selecciona la configuración predeterminada.</li><li>En la página **Actualizaciones de software**, el administrador de ConfigMgr configura los filtros de propiedades y criterios de búsqueda siguientes:<br /><ul><li>Fecha de publicación o revisión **Último mes**.</li><li>Clasificación de actualizaciones **Actualizaciones de seguridad**.</li></ul></li><li>En la página **Evaluación**, el administrador de ConfigMgr habilita la programación de la ejecución de la regla para el **segundo jueves** de cada **mes**.  El administrador de ConfigMgr también comprueba que la programación de sincronización está establecida para ejecutarse el **segundo miércoles** de cada **mes**.</li><li>El administrador de ConfigMgr utiliza la configuración predeterminada en las páginas Programación de implementación, Experiencia del usuario, Alertas y Configuración de descarga.</li><li>En la página **Paquete de implementación**, el administrador de ConfigMgr especifica un nuevo paquete de implementación.</li><li>El administrador de ConfigMgr utiliza la configuración predeterminada de las páginas Ubicación de descarga y Selección del idioma.</li></ol>|[Implementar actualizaciones de software automáticamente](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a> Paso 3: Comprobar que las actualizaciones de software están listas para ser implementadas  
 El segundo jueves de cada mes, el administrador de ConfigMgr comprueba que las actualizaciones de software están listas para implementarse. El administrador realiza el paso siguiente.  

|Proceso|Referencia|  
|-------------|---------------|  
|El administrador de ConfigMgr comprueba que la sincronización de las actualizaciones de software ha finalizado correctamente.|[Estado de sincronización de las actualizaciones de software](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a> Paso 4: Implementar el grupo de actualizaciones de software  
 Después de comprobar que las actualizaciones de software están listas para implementarse, el administrador de ConfigMgr las implementa. El administrador realiza los pasos de la tabla siguiente.  

|Proceso|Referencia|  
|-------------|---------------|  
|El administrador de ConfigMgr crea dos implementaciones de prueba para el nuevo grupo de actualizaciones de software. El administrador considera los siguientes entornos para cada implementación:<br /><br /> **Implementación de prueba de estación de trabajo**: el administrador de ConfigMgr tiene en cuenta los siguientes aspectos para la implementación de prueba de estación de trabajo:<br /><br /><ul><li>Especifica una recopilación de implementación que contiene un subconjunto de clientes de estación de trabajo para comprobar la implementación.</li><li>Configura las opciones de implementación que son adecuadas para los clientes de estación de trabajo de su entorno.</li></ul><br />**Implementación de prueba de servidor**: el administrador de ConfigMgr tiene en cuenta los siguientes aspectos para la implementación de prueba de servidor:<br /><br /><ul><li>Especifica una recopilación de implementación que contiene un subconjunto de clientes de servidor para comprobar la implementación.</li><li>Configura las opciones de implementación que son adecuadas para los clientes de servidor de su entorno.</li></ul>|[Implementar actualizaciones de software](deploy-software-updates.md)|  
|El administrador de ConfigMgr comprueba que las implementaciones de prueba se han implementado correctamente.|[Estado de implementación de actualizaciones de software](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|El administrador de ConfigMgr actualiza las dos implementaciones con nuevas recopilaciones que incluyen sus servidores y estaciones de trabajo de producción.|Sin información adicional|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a> Paso 5: Supervisar el cumplimiento de las actualizaciones de software implementadas  
 El administrador de ConfigMgr supervisa el cumplimiento de las implementaciones de actualizaciones de software. El administrador realiza el paso de la tabla siguiente.  

|Proceso|Referencia|  
|-------------|---------------|  
|El administrador de ConfigMgr supervisa el estado de la implementación de actualizaciones de software en la consola de Configuration Manager y comprueba los informes de implementación de actualizaciones de software disponibles en la consola.|[Supervisar actualizaciones de software](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a> Paso 6: Agregar actualizaciones de software mensuales al grupo de actualizaciones anual  
 El administrador de ConfigMgr agrega las actualizaciones de software del grupo de actualizaciones de software mensuales al grupo de actualizaciones de software anuales. El administrador realiza el paso de la tabla siguiente.  

|Proceso|Referencia|  
|-------------|---------------|  
|El administrador de ConfigMgr selecciona las actualizaciones de software del grupo de actualizaciones de software mensuales y agrega las actualizaciones de software al grupo de actualizaciones de software que se crearon para el cumplimiento anual. El administrador realiza un seguimiento del cumplimiento de las actualizaciones de software y crea varios informes para su administración.|[Agregar actualizaciones de software a un grupo de actualizaciones implementado](add-software-updates-to-an-update-group.md)|  

El administrador de ConfigMgr ha finalizado correctamente la implementación mensual de actualizaciones de software de seguridad. El administrador continúa supervisando y realizando informes sobre el cumplimiento de las actualizaciones de software para garantizar que los clientes de su entorno satisfacen los niveles de cumplimiento requeridos.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a> Procesos mensuales periódicos para implementar actualizaciones de software  
 Después del primer mes en el que nuestro administrador de ConfigMgr implementa las actualizaciones de software, dicho administrador realiza los pasos del tres al seis para implementar las actualizaciones de software de seguridad mensuales publicadas por Microsoft.  
