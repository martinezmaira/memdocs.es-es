---
title: Preparar la instalación de sitios
titleSuffix: Configuration Manager
description: Si tiene previsto instalar varios sitios de Configuration Manager, lea esta información para ahorrar tiempo y evitar errores.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700723"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Preparar la instalación de sitios de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para preparar una implementación correcta de uno o varios sitios de Configuration Manager, debe familiarizarse con la información descrita en este artículo. Estos pasos le pueden ahorrar tiempo a la hora de instalar varios sitios y pueden evitar que se lleven a cabo pasos incorrectos, con lo que se tendrían que volver a instalar los sitios.

> [!TIP]
> Al administrar el sitio de Configuration Manager y la infraestructura de la jerarquía, los términos *mejorar*, *actualizar* e *instalar* se utilizan para describir los tres conceptos diferentes. Para obtener información sobre cómo se usa cada término, vea [Acerca de la actualización e instalación](../../../understand/upgrade-update-install.md).

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Opciones para instalar los diferentes tipos de sitios
Al instalar un sitio de Configuration Manager nuevo, la versión de los archivos de origen que se pueden usar depende de la versión de los sitios que ya están en la jerarquía (en caso de que haya). Los métodos de instalación disponibles dependen del tipo de sitio que quiera instalar.  

Antes de instalar un sitio, asegúrese de que ha planeado la jerarquía y de que conoce el tipo de sitio que quiere instalar. Para obtener más información, consulte [Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Diseñar una jerarquía de sitios).


### <a name="first-site"></a>Primer sitio
El primer sitio que se instale en una jerarquía será un sitio primario independiente o un sitio de administración central.

