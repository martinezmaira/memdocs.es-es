---
title: Carpeta CD.Latest
titleSuffix: Configuration Manager
description: Obtenga información sobre el proceso que proporciona actualizaciones al producto desde la consola de Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704053"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>La carpeta CD.Latest para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager dispone de un proceso que proporciona actualizaciones al producto desde su consola. Para admitir este nuevo método de actualización de Configuration Manager, se crea una nueva carpeta con el nombre **CD.Latest**. Esta carpeta contiene una copia de los archivos de instalación de Configuration Manager para la versión actualizada de su sitio.  

La carpeta CD.Latest contiene una carpeta denominada **Redist** que contiene los archivos redistribuibles que configuran las descargas y los usos. Estos archivos coinciden con la versión de los archivos de Configuration Manager que se encuentran en la carpeta CD.Latest. Al ejecutar el programa de instalación desde una carpeta CD.Latest más reciente, debe utilizar los archivos que coincidan con esa versión del programa de instalación. Puede dirigir el programa de instalación para descargar los archivos nuevos y actuales de Microsoft o dirigir el programa de instalación para utilizar los archivos desde la carpeta Redist incluida en la carpeta CD.Latest.

El medio de línea de base no incluye una carpeta **Redist**. El sitio no crea una carpeta Redist hasta que instale una actualización en la consola. Mientras tanto, use la carpeta Redist que ha usado al instalar sitios desde el medio de línea base.  

> [!TIP]  
> Asegúrese de que los archivos redistribuibles que usa están actualizados. Si no ha descargado recientemente los archivos redistribuibles, permita que el programa de instalación lo haga desde Microsoft.   

A continuación se presentan diferentes escenarios en los que se crea o actualiza la carpeta CD.Latest en un sitio de administración central o un servidor de sitio primario:  

- Si instala una actualización o una revisión desde la consola de Configuration Manager, el sitio crea o actualiza la carpeta en la carpeta de instalación de Configuration Manager.  

- Si ejecuta la tarea de copia de seguridad integrada de Configuration Manager, el sitio crea o actualiza la carpeta en la ubicación de la carpeta de copia de seguridad designada.  

- Al instalar un sitio nuevo con un medio de línea de base, el sitio crea la carpeta CD.Latest.


## <a name="supported-scenarios"></a>Escenarios admitidos

Los archivos de origen de la carpeta CD.Latest se admiten para los siguientes escenarios:  

### <a name="backup-and-recovery"></a>Copia de seguridad y recuperación
Para recuperar un sitio, use los archivos de origen de una carpeta CD.Latest que coincida con el sitio. Al ejecutar una copia de seguridad de sitio mediante la tarea de copia de seguridad de sitio integrada, la carpeta CD.Latest se incluye como parte de la copia de seguridad.

- Cuando vuelva a instalar el sitio como parte de una recuperación del sitio, hágalo desde la carpeta CD.Latest incluida en la copia de seguridad. De este modo, el sitio se instala con las versiones de archivo que coinciden con la copia de seguridad del sitio y la base de datos del sitio.  

    - Si no tiene acceso a la versión de la carpeta correcta de CD.Latest, obtenga la carpeta CD.Latest con las versiones de archivo correctas instalando un sitio en un entorno de laboratorio. A continuación, actualice el sitio para que coincida con la versión que desea recuperar.  

    - Si no tiene disponibles la carpeta CD.Lastest correcta y su contenido, no puede recuperar un sitio. En este caso, deberá volver a instalar el sitio.  

- Cuando no tiene una carpeta CD.Latest pero sí un sitio primario secundario o un sitio de administración central en funcionamiento, puede usar ese sitio como sitio de referencia en una recuperación del sitio.  

### <a name="install-a-child-primary-site"></a>Instalar un sitio primario secundario
Si quiere instalar un nuevo sitio primario secundario debajo de un sitio de administración central que ha instalado una o varias actualizaciones en la consola, use el programa de instalación y los archivos de origen de la carpeta CD.Latest desde el sitio de administración central. Este proceso utiliza los archivos de origen de instalación que coinciden con la versión del sitio de administración central. Para obtener más información, consulte [Use the Setup Wizard to install sites](../deploy/install/use-the-setup-wizard-to-install-sites.md) (Usar el asistente para instalación para instalar sitios).  

### <a name="expand-a-stand-alone-primary-site"></a>Expandir un sitio primario independiente
Si va a expandir un sitio primario independiente mediante la instalación de un nuevo sitio de administración central, necesita usar el programa de instalación y los archivos de origen de la carpeta CD.Latest desde el sitio primario. Este proceso utiliza los archivos de origen de instalación que coinciden con la versión del sitio primario. Para obtener más información, consulte [Expandir un sitio primario independiente](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Instalar un sitio secundario
<!-- SCCMDocs-pr issue #3164 -->
Si quiere instalar un nuevo sitio secundario debajo de un sitio primario que ha instalado una o varias actualizaciones en la consola, use los archivos de origen de la carpeta CD.Latest desde el sitio primario. 

Para obtener más información, vea [Instalar un sitio secundario](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Escenarios no admitidos

Los archivos de origen de CD.Latest actualizados no se admiten para lo siguiente:  

- Instalación de un sitio nuevo para una jerarquía nueva  
- Actualización de un sitio de Microsoft System Center 2012 Configuration Manager a la rama actual de Configuration Manager
- Instalación de clientes de Configuration Manager
- Instalación de consolas de Configuration Manager
