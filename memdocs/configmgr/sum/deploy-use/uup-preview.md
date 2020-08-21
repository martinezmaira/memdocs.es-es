---
title: Versión preliminar de UUP
titleSuffix: Configuration Manager
description: Instrucciones para la versión preliminar de la integración de UUP
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c37fab775cdb90667ff1bc9f77dbbcaa1864b6f0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696793"
---
# <a name="uup-private-preview-instructions"></a>Instrucciones de la versión preliminar privada de UUP

> [!Note]  
> Esta información está relacionada con una característica en versión preliminar que se puede modificar sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

## <a name="introduction"></a>Introducción

La Plataforma de actualización unificada (UUP) es la plataforma de empaquetado y publicación que usan los dispositivos de consumidor y de empresa para recibir actualizaciones de Windows Update para empresas. El programa de versión preliminar privada de UUP está destinado a los clientes que han acordado ayudar a Microsoft a validar el uso de las actualizaciones de UUP en Configuration Manager, a fin de solventar los problemas que los clientes notifican relacionados con el mantenimiento de Windows en la actualidad. En este momento, estas actualizaciones no están disponibles públicamente.

Para más información sobre UUP, consulte la siguiente entrada de blog de Windows: [Actualización en nuestra plataforma de actualización unificada (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Ventajas

La característica de UUP y las actualizaciones acumulativas de Windows 10 ayudan a resolver muchos de los problemas que los clientes notifican relacionados con el mantenimiento de Windows hoy en día.

### <a name="feature-updates"></a>Actualizaciones de características

- Con la actualización de características de UUP, el proceso de Windows Update conserva características a petición (FOD) y paquetes de idioma.

- Actualice directamente al nivel de cumplimiento de seguridad más reciente. No es necesario instalar actualizaciones de seguridad justo después de una actualización de características. Microsoft publica una nueva actualización de características cada mes con la actualización de seguridad acumulativa más reciente. No es necesario descargar o distribuir la mayor parte del contenido de actualización de características cada mes. Solo se descarga la actualización de seguridad, que UUP comparte con la actualización acumulativa.

### <a name="cumulative-updates"></a>Actualizaciones acumulativas

- Las actualizaciones acumulativas con UUP incluyen actualizaciones de la pila de servicio (SSU) con actualizaciones mensuales de seguridad acumulativas. Este comportamiento solucionó dificultades con la organización de estas dos actualizaciones. Permite garantizar que las actualizaciones de la pila de servicio se han implementado para instalar las actualizaciones acumulativas. No es necesario administrar y organizar estas relaciones.

- Las actualizaciones acumulativas con UUP permiten distribuir el contenido de FOD y de los paquetes de idioma sin conexión. Este comportamiento permite a los usuarios agregarlos a petición. Los usuarios no tienen que descargar nada de Internet y no es necesario averiguar cómo preconfigurar el contenido.

## <a name="set-up"></a>Configuración

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. Enviar el identificador de WSUS a Microsoft

Para participar en la versión preliminar privada de UUP, comparta su identificador de WSUS con su persona de contacto de la versión preliminar de UUP. Microsoft aprobará su entorno de WSUS en el programa de versión preliminar de UUP. Sin este identificador, no podrá ver las actualizaciones de UUP hasta que la versión preliminar sea pública.

Para obtener el identificador de WSUS, ejecute el siguiente script de PowerShell:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

La propiedad **MUUrl** debe ser `https://sws.update.microsoft.com`. Para cambiarla, vea la resolución en este artículo de soporte técnico: [Se produce un error en la sincronización de WSUS con excepción SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)

### <a name="2-update-configuration-manager"></a>2. Actualizar Configuration Manager

Realice los siguientes cambios en el sitio de Configuration Manager para admitir esta versión preliminar de UUP:

#### <a name="diagnostics-and-usage-data-level"></a>Diagnósticos y nivel de datos de uso

Considere la posibilidad de aumentar el nivel de uso de datos y de diagnóstico de Configuration Manager durante esta versión preliminar. Mediante el nivel **Completo**, Microsoft puede analizar y solucionar los problemas relacionados con esta nueva característica. Para más información, consulte [Niveles de recopilación de datos de uso y diagnóstico en la versión 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>Instalar la actualización más reciente

1. Actualice el sitio con una de las siguientes actualizaciones:

    - Versión 1902 con el [paquete acumulativo de actualizaciones](https://support.microsoft.com/help/4500571)
    - [Versión 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](../../core/servers/manage/install-in-console-updates.md).

2. Actualice los clientes.  

    - Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - Para evitar la *descarga innecesaria de unos 6 GB* de contenido no usado al cliente, actualice todos los clientes a los que destine las actualizaciones de UUP.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Actualizar los clientes de Windows a una versión compatible

Para que las actualizaciones de UUP se instalen correctamente, instale estas dos actualizaciones:

1. Un nivel de cumplimiento mensual acumulativo mínimo específico.

2. Una actualización específica no acumulativa que no sea de seguridad del Catálogo de Microsoft Update. Para importar la actualización en Configuration Manager para su implementación, consulte [Importación de actualizaciones desde el Catálogo de Microsoft Update](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Versiones admitidas de Windows 10 y actualizaciones necesarias

| Versión de Windows 10 | Nivel de cumplimiento mínimo | Actualización del catálogo adicional |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, versión 1903** | RTM | 7 de noviembre de 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, versión 1809** | Agosto de 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 de noviembre de 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, versión 1803** | Abril de 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 de noviembre de 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, versión 1709** | Abril de 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 de noviembre de 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Si aplica las actualizaciones del 12 de noviembre de 2019 al cliente antes de aplicar la actualización del catálogo adicional del 7 de noviembre de 2019, se sobrescribirán los cambios del Agente de Windows Update necesarios para admitir UUP. Para corregir los clientes en este escenario, aplique la actualización del catálogo adicional después de instalar las actualizaciones del 12 de noviembre de 2019.
> - Si aplica una actualización de características al cliente, tendrá que volver a instalar la actualización del catálogo adicional una vez que se haya completado la actualización.
> - Para que sea más fácil probar las actualizaciones de características, importe las actualizaciones en Configuration Manager. Para obtener más información, consulte [Importación de actualizaciones desde el Catálogo de Microsoft Update](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). Una vez completada la actualización de características, se muestra la actualización del catálogo adicional **según sea necesario**, lo que permite la implementación automática en la versión del sistema operativo de nivel superior.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. Permitir que los clientes descarguen contenido diferencial cuando esté disponible

Para que las actualizaciones de UUP se descarguen correctamente, habilite la configuración del cliente en **Permitir que los clientes descarguen contenido diferencial cuando esté disponible**. Mediante esta configuración, Configuration Manager permite que el Agente de Windows Update (WUA) determine el contenido necesario que se debe descargar en los clientes. Este comportamiento reemplaza al predeterminado, según el cual el cliente de Configuration Manager descarga todo el contenido asociado a la actualización de UUP. Cuando se habilita esta opción, WUA determina el contenido adicional que se necesita de cada actualización de UUP. Por ejemplo, solo los paquetes de idioma y FOD necesarios.

Cuando se habilita esta configuración, no afecta a las descargas de Internet de contenido del servidor. Solo se aplica a las descargas del cliente. Antes de implementar las actualizaciones de UUP en los clientes, aplique esta configuración a los que tengan las versiones compatibles con UUP. Las actualizaciones de cliente de requisitos previos corrigen los problemas de compatibilidad de las actualizaciones de UUP en WSUS y Configuration Manager.

Para más información sobre esta configuración de cliente, consulte [Información sobre la configuración de cliente: actualizaciones de software](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available).

### <a name="5-review-your-software-update-infrastructure"></a>5. Revisar la infraestructura de actualizaciones de software

Antes de sincronizar las actualizaciones de UUP, revise las reglas de implementación automática (ADR) y los planes de mantenimiento. Si no quiere que estas actualizaciones se implementen automáticamente, revise las ADR para filtrarlas. Para obtener más información, vea [Cómo buscar actualizaciones de UUP sincronizadas](#how-to-find-synced-uup-updates). De forma predeterminada, los planes de mantenimiento existentes solo implementan actualizaciones que no sean de UUP. Puede modificar los planes de mantenimiento para cambiar este comportamiento.

Revise los informes de cumplimiento y adapte lo necesario. Por ejemplo, si mide el cumplimiento en todos los productos, ahora verá tanto las actualizaciones acumulativas de UUP como las que no son de UUP. Los dispositivos informarán del cumplimiento de ambos tipos de actualizaciones. Asegúrese de que los informes de cumplimiento tengan en cuenta este cambio.

## <a name="enable-uup-and-start-testing"></a>Habilitar UUP e iniciar las pruebas

### <a name="select-products-and-classifications-to-sync"></a>Selección de productos y clasificaciones para sincronizar

Una vez que esté listo para iniciar la sincronización de las actualizaciones de UUP y que Microsoft haya aprobado su identificador de WSUS, habilite los nuevos productos:

1. [Sincronice las actualizaciones de software](../get-started/synchronize-software-updates.md) para rellenar los productos nuevos.  

2. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.

3. Seleccione el sitio de nivel superior, que será un sitio de administración central (CAS) o uno primario independiente.

4. En la cinta, seleccione **Configurar componentes de sitio** y elija **Punto de actualización de software**.

5. Vaya a la pestaña **Productos** y seleccione uno o varios de los productos siguientes: 

    - **Versión preliminar de UUP de Windows 10**
    - **Versión preliminar de UUP de Windows Server**

6. Vaya a la pestaña **Clasificaciones** y seleccione las opciones siguientes:  

    - **Actualizaciones de seguridad**: Para ver las actualizaciones acumulativas de UUP  
    - **Actualizaciones**: Para ver las actualizaciones de características de UUP:  

7. Vuelva a sincronizar las actualizaciones de software para ver las actualizaciones de UUP nuevas.

### <a name="how-to-find-synced-uup-updates"></a>Cómo buscar actualizaciones de UUP sincronizadas

Después de sincronizar las actualizaciones de UUP en el entorno, búsquelas en la consola de Configuration Manager para realizar pruebas. Hay dos formas de buscar las actualizaciones de versión preliminar:

- Como estas actualizaciones de versión preliminar se encuentran en productos independientes, use el producto para filtrarlas o buscarlas. Use el filtro de productos del plan de mantenimiento para implementar las actualizaciones de características que son de UUP y las que no lo son.  

- En los nodos **Todas las actualizaciones de software** y **Todas las actualizaciones de Windows 10** de la **Biblioteca de software**, hay una columna opcional nueva, **Etiqueta**. Esta propiedad también está disponible como filtro en las ADR. En el caso de las actualizaciones de UUP, busque `UUP` en este campo. Está en blanco para las actualizaciones que no son de UUP.  

### <a name="updates-available-during-preview"></a>Actualizaciones disponibles durante la versión preliminar

Para obtener más información sobre todas las actualizaciones de Windows 10 que ha publicado Microsoft, consulte [Información de versión de Windows 10](/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Actualizaciones acumulativas para pruebas

Aunque probablemente verá disponibles varias actualizaciones con la etiqueta UUP, comience con la actualización de **septiembre de 2019** (2019-09) o una versión posterior. Por ejemplo:

- 2019-09 Actualización acumulativa para Windows 10, versión 1809, para sistemas basados en x64 (KB4512578)
- 2019-09 Actualización acumulativa para Windows 10, versión 1803, para sistemas basados en x64 (KB4516058)
- 2019-09 Actualización acumulativa para Windows 10, versión 1709, para sistemas basados en x64 (KB4516066)

#### <a name="feature-updates-to-test"></a>Actualizaciones de características para pruebas

Aunque probablemente verá disponibles varias actualizaciones con la etiqueta UUP, comience con la actualización de **septiembre de 2019** (2019-09B) o una versión posterior. Por ejemplo:

- Actualización de características a Windows 10, versión 1809, x64 2019-09B
- Actualización de características a Windows 10, versión 1803, x64 2019-09B

## <a name="scenarios-to-test"></a>Escenarios para pruebas

### <a name="test-feature-updates"></a>Actualizaciones de características de prueba

- Actualice directamente al nivel de cumplimiento de seguridad elegido.  

- Instale los paquetes de idioma y FOD antes de la actualización. Asegúrese de que la actualización conserva estos componentes.  

### <a name="test-cumulative-updates"></a>Actualizaciones acumulativas de prueba

Durante la versión preliminar, mantenga el cumplimiento normativo de los clientes con la actualización de tipo de UUP durante varias actualizaciones consecutivas. Esta prueba le ayudará a comprender el comportamiento en curso.

### <a name="test-content"></a>Contenido de prueba

La primera actualización para cada combinación de versión principal (1809, 1803, 1709), arquitectura e idioma parecerá ser grande, tanto en número de archivos como en espacio en disco, en comparación con lo que ya ha visto en las actualizaciones que no son de UUP. Este contenido adicional es principalmente para todos los paquetes de idioma y FOD para las actualizaciones acumulativas. En el caso de las actualizaciones de características, hay contenido adicional de tamaño considerable para esa primera actualización.

Para futuras actualizaciones acumulativas y de características, la cantidad de contenido nuevo que el sitio descarga y distribuye es mucho menor. UUP comparte de forma inteligente todo el contenido de FOD y de los paquetes de idioma entre las actualizaciones. No es necesario volver a descargar o redistribuir este contenido compartido. Durante la versión preliminar, en las versiones 1709 y 1803 de Windows 10, esta descarga mensual tiene aproximadamente el mismo tamaño que las actualizaciones acumulativas que se ven en los escenarios que no son de UUP. En Windows 10, versión 1809 y posteriores, la descarga incremental de la actualización acumulativa es mucho menor cada mes.

Al examinar el contenido total *que no es rápido* que se descarga y se distribuye a lo largo de un período de 12 meses, la versión 1803 de Windows 10 sin UUP debería ser prácticamente igual a la versión 1809 con UUP. El contenido total que se descarga y se distribuye durante todo el ciclo de vida de la versión es menor en la 1809 con UUP.

### <a name="supported-content-channels"></a>Canales de contenido admitidos

Para la versión preliminar, pruebe escenarios típicos reales. UUP es compatible con todos los canales de contenido, incluidos:

- Optimización de distribución (DO) de Windows
  - Cuando use DO, asegúrese de que se ha configurado correctamente. Para obtener más información, vea [Optimización de la distribución de actualizaciones de Windows 10](optimize-windows-10-update-delivery.md).
- Caché del mismo nivel de Configuration Manager
- Windows BranchCache
- Use la opción **sin paquete de implementación** y la descarga de los clientes directamente desde Microsoft Update. Use esta opción con la optimización de entrega.
- Proveedores de contenido alternativos de terceros

Para obtener más información sobre los canales de contenido, vea [Optimización de la distribución de actualizaciones de Windows 10](optimize-windows-10-update-delivery.md).

<!-- TODO: Addlink to WSUS Perf documentation-->