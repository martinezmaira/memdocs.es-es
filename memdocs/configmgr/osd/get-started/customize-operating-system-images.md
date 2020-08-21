---
title: 'Personalizar las imágenes de sistema operativo '
titleSuffix: Configuration Manager
description: Use secuencias de tareas de captura y compilación, la configuración manual o una combinación de ambas para personalizar una imagen de sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4f1d89707fa3e1765067c264d2abec12116bde88
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697728"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Personalizar imágenes de sistema operativo con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las imágenes de sistema operativo de Configuration Manager son archivos WIM y representan una recopilación comprimida de archivos de referencia y carpetas necesarios para instalar y configurar correctamente un sistema operativo en un equipo. Una imagen de sistema operativo personalizada se compila y captura mediante un equipo de referencia que se configura con todos los archivos de sistema operativo, los archivos auxiliares, las actualizaciones de software, las herramientas y las aplicaciones de software necesarios. La medida en que configure el equipo de referencia manualmente depende de usted. Puede automatizar completamente la configuración del equipo de referencia mediante el uso de una secuencia de tareas de compilación y captura, puede configurar manualmente algunos aspectos del equipo de referencia y automatizar luego el resto mediante secuencias de tareas, o puede configurar manualmente el equipo de referencia sin usar secuencias de tareas. Use las siguientes secciones para personalizar un sistema operativo.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a> Preparar el equipo de referencia  
 Existen algunas consideraciones a tener en cuenta antes de capturar una imagen de sistema operativo desde un equipo de referencia.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a> Decidir entre una configuración automatizada o manual  
 A continuación se indican las ventajas y desventajas de una configuración automatizada y manual del equipo de referencia.  

#### <a name="automated-configuration"></a>Configuración automatizada  
 **Ventajas**  

- La configuración puede ser totalmente desatendida, lo que elimina la necesidad de que esté presente un administrador o usuario.  

- Puede volver a utilizar la secuencia de tareas para repetir la configuración de equipos de referencia adicionales con un alto nivel de confianza.  

- Puede modificar la secuencia de tareas para reflejar diferencias en los equipos de referencia sin tener que volver a crear la secuencia de tareas completa.  

  **Desventajas**  

- La acción inicial para generar una secuencia de tareas puede tardar mucho tiempo en crearse y probarse.  

- Si los requisitos del equipo de referencia cambian significativamente, se tardará mucho tiempo en volver a crear y volver a probar la secuencia de tareas.  

#### <a name="manual-configuration"></a>Configuración manual  
 **Ventajas**  

- No es necesario crear una secuencia de tareas o dedicar tiempo a probar la secuencia de tareas y solucionar problemas de la misma.  

- Puede instalar directamente desde CD sin poner todos los paquetes de software (incluido el propio Windows) en un paquete de Configuration Manager.  

  **Desventajas**  

- La exactitud de la configuración del equipo de referencia depende del administrador o el usuario que configure el equipo.  

- Debe comprobar y probar que el equipo de referencia esté configurado correctamente.  

- No puede volver a utilizar el método de configuración.  

- Exige que una persona participe activamente en todo el proceso.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a> Consideraciones para el equipo de referencia  
 A continuación se enumeran los elementos básicos para tener en cuenta al configurar un equipo de referencia.  

-   **Sistema operativo que se va a implementar**  

     El equipo de referencia debe instalarse con el sistema operativo que se va a implementar en los equipos de destino. Para obtener más información sobre los sistemas operativos que puede implementar, consulte [Infrastructure requirements for operating system deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisitos de infraestructura para la implementación de sistema operativo).  

-   **Service Pack apropiado**  

     El equipo de referencia debe instalarse con el sistema operativo que se va a implementar en los equipos de destino.  

-   **Actualizaciones de software apropiadas**  

     Instale todas las aplicaciones de software que desee incluir en la imagen del sistema operativo que capture del equipo de referencia. También puede instalar las aplicaciones de software al implementar la imagen capturada del sistema operativo en los equipos de destino.  

-   **Pertenencia a grupo de trabajo**  

     El equipo de referencia debe configurarse como un miembro de un grupo de trabajo.  

