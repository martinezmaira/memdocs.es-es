---
title: Aprovisionar previamente BitLocker en Windows PE
titleSuffix: Configuration Manager
description: La tarea Aprovisionar previamente BitLocker en Configuration Manager habilita BitLocker en el Entorno de preinstalación de Windows antes de la implementación del sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124950"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Aprovisionamiento previo de BitLocker en Windows PE con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

El paso de secuencia de tareas **Tener en servicio BitLocker** de Configuration Manager permite habilitar BitLocker en el Entorno de preinstalación de Windows (Windows PE) antes de la implementación del sistema operativo. Sólo se cifra el espacio de la unidad que se utiliza, por ello los tiempos de cifrado son mucho más rápidos. Se realiza mediante un protector de borrado generado aleatoriamente que se aplica al volumen formateado y el cifrado del volumen antes de ejecutar el proceso de instalación de Windows. La capacidad para tener en servicio BitLocker se introdujo con Windows 8 y Windows Server 2012. Sin embargo, puede tener en servicio BitLocker en una unidad de disco duro e instalar Windows 7 siempre y cuando siga pasos específicos. Una vez finalizada la instalación de Windows 7, debe establecer un protector de clave de BitLocker porque el panel de control de BitLocker de Windows 7 no es compatible con BitLocker con un protector de borrado. Debe agregar un protector de clave mediante el paso **Habilitar BitLocker** o mediante la herramienta de línea de comandos manage-bde.exe.  

 En general, para tener en servicio BitLocker correctamente en un equipo en el que se instalará Windows 7, debe hacer lo siguiente:  

- Reiniciar el equipo en Windows PE  

  > [!IMPORTANT]  
  >  Debe utilizar una imagen de arranque con Windows PE 4 o posterior para tener en servicio BitLocker. Para obtener más información sobre las versiones de Windows PE admitidas en Configuration Manager, consulte [Dependencias externas a Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Crear particiones y formatear el disco duro  

- Tener en servicio BitLocker  

- Instalar Windows 7 con una determinada configuración de red y de sistema operativo  

- Agregar un protector de clave a BitLocker  

  En Configuration Manager, la manera recomendada para tener en servicio BitLocker en un disco duro e instalar Windows 7 consiste en crear una nueva secuencia de tareas y seleccionar **Instalar un paquete de imágenes existente** en la página **Crear nueva secuencia de tareas** del **Asistente para crear secuencia de tareas**. El asistente crea los pasos de secuencia de tareas que se indican en la tabla siguiente.  

> [!NOTE]  
>  La secuencia de tareas puede tener pasos adicionales según la configuración de las opciones del asistente. Por ejemplo, puede tener el paso **Capturar configuración de Windows** si seleccionó **Capturar configuración de Microsoft Windows** en la página **Migración de estado** del asistente.  

|Paso de secuencia de tareas|Detalles|  
|------------------------|-------------|  
|Deshabilitar BitLocker|Este paso deshabilita el cifrado de BitLocker si está habilitado. Para obtener más información, consulte [Deshabilitar BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Reiniciar el equipo en Windows PE|Este paso reinicia el equipo en Windows PE mediante la ejecución de la imagen de arranque asignada a la secuencia de tareas. Debe utilizar una imagen de arranque con Windows PE 4 o posterior para tener en servicio BitLocker. Para obtener más información, consulte [Reiniciar equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Disco de partición 0 - BIOS<br /><br /> Disco de partición 0 - UEFI|Mediante estos pasos se realiza el formateo y la partición de la unidad especificada en el equipo de destino a través de BIOS o UEFI. La secuencia de tareas utiliza UEFI cuando detecta que el equipo de destino está en modo UEFI. Para obtener más información, consulte [Formatear y crear particiones en el disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Tener en servicio BitLocker|Este paso habilita BitLocker en una unidad cuando se usa Windows PE. Solo se cifra el espacio utilizado de la unidad. No hay datos porque se realizó el formateo y la partición del disco duro en el paso anterior y, por lo tanto, el cifrado se completa con gran rapidez. Para obtener más información, consulte [Tener en servicio BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Aplicar sistema operativo|En este paso se prepara el archivo de respuesta que se usa para instalar el sistema operativo en el equipo de destino, y se configura la variable de secuencia de tareas OSDTargetSystemDrive como la letra de la unidad de la partición que contiene los archivos del sistema operativo. El paso Instalar Windows y Configuration Manager usa la variable y el archivo de respuesta para instalar el sistema operativo. Para obtener más información, vea [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Aplicar configuraciones de Windows|En este paso se agrega la configuración de Windows al archivo de respuesta. El paso Instalar Windows y Configuration Manager usa el archivo de respuesta para instalar el sistema operativo. Para obtener más información, consulte [Aplicar configuraciones de Windows](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Aplicar configuración de red|En este paso se agrega la configuración de red al archivo de respuesta. El paso Instalar Windows y Configuration Manager usa el archivo de respuesta para instalar el sistema operativo. Para obtener más información, consulte [Paso Aplicar configuración de red](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Aplicar controladores del dispositivo|En este paso se buscan e instalan controladores como parte de la implementación de sistema operativo. Para obtener más información, consulte [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Instalar Windows y Configuration Manager|Este paso realiza la transición desde Windows PE al nuevo sistema operativo. Este paso de secuencia de tareas es una parte necesaria de cualquier implementación de sistema operativo. Se instala el cliente de Configuration Manager en el nuevo sistema operativo y se prepara para que la secuencia de tareas continúe con la ejecución en el sistema operativo. Para obtener más información, consulte [Instalar Windows y Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Habilitar BitLocker|Este paso habilita el cifrado de BitLocker en la unidad de disco duro y establece los protectores de clave. Ya que el disco duro se aprovisionó previamente con BitLocker, este paso se completa muy rápidamente. Windows 7 requiere que se agregue un protector de clave. Si no utiliza este paso, puede ejecutar la herramienta de línea de comandos manage-bde.exe para configurar un protector de clave. Para obtener más información, consulte [Habilitar BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
