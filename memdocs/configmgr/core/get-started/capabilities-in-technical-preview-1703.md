---
title: Funcionalidades de Technical Preview 1703
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1703.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fb13844dd05049b9186909884aa0c457a8cfacd9
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428408"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Funciones de Technical Preview 1703 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1703 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementación de aplicaciones iOS adquiridas por volumen en colecciones de dispositivos

Ahora puede implementar aplicaciones con licencia para dispositivos y usuarios. Dependiendo de la capacidad de las aplicaciones para admitir licencias de dispositivo, se solicitará una licencia adecuada al realizar la implementación, como sigue:

|||||
|-|-|-|-|
|Versión de Configuration Manager|¿La aplicación admite licencias de dispositivo?|Tipo de colección de implementación|Licencia exigida|
|Anterior a 1702|Sí|Usuario|Licencia de usuario|
|Anterior a 1702|No|Usuario|Licencia de usuario|
|Anterior a 1702|Sí|Dispositivo|Licencia de usuario|
|Anterior a 1702|No|Dispositivo|Licencia de usuario|
|1702 y versiones posteriores|Sí|Usuario|Licencia de usuario|
|1702 y versiones posteriores|No|Usuario|Licencia de usuario|
|1702 y versiones posteriores|Sí|Dispositivo|Licencia de dispositivo|
|1702 y versiones posteriores|No|Dispositivo|Licencia de usuario|


## <a name="direct-links-to-applications-in-software-center"></a>Vínculos directos a aplicaciones del centro de software

Ahora puede ofrecer a los usuarios finales un vínculo directo a una aplicación en el centro de software. Esto significa que ya no deben abrir el centro de software y buscar una aplicación antes de poder instalarla. Esto solo está disponible para las aplicaciones de Configuration Manager, no para los paquetes y programas o las secuencias de tareas.

### <a name="try-it-out"></a>Haga la prueba                 

Use el siguiente formato de dirección URL para abrir el centro de software desde una aplicación determinada:

**Softwarecenter:SoftwareId=_Identificador de aplicación_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Cómo obtener el identificador de aplicación de una aplicación.

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo Biblioteca de software, expanda **Administración de aplicaciones** y, después, haga clic en **Aplicaciones**.
3. En la vista **Aplicaciones**, haga clic con el botón derecho en uno de los encabezados de columna y, después, en la lista seleccione **Id. único de CI**. Verá que el identificador único de cada aplicación se muestra ahora en la lista.
4. Tenga en cuenta el **identificador único de CI** de la aplicación a la que quiere proporcionar un vínculo, por ejemplo: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5. Después, quite cualquier texto que aparezca tras el GUID de la aplicación, en este caso, **/2**. Esto le deja con el identificador de aplicación.
6. Por último, para terminar de crear el vínculo, anteponga **Softwarecenter:SoftwareID=** . Siguiendo con el ejemplo anterior, el vínculo final será: **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Mediante este vínculo, los usuarios finales pueden abrir el centro de software directamente en la aplicación especificada.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificados PFX para equipos cliente Windows de Configuration Manager

Ahora puede implementar perfiles de certificado PFX que haya importado a equipos cliente de Configuration Manager con Windows 10.

### <a name="try-it-out"></a>Haga la prueba

Siga las instrucciones de [Cómo crear perfiles de certificados PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md) para importar un perfil PFX, implementarlo y, después, comprobar si el certificado se ha instalado para el usuario de destino.



## <a name="configure-azure-services-wizard"></a>Asistente para configuración de Servicios de Azure
Technical Preview 1703 presenta el asistente para la **configuración de Servicios de Azure**. Este asistente proporciona una experiencia de configuración común que reemplaza los flujos de trabajo individuales para configurar los servicios en la nube que usa con Configuration Manager. Esto se realiza mediante una **aplicación web de Azure** para proporcionar la información de suscripción y configuración que, de lo contrario, especificaría cada vez que configurase un nuevo componente o servicio de Configuration Manager con Azure.

Con Technical Preview 1703, con este asistente solo se configura la Tienda Windows para empresas (WSfB).  Otros servicios en la nube se configuran mediante sus flujos de trabajo independientes.

