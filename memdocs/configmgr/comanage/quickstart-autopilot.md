---
title: Windows Autopilot con administración conjunta
titleSuffix: Configuration Manager
description: Use Windows Autopilot con administración conjunta en Configuration Manager para simplificar la configuración de nuevos dispositivos Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b97f9bb6be00129e0b88dc3943af1de166a801d4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690953"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot con administración conjunta

Recibir un nuevo dispositivo con Windows 10 es emocionante. Sin embargo, puede llevar tiempo configurar todas las configuraciones y aplicaciones para que pueda ser productivo. La administración conjunta resuelve este problema de aprovisionamiento de dispositivos con Windows Autopilot.

Autopilot proporciona una experiencia simplificada para usted y sus usuarios en las situaciones siguientes:
- Configurar y preconfigurar nuevos dispositivos con Windows 10  
- Restablecer, reciclar y recuperar dispositivos existentes  

Autopilot reduce el tiempo, los recursos y la complejidad asociados con la implementación, administración y retirada de los dispositivos. Al mismo tiempo, la experiencia para sus usuarios es ágil y sencilla desde el primer momento.

Windows Autopilot admite varios escenarios, todos los cuales se maximizarán con la administración conjunta:

- Los usuarios pueden impulsar sus propias implementaciones de nuevos dispositivos en Active Directory con unión híbrida a Azure AD o Azure Active Directory (Azure AD)  

- Puede configurar la implementación automática de nuevas implementaciones de dispositivos en Azure AD para quioscos y dispositivos compartidos.  

- Con Windows Autopilot para dispositivos existentes, use Configuration Manager para migrar un dispositivo existente de Windows 7 y Active Directory a Windows 10 y Azure AD.  

En el siguiente video, el Jefe de Programas Senior Danny Guillory y el Jefe Principal de Programas Andrew McMurray debaten sobre Autopilot con la administración conjunta y demuestran su funcionamiento.

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Ventajas

Cuando usa la administración conjunta y Autopilot juntos, se asegura de que los nuevos dispositivos que acceden a la red terminan en el mismo estado de administración. En esta configuración, los dispositivos están inscritos en Intune y tienen un cliente de Configuration Manager.  Le permite usar el nuevo modelo de aprovisionamiento de Windows 10 y le ayuda a eliminar la necesidad de crear, mantener y actualizar imágenes personalizadas del sistema operativo. 

En todos estos escenarios, puede [habilitar la administración conjunta](how-to-prepare-Win10.md) automáticamente de Intune. Esta automatización le ayuda con el proceso de aprovisionamiento y la administración continua del dispositivo.

Con Autopilot, no deberá preocuparse por las imágenes y los controladores. Céntrese en aprovisionar dispositivos mediante este proceso automatizado utilizando Intune y Configuration Manager a través de la administración conjunta.


Le mostramos cómo usar conjuntamente la administración conjunta y Autopilot ahora mismo:

#### <a name="reduce-time-costs-and-complexity"></a>Reducción de tiempo, costos y complejidad
Windows Autopilot usa la versión optimizada por OEM de Windows 10 que está preinstalada en el dispositivo. Esta configuración ahorra a las organizaciones el esfuerzo de tener que mantener imágenes y controladores personalizados para cada modelo de dispositivo en uso. En lugar de restablecer la imagen inicial del dispositivo, transforme la instalación de Windows 10 existente a un estado "listo para el negocio". Aplica configuraciones y directivas, instala aplicaciones y cambia la edición de Windows 10. Por ejemplo, actualiza de Windows 10 Pro a Windows 10 Enterprise para que pueda admitir características avanzadas.

#### <a name="improve-the-user-experience"></a>Mejora de la experiencia del usuario
La mejor experiencia de usuario causa una menor interrupción y les ayuda a volver a centrarse en su trabajo. Windows Autopilot ofrece un enfoque sencillo para ayudar a los usuarios a configurar su solución rápidamente con unos pocos clics y sus credenciales de Azure AD. En el caso de las muchas organizaciones con un gran número de empleados remotos, use Windows Autopilot para el envío de nuevos dispositivos directamente desde el fabricante.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Uso de Autopilot y Configuration Manager para migrar los dispositivos existentes de Windows 7 a Windows 10
Con Windows Autopilot para los dispositivos existentes, crea un archivo de configuración y lo implementa con una secuencia de tareas de Configuration Manager. Este proceso migra fácilmente los dispositivos existentes de Windows 7 a Windows 10. Utiliza una imagen de firma de Windows 10 en Configuration Manager y luego la aplica al dispositivo con Windows 7 existente con la configuración de Autopilot. Cuando el usuario inicia el dispositivo, usa el proceso de incorporación controlado por el usuario de Autopilot.

Estos son los pasos de Autopilot para los dispositivos existentes:

![Información general del proceso de Windows Autopilot para dispositivos existentes](media/autopilot-for-existing-devices.png)

1. Implementar la directiva de grupo para redirigir las carpetas conocidas a OneDrive
2. Generar el archivo de configuración de Autopilot
3. Implementar una secuencia de tareas para actualizar a Windows 10
4. El equipo con Windows 10 pasa por Autopilot en el primer arranque

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernización del aprovisionamiento de dispositivos para todos los tipos de trabajos
Con Autopilot, ahora puede proporcionar una implementación de sistema operativo de manos libres en dispositivos sin personal de operación o dispositivos compartidos con el modo de implementación automática. Esta configuración satisface las necesidades de todos los distintos tipos de trabajos. Además, la función de restablecimiento de Windows Autopilot asegura que el reaprovisionamiento de un dispositivo a un nuevo usuario sea simple y fácil. Este proceso simplifica lo que tradicionalmente ha sido una tarea difícil cuando tiene trabajadores temporales o contratados. 



## <a name="case-study"></a>Caso práctico

La compañía alemana de transporte ferroviario y logística Shenker DB usa Autopilot para aumentar la productividad de los empleados y liberar a sus equipos de TI de trabajar en las tareas cotidianas de asistencia. Shenker se ha alejado de la creación tradicional de imágenes y la ha reemplazado por un aprovisionamiento mediante la nube. Ahora usa la unión a Azure AD e Intune para poner en funcionamiento los nuevos dispositivos rápidamente. 

En lugar de que sus empleados remotos pierdan tiempo viajando a una ubicación con servicios de TI, Shenker ahora usa Windows Autopilot. Así, envía el hardware de sus trabajadores directamente del fabricante a su oficina local. El trabajador conecta el nuevo dispositivo a Internet e inicia sesión con sus credenciales de Azure AD. El dispositivo, a continuación, se conecta a las aplicaciones y servicios que el departamento de TI de Schenker asigna al perfil individual del usuario.

Para obtener más información, consulte [Global logistics firm centralizes IT, unites employees with modern digital workplace](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10) (Empresa de logística global centraliza la TI y une a los empleados con el moderno lugar de trabajo digital).



## <a name="value-proposition"></a>Propuesta de valor

Cree satisfacción en su organización mediante la creación de una mejor experiencia para los usuarios. Use Windows Autopilot para reducir los costos. Libere su tiempo para centrarse en otros proyectos para generar más valor e impacto para su organización.



## <a name="configure"></a>Configurar

Vea los siguientes artículos para más información:

[Inscripción de dispositivos Windows en Intune con Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot para dispositivos existentes](../osd/deploy-use/windows-autopilot-for-existing-devices.md)

