---
title: 'Instalación de un sitio con el medio de línea base 1606 '
titleSuffix: Configuration Manager
description: Instale o actualice a la LTSB de System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707013"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Instalación y actualización con el medio de línea base de la versión 1606

*Se aplica a: System Center Configuration Manager (rama de mantenimiento a largo plazo)*

Cuando se ejecuta el programa de instalación del medio de línea base de la versión 1606 de Configuration Manager, se puede instalar un sitio de rama de mantenimiento a largo plazo de Configuration Manager.

El medio de línea base está disponible en DVD como parte de Microsoft System Center 2016 o desde la rama de mantenimiento a largo plazo de System Center Configuration Manager, versión 1606. Para obtener información sobre el medio de línea base, consulte [Versiones de actualización y línea base](../servers/manage/updates.md#bkmk_Baselines).


Cuando use el medio de línea base de la versión 1606, el sitio que instala o al que actualiza es:
- *Un sitio de rama actual* que es equivalente a un sitio que se instaló primero mediante el medio de línea base 1511 y, después, se actualizó a la versión 1606 además del paquete acumulativo de revisiones 1606: KB3186654.
- *Un sitio de LTSB* que es equivalente al sitio de rama actual que ejecuta la versión 1606 además del paquete acumulativo de revisiones 1606: KB3186654. El medio de línea base ya incluye el paquete acumulativo de revisiones.  En cambio, la LTSB no admite todas las características o capacidades que están disponibles en la rama actual, como se detalla en [Introducción a la rama de mantenimiento a largo plazo de System Center Configuration Manager](introduction-to-the-ltsb.md).

Si no está familiarizado con las diferentes ramas de Configuration Manager, vea [Qué rama de Configuration Manager debo usar](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Cambios en la configuración con el medio de línea base 1606
El medio de línea base 1606 presenta los siguientes cambios en la instalación de Configuration Manager.

### <a name="branch-and-edition"></a>Rama y edición
Cuando ejecuta el programa de instalación, se le presenta una página de licencia donde puede seleccionar la rama de Configuration Manager que quiere instalar. Puede elegir la rama actual o la LTSB como una instalación con licencia, o puede elegir una edición de evaluación de la rama actual como una instalación sin licencia.

Para más información, vea [Licencias y ramas de Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiración de Software Assurance
Durante la instalación, tiene la opción de escribir el valor **fecha de expiración de Software Assurance**. Este es un valor opcional que puede especificar como un recordatorio útil.

> [!NOTE]
> Microsoft no valida la fecha de expiración que especifique y no la usará para la validación de la licencia.  pero usted puede usarla como un recordatorio de la fecha de expiración. Esto es útil porque Configuration Manager busca de forma periódica nuevas actualizaciones de software que se ofrecen en línea y el estado de su licencia de Software Assurance debe ser actual para que pueda usar estas actualizaciones adicionales.    

- Puede especificar el valor de fecha en la página **Clave de producto** del Asistente para instalación cuando ejecute el programa de instalación del medio de línea base de la versión 1606 de Configuration Manager.
- También puede especificar esta fecha seleccionando **Propiedades de configuración de jerarquía** > **Licencia** en la consola de Configuration Manager.

Para más información, vea "Contratos de Software Assurance" en [Licencias y ramas de Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configuraciones previas a la actualización adicionales
Antes de iniciar una actualización de System Center 2012 Configuration Manager a la LTSB, debe realizar los siguientes pasos adicionales como parte de la lista de comprobación previa a la actualización.  
Desinstale los roles de sistema de sitio que la LTSB no admiten:
- Punto de sincronización de Asset Intelligence
- Conector de Microsoft Intune
- Puntos de distribución basados en la nube

Para obtener más información, consulte [Actualizar a System Center Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Nuevas opciones de instalación generadas por script
El medio de línea base de la versión 1606 admite una nueva clave de archivo de script desatendido para las instalaciones generadas por script de un sitio nuevo de nivel superior. Se aplica a la instalación de un nuevo sitio primario independiente o a la adición de un sitio de administración central como parte de un escenario de expansión de sitios.

Al usar un script desatendido para instalar una rama con licencia, debe agregar la siguiente sección, los nombres de clave y valores a la sección de opciones del script. No es necesario usar estos valores para la instalación mediante script de la edición de evaluación de la rama actual:  

 **SABranchOptions**
- **Nombre de clave: SAActive**
  - Values: 0 o 1.  
  - Detalles:  0 instala una edición de evaluación sin licencia de la Rama actual y 1 instala una edición con licencia.   

- **CurrentBranch**
  - Values: 0 o 1.  
  - Detalles:  0 instala la rama de mantenimiento a largo plazo y 1 instala la rama actual.  

Por ejemplo, para instalar una edición de rama actual con licencia, usará:

**Nombre de clave: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** solo funciona con el programa de instalación desde el medio de línea base. No se aplica cuando ejecuta el programa de instalación desde la carpeta CD.Latest de un sitio que ha instalado previamente mediante el medio de línea base de la versión 1606.
>
> **SABranchOptions** no se aplica a actualizaciones generadas por script de System Center 2012 Configuration Manager y siempre da como resultado la rama actual.

Para más información, vea [Usar una línea de comandos para instalar sitios de Configuration Manager](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Instalar un nuevo sitio
Cuando use el medio de línea base 1606 para instalar un nuevo sitio de cualquier rama, use los procedimientos de instalación, preparación y planeación de sitios que se documentan en el tema [Instalación de sitios de Configuration Manager](../servers/deploy/install/installing-sites.md), además de las siguientes consideraciones sobre el programa de instalación:

- Durante la instalación, debe elegir la rama de Configuration Manager que quiere instalar, y puede especificar la información de su contrato de Software Assurance.
- Todos los sitios de una misma jerarquía deben ejecutar la misma rama. Tener una jerarquía con una mezcla de LTSB y rama actual en diferentes sitios no se admite.
- Nueva instalación generada por script. Para más información, vea "Nuevas opciones de instalación generadas por script" anteriormente en este artículo.

## <a name="expand-a-stand-alone-primary-site"></a>Expandir un sitio primario independiente
Puede expandir un sitio primario independiente que ejecuta la LTSB.  El proceso no es diferente del que se usó para un sitio de rama actual con una salvedad:

- Al instalar el nuevo sitio de administración central, debe usar el programa de instalación del medio de origen original que usó para instalar el sitio de LTSB. No se admite ejecutar el programa de instalación de la carpeta CD.Latest para este escenario.

Para más información sobre la expansión de un sitio, vea "Expandir un sitio primario independiente" en [Install a site using the Setup Wizard (Instalar un sitio mediante el Asistente para instalación)](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Actualización desde System Center 2012 Configuration Manager
Cuando actualice desde System Center 2012 Configuration Manager, use los procedimientos de preparación y planeación del sitio como se documenta en el tema [Actualizar a Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md), pero con los siguientes cambios:

**Actualizar a la rama actual:**
- Durante el programa de instalación, debe elegir la rama actual, y puede especificar la información de su contrato de Software Assurance.
- Nueva instalación generada por script. Para más información, vea "Nuevas opciones de instalación generadas por script" anteriormente en este artículo.

**Actualizar a la LTSB:**  
- Pasos adicionales para seguir en la lista de comprobación previa a la actualización.
- Durante el programa de instalación, debe elegir la LTSB, y puede especificar la información de su contrato de Software Assurance.
- Solo puede actualizar un sitio que ejecuta System Center 2012 Configuration Manager con el Service Pack 1, System Center 2012 Configuration Manager con el Service Pack 2, System Center 2012 R2 Configuration Manager con el Service Pack 1 o System Center 2012 R2 Configuration Manager sin ningún Service Pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Rutas de actualización local para el medio de línea base 1606
Puede usar el medio de línea base 1606 para actualizar lo siguiente a una edición con licencia de Configuration Manager:
- System Center 2012 R2 Configuration Manager con Service Pack 1
- System Center 2012 R2 Configuration Manager sin Service Pack (requiere usar el media de línea base para la versión 1606 que se volvió a publicar el 15 de diciembre de 2016).
- System Center 2012 Configuration Manager con Service Pack 2
- System Center 2012 Configuration Manager con Service Pack 1 (requiere el uso del medio de línea base para la versión 1606 que se volvió a publicar el 15 de diciembre de 2016).


También puede usar este medio para actualizar una edición de evaluación sin licencia de la rama actual a una versión de licencia completa de la rama actual.

Este medio no admite la actualización de:
- Otras versiones de System Center 2012 Configuration Manager.
- Configuration Manager 2007 o versiones anteriores.
- Una instalación de versión candidata de Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre la carpeta CD.Latest y la LTSB
Lo siguiente son limitaciones para usar el medio que Configuration Manager crea en la carpeta CD.Latest del servidor de sitio. Estos límites se aplican a sitios que ejecutan la LTSB:

Los medios de la carpeta CD.Latest son compatibles con:
- Recuperación del sitio.
- Mantenimiento del sitio.
- Instalación de sitios primarios secundarios adicionales.

El medio de la carpeta CD.Latest no es compatible con:  
- Instalación de un sitio de administración central como parte de un escenario de expansión de sitios.

Para más información, vea [la carpeta CD.Latest](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Copia de seguridad, recuperación y mantenimiento de sitio para la LTSB
Para hacer una copia de seguridad, recuperar o ejecutar el mantenimiento de un sitio que ejecuta la LTSB, use la guía y los procedimientos de [Copia de seguridad y recuperación de Configuration Manager](../servers/manage/backup-and-recovery.md).  

Use el programa de instalación de Configuration Manager de la carpeta CD.Latest de la copia de seguridad de su sitio de LTSB.
