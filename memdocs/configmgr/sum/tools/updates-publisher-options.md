---
title: Configuración de opciones
titleSuffix: Configuration Manager
description: Configurar opciones para usar System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700073"
---
# <a name="configure-options-for-updates-publisher"></a>Configurar opciones de Updates Publisher

*Se aplica a: System Center Updates Publisher*

Revise y configure las opciones y los valores de configuración relacionados que afectan al funcionamiento de Updates Publisher.

Para acceder a las opciones de Updates Publisher, haga clic en la pestaña **Propiedades**de **Updates Publisher** que se encuentra en la esquina superior izquierda de la consola y elija **Opciones**.

![Opciones](media/properties1.png)   


Las opciones se dividen en las siguientes categorías:

-   Servidor de actualización
-   Servidor de Configuration Manager
-   Configuración de proxy
-   Editores de confianza
-   avanzadas
-   Updates
-   Registro

## <a name="update-server"></a>Servidor de actualización
Debe configurar Updates Publisher para que funcione con un servidor de actualización como Windows Server Update Services (WSUS) para poder [publicar actualizaciones](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace). Esto incluye especificar el servidor, los métodos de conexión a ese servidor cuando es remoto con respecto a la consola y un certificado que use las actualizaciones firmadas digitalmente que publique.

- **Configurar un servidor de actualización**. Cuando configure un servidor de actualización, seleccione el servidor WSUS de nivel superior (servidor de actualización) de la jerarquía de Configuration Manager para que todos los sitios secundarios tengan acceso a las actualizaciones que publique.

  Si el servidor de actualización es remoto con respecto al servidor de Updates Publisher, especifique el nombre de dominio completo (FQDN) del servidor e indique si se va a conectar mediante SSL. Cuando se conecta mediante SSL, el puerto predeterminado cambia de 8530 a 8531. Asegúrese de que el puerto que establece coincide con el que usa el servidor de actualización.

  > [!TIP]  
  > Si no configura un servidor de actualización, todavía puede usar Updates Publisher para crear actualizaciones de software.

- **Configurar el certificado de firma**. Debe configurar un servidor de actualización y conectarse correctamente al mismo para poder configurar el certificado de firma.

  Updates Publisher usa el certificado de firma para firmar las actualizaciones de software que se publican en el servidor de actualización. La publicación no se realiza si el certificado digital no está disponible en el almacén de certificados del servidor de actualización o del equipo en donde se ejecuta Updates Publisher.

  Para obtener más información sobre cómo agregar el certificado al almacén de certificados, Vea [Certificates and security for Updates Publisher](updates-publisher-security.md) (Certificados y seguridad de Updates Publisher).

  Si el servidor de actualización no detecta automáticamente un certificado digital, elija una de las siguientes opciones:

  -   **Examinar**: esta opción solo está disponible cuando el servidor de actualización está instalado en el servidor donde se ejecuta la consola. Después de seleccionar un certificado, debe elegir **Crear** para agregar el certificado al almacén de certificados de WSUS en el servidor de actualización. Debe especificar la contraseña del archivo **.pfx** de los certificados que seleccione con este método.

  -   **Crear**: use esta opción para crear un certificado. Esta opción también agrega el certificado al almacén de certificados de WSUS en el servidor de actualización.

  **Si crea su propio certificado**, configure lo siguiente:

  -   Habilite la opción **Permitir que se pueda exportar la clave privada**.

  -   Establezca **Uso de claves** en firma digital.

  -   Establezca **Tamaño mínimo de clave** en un valor igual o mayor que 2048 bits.

  Use la opción **Quitar** para quitar un certificado del almacén de certificados de WSUS. Esta opción está disponible cuando el servidor de actualización es local con respecto a la consola de Updates Publisher que se use o cuando se usa **SSL** para conectarse a un servidor de actualización remoto.

## <a name="configmgr-server"></a>Servidor de Configuration Manager
Use estas opciones cuando utilice Configuration Manager con Updates Publisher.

-   **Specify the Configuration Manager server** (Especificar el servidor de Configuration Manager): después de habilitar la configuración con Configuration Manager, especifique la ubicación del servidor del sitio de nivel superior de la jerarquía de Configuration Manager. Si ese servidor es remoto con respecto a la instalación de Updates Publisher, especifique el FQDN del servidor del sitio. Elija **Prueba de conexión** para asegurarse de que se puede conectar al servidor del sitio.

-   **Configure thresholds** (Configurar umbrales): los umbrales se usan cuando se publican actualizaciones con el tipo de actualización automático. Los valores de umbral ayudan a determinar cuando se publica el contenido completo de una actualización en lugar de solo los metadatos. Para obtener más información sobre tipos de publicación, vea [Assign updates to a publication](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) (Asignar actualizaciones a una publicación).

    Puede habilitar uno de los siguientes conjuntos de reglas, o bien ambos:

    -   **Requested client count threshold** (Umbral de cuenta de clientes solicitados): este umbral define cuántos clientes deben solicitar una actualización para que Updates Publisher pueda publicar automáticamente el conjunto de contenido completo para esa actualización. Hasta que el número de clientes especificado soliciten la actualización, solo se publican los metadatos de las actualizaciones.

    -   **Package source size threshold (MB)** [Umbral de tamaño de origen del paquete (MB]): esta opción impide la publicación automática de actualizaciones que superen el tamaño especificado. Si el tamaño de las actualizaciones supera este valor, solo se publican los metadatos. Las actualizaciones de tamaño menor que el especificado pueden tener publicado su contenido completo.

## <a name="proxy-settings"></a>Configuración de proxy
Updates Publisher usa la configuración de proxy cuando se importan catálogos de software desde Internet o se publican actualizaciones en Internet.

