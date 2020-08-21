---
title: Administración de la configuración de actualizaciones de software
titleSuffix: Configuration Manager
description: Obtenga información acerca de la configuración de cliente adecuada para las actualizaciones de software en su sitio después de instalar el punto de actualización de software.
ms.date: 06/04/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e0395d41c2886bca1d623fb2736bfc86012f89b4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696759"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a> Administrar la configuración de las actualizaciones de software  

*Se aplica a: Configuration Manager (rama actual)*

Después de sincronizar las actualizaciones de software en Configuration Manager, configure y compruebe la configuración en las secciones siguientes.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a> Configuración de cliente para las actualizaciones de software  
Después de instalar el punto de actualización de software, la actualización de software estará habilitada en los clientes de manera predeterminada, y las opciones de la página **Actualizaciones de software** de la configuración de cliente tendrán valores predeterminados. La configuración de cliente se utiliza en todo el sitio e influye en el momento en que se examina el cumplimiento de las actualizaciones de software, y en cómo y cuándo se instalan actualizaciones de software en los equipos cliente. Antes de implementar las actualizaciones de software, compruebe que la configuración de cliente sea la adecuada para las actualizaciones de software de su sitio.  

> [!IMPORTANT]  
>  La opción **Habilitar actualizaciones de software en clientes** está habilitada de manera predeterminada. Si desactiva esta opción, Configuration Manager quita las directivas de implementación existentes del cliente.  

Para obtener información sobre cómo especificar la configuración de cliente, vea [Cómo establecer la configuración del cliente](../../core/clients/deploy/configure-client-settings.md).  

