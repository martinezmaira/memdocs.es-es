---
title: Novedades de la versión 1606
titleSuffix: Configuration Manager
description: Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1606 de Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4298a6a66d60d79d05f8b5cdc9ff8caa0e7f4426
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074034"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Novedades de la versión 1606 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1606 de Configuration Manager está disponible como una actualización en consola para sitios instalados previamente que ejecutan las versiones 1511 o 1602. La versión 1511 es la versión de línea base inicial que se usa para instalar sitios nuevos de Configuration Manager.
> [!TIP]  
> Más información acerca de:  
>   
> - [Instalación de nuevos sitios](../../servers/deploy/install/prepare-to-install-sites.md) (con una versión de línea base como 1511)  
> - [Instalación de actualizaciones en los sitios](../../servers/manage/updates.md) (como la actualización 1602 o 1606)  

 En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1606 de Configuration Manager.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Actualizaciones y mantenimiento

### <a name="changes-for-the-updates-and-servicing-node"></a>Cambios en el nodo Actualizaciones y mantenimiento
A continuación se muestran los cambios en el nodo Actualizaciones y mantenimiento de la consola de Configuration Manager:
> [!NOTE]
> Estos cambios no estarán disponibles hasta después de instalar la versión 1606.

- **Cambio de nombre de nodo:**

    En el área de trabajo **Supervisión**, el nombre del nodo **Estado de mantenimiento del sitio** ha cambiado a **Actualizaciones y estado de mantenimiento**.
- **Más información del estado de instalación:**

    Al ver el estado de instalación de actualización de un sitio, ahora la consola muestra detalles independientes para las siguientes acciones:
    - **Descargar** (se aplica únicamente al sitio de nivel superior en el que está instalado el rol de sistema de sitio del punto de conexión de servicio).
    - **replicación**
    - **Comprobación de requisitos previos**
    - **Instalación**

  Además, ahora hay información más detallada para cada paso, incluso en qué archivo de registro puede ver más información.  
-   **Nueva opción para omitir errores de requisitos previos:**

    En las áreas de trabajo **Administración** y **Supervisión**, el nodo **Actualizaciones y mantenimiento** incluye un nuevo botón en la cinta de opciones denominado **Omitir advertencias de requisitos previos**.

    Cuando instale actualizaciones sin usar la opción Omitir advertencias de requisitos previos (desde el Asistente para actualizaciones) y esa instalación de actualización se detenga debido a una advertencia, puede seleccionar **Omitir advertencias de requisitos previos** en la cinta de opciones. Esto desencadena una continuación automática de la instalación de actualización.  



- **Vista más clara de las actualizaciones:**

    En el nodo **Actualizaciones y mantenimiento**, ahora verá solo la actualización instalada más reciente y las nuevas actualizaciones disponibles para instalar. Para ver actualizaciones instaladas previamente, haga clic en el nuevo botón **Historial** que aparece en la cinta de opciones.  

-   **Cambio de nombre de la opción de preproducción:**

    En el nodo **Actualizaciones y mantenimiento**, el botón **Opciones de cliente** ahora se denomina **Promover el cliente de preproducción**.


###  <a name="pre-release-features"></a>Características de la versión preliminar
A partir de la versión 1606, debe dar su consentimiento para usar características de la versión preliminar de Configuration Manager antes de poder seleccionarlas y permitir su uso. Para más información, consulte [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).

### <a name="new-distribution-point-update-behavior"></a>Nuevo comportamiento de actualización del punto de distribución
La actualización 1606 presenta cambios que mejoran la disponibilidad de los puntos de distribución al instalar las actualizaciones futuras.

Una vez instalada la actualización 1606, al instalar a continuación una actualización en el sitio que requiere la reinstalación automática de los roles de sistema de sitio del punto de distribución de extracción y estándar, ya no se desconectan todos los puntos de distribución para actualizarse al mismo tiempo. En su lugar, el servidor de sitio usa la configuración de distribución de contenido del sitio para distribuir la actualización a un subconjunto de puntos de distribución en un momento determinado. El resultado es que solo algunos puntos de distribución se desconectan para instalar la actualización. Esto permite a los puntos de distribución que todavía no han comenzado a actualizarse o que han completado la actualización que permanezcan en línea y puedan proporcionar contenido a los clientes.



