---
title: Creación de líneas base de configuración
titleSuffix: Configuration Manager
description: Cree líneas base de configuración en Configuration Manager que pueda implementar en una recopilación.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1365aec90093ee24ad967e1d68e7c414b4efa254
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906663"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Creación de líneas base de configuración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


Las líneas base de configuración de Configuration Manager contienen elementos de configuración predefinidos y, de manera opcional, otras líneas base de configuración. Después de crear una línea base de configuración, puede implementarla en una recopilación para que los dispositivos de esa recopilación descarguen la línea base de configuración y evalúen su cumplimiento con ella.  

> [!TIP]
> No hay ninguna manera de especificar el orden en el que el cliente de Configuration Manager evalúa los elementos de configuración en una línea de base. No es determinista.<!-- MEMDocs#175 -->

## <a name="configuration-baselines"></a>Líneas de base de configuración

 Las líneas base de configuración de Configuration Manager pueden contener revisiones específicas de elementos de configuración o pueden estar configuradas para usar siempre la última versión de un elemento de configuración. Para obtener más información sobre las revisiones de elementos de configuración, consulte [Management tasks for configuration data](../../compliance/deploy-use/management-tasks-for-configuration-data.md) (Tareas de administración para datos de configuración).  

 Puede usar dos métodos para crear líneas base de configuración:  

- Importar datos de configuración de un archivo Para iniciar el **Asistente para importar datos de configuración**, en el nodo **Elementos de configuración** o **Líneas de base de configuración** en el área de trabajo **Activos y compatibilidad** , haga clic en **Importar datos de configuración**. Para obtener más información, vea [Import configuration data (Importar datos de configuración)](import-configuration-data.md).

- Use el cuadro de diálogo **Crear línea de base de configuración** para crear una nueva línea base de configuración.  

## <a name="create-a-configuration-baseline"></a>Crear una línea base de configuración

Para crear una línea base de configuración mediante el cuadro de diálogo **Crear línea base de configuración**, use el procedimiento siguiente:  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**.  

2. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear línea de base de configuración**.  

3. En el cuadro de diálogo **Crear línea de base de configuración** , escriba un nombre único y una descripción para la línea de base de configuración. Puede usar un máximo de 255 caracteres para el nombre y 512 caracteres para la descripción.  

4. En la lista **Datos de configuración** se muestran todos los elementos de configuración o líneas base de configuración que se incluyen en esta línea base de configuración. Haga clic en **Agregar** para agregar un nuevo elemento de configuración o línea base de configuración a la lista. Puede elegir entre los elementos siguientes:  

   - **Elementos de configuración**  

   - **Actualizaciones de software**  

   - **Líneas de base de configuración**  
     > [!IMPORTANT]
     > Debe limitar cada línea base de configuración a un máximo de 1000 actualizaciones de software.
5. Use la lista **Cambiar propósito** para especificar el comportamiento de un elemento de configuración que ha seleccionado en la lista **Datos de configuración**. Puede elegir entre los elementos siguientes:  

   -   **Requerido**: la línea base de configuración se evalúa como no conforme si el elemento de configuración no se detecta en un dispositivo cliente. Si se detecta, se evalúa para el cumplimiento.  

   -   **Opcional**: el elemento de configuración solo se evalúa para el cumplimiento si la aplicación a la que hace referencia se encuentra en los equipos cliente. Si no se encuentra la aplicación, la línea base de configuración no se marca como no conforme (solo es aplicable a los elementos de configuración de la aplicación).  

   -   **Prohibido**: la línea base de configuración se evalúa como no conforme si el elemento de configuración se detecta en los equipos cliente (solo es aplicable a los elementos de configuración de aplicación).  

   > [!NOTE]
   >  La lista **Cambio propósito** solo está disponible si se ha hecho clic en la opción **Este elemento de configuración contiene configuraciones de aplicación** en la página **General** del **Asistente para crear elemento de configuración**.  