- Use la información de este tema de vista previa para reemplazar los pasos de configuración de la sección [Configuración de la sincronización de la Tienda Windows para empresas](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) del tema de la rama actual [Administración de aplicaciones desde la Tienda Windows para empresas con Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

- Para obtener más información sobre las aplicaciones web, vea [Autenticación y autorización en el Servicio de aplicaciones de Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) e [Introducción a Aplicaciones web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Requisitos previos y planeamiento
Cuando establezca una conexión entre Configuration Manager y la Tienda Windows para empresas, deberá proporcionar una carpeta donde se conservará el contenido de la aplicación sincronizado desde la tienda. Para asegurarse de que esta carpeta sea segura y que su contenido se pueda implementar en dispositivos, compruebe que se hayan aplicado los permisos siguientes:
- El equipo en el que instale el rol de sistema de sitio del punto de conexión de servicio (el sitio de nivel superior de la jerarquía) debe tener permisos de lectura y escritura en la carpeta que haya especificado al usar la cuenta **Computer$** .  

- El autor de la aplicación debe tener permisos de lectura en la carpeta que haya especificado.  

- La cuenta **Computer$** de cada equipo que hospede una instancia del proveedor de SMS debe poder usar la carpeta que haya especificado.

En Azure Active Directory, registre Configuration Manager como una herramienta de administración de aplicación web o API web. De este modo, se crea el identificador de cliente que necesitará más adelante.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Usar el asistente para configurar el servicio en la nube de WSfB

1. En la consola, vaya a **Administración** > **Introducción** > **Administración de servicios en la nube** > **Azure** > **Servicios de Azure** y, después, elija **Configurar servicios de Azure** para iniciar el **Asistente para servicios de Azure**.

2. En la página **Servicios de Azure**, seleccione el servicio que quiera configurar y, después, haga clic en **Siguiente**. Con esta vista previa solo se puede configurar WSfB.

3. En la página **General**, proporcione un nombre descriptivo para el **Nombre del servicio de Azure** y una descripción opcional y, después, haga clic en **Siguiente**.

4. En la página **Aplicación**, especifique el entorno de Azure y, después, haga clic en **Examinar** para abrir la ventana Aplicación del servidor.

5. En la ventana **Aplicación del servidor**, seleccione la aplicación de servidor que quiera usar y, después, haga clic en **Aceptar**.
   Las aplicaciones de servidor son las aplicaciones web de Azure que contienen las configuraciones de la cuenta de Azure, incluidos el identificador de inquilino, el identificador de cliente y una clave secreta para los clientes. Si no tiene una aplicación de servidor disponible, use una de las siguientes:
   - **Crear**: para crear una aplicación de servidor, haga clic en **Crear**. Proporcione un nombre descriptivo para la aplicación y el inquilino. Después, una vez que inicie sesión en Azure, Configuration Manager crea automáticamente la aplicación web en Azure, incluidos el identificador de cliente y la clave secreta para su uso con la aplicación web. Podrá verlos más adelante desde Azure Portal.
   - **Importar**: para usar una aplicación web que ya existe en su suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el inquilino y, después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web que quiere que use Configuration Manager. Después de **Comprobar** la información, haga clic en **Aceptar** para continuar.  </br></br>

6. Revise la página **Información** y complete los pasos y configuraciones adicionales tal como se indica. Estas configuraciones son necesarias para usar el servicio con Configuration Manager.
   Por ejemplo, para configurar WSfB:

   1. En Azure, debe registrar Configuration Manager como una aplicación web o API web y registrar el identificador de cliente. Especifique también una clave de cliente para su uso con la herramienta de administración (que es Configuration Manager).

   2.    En la consola de WSfB debe configurar Configuration Manager como la herramienta de administración de almacén, habilitar la compatibilidad de aplicaciones con licencia sin conexión y, después, comprar al menos una aplicación.   </br>

   Haga clic en **Siguiente** cuando esté listo para continuar.

7. En la página **Configuraciones de aplicación**, realice las configuraciones del catálogo de aplicaciones y el idioma para este servicio y, después, haga clic en **Siguiente**.
8. Cuando finalice el asistente, la consola de Configuration Manager muestra que ha configurado la **Tienda Windows para empresas** como un **Tipo de servicio de nube**.

Ahora puede usar el resto del [contenido de la rama actual](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) para administrar aplicaciones desde la WSfB para sincronizar, crear e implementar y supervisar las aplicaciones de la Tienda Windows para empresas.

### <a name="modify-a-cloud-service-configuration"></a>Modificar la configuración de un servicio en la nube
Puede ver y editar las propiedades de un servicio en la nube para modificar la configuración.

En la consola, vaya a **Administración** > **Introducción** > **Administración de servicios en la nube** > **Azure** > **Servicios de Azure** y, después, elija **Configurar servicios de Azure**, seleccione un servicio en la nube y luego elija **Propiedades**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversión de BIOS a UEFI durante una actualización local
Windows 10 Creators Update presenta una herramienta de conversión sencilla que automatiza el proceso para volver a particionar el disco duro de hardware compatible con UEFI e integra la herramienta de conversión en el proceso de actualización local de Windows 7 a Windows 10. Cuando esta herramienta se combina con la secuencia de tareas de actualización del sistema operativo y la herramienta de OEM que convierte el firmware de BIOS a UEFI, puede convertir los equipos de BIOS a UEFI durante una actualización local a Windows 10 Creators Update. Para obtener más información, consulte [Task sequence steps to manage BIOS to UEFI conversion (Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI)](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

## <a name="collapsible-task-sequence-groups"></a>Grupos de secuencias de tareas contraíbles
Esta versión introduce la capacidad de expandir y contraer los grupos de la secuencia de tareas. Puede expandir o contraer grupos individuales o expandir o contraer todos los grupos a la vez.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Configuración de cliente para configurar Windows Analytics para Upgrade Readiness
A partir de esta versión, puede usar la configuración de cliente de dispositivo para simplificar la configuración de los datos de diagnóstico de Windows necesarios para usar soluciones de Windows Analytics como Upgrade Readiness con Configuration Manager. Configuration Manager puede recuperar datos de Windows Analytics que pueden proporcionar información valiosa sobre el estado actual de su entorno en función de los datos de diagnóstico de Windows notificados por los equipos cliente. Los equipos cliente hacen llegar los datos de diagnóstico de Windows al servicio de diagnóstico de Windows y, a continuación, los datos pertinentes se transfieren a soluciones de Windows Analytics que se hospedan en una de las áreas de trabajo de OMS de su organización. Upgrade Readiness es una solución de Windows Analytics que puede ayudarle a priorizar las decisiones sobre las actualizaciones de Windows para los dispositivos administrados.

### <a name="prerequisites"></a>Requisitos previos
- Debe haber configurado el sitio para usar el servicio de nube de Upgrade Readiness.

### <a name="configure-windows-analytics-client-settings"></a>Configurar los ajustes de cliente de Windows Analytics
Para configurar Windows Analytics, en la consola de Configuration Manager vaya a **Administración** > **Configuración de cliente**, haga doble clic en **Create Custom Device Client Settings** (Crear configuración de cliente de dispositivo personalizada) y, después, seleccione **Windows Analytics**.  

A continuación, configure lo siguiente después de navegar a la pestaña de configuración de **Windows Analytics**:
- **Identificador comercial**  
La clave de identificador comercial asigna información desde los dispositivos que administra hasta el área de trabajo de OMS que hospeda los datos de Windows Analyitics de su organización. Si ya ha configurado una clave de identificador comercial para su uso con Upgrade Readiness, úsela. Si todavía no tiene una clave de id. comercial, genere una.

- Establezca un **nivel de datos de diagnóstico para dispositivos con Windows 10**.

- Elija **participar en la recopilación de datos comerciales en dispositivos con Windows 7, 8 y 8.1**.   

- **Configurar la recopilación de datos de Internet Explorer** En dispositivos que ejecutan Windows 8.1 o versiones anteriores, la recopilación de datos de Internet Explorer puede permitir que Upgrade Readiness detecte incompatibilidades de aplicaciones web que podrían impedir una actualización sin problemas a Windows 10. La recopilación de datos de Internet Explorer se puede habilitar en función de cada zona de Internet.
