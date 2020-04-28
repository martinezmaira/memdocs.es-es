---
title: Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo personalizar una secuencia de tareas de implementación de sistema operativo para preparar una partición FAT32 para la transición a UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079372"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI
Windows 10 proporciona muchas características de seguridad nuevas que requieren dispositivos compatibles con UEFI. Es posible que tenga equipos modernos de Windows que admiten UEFI, pero que usan un BIOS heredado. Para convertir un dispositivo a UEFI es necesario que vuelva a particionar el disco duro y vuelva a configurar el firmware de cada equipo. Mediante el uso de secuencias de tareas en Configuration Manager, puede preparar un disco duro para la conversión de BIOS en UEFI, convertir de BIOS a UEFI como parte del proceso de actualización local y recopilar información de UEFI como parte del inventario de hardware.

## <a name="hardware-inventory-collects-uefi-information"></a>El inventario de hardware recopila información de UEFI
A partir de la versión 1702, para ayudarlo a determinar si un equipo se inicia en modo UEFI, están disponibles una nueva clase de inventario de hardware (**SMS_Firmware**) y la propiedad (**UEFI**). Cuando un equipo se inicia en modo UEFI, la propiedad **UEFI** está establecida en **TRUE**. Esto está habilitado en el inventario de hardware de forma predeterminada. Para más información sobre el inventario de hardware, vea [Cómo configurar el inventario de hardware](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Creación de una secuencia de tareas personalizada para preparar el disco duro para la conversión de BIOS a UEFI
A partir de la versión 1610 de Configuration Manager, ahora puede personalizar una secuencia de tareas de implementación de sistema operativo con una nueva variable, TSUEFIDrive, para que el paso **Reiniciar el equipo** prepare una partición FAT32 en la unidad de disco duro para la transición a UEFI. En el procedimiento siguiente se proporciona un ejemplo de cómo crear pasos de secuencia de tareas para preparar la unidad de disco duro para la conversión de BIOS en UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar la partición FAT32 para la conversión a UEFI:
En una secuencia de tareas existente para instalar un sistema operativo, agregue un nuevo grupo con pasos para realizar la conversión de BIOS a UEFI.

1. Cree un nuevo grupo de secuencia de tareas después de los pasos para capturar archivos y configuraciones y antes de los pasos para instalar el sistema operativo. Por ejemplo, cree un grupo después del grupo **Capturar archivos y configuraciones** denominado **BIOS a UEFI**.
2. En la pestaña **Opciones** del nuevo grupo, agregue una nueva variable de secuencia de tareas como una condición donde **_SMSTSBootUEFI** **No es igual** a **true**. Esto evita que los pasos del grupo se ejecuten cuando un equipo ya está en modo UEFI.

   ![Grupo BIOS a UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Debajo del nuevo grupo, agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.  
4. En la pestaña **Opciones**, agregue una variable de secuencia de tareas como una condición donde **_SMSTSInWinPE es igual a false**. Esto evita que este paso se ejecute si el equipo ya está en Windows PE.

   ![Paso Reiniciar el equipo](../../core/get-started/media/restart-in-windows-pe.png)
5. Agregue un paso para iniciar la herramienta de OEM que va a convertir el firmware de BIOS a UEFI. Normalmente será un paso de secuencia de tareas **Ejecutar línea de comandos** con una línea de comandos para iniciar la herramienta de OEM.
6. Agregue el paso de secuencia de tareas Formatear y crear particiones en el disco que va a crear particiones en la unidad de disco duro y a aplicarle formato. En el paso, haga lo siguiente:
   1. Cree la partición FAT32 que se convertirá en UEFI antes de instalar el sistema operativo. Elija **GPT** para **Tipo de disco**.
    ![Paso Formatear y crear particiones en el disco](../media/format-and-partition-disk.png)
   2. Vaya a las propiedades de la partición FAT32. Escriba **TSUEFIDrive** en el campo **Variable**. Cuando la secuencia de tareas detecte esta variable, se preparará para la transición a UEFI antes de reiniciar el equipo.
    ![Propiedades de la partición](../../core/get-started/media/partition-properties.png)
   3. Cree una partición NTFS que el motor de secuencia de tareas use para guardar su estado y para almacenar archivos de registro.
7. Agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversión de BIOS a UEFI durante una actualización local
Windows 10 Creators Update presenta una herramienta de conversión sencilla que automatiza el proceso para volver a particionar el disco duro de hardware compatible con UEFI e integra la herramienta de conversión en el proceso de actualización local de Windows 7 a Windows 10. Cuando esta herramienta se combina con la secuencia de tareas de actualización del sistema operativo y la herramienta de OEM que convierte el firmware de BIOS a UEFI, puede convertir los equipos de BIOS a UEFI durante una actualización local a Windows 10 Creators Update.

**Requisitos**:
- Windows 10 Creators Update
- Equipos compatibles con UEFI
- Herramienta de OEM que convierte el firmware del equipo de BIOS a UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Para convertir de BIOS a UEFI durante una actualización local
1. Cree una secuencia de tareas de actualización del sistema operativo que realiza una actualización local a Windows 10 Creators Update.
2. Edite la secuencia de tareas. En el **grupo Posprocesamiento**, agregue los siguientes pasos a la secuencia de tareas:
   1. En General, agregue un paso **Ejecutar línea de comandos**. Va a agregar la línea de comandos para la herramienta MBR2GPT que convierte un disco de MBR a GPT sin modificar o eliminar datos del disco. En la línea de comandos, escriba lo siguiente:  **MBR2GPT /convert /disk:0 /AllowFullOS**. También puede ejecutar la herramienta MBR2GPT.EXE en Windows PE en lugar de en el sistema operativo completo. Para ello, agregue un paso para reiniciar el equipo a WinPE antes del paso de ejecutar la herramienta MBR2GPT.EXE y eliminar la opción /AllowFullOS de la línea de comandos. Para obtener información detallada sobre la herramienta y las opciones disponibles, vea [MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Agregue un paso para iniciar la herramienta de OEM que va a convertir el firmware de BIOS a UEFI. Normalmente será un paso de secuencia de tareas Ejecutar línea de comandos con una línea de comandos para iniciar la herramienta de OEM.
   3. En General, agregue el paso **Reiniciar equipo**. Para especificar lo que se debe ejecutar después del reinicio, seleccione **El sistema operativo predeterminado instalado actualmente**.
3. Implemente la secuencia de tareas.
