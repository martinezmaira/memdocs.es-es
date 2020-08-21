---
title: Preparar los roles de sistema de sitio para la implementación de SO
titleSuffix: Configuration Manager
description: Configure los roles de sistema de sitio antes de implementar sistemas operativos en Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d9331ce452e40944e4a9b363773d254a32f2c58
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697490"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Preparar los roles de sistema de sitio para las implementaciones de sistema operativo con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para implementar sistemas operativos en Configuration Manager, primero prepare los siguientes roles de sistema de sitio que requieren configuraciones y consideraciones específicas.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Puntos de distribución  

El rol de sistema de sitio de punto de distribución hospeda archivos de origen para que los clientes los descarguen. Este contenido es para las aplicaciones, actualizaciones de software, imágenes de SO, imágenes de arranque y paquetes de controladores. Puede controlar la distribución del contenido mediante las opciones de ancho de banda, limitación y programación.  

Es importante disponer de suficientes puntos de distribución para admitir la implementación de sistemas operativos en los equipos. También es importante planear la ubicación de estos puntos de distribución en la jerarquía. Para obtener más información, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido). En este artículo se incluyen algunas consideraciones adicionales de planeación para puntos de distribución específicos de la implementación de SO.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> Consideraciones de planeación adicionales para puntos de distribución  

Los elementos siguientes son aspectos de planeación adicionales que se deben tener en cuenta para los puntos de distribución:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>¿Cómo puedo impedir las implementaciones de SO no deseadas?  
Configuration Manager no distingue los servidores de sitio de otros equipos de destino en una recopilación. Si se implementa una secuencia de tareas requerida en una recopilación que incluye un servidor de sitio, este ejecuta la secuencia de tareas de la misma manera que otros equipos de la recopilación. Asegúrese de que la implementación de SO use una recopilación que incluya los clientes previstos.  