6. Use la lista **Cambiar revisión** para seleccionar una revisión determinada o la más reciente del elemento de configuración para evaluar el cumplimiento de dispositivos cliente o seleccione **Usar siempre el más reciente** para emplear siempre la revisión más reciente. Para obtener más información sobre las revisiones de elementos de configuración, consulte [Management tasks for configuration data](../../compliance/deploy-use/management-tasks-for-configuration-data.md) (Tareas de administración para datos de configuración).  

7. Para eliminar un elemento de configuración de la línea base de configuración, seleccione un elemento de configuración y luego haga clic en **Quitar**.  

8. A partir de la versión 1806, seleccione si quiere **Aplicar siempre esta línea de base para los clientes administrados conjuntamente**. Cuando se activa, esta línea de base se aplicará incluso en los clientes que se administran mediante Intune.  Esta excepción podría utilizarse para definir la configuración que necesita su organización, pero aún no está disponible en Intune.

9. Opcionalmente, haga clic en **Categorías** para asignar categorías a la línea de base de búsqueda y filtrado. 

10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear línea de base de configuración** y crear la línea base de configuración.  

>[!NOTE]
> La modificación de una línea de base existente, como establecer **Aplicar siempre esta línea de base para los clientes administrados conjuntamente**, aumentará la versión de contenido de línea de base. Los clientes tendrán que evaluar la nueva versión para actualizar los informes de línea de base.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a> Inclusión de líneas base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento
<!--3608345-->
*(Se incorporó en la versión 1910)*

A partir de la versión 1910, puede agregar la evaluación de líneas base de configuración personalizadas como una regla de evaluación de directivas de cumplimiento. Al crear o editar una línea base de configuración, tiene una opción para **Evaluar la línea base como parte de la evaluación de las directivas de cumplimiento**. Al agregar o editar una regla de directivas de cumplimiento, tiene una condición denominada **Incluir las líneas base configuradas en la evaluación de las directivas de cumplimiento**. En el caso de los dispositivos administrados conjuntamente, al configurar Intune para que tome los resultados de la evaluación de cumplimiento de Configuration Manager como parte del estado general de cumplimiento, esta información se envía a Azure AD, lo cual le permite usarla para el acceso condicional a los recursos de Office 365. Para más información, consulte [Acceso condicional con administración conjunta](../../comanage/quickstart-conditional-access.md).

Para incluir líneas base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento, haga lo siguiente:

- Cree e implemente una directiva de cumplimiento en una recopilación de usuarios con una regla para [**incluir las líneas base configuradas en la evaluación de las directivas de cumplimiento**](#bkmk_CA).
- Seleccione [**Evaluar esta línea de base como parte de la evaluación de las directivas de cumplimiento**](#bkmk_eval-baseline) en una línea base de configuración implementada en una recopilación de dispositivos.

> [!IMPORTANT]
> Al tener como destino dispositivos que se administran de manera conjunta, asegúrese de que cumple con los [requisitos previos para la administración conjunta](../../comanage/overview.md#prerequisites).

### <a name="example-evaluation-scenario"></a>Escenario de evaluación de ejemplo

Cuando un usuario forma parte de una recopilación de destino con una directiva de cumplimiento que incluye la condición de regla **Incluir líneas de base configuradas en la evaluación de las directivas de cumplimiento**, cualquier línea de base con la opción **Evaluar esta línea base como parte de la evaluación de las directivas de cumplimiento** seleccionada que se ha implementado en el usuario o en el dispositivo del usuario se evaluará para el cumplimiento. Por ejemplo:

- `User1` forma parte de `User Collection 1`.
- `User1` utiliza `Device1`, que se encuentra en `Device Collection 1` y `Device Collection 2`.
- `Compliance Policy 1` tiene la condición de regla **Incluir líneas de base configuradas en la evaluación de las directivas de cumplimiento** y se implementa en `User Collection 1`.
- `Configuration Baseline 1` tiene **Evaluar esta línea de base como parte de la evaluación de las directivas de cumplimiento** seleccionada y se implementa en `Device Collection 1`.
- `Configuration Baseline 2` tiene **Evaluar esta línea de base como parte de la evaluación de las directivas de cumplimiento** seleccionada y se implementa en `Device Collection 2`.

En este escenario, cuando `Compliance Policy 1` evalúa `User1` con `Device1`, `Configuration Baseline 1` y `Configuration Baseline 2` también se evalúan.

- `User1` a veces usa `Device2`.
- `Device2` es miembro de `Device Collection 2` y `Device Collection 3`.
- `Device Collection 3` tiene `Configuration Baseline 3` implementado, pero **Evaluar esta línea de base como parte de la evaluación de las directivas de cumplimiento** no está seleccionada.

Cuando `User1` utiliza `Device2`, solo se evalúa `Configuration Baseline 2` cuando `Compliance Policy 1` evalúa.

> [!NOTE]
><!--5582516-->
> Si la directiva de cumplimiento evalúa una nueva línea de base que nunca se ha evaluado antes en el cliente, puede informar del no cumplimiento. Esto sucede si la evaluación de la línea de base sigue en ejecución cuando se evalúa el cumplimiento. Para solucionar esta incidencia, en el **Centro de software** haga clic en **Comprobar cumplimiento**.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a> Creación e implementación de una directiva de cumplimiento con una regla para la evaluación de directivas de cumplimiento de línea base

1. En el área de trabajo **Activos y cumplimiento**, expanda **Configuración de cumplimiento** y luego seleccione el nodo **Directivas de cumplimiento**.
1. Haga clic en **Crear directiva de cumplimiento** en la cinta para abrir el **Asistente para crear directivas de cumplimiento**. 
1. En la página **General**, seleccione **Reglas de cumplimiento para dispositivos administrados con el cliente de Configuration Manager**.
   - Los dispositivos deben administrarse con el cliente de Configuration Manager para incluir líneas de base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento.
1. Seleccione las plataformas en las páginas **Plataformas compatibles**.
1. En la página **Reglas**, seleccione **Nueva** y luego la condición **Incluir líneas de base configuradas en la evaluación de las directivas de cumplimiento**.

   ![Condición Incluir las líneas base configuradas en la evaluación de las directivas de cumplimiento](./media/3608345-create-compliance-policy-rule.png)

1. Haga clic en **Aceptar** y luego en **Siguiente** para llegar a la página **Resumen**.
1. Compruebe las opciones seleccionadas y haga clic en **Siguiente** y luego en **Cerrar**.
1. En el nodo **Directivas de cumplimiento**, haga clic con el botón derecho en la directiva que se ha creado y seleccione **Implementar**.
1. Elija la recopilación, la configuración de generación de alertas y la programación de evaluación de cumplimiento de la directiva.
1. Haga clic en **Aceptar** para implementar la directiva de cumplimiento.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Selección de una línea base de configuración y activación de "Evaluar la línea base como parte de la evaluación de las directivas de cumplimiento"

1. En el área de trabajo **Activos y cumplimiento**, expanda **Configuración de cumplimiento** y luego seleccione el nodo **Líneas base de configuración**.
1. Haga clic con el botón derecho en una línea de base existente implementada en una recopilación de dispositivos y, después, seleccione **Propiedades**. Si es necesario, puede crear una línea base nueva.
   - La línea de base debe implementarse en una recopilación de dispositivos, no en una recopilación de usuarios.
1. Habilite la opción **Evaluar esta línea de base como parte de la evaluación de las directivas de cumplimiento**.
   - En el caso de los dispositivos administrados de manera conjunta que tienen Intune como la autoridad de **Configuración de dispositivo**, asegúrese de que también esté seleccionada la opción **Aplicar siempre esta línea de base, incluso para clientes administrados conjuntamente**.
1. Haga clic en **Aceptar** para guardar los cambios en la línea de base de configuración.

   ![Cuadro de diálogo de Propiedades de línea base de configuración](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Registro de archivos de líneas base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento

- ComplianceHandler.log
- SettingsAgent.log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Pasos siguientes

[Importar datos de configuración](import-configuration-data.md)