-   Especifique el FQDN o la dirección IP de un servidor proxy. Se admiten IPv4 y IPv6.

-   Si el servidor proxy autentica usuarios para el acceso a Internet, debe especificar el nombre de Windows. No se admite un nombre principal de usuario (UPN).

## <a name="trusted-publishers"></a>Editores de confianza
Cuando se importa un catálogo de actualizaciones, se agrega el origen del catálogo (según su certificado) a un editor de confianza. De manera similar, cuando se publica una actualización, el origen del certificado de las actualizaciones se agrega como editor de confianza.

Puede ver los detalles del certificado de cada editor y quitar un editor de la lista de editores de confianza.

El contenido de editores que no son de confianza puede dañar los equipos cliente cuando el cliente busca actualizaciones. Solo debe aceptar contenido de editores en los que confíe.

## <a name="advanced"></a>avanzadas
Las opciones avanzadas incluyen:

-   **Ubicación del repositorio**: vea y modifique la ubicación del archivo de base de datos, **scupdb.sdf**. Este archivo es el repositorio de Updates Publisher.

-   **Marca de tiempo**: cuando se habilita, se agrega a las actualizaciones que firma una marca de tiempo que identifica cuándo se firmó. Una actualización que se firme mientras un certificado sea válido se puede usar después de que el certificado expire. De manera predeterminada, las actualizaciones de software no se pueden implementar después de que su certificado de firma expire.

-   **Check for updates to subscribed catalogs** (Buscar actualizaciones de catálogos suscritos): cada vez que Updates Publisher se inicia, puede buscar automáticamente actualizaciones de los catálogos a lo que se haya suscrito. Cuando se encuentra una actualización de catálogo, se ofrecen detalles como **Alertas recientes** en la ventana **Introducción** del **área de trabajo Actualizaciones**.

-   **Revocación de certificados**: elija esta opción para habilitar comprobaciones de revocación de certificados.

-   **Local source publishing** (Publicación de origen local): Updates Publisher puede usar una copia local de una actualización que publique antes de descargar esa actualización de Internet. La ubicación puede ser una carpeta en el equipo que ejecuta Updates Publisher. De manera predeterminada, esta ubicación es **Mis documentos\LocalSourcePublishing.** Úsela cuando haya descargado una o más actualizaciones anteriormente o haya realizado modificaciones a una actualización que quiera implementar.

-   **Software Updates Cleanup Wizard** (Asistente para la limpieza de actualizaciones de software): inicia el asistente para la limpieza de actualizaciones. El asistente hace que expiren las actualizaciones que están en el servidor de actualización pero no en el repositorio de Updates Publisher. Vea [Expire unreferenced updates](#expire-unreferenced-software-updates) (Expirar actualizaciones sin referencia) para obtener más información.

## <a name="updates"></a>Updates
 Updates Publisher puede buscar nuevas actualizaciones automáticamente cada vez que se abre. También puede optar por recibir compilaciones de vista previa de Updates Publisher.

Para buscar actualizaciones manualmente, haga clic en ![Propiedades](media/properties2.png) en la consola de Updates Publisher  
para abrir **Propiedades de Updates Publisher** y elija **Buscar actualización**.

Cuando Updates Publisher encuentra una nueva actualización, muestra la ventana **Actualización disponible** y se tiene la posibilidad de instalarla. Si opta por no instalar la actualización, la próxima vea que abra la consola se le ofrecerá esa posibilidad.

## <a name="logging"></a>Registro
Updates Publisher registra información básica sobre Updates Publisher en **%WINDIR%\Temp\UpdatesPublisher.log**.

Use el Bloc de notas o **CMTrace** para ver el registro. CMTrace es la herramienta de archivos de registro de Configuration Manager que se encuentra en la carpeta **SMSSetup\Tools**Tools del medio de origen de Configuration Manager.

Puede cambiar el tamaño del registro y su nivel de detalle.

Cuando habilita el registro de la base de datos, se incluye la información sobre las consultas que se ejecutan en la base de datos de Updates Publisher. El uso del registro de la base de datos puede traducirse en un rendimiento menor del equipo de Updates Publisher.

Para ver el archivo de registro, haga clic en ![Propiedades](media/properties2.png) en la consola para abrir las **Propiedades de Updates Publisher** y elija **Ver archivo de registro**.

## <a name="expire-unreferenced-software-updates"></a>Expirar actualizaciones de software sin referencia
Puede ejecutar el **Software Updates Cleanup Wizard** (Asistente para la limpieza de actualizaciones de software) para hacer expirar actualizaciones que se encuentran en el servidor de actualización pero no en el repositorio de Updates Publisher. Este se lo notifica a Configuration Manager que luego quita esas actualizaciones de las implementaciones futuras.

El acto de hacer expirar una actualización es irreversible. Realice esta tarea solo cuando esté seguro de que las actualizaciones de software que selecciona ya no sean necesarias en la organización.

### <a name="to-remove-expired-software-updates"></a>Para quitar actualizaciones de software expiradas
1.  Haga clic en ![Propiedades](media/properties2.png) en la consola de Updates Publisher para abrir las **Propiedades de Updates Publisher** y elija **Opciones**.

2.  Elija **Avanzadas** y luego, en **Software Update Clean Wizard** (Asistente para la limpieza de actualizaciones de software), elija **Iniciar**.

3.  Seleccione las actualizaciones software que quiere que expiren y elija **Siguiente**.

4.  Después de revisar las selecciones, elija **Siguiente** para aceptarlas y hacer expirar esas actualizaciones.

5.  Cuando el asistente termine, elija **Cerrar** para finalizar el asistente.
