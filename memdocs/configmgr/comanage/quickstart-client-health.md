---
title: Estado del cliente con la administración conjunta
titleSuffix: Configuration Manager
description: Mantenga la visibilidad del estado de cliente de Configuration Manager desde Intune en Azure Portal.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690833"
---
# <a name="client-health-with-co-management"></a>Estado del cliente con la administración conjunta

El estado de la red está vinculado directamente al estado de los dispositivos que se conectan y desconectan de ella. Intune puede comunicarse con un cliente en mal estado, incluso cuando no está en la red. Use la administración conjunta para combinar esta característica con la capacidad de Configuration Manager de informar del 98 % de los clientes en buen estado conocidos. Así, puede detectar, evaluar y proporcionar visibilidad en todos los clientes en tiempo real. Intune también agrega la compatibilidad necesaria para las actualizaciones de cumplimiento a través de todos los clientes conectados.

En el siguiente vídeo, el Jefe de Programas Senior Rob York y el Jefe de Marketing de Productos Locky Ainley abordan el estado de los clientes con la administración conjunta y demuestran su funcionamiento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Ventajas

Evaluar el estado del cliente es una prioridad de primer orden. System Center 2012 Configuration Manager ha agregado **CCMeval**. Esta utilidad es externa al cliente de Configuration Manager. Proporciona supervisión del estado del cliente y corrección automática. Sin embargo, esta capacidad de notificación se basa en un dispositivo que se encuentra físicamente o virtualmente en su red interna. La administración conjunta ayuda a resolver este problema.

Con la administración conjunta, Intune puede informar sobre el estado de mantenimiento del cliente. Proporciona información de marca de tiempo para la validez de los datos. Esta información le indica si los dispositivos están en buen estado, pueden conectarse, pueden instalar aplicaciones o pueden actualizar a las compilaciones necesarias del SO. 

Para obtener una descripción detallada de esta característica, vea este vídeo de la sesión [What's New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) (Novedades de Configuration Manager) en Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Cuando Configuration Manager proporciona el estado del dispositivo de que el cliente está instalado, pero no lo está, Intune puede proporcionar más información sin necesidad de conectarse al cliente. La información de estado del dispositivo en Intune es fácil de entender. Si el estado es distinto de **Correcto**, ofrece recomendaciones y pasos adicionales para solucionar el problema.

> [!Note]  
> Una versión futura prevé las siguientes ventajas:
> - Configuration Manager incluirá una funcionalidad adicional en CCMeval.  
> - Será más fácil identificar los equipos potencialmente en mal estado tanto en Configuration Manager como en Intune.  
> - Puede agrupar los datos de estado de cliente en Intune.  



## <a name="value-proposition"></a>Propuesta de valor

Con esta característica, ahora dispone de un origen de datos externo con Intune. Permite determinar los pasos siguientes para solucionar el problema de una amplia variedad de problemas del cliente. Ahora no es necesario crear informes adicionales o usar otras herramientas para extraer datos de cliente.

Cuando tenga clientes con un mantenimiento correcto, cumplirá oportunamente con las revisiones. Un mejor cumplimiento de las revisiones implica una mejor seguridad.



## <a name="configure"></a>Configurar

Para empezar a usar esta característica, siga estos pasos:

- Actualice los dispositivos a Windows 10, versión 1709 o posterior.  

- [Habilite la administración conjunta](how-to-enable.md).  
    - No es necesario cambiar ninguna carga de trabajo a Intune.  

- Actualice el sitio de Configuration Manager y los clientes a la *versión 1806* o posterior.  


### <a name="review-configuration-manager-client-health-in-intune"></a>Revise el estado del cliente de Configuration Manager en Intune.

1. Inicie sesión en [Azure Portal](https://portal.azure.com/).  

2. Elija **All services (Todos los servicios)**  > **Intune**. Intune se encuentra en la sección **Supervisión y administración**.  

3. Una vez que haya abierto el panel **Microsoft Intune**, en el menú bajo **Ayuda y soporte técnico**, vaya a la página **Troubleshooting**.  

4. Use la opción **Seleccionar usuario**, busque el dispositivo específico en la lista **dispositivos** y selecciónelo para abrir la página del dispositivo.  

5. La información de administración conjunta se muestra en la parte inferior de la página de dispositivos. Esta información incluye los siguientes campos para el estado de cliente:  
    - **Estado del agente de Configuration Manager**  
    - **Última inserción en el repositorio del agente de Configuration Manager**  

> [!Tip]  
> Los dispositivos inscritos en Intune se conectan al servicio de nube tres veces al día, cada ocho horas aproximadamente. 
