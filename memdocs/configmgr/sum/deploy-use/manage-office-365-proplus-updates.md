---
title: Administración de las actualizaciones de Office 365 ProPlus
titleSuffix: Configuration Manager
description: Configuration Manager sincroniza las actualizaciones de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio para que las actualizaciones estén disponibles para su implementación en los clientes.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 4967b8b289d54a6355cb0a1e6454d5fac469a733
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110413"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Administración de Office 365 ProPlus con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Note]
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.

Configuration Manager permite administrar aplicaciones de Office 365 ProPlus de las siguientes formas:

- [Implementación de aplicaciones de Office 365](#deploy-office-365-apps): puede iniciar el Instalador de Office 365 desde el panel [Administración de clientes de Office 365](office-365-dashboard.md) para facilitar la experiencia de instalación inicial de la aplicación de Office 365. El asistente permite configurar opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office y crear e implementar una aplicación de script con el contenido.

- [Implementación de actualizaciones de Office 365](#deploy-office-365-updates): puede administrar las actualizaciones del cliente de Office 365 mediante el flujo de trabajo de administración de actualizaciones de software. Cuando Microsoft publica una nueva actualización de cliente de Office 365 en Content Delivery Network (CDN) de Office, Microsoft también publica un paquete de actualización para Windows Server Update Services (WSUS). Después de que Configuration Manager sincroniza la actualización de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio, la actualización está disponible para implementarla en los clientes.

   > [!NOTE]
   > A partir de la versión 2002 de Configuration Manager, puede importar actualizaciones de Office 365 en entornos desconectados. Para obtener más información, consulte [Sincronización de actualizaciones de Office 365 desde un punto de actualización de software desconectado](../get-started/synchronize-office-updates-disconnected.md).   

- [Adición de idiomas para descargar actualizaciones de Office 365](#bkmk_o365_lang): puede agregar compatibilidad con Configuration Manager para descargar actualizaciones de los idiomas compatibles con Office 365. Esto significa que no es necesario que Configuration Manager admita el idioma mientras lo haga Office 365. Antes de la versión 1610 de Configuration Manager, debe descargar e implementar actualizaciones en los mismos idiomas configurados en los clientes de Office 365.

- [Cambiar el canal de actualización](#bkmk_channel): puede usar una directiva de grupo para distribuir un cambio del valor de una clave del Registro en los clientes de Office 365.

Para revisar la información de los clientes de Office 365 e iniciar algunas de estas acciones de administración de Office 365, utilice el [panel de administración de clientes de Office 365](office-365-dashboard.md).

## <a name="deploy-office-365-apps"></a>Implementación de aplicaciones de Office 365  
Inicie el Instalador de Office 365 desde el panel de administración de clientes de Office 365 para realizar la instalación inicial de las aplicaciones de Office 365. El asistente permite configurar opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office y crear e implementar una aplicación de script para los archivos. Hasta que se instale Office 365 en los clientes y se ejecute la [tara de actualizaciones automáticas de Office](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus), las actualizaciones de Office 365 no son aplicables. Puede ejecutar manualmente la tarea de actualización con fines de prueba.

Con las versiones anteriores de Configuration Manager, hay que realizar los siguientes pasos para instalar por primera vez aplicaciones de Office 365 en los clientes:
- Descargar la herramienta de implementación de Office 365 (ODT)
- Descargar los archivos de origen de instalación de Office 365 (incluidos todos los paquetes de idioma necesarios)
- Generar el archivo Configuration.xml que especifica la versión y el canal correctos de Office
- Crear e implementar un paquete heredado o una aplicación de script para que los clientes instalen las aplicaciones de Office 365

### <a name="requirements"></a>Requisitos
- El equipo que ejecuta el Instalador de Office 365 debe tener acceso a Internet.  
- El usuario que ejecuta el Instalador de Office 365 debe tener acceso de **lectura** y **escritura** para el uso compartido de la ubicación de contenido que se ofrece en el asistente.
- Si recibe un error de descarga 404, copie los archivos siguientes en la carpeta %temp% del usuario:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Implementar aplicaciones de Office 365 con la versión 1806 Configuration Manager o posteriores: 
A partir de la versión 1806 de Configuration Manager, la Herramienta de personalización de Office está integrada con el programa de instalación de Office 365 en la consola de Configuration Manager. Al crear una implementación de Office 365, puede establecer de manera dinámica la configuración más reciente de la manejabilidad de Office. <!--1358149-->

1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.
2. Haga clic en **Programa de instalación de Office 365** en el panel superior derecho. Se abre el Asistente para la instalación del cliente de Office 365.
3. En la página **Configuración de la aplicación**, proporcione un nombre y una descripción para la aplicación, escriba la ubicación de descarga de los archivos y haga clic en **Siguiente**. La ubicación se debe especificar de la siguiente forma: &#92;&#92;*servidor*&#92;*recurso compartido*.
4. En la página **Configuración Office**, haga clic en **Ir a la herramienta de personalización de Office**. Se abrirá la [Herramienta de personalización de Office de hacer clic y ejecutar](https://config.office.com).
5. Configure los valores deseados para la instalación de Office 365. Haga clic en **Enviar** en la esquina superior derecha de la página cuando complete la configuración. 
6. En la página **Implementación**, determine si quiere implementar ahora o en un momento posterior. Si decide implementar más adelante, puede encontrar la aplicación en la **Biblioteca de Software** > **Administración de aplicaciones** > **Aplicaciones**.  
7. Confirme la configuración en la página **Resumen**. 
8. Haga clic en **Siguiente** y después en **Cerrar** una vez que se complete el Asistente para la instalación del cliente de Office 365. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Implementar aplicaciones de Office 365 con la versión 1802 Configuration Manager o anteriores:

1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.
2. Haga clic en **Programa de instalación de Office 365** en el panel superior derecho. Se abre el Asistente para la instalación del cliente de Office 365.
3. En la página **Configuración de la aplicación**, proporcione un nombre y una descripción para la aplicación, escriba la ubicación de descarga de los archivos y haga clic en **Siguiente**. La ubicación se debe especificar de la siguiente forma: &#92;&#92;*servidor*&#92;*recurso compartido*.
4. En la página **Importar configuración de cliente**, elija si quiere importar la configuración del cliente de Office 365 desde un archivo de configuración XML existente o especificarla manualmente. Haga clic en **Siguiente** cuando haya terminado.  

    Si tiene un archivo de configuración existente, escriba su ubicación y vaya al paso 7. Debe especificar la ubicación con el formato &#92;&#92;*servidor*&#92;*recurso compartido*&#92;*nombre archivo*.XML.
    > [!IMPORTANT]    
    > El archivo de configuración XML debe contener solo [idiomas admitidos por el cliente Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. En la página **Productos de cliente**, seleccione el conjunto de aplicaciones Office 365 que use. Seleccione las aplicaciones que quiera incluir. Seleccione los productos de Office adicionales que deban incluirse y, después, haga clic en **Siguiente**.
6. En la página **Configuración de cliente**, elija la configuración que quiere incluir y luego haga clic en **Siguiente**.
7. En la página **Implementación**, elija si quiere implementar la aplicación y haga clic en **Siguiente**. <br/>Si decide no implementar el paquete en el asistente, vaya al paso 9.
8. Configure el resto de las páginas del asistente como lo haría para una implementación de aplicación normal. Para obtener más información, consulte [Crear e implementar una aplicación](../../apps/get-started/create-and-deploy-an-application.md).
9. Complete el asistente.
10. Puede implementar o modificar la aplicación en **Biblioteca de software** > **Información general** > **Administración de aplicaciones** > **Aplicaciones**.    

Después de crear e implementar aplicaciones de Office 365 mediante el Instalador de Office 365, Configuration Manager no administrará las actualizaciones de Office de forma predeterminada. Para permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager, vea [Implementar actualizaciones de Office 365 con Configuration Manager](#deploy-office-365-updates).

Después de implementar las aplicaciones de Office 365, puede crear reglas de implementación automática para mantener esas aplicaciones. Para crear una regla de implementación automática para las aplicaciones de Office 365, haga clic en **Crear un ADR** desde el [panel de administración de clientes de Office 365](office-365-dashboard.md). Seleccione **Cliente de Office 365** cuando elija el producto. Para más información, vea [Implementar actualizaciones de software automáticamente](automatically-deploy-software-updates.md).


## <a name="drill-through-required-office-365-updates"></a>Obtención de detalles de actualizaciones necesarias de Office 365
<!--4224414-->
*(Se introdujo en la versión 1906)*

Se pueden obtener detalles de las estadísticas de compatibilidad para ver qué dispositivos requieren una actualización de software de Office 365 específica. Para ver la lista de dispositivos, necesita permiso para ver las actualizaciones y las colecciones a las que pertenecen los dispositivos. Para explorar en profundidad la lista de dispositivos:

1. Vaya a **Biblioteca de software** > **Administración de clientes de Office 365** > **Actualizaciones de Office 365**.
1. Seleccione las actualizaciones que requiera al menos un dispositivo.
1. En la pestaña **Resumen** encontrará un gráfico circular bajo **Estadísticas**.
1. Seleccione el hipervínculo **Vista necesaria** situado junto al gráfico circular para obtener los detalles de la lista de dispositivos.
1. Esta acción le llevará a un nodo temporal en **Dispositivos** donde podrá ver los dispositivos que requieren la actualización. También puede realizar acciones para el nodo, como crear una colección a partir de la lista.


## <a name="deploy-office-365-updates"></a>Implementación de actualizaciones de Office 365

Siga estos pasos para implementar actualizaciones de Office 365 con Configuration Manager:

1. [Compruebe los requisitos](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365 en la sección **Requisitos para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365** del artículo.  

2. [Configurar puntos de actualización de software](../get-started/configure-classifications-and-products.md) para sincronizar las actualizaciones de cliente de Office 365. Definir las **actualizaciones** para la clasificación y seleccionar el **cliente de Office 365** para el producto. Sincronice las actualizaciones de software después de configurar los puntos de actualización de software para usar la clasificación **Actualizaciones**.
3. Permita que los clientes de Office 365 reciban actualizaciones de Configuration Manager. Use la directiva de grupo o la configuración de cliente de Configuration Manager para habilitar el cliente.

    **Método 1**: a partir de la versión 1606 de Configuration Manager, se puede usar la configuración de cliente de Configuration Manager para administrar el agente cliente de Office 365. Después de configurar esta opción e implementar las actualizaciones de Office 365, el agente cliente de Configuration Manager se comunica con el agente cliente de Office 365 para descargar las actualizaciones desde un punto de distribución e instalarlas. Configuration Manager realiza un inventario de la configuración de cliente de Office 365 ProPlus.    

      1. En la consola de Configuration Manager, haga clic en **Administración** > **Información general** > **Configuración de cliente**.  

      2. Abra la configuración de dispositivo adecuada para habilitar el agente cliente. Para más información sobre las configuraciones de cliente predeterminadas y personalizadas, consulte [Cómo establecer la configuración de cliente](../../core/clients/deploy/configure-client-settings.md).  

      3. Haga clic en **Actualizaciones de software** y seleccione **Sí** para el valor **Habilitar administración del Agente cliente de Office 365**.  

    **Método 2**:  [permita que los clientes de Office 365 reciban actualizaciones](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) de Configuration Manager mediante la directiva de grupo o la herramienta de implementación de Office.  

4. [Implemente actualizaciones de Office 365](deploy-software-updates.md) en los clientes.

> [!Important]
> - A partir de la versión 1706 de Configuration Manager, las actualizaciones de cliente de Office 365 se han movido al nodo **Administración de clientes de Office 365** >**Actualizaciones de Office 365**. Este movimiento no afectará a la configuración actual de ADR. 
> - Antes de la versión 1610 de Configuration Manager, debe descargar e implementar actualizaciones en los mismos idiomas configurados en los clientes de Office 365. Por ejemplo, supongamos que tiene un cliente de Office 365 configurado con los idiomas en-us y de-de. En el servidor de sitio, descargue e implemente solo el contenido de en-us correspondiente a una actualización de Office 365 correspondiente. Cuando el usuario inicie la instalación de esta actualización desde el Centro de software, la actualización se bloquea mientras se descarga el contenido para de-de. 

> [!NOTE]  
>
> Si Office 365 ProPlus se instaló recientemente y, dependiendo de cómo se haya instalado, es posible que el canal de actualización aún no se haya establecido. En ese caso, las actualizaciones implementadas se detectarán como no aplicables. Hay un [tarea programada de Actualizaciones automáticas](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) creada cuando se instala Office 365 ProPlus. En esta situación, es necesario ejecutar esta tarea al menos una vez para que el canal de actualización se establezca y las actualizaciones se detecten como aplicables.
>
> Si Office 365 ProPlus se instaló recientemente y las actualizaciones implementadas no se detectan, desde el punto de vista de las pruebas, puede iniciar la tarea de Actualizaciones automáticas de Office manualmente y luego iniciar el [ciclo de evaluación de implementación de Actualizaciones de software](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) en el cliente. Para instrucciones sobre cómo hacer esto en una secuencia de tareas, consulte [Actualización de Office 365 ProPlus en una secuencia de tareas](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence).

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Comportamiento al reiniciar y notificaciones de cliente para las actualizaciones de Office 365
Al implementar una actualización en un cliente de Office 365, el comportamiento de reinicio y las notificaciones de cliente serán distintas en función de la versión de Configuration Manager. En la tabla siguiente se proporciona información sobre la experiencia de usuario final cuando el cliente recibe una actualización de Office 365:

|Versión de Configuration Manager |Experiencia del usuario final|  
|----------------|---------------------|
|1706, 1710|El cliente recibe notificaciones emergentes y en la aplicación, así como un cuadro de diálogo de cuenta atrás, antes de instalar la actualización.|
|1802| El cliente recibe notificaciones emergentes y en la aplicación, así como un cuadro de diálogo de cuenta atrás, antes de instalar la actualización. </br>Si las aplicaciones de Office 365 se ejecutan durante la aplicación de una actualización de cliente de Office 365, las aplicaciones de Office no se cerrarán forzosamente. En su lugar, se devolverá la instalación de la actualización y se requerirá el reinicio del sistema. <!--510006-->|


> [!Important]
>
>En la versión 1706 de Configuration Manager, tenga en cuenta los siguientes detalles:
>
>- Un icono de notificación se muestra en el área de notificación de la barra de tareas para aplicaciones necesarias, donde la fecha límite es 48 horas y el contenido de la actualización se ha descargado. 
>- Un cuadro de diálogo de cuenta atrás se muestra en las aplicaciones necesarias, donde la fecha límite es de 7,5 horas y la actualización se ha descargado. El usuario puede posponer el cuadro de diálogo de cuenta atrás hasta tres veces antes de la fecha límite. Cuando se hace, se muestra la cuenta atrás de nuevo después de 2 horas. Si no se pospone, hay una cuenta regresiva de 30 minutos y la actualización se instala cuando expira la cuenta atrás.
>- Una notificación emergente podría no mostrarse hasta que el usuario haga clic en el icono del área de notificación. Además, si en el área de notificación hay poco espacio, el icono de notificación podría no mostrarse, a menos que el usuario abra o expanda el área de notificación. 
>- El cuadro de diálogo de notificación y cuenta atrás podría iniciarse cuando el usuario no esté trabajando activamente en el dispositivo. Por ejemplo, si el dispositivo está bloqueado por la noche, es posible que las aplicaciones de Office que se ejecutan en el dispositivo se cierren forzosamente para instalar la actualización. Antes de cerrar la aplicación, Office guarda los datos de aplicación para evitar la pérdida de datos. 
>- Si la fecha límite ya ha pasado o está configurada para iniciarse lo antes posible, las aplicaciones de Office en ejecución podrían cerrarse forzosamente sin enviar notificaciones. 
>- Si el usuario instala una actualización de Office antes de la fecha límite, Configuration Manager comprueba que está instalada la actualización cuando se alcanza la fecha límite. Si no se detecta la actualización en el dispositivo, se instala la actualización. 
>- La barra de notificación en aplicación no se muestra en una aplicación de Office en ejecución antes de descargarse la actualización. Después de descargarse, la notificación en aplicación solo se muestra para las aplicaciones recién abiertas.
>- Para las actualizaciones de Office que desencadena una ventana de servicio o las programadas para un horario no comercial, las aplicaciones de Office en ejecución podrían cerrarse forzosamente para instalar la actualización sin enviar notificaciones. 
>- Para obtener más información, vea [Notificaciones de actualización de usuarios finales de Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a> Adición de idiomas para descargar actualizaciones de Office 365
Puede agregar compatibilidad con Configuration Manager para descargar actualizaciones de los idiomas compatibles con Office 365.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Descarga de actualizaciones para idiomas adicionales en la versión 1902
<!--3555955-->

Desde la versión 1902 de Configuration Manager, el flujo de trabajo de actualización ahora separa los 38 idiomas de **Windows Update** de los numerosos idiomas adicionales de la **actualización de cliente de Office 365**.

Para seleccionar los idiomas necesarios, use los siguientes recursos de la página **Selección del idioma**:
- Asistente para crear regla de implementación automática
- Asistente para implementar actualizaciones de software
- Asistente para descargar actualizaciones de software
- Propiedades de la regla de implementación automática

En la página **Selección de idiomas**, seleccione **Actualización de cliente de Office 365** y, después, haga clic en **Editar**. Agregue los idiomas necesarios para Office 365 y haga clic en **Aceptar**.

![Captura de pantalla de adición de idiomas adicionales para Office 365](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Para agregar compatibilidad para descargar actualizaciones de idiomas adicionales en la versión 1810 y anteriores

Siga el procedimiento de abajo en el punto de actualización de software del sitio de administración central o del sitio primario independiente.

> [!IMPORTANT]  
> La configuración de idiomas de actualización de Office 365 adicionales es una configuración global del sitio. Después de agregar los idiomas con el procedimiento siguiente, todas las actualizaciones de Office 365 se descargarán en esos idiomas, y en los que seleccione en la página **Selección de idioma** del Asistente para descargar actualizaciones de software o del Asistente para implementar actualizaciones de software.

1. Desde el símbolo del sistema, escriba *wbemtest* como usuario administrativo para abrir la Herramienta de comprobación del instrumental de administración de Windows.
2. Haga clic en **Conectar** y, después, escriba *root\sms\site_&lt;códigoDeSitio&gt;* .
3. Haga clic en **Consulta** y, después, ejecute la consulta siguiente: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta WMI](../media/1-wmiquery.png)
4. En el panel de resultados, haga doble clic en el objeto con el código de sitio del sitio de administración central o del sitio primario independiente.
5. Seleccione la propiedad **Props**, haga clic en **Editar propiedad** y, después, haga clic en **Ver incrustado**.
   ![Editor de propiedades](../media/2-propeditor.png)
6. Empiece en el primer resultado de la consulta y abra cada objeto hasta que encuentre el objeto que tenga **AdditionalUpdateLanguagesForO365** para la propiedad **PropertyName**.
7. Seleccione **Value2** y haga clic en **Editar propiedad**.  
   ![Editar la propiedad Value2](../media/3-queryresult.png)
8. Agregue idiomas adicionales a la propiedad **Value2** y haga clic en **Guardar propiedad**. <br/> Por ejemplo, pt-pt (para portugués de Portugal), af-za (para afrikáans de Sudáfrica), nn-no (para noruego nynorsk de Noruega), etc. Escribiría `pt-pt,af-za,nn-no` para los idiomas de ejemplo. No use espacios entre los idiomas.
 
   ![Agregar idiomas en el Editor de propiedades](../media/4-props.png)  
9. Haga clic en **Cerrar**, **Cerrar**, **Guardar propiedad** y **Guardar objeto** (si hace clic en **Cerrar** aquí se descartarán los valores). Haga clic en **Cerrar** y en **Salir** para salir de la Herramienta de comprobación del instrumental de administración de Windows.
10. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365** > **Actualizaciones de Office 365**.
11. Ahora, las actualizaciones de Office 365 se descargarán en los idiomas seleccionados en el asistente y en los que haya configurado en este procedimiento. Para comprobar que las actualizaciones se han descargado en esos idiomas, vaya al origen del paquete de la actualización y busque los archivos con el código de idioma en el nombre de archivo.  
    ![Nombres de archivo con idiomas adicionales](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>Actualización de Office 365 ProPlus en una secuencia de tareas
Cuando se usa el paso de la secuencia de tareas [Instalar actualizaciones de software](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) para instalar las actualizaciones de Office 365, es posible que las actualizaciones implementadas se detecten como no aplicables.  Esto puede ocurrir si la tarea programada de Actualizaciones automáticas de Office no se ha ejecutado al menos una vez (consulte la nota de [Implementación de actualizaciones de Office 365](manage-office-365-proplus-updates.md#deploy-office-365-updates)). Por ejemplo, esto podría suceder si Office 365 ProPlus se ha instalado inmediatamente antes de ejecutar este paso.

Para asegurarse de que el canal de actualización está establecido para que las actualizaciones implementadas se detecten correctamente, use uno de los métodos siguientes:

**Método 1**:
1. En una máquina con la misma versión de Office 365 ProPlus, abra el Programador de tareas (taskschd.msc) e identifique la tarea de las actualizaciones automáticas de Office 365. Por lo general, se encuentra en **Biblioteca del Programador de tareas** >**Microsoft**>**Office**.
2. Haga clic con el botón derecho en la tarea de actualización automática y seleccione **Propiedades**.
3. Vaya a la pestaña **Acciones** y haga clic en **Editar**. Copie el comando y los argumentos. 
4. En la consola de Configuration Manager, edite la secuencia de tareas.
5. Agregue un nuevo paso **Ejecutar línea de comandos** antes del paso **Instalar actualizaciones de software** en la secuencia de tareas. Si Office 365 ProPlus se instala como parte de la misma secuencia de tareas, asegúrese de que este paso se ejecuta después de instalar Office.
6. Copie el comando y los argumentos que ha recopilado de la tarea programada de actualizaciones automáticas de Office. 
7. Haga clic en **Aceptar**. 

**Método 2**:
1. En una máquina con la misma versión de Office 365 ProPlus, abra el Programador de tareas (taskschd.msc) e identifique la tarea de las actualizaciones automáticas de Office 365. Por lo general, se encuentra en **Biblioteca del Programador de tareas** >**Microsoft**>**Office**.
2. En la consola de Configuration Manager, edite la secuencia de tareas.
3. Agregue un nuevo paso **Ejecutar línea de comandos** antes del paso **Instalar actualizaciones de software** en la secuencia de tareas. Si Office 365 ProPlus se instala como parte de la misma secuencia de tareas, asegúrese de que este paso se ejecuta después de instalar Office.
4. En el campo de la línea de comandos, escriba la línea de comandos que ejecutará la tarea programada. Vea el ejemplo siguiente asegurándose de que la cadena de comillas coincide con la ruta de acceso y el nombre de la tarea identificada en el paso 1.  

    Ejemplo: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Haga clic en **Aceptar**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a><a name="bkmk_channel"></a> Cambiar el canal de actualización después de permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager

Después de implementar Office 365 ProPlus, puede cambiar el canal de actualización con directiva de grupo o la Herramienta de implementación de Office (ODT). Por ejemplo, puede trasladar un dispositivo del Canal semianual al Canal semianual (dirigido). Al cambiar de canal, Office se actualiza automáticamente sin tener que volver a instalar ni descargar la versión completa. Para obtener más información, consulte el artículo sobre cómo [cambiar el canal de actualización de Office 365 ProPlus para dispositivos de su organización](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Pasos siguientes

Utilice el panel de administración de clientes de Office 365 en Configuration Manager para revisar la información de los clientes de Office 365 e implementar las aplicaciones de Office 365. Para más información, consulte [Panel de administración de clientes de Office 365](office-365-dashboard.md).