**Medios de instalación**: para instalar un sitio de administración central o un sitio primario independiente como primer sitio de una nueva jerarquía, debe [usar una versión de línea base](../../../../core/servers/manage/updates.md#bkmk_Baselines) de Configuration Manager. No instale el primer sitio de una jerarquía nueva con los archivos de origen actualizados desde la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de cualquier sitio.

**Método de instalación**: puede instalar cualquier tipo de sitio mediante el [Asistente para instalación de Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md); también puede configurar un script para usarlo con una [instalación de línea de comandos generada por scripts](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sitios adicionales
Una vez instalado el sitio inicial, puede agregar más sitios en cualquier momento. Existen las siguientes opciones para agregar sitios (hasta los [límites admitidos](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Sitio que tiene|Tipo de sitio adicional que puede instalar|
|---|---|
|Sitio de administración central|Sitio primario secundario|
|Sitio primario secundario|Sitio secundario|
|Sitio primario independiente|Sitio secundario (puede expandir el sitio primario, lo cual convierte el sitio primario independiente en un sitio primario secundario)|

**Medios de instalación**: al instalar un sitio de administración central para expandir un sitio primario independiente, o al instalar un nuevo sitio primario secundario en una jerarquía existente, debe usar medios de instalación (que contienen archivos de origen) que coincidan con la versión de los sitios existentes.

> [!IMPORTANT]
> Si ha instalado actualizaciones en la consola que han cambiado la versión de los sitios instalados previamente, no use los medios de instalación originales. En su lugar, use archivos de origen de la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de un sitio actualizado. Configuration Manager requiere el uso de archivos de origen que coincidan con la versión del sitio existente al que se conectará el nuevo sitio.

Es necesario instalar un sitio secundario desde la consola de Configuration Manager. De este modo, los sitios secundarios siempre se instalan mediante los archivos de origen del sitio primario principal.

**Método de instalación**: el método empleado para instalar sitios adicionales depende del tipo de sitio que quiera instalar.
- **Agregar un sitio de administración central**:  puede usar el Asistente para instalación de Configuration Manager o una línea de comandos generada por scripts para instalar el nuevo sitio de administración central como sitio primario en el sitio primario independiente existente. Para obtener más información, vea [Expandir un sitio primario independiente](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Agregar un sitio primario secundario**:  puede usar el Asistente para instalación de Configuration Manager o una instalación de línea de comandos para agregar un sitio primario secundario debajo de un sitio de administración central.
- **Agregar un sitio secundario**:  use la consola de Configuration Manager para instalar un sitio secundario debajo de un sitio primario. No se admiten otros métodos para agregar sitios secundarios.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a> Tareas comunes que se deben realizar antes de iniciar una instalación
- **Analice la topología de la jerarquía que se usará para la implementación**    
Para más información, vea [Diseñar una jerarquía de sitios para Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Prepare y configure servidores para cumplir los requisitos previos y las configuraciones admitidas para usarlos con Configuration Manager**         
Para obtener más información, consulte [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

- **Instale y configure SQL Server para hospedar la base de datos del sitio**     
Para más información, vea [Versiones de SQL Server compatibles con Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Prepare el entorno de red para admitir Configuration Manager**      
Para obtener más información, vea [Configurar firewalls, puertos y dominios para System Center Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Si va a usar una infraestructura de clave pública (PKI), prepare su infraestructura y certificados**      
Para obtener más información, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Instale las actualizaciones de seguridad más recientes en los equipos que va a usar como servidores de sitio o servidores del sistema de sitio y, si es necesario, reinícielos**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Acerca de los nombres de sitio y los códigos de sitio
Para identificar y administrar los sitios en una jerarquía de Configuration Manager se usan códigos y nombres de sitio. En la consola de Configuration Manager, el código y el nombre de sitio se muestran con el formato &lt;*código de sitio*\> - &lt;*nombre de sitio*\>. Los códigos de sitio que use en su jerarquía deben ser únicos. Si el esquema de Active Directory se extiende para Configuration Manager y los sitios publican datos, los códigos de sitio que se usan en un bosque de Active Directory deben ser únicos incluso si se usan en otra jerarquía de Configuration Manager o si se han usado en instalaciones anteriores de Configuration Manager. Asegúrese de planear cuidadosamente sus códigos y nombres de sitio antes de implementar su jerarquía.

### <a name="specify-a-site-code-and-site-name"></a>Especificar un nombre de sitio y un código de sitio
Cuando ejecuta el programa de instalación de Configuration Manager, se le solicita que proporcione un código de sitio y un nombre de sitio para el sitio de administración central y para la instalación de los sitios primarios y secundarios. El código de sitio debe identificar de manera única cada sitio en la jerarquía. Dado que el código de sitio se usa en nombres de carpetas, nunca use los siguientes nombres para el código de sitio, entre los que se incluyen nombres reservados para Configuration Manager y para Windows:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> El programa de instalación de Configuration Manager no comprueba si un código de sitio ya está en uso.

Para especificar el código de sitio de un sitio mientras se ejecuta el programa de instalación de Configuration Manager, debe escribir tres caracteres alfanuméricos. En los códigos de sitio solo se permiten las letras de la a *A* a la *Z* y los números del *0* al *9*, en cualquier combinación. La secuencia de letras o números no tiene ningún efecto en la comunicación entre sitios. Por ejemplo, no es necesario asignar el nombre *ABC* a un sitio primario y el nombre *DEF* a un sitio secundario.

El nombre del sitio es un identificador de nombre descriptivo del sitio. Solo se pueden usar los caracteres de la *A* a la *Z*, de la *a* a la *z*, del *0* al *9* y el guión ( *-* ) en los nombres de sitio.

> [!IMPORTANT]
> No se puede cambiar el código o el nombre de sitio después de instalar el sitio.

### <a name="reuse-a-site-code"></a>Volver a usar un código de sitio
Los códigos de sitio no se pueden usar más de una vez en una jerarquía de Configuration Manager para un sitio de administración central o para un sitio primario, aunque se hayan desinstalado el código de sitio y el sitio original. Si vuelve a usar un código de sitio, corre el riesgo de que se produzcan conflictos de identificador de objeto en su jerarquía. Puede volver a usar el código de sitio de un sitio secundario si ninguno de estos se usan más en la jerarquía de Configuration Manager o en el bosque de Active Directory.

## <a name="limits-and-restrictions-for-installed-sites"></a>Límites y restricciones de los sitios instalados
Antes de instalar un sitio, debe comprender las siguientes limitaciones que se aplican a los sitios y las jerarquías:
- Después de ejecutar el programa de instalación, no podrá cambiar las siguientes propiedades del sitio a menos que lo desinstale y lo vuelva a instalar con los nuevos valores:  
  - Directorio de instalación de archivos de programa  
  - Código de sitio  
  - Descripción del sitio  
- Si la jerarquía incluye un sitio de administración central:  
  - Configuration Manager no admite mover un sitio primario secundario fuera de una jerarquía para crear un sitio primario independiente o para adjuntarlo a otra jerarquía. En su lugar, desinstale el sitio primario secundario y, luego, vuelva a instalarlo como un nuevo sitio primario independiente o como un sitio secundario del sitio de administración central de otra jerarquía.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a> Pasos opcionales antes de ejecutar el programa de instalación
**Ejecutar manualmente el [descargador del programa de instalación](../../../../core/servers/deploy/install/setup-downloader.md)**

Para descargar los archivos de instalación actualizados para Configuration Manager, puede ejecutar el descargador del programa de instalación. Si el equipo en el que se ejecutará el programa de instalación no está conectado a Internet, o bien si tiene previsto instalar varios servidores de sitio, le recomendamos que use el descargador del programa de instalación para descargar las actualizaciones necesarias para la instalación. A continuación encontrará información adicional:
- De forma predeterminada, el programa de instalación se conecta a Internet para descargar archivos de instalación actualizados.
- De forma predeterminada, los archivos se almacenan en la carpeta Redist.
- Puede dirigir el programa de instalación a una ubicación de red en la que haya almacenado previamente una copia de estos archivos.

**Ejecutar manualmente el [Comprobador de requisitos previos](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Para identificar y corregir problemas antes de ejecutar el programa de instalación para instalar un sitio y antes de instalar un rol de sistema de sitio en un servidor, puede ejecutar el Comprobador de requisitos previos. El Comprobador de requisitos previos ayuda a garantizar que el equipo cumple los requisitos para hospedar el sitio o el rol de sistema de sitio. A continuación encontrará información adicional:
- De forma predeterminada, el programa de instalación ejecuta el Comprobador de requisitos previos.
- Si se detectan errores, el programa de instalación se detiene hasta que se solucione el problema.

**Identificar puertos opcionales**

Puede identificar los puertos opcionales que los sistemas de sitio y los clientes pueden usar. A continuación encontrará información adicional:
- De forma predeterminada, los sistemas de sitio y los clientes usan puertos predefinidos para comunicarse.
- Durante la instalación, puede configurar puertos alternativos.

Para más información, vea [Puertos usados](../../../../core/plan-design/hierarchy/ports.md).
