---
title: Ayuda del cliente Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información sobre las características y las mejoras de Endpoint Protection que ayudan a proteger el equipo frente a amenazas.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709213"
---
# <a name="endpoint-protection-client-help"></a>Ayuda del cliente Endpoint Protection

*Se aplica a: Configuration Manager (rama actual)*


Esta versión de Windows Defender o Endpoint Protection incluye las siguientes características para ayudar a proteger el equipo frente a amenazas:  

-   **Integración con Firewall de Windows.** El programa de instalación de Endpoint Protection permite activar o desactivar Firewall de Windows.  
-   **Sistema de inspección de redes.** Esta característica mejora la protección en tiempo real mediante la inspección del tráfico de red con el fin de ayudar de forma proactiva a bloquear los ataques a vulnerabilidades conocidas basadas en red.  
-   **Motor de protección.** La protección en tiempo real detecta e impide que el malware se instale o se ejecute en su equipo. El motor actualizado ofrece capacidades mejoradas de detección y limpieza con un mejor rendimiento.  

Windows Defender se incluye en el sistema operativo de Windows 10.  En versiones anteriores de Windows, su administrador puede proporcionar Windows Defender o Endpoint Protection mediante software de administración.

También encontrará una lista de las [preguntas más frecuentes sobre Windows Defender y Endpoint Protection](endpoint-protection-client-faq.md). Para ayudar en la solución de problemas, vea [Solución de problemas del cliente de Windows Defender o Endpoint Protection](troubleshoot-endpoint-client.md). Para obtener una lista de características nuevas, vea [Novedades de Windows Defender](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Integración con el Firewall de Windows  
 El Firewall de Windows ayuda a impedir que los atacantes o el software malintencionado obtengan acceso al equipo a través de Internet o de una red. Ahora, cuando instala Endpoint Protection, el Asistente para instalación comprueba que el Firewall de Windows esté activado. Si ha desactivado deliberadamente el Firewall de Windows, puede evitar que se active desactivando una casilla. Puede cambiar la configuración del Firewall de Windows en cualquier momento a través de las opciones de Sistema y seguridad en el Panel de control.  

## <a name="network-inspection-system"></a>Sistema de inspección de redes  
 Los atacantes efectúan cada vez más ataques basados en red contra vulnerabilidades que están expuestas antes de que los proveedores de software puedan desarrollar y distribuir actualizaciones de seguridad. Los estudios de las vulnerabilidades muestran que puede transcurrir un mes o más desde el momento de la notificación del ataque inicial hasta que se desarrolle, pruebe y publique una actualización de seguridad adecuada. Este intervalo sin protección deja a muchos equipos a merced de los ataques durante un periodo de tiempo considerable. El sistema de inspección de redes trabaja con la protección en tiempo real para proteger mejor a los equipos frente a ataques basados en red; para ello, reduce enormemente el intervalo de tiempo entre la detección de la vulnerabilidad y el desarrollo de un parche, que pasa a ser de semanas a unas pocas horas.  

## <a name="award-winning-protection-engine"></a>Motor de protección galardonado  
 En el interior de Windows Defender o Endpoint Protection, se actualiza regularmente su galardonado motor de protección. El motor está respaldado por un equipo de investigadores en antimalware del Centro de protección contra malware de Microsoft, y ofrece respuestas respecto a las amenazas de malware más recientes durante las 24 horas del día.  

## <a name="windows-defender-settings"></a>Configuración de Windows Defender
La configuración de Windows Defender permite opciones que ayudan a proteger su equipo de software malintencionado. Su administrador puede administrarle algunas opciones de Windows Defender. Puede administrar otras con la configuración de Windows Defender. Le recomendamos que permita que la configuración de Windows Defender le ayude a proteger su equipo y sus datos.

Para ver la configuración de Windows Defender, busque `Windows Defender` en su equipo. Abra **Windows Defender** y seleccione **Configuración**. La configuración de Windows Defender incluye:
- **Protección en tiempo real**: detecta e impide que el malware se instale o se ejecute en su equipo.
- **Protección basada en la nube**: Windows Defender envía información a Microsoft sobre amenazas de seguridad potenciales.
- **Envío de muestras automático**: permite que Windows Defender envíe muestras de archivos sospechosos a Microsoft para ayudar a mejorar la detección de malware.
- **Exclusiones**: puede excluir procesos, extensiones de archivo, carpetas o archivos específicos del análisis de Windows Defender.
- **Notificación mejorada**: permite las notificaciones que informan sobre el estado de su equipo. Incluso en el estado **Desactivado** recibirá notificaciones importantes.
- **Windows Defender sin Conexión**: puede ejecutar Windows Defender sin Conexión para ayudar a buscar y quitar software malintencionado. Este análisis reiniciará su equipo y tardará unos 15 minutos.

### <a name="see-also"></a>Vea también  
 [Preguntas más frecuentes sobre el cliente de Endpoint Protection](endpoint-protection-client-faq.md)   
 [Solución de problemas del cliente de Windows Defender o Endpoint Protection](troubleshoot-endpoint-client.md)