-   **Sysprep**  

     La Herramienta de preparación del sistema (Sysprep) es una tecnología que puede utilizar con otras herramientas de implementación para instalar sistemas operativos Windows en hardware nuevo. Sysprep prepara un equipo para la creación de imágenes de discos o la entrega a un cliente mediante la configuración del equipo para crear un nuevo identificador de seguridad (SID) de equipo cuando este se reinicie. Además, Sysprep limpia las opciones de configuración específicas del equipo y del usuario y los datos que no deben copiarse en un equipo de destino.  

     Puede preparar manualmente el equipo de referencia con Sysprep si ejecuta el comando siguiente:  

     `Sysprep /quiet /generalize /reboot`  

     La opción /generalize indica a Sysprep que quite los datos específicos del sistema de la instalación de Windows. La información específica del sistema incluye registros de eventos, identificadores de seguridad (SID) únicos y otros datos exclusivos. Después de quitar la información exclusiva del sistema, el equipo se reinicia.  

     Puede automatizar Sysprep mediante el uso del paso de la secuencia de tareas [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) (Preparar Windows para la captura) o los medios de captura.  

    > [!IMPORTANT]  
    >  En el paso de la secuencia de tareas [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) (Preparar Windows para la captura) se intenta restablecer la contraseña del administrador local del equipo de referencia en un valor en blanco antes de que se ejecute Sysprep. Si la directiva de seguridad local **La contraseña debe cumplir los requisitos de complejidad** está habilitada, este paso de la secuencia de tareas no restablece la contraseña del administrador. En este escenario, deshabilite esta directiva antes de ejecutar la secuencia de tareas.  

     Para más información acerca de Sysprep, consulte [Información general sobre Sysprep (preparación del sistema)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).  

-   **Herramientas y scripts adecuados necesarios para minimizar escenarios de instalación**  

     Herramientas y scripts adecuados necesarios para minimizar escenarios de instalación  

-   **Personalización de escritorio adecuada, como papel tapiz, personalización de marca y perfil de usuario predeterminado**  

     Puede configurar el equipo de referencia con las propiedades de personalización del escritorio que desee incluir al capturar la imagen del sistema operativo del equipo de referencia. Las propiedades del escritorio incluyen papel tapiz, personalización de marca corporativa y un perfil de usuario predeterminado estándar.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a> Compilar manualmente un equipo de referencia  
 Use el siguiente procedimiento para compilar manualmente un equipo de referencia.  

> [!NOTE]  
>  Si compila manualmente el equipo de referencia, puede capturar la imagen de sistema operativo usando medios de captura. Para obtener más información, consulte [Create capture media](../deploy-use/create-capture-media.md) (Crear medios de captura).  

#### <a name="to-manually-build-the-reference-computer"></a>Para compilar el equipo de referencia manualmente  

1. Identifique el equipo que se va a utilizar como equipo de referencia.  

2. Configure el equipo de referencia con el sistema operativo apropiado y cualquier otro software necesario para crear la imagen del sistema operativo que va a implementar.  

   > [!WARNING]  
   >  Como mínimo, instale el sistema operativo y el Service Pack adecuados, los controladores de soporte y las actualizaciones de software necesarias.  

3. Configure el equipo de referencia para que sea miembro de un grupo de trabajo.  

4. Restablezca la contraseña de administrador local en el equipo de referencia de tal manera que no se especifique ninguna.  

5. Ejecute Sysprep con el comando:  **sysprep /quiet /generalize /reboot**. La opción /generalize indica a Sysprep que quite los datos específicos del sistema de la instalación de Windows. La información específica del sistema incluye registros de eventos, identificadores de seguridad (SID) únicos y otros datos exclusivos. Después de quitar la información exclusiva del sistema, el equipo se reinicia.  

   Cuando el equipo de referencia esté listo, use una secuencia de tareas para capturar la imagen de sistema operativo del equipo de referencia.  Para conocer los pasos detallados, consulte [Capture an operating system image from an existing reference computer](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer) (Capturar una imagen de sistema operativo a partir de un equipo de referencia existente).  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a> Usar una secuencia de tareas para compilar un equipo de referencia  
 Puede automatizar el proceso para crear un equipo de referencia usando una secuencia de tareas para implementar el sistema operativo, los controladores, las aplicaciones, etc.  Use las etapas siguientes para compilar el equipo de referencia y, después, para capturar la imagen de sistema operativo del equipo de referencia.  

-   Use una secuencia de tareas para compilar y capturar la imagen de sistema operativo del equipo de referencia.  Para conocer los pasos detallados, consulte [Usar una secuencia de tareas para compilar y capturar un equipo de referencia](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).