Administre el comportamiento de las implementaciones de secuencias de tareas de alto riesgo. Una implementación de alto riesgo es una implementación que se instala automáticamente en un cliente y puede provocar resultados no deseados. Por ejemplo, una secuencia de tareas con el propósito Requerido que implementa un sistema operativo. Para reducir el riesgo de una implementación de alto riesgo no deseada, configure opciones de comprobación de la implementación. Para obtener más información, consulte [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>¿Cuántos equipos pueden recibir una imagen de SO al mismo tiempo desde un único punto de distribución?  
Para determinar cuántos puntos de distribución se necesitan, tenga en cuenta las variables siguientes:  
- La velocidad de procesamiento del punto de distribución.
- La velocidad de disco del punto de distribución.
- El ancho de banda disponible en la red.
- El tamaño del paquete de imagen.   
  
Por ejemplo, si no se tienen en cuenta otros factores de recursos del servidor, el número máximo de equipos que pueden procesar un paquete de imágenes de 4 GB en una hora en una red Ethernet de 100 megabits por segundo es de 11 equipos.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Si tiene que implementar un SO en un número específico de equipos en un intervalo de tiempo determinado, distribuya la imagen en un número adecuado de puntos de distribución.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>¿Puedo implementar un SO en un punto de distribución?  
Puede implementar un SO en un punto de distribución, pero la imagen de SO se debe recibir desde otro punto de distribución.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Configuración de puntos de distribución para aceptar solicitudes PXE  

Para implementar sistemas operativos en clientes de Configuration Manager que efectúan solicitudes de arranque PXE, configure uno o varios puntos de distribución para que acepten las solicitudes PXE. Una vez configurado el punto de distribución, responde a las solicitudes de arranque de PXE y determina las acciones de implementación adecuadas que se van a llevar a cabo. Para obtener más información, consulte [Instalar o modificar un punto de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Personalización de los tamaños de bloque de TFTP de RamDisk y de ventana en puntos de distribución habilitados con PXE  

Se pueden personalizar los tamaños de bloque de TFTP de RamDisk y de ventana para los puntos de distribución habilitados con PXE. Si ha personalizado la red, un tamaño de bloque o ventana grande podría provocar que se produjera un error de tiempo de espera en la descarga de la imagen de arranque. Las personalizaciones del tamaño del bloque y la ventana de TFTP de RamDisk permiten optimizar el tráfico de TFTP al usar PXE para cumplir los requisitos de red específicos. Para determinar la configuración más eficaz, pruebe la configuración personalizada en el entorno.  

-   **Tamaño del bloque TFTP**: el tamaño de bloque es el tamaño de los paquetes de datos que el servidor envía al cliente que está descargando el archivo. Un tamaño de bloque mayor permite que el servidor envíe menos paquetes, por lo que habrá menos demoras por los recorridos de ida y vuelta entre el servidor y el cliente. Pero un tamaño de bloque grande genera fragmentación en los paquetes, lo que la mayoría de implementaciones de cliente de PXE no admiten.  

-   **Tamaño de ventana de TFTP**: TFTP requiere un paquete de confirmación para cada bloque de datos que se envía. El servidor no envía el siguiente bloque de la secuencia hasta que reciba el paquete de confirmación del bloque anterior. Las ventanas TFTP permiten definir cuántos bloques de datos se necesitan para llenar una ventana. El servidor envía los bloques de datos sucesivamente hasta que se completa la ventana; en ese momento, el cliente envía un paquete de confirmación. Si se aumenta este tamaño de ventana, se reduce el número de demoras por los recorridos de ida y vuelta entre el cliente y el servidor, y se disminuye el tiempo global necesario para descargar una imagen de arranque.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modificar el tamaño de la ventana de TFTP de RamDisk  
Para personalizar el tamaño de la ventana de TFTP de RamDisk, agregue la clave del Registro siguiente a los puntos de distribución habilitados con PXE:  

- **Ubicación**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nombre**: RamDiskTFTPWindowSize  
- **Tipo**: REG_DWORD  
- **Valor**: (tamaño de ventana personalizado)  
    - El valor predeterminado es **1** (un bloque de datos llena la ventana).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modificar el tamaño de bloque de TFTP de RamDisk  
Para personalizar el tamaño de la ventana de TFTP de RamDisk, agregue la clave del Registro siguiente a los puntos de distribución habilitados con PXE:  

- **Ubicación**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nombre**: RamDiskTFTPBlockSize  
- **Tipo**: REG_DWORD  
- **Valor**: (tamaño de bloque personalizado)  
    - El valor predeterminado es **4096**.  

> [!Note]  
> Los Servicios de implementación de Windows y el servicio de respondedor PXE de Configuration Manager admiten estas configuraciones de TFTP.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> Configuración de puntos de distribución para admitir la multidifusión  

Multidifusión es un método de optimización de red. Úselo en los puntos de distribución si es probable que varios clientes descarguen la misma imagen de SO al mismo tiempo. Cuando se usa la multidifusión, varios equipos pueden descargar la imagen de SO al mismo tiempo, ya que el punto de distribución la distribuye mediante multidifusión. Sin la multidifusión, el punto de distribución envía una copia de los datos a cada cliente a través de una conexión independiente. Para obtener más información, consulte [Usar multidifusión para implementar Windows a través de la red](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

Antes de implementar el sistema operativo, configure un punto de distribución para admitir la multidifusión. Para obtener más información, vea [Instalación y configuración de puntos de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Punto de migración de estado  

El punto de migración de estado almacena los datos de estado de usuario que USMT captura en un equipo y después restaura en otro. Pero cuando se captura la configuración de usuario para la implementación de SO en el mismo equipo, como una implementación en la que se actualiza Windows en el equipo de destino, se puede elegir si los datos se almacenan en el mismo equipo mediante vínculos físicos o usar un punto de migración de estado. En algunas implementaciones, al crear el almacén de estado, Configuration Manager crea automáticamente una asociación entre el almacén de estado y el equipo de destino. Al planear el punto de migración de estado, tenga en cuenta los factores siguientes:    


### <a name="user-state-size"></a>Tamaño de estado de usuario  

El tamaño de estado de usuario afecta directamente al almacenamiento en disco en el punto de migración de estado y al rendimiento de la red durante la migración. Tenga en cuenta el tamaño de estado de usuario y el número de equipos que desea migrar. También es preciso tener en cuenta la configuración que desea migrar desde el equipo. Por ejemplo, si ya se ha realizado una copia de seguridad de la carpeta **Mis documentos** en un servidor, tal vez no sea necesario migrarla como parte de la implementación de imagen. Evitar la realización de migraciones innecesarias reduce el tamaño total del estado de usuario y minimiza el efecto que podría tener en el rendimiento de la red y el almacenamiento en disco en el punto de migración de estado.  


### <a name="user-state-migration-tool"></a>Herramienta de migración de estado de usuario  

Para capturar y restaurar el estado de usuario durante la implementación de sistemas operativos, use el paquete de la Herramienta de migración de estado de usuario (USMT) que apunta a los archivos de origen de USMT. Configuration Manager crea automáticamente este paquete en la consola de Configuration Manager en **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**. Configuration Manager usa USMT 10 para capturar el estado de usuario de un sistema operativo y después restaurarlo en otro. En Windows Assessment and Deployment Kit (ADK de Windows) para Windows 10 se incluye USMT 10.

Para obtener una descripción de otros escenarios de migración para USMT 10, vea [Common Migration Scenarios](/windows/deployment/usmt/usmt-common-migration-scenarios) (Escenarios comunes de migración) en la documentación de Windows.  


### <a name="retention-policy"></a>Directiva de retención  

Al configurar el punto de migración de estado, especifique el intervalo de tiempo para mantener los datos de estado de usuario que almacena. El periodo de tiempo para mantener los datos en el punto de migración de estado depende de dos factores:  

-   El efecto de los datos almacenados en el almacenamiento en disco.  

-   La posibilidad de que sea necesario mantener los datos durante un tiempo por si fuera preciso migrarlos de nuevo.  
  
  
La migración de estado se produce en dos fases: captura y restauración de los datos. Al capturar los datos, se recopilan los datos de estado de usuario y se guardan en el punto de migración de estado. Al restaurar los datos, los datos de estado de usuario se recuperan del punto de migración de estado, se escriben en el equipo de destino y, a continuación, la secuencia de tareas **Liberar almacén de estado** los libera. Al realizar la liberación de los datos, se inicia el temporizador de retención. Si selecciona la opción de eliminar inmediatamente los datos migrados, los datos de estado de usuario se eliminan en cuanto se liberan. Si selecciona la opción de mantener los datos durante un determinado periodo de tiempo, los datos se eliminan al finalizar dicho periodo, después de la liberación de los datos de estado. Cuanto más tiempo se establezca el periodo de retención, es probable que se necesite más espacio en disco.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Seleccionar una unidad para el almacenamiento de datos de migración de estado de usuario  

Al configurar el punto de migración de estado, especifique la unidad del servidor en la que quiere almacenar los datos de migración de estado de usuario. Debe seleccionar una unidad de una determinada lista de unidades. Sin embargo, algunas de estas unidades pueden representar unidades que no permiten la escritura, como unidades de CD o unidades de recursos compartidos que no son de red. Es posible que algunas letras de unidad no estén asignadas a las unidades del equipo. Especifique una unidad compartida y que permita la escritura al configurar el punto de migración de estado.  


### <a name="configure-a-state-migration-point"></a>Configurar un punto de migración de estado  

Utilice los siguientes métodos para configurar un punto de migración de estado para almacenar los datos de estado de usuario:  

-   Use el **Asistente para crear servidor de sistema de sitio** para crear un nuevo servidor de sistema de sitio para el punto de migración de estado.  

-   Use el **Asistente para agregar roles de sistema de sitio** para agregar un punto de migración de estado a un servidor existente.  

Al usar estos asistentes, se le solicitará que proporcione la información siguiente para el punto de migración de estado:  

-   Las carpetas para almacenar los datos de estado de usuario.  

-   El número máximo de clientes que pueden almacenar datos en el punto de migración de estado.  

-   Seleccione el espacio libre mínimo para que el punto de migración de estado almacene datos de estado de usuario.  

-   La directiva de eliminación para el rol. Especifique que los datos de estado de usuario se eliminen inmediatamente después de ser restaurados en un equipo, o bien después de un número específico de días tras ser restaurados en un equipo.  

-   Si el punto de migración de estado responde solo a solicitudes de restauración de datos de estado de usuario. Cuando se habilita esta opción, no se puede utilizar el punto de migración de estado para almacenar datos de estado de usuario.  

Para consultar los pasos necesarios para instalar un rol de sistema de sitio, consulte [Add site system roles](../../core/servers/deploy/configure/add-site-system-roles.md) (Agregar roles de sistema de sitio).