Para obtener más información sobre la configuración de cliente, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md).  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a> Configuración de directiva de grupo para actualizaciones de software  
Hay configuraciones de directiva de grupo específicas empleadas por el Agente de Windows Update (WUA) en equipos cliente para conectarse a WSUS que se ejecuta en el punto de actualización de software. Esta configuración de directiva de grupo también se usa para analizar correctamente la compatibilidad de las actualizaciones de software y actualizar automáticamente las actualizaciones de software y el WUA.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Directiva local que especifica la ubicación del servicio Microsoft Update en la intranet  
Cuando se crea el punto de actualización de software para un sitio, los clientes reciben una directiva de equipo que proporciona el nombre de servidor del punto de actualización de software y configura la directiva local **Especificar ubicación del servicio de Windows Update en la intranet** en el equipo. El WUA recupera el nombre de servidor especificado en la configuración **Establecer el servicio de actualización de la intranet para detectar actualizaciones** y, a continuación, se conecta a este servidor al analizar la compatibilidad de las actualizaciones de software. Cuando se crea una directiva de dominio para la opción **Especificar la ubicación del servicio Microsoft Update en la intranet** , dicha directiva reemplaza la directiva local y, además, el WUA podría conectarse a un servidor que no sea el punto de actualización de software. Si esto ocurre, el cliente podría analizar la compatibilidad de la actualización de software según diferentes productos, clasificaciones e idiomas. Por lo tanto, no se debe configurar la directiva de Active Directory para equipos cliente.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Directiva local que permite el contenido firmado procedente de la ubicación del servicio Microsoft Update de la intranet  
Debe habilitar la configuración de la directiva de grupo **Permitir el contenido firmado procedente de la ubicación del servicio Microsoft Update de la intranet** antes de que el WUA de los equipos analice si hay actualizaciones de software creadas y publicadas mediante el editor de actualizaciones de System Center. Si la configuración de directiva está habilitada, el WUA aceptará actualizaciones de software recibidas a través de una ubicación en intranet si las actualizaciones de software están firmadas en el almacén de certificados de **Editores de confianza** en el equipo local. Para obtener más información acerca de la configuración de directiva de grupo requerida para el editor de actualizaciones, consulte [Updates Publisher 2011 Documentation Library (Biblioteca de documentación del editor de actualizaciones 2011)](/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

### <a name="automatic-updates-configuration"></a>Configuración de actualizaciones automáticas  
Las actualizaciones automáticas permiten que los equipos cliente reciban actualizaciones de seguridad y otras descargas importantes. Las actualizaciones automáticas se especifican mediante la configuración de la directiva de grupo **Configurar actualizaciones automáticas** o mediante el Panel de control en el equipo local. Cuando las actualizaciones automáticas están habilitadas, los equipos cliente recibirán notificaciones de actualización y según las opciones configuradas, los equipos cliente descargarán e instalarán las actualizaciones necesarias. Cuando las actualizaciones automáticas coexisten con las actualizaciones de software, cada equipo cliente podría mostrar iconos y elementos emergentes de notificaciones en pantalla para la misma actualización. Además, cuando se requiere un reinicio, cada equipo cliente podría mostrar un cuadro de diálogo de reinicio para la misma actualización.  

### <a name="self-update"></a>Auto-actualización  
Cuando las actualizaciones automáticas están activadas en los equipos cliente, el WUA realiza automáticamente una auto-actualización cada vez que haya disponible una versión más reciente o cuando haya problemas con un componente del WUA. Cuando las actualizaciones automáticas no están configuradas o están deshabilitadas, y los equipos cliente tienen una versión anterior del WUA, los equipos cliente deben ejecutar el archivo de instalación del WUA.  

## <a name="software-updates-properties"></a>Propiedades de las actualizaciones de software
Las propiedades de la actualización de software proporcionan información acerca de las actualizaciones de software y el contenido asociado. También puede utilizar estas propiedades para configurar opciones de las actualizaciones de software. Cuando abra las propiedades de varias actualizaciones de software, solo se mostrarán las pestañas **Duración máxima de la ejecución** y **Gravedad personalizada** .   

Utilice el procedimiento siguiente para abrir las propiedades de la actualización de software.  

#### <a name="to-open-software-update-properties"></a>Para abrir las propiedades de la actualización de software  

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  
2. En el área de trabajo de la biblioteca de software, expanda **Actualizaciones de software**y haga clic en **Todas las actualizaciones de software**.  
3. Seleccione una o varias actualizaciones de software y, a continuación, en la pestaña **Inicio** , haga clic en **Propiedades** en el grupo **Propiedades** .  

   > [!NOTE]  
   >  En el nodo **Todas las actualizaciones de software**, Configuration Manager solo muestra las actualizaciones de software con una clasificación de **Crítico** y **Seguridad** publicadas en los últimos 30 días.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a> Revisar la información de la actualización de software  
En las propiedades de la actualización de software, puede revisar información detallada acerca de una actualización de software. No se muestra la información detallada cuando seleccione más de una actualización de software. Las secciones siguientes describen la información que está disponible para una actualización de software seleccionada.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a> Detalles de la actualización de software  
En la pestaña **Detalles de la actualización de software** , puede ver la siguiente información de resumen sobre la actualización de software seleccionada:  

- **Id. de boletín**: especifica el identificador de boletín asociado a las actualizaciones de software de seguridad. Para obtener detalles sobre el boletín de seguridad, busque el identificador del boletín en la página web del [Centro de respuestas de seguridad de Microsoft](https://portal.msrc.microsoft.com/).  

> [!NOTE]
> Está cambiando la forma en que Microsoft documenta las actualizaciones de seguridad. En el modelo anterior se usaban las páginas web de los boletines de seguridad y se incluían los números de identificación de los boletines (por ejemplo, MS16-XXX) como punto de pivote. Esta forma de documentación de las actualizaciones de seguridad, incluidos los números de identificación de los boletines, se va a retirar y se va reemplazar por la Guía de actualizaciones de seguridad. En lugar de los identificadores de boletín, la nueva guía gira en torno a los números de identificación de vulnerabilidades y los números de identificación de artículos de KB. Para más información, consulte las [P+F sobre la Guía de actualizaciones de seguridad](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **Id. de artículo**: especifica el identificador de artículo de la actualización de software. El artículo al que se hace referencia proporciona información más detallada acerca de la actualización de software y qué soluciona o mejora.  

- **Fecha de revisión**: especifica la fecha en que se modificó por última vez la actualización de software.  

- **Clasificación de máxima gravedad**: especifica la clasificación de gravedad definida por el proveedor para la actualización de software.  

- **Descripción**: proporciona información general sobre la condición que arregla o mejora la actualización de software.  

- **Idiomas aplicables**: muestra los idiomas a los que se aplica la actualización de software.  

- **Productos afectados**: muestra los productos a los que se aplica la actualización de software.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a> Información de contenido  
En la pestaña **Información de contenido** , revise la siguiente información acerca del contenido que se asocia con la actualización de software seleccionada:  

-   **Id. de contenido**: especifica el identificador de contenido de la actualización de software.  

-   **Descargado**: indica si Configuration Manager ha descargado los archivos de la actualización de software.  

-   **Idiomas**: especifica los idiomas de la actualización de software.  

-   **Ruta de origen**: especifica la ruta de acceso de los archivos de origen de la actualización de software.  

-   **Tamaño (MB)** : especifica el tamaño de los archivos de origen de la actualización de software.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> Información de agrupación personalizada  
En la pestaña **Información de agrupación personalizada** , revise la información de agrupación personalizada de la actualización de software. Si la actualización de software seleccionada contiene actualizaciones de software agrupadas incluidas en el archivo de la actualización de software, éstas se muestran en la sección **Información de agrupación** . Esta pestaña no muestra las actualizaciones de software agrupadas que se incluyen en la pestaña **Información de contenido** , como los archivos de actualización para los distintos idiomas.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> Información de sustitución  
En la pestaña **Información de sustitución** , puede ver la siguiente información acerca de la sustitución de la actualización de software:  

- **Esta actualización se ha sustituido por las siguientes actualizaciones**: especifica las actualizaciones de software que sustituyen a esta actualización, lo que significa que las actualizaciones que se muestran son más recientes. En la mayoría de los casos, se implementará una de las actualizaciones de software que sustituye a la actualización de software. Las actualizaciones de software que se muestran en la lista contienen hipervínculos a páginas web que proporcionan más información acerca de las actualizaciones de software. Si la actualización no se ha sustituido, aparecerá **Ninguno** .  

- **Esta actualización sustituye a las siguientes actualizaciones**: especifica las actualizaciones de software que sustituye esta actualización de software, lo cual significa que esta actualización de software es más reciente. En la mayoría de los casos, se implementará esta actualización de software para reemplazar las actualizaciones de software sustituidas. Las actualizaciones de software que se muestran en la lista contienen hipervínculos a páginas web que proporcionan más información acerca de las actualizaciones de software. Si esta actualización no sustituye a ninguna otra, aparecerá **Ninguno** .  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> Configurar opciones de actualización de software  
En las propiedades, se pueden configurar las opciones de actualización de software de una o varias actualizaciones de software. La mayoría de las opciones de actualización de software sólo se pueden configurar en el sitio de administración central o en el sitio primario independiente. La información de las siguientes secciones le permitirá configurar las opciones de las actualizaciones de software.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> Establecer el tiempo máximo de ejecución  
En la pestaña **Duración máxima de la ejecución** , establezca el período de tiempo máximo que se asigna a una actualización de software para completarse en equipos cliente. Si la actualización supera el valor de este período máximo, Configuration Manager crea un mensaje de estado y detiene la instalación de actualizaciones de software. Esta opción sólo se puede configurar en un sitio primario independiente o en el sitio de administración central.  

Configuration Manager también utiliza esta opción para determinar si la instalación de las actualizaciones de software se van a iniciar dentro de una ventana de mantenimiento configurada. Si este período máximo de tiempo es mayor que el tiempo restante disponible en la ventana de mantenimiento, la instalación de actualizaciones de software se pospone hasta el inicio de la siguiente ventana de mantenimiento. Si se van a instalar varias actualizaciones de software en un equipo cliente con una ventana de mantenimiento configurada (período de tiempo), las actualizaciones de software irán instalando desde la que tiene la duración de ejecución más baja hasta la más alta. Antes de instalar cada actualización de software, el cliente comprueba que la ventana de mantenimiento disponible proporcionará tiempo suficiente para instalar la actualización de software. Una vez iniciada la instalación de una actualización de software, su proceso de instalación continuará aunque su duración sea más prolongada que la ventana de mantenimiento. Para más información sobre las ventanas de mantenimiento, consulte [Cómo usar ventanas de mantenimiento en System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  

En la pestaña **Duración máxima de la ejecución** , puede ver y configurar las siguientes opciones:  

- **Duración máxima de la ejecución**: especifica el número máximo de minutos que se asigna a una instalación de actualización de software para que se complete antes de que Configuration Manager la detenga. Esta configuración también se utiliza para determinar si resta tiempo suficiente para instalar la actualización antes del final de la ventana de mantenimiento. El valor predeterminado es 60 minutos para los Service Pack. Para otros tipos de actualización de software, el valor predeterminado es 10 minutos si realizó una instalación nueva de la versión 1511 de Configuration Manager o posterior y 5 minutos al actualizar desde una versión anterior. El valor puede ir de 5 a 9999 minutos.  

> [!IMPORTANT]  
>  Asegúrese de configurar el valor de tiempo de ejecución máximo menor que el tiempo de ventana de mantenimiento configurado o aumente el tiempo de ventana de mantenimiento a un valor mayor que el tiempo de ejecución máximo. De lo contrario, la instalación de la actualización de software no se iniciará.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a> Establecer gravedad personalizada  
En las propiedades de una actualización de software, puede utilizar la pestaña **Gravedad personalizada** para configurar los valores de gravedad personalizada de las actualizaciones de software. Esto puede ser necesario si los valores de gravedad predefinidos no satisfacen sus necesidades. Los valores personalizados se incluyen en la columna **Gravedad personalizada** de la consola de Configuration Manager. Puede ordenar las actualizaciones de software por los valores de gravedad personalizada definidos, y también puede crear consultas e informes que puedan filtrar en estos valores. Esta opción sólo se puede configurar en un sitio de administración central o un sitio primario independiente.  

Puede configurar las siguientes opciones en la pestaña **Gravedad personalizada** .  

- **Gravedad personalizada**: establece un valor de gravedad personalizado para las actualizaciones de software. Seleccione **Crítico**, **Importante**, **Moderado**o **Bajo** en la lista. De forma predeterminada, no hay ningún valor de gravedad personalizada establecido.

## <a name="crl-checking-for-software-updates"></a>Comprobación de CRL para actualizaciones de software
De forma predeterminada, la lista de revocación de certificados (CRL) no se comprueba al verificar la firma en las actualizaciones de software de Configuration Manager. La comprobación de CRL cada vez que se usa un certificado proporciona una mayor seguridad frente a certificados revocados, pero incorpora un retraso en la conexión e implica un procesamiento adicional en el equipo que realiza la comprobación de CRL.  

Si se utiliza, la comprobación de CRL debe estar habilitada en las consolas de Configuration Manager que procesan las actualizaciones de software.  

#### <a name="to-enable-crl-checking"></a>Para habilitar la comprobación de CRL  
En el equipo que realiza la comprobación de CRL, desde el DVD del producto, ejecute lo siguiente desde un símbolo del sistema: **\SMSSETUP\BIN\X64\\** <*language*> **\UpdDwnldCfg.exe /checkrevocation**.  

Por ejemplo, para Inglés (Estados Unidos) debe ejecutar **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**