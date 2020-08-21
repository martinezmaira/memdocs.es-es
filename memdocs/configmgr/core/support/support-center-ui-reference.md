---
title: Referencia de la interfaz de usuario del Centro de soporte técnico
titleSuffix: Configuration Manager
description: Aprenda a usar las herramientas del Centro de soporte técnico.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 79d483f95c12c1da1e34ca556836a1f42bbffbef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699456"
---
# <a name="support-center-user-interface-reference"></a>Referencia de la interfaz de usuario del Centro de soporte técnico

*Se aplica a: Configuration Manager (rama actual)*

Este es un artículo de referencia sobre las interfaces de usuario (IU) de las herramientas del Centro de soporte técnico:
- Support Center
- Visor de registros del Centro de soporte técnico
- Visor del Centro de soporte técnico



## <a name="support-center-reference"></a>Referencia del Centro de soporte técnico

En esta sección se describe la interfaz de usuario de la herramienta **Centro de soporte técnico**. 
- [Menú Ventana](#bkmk_support-window)  
- [Pestaña Inicio](#bkmk_support-home)  
- [Pestaña Cliente](#bkmk_support-client)  
- [Pestaña Directiva](#bkmk_support-policy)  
- [Pestaña Contenido](#bkmk_support-content)  
- [Pestaña Inventario](#bkmk_support-inventory)  
- [Pestaña Solución de problemas](#bkmk_support-troubleshoot)  
- [Pestaña Registros](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a> Menú Ventana

En la esquina superior izquierda de la ventana del Centro de soporte técnico, haga clic en la flecha del cuadro azul para abrir este menú.

#### <a name="local-machine-connection"></a>Conexión del equipo local
El Centro de soporte técnico recopila archivos de registro y soluciona problemas en el cliente donde se ejecuta el Centro de soporte técnico.

#### <a name="remote-connection"></a>Conexión remota
Establece una conexión remota con otro cliente de Configuration Manager. Después de conectar, el Centro de soporte técnico recopila archivos de registro y soluciona problemas en el cliente con el que está conectado.

#### <a name="about"></a>Acerca de
Proporciona información sobre el Centro de soporte técnico.

#### <a name="options"></a>Options
En el cuadro de diálogo **Opciones** , puede:
- Reducir el movimiento de los elementos animados de la interfaz de usuario  
- Cambiar la ubicación predeterminada para guardar archivos de paquete de datos  
- Cambiar la ubicación de los archivos temporales    
- Restablecer advertencias. Los mensajes de advertencia suprimidos anteriormente aparecen de nuevo cuando se desencadena.  
- Restablecer el valor predeterminado de la ruta de acceso de archivo temporal, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Salir
Cierra el Centro de soporte técnico.



### <a name="home-tab"></a><a name="bkmk_support-home"></a> Pestaña Inicio

#### <a name="collect-selected-data"></a>Recopilar datos seleccionados
El Centro de soporte técnico recopila información del cliente de Configuration Manager. De forma predeterminada, recopila los siguientes tipos:
- Archivos de registro
- Recopilador de configuración de cliente
- Sistema operativo

Para recopilar otros tipos de información, active la casilla situada junto al nombre de ese tipo.

Seleccione la lista desplegable de la parte inferior del botón **Recopilar datos seleccionados** en la cinta y luego **Recopilar todos los datos**. Esta acción recopila el conjunto completo de datos de estado del cliente.

Mientras el Centro de soporte técnico recopila datos, haga clic en **Cancelar recopilación** para detenerlo.

#### <a name="data-types"></a>Tipos de datos
Cuando se activa la casilla de una opción, el Centro de soporte técnico recopila ese tipo de datos la siguiente vez que se selecciona **Recopilar datos seleccionados**. Los siguientes tipos están disponibles:  

- **Archivos de registro**: archivos de registro del cliente, que incluyen registros de configuración  

- **Directiva**: colección de directivas de cliente  

- **Certificados**: información de clave pública de los certificados de cliente. El Centro de soporte técnico no recopila claves privadas de certificados.  

- **Recopilador de configuración de cliente**: información del cliente de Configuration Manager. No se puede deshabilitar este tipo de datos.  

- **Registro del cliente**: recopila información de configuración del cliente del Registro. El Centro de soporte técnico solo recopila información del Registro de Configuration Manager.  

- **WMI de cliente**: información de configuración del cliente de WMI. El Centro de soporte técnico no recopila la directiva del cliente.  

- **Solución de problemas**: datos de solución de problemas en tiempo real para ayudar a diagnosticar problemas comunes de cliente relativos a Active Directory, puntos de administración, redes, asignaciones de directivas y registro.  

    > [!NOTE]  
    > Este tipo de datos no se admite cuando se realiza una conexión remota a otro cliente.  

- **Volcados de depuración**: realiza el volcado de depuración del cliente y procesos relacionados. Los volcados de depuración pueden ser de gran tamaño. Habilite esta opción solo cuando solucione problemas de rendimiento del cliente.  

    > [!WARNING]  
    > Recopilar volcados de depuración hará que los paquetes de datos sean muy voluminosos (en algunos casos, de varios cientos de MB).  
    >  
    > Los volcados de depuración pueden contener información confidencial, como contraseñas, secretos criptográficos o datos de usuario. Los volcados de depuración solo se deben recopilar por recomendación del personal de Soporte técnico de Microsoft. Los paquetes de datos que contienen volcados de depuración deben controlarse cuidadosamente para protegerlos frente al acceso no autorizado.  
    >  
    > Este tipo de datos no se admite cuando se realiza una conexión remota a otro cliente.  

- **Sistema operativo**: recopila información de configuración sobre el equipo local. Estos datos incluyen información sobre la instalación de Windows, los adaptadores de red y la configuración de servicio del sistema. No se puede deshabilitar este tipo de datos.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a> Pestaña Cliente

#### <a name="load-or-refresh"></a>Cargar o actualizar
El Centro de soporte técnico carga o actualiza los detalles del cliente de Configuration Manager.

#### <a name="control-client-agent-service"></a>Servicio de agente de cliente de control
Realiza una de las siguientes acciones en el servicio de agente cliente de Configuration Manager (ccmexec) en el cliente conectado:  

- **Reiniciar cliente**  

    > [!IMPORTANT]  
    > Si el servicio de agente cliente no se reinicia correctamente, Configuration Manager no puede administrar el cliente hasta que se inicia el servicio.  

- **Iniciar cliente**  

- **Detener cliente**  

    > [!IMPORTANT]  
    > Configuration Manager no puede administrar el cliente hasta que se inicia el servicio.  

#### <a name="properties"></a>Propiedades
Al cargar los detalles del cliente, el Centro de soporte técnico muestra las siguientes propiedades:  

- **Id. de cliente**: identificador único que Configuration Manager usa para identificar al cliente.  

- **Id. de hardware**: identificador único que Configuration Manager usa para identificar al hardware del cliente.  

- **Aprobado**: indica si el cliente se ha aprobado en Configuration Manager.  

- **Estado de registro**: indica si el cliente está registrado con Configuration Manager.  

- **Accesible desde Internet**: indica si el cliente está en Internet.  

- **Versión**: número de versión del cliente de Configuration Manager instalado.  

- **Código de sitio**: código de sitio del sitio primario al que está asignado el cliente.  

- **Punto de administración asignado**: nombre de dominio completo (FQDN) del punto de administración asignado actualmente del cliente.  

- **Punto de administración residente**: FQDN del punto de administración residente.  

- **Punto de administración de proxy**: nombre de host o FQDN del punto de administración proxy (si existe).  

- **Código de sitio de proxy**: Código de sitio del sitio secundario (si lo hay)  

- **Estado del proxy**: estado del punto de administración proxy del cliente de Configuration Manager. Por ejemplo, **Activo** o **Pendiente**.  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a> Pestaña Directiva

Use las acciones de esta pestaña en lugar de la herramienta anterior [PolicySpy](policy-spy.md).

#### <a name="load-policy"></a>Cargar directiva
Esta opción varía en función de la vista:

- **Cargar directiva real**: haga clic en **Real** en el grupo Vista y luego seleccione esta opción en el grupo Directiva. El Centro de soporte técnico carga la directiva de cliente que ha seleccionado.  

- **Cargar directiva solicitada**: haga clic en **Solicitada** en el grupo Vista y luego seleccione esta opción en el grupo Directiva. El Centro de soporte técnico carga la directiva de cliente solicitada del cliente.  

- **Cargar directiva predeterminada**: haga clic en **Predeterminada** en el grupo Vista y luego seleccione esta opción en el grupo Directiva. El Centro de soporte técnico carga la directiva predeterminada de este cliente.  

Seleccione la lista desplegable de la parte inferior de este botón para ver otras opciones:

- **Cargar o actualizar todo**: carga o actualiza la directiva real, solicitada y predeterminada a la vez.  

#### <a name="actual-view"></a>Vista real
Abre la vista de directiva real.

#### <a name="requested-view"></a>Vista solicitada
Abre la vista de directiva solicitada.

#### <a name="default-view"></a>Vista predeterminada
Abre la vista de directiva predeterminada. (Esta directiva es la que obtiene el dispositivo al instalar el cliente de Configuration Manager).

#### <a name="request-and-evaluate-policy"></a>Solicitar y evaluar directiva
El Centro de soporte técnico solicita la directiva de cliente del punto de administración y luego evalúa esa directiva en el cliente.

Seleccione la lista desplegable de la parte inferior de este botón para ver otras opciones:  

- **Solicitar directiva**: el Centro de soporte técnico solicita la directiva de cliente del punto de administración.  

- **Evaluar la directiva**: el Centro de soporte técnico evalúa la directiva de cliente en el cliente.  

- **Restablecer valores predeterminados de directiva**: el Centro de soporte técnico indica al cliente de Configuration Manager que vuelva a aplicar la directiva predeterminada. Quita todas las directivas de equipo y de usuario del cliente.  

#### <a name="listen-for-policy-events"></a>Realizar escuchas de eventos de directiva
El Centro de soporte técnico escucha los eventos de directiva. Seleccione esta opción de nuevo para deshabilitar la escucha de eventos de directiva. Para ver **eventos de directiva**, haga clic en la flecha situada en la parte inferior de esta pestaña. 

#### <a name="clear-events"></a>Borrar eventos
El Centro de soporte técnico borra cualquier evento de directiva.



### <a name="content-tab"></a><a name="bkmk_support-content"></a> Pestaña Contenido

Ve el contenido del cliente, incluido el almacenado en caché. Supervisa el progreso de las implementaciones de aplicaciones y las actualizaciones de software. 

#### <a name="load-or-refresh"></a>Cargar o actualizar
*Se aplica a las vistas Contenido y Caché*

El Centro de soporte técnico carga o actualiza la lista de contenido que hay actualmente en el cliente.

#### <a name="invoke-trigger"></a>Invocar desencadenador
Los siguientes elementos de este menú solicitan una acción de cliente relacionada con el contenido:  

- **Servicios de ubicación**  

    - **Actualizar ubicaciones de contenido**: actualiza los puntos de distribución usados por las descargas de contenido activas.  

    - **Actualizar puntos de administración**: actualiza la lista interna de puntos de administración que el cliente usa.  

    - **Agotar tiempo de espera de solicitudes de contenido**: si alguna solicitud de ubicación de contenido se ha estado ejecutando durante demasiado tiempo, esta acción detiene la solicitud.  

- **Evaluación de implementación de aplicaciones**: inicia una tarea que evalúa las aplicaciones implementadas.  

- **Evaluación de implementación de actualizaciones de software**: inicia una tarea que evalúa las actualizaciones de software implementadas.  

- **Análisis de origen de actualizaciones de software**: inicia una tarea que analiza las ubicaciones de origen de las actualizaciones.  

- **Actualización de lista de origen de Windows Installer**: inicia una tarea que actualiza la ubicación de origen de las instalaciones de Windows Installer (MSI).  

#### <a name="content-view"></a>Vista de contenido
Vea las aplicaciones, los paquetes y las actualizaciones que se han cargado en el cliente. Si selecciona una aplicación, un paquete o una actualización, puede ver detalles sobre ese contenido. En algunas aplicaciones, también puede realizar las siguientes acciones:  

- **Actualizar**: actualiza la vista de detalles.  

- **Comprobar o descargar**: comprueba que una aplicación está disponible para la descarga.  

- **Instalar**: instala la aplicación.  

- **Desinstalar**: Desinstalar la aplicación  

#### <a name="cache-view"></a>Vista Caché
Vea la configuración de la memoria caché del cliente, así como detalles sobre el contenido de la memoria caché. Cuando se conecta el Centro de soporte técnico a un cliente local, también es posible realizar las siguientes acciones:  

- Para cambiar la ubicación de la caché, haga clic en **Cambiar** junto al campo **Ubicación de caché**.  

- Para ajustar el tamaño de la caché, seleccione **Cambiar** junto al campo **Tamaño de caché**.  

- Para borrar la caché del cliente, haga clic en **Borrar** junto al campo **Caché en uso**.  

En esta vista se muestran las siguientes propiedades:  

- **Ubicación**: ubicación de cada carpeta de la caché. Haga clic en el vínculo para abrir la carpeta en el Explorador de Windows.   
- **Id. de contenido**  
- **Id. de caché**  
- **Size**  
- **Última referencia**: esta propiedad es la fecha en la que el cliente ha leído o escrito en este elemento de la caché por última vez.  

#### <a name="monitoring-view"></a>Vista de supervisión
Seleccione **Supervisar** para ver el progreso activo de las implementaciones de aplicaciones y las actualizaciones de software. Esta vista muestra los mensajes de estado generados desde la aplicación y los mensajes de WMI de eventos de actualización de software.

En esta vista se muestran las siguientes propiedades de cada evento:  

- **Hora**: hora a la que el cliente ha generado el evento.  
- **Tipo de tema**: tipo del mensaje de estado.  
- **Id. del tema**: identificador del mensaje de estado; se usa para asignarse a eventos en los archivos de registro.  
- **Tipo de id. del tema**: subtipo del mensaje de estado.  
- **Id. de estado**: resultado de la acción que se está supervisando.  
- **Detalles** y **Datos de evento**: más información sobre los mensajes de estado que se muestran en esta vista. Puede que Detalles del estado esté en blanco algunas veces.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a> Pestaña Inventario

#### <a name="load-or-refresh"></a>Cargar o actualizar
El Centro de soporte técnico carga o actualiza la lista de inventario del cliente para la vista seleccionada.

#### <a name="invoke-trigger"></a>Invocar desencadenador

> [!Note]  
> En el caso de las tareas distintas a **Ciclo de informe de medición de software**:  
> - Si la tarea se solicita cuando ya se está ejecutando otra tarea de inventario, el cliente pone la nueva tarea en cola para que se ejecute después de que se haya completado la tarea actual y otras tareas que estén en cola.  
> - Siga el progreso de la tarea en **InventoryAgent.log**.  

Los siguientes elementos de este menú solicitan una acción de cliente relacionada con el inventario:  

- **Ciclo de recopilación de datos de detección (latido)** : desencadena la tarea de cliente que sirve para recopilar información de detección de dispositivos.  

- **Ciclo de recopilación de archivos**: desencadena la tarea de cliente que sirve para recopilar archivos locales.  

- **Ciclo de inventario de hardware**: desencadena la tarea de cliente que sirve para recopilar datos de inventario de hardware.  

- **Ciclo de recopilación de IDMIF**: desencadena la tarea de cliente que sirve para recopilar datos de IDMIF.  

- **Ciclo de inventario de software**: desencadena la tarea de cliente que sirve para recopilar datos de inventario de software.  

- **Ciclo de informe de medición de software**: desencadena la tarea de cliente que sirve para elaborar un informe de medición de software y enviarlo al punto de administración. Siga el progreso de esta tarea en **SWMTRReportGen.log**.

- **Enviar mensajes de estado no enviados en cola**: desencadena la tarea de cliente para vaciar la cola de mensajes de estado.

- **Advanced**  
    - **Ciclo de inventario de hardware (resincronización completa)**  
    - **Ciclo de inventario de software (resincronización completa)**  


#### <a name="views"></a>Vistas
Si una característica no está habilitada, la vista no muestra ningún dato. 

- **Estado**: muestra los conjuntos de datos de inventario recopilados por el cliente.  

- **DDR**: información sobre los datos de detección de cliente recopilados del cliente.  

- **HINV**: información sobre los datos de inventario de hardware recopilados del cliente.  

- **SINV**: información sobre los datos de inventario de software recopilados del cliente.  

- **Colección de archivos**: información sobre los archivos recopilados del cliente.  

- **IDMIF**: información sobre los datos IDMIF y NOIDMIF recopilados del cliente.  

- **Medición**: información sobre los datos de medición de software recopilados del cliente.  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a> Pestaña Solución de problemas

Soluciona algunos de los problemas más habituales con los clientes de Configuration Manager:  
- Problemas con Active Directory  
- Redes de Windows  
- Configuration Manager   
    - Puntos de administración  
    - Asignación de directivas  
    - Registro  


> [!NOTE]  
> Esta pestaña no está disponible al conectarse a un cliente remoto de Configuration Manager.


#### <a name="start"></a>Start
Inicia la solución de problemas en el cliente.

- **Active Directory**: realiza una consulta a Active Directory para recuperar información de sitio de Configuration Manager publicada.  
- **MPCERTIFICATE**: Obtiene los certificados de los puntos de administración.  
- **MPLIST**: Obtiene una lista de los puntos de administración.  
- **MPKEYINFORMATION**: obtiene información de clave criptográfica de puntos de administración.  
- **Redes**: Soluciona problemas relacionados con las redes.  
- **Asignaciones de directiva**: Recupera las asignaciones de directiva.  
- **Registro**: comprueba que el cliente está registrado con el sitio.  

#### <a name="view-selected-log"></a>Ver registro seleccionado
Después de seleccionar una fila en la pestaña Solución de problemas, seleccione esta acción para ver el archivo de registro.

#### <a name="keep-previous-results"></a>Mantener resultados anteriores
Si ejecuta la solución de problemas en el cliente y luego quiere volver a intentarlo, elija esta opción para conservar los resultados del primer intento. De lo contrario, el Centro de soporte técnico sobrescribe archivos de registro de solución de problemas anteriores.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a> Pestaña Registros

En esta sección se enumeran los elementos de la pestaña **Registros** de la herramienta Centro de soporte técnico. 

Esta pestaña es prácticamente idéntica a la herramienta **Visor de registros**. La herramienta **Visor de registros** no incluye las características **Configurar registro de cliente** y **Grupos de registros** descritas en esta sección. La sección [Referencia del visor de registros del Centro de soporte técnico](#bkmk_log-viewer) detalla las otras opciones disponibles en esta pestaña.

#### <a name="configure-client-logging"></a>Configurar registro de cliente

Establece las siguientes opciones: 
- **Nivel de registro de cliente**: tamaño de archivo y nivel de detalle de registro.  
- **Recuento máximo de archivos**: permite más de un archivo de registro de un tipo determinado.  
- **Tamaño máximo de archivo**: tamaño en bytes de cualquier archivo de registro dado antes de que el cliente cree un registro.  

> [!NOTE]  
> Si establece estos valores en niveles demasiado bajos, es posible que el cliente no pueda registrar ninguna información útil. Si establece estos valores en niveles demasiado altos, los registros del cliente pueden usar grandes cantidades de almacenamiento.  

#### <a name="log-groups"></a>Grupos de registros

En lugar de seleccionar manualmente los archivos de registro mediante el botón **Abrir registros**, use esta lista desplegable para abrir todos los archivos de registro asociados a las siguientes áreas de características: 
- **Administración de configuración deseada**
- **Inventario**
- **Distribución de software**
- **Actualizaciones de software**
- **Administración de aplicaciones**
- **Directiva**
- **Registro de cliente**
- **Implementación de sistema operativo**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a> Referencia del visor de registros del Centro de soporte técnico

En esta sección se describe la interfaz de usuario de la herramienta **Visor de registros del Centro de soporte técnico**. 

- [Menú Ventana](#bkmk_log-window)  
- [Pestaña Inicio](#bkmk_log-home)  

La herramienta **Visor de registros** es prácticamente idéntica a la pestaña **Registros** del **Centro de soporte técnico**. La herramienta **Visor de registros** no incluye las opciones **Configurar registro de cliente** y **Grupos de registros**.


### <a name="window-menu"></a><a name="bkmk_log-window"></a> Menú Ventana

En la esquina superior izquierda de la ventana del visor de registros del Centro de soporte técnico, haga clic en la flecha del cuadro azul para abrir este menú.

#### <a name="open-logs"></a>Abrir registros
Va a la ubicación de los archivos de registro que se van a abrir. 

#### <a name="options"></a>Options
En el cuadro de diálogo **Opciones** , puede:
- Reducir el movimiento de los elementos animados de la interfaz de usuario  
- Registrar el visor de registros como aplicación predeterminada para los archivos de registro con las extensiones de archivo .log y .lo_.  
- Restablecer advertencias. Los mensajes de advertencia suprimidos anteriormente aparecen de nuevo cuando se desencadena.  

#### <a name="about"></a>Acerca de
Muestra información sobre el visor de registros del Centro de soporte técnico

#### <a name="close"></a>Cerrar
Cierra el visor de registros del Centro de soporte técnico


### <a name="home-tab"></a><a name="bkmk_log-home"></a> Pestaña Inicio

#### <a name="open-logs"></a>Abrir registros 
El Centro de soporte técnico le pide que seleccione uno o más archivos de registro para abrir.

Seleccione la lista desplegable de la parte inferior del botón **Abrir registros** de la cinta y seleccione una de las siguientes opciones adicionales: 
- **Abrir registros en la vista actual**: abre los archivos de registro seleccionados en la vista actual.  
- **Abrir registros en una ventana nueva**: abre los archivos de registro seleccionados en un ventana **Visor de registros** nueva.  

#### <a name="close-and-clear-logs"></a>Cerrar y borrar registros
Cierra los archivos de registro abiertos. Además, borra todas las entradas de archivo de registro mostradas en la ventana. El Centro de soporte técnico no muestra estas entradas en el futuro.

Seleccione la lista desplegable de la parte inferior del botón **Cerrar y borrar registros** de la cinta y seleccione una de las siguientes opciones adicionales: 
- **Borrar todas las entradas**: Borra todas las entradas de archivo de registro que se muestren en la ventana. El Centro de soporte técnico no muestra estas entradas en el futuro.  
- **Cerrar todos los registros**: Cierra los archivos de registro que haya abiertos.  

#### <a name="find"></a>Buscar
Abre el cuadro de diálogo **Buscar**. Escriba la cadena que quiera buscar. Para evitar coincidencias en cadenas cortas de otras cadenas, puede elegir la coincidencia de palabras completas. También puede elegir la coincidencia entre mayúsculas y minúsculas de la cadena.

#### <a name="find-next"></a>Buscar siguiente
Tras encontrar una coincidencia de la cadena que está buscando, esta opción le lleva a la siguiente coincidencia.

#### <a name="find-previous"></a>Buscar anterior
Tras encontrar dos o más coincidencias de la cadena que está buscando, esta opción le lleva a la coincidencia anterior.

#### <a name="options"></a>Options

- **Actualización dinámica**: supervisa los cambios de un archivo de registro abierto. Esta característica no funciona si hay varios archivos de registro abiertos. Esta opción está habilitada de forma predeterminada.  

- **Desplazamiento automático**: si también ha elegido la opción **Actualización dinámica**, esta opción desplaza de forma automática la vista del registro para mostrar las entradas recién agregadas. Esta característica no funciona si hay varios archivos de registro abiertos. Esta opción está habilitada de forma predeterminada.  

- **Mostrar detalles**: si selecciona un mensaje de archivo de registro, en la parte inferior de la pestaña **Registros** se muestran los detalles del mensaje de archivo de registro. Esta opción está habilitada de forma predeterminada.  

- **Filtro rápido**: filtra los mensajes de archivo de registro en todos los archivos de registro abiertos para encontrar una cadena específica. Puede filtrar por un texto de registro, por un nombre de componente o por un identificador de subproceso. Para buscar mensajes de registro similares, haga clic con el botón derecho en un mensaje de registro y seleccione **Filtro rápido** en el texto del registro.  

- **Ajustar texto de registro**: ajusta mensajes largos y de varias líneas para que quepan en una sola columna. Este comportamiento facilita la lectura de estos mensajes. Esta opción está habilitada de forma predeterminada.  

- **Visualización de la entrada de registro sin procesar**: muestra líneas de registro sin procesar.  

- **Filtros avanzados**: abre el cuadro de diálogo **Filtros avanzados**. Para obtener más información, vea [Filtros de archivos de registro avanzados](#bkmk_adv-filters).  

- **Vínculos de código de error**: los códigos de error del texto del registro aparecen resaltados y se puede hacer clic en ellos. Esta opción está habilitada de forma predeterminada.  

#### <a name="error-lookup"></a>Búsqueda de errores
Escriba un código de error para buscar ese código de error en los archivos de registro abiertos. Use los siguientes formatos de código de error:
- **Entero de 32 bits (con signo)** : por ejemplo, `-2147024891`  
- **Entero de 32 bits (sin signo)** : por ejemplo, `2147942405`  
- **Hexadecimal de 32 bits**: por ejemplo, `0x80070005`  

#### <a name="decode-certificate"></a>Descodificar certificado
En el cuadro de diálogo **Descodificar certificado**, pegue el valor de certificado serializado de cualquier certificado del cliente. Busque este valor en el Registro, en archivos de registro o en WMI. Seleccione **Proceso** para ver información general y detalles sobre el certificado. Esta información incluye su ruta de certificación. Haga clic en **Exportar** para exportar el certificado como un archivo **.cer**.



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a> Filtros de archivos de registro avanzados

Los filtros de archivos de registro avanzados permiten incluir, excluir o resaltar cadenas concretas. Estas cadenas pueden aparecer en un archivo de registro o grupo de archivos de registro al mirar entradas de archivos de registro. Use búsquedas con caracteres comodín al crear un filtro. Cuando tenga una combinación útil de filtros, guárdelos como un *conjunto de filtros*. 

Los filtros de archivos de registro avanzados sustituyen a los filtros rápidos. Use ambos conjuntamente, aunque los filtros rápidos solo se aplican a los datos de registro mostrados. Los filtros avanzados determinan qué datos se muestran inicialmente antes de aplicarles ningún filtro rápido.

En el cuadro de diálogo Filtros avanzados, puede crear conjuntos de filtros complejos. Estos conjuntos de filtros buscan cadenas en muchos componentes de archivos de registro. Estos componentes incluyen mensajes, subprocesos, niveles de registro y componentes. Un conjunto de filtros contiene varias instrucciones de filtro que sirven para incluir, excluir o resaltar mensajes de archivo de registro. Un filtro define una columna de archivo de registro en la que buscar, un operador y un valor. El valor puede contener expresiones regulares, como el *carácter comodín*`*`.


### <a name="add-a-filter"></a>Agregar un filtro

1. En la ventana **Visor de registros**, o en la pestaña **Registros** del Centro de Soporte técnico, seleccione **Filtros avanzados**.  

2. En el cuadro de diálogo Filtros avanzados, haga clic en **Agregar**. Luego seleccione una de las siguientes opciones para actuar sobre las entradas de registro que coincidan con el filtro:  
    - **Incluir**  
    - **Excluir**  
    - **Resaltar**  

3. En el cuadro de diálogo **Configuración de filtro avanzado**, elija una columna y un operador:  

    - **Columna**: elija dónde buscar cadenas que coincidan con el filtro:  

         - **Texto de registro**: busca en el texto de un archivo de registro.  

         - **Gravedad del registro**: busca registros con un nivel de gravedad específico. Establezca estos niveles de gravedad en el campo **Valor**.  

         - **Componente**: busca un componente específico por nombre.  

         - **Id. de subproceso**: busca mensajes de registro con un identificador de subproceso concreto.  

         - **Archivo de origen**: busca mensajes de registro que aparezcan en un archivo de registro específico.  

    - **Operador**: elija un operador para el filtro.  

4. Escriba un valor por el que filtrar en el campo **Valor**. Si el valor contiene expresiones regulares, seleccione **Habilitar coincidencia de expresiones regulares**.  


### <a name="manage-filter-sets"></a>Administrar conjuntos de filtros

- Para editar un filtro, selecciónelo y luego haga clic en **Editar**.  

- Para eliminar un filtro, selecciónelo y luego haga clic en **Eliminar**.  

- Para borrar todos los filtros, haga clic en **Borrar**.  

- Para guardar el conjunto de filtros actual, haga clic en **Guardar filtros**. Luego guarde el conjunto de filtros como un archivo **.filterset**.  

- Para cargar un conjunto de filtros guardado, haga clic en **Cargar filtros**. Luego vaya a un archivo **.filterset** guardado previamente.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a> Referencia del Visor del Centro de soporte técnico

En esta sección se describe la interfaz de usuario (UI) de la herramienta **Visor del Centro de soporte técnico** de Configuration Manager. Las pestañas disponibles varían según el contenido del paquete de solución de problemas. El [menú Ventana](#bkmk_viewer-window) y la [pestaña Inicio](#bkmk_viewer-home) aparecen de forma predeterminada.
- [Menú Ventana](#bkmk_viewer-window)
- [Pestaña Inicio](#bkmk_viewer-home)
- [Pestaña Configuración](#bkmk_viewer-config)
- [Pestaña Registros](#bkmk_viewer-logs)
- [Pestaña Volcados de depuración](#bkmk_viewer-debug)
- [Pestaña WMI](#bkmk_viewer-wmi)
- [Pestaña Registro](#bkmk_viewer-registry)
- [Pestaña Directiva](#bkmk_viewer-policy)
- [Pestaña Certificados](#bkmk_viewer-certs)
- [Pestaña Solución de problemas](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a> Menú Ventana

En la esquina superior izquierda de la ventana del Visor del Centro de soporte técnico, haga clic en la flecha del cuadro azul para abrir este menú.

#### <a name="open-bundle"></a>Abrir paquete
Va a la ubicación de un paquete de datos creado por el Centro de soporte técnico.

#### <a name="about"></a>Acerca de
Muestra información sobre el Visor del Centro de soporte técnico.

#### <a name="options"></a>Options
En el cuadro de diálogo **Opciones** , puede:
- Reducir el movimiento de los elementos animados de la interfaz de usuario  
- Cambiar la ubicación de los archivos temporales    
- Restablecer advertencias. Los mensajes de advertencia suprimidos anteriormente aparecen de nuevo cuando se desencadena.  
- Restablecer el valor predeterminado de la ruta de acceso de archivo temporal, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Salir
Se sale del Visor del Centro de soporte técnico.


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a> Pestaña Inicio

#### <a name="open-bundle"></a>Abrir paquete
Va a la ubicación de un paquete de datos creado por el Centro de soporte técnico.

#### <a name="open-log-file"></a>Abrir archivo de registro
Selecciona uno o más archivos de registro para abrirlos.

#### <a name="decode-certificate"></a>Descodificar certificado
En el cuadro de diálogo **Descodificar certificado**, pegue el valor de certificado serializado de cualquier certificado del cliente. Busque este valor en el Registro, en archivos de registro o en WMI. Seleccione **Proceso** para ver información general y detalles sobre el certificado. Esta información incluye su ruta de certificación. Haga clic en **Exportar** para exportar el certificado como un archivo **.cer**.


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a> Pestaña Configuración

La pestaña **Configuración** de la herramienta Visor del Centro de soporte técnico proporciona las siguientes vistas, usando para ello los datos recuperados de los proveedores de WMI:

#### <a name="client"></a>Cliente
En esta vista se muestra la misma información que en la pestaña **Cliente** del Centro de soporte técnico.

#### <a name="operating-system"></a>Sistema operativo
Detalles sobre el sistema operativo del cliente. Usa la clase [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="computer"></a>Equipo
Detalles sobre el equipo cliente. Usa la clase [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="services"></a>Servicios
Detalles sobre los servicios que se ejecutan en el equipo cliente. Usa la clase [Win32_Service](/windows/desktop/CIMWin32Prov/win32-service).

#### <a name="network-adapters"></a>Adaptadores de red
Detalles sobre los adaptadores de red instalados en el equipo cliente. Usa la clase [Win32_NetworkAdapterConfiguration](/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration).


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a> Pestaña Registros

La pestaña **Registros** muestra una lista de los archivos de registro incluidos en el paquete. Cada fila de esta pestaña proporciona la ruta de acceso, el nombre y el tamaño del archivo de registro. 

#### <a name="open"></a>Abrir
Después de seleccionar un archivo de registro, haga clic en este botón para abrir el **Visor de registros**. Proporciona un subconjunto de la funcionalidad observada en la pestaña Registros del Centro de soporte técnico.

#### <a name="decode-certificate"></a>Descodificar certificado
En el cuadro de diálogo **Descodificar certificado**, pegue el valor de certificado serializado de cualquier certificado del cliente. Busque este valor en el Registro, en archivos de registro o en WMI. Seleccione **Proceso** para ver información general y detalles sobre el certificado. Esta información incluye su ruta de certificación. Haga clic en **Exportar** para exportar el certificado como un archivo **.cer**.


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a> Pestaña Volcados de depuración

Cada fila de esta pestaña proporciona detalles de los archivos de volcado de depuración que hay disponibles para exportar. Use esta pestaña para exportar archivos de volcado de depuración (.dmp) para un análisis más detallado. Este análisis emplea una herramienta de depuración como WinDbg. 

> [!WARNING]  
> Los volcados de depuración pueden contener información confidencial, como contraseñas, secretos criptográficos o datos de usuario. Recopile volcados de depuración únicamente por recomendación del personal de Soporte técnico de Microsoft. Los paquetes de datos que contienen volcados de depuración deben controlarse cuidadosamente para protegerlos frente al acceso no autorizado.  

#### <a name="export"></a>Exportar
Guarda una copia del archivo de volcado de depuración seleccionado.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a> Pestaña WMI

En esta pestaña se muestra el conjunto de datos WMI del cliente de Configuration Manager incluido en el paquete de datos. 

#### <a name="find"></a>Buscar
Abre el cuadro de diálogo Buscar, que tiene las siguientes características:  

- **Buscar**: escriba una cadena que quiera buscar en el conjunto de datos WMI. Admite caracteres comodín.  

- **Buscar en**: elija si quiere buscar en el conjunto de datos WMI una coincidencia de **nombre de instancia o clase**, **propiedad** o **valor**.  

- **Solo cadenas completas**: de forma predeterminada, el cuadro de diálogo Buscar busca cadenas que contengan la cadena que se está buscando. Active esta casilla para buscar únicamente las cadenas que sean exactamente iguales que la cadena que haya especificado.  

#### <a name="find-next"></a>Buscar siguiente
Este botón abre la siguiente instancia de la cadena que haya especificado en el cuadro de diálogo Buscar en el conjunto de datos WMI.

#### <a name="decode-certificate"></a>Descodificar certificado
En el cuadro de diálogo **Descodificar certificado**, pegue el valor de certificado serializado de cualquier certificado del cliente. Busque este valor en el Registro, en archivos de registro o en WMI. Seleccione **Proceso** para ver información general y detalles sobre el certificado. Esta información incluye su ruta de certificación. Haga clic en **Exportar** para exportar el certificado como un archivo **.cer**.


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a> Pestaña Registro

Use la pestaña **Registro** para ver los datos del Registro incluidos en el paquete de datos y para exportar esos datos para un análisis más profundo.

#### <a name="export"></a>Exportar
Guarda una copia de la clave y subclaves del Registro que seleccione como archivo de Registro (.reg).

#### <a name="find"></a>Buscar
Abre el cuadro de diálogo Buscar, que tiene las siguientes características:  

- **Buscar**: escriba una cadena que quiera buscar en el conjunto de datos WMI. Admite caracteres comodín.  

- **Buscar en**: elija si quiere buscar en el conjunto de datos WMI una coincidencia de **nombre de instancia o clase**, **propiedad** o **valor**.  

- **Solo cadenas completas**: de forma predeterminada, el cuadro de diálogo Buscar busca cadenas que contengan la cadena que se está buscando. Active esta casilla para buscar únicamente las cadenas que sean exactamente iguales que la cadena que haya especificado.  

#### <a name="find-next"></a>Buscar siguiente
Este botón abre la siguiente instancia de la cadena que haya especificado en el cuadro de diálogo Buscar en el conjunto de datos WMI.

#### <a name="decode-certificate"></a>Descodificar certificado
En el cuadro de diálogo **Descodificar certificado**, pegue el valor de certificado serializado de cualquier certificado del cliente. Busque este valor en el Registro, en archivos de registro o en WMI. Seleccione **Proceso** para ver información general y detalles sobre el certificado. Esta información incluye su ruta de certificación. Haga clic en **Exportar** para exportar el certificado como un archivo **.cer**.


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a> Pestaña Directiva

La pestaña **Directiva** sirve para ver los datos de directiva incluidos en el paquete de datos. 

#### <a name="find"></a>Buscar
Abre el cuadro de diálogo Buscar, que tiene las siguientes características:  

- **Buscar**: escriba una cadena que quiera buscar en el conjunto de datos WMI. Admite caracteres comodín.  

- **Buscar en**: elija si quiere buscar en el conjunto de datos WMI una coincidencia de **nombre de instancia o clase**, **propiedad** o **valor**.  

- **Solo cadenas completas**: de forma predeterminada, el cuadro de diálogo Buscar busca cadenas que contengan la cadena que se está buscando. Active esta casilla para buscar únicamente las cadenas que sean exactamente iguales que la cadena que haya especificado.  

#### <a name="find-next"></a>Buscar siguiente
Este botón abre la siguiente instancia de la cadena que haya especificado en el cuadro de diálogo Buscar en el conjunto de datos WMI.

#### <a name="decode-certificate"></a>Descodificar certificado
En el cuadro de diálogo **Descodificar certificado**, pegue el valor de certificado serializado de cualquier certificado del cliente. Busque este valor en el Registro, en archivos de registro o en WMI. Seleccione **Proceso** para ver información general y detalles sobre el certificado. Esta información incluye su ruta de certificación. Haga clic en **Exportar** para exportar el certificado como un archivo **.cer**.


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a> Pestaña Certificados

La pestaña **Certificados** sirve para ver los certificados incluidos en el paquete de datos y exportarlos.

#### <a name="view-certificate"></a>Ver certificado
Muestra información sobre un certificado seleccionado.

#### <a name="export"></a>Exportar
Abre un cuadro de diálogo **Guardar como** para guardar una copia del certificado seleccionado.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a> Pestaña Solución de problemas

Use la pestaña **Solución de problemas** para ver los archivos de registro creados mediante la pestaña Solución de problemas del Centro de soporte técnico.

#### <a name="view-log"></a>Ver registro
Después de seleccionar una fila en la pestaña **Solución de problemas**, seleccione esta opción para ver el archivo de registro con el visor de registros.