## <a name="accessibility"></a><a name="accessibility"></a> Accesibilidad
Para navegar entre los distintos nodos de un área de trabajo, ahora puede escribir la primera letra del nombre de un nodo. Cada presión de tecla mueve el cursor al siguiente nodo que comience con esa letra. Para los usuarios que tengan un lector de pantalla, el lector lee el nombre de ese nodo. Para más información sobre las opciones de accesibilidad, vea [Características de accesibilidad](../../../core/understand/accessibility-features.md).

## <a name="administration"></a><a name="administration"></a> Administración
A continuación se presentan cambios en la administración de la consola de Configuration Manager:
### <a name="oms-connector"></a>Conector de OMS

Ahora puede conectar Configuration Manager como recopilaciones de Configuration Manager a [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/). De este modo, los datos (como colecciones) de la implementación de Configuration Manager estarán visibles en OMS. Para obtener más información, vea [Sincronizar datos de Configuration Manager con Microsoft Operations Management Suite aquí](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

El conector de OMS es una característica de la versión preliminar. Para habilitarla, consulte [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).

### <a name="support-for-cache-size-in-client-settings"></a>Configuración del tamaño de la memoria caché en Configuración de cliente

Ahora puede configurar el tamaño de la carpeta de la memoria caché en los equipos cliente con **Configuración de cliente** en la consola de Configuration Manager. Anteriormente, solo podía establecer el tamaño de la caché de cliente al instalar o reinstalar el software de cliente. Ahora puede especificar el tamaño de la memoria caché como un valor del cliente (predeterminado o personalizado) y, después, hacer que ese valor se aplique con la siguiente actualización de directiva en el cliente, sin necesidad reinstalarlo. Para obtener más información, vea [Configurar la caché del cliente para clientes de Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Administración local de dispositivos móviles

### <a name="support-for-multiple-device-management-points"></a>Varios puntos de administración de dispositivos

La administración local de dispositivos móviles (MDM) admite una nueva función de Windows 10 Anniversary Update que configura automáticamente un dispositivo inscrito para que tenga más de un punto de administración de dispositivos disponible. Esta función permite al dispositivo retroceder a otro punto de administración de dispositivos cuando el que usa normalmente no está disponible. Esta capacidad solo funciona con equipos y dispositivos que tienen instalado Windows 10 Anniversary Update.


## <a name="application-management"></a>Administración de aplicaciones

### <a name="manage-apps-from-the-windows-store-for-business"></a>Administración de aplicaciones adquiridas en la Tienda Windows para empresas

La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y adquirir aplicaciones de Windows para su organización, individualmente o por volumen. Al conectar el almacén a Configuration Manager, puede sincronizar la lista de aplicaciones que haya adquirido con Configuration Manager, verlas en la consola de Configuration Manager e implementarlas como lo haría con cualquier otra aplicación.

Para más información, vea [Administración de aplicaciones desde la Tienda Windows para empresas con Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Administración de aplicaciones iOS adquiridas por volumen

Se ha mejorado el flujo de trabajo para administrar las aplicaciones iOS adquiridas por volumen e implementarlas con Configuration Manager.


### <a name="software-center-user-interface"></a>Interfaz de usuario del Centro de software

La interfaz de usuario del Centro de software se ha simplificado para facilitar la detección.
*  Las pestañas **Estado de la instalación** y **Software instalado** se han combinado en una única pestaña llamada **Estado de la instalación**.
*  Las **actualizaciones**, los **sistemas operativos** y las **aplicaciones** se han dividido en tres pestañas independientes.
* Ahora se pueden seleccionar varias actualizaciones para su instalación a la vez, o se pueden instalar todas las actualizaciones a la vez haciendo clic en **Instalar todo**.

### <a name="content-status-links"></a>Vínculos de estado del contenido
En las propiedades de una aplicación o paquete, ahora hay un vínculo que le llevará al estado de ese objeto.

## <a name="software-updates"></a>Actualizaciones de software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Configuración de cliente para administrar el agente cliente de Office 365
Ahora puede utilizar una configuración del cliente de Configuration Manager para administrar el agente cliente de Office 365. Después de configurar esta opción e implementar las actualizaciones de Office 365, el agente cliente de Configuration Manager se comunica con el de Office 365 para descargar e instalar las actualizaciones de Office 365 desde un punto de distribución.

Para obtener más información, consulte [Administración de actualizaciones ProPlus de Office 365 con Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Cambio manual de clientes a un nuevo punto de actualización de software
Ahora puede habilitar una opción que permite a los clientes de Configuration Manager cambiar a un nuevo punto de actualización de software cuando hay problemas con el punto de actualización de software activo. Una vez habilitada, los clientes buscarán otro punto de actualización de software en el siguiente examen.

Para obtener más información, consulte [Planeación de actualizaciones de software en Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opciones de reinicio para clientes de Windows 10 después de la instalación de las actualizaciones de software
Cuando se implementa y se instala en un equipo una actualización de software que requiere un reinicio con Configuration Manager, se programa un reinicio pendiente. También se muestra un cuadro de diálogo de reinicio. A partir de la versión 1606 de Configuration Manager, las opciones **Actualizar y reiniciar** y **Actualizar y apagar** están disponibles siempre que haya un reinicio pendiente para una actualización de software de Configuration Manager. Están disponibles en las opciones de energía de Windows de equipos de Windows 10. Después de usar una de estas opciones, tras reiniciar el equipo, no se mostrará el cuadro de diálogo de reinicio.

Para más información, vea [Planeación de actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Ejecutar un examen de cumplimiento de actualizaciones de software inmediatamente después de que un cliente instale actualizaciones de software y reinicie
Ahora puede ejecutar un examen de cumplimiento inmediatamente después de que un cliente instale actualizaciones de software y reinicie. Para configurar esta opción en una implementación, en la página **Experiencia del usuario** del Asistente para implementar actualizaciones de software, seleccione **Si alguna actualización de esta implementación requiere un reinicio del sistema, ejecute el ciclo de evaluación de implementación de actualizaciones tras el reinicio**. Esto permite al cliente comprobar las actualizaciones de software adicionales que entran en vigor después de que el cliente reinicie y, después, instalarlas (para cumplir así los requisitos) durante la misma ventana de mantenimiento. Para obtener más información, vea [Implementar actualizaciones de software automáticamente](../../../sum/deploy-use/automatically-deploy-software-updates.md) o [Implementar actualizaciones de software manualmente](../../../sum/deploy-use/manually-deploy-software-updates.md).

## <a name="operating-system-deployment"></a>Implementación de sistema operativo

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Mejoras en el paso de secuencia de tareas: Instalar actualizaciones de software
Una nueva configuración, **Evaluar actualizaciones de software desde los resultados de análisis en caché**, le ofrece la opción de realizar un examen completo de actualizaciones de software, en lugar de usar los resultados del análisis almacenado en caché. Para obtener más información, consulte [Task sequence steps (Pasos de la secuencia de tareas)](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Además, está disponible una nueva variable de secuencia de tareas, **SMSTSSoftwareUpdateScanTimeout**. Esta variable le permite controlar el tiempo de espera para la detección de actualizaciones de software durante el paso de la secuencia de tareas Instalar actualizaciones de software. El valor predeterminado es 30 minutos. Para más información, vea [Variables integradas de secuencia de tareas](../../../osd/understand/task-sequence-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>La variable de secuencia de tareas OSDPreserveDriveLetter ha dejado de usarse.
La variable de secuencia de tareas OSDPreserveDriveLetter está en desuso. A partir de la versión 1606 de Configuration Manager, el programa de instalación de Windows determina de forma predeterminada la mejor letra de unidad para usar (normalmente C:) durante la implementación de un sistema operativo.

Para más información, vea [Variables integradas de secuencia de tareas](../../../osd/understand/task-sequence-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalización del tamaño de la ventana de TFTP de RamDisk para los puntos de distribución habilitados con PXE
Ahora puede personalizar el tamaño de ventana de RamDisk para los puntos de distribución habilitados con PXE. Si ha personalizado su red podría provocar que se produjera un error de tiempo de espera en la descarga de la imagen de arranque porque el tamaño de la ventana es demasiado grande. La personalización del tamaño de la ventana del Protocolo trivial de transferencia de archivos (TFTP) de RamDisk le permite optimizar el tráfico de TFTP cuando está usando PXE para cumplir los requisitos de red específicos.

Para más información, vea [Preparación de los roles de sistema de sitio para la implementación de sistemas operativos con Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Configuración de cumplimiento

### <a name="smart-lock-setting-for-android-devices"></a>Configuración de Smart Lock para dispositivos Android
Se ha agregado una nueva opción de configuración, **Permitir Smart Lock y otros agentes de confianza**, al elemento de configuración de Android y Samsung KNOX Standard.

Esta opción le permite controlar la característica Smart Lock en dispositivos Android compatibles. Esta función del teléfono, conocida en ocasiones como "agentes de confianza", le permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo si el dispositivo está en una ubicación de confianza. Por ejemplo, una ubicación de confianza puede ser cuando se conecta a un dispositivo Bluetooth específico o cuando está cerca de una etiqueta NFC. Puede usar esta opción para impedir que los usuarios configuren Smart Lock.


## <a name="device-configuration-and-protection"></a>Configuración y protección de dispositivos

### <a name="product-name-changes"></a>Cambio de nombre de producto

* Microsoft Passport for Work ahora se conoce como **Windows Hello para empresas**.
* La protección de datos empresariales ahora se conoce como **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implementación de Windows Hello para empresas (Passport for Work)

Ahora puede implementar directivas de Windows Hello para empresas para dispositivos de Windows 10 unidos a dominio administrados por el cliente de Configuration Manager.

La consola de Configuration Manager se ha actualizado para reflejar estos cambios.

### <a name="ios-activation-lock"></a>Bloqueo de activación de iOS
Configuration Manager puede ayudarle a administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en iOS 7.1 y en dispositivos más modernos. Cuando el bloqueo de activación está habilitado, es necesario escribir el identificador y la contraseña de Apple del usuario antes de que se pueda:
* Desactivar Buscar mi iPhone.
* Borrar el dispositivo.
* Reactivar el dispositivo.

Configuration Manager puede ayudarle a administrar el bloqueo de activación de dos formas:

- Habilitando el bloqueo de activación en los dispositivos supervisados.
- Omitiendo el bloqueo de activación en los dispositivos supervisados.


### <a name="microsoft-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Microsoft Defender

Endpoint Protection puede ayudar a administrar y supervisar Protección contra amenazas avanzada (ATP) de Microsoft Defender. Protección contra amenazas avanzada de Microsoft Defender es un nuevo servicio que ayuda a las empresas a detectar ataques avanzados en sus redes, a investigarlos y a responder a ellos. Las directivas de Configuration Manager pueden ayudarle a incorporar y supervisar equipos administrados que ejecutan Windows 10, versión 1607 (compilación 14328) o posterior.

Para más información, consulte [Protección contra amenazas avanzada (ATP) de Microsoft Defender](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorías de dispositivos
Puede crear categorías de dispositivos, que se pueden usar para colocar automáticamente los dispositivos en recopilaciones de dispositivos cuando usa Configuration Manager con Microsoft Intune. Después, cuando los usuarios inscriben un dispositivo en Intune, tienen que elegir una categoría de dispositivos. Además, puede cambiar la categoría de un dispositivo desde la consola de Configuration Manager.

Para más información, vea [Clasificación automática de dispositivos en recopilaciones con Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Declaración previa de dispositivos con números de serie iOS o IMEI

Puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI) o los números de serie de iOS. Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o puede escribir la información de los dispositivos de manera manual. La información importada establece la propiedad de los dispositivos que se inscriban como "Corporativos" en las listas de dispositivos. Se sigue necesitando una licencia de Intune para cada usuario que acceda al servicio.

### <a name="on-premises-health-attestation-service-communication"></a>Comunicación del servicio de Atestación de estado local

Ahora puede habilitar la supervisión de servicios de Atestación de estado para equipos con Windows 10 usando solo infraestructura local, de manera que los equipos sin acceso a Internet puedan notificar la Atestación de estado de dispositivo (DHA).

Para más información, vea [Atestación de estado para Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Control remoto
Permita a los usuarios que acepten o rechacen las transferencias de archivos antes de transferir el contenido desde el portapapeles compartido en una sesión de control remoto. Los usuarios solo necesitan conceder permisos una vez por sesión, y el espectador no puede concederse permiso a sí mismo para continuar con la transferencia de archivos. Puede encontrar esta nueva configuración en el área de trabajo **Administración**. Vaya a **Configuración de cliente** y, después, en **Configuración predeterminada**, abra el panel **Herramientas remotas**.
