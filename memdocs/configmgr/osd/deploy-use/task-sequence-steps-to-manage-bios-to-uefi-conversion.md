---
title: Conversión de BIOS a UEFI
titleSuffix: Configuration Manager
description: Aprenda a personalizar una secuencia de tareas de implementación de sistema operativo para preparar una partición FAT32 para la transición a UEFI.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0118dd448520a6f0c21bfeea5f8509bd8e49fd46
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429362"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI

Windows 10 proporciona muchas características de seguridad nuevas que requieren dispositivos compatibles con UEFI. Es posible que tenga dispositivos Windows más recientes que admiten UEFI, pero que usan BIOS heredado. Anteriormente, para convertir un dispositivo a UEFI era necesario ir a cada dispositivo, volver a particionar el disco duro y reconfigurar el firmware.

Con Configuration Manager puede automatizar las siguientes acciones:

- Preparación de un disco duro para la conversión de BIOS a UEFI
- Conversión de BIOS a UEFI como parte del proceso de actualización local
- Recopilación de información de UEFI como parte del inventario de hardware

## <a name="hardware-inventory-collects-uefi-information"></a>El inventario de hardware recopila información de UEFI

Para ayudarle a determinar si un equipo se inicia en modo UEFI dispone de la clase de inventario de hardware (**SMS_Firmware**) y la propiedad (**UEFI**). Cuando un equipo se inicia en modo UEFI, la propiedad **UEFI** está establecida en **TRUE**. El inventario de hardware habilita esta clase de forma predeterminada. Para más información sobre el inventario de hardware, vea [Cómo configurar el inventario de hardware](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Creación de una secuencia de tareas personalizada para preparar el disco duro

Puede personalizar una secuencia de tareas de implementación del sistema operativo con la variable **TSUEFIDrive**. En el paso **Reiniciar equipo** se prepara una partición FAT32 en la unidad de disco duro para la transición a UEFI. En el procedimiento siguiente se ofrece un ejemplo de cómo crear pasos de secuencia de tareas para realizar esta acción.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Preparación de la partición FAT32 para la conversión a UEFI

En una secuencia de tareas existente para instalar un sistema operativo, agregue un nuevo grupo con pasos para realizar la conversión de BIOS a UEFI.

1. Cree otro grupo de secuencia de tareas después de los pasos para capturar archivos y configuraciones y antes de los pasos para instalar el sistema operativo. Por ejemplo, cree un grupo después del grupo **Capturar archivos y configuraciones** denominado **BIOS a UEFI**.

1. En la pestaña **Opciones** del nuevo grupo, agregue una nueva variable de secuencia de tareas como condición. Establezca **_SMSTSBootUEFI no es igual a true**. Con esta condición, la secuencia de tareas solo ejecuta estos pasos en los dispositivos BIOS.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Condición en el grupo de BIOS a UEFI":::

1. Debajo del nuevo grupo, agregue el paso de secuencia de tareas **Reiniciar el equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas**. Con esta acción se reinicia el equipo en Windows PE.

1. En la pestaña **Opciones**, agregue una variable de secuencia de tareas como condición. Establezca **_SMSTSInWinPE es igual a false**. Con esta condición, la secuencia de tareas no ejecuta este paso si el equipo ya está en Windows PE.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Condición en el paso Reiniciar equipo":::

1. Agregue un paso para iniciar la herramienta de OEM que va a convertir el firmware de BIOS a UEFI. Este paso suele ser **Ejecutar línea de comandos**, con el comando para ejecutar la herramienta de OEM.

1. Agregue el paso de secuencia de tareas **Formatear y crear particiones en el disco**. En este paso, configure las siguientes opciones:

    1. Cree la partición FAT32 para convertir a UEFI antes de instalar el sistema operativo. Como **Tipo de disco**, elija **GPT**.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Configuración del paso Formatear y crear particiones en el disco":::

    1. Vaya a las propiedades de la partición FAT32. En el campo **Variable**, escriba `TSUEFIDrive`. Cuando la secuencia de tareas detecta esta variable, prepara la partición para la transición a UEFI antes de reiniciar el equipo.

        :::image type="content" source="media/partition-properties.png" alt-text="Configuración de las propiedades de la partición FAT32":::

    1. Cree una partición NTFS que la secuencia de tareas use para guardar su estado y para almacenar archivos de registro.

1. Agregue otro el paso de secuencia de tareas **Reiniciar equipo**. En **Especifique qué desea ejecutar después del reinicio**, seleccione **La imagen de arranque asignada a esta secuencia de tareas** para iniciar el equipo en Windows PE.

    > [!TIP]
    > De forma predeterminada, el tamaño de la partición EFI es 500 MB. En algunos entornos, la imagen de arranque es demasiado grande para almacenarla en esta partición. Para solucionar este problema, aumente el tamaño de la partición EFI. Por ejemplo, establézcalo en 1 GB.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> Conversión de BIOS a UEFI durante una actualización local

Windows 10 incluye una sencilla herramienta de conversión, **MBR2GPT**. Automatiza el proceso para volver a particionar el disco duro para el hardware habilitado para UEFI. Puede integrar la herramienta de conversión en el proceso de actualización local a Windows 10. Combine esta herramienta con la secuencia de tareas de actualización y la herramienta de OEM que convierte el firmware de BIOS a UEFI.

### <a name="requirements"></a>Requisitos

- Una versión compatible de Windows 10
- Equipos compatibles con UEFI
- Herramienta de OEM que convierte el firmware del equipo de BIOS a UEFI

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Proceso de conversión de BIOS a UEFI durante una secuencia de tareas de actualización local

1. [Creación de una secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Edite la secuencia de tareas. En el grupo **Posprocesamiento**, realice los cambios siguientes:

    1. Agregue el paso **Ejecutar línea de comandos**. Especifique la línea de comandos para la herramienta MBR2GPT. Cuando se ejecute en el sistema operativo completo, configúrelo para convertir el disco de MBR a GPT sin modificar ni borrar datos. En **Línea de comandos**, escriba el siguiente comando: `MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > También puede ejecutar la herramienta MBR2GPT.EXE en Windows PE en lugar de en el sistema operativo completo. Agregue un paso para reiniciar el equipo en Windows PE antes del paso para ejecutar la herramienta MBR2GPT.EXE. Quite entonces la opción **/AllowFullOS** de la línea de comandos.

    Para más información sobre la herramienta y las opciones disponibles, consulte [MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt).

    1. Agregue un paso para ejecutar la herramienta de OEM que convierte el firmware de BIOS a UEFI. Este paso suele ser **Ejecutar línea de comandos**, con una línea de comandos para ejecutar la herramienta de OEM.

    1. Agregue el paso **Reiniciar equipo** y seleccione **El sistema operativo predeterminado instalado actualmente**.

1. Implemente la secuencia de tareas.
