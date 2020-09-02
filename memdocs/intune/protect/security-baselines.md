---
title: 'Uso de líneas de base de seguridad en Microsoft Intune: Azure | Microsoft Docs'
description: Use la configuración de seguridad de Windows recomendada para proteger a los usuarios y a los datos de los dispositivos con Microsoft Intune en la administración de dispositivos móviles. Habilite el cifrado, configure Advanced Threat Protection de Microsoft Defender, controle Internet Explorer, establezca directivas de seguridad locales, exija una contraseña, bloquee las descargas de Internet, y mucho más.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom:
- intune-azure
- contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a3954057d14aaf24a1a0147d9717cfc01413d51
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914929"
---
# <a name="use-security-baselines-to-configure-windows-10-devices-in-intune"></a>Uso de líneas de base de seguridad para configurar dispositivos Windows 10 en Intune

Use líneas de base de seguridad de Intune que le ayuden a proteger a sus usuarios y dispositivos. Las líneas de base de seguridad son grupos preconfigurados de configuraciones de Windows que le ayudan a aplicar un grupo conocido de configuraciones y valores predeterminados que recomiendan los equipos de seguridad pertinentes. Al crear un perfil de líneas de base de seguridad en Intune, está creando una plantilla que consta de varios perfiles de *configuración de dispositivos*.

Esta característica se aplica a:

- Windows 10, versión 1809 y posteriores

Usted se encarga de implementar líneas de base de seguridad en grupos de usuarios o dispositivos en Intune y la configuración se aplica a dispositivos que ejecutan Windows 10 o posterior. Por ejemplo, la *línea de base de seguridad MDM* habilita automáticamente BitLocker para unidades extraíbles, requiere automáticamente una contraseña para desbloquear un dispositivo, deshabilita automáticamente la autenticación básica, etc. Si un valor predeterminado no funciona para su entorno, personalice la línea de base para aplicar la configuración que necesita.

Los tipos de línea de base independientes pueden incluir la misma configuración, pero usar valores predeterminados distintos de esa configuración. Es importante conocer los valores predeterminados de las líneas de base que elige usar y, a continuación, modificar cada línea de base para ajustarlas a sus necesidades organizativas.

> [!NOTE]
> Microsoft no recomienda usar versiones preliminares de líneas de base de seguridad en un entorno de producción. La configuración de una línea de base en versión preliminar podría cambiar en el transcurso de la versión preliminar.

Las líneas de base de seguridad es poder ayudarlo a tener un flujo de trabajo seguro de un extremo a otro cuando trabaja con Microsoft 365. Estas son algunas de las ventajas:

- Una línea de base de seguridad incluye los procedimientos recomendados y las recomendaciones sobre la configuración que afectan a la seguridad. Intune se asocia con el mismo equipo de seguridad de Windows que crea las líneas de base de seguridad de directiva de grupo. Estas recomendaciones se basan en la orientación y en una amplia experiencia.
- Si es nuevo en Intune y no está seguro de por dónde empezar, las líneas de base de seguridad ofrecen una ventaja. Puede crear e implementar rápidamente un perfil seguro, sabiendo que ayuda a proteger los recursos y datos de su organización.
- Si actualmente usa una directiva de grupo, migrar a Intune para la administración es mucho más fácil con estas líneas de base. Estas líneas de base están integradas de forma nativa en Intune e incluyen una experiencia de administración moderna.

Las [líneas de base de seguridad de Windows](/windows/security/threat-protection/windows-security-baselines) son un excelente recurso para obtener más información sobre esta característica. La [administración de dispositivos móviles](/windows/client-management/mdm/) (MDM) es un magnífico recurso sobre MDM y lo que puede hacer en los dispositivos Windows.

## <a name="available-security-baselines"></a>Líneas de base de seguridad disponibles

Las instancias de línea de base de seguridad siguientes están disponibles para usarlas con Intune. Use los vínculos para ver la configuración de la instancia más reciente de cada línea de base.

- **Línea de base de seguridad MDM**
  - [Línea de base de seguridad de MDM para mayo de 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Versión preliminar: línea de base de seguridad de MDM para octubre de 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)

