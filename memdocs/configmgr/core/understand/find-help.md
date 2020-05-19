---
title: Búsqueda de ayuda
titleSuffix: Configuration Manager
description: Busque recursos para obtener más información sobre Configuration Manager.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bae98a8df1d8b8ff843bd333083c4c6ad68848c
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343191"
---
# <a name="find-help-for-using-configuration-manager"></a>Buscar ayuda para usar Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se proporcionan las siguientes secciones con varios recursos para buscar ayuda sobre el uso de Configuration Manager:  

- [Documentación del producto](#bkmk_Info)  

- [Compartir comentarios sobre el producto](#product-feedback)  

- [Seguir el blog del equipo de Configuration Manager](#BKMK_ProductGroupBlog)  

- [Opciones de soporte técnico y recursos de la comunidad](#BKMK_SupportOptions)  

Para obtener ayuda sobre la accesibilidad del producto, vea [Características de accesibilidad](accessibility-features.md).  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> Documentación del producto  

Para acceder a la documentación más reciente del producto, comience en el [índice de biblioteca](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Para obtener sugerencias sobre cómo buscar, proporcionar comentarios y obtener más información sobre el uso de la documentación del producto, vea [Cómo usar los documentos](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> Comentarios sobre el producto a partir de la versión 1806

A partir de la versión 1806 de Configuration Manager, puede enviar comentarios sobre el producto directamente desde la consola. Si tiene que adjuntar registros, use [Concentrador de comentarios](#BKMK_FeedbackHub). Puede hacer lo siguiente: <!--1357542-->

- **Enviar una sonrisa**: envíe comentarios sobre lo que le ha gustado.
- **Enviar un ceño fruncido**: envíe comentarios sobre lo que no le ha gustado.
- **Enviar una sugerencia**: se abre el [Sitio web de UserVoice](https://configurationmanager.uservoice.com/) para que pueda compartir su idea.

  ![Enviar comentarios en Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Enviar una sonrisa o un ceño fruncido

Para enviar comentarios sobre algo que le gustó siga las siguientes instrucciones:

1. En la esquina superior derecha de la consola, haga clic en la cara sonriente.
2. En el menú desplegable, seleccione **Enviar una sonrisa** o **Enviar un ceño fruncido**.
3. Utilice el cuadro de texto para explicar lo que le ha gustado y lo que no. 
4. Elija si quiere compartir su dirección de correo electrónico y una captura de pantalla.
5. Haga clic en **Enviar comentarios**
     - Si no tiene conectividad a Internet, haga clic en **Guardar** en la parte inferior. Siga las instrucciones de la sección [Enviar comentarios que ha guardado para enviarlos más tarde](#BKMK_NoInternet) para enviarlo a Microsoft. 

![Formulario de envío de comentarios en Configuration Manager 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Mensajes de estado para enviar una sonrisa
<!--5891852-->
A partir de Configuration Manager 2002, al usar las opciones **Enviar una sonrisa** o **Enviar un ceño fruncido**, se crea un mensaje de estado en el momento de enviar los comentarios. Con esta mejora se proporciona un registro de lo siguiente:
- Momento en el que se han enviado los comentarios
- Quién ha enviado los comentarios
- Identificador de los comentarios
- Si los comentarios se han enviado correctamente o no
   - Si el identificador es el 53900, significa que los comentarios se han enviado correctamente.
   - En cambio, si el identificador es el 53901, significa que los comentarios no se han enviado.

Puede ver los mensajes de estado en **Supervisión** > **Estado del sistema** > **Consultas de mensaje de estado**. Comience con la consulta **Todos los mensajes de estado** y seleccione el período de tiempo. Cuando se carguen los mensajes, haga clic en el botón **Filtrar mensajes** y filtre por el identificador de mensaje 53900 o 53901.

Los mensajes de estado no se crean si [envía comentarios que ha guardado para enviar más tarde](find-help.md#BKMK_NoInternet).

[![Mensaje de estado que indica que los comentarios se han enviado correctamente](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Enviar una sugerencia

Cuando **envía una sugerencia**, se le redirige a [UserVoice](https://configurationmanager.uservoice.com/), un sitio web de terceros, para que comparta su idea. El equipo de producto de Configuration Manager usa los siguientes valores de estado en UserVoice:

- **Anotado**: entendemos la solicitud y tiene sentido. La hemos agregado a nuestro trabajo pendiente.
- **Planeado**: hemos empezado a escribir código para esta característica y esperamos que aparezca en una compilación de versión preliminar técnica dentro de los próximos meses.
- **Iniciado**: la característica se encuentra actualmente en una versión preliminar técnica. Pruébela y envíenos sus comentarios para hacernos saber si va por buen camino. Incluya comentarios adicionales en la sección de comentarios de la solicitud original para que otros usuarios puedan verlos y escribir su opinión. Nosotros también los consultaremos y nos basaremos en ellos para intentar mejorar la característica.
- **Completado**: la primera versión de la característica se encuentra en una compilación de producción. Este estado no significa que hayamos completado la característica al 100 % y que no vayamos a mejorarla más, sino que la primera versión de la característica se encuentra en una compilación de producción y puede empezar a usarse. La hemos marcado como completada por las razones siguientes:
  - Queremos que sepa que la característica está lista para la producción.
  - Queremos devolverle sus votos de UserVoice para que pueda usarlos en otros elementos.
  - Puede presentar nuevas solicitudes de cambio de diseño para esta característica, a fin de hacernos saber cuál es la siguiente mejora más importante para la característica.

### <a name="information-sent-with-feedback"></a>Información enviada con comentarios

Cuando **envíe una sonrisa** o **envíe un ceño fruncido**, se incluirá la información siguiente con los comentarios:

- Información de compilación del sistema operativo
- Id. de jerarquía de Configuration Manager
- Información de compilación del producto
- Información de idioma
- Identificador de dispositivo 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> Enviar comentarios que ha guardado para enviarlos más tarde

1. Haga clic en **Guardar** en la parte inferior de la ventana **Proporcionar comentarios**. 
2. Guarde el archivo .zip. Si el equipo local no tiene acceso a Internet, copie el archivo en una máquina conectada a Internet. 
3. Si es necesario, copie la carpeta UploadOfflineFeedback ubicada en `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`.
    - Para obtener más información sobre la carpeta CD.Latest, vea [La carpeta CD.Latest](../servers/manage/the-cd.latest-folder.md)

4. En una máquina conectada a Internet, abra un símbolo del sistema. 
5. Ejecute el comando siguiente: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`.
    
    - Si quiere, puede especificar los parámetros siguientes:
        -  `-t, --timeout` Tiempo de espera en segundos para enviar los datos. 0 es ilimitado. El valor predeterminado es 30.
        - `-s --silent` Ningún registro en la consola (no se puede combinar con --verbose)
        - `-v, --verbose` Registro detallado de salida en la consola (no se puede combinar con --silent)
        - `--help` Muestra la pantalla de ayuda
    
    - A partir de la versión 1910, la utilidad UploadOfflineFeedback admite el uso de un servidor proxy. Puede especificar los parámetros siguientes:
        - `-x, --proxy` especifica el servidor proxy que se va a conectar a Internet.
        - `-o, --port` especifica el puerto del servidor proxy que se va a conectar a Internet.
        - `-u, --user` especifica el nombre de usuario del servidor proxy que se va a conectar a Internet.
        - `-w, --password` especifica la contraseña del servidor proxy que se va a conectar a Internet. Escriba un asterisco (*) para generar una solicitud de contraseña. La contraseña no se muestra cuando se escribe en la solicitud de contraseña. Se recomienda especialmente usar un asterisco (*) para generar una solicitud de entrada de contraseña, ya que el texto sin formato en la línea de comandos es menos seguro.
        - `-i` para omitir la comprobación de conexión: Omite la comprobación de conexión de red, solo carga los comentarios con la configuración especificada.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> Confirmación de comentarios de la consola

<!--3556010-->
A partir de la versión 1902, al enviar comentarios a través de la consola de Configuration Manager o UploadOfflineFeedback.exe, aparecerá un mensaje de confirmación. Este mensaje incluye un **identificador de comentario** que puede enviar a Microsoft como identificador de seguimiento.

- Para copiar el **identificador de comentario**, seleccione el icono de copia situado junto al identificador o use las teclas de método abreviado **CTRL** + **C**.
  - Este identificador no se almacena en el equipo, así que asegúrese de copiarlo antes de cerrar la ventana.
- Si hace clic en **No volver a mostrar este mensaje**, suprimirá el cuadro de diálogo y evitará que aparezca en el futuro.

   ![Confirmación de comentarios de la consola en Configuration Manager 1902](media/1902-feedback-id-example.png)
- La herramienta de comando **UploadOfflineFeedback** escribe el **FeedbackID** en la consola, a menos que se use -s o --silent.

  ![Confirmación de comentarios de UploadOfflineFeedback.exe en Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> Comentarios sobre el producto para la versión 1802 y anteriores

Notifique los posibles defectos del producto a través de la [aplicación Centro de opiniones](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) integrada en Windows 10. Cuando **agregue nuevos comentarios**, no olvide seleccionar la categoría **Enterprise Management** y, después, elija una de las subcategorías siguientes:
- Cliente de Configuration Manager
- Consola de Configuration Manager
- Implementación del sistema operativo de Configuration Manager
- Servidor de Configuration Manager

Siga usando la [página de UserVoice](https://configurationmanager.uservoice.com/) para votar por nuevas ideas de características en Configuration Manager. El equipo de producto de Configuration Manager usa los siguientes valores de estado en UserVoice:

- **Anotado**: entendemos la solicitud y tiene sentido. La hemos agregado a nuestro trabajo pendiente.
- **Planeado**: hemos empezado a escribir código para esta característica y esperamos que aparezca en una compilación de versión preliminar técnica dentro de los próximos meses.
- **Iniciado**: la característica se encuentra actualmente en una versión preliminar técnica. Pruébela y envíenos sus comentarios para hacernos saber si va por buen camino. Incluya comentarios adicionales en la sección de comentarios de la solicitud original para que otros usuarios puedan verlos y escribir su opinión. Nosotros también los consultaremos y nos basaremos en ellos para intentar mejorar la característica.
- **Completado**: la primera versión de la característica se encuentra en una compilación de producción. Este estado no significa que hayamos completado la característica al 100 % y que no vayamos a mejorarla más, sino que la primera versión de la característica se encuentra en una compilación de producción y puede empezar a usarse. La hemos marcado como completada por las razones siguientes:
  - Queremos que sepa que la característica está lista para la producción.
  - Queremos devolverle sus votos de UserVoice para que pueda usarlos en otros elementos.
  - Puede presentar nuevas solicitudes de cambio de diseño para esta característica, a fin de hacernos saber cuál es la siguiente mejora más importante para la característica.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Blog del equipo de Configuration Manager  

El equipo de ingeniería de Configuration Manager y los equipos asociados usan el [blog Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) para ofrecer información técnica y otras noticias sobre Configuration Manager y tecnologías relacionadas. Nuestras entradas de blog complementan la documentación del producto y la información de soporte técnico.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> Opciones de soporte técnico y recursos de la comunidad  

Los vínculos siguientes proporcionan información acerca de opciones de soporte y recursos de la comunidad:  

-   [Soporte técnico de Microsoft](https://aka.ms/cmcbsupport)  

-   [Comunidad de Configuration Manager: guía de supervivencia de Configuration Manager (rama actual)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Página de foros de Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
