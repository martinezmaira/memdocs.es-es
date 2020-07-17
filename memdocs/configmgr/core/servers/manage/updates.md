---
title: Actualizaciones y mantenimiento
titleSuffix: Configuration Manager
description: Conozca el método de servicio en la consola denominado Actualizaciones y mantenimiento con el que es más fácil encontrar e instalar actualizaciones recomendadas.
ms.date: 06/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5eb1a5ef844a8dbf94cbde9d2c99986ce0634260
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422802"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Actualizaciones y servicio para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager usa un método de servicio en la consola denominado **Actualizaciones y mantenimiento**. Este método en la consola facilita la búsqueda e instalación de actualizaciones recomendadas para su infraestructura de Configuration Manager. El servicio en la consola se complementa con actualizaciones fuera de banda, como revisiones. Las actualizaciones fuera de banda están destinadas a los clientes que necesitan solucionar problemas que pueden ser específicos para su entorno.  

> [!TIP]  
> Los términos *actualizar* e *instalar* se usan para describir dos conceptos independientes en Configuration Manager. Para obtener más información sobre cómo se usa cada término, vea [Acerca de la actualización e instalación](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Versiones de línea de base y versiones de actualización  

Use la versión de línea de base más reciente cuando instale un sitio nuevo en una jerarquía nueva.

- Además, use una versión de línea base para actualizar desde System Center 2012 Configuration Manager.  

- Después de actualizar a la rama actual de Configuration Manager, no use las versiones de línea base para mantenerse al día. Use solo [actualizaciones en la consola](install-in-console-updates.md) para actualizar a la versión más reciente.  

- Las versiones de línea de base adicionales se publican periódicamente. Al usar la versión de línea base más reciente para instalar una nueva jerarquía, evita tener que instalar una versión obsoleta o no compatible de Configuration Manager y luego una actualización adicional de su infraestructura para actualizarla.  

Una vez que instala una versión de línea de base, las versiones adicionales de Configuration Manager se encuentran disponibles como actualizaciones en la consola. Las actualizaciones en la consola actualizan la infraestructura a la versión más reciente de Configuration Manager.  

- Las actualizaciones en la consola se instalan para actualizar la versión del sitio de primer nivel.  

- Las actualizaciones que se instalan en el sitio de administración central se instalan automáticamente en los sitios primarios y secundarios. Controle esta sincronización mediante una ventana de mantenimiento en el sitio primario.  

- Actualice manualmente los sitios secundarios a una nueva versión de actualización desde la consola.  

Cuando instala una actualización, esta almacena los archivos de instalación de esa versión en el servidor de sitio, en una carpeta denominada **CD.Latest**. Para obtener más información sobre estos archivos, vea [La carpeta CD.Latest](the-cd.latest-folder.md).  

- Use los archivos de la carpeta CD.Latest durante la recuperación del sitio. Además, cuando la jerarquía ya no ejecute una versión de línea base, use estos archivos para instalar otros sitios.  

- No puede usar archivos de instalación de CD.Latest para instalar el primer sitio de una jerarquía nueva ni para actualizar un sitio desde System Center 2012 Configuration Manager.  

### <a name="version-details"></a>Detalles de la versión

Algunas actualizaciones de Configuration Manager se encuentran disponibles tanto como una versión de actualización en la consola para la infraestructura existente como una versión de línea de base nueva.  

#### <a name="supported-versions"></a>Versiones admitidas

Las siguientes versiones admitidas de Configuration Manager están actualmente disponibles como línea de base, actualización, o ambas:  

| Version | Fecha de disponibilidad | [Fecha de finalización del soporte técnico](current-branch-versions-supported.md) | Línea de base | Actualización en la consola |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1 de abril de 2020 | 1 de octubre de 2021 | Sí<sup>[Nota 1](#bkmk_note1)</sup> | Sí |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29 de noviembre de 2019 | 29 de mayo de 2021 | No | Sí |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26 de julio de 2019 | 26 de enero de 2021 | No | Sí |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27 de marzo de 2019 | 27 de septiembre de 2020 | Sí | Sí |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27 de noviembre de 2018 | 1 de diciembre de 2020 | No | Sí |

La **fecha de disponibilidad** es cuando se publica el [anillo de actualización inicial](checklist-for-installing-update-2002.md#early-update-ring). Los medios de línea base estarán disponibles en el Centro de servicios de licencias por volumen después de que la actualización esté disponible globalmente.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Nota 1:** </sup> El medio de línea de base está disponible como parte de las versiones siguientes en el [Centro de servicios de licencias por volumen](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
>
> - Microsoft Endpoint ConfigMgr (rama actual)
> - System Center Datacenter
> - System Center Standard  
>
> Por ejemplo, busque `Microsoft Endpoint Configmgr (current branch)` en el VLSC. Busque el medio de línea de base en la lista de archivos y descargue el de esa versión.  

#### <a name="historical-versions"></a>Historial de versiones

En la siguiente tabla se enumeran las versiones históricas de la rama actual de Configuration Manager que están fuera del soporte técnico:

| Version | Fecha de disponibilidad | Fecha de finalización del soporte técnico | Línea de base | Actualización en la consola |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31 de julio de 2018 | 31 de enero de 2020 | No | Sí |
| **1802** <br /> (5.00.8634) | 22 de marzo de 2018 | 22 de septiembre de 2019 | Sí | Sí |
| **1710** <br /> (5.00.8577) | 20 de noviembre de 2017 | 20 de mayo de 2019 | No | Sí |
| **1706** <br /> (5.00.8540) | 31 de julio de 2017 | 31 de julio de 2018 | No | Sí |
| **1702** <br /> (5.00.8498) | 27 de marzo de 2017 | 27 de marzo de 2018 | Sí | Sí |
| **1610** <br /> (5.00.8458) | 18 de noviembre de 2016 | 18 de noviembre de 2017 | No | Sí |
| **1606** <br /> (5.00.8412.1000) | 22 de julio de 2016 | 22 de julio de 2017 | No | Sí |
| **1606 con KB 3186654** <br />(5.00.8412.1307) | 12 de octubre de 2016 | 12 de octubre de 2017 | Sí | No |
| **1602** <br /> (5.00.8355) | 11 de marzo de 2016 | 11 de marzo de 2017 | No | Sí |
| **1511** <br /> (5.00.8325) | 8 de diciembre de 2015 | 8 de diciembre de 2016 | Sí | No |  

#### <a name="how-to-check-the-version"></a>Cómo comprobar la versión

Para comprobar la versión del sitio de Configuration Manager, en la consola, vaya a **Acerca de Configuration Manager** en la esquina superior izquierda. Este cuadro de diálogo muestra las versiones del sitio y la consola.  

> [!Note]  
> La versión de la consola es ligeramente distinta de la versión del sitio. La versión secundaria de la consola corresponde a la versión de lanzamiento de Configuration Manager. Por ejemplo, en Configuration Manager versión 1802, la versión de sitio inicial es 5.0.8634.1000 y la versión inicial de la consola es 5. **1802**.1082.1700. Los números de compilación (1082) y revisión (1700) pueden cambiar con futuras revisiones.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Actualizaciones y servicio en la consola  

Cuando usa una instalación lista para producción de la rama actual de Configuration Manager, la mayoría de las actualizaciones están disponibles con el canal **Actualizaciones y mantenimiento**. Este método identifica, descarga y pone a disposición las actualizaciones que se aplican a la versión y la configuración actual de la infraestructura. Incluye solo las actualizaciones que Microsoft recomienda para todos los clientes.

Estas actualizaciones incluyen:  

- Versiones nuevas, como las versiones 1906, 1910 o 2002.

- Actualizaciones que incluyen características nuevas para la versión actual.

- Revisiones para la versión de Configuration Manager que todos los clientes deben instalar.

    > [!Note]  
    > A partir de la versión 1902, ahora las revisiones en la consola tienen relaciones de sustitución. Para obtener más información, vea [Sustitución para las revisiones en la consola](#bkmk_supersede).

Las actualizaciones en la consola proporcionan mayor estabilidad y solucionan problemas comunes. Reemplazan los tipos de actualización vistos para versiones anteriores del producto por Service Packs, actualizaciones acumulativas, revisiones aplicables a todos los clientes y la extensión para Microsoft Intune.

Las actualizaciones en la consola se pueden aplicar a uno o varios de los siguientes sistemas:  

- Servidores de sitio principal y de administración central  

- Roles de sistema de sitio y servidores de sistema de sitio  

- Instancias del proveedor de SMS  

- Consolas de Configuration Manager  

- Clientes de Configuration Manager  

Configuration Manager detecta automáticamente las nuevas actualizaciones. Sincronice el punto de conexión de servicio de Configuration Manager con el servicio en la nube de Microsoft y tenga en cuenta los siguientes comportamientos:  

- Cuando el punto de conexión de servicio está en modo en línea, el sitio se sincroniza con Microsoft todos los días. Identifica automáticamente las nuevas actualizaciones que se aplican a la infraestructura. Para descargar las actualizaciones y los archivos redistribuibles, el equipo que hospeda el rol de sistema de sitio del punto de conexión de servicio usa el contexto **System** para acceder a las siguientes ubicaciones de Internet: go.microsoft.com y download.microsoft.com. Para obtener más información sobre otras ubicaciones usadas por el punto de conexión de servicio, vea [Requisitos de acceso a Internet](../deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

- Cuando el punto de conexión de servicio está en modo sin conexión, se usa la herramienta de conexión de servicio para realizar manualmente la sincronización con la nube de Microsoft. Para obtener más información, vea [Uso de la herramienta de conexión de servicio](use-the-service-connection-tool.md).  

- Las actualizaciones en la consola reemplazan la necesidad de ubicar e instalar de manera independiente las actualizaciones individuales, Service Packs y características nuevas.  

- Instale solo las actualizaciones en la consola que elija. Al instalar algunas actualizaciones, puede seleccionar las características individuales que quiere habilitar y usar. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](install-in-console-updates.md#bkmk_options).  

Cuando se instala una actualización en la consola, se produce el siguiente proceso:  

- Ejecuta automáticamente una comprobación de los requisitos previos. También puede ejecutar esta comprobación de forma manual antes de comenzar la instalación.  

- Se instala en el sitio de nivel superior del entorno. Este sitio es el sitio de administración central, si dispone de uno. En una jerarquía, la actualización se instala automáticamente en los sitios primarios. Controle cuándo se puede actualizar cada servidor de sitio primario mediante [Ventanas de servicio para servidores de sitio](service-windows.md).  

- Una vez que un servidor de sitio se actualiza, se actualizan automáticamente todos los roles de sistema de sitio afectados. Estos roles incluyen instancias del proveedor de SMS. Una vez que el sitio instala la actualización, las consolas de Configuration Manager también le piden al usuario de la consola que la actualice.  

- Si una actualización incluye el cliente de Configuration Manager, tiene la opción de probar la actualización en el entorno de preproducción o de aplicar la actualización de forma inmediata a todos los clientes.  

- Una vez que se actualiza un sitio principal, los sitios secundarios no se actualizan automáticamente. En lugar de eso, es usted quien debe iniciar manualmente la actualización de los sitios secundarios.  

> [!NOTE]  
> La rama actual de Configuration Manager, la rama de mantenimiento a largo plazo y la rama de Technical Preview son versiones distintas. Las actualizaciones que se aplican a una rama no están disponibles como actualizaciones en consola para las demás. Para más información sobre las diferentes ramas, consulte [¿Qué rama de Configuration Manager debo utilizar?](../../understand/which-branch-should-i-use.md).

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a> Sustitución para las revisiones en la consola

<!-- 3229613 -->
A partir de la versión 1902, ahora las revisiones en la consola tienen relaciones de sustitución. Cuando Microsoft publica una nueva revisión de Configuration Manager, en la consola no se mostrarán todas las revisiones que se han sustituido por esta nueva revisión. Este nuevo comportamiento permite determinar qué revisiones se van a instalar.

### <a name="supersedence-example"></a>Ejemplo de sustitución

Hay tres revisiones disponibles: Revisión A, Revisión B y Revisión C. La Revisión A se ha reemplazado por la Revisión B y esta por la Revisión C.

|Revisión A|Revisión B|Revisión C|Vista en la consola|
|--------|--------|--------|---------------|
|Sin instalar|Sin instalar|Sin instalar|Se muestran las tres revisiones|
|Instalado|Instalado|Sin instalar|La Revisión B se muestra como instalada<br/>La Revisión C se muestra como lista para instalar|
|Sin instalar|Sin instalar|Instalado|La Revisión C se muestra como instalada|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Revisiones fuera de banda  

Algunas revisiones se publican con disponibilidad limitada para abordar problemas concretos. Otras revisiones se aplican a todos los clientes, pero no se pueden instalar con el método en la consola. Estas revisiones se entregan fuera de banda y no se detectan desde el servicio en la nube de Microsoft.  

Normalmente, cuando se busca corregir o atajar un problema con la implementación de Configuration Manager, se puede obtener información sobre las revisiones fuera de banda desde los servicios de asistencia al cliente de Microsoft, en un artículo de Knowledge Base del servicio de soporte técnico de Microsoft o en el [blog del equipo de Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog).

Instale estas revisiones manualmente, mediante uno de estos dos métodos:  

### <a name="update-registration-tool"></a>Herramienta de registro de actualizaciones

Esta herramienta importa manualmente la revisión a la consola de Configuration Manager. Luego instala la actualización como si fuera una actualización en la consola que se detecta automáticamente.  

Este método se usa para las revisiones que usan la siguiente estructura de nombre de archivo:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Para obtener más información, vea [Use the update registration tool to import hotfixes](use-the-update-registration-tool-to-import-hotfixes.md) (Uso de la herramienta de registro de actualizaciones para importar revisiones).  

### <a name="hotfix-installer"></a>Instalador de revisiones

Use esta herramienta para instalar manualmente una revisión que no se puede instalar con el método en la consola.  

Este método se emplea para las correcciones que usan la siguiente estructura de nombre de archivo:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Para obtener más información, vea [Uso del instalador de revisiones para instalar actualizaciones](use-the-hotfix-installer-to-install-updates.md).  

## <a name="next-steps"></a>Pasos siguientes

Los siguientes artículos pueden ayudarle a obtener información sobre cómo encontrar e instalar los distintos tipos de actualizaciones para Configuration Manager:  

- [Instalación de actualizaciones en la consola](install-in-console-updates.md)  

- [Uso de la herramienta de conexión de servicio](use-the-service-connection-tool.md)  

- [Uso de la herramienta de registro de actualizaciones para importar revisiones](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Uso del instalador de revisiones para instalar actualizaciones](use-the-hotfix-installer-to-install-updates.md)  

Para más información sobre la rama Technical Preview, vea [Technical Preview](../../get-started/technical-preview.md).