- **Línea de base de Microsoft Defender ATP**
   *(Para usar esta línea de base, su entorno debe cumplir con los requisitos previos para usar [Protección contra amenazas avanzada de Microsoft Defender](advanced-threat-protection.md#prerequisites))* .
  - [Línea de base de ATP de Microsoft Defender para abril de 2020: versión 4](security-baseline-settings-defender-atp.md?pivots=atp-april-2020)
  - [Línea de base de ATP de Microsoft Defender para marzo de 2020: versión 3](security-baseline-settings-defender-atp.md?pivots=atp-march-2020)

  > [!NOTE]
  > La base de referencia de seguridad de ATP de Microsoft Defender se ha optimizado para dispositivos físicos y actualmente no se recomienda su uso en máquinas virtuales (VM) ni puntos de conexión de VDI. Ciertas configuraciones de base de referencia pueden afectar a las sesiones interactivas remotas en entornos virtualizados.  Para obtener más información, vea [Aumento del cumplimiento de la base de referencia de seguridad de ATP de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) en la documentación de Windows.

- **Línea de base de Microsoft Edge**
  - [Línea de base de Microsoft Edge para abril de 2020 (Edge versión 80 y posteriores)](security-baseline-settings-edge.md?pivots-edge-april-2020)
  - [Versión preliminar: Línea de base de Microsoft Edge de octubre de 2019 (Edge versión 77 y posteriores)](security-baseline-settings-edge.md?pivots=edge-october-2019)

Puede continuar usando y editando los perfiles que creó anteriormente en función de una plantilla en versión preliminar, incluso si dicha plantilla deja de estar disponible para la creación de nuevos perfiles.

Cuando esté listo para pasar a una versión más reciente de una línea base que use, vea [Cambio de la versión de línea de base de un perfil](#change-the-baseline-version-for-a-profile) en este artículo. 

## <a name="about-baseline-versions-and-instances"></a>A cerca de las instancias y versiones de línea de base

Cada nueva instancia de versión de una línea de base puede agregar o quitar la configuración, o aplicar otros cambios. Por ejemplo, a medida que la nueva configuración de Windows 10 está disponible con nuevas versiones de Windows 10, la línea de base de seguridad MDM podría recibir una nueva instancia de versión con la configuración más reciente.

En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), en **Seguridad de los puntos de conexión** > **Líneas de base de seguridad** verá una lista de las líneas de base disponibles. La lista incluye lo siguiente:
- Nombre de la plantilla de línea base.
- Cuántos perfiles tiene que usen ese tipo de línea base.
- Cuántas instancias independientes (versiones) del tipo base hay disponibles.
- Fecha de *Última publicación* que identifica cuándo estuvo disponible la versión más reciente de la plantilla de línea base.

Si quiere ver más información sobre las versiones de línea base que usa, seleccione un tipo de línea base, como *Línea de base de seguridad de MDM*, para abrir su panel *Perfiles* y, luego, elija **Versiones**. Intune muestra detalles sobre las versiones de esa línea de base que se encuentran en uso por parte de sus perfiles. Los detalles incluyen la versión de línea base más reciente y actual. Puede seleccionar una sola versión para ver más detalles sobre los perfiles en los que se usa.

Puede optar por [cambiar la versión](#change-the-baseline-version-for-a-profile) de una línea de base que está en uso con un perfil determinado. Al cambiar de versión, no es necesario crear un nuevo perfil de línea base para aprovechar las versiones actualizadas, sino que se puede seleccionar un perfil de línea base y usar la opción integrada para cambiar la versión de la instancia de ese perfil por una nueva.

### <a name="compare-baseline-versions"></a>Comparación de versiones de línea de base

En el panel **Versiones** de una línea de base de seguridad se muestra una lista de todas las versiones de esta línea de base que ha implementado. En la lista también se incluye la versión más reciente y activa de la línea de base. Cuando se crea un *perfil* de línea de base de seguridad, el perfil usa la versión más reciente de esta.  Puede seguir usando y editando perfiles creados anteriormente en los que se usa una versión de la línea de base anterior, incluidas las líneas de base creadas mediante una versión preliminar.

Para entender lo que ha cambiado entre versiones, active las casillas de dos versiones diferentes y seleccione **Comparar líneas base**. Luego se le pide que descargue un archivo CSV que detalla esas diferencias.

La descarga identifica cada configuración de las dos versiones de línea de base e indica si esta configuración ha cambiado (*notEqual*) o no (*equal*). Los detalles también incluyen el valor predeterminado de la configuración por versión y si la configuración se *ha agregado* a la versión más reciente o se *ha quitado* de esta.

![Comparar líneas de base](./media/security-baselines/compare-baselines.png)

## <a name="avoid-conflicts"></a>Evitación de conflictos

Puede usar una o varias de las líneas de base disponibles en su entorno de Intune al mismo tiempo. También puede usar varias instancias de las mismas líneas de base de seguridad con diversas personalizaciones.

Al usar varias líneas de base de seguridad, revise la configuración en cada una para identificar los casos en los que diferentes configuraciones de líneas de base presentan valores en conflicto del mismo ajuste. Dado que puede implementar líneas de base de seguridad diseñadas para diversas intenciones e implementar varias instancias de la misma línea de base que incluye la configuración personalizada, es posible que cree conflictos de configuración para dispositivos que deben investigarse y resolverse.

Además, las líneas de base de seguridad suelen administrar la misma configuración que se puede establecer con [perfiles de configuración de dispositivos](../configuration/device-profiles.md) u otros tipos de directivas. Por lo tanto, tenga en cuenta las directivas y los perfiles adicionales de la configuración cuando trate de evitar o resolver conflictos.

Utilice la información de los vínculos siguientes para ayudar a identificar y resolver conflictos:

- [Solución de problemas de directivas y perfiles en Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Supervisión de las líneas de base de seguridad](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="manage-baselines"></a>Administración de las líneas de base

Las tareas comunes cuando se trabaja con líneas de base de seguridad incluyen:

- [Crear un perfil](#create-the-profile): para definir la configuración que desea utilizar y asignar la línea de base a los grupos.
- [Cambiar la versión](#change-the-baseline-version-for-a-profile): cambiar la versión de línea de base en uso por un perfil.
- [Quitar una asignación de línea de base](#remove-a-security-baseline-assignment): obtenga información sobre lo que ocurre cuando deja de administrar la configuración con una línea de base de seguridad.


### <a name="prerequisites"></a>Requisitos previos

- Para administrar líneas base en Intune, la cuenta debe tener el rol [Administrador de directiva y de perfil](../fundamentals/role-based-access-control.md#built-in-roles) integrado.

- El uso de algunas líneas de base podría exigirle tener una suscripción activa a servicios adicionales, como ATP de Microsoft Defender.

### <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión** > **Líneas base de seguridad** para ver la lista de líneas base disponibles.

   ![Selección de una línea de base de seguridad para configurar](./media/security-baselines/available-baselines.png)

3. Seleccione la línea de base que le gustaría usar y, luego, **Crear perfil**.

4. En la pestaña **Aspectos básicos**, especifique estas propiedades:

   - **Nombre**: escriba un nombre para el perfil de las líneas de base de seguridad. Por ejemplo, escriba *Perfil estándar para ATP de Defender*.

   - **Descripción**: escriba algún texto que describa lo que hace esta línea de base. La descripción es para que introduzca cualquier texto que desee. Es opcional, pero recomendable.

   Seleccione **Siguiente** para ir a la siguiente pestaña. Una vez que haya avanzado a una nueva pestaña, podrá seleccionar su nombre para volver a una consultada anteriormente.

5. En la pestaña Opciones de configuración, consulte los grupos de **Configuración** que están disponibles en la línea de base que seleccionó. Puede expandir un grupo para ver su configuración, además de los valores predeterminados de dicha configuración de la línea de base. Para encontrar la configuración específica:
   - Seleccione un grupo para expandir y revisar la configuración disponible.
   - Use la barra de *búsqueda* y especifique las palabras clave que filtran la vista para mostrar solo esos grupos que incluyen sus criterios de búsqueda.

   Cada uno de los valores de una línea de base cuenta con una configuración predeterminada para esa versión de línea de base. Vuelva a configurar los valores predeterminados para cumplir con las necesidades de su empresa. Diferentes líneas de base podrían incluir la misma configuración y usar valores predeterminados distintos de la configuración, según la intención de la línea de base.

   ![Expansión de un grupo para ver los valores de ese grupo](./media/security-baselines/sample-list-of-settings.png)

6. En la pestaña **Etiquetas de ámbito**, seleccione **Seleccionar etiquetas de ámbito** para abrir el panel *Seleccionar etiquetas* para asignar etiquetas de ámbito al perfil.

7. En la pestaña **Asignaciones**, seleccione **Seleccionar grupos para incluir** y, a continuación, asigne la línea de base a uno o varios grupos. Use **Seleccionar grupos para excluir** para ajustar la asignación.

   ![Asignar un perfil](./media/security-baselines/assignments.png)

8. Cuando esté listo para implementar la línea de base, avance a la pestaña **Revisar y crear** para revisar los detalles de la línea de base. Seleccione **Crear** para guardar e implementar el perfil.

   Tan pronto como cree el perfil, se insertará en el grupo asignado y es posible que se aplique inmediatamente.

   > [!TIP]
   > Si guarda un perfil sin asignarlo primero a grupos, más tarde podrá editarlo para hacerlo.

   ![Revisión de la línea de base](./media/security-baselines/review.png)

9. Después de crear un perfil, edítelo en **Seguridad de los puntos de conexión** > **Líneas de base de seguridad**, seleccione el tipo de línea de base que ha configurado y, luego, **Perfiles**. Seleccione el perfil en la lista de perfiles disponibles y, a continuación, seleccione **Propiedades**. Puede editar la configuración desde todas las pestañas de configuración disponibles y seleccionar **Revisar y guardar** para confirmar sus cambios.

### <a name="change-the-baseline-version-for-a-profile"></a>Cambio de la versión de línea de base de un perfil

Puede cambiar la versión de la instancia de línea de base que se usa con un perfil.  Al cambiar la versión, se selecciona una instancia disponible de la misma línea de base. No puede cambiar entre dos tipos de línea de base distintos, como cambiar un perfil que usa una línea de base para ATP de Defender a usar la línea de base de seguridad MDM.

Durante la configuración de un cambio de la versión de línea de base, puede descargar un archivo CSV que muestra los cambios entre las dos versiones de línea de base implicadas. También tiene la opción de conservar todas las personalizaciones de la versión de línea de base original, o bien implementar la nueva versión con todos sus valores predeterminados. No tiene la opción de realizar cambios en la configuración individual cuando se cambia la versión de una línea de base para un perfil.

Al guardar, después de completarse la conversión, la línea de base se volverá a implementar inmediatamente en grupos asignados.

**Durante la conversión**:

- Se agrega y establece una nueva configuración que no estaba en la versión original que estaba usando para utilizar los valores predeterminados.

- La configuración que no esté en la nueva versión de línea de base seleccionada se quitará y este perfil de la línea de base de seguridad ya no la aplicará.

  Si un perfil de línea de base deja de administrar una configuración, dicha configuración no se restablecerá en el dispositivo. En su lugar, la configuración del dispositivo seguirá estando establecida en su última configuración hasta que otro proceso la administra para cambiarla. Entre los ejemplos de procesos que pueden cambiar una configuración una vez que deja de administrarla se incluyen un perfil de línea de base diferente, una configuración de directiva de grupo o una configuración manual realizada en el dispositivo.

#### <a name="to-change-the-baseline-version-for-a-profile"></a>Para cambiar la versión de línea de base de un perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431). 

2. Seleccione **Seguridad de los puntos de conexión** > **Líneas base de seguridad** y, luego, seleccione el icono del tipo de línea base que tenga el perfil que quiere cambiar.

3. A continuación, seleccione **Perfiles**, active la casilla del perfil que desea editar y seleccione **Cambiar versión**.

   ![seleccionar una línea de base](./media/security-baselines/select-baseline.png)

4. En el panel **Cambiar versión**, use la lista desplegable **Select a security baseline to update to** (Seleccionar una línea de base de seguridad a la que actualizar) y seleccione la instancia de versión que desea usar.

   ![seleccionar una versión](./media/security-baselines/select-instance.png)

5. Seleccione **Revisar actualización** para descargar un archivo CSV que muestre la diferencia entre la versión de la instancia actual del perfil y la nueva versión seleccionada. Revise este archivo para comprender qué configuración es nueva o se quita, y cuáles son los valores predeterminados de esta configuración en el perfil actualizado.

   Cuanto esté listo, continúe con el siguiente paso.

6. Elija una de las dos opciones para **Seleccionar un método para actualizar el perfil**:
   - **Aceptar los cambios en la línea de base, pero conservar mis personalizaciones de configuración existentes**: esta opción conserva las personalizaciones que realizó en el perfil de la línea de base y las aplica a la nueva versión que ha seleccionado para su uso.
   - **Aceptar los cambios en la línea de base y descartar las personalizaciones de configuración existentes**: esta opción sobrescribe su perfil original por completo. El perfil actualizado usará los valores predeterminados de todas las configuraciones.

7. Seleccione **Enviar**. El perfil se actualiza a la versión de línea de base seleccionada y, una vez que se ha completado la conversión, la línea de base vuelve a implementarse inmediatamente en grupos asignados.

### <a name="remove-a-security-baseline-assignment"></a>Quitar una asignación de la línea de base de seguridad

Si una configuración de líneas de base de seguridad deja de aplicarse a un dispositivo o la configuración de una línea de base se establece en *No configurado*, esa configuración de un dispositivo no se revertirá a una configuración administrada previamente. En su lugar, la configuración administrada previamente del dispositivo conservará sus últimas configuraciones tal como se reciben de la línea de base hasta que otro proceso actualice esa configuración del dispositivo.

Otros procesos que podrían cambiar la configuración del dispositivo posteriormente incluyen una línea de base de seguridad nueva o diferente, un perfil de configuración de dispositivo, configuraciones de directiva de grupo o una edición manual de la configuración del dispositivo.

### <a name="duplicate-a-security-baseline"></a>Duplicado de una línea base de seguridad

Puede crear duplicados de las líneas base de seguridad. Un escenario en el que el duplicado de una línea base resulta útil es cuando se quiere asignar una línea base similar pero distinta a un subconjunto de dispositivos. Al crear un duplicado, no es necesario volver a crear manualmente toda la línea base, sino que se puede duplicar cualquiera de las líneas base actuales y luego incorporar solo los cambios que necesita la nueva instancia. Solo se puede cambiar un valor específico y el grupo al que está asignada la línea base.

Al crear un duplicado, se le asigna un nuevo nombre a la copia. La copia se realiza con las mismas opciones de configuración y etiquetas de ámbito que la original, pero no tiene ninguna asignación. Debe modificar la nueva línea base para agregar asignaciones.

Todas las líneas base de seguridad admiten la creación de un duplicado.

Después de duplicar una línea base, revise y edite la nueva instancia para realizar cambios en su configuración.

#### <a name="to-duplicate-a-baseline"></a>Para duplicar una línea base

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vaya a **Seguridad de los puntos de conexión** > **Líneas base de seguridad**, seleccione el tipo de línea base que quiere duplicar y luego **Perfiles**.
3. Haga clic con el botón derecho en el perfil que quiere duplicar y seleccione **Duplicar**, o bien seleccione los puntos suspensivos ( **...** ) situados a la derecha de la línea base y luego **Duplicar**.
4. Proporcione un **Nuevo nombre** a la línea base y seleccione **Guardar**.

Después de *Actualizar*, el nuevo perfil de línea base aparece en el centro de administración.

#### <a name="to-edit-a-baseline"></a>Para editar una línea base

1. Seleccione la línea base y luego **Propiedades**.
2. Seleccione **Configuración** para expandir la lista de categorías de opciones de la línea base. No se pueden modificar las opciones desde esta vista, pero se puede revisar cómo están configuradas.
3. Para modificar la configuración, seleccione **Editar** en cada categoría en la que quiera hacer un cambio:
   - Aspectos básicos
   - Assignments
   - Etiquetas de ámbito
   - Opciones de configuración
4. Una vez realizados los cambios, seleccione **Guardar** para guardar las modificaciones.  Debe guardar las modificaciones realizadas en una categoría para poder especificar modificaciones en categorías adicionales.

### <a name="older-baseline-versions"></a>Versiones de línea de base anteriores

Microsoft Endpoint Manager actualiza las versiones de las líneas de base de seguridad integradas en función de las necesidades cambiantes de una organización habitual. En cada versión nueva se genera una actualización de la versión de una línea de base determinada. Se espera que los clientes usen la versión de línea de base más reciente como punto de partida para sus perfiles de configuración de dispositivos.

Cuando ya no hay ningún perfil que use una línea base anterior enumerada en el inquilino, Microsoft Endpoint Manager solo muestra la versión de línea base más reciente disponible.

Si tiene un perfil asociado a una línea de base anterior, seguirá apareciendo.

## <a name="co-managed-devices"></a>Dispositivos administrados conjuntamente

Las líneas de base de seguridad en dispositivos administrados por Intune son similares a los dispositivos administrados conjuntamente con Configuration Manager. Los dispositivos administrados conjuntamente usan Configuration Manager y Microsoft Intune para administrar los dispositivos Windows 10 al mismo tiempo. Le permite conectar a la nube su inversión existente de Configuration Manager a las ventajas de Intune. La [introducción a la administración conjunta](/configmgr/comanage/overview) es un excelente recurso si usa Configuration Manager y también quiere las ventajas de la nube.

Cuando se usen dispositivos administrados conjuntamente, debe cambiar la carga de trabajo de la **configuración del dispositivo** (su configuración) a Intune. [Las cargas de trabajo de configuración de dispositivo](/configmgr/comanage/workloads#device-configuration) proporcionan más información.

## <a name="q--a"></a>Q & A

### <a name="why-these-settings"></a>¿Por qué esta configuración?

El grupo de seguridad de Microsoft acumula muchos años de experiencia trabajando directamente con los desarrolladores de Windows y la comunidad de seguridad para crear estas recomendaciones. Las configuraciones de esta línea de base se consideran las opciones de configuración relacionadas con la seguridad más pertinentes. En cada nueva compilación de Windows, el equipo ajusta sus recomendaciones basándose en las características lanzadas recientemente.

### <a name="is-there-a-difference-in-the-recommendations-for-windows-security-baselines-for-group-policy-vs-intune"></a>¿Hay alguna diferencia en las recomendaciones para las líneas de base de seguridad de Windows para la directiva de grupo frente a Intune?

El mismo equipo de seguridad de Microsoft eligió y organizó la configuración para cada línea de base. Intune incluye todas las configuración pertinentes en la línea de base de seguridad de Intune. Hay algunas configuraciones en la línea de base de la directiva de grupo que son específicas de un controlador de dominio local. Estas opciones se excluyen de las recomendaciones de Intune. Todas las demás configuraciones son las mismas.

### <a name="are-the-intune-security-baselines-cis-or-nsit-compliant"></a>¿Son compatibles las líneas de base de seguridad CIS o NSIT de Intune?

Estrictamente hablando, no. El equipo de seguridad de Microsoft consulta a las organizaciones, como CIS, para recopilar sus recomendaciones. Sin embargo, no hay una asignación unívoca entre las líneas de base de Microsoft y "compatibles con CIS".

### <a name="what-certifications-does-microsofts-security-baselines-have"></a>¿Qué certificaciones tienen las líneas de base de seguridad de Microsoft? 

- Microsoft continúa publicando líneas de base de seguridad para directivas de grupo (GPO) y el [Security Compliance Toolkit](/windows/security/threat-protection/security-compliance-toolkit-10), como ha hecho durante muchos años. Muchas organizaciones usan estas líneas de base. Las recomendaciones que figuran en estas líneas de base provienen del compromiso del equipo de seguridad de Microsoft con clientes empresariales y agencias externas, incluido el Departamento de Defensa (DoD), el Instituto Nacional de Estándares y Tecnología (NIST), etc. Compartimos nuestras recomendaciones y líneas de base con estas organizaciones. Estas organizaciones también tienen sus propias recomendaciones que reflejan fielmente las recomendaciones de Microsoft. Dado que la administración de dispositivos móviles (MDM) continúa creciendo en la nube, Microsoft ha creado recomendaciones de MDM equivalentes de estas líneas de base de directivas de grupo. Estas líneas de base adicionales están integradas en Microsoft Intune e incluyen informes de cumplimiento sobre usuarios, grupos y dispositivos que siguen (o no) la línea de base.

- Muchos clientes utilizan las recomendaciones de línea de base de Intune como punto de partida y luego las personalizan para satisfacer sus demandas de TI y seguridad. La **línea de base de seguridad de MDM** de Windows 10 RS5 de Microsoft es la primera línea de base que se lanza. Esta línea de base se construye como una infraestructura genérica que permite a los clientes eventualmente importar otras líneas de base de seguridad basadas en CIS, NIST y otros estándares. En la actualidad, está disponible para Windows y eventualmente incluirá iOS/iPadOS y Android.

- La migración de las directivas de grupo de Active Directory locales a una solución en la nube pura mediante Azure Active Directory (AD) con Microsoft Intune es una odisea. Para ayudar, se incluyen plantillas de directiva de grupo en el [kit de herramientas para el cumplimiento de la seguridad](/windows/security/threat-protection/security-compliance-toolkit-10) que pueden ayudar a administrar dispositivos híbridos unidos a Azure AD. Estos dispositivos pueden obtener configuraciones de MDM desde la nube (Intune) y configuraciones de directiva de grupo desde los controladores de dominio locales según sea necesario.

## <a name="next-steps"></a>Pasos siguientes

- Consulte la configuración en las versiones más recientes de las líneas de base disponibles:
  - [Línea de base de seguridad MDM](security-baseline-settings-mdm-all.md)
  - [Línea de base de ATP de Microsoft Defender](security-baseline-settings-defender-atp.md)

- Comprobación del estado y supervisión de la [base de referencia y el perfil](security-baselines-monitor.md)