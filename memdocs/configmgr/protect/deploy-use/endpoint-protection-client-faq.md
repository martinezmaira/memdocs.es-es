---
title: Preguntas más frecuentes sobre el cliente de Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga respuestas a las preguntas más frecuentes sobre Windows Defender y Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906831"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Preguntas más frecuentes sobre el cliente de Endpoint Protection

*Se aplica a: Configuration Manager (rama actual)*


Estas preguntas más frecuentes están dirigidas a usuarios de equipos cuyos administradores de TI hayan implementado Windows Defender o Endpoint Protection en sus equipos administrados. Este contenido podría no ser aplicable a otro software antimalware. Microsoft System Center Endpoint Protection administra Windows Defender en Windows 10. También puede implementar y administrar el cliente de Endpoint Protection en equipos anteriores a Windows 10. Aunque en este artículo se describe Windows Defender, su información también se aplica a Endpoint Protection.  

-   [¿Por qué es necesario el software antivirus y antispyware?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [¿Cómo puedo saber si mi equipo está infectado con software malintencionado?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [¿Cómo encuentro la versión de Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [¿Qué debo hacer si Windows Defender o Endpoint Protection detecta software malintencionado en mi equipo?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [¿Qué es un virus?](#what-is-a-virus)  
-   [¿Qué es un spyware?](#what-is-spyware)  
-   [¿Cuál es la diferencia entre virus, spyware y otro software potencialmente peligroso?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [¿De dónde provienen los virus, el spyware y otro software potencialmente no deseado?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [¿Puede mi equipo infectarse con software malintencionado sin mi conocimiento?](#can-i-get-malicious-software-without-knowing-it)  
-   [¿Por qué es importante revisar los contratos de licencia antes de instalar software?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [¿Qué diferencias hay entre Endpoint Protection y Windows Defender?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [¿Por qué Windows Defender no detecta cookies?](#why-doesnt-windows-defender-detect-cookies)  
-   [¿Cómo puedo evitar el malware?](#how-can-i-prevent-malware)  
-   [¿Qué son las definiciones de virus y spyware?](#what-are-virus-and-spyware-definitions)  
-   [¿Cómo mantengo las definiciones de virus y spyware actualizadas?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [¿Cómo quito o restauro elementos puestos en cuarentena por Windows Defender o Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [¿Qué es la protección en tiempo real?](#what-is-real-time-protection)  
-   [¿Cómo sé que se ejecuta Windows Defender o Endpoint Protection en mi equipo?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [¿Cómo se configuran las alertas de Windows Defender o Endpoint Protection?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>¿Por qué es necesario el software antivirus y antispyware?  

 Es fundamental asegurarse de que el equipo cuenta con un software de protección frente a software malintencionado. El software malintencionado, que incluye virus, spyware u otro software potencialmente no deseado, puede intentar instalarse en el equipo en cualquier momento en que se conecte a Internet. También puede infectar el equipo al instalar un programa mediante un CD, DVD u otro medio extraíble. El software malintencionado también puede programarse para ejecutarse en momentos inesperados, no solo al instalarse.  

 Windows Defender o Endpoint Protection ofrece tres maneras de ayudar a impedir que el software malintencionado infecte el equipo:  

-   **Uso de protección en tiempo real**: esta protección permite que Windows Defender supervise el equipo en todo momento y envíe una alerta si algún software malintencionado, como virus, spyware u otro software potencialmente no deseado intenta instalarse o ejecutarse en el equipo. De este modo, Windows Defender suspende el software y permite que el usuario siga la recomendación respecto del software o realice una acción alternativa.

-   **Opciones de exploración**: puede usar Windows Defender para detectar amenazas potenciales, como virus, spyware y otro software malintencionado, que podrían poner el equipo en riesgo. También puede utilizarlo para programar exámenes con regularidad y para quitar el software malintencionado que se hubiera detectado durante el examen.  

-   **Comunidad Microsoft Active Protection Service**: esta comunidad en línea ayuda a ver cómo otras personas responden al software que aún no se ha clasificado en cuanto a riesgos. Puede usar esta información para decidir si permite o no el software en su equipo. A cambio, si participa, sus elecciones se agregan a la clasificación de la comunidad para ayudar a otros usuarios a decidir lo que hacer.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>¿Cómo puedo saber si mi equipo está infectado con software malintencionado?  

 Es posible que tenga algún tipo de software malintencionado (por ejemplo, virus, spyware u otro software potencialmente no deseado) en el equipo si:  

-   Observa nuevas barras de herramientas, vínculos o favoritos que no ha agregado deliberadamente al explorador web.  

-   La página principal, el puntero del mouse o el programa de búsqueda cambian de forma inesperada.  

-   Escribe la dirección de un sitio específico, como un motor de búsqueda, pero se lo dirige a otro sitio web sin previo aviso.  

-   Se eliminan automáticamente archivos del equipo.  

-   El equipo se usa para atacar a otros equipos.  

-   Aparecen ventanas emergentes, incluso aunque no esté navegando en Internet.  

-   El equipo de repente comienza a funcionar más despacio de lo normal. No todos los problemas de rendimiento del equipo están causados por software malintencionado, pero este software, en especial el spyware, puede ocasionar un cambio notable.  

Puede haber software malintencionado en el equipo aunque no se observe ningún síntoma. Este tipo de software puede recopilar información sobre usted y su equipo sin su conocimiento o consentimiento. Para ayudar a proteger su privacidad y su equipo, debe ejecutar Windows Defender o Endpoint Protection en todo momento.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>¿Cómo encuentro la versión de Windows Defender?
 Para ver la versión de Windows Defender que se ejecuta en el equipo, abra Windows Defender (haga clic en **Inicio** y busque **Windows Defender**), haga clic en **Configuración** y desplácese a la parte inferior de la configuración de Windows Defender hasta que encuentre **Información de versión**.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>¿Qué debo hacer si Windows Defender o Endpoint Protection detecta software malintencionado en mi equipo?  

 Si Windows Defender detecta software malintencionado o potencialmente no deseado en el equipo (ya sea al supervisarlo mediante protección en tiempo real o tras efectuar un examen), le avisa sobre el elemento detectado mediante un mensaje de notificación en la esquina inferior derecha de la pantalla.  

 El mensaje de notificación incluye un botón **Limpiar el equipo** y un vínculo **Mostrar detalles** que permite ver información adicional acerca del elemento detectado. Haga clic en el vínculo **Mostrar detalles** para abrir la ventana **Detalles de posibles amenazas** a fin de obtener información adicional acerca del elemento detectado. Entonces puede seleccionar la acción que va a aplicar al elemento o hacer clic en **Limpiar el equipo**. Si necesita ayuda para determinar qué acción va a aplicar sobre el elemento detectado, use como guía el nivel de alerta que Windows Defender ha asignado al elemento (para obtener más información, vea Información sobre los niveles de alerta).  

 Los niveles de alerta ayudarán a elegir cómo responder a los virus, spyware y otro software potencialmente no deseado. Aunque Windows Defender le va a recomendar que quite todos los virus y el spyware, no todo el software marcado es malintencionado o no deseado. La información siguiente puede ayudarlo a decidir qué hacer si Windows Defender detecta software potencialmente no deseado en su equipo.  

 En función del nivel de alerta, puede seleccionar una de las siguientes acciones para aplicarla al elemento detectado:  

- **Quitar**: esta acción quita el software del equipo de forma permanente.  

- **Cuarentena**: esta acción pone el software en cuarentena de modo que no pueda ejecutarse. Si Windows Defender pone un software en cuarentena, lo mueve a otra ubicación del equipo y, así, evita que se ejecute hasta que usted decida restaurarlo o quitarlo del equipo.  

- **Permitir**: esta acción agrega el software a la lista de permitidos de Windows Defender y permite que se ejecute en el equipo. Windows Defender dejará de alertar sobre los riesgos que el software pueda suponer para la privacidad o el equipo.  

  Si selecciona **Permitir** para un elemento (por ejemplo, software), Windows Defender dejará de alertar sobre los riesgos que el software pueda suponer para la privacidad o el equipo. Por tanto, agregue software a la lista de permitidos únicamente si confía en él y en su publicador.  

### <a name="how-to-remove-potentially-harmful-software"></a>Cómo quitar el software potencialmente peligroso

Para quitar todos los elementos no deseados o potencialmente peligrosos que Windows Defender detecta de forma rápida y sencilla, use la opción **Limpiar el equipo** .  

1.  Cuando vea el mensaje de notificación que Windows Defender muestra en el área de notificación al detectar amenazas potenciales, haga clic en **Limpiar el equipo**.  

2.  Windows Defender quita las amenazas potenciales y le avisa cuando termina de limpiar el equipo.  

3.  Para obtener más información acerca de las amenazas detectadas, haga clic en la pestaña **Historial** y seleccione **Todos los elementos detectados**.  

4.  Si no desea ver todos los elementos detectados, haga clic en **Ver detalles**. Si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o confirme la acción.

> [!NOTE]  
>  Durante la limpieza del equipo, y siempre que sea posible, Windows Defender solo quita la parte infectada de un archivo, no el archivo completo.  

##  <a name="what-is-a-virus"></a>¿Qué es un virus?  
 Los virus informáticos son programas de software diseñados expresamente para interferir con el funcionamiento del equipo, para registrar, dañar o eliminar datos o para infectar otros equipos a través del uso de Internet. A menudo, los virus ralentizan las operaciones y provocan otros problemas en el proceso.  

##  <a name="what-is-spyware"></a>¿Qué es el spyware?  
 El spyware es software que puede instalarse o ejecutarse por sí solo en el equipo sin su consentimiento o sin proporcionarle el aviso o el control correspondiente. Además, el spyware podría no mostrar síntomas tras infectar el equipo, pero muchos programas malintencionados o no deseados pueden afectar el funcionamiento del equipo. Por ejemplo, el spyware puede supervisar el comportamiento en línea del usuario o recopilar información personal (como información que puede identificar al usuario u otra información confidencial), modificar la configuración del equipo o hacer que el equipo se ejecute lentamente.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>¿Cuál es la diferencia entre virus, spyware y otro software potencialmente peligroso?  
 Tanto los virus como el spyware se instalan en el equipo sin conocimiento del usuario y ambos tienen la capacidad de ser intrusivos y destructivos. También tienen la capacidad de capturar la información que se almacena en el equipo y dañarla o eliminarla. Ambos pueden afectar negativamente al rendimiento del equipo.  

 Las principales diferencias entre los virus y el spyware es su comportamiento en el equipo. Los virus, al igual que los organismos vivos, tienen el propósito de infectar un equipo, replicarse y luego propagarse a tantos equipos como sea posible. Pero el spyware se parece más bien a un topo, ya que intenta "meterse" en el equipo y permanecer allí tanto como sea posible y envía información valiosa sobre el equipo a un origen externo mientras está allí.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>¿De dónde provienen los virus, el spyware y otro software potencialmente no deseado?  
 El software no deseado, como los virus, puede instalarse a través de sitios web o programas que descarga el usuario o que se instalan mediante un CD, DVD, un disco duro externo o un dispositivo. El spyware suele instalarse a través de software gratuito, como programas de uso compartido de archivos, protectores de pantalla o barras de herramientas de búsqueda.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>¿Puede mi equipo infectarse con software malintencionado sin mi conocimiento?  
 Sí, existe software malintencionado que puede instalarse desde un sitio web a través de un programa o un script insertados en una página web. Parte del software malintencionado requiere la ayuda del usuario para instalarse. Este tipo de software usa elementos emergentes web o software gratuito que requiere que el usuario acepte un archivo descargable. Sin embargo, si mantiene Microsoft Windows® actualizado y no reduce la configuración de seguridad, puede minimizar las posibilidades de una infección.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>¿Por qué es importante revisar los contratos de licencia antes de instalar software?  
 Cuando visite sitios web, no acepte automáticamente cualquier descarga que ofrezca el sitio. Si descarga software gratuito, como programas de uso compartido de archivos o protectores de pantalla, lea detenidamente el contrato de licencia. Busque las cláusulas que indican que debe aceptar la publicidad y las ventanas emergentes de la compañía o que el software enviará cierta información al publicador del software.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>¿Qué diferencias hay entre Endpoint Protection y Windows Defender?  
 Endpoint Protection es un software antimalware, lo que significa que se ha diseñado para detectar y ayudar a proteger el equipo frente a una amplia gama de software malintencionado, que incluye virus, spyware y otro software potencialmente no deseado. Windows Defender, que se instala automáticamente con el sistema operativo Windows, es un software que detecta y detiene el spyware.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>¿Por qué Windows Defender no detecta cookies?  
 Las cookies son pequeños archivos de texto que los sitios web colocan en el equipo para almacenar información sobre el usuario y sus preferencias. Los sitios web usan las cookies para ofrecer una experiencia personalizada y recopilar información sobre el uso del sitio web. Windows Defender no detecta cookies, porque no las considera una amenaza para la privacidad del usuario o la seguridad del equipo. La mayoría de los exploradores de Internet permiten bloquear las cookies.  

##  <a name="how-can-i-prevent-malware"></a>¿Cómo puedo evitar el malware?  
 Dos de las preocupaciones más importantes para los usuarios de equipos hoy en día son los virus y el spyware. En ambos casos, aunque pueden resultar un problema, es posible defenderse de estas amenazas con bastante facilidad con tan solo un poco de planeación:  

-   Mantenga actualizado el software del equipo y acuérdese de instalar todas las revisiones. Recuerde actualizar el sistema operativo de forma regular.  

-   Asegúrese de que el software antivirus y antispyware, Windows Defender, usa las actualizaciones más recientes contra amenazas potenciales (consulte ¿Cómo mantengo las definiciones de virus y spyware actualizadas?). Además, asegúrese de usar siempre la versión más reciente de Windows Defender.  

-   Descargue solo actualizaciones de orígenes de confianza. En el caso de los sistemas operativos Windows, vaya siempre al [catálogo de Microsoft Update](https://catalog.update.microsoft.com).  Para otro software, utilice siempre los sitios web legítimos de la empresa o la persona que lo produce.

-   Si recibe un correo electrónico con archivos adjuntos y no está seguro del origen, elimínelo inmediatamente. No descargue aplicaciones ni archivos de orígenes desconocidos y tenga cuidado al intercambiar archivos con otros usuarios.  

-   Instale y use un firewall. Se recomienda que habilite Firewall de Windows.  

##  <a name="what-are-virus-and-spyware-definitions"></a>¿Qué son las definiciones de virus y spyware?  
 Si usa Windows Defender o Endpoint Protection, es importante contar con definiciones de spyware y antivirus actualizadas. Las definiciones son archivos que tienen un comportamiento similar a una enciclopedia de amenazas potenciales de software que está en continuo crecimiento. Windows Defender o Endpoint Protection usa las definiciones para determinar si el software que detecta es virus, spyware u otro software potencialmente no deseado y luego le avisa sobre los posibles riesgos. Para ayudar a mantener las definiciones actualizadas, Windows Defender o Endpoint Protection coopera con Microsoft Update con el fin de instalar automáticamente nuevas definiciones conforme se publican. También puede configurar Windows Defender o Endpoint Protection para que busque en línea las definiciones actualizadas antes de proceder al examen.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>¿Cómo mantengo las definiciones de virus y spyware actualizadas?  
 Las definiciones de virus y spyware son archivos que tienen un comportamiento similar a una enciclopedia de software malintencionado conocido, que incluye virus, spyware y otro software potencialmente no deseado. Dado que el desarrollo de software malintencionado es constante, Windows Defender o Endpoint Protection se basa en definiciones actualizadas para determinar si el software que intenta instalarse, ejecutarse o cambiar la configuración del equipo es virus, spyware u otro software potencialmente no deseado.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Para buscar nuevas definiciones automáticamente antes de los exámenes programados (recomendado)  

1.  Abra el cliente de Windows Defender o Endpoint Protection haciendo clic en el icono del área de notificación o inícielo desde el menú **Inicio** .  

2.  Haga clic en **Configuración**y luego en **Examen programado**.  

3.  Asegúrese de que esté activada la casilla **Buscar las definiciones de virus y spyware más recientes antes de ejecutar un examen programado** y luego haga clic en **Guardar cambios**. Si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o confirme la acción.  

### <a name="to-check-for-new-definitions-manually"></a>Para buscar nuevas definiciones manualmente

 Windows Defender o Endpoint Protection actualiza automáticamente las definiciones de virus y spyware en el equipo. Si no se han actualizado las definiciones durante más de siete días (por ejemplo, si no encendió el equipo durante una semana), Windows Defender o Endpoint Protection le notificarán que las definiciones están obsoletas.  

1.  Abra el cliente de Windows Defender o Endpoint Protection haciendo clic en el icono del área de notificación o inícielo desde el menú **Inicio** .  

2.  Para buscar nuevas definiciones, haga clic en la pestaña **Actualizar** y luego haga clic en **Actualizar definiciones**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>¿Cómo quito o restauro elementos puestos en cuarentena por Windows Defender o Endpoint Protection?  

 Si Windows Defender o Endpoint Protection pone un software en cuarentena, lo mueve a otra ubicación del equipo y, así, evita que se ejecute hasta que usted decida restaurarlo o quitarlo del equipo.  

 Para todos los pasos mencionados en este procedimiento, si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o confirme la acción.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Para quitar o restaurar elementos puestos en cuarentena por Windows Defender o Endpoint Protection


1.  Haga clic en la pestaña **Historial** , seleccione **Elementos en cuarentena**y luego seleccione la opción **Elementos en cuarentena** .  

2.  Haga clic en **Ver detalles** para ver todos los elementos.  

3.  Revise cada elemento y, en cada uno de ellos, haga clic en **Quitar** o en **Restaurar**. Si desea quitar todos los elementos en cuarentena del equipo, haga clic en **Quitar todo**.  

##  <a name="what-is-real-time-protection"></a>¿Qué es la protección en tiempo real?  

 La protección en tiempo real permite que Windows Defender supervise el equipo en todo momento y le avise cuando amenazas potenciales, como virus y spyware, intentan instalarse o ejecutarse en el equipo. Dado que esta característica es un elemento importante del mecanismo que usa Windows Defender para ayudar a proteger el equipo, debe asegurarse de que siempre esté siempre activada. Si se desactiva la protección en tiempo real, Windows Defender le avisa y cambia el estado del equipo a **"En riesgo"** .  

 Siempre que la protección en tiempo real detecta una amenaza real o potencial, Windows Defender muestra una notificación. Ahora puede elegir entre las siguientes opciones:  

- Haga clic en **Limpiar el equipo** para quitar el elemento detectado. Windows Defender quitará automáticamente el elemento del equipo.  

- Haga clic en el vínculo **Mostrar detalles** para mostrar la ventana de detalles de amenazas potenciales y luego elija la acción que va a aplicar al elemento detectado.  

  Puede elegir el software y la configuración que quiere que Windows Defender supervise, pero es conveniente activar la protección en tiempo real y habilitar todas sus opciones. En la siguiente tabla se explican las opciones disponibles.  

|||  
|-|-|  
|**Opción de protección en tiempo real**|**Finalidad**|  
|Examinar todas las descargas|Esta opción supervisa los archivos y los programas que se descargan, incluidos los archivos que se descargan automáticamente a través de Windows Internet Explorer y Microsoft Outlook® Express, como los controles ActiveX® y los programas de instalación de software. El propio explorador puede descargar, instalar o ejecutar estos archivos. El software malintencionado, como virus, spyware y otro software potencialmente no deseado, puede incluirse con estos archivos e instalarse sin su conocimiento.<br /><br /> Con la opción de protección en tiempo real, Windows Defender supervisa el equipo en todo momento y comprueba si existen archivos o programas malintencionados que se hayan descargado. Esta característica de supervisión significa que Windows Defender no necesita ralentizar su experiencia de navegación ni de correo electrónico requiriendo una comprobación de los archivos o programas que quiere descargar.|  
|Supervisar la actividad de archivos y programas en el equipo|Esta opción supervisa cuándo comienzan a ejecutarse archivos y programas en el equipo y luego avisa sobre las acciones que estos realizan y las acciones que se toman al respecto. Esto es importante, porque el software malintencionado puede aprovechar vulnerabilidades de los programas instalados para ejecutar software malintencionado o no deseado sin su conocimiento. Por ejemplo, el spyware puede ejecutarse en segundo plano cuando usted inicia un programa que usa con frecuencia. Windows Defender supervisa los programas y avisa si detecta actividad sospechosa.|  
|Habilitar supervisión del comportamiento|Esta opción supervisa las recopilaciones de comportamientos para detectar patrones sospechosos que podrían no detectarse mediante los métodos convencionales de detección antivirus.|  
|Habilitar Sistema de inspección de red|Esta opción ayuda a proteger el equipo frente a vulnerabilidades de seguridad conocidas de tipo día cero, lo que reduce la ventana de tiempo entre el momento en que se detecta una vulnerabilidad y se aplica una actualización.|  

### <a name="to-turn-off-real-time-protection"></a>Para desactivar la protección en tiempo real  

1.  Haga clic en **Configuración**y, a continuación, en **Protección en tiempo real**.  

2.  Desactive las opciones de protección en tiempo real que quiere desactivar y luego haga clic en **Guardar cambios**. Si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o confirme la acción.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>¿Cómo sé que se ejecuta Windows Defender o Endpoint Protection en mi equipo?  

 Después de instalar Windows Defender en el equipo, puede cerrar la ventana principal y dejar que Windows Defender se ejecute silenciosamente en segundo plano. Windows Defender seguirá ejecutándose en el equipo, lo supervisará y ayudará a protegerlo contra las amenazas.  

 Por supuesto, sabrá que Windows Defender está en ejecución siempre que este muestre mensajes de notificación en el área de notificación. Estas notificaciones avisan sobre amenazas potenciales detectadas por Windows Defender.  

 Recibirá también otras notificaciones de alerta, por ejemplo, si por alguna razón se ha desactivado la protección en tiempo real, si no ha actualizado las definiciones de virus y spyware durante varios días o cuando haya actualizaciones disponibles. Windows Defender también muestra brevemente una notificación para indicar que está examinando el equipo.  

> [!TIP]
> 
> Si no ve el icono de Windows Defender en el área de notificación, haga clic en la flecha del área de notificación para mostrar los iconos ocultos, incluido el icono de Windows Defender.  


 Su color depende del estado actual del equipo:  

-   El verde indica que el equipo está "protegido".  

-   El amarillo indica que el equipo está "potencialmente desprotegido".  

-   El rojo indica que el equipo está "en peligro".  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>¿Cómo se configuran las alertas de Windows Defender o Endpoint Protection?  
 Si Windows Defender está en ejecución en el equipo, le avisa automáticamente si detecta virus, spyware u otro software potencialmente no deseado. También puede establecer Windows Defender de modo que le avise si ejecuta software que aún no se ha examinado y puede optar por recibir una alerta si algún software realiza cambios en el equipo.  

### <a name="to-set-up-alerts"></a>Para configurar las alertas  

1.  Haga clic en **Configuración**y, a continuación, en **Protección en tiempo real**.  

2.  Asegúrese de que la casilla **Activar protección en tiempo real (recomendado)** esté activada.  

3.  Active las casillas situadas junto a las opciones de protección en tiempo real que desee ejecutar y, a continuación, haga clic en **Guardar cambios**. Si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o confirme la acción.  

### <a name="see-also"></a>Vea también  
 [Solución de problemas del cliente de Windows Defender o Endpoint Protection](troubleshoot-endpoint-client.md)   

 [Ayuda del cliente de Endpoint Protection](endpoint-protection-client-help.md)
