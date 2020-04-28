---
title: Funcionalidades de Technical Preview 1603
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1603.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73e3e19df4ce545e4cbb36109da2710e848f1159
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076227"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Funciones de Technical Preview 1603 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1603 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Además, cuando usa System Center Technical Preview 5, esta versión se instala como una versión de línea base de Configuration Manager Technical Preview. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

 **Problemas conocidos de esta Technical Preview:**  

- Esta versión no incorpora nuevas características, sino que incluye actualizaciones para características publicadas anteriormente. Por tanto, la página Características del asistente para actualizar estará vacía si ya ha actualizado a 1602 y ha habilitado todas las características incluidas en 1602.  

- Una vez que el servidor del sitio se actualice a Technical Preview 1603, los clientes no podrán usar las características de control remoto hasta que actualicen también a 1603.  

  **Estas son las nuevas características que puede probar con esta versión.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a> Mejoras en el Centro de software  

### <a name="new-tiled-view-for-apps"></a>Nueva vista en iconos para aplicaciones  
 Los usuarios finales ahora pueden elegir entre una lista de aplicaciones o una vista en mosaico de aplicaciones en la pestaña **Aplicaciones** del Centro de software.  

### <a name="select-multiple-updates-in-software-center"></a>Selección de varias actualizaciones en el Centro de software  
 En la pestaña **Actualizaciones** del Centro de software, ahora puede seleccionar varias actualizaciones o bien seleccionar **Actualizar todo** para empezar a instalar varias actualizaciones simultáneamente.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a> Mejoras en el control remoto  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Límite del acceso al portapapeles compartido en una sesión de control remoto  
 Ahora puede habilitar la nueva configuración de cliente de herramientas remotas **Solicitar al usuario permiso de transferencia de archivos compartidos del portapapeles** para limitar el acceso al portapapeles compartido en una sesión de control remoto.  

 Cuando está habilitado, el usuario final que comparte una sesión remota debe conceder permisos al visor de esa sesión para que este pueda transferir archivos desde la sesión a su equipo local a través del portapapeles compartido.  

 De este modo, se agrega un nivel de protección para el usuario final como anteriormente: si se ha concedido al visor control total del equipo del usuario final, este podrá usar el portapapeles compartido para transferir archivos desde la sesión a su equipo local en un modo totalmente transparente para el usuario final.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Personalización del tamaño de bloque de TFTP de RamDisk y el tamaño de la ventana de puntos de distribución habilitados con PXE  
 En 1603 Technical Preview, tiene la posibilidad de personalizar el tamaño de bloque de TFTP de RamDisk y el tamaño de la ventana de puntos de distribución habilitados con PXE. El hecho de haber personalizado su red podría provocar que se produjera un error de tiempo de espera en la descarga de la imagen de arranque porque el tamaño del bloque o la ventana es demasiado grande. La personalización tanto del tamaño del bloque como del de la ventana de TFTP de RamDisk le permiten optimizar el tráfico de TFTP al utilizar PXE para cumplir los requisitos de red específicos.   
Debe probar la configuración personalizada en su entorno para determinar lo que es más eficaz.  

-   **Tamaño del bloque TFTP**: el tamaño de bloque es el tamaño de los paquetes de datos enviados por el servidor al cliente que está descargando el archivo (como se describe en RFC 2347). Un tamaño de bloque mayor permite que el servidor envíe menos paquetes, por lo que habrá menos demoras por los recorridos de ida y vuelta entre el servidor y el cliente. Sin embargo, un tamaño de bloque grande genera fragmentación en los paquetes, lo cual no se admite en la mayoría de implementaciones de cliente de PXE.  

-   **Tamaño de ventana de TFTP**: TFTP requiere un paquete de confirmación para cada bloque de datos que se envía. El servidor no envía el siguiente bloque de la secuencia hasta que reciba el paquete de confirmación del bloque anterior. La característica basada en ventanas de TFTP forma parte de Servicios de implementación de Windows y permite definir cuántos bloques de datos son necesarios para completar una ventana. El servidor envía los bloques de datos sucesivamente hasta que se completa la ventana; en ese momento, el cliente envía un paquete de confirmación. Al aumentar el tamaño de la ventana se reduce el número de demoras por los recorridos de ida y vuelta entre el cliente y el servidor y se disminuye el tiempo global necesario para descargar una imagen de arranque.  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar las siguientes tareas y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo ha funcionado:  

-   Puedo personalizar el tamaño de la ventana de TFTP de RamDisk en el punto de distribución habilitado con PXE.  

-   Puedo personalizar el tamaño del bloque de TFTP de RamDisk en el punto de distribución habilitado con PXE.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar el tamaño de la ventana de TFTP de RamDisk  

- Agregue la siguiente clave del Registro en puntos de distribución habilitados con PXE para personalizar el tamaño de la ventana de TFTP de RamDisk:  

   **Ubicación**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nombre: RamDiskTFTPWindowSize  

   **Tipo**: REG_DWORD  

   **Valor**: &lt;tamaño de ventana personalizado\>  

  El valor predeterminado es 1 (1 bloque de datos completa la ventana)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar el tamaño de bloque de TFTP de RamDisk  

- Agregue la siguiente clave del Registro en puntos de distribución habilitados con PXE para personalizar el tamaño de la ventana de TFTP de RamDisk:  

   **Ubicación**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nombre: RamDiskTFTPBlockSize  

   **Tipo**: REG_DWORD  

   **Valor**: &lt;tamaño de bloque personalizado\>  

  El valor predeterminado es 4096 (4k).  
