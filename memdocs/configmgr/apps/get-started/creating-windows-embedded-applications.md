---
title: Creación de aplicaciones de Windows Embedded
titleSuffix: Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos de Windows Embedded.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689843"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Creación de aplicaciones de Windows Embedded con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Además de los otros requisitos y procedimientos de Configuration Manager para crear una aplicación, también debe tener en cuenta las consideraciones siguientes al crear e implementar aplicaciones para dispositivos de Windows Embedded.  

## <a name="general-considerations"></a>Consideraciones generales  

-   Cuando se implementan aplicaciones en dispositivos de Windows Embedded habilitados para el filtro de escritura, se puede especificar si se desea deshabilitar el filtro de escritura en el dispositivo durante la implementación de la aplicación. Luego, puede elegir reiniciar el filtro de escritura después de la implementación de la aplicación. Si el filtro de escritura no está deshabilitado, el software se implementa en una superposición temporal. Esto significa que, a menos que otra implementación fuerce que los cambios se mantengan, el software dejará de estar instalado cuando el dispositivo se reinicie.  

-   Cuando implemente una aplicación en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Esto le permite administrar cuándo se deshabilita y habilita el filtro de escritura, y cuándo se reinicia el dispositivo.  

-   La opción que permite controlar el comportamiento de los filtros de escritura es la casilla **Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)** .  

## <a name="tips-for-deploying-applications"></a>Sugerencias para la implementación de aplicaciones  

**Utilice las aplicaciones necesarias en lugar de las aplicaciones disponibles para dispositivos de Windows Embedded que tengan habilitados filtros de escritura.** Dado que los usuarios no pueden instalar aplicaciones del Centro de software de un dispositivo de Windows Embedded con filtros de escritura habilitados, implemente siempre las aplicaciones con el propósito de implementación de **requerida** en lugar de **disponible** en estos dispositivos. Por lo general, esto no significa un problema porque los equipos que ejecutan un sistema operativo Windows Embedded suelen ejecutar una sola aplicación que debe ejecutarse del mismo modo para varios usuarios. Por este motivo, estos dispositivos están bloqueados y altamente administrados por el departamento de TI. Las aplicaciones necesarias son adecuadas para este escenario.

 Sin embargo, si los usuarios deben ejecutar más de una aplicación en dispositivos incrustados que tienen habilitados filtros de escritura, informe a estos usuarios sobre las siguientes limitaciones:  

-   Los usuarios no pueden instalar el software necesario desde el Centro de software.  

-   Los usuarios no pueden cambiar su horario comercial en la pestaña Opciones del Centro de software.  

-   Los usuarios no pueden posponer la instalación de una aplicación necesaria.  

Además, los usuarios que tienen derechos reducidos no pueden iniciar sesión durante un período de mantenimiento si Configuration Manager está realizando cambios en las instalaciones y actualizaciones de software. Durante este período, los usuarios ven un mensaje que les informa que el dispositivo no está disponible porque se le están realizando tareas de mantenimiento.  

**No implemente aplicaciones en dispositivos de Windows Embedded que tienen habilitados filtros de escritura si las aplicaciones requieren que el usuario acepte los términos de licencia.** Cuando los filtros de escritura se deshabilitan para que Configuration Manager pueda instalar software en dispositivos incrustados, los usuarios con derechos reducidos no pueden iniciar sesión en esos dispositivos. Si la instalación requiere que el usuario acepte los términos de licencia, esto no será posible y la instalación producirá un error. Asegúrese de no implementar software para dispositivos de Windows Embedded si la instalación requiere la interacción del usuario. Puede usar la lista Plataformas aplicables para filtrar estos sistemas operativos.  
