---
title: Acceso condicional con administración conjunta
titleSuffix: Configuration Manager
description: Controle el acceso a recursos de la organización según las reglas de cumplimiento de Intune.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f5b9addd35dd3e9252c1b988de4bb006e9a5bc0d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694974"
---
# <a name="conditional-access-with-co-management"></a>Acceso condicional con administración conjunta

El acceso condicional se asegura de que solo los usuarios de confianza puedan acceder a recursos de la organización en dispositivos de confianza con aplicaciones de confianza. Se crea a partir de cero en la nube. Siempre funciona igual, ya sea que esté administrando los dispositivos con Intune o ampliando la implementación de Configuration Manager con la administración conjunta.

En el siguiente vídeo, el Jefe de Programas Senior Joey Glocke y el Jefe de Marketing de Productos Locky Ainley abordan el acceso condicional con la administración conjunta y demuestran su funcionamiento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Con la administración conjunta, Intune evalúa todos los dispositivos de la red para determinar cuál es el nivel de confianza. Realiza esta evaluación de las dos maneras siguientes:

1. Intune se asegura de que un dispositivo o aplicación esté administrado y configurado con seguridad. Esta comprobación depende de cómo establezca las directivas de cumplimiento de su organización. Por ejemplo, asegúrese de que todos los dispositivos tengan habilitado el cifrado y que no se hayan liberado.  

    - Esta evaluación es anterior a la infracción de seguridad y se basa en la configuración.  

    - En el caso de los dispositivos administrados conjuntamente, Configuration Manager también realiza la evaluación basada en la configuración. Por ejemplo, actualizaciones requeridas o cumplimiento de aplicaciones. Intune combina esta evaluación junto con su propia evaluación.  

2. Intune detecta los incidentes de seguridad activos en un dispositivo. Usa la seguridad inteligente de [Protección contra amenazas avanzada de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (anteriormente ATP de Windows Defender) y otros [proveedores de defensa contra amenazas móviles](https://www.lookout.com/about/partners/microsoft). Estos asociados ejecutan los análisis de comportamiento en curso en los dispositivos. Este análisis detecta incidentes activos y, a continuación, pasa esta información a Intune para la evaluación de cumplimiento en tiempo real.  

    - Esta evaluación es posterior a la infracción de seguridad y se basa en incidentes.  

El Vicepresidente Corporativo de Microsoft Brad Anderson analiza el acceso condicional en profundidad con demostraciones en vivo durante el discurso de apertura de Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

El acceso condicional también proporciona un lugar centralizado para ver el estado de todos los dispositivos conectados en red. Obtiene las ventajas de la escala en la nube, que es especialmente valiosa para probar instancias de producción de Configuration Manager.


## <a name="benefits"></a>Ventajas

Cada equipo de TI está obsesionado con la seguridad de red. Es obligatorio asegurarse de que cada dispositivo cumpla con sus requisitos de seguridad y negocio antes de acceder a su red. Con el acceso condicional, puede determinar los factores siguientes: 
- Si se cifran todos los dispositivos  
- Si se instala malware  
- Si se actualiza la configuración  
- Si se ha liberado o modificado  

El acceso condicional combina el control detallado sobre los datos de la organización con una experiencia de usuario que maximiza la productividad del trabajador en cualquier dispositivo desde cualquier ubicación.

El siguiente vídeo muestra cómo se integra [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) en escenarios comunes que suelen producirse:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Con la administración conjunta, Intune puede incorporar las responsabilidades de Configuration Manager para evaluar el cumplimiento de los estándares de seguridad de actualizaciones o aplicaciones requeridas. Este comportamiento es importante para cualquier organización de TI que desee continuar utilizando Configuration Manager para la administración de revisiones y aplicaciones complejas.

El acceso condicional también es una parte fundamental del desarrollo de la arquitectura de la [red de Confianza cero](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/). Con acceso condicional, los controles de acceso a dispositivos compatibles abarcan las capas fundamentales de la red de Confianza cero. Esta funcionalidad es una gran parte del modo de proteger su organización en el futuro.

Para más información, vea la entrada de blog sobre [Enhancing conditional access with machine-risk data from Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559) (Mejora del acceso condicional con los datos de riesgo de la máquina de Protección contra amenazas avanzada de Microsoft Defender).



## <a name="case-studies"></a>Casos prácticos

La empresa de consultoría informática Wipro usa el acceso condicional para proteger y administrar los dispositivos usados por sus 91 000 empleados. En caso práctico reciente, el Vicepresidente de TI de Wipro señaló lo siguiente:

> *Lograr el acceso condicional es una gran victoria para Wipro. Ahora, todos los empleados tienen acceso móvil a la información a petición.* 
> *Hemos mejorado la productividad de nuestros empleados y nuestra situación en cuanto a seguridad. Ahora 91 000 empleados se benefician de un acceso muy seguro a más de 100 aplicaciones desde cualquier dispositivo, en cualquier lugar.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Otros ejemplos son: 

- Nestlé, que usa el acceso condicional basado en aplicaciones para más de 150 000 empleados.  

- La compañía de software de automatización, Cadence, que ahora puede asegurarse de que "solo los dispositivos administrados tengan acceso a las Aplicaciones de Microsoft 365, como Teams y la intranet de la compañía". También pueden ofrecer a sus recursos humanos "un acceso más seguro a otras aplicaciones basadas en la nube, como Workday y Salesforce". Para obtener más información acerca de la experiencia de Cadence con Intune, consulte [Cadence increases the pace of business with mobile collaboration tools in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365) (Cadence aumenta el ritmo de negocios con herramientas de colaboración móviles en Microsoft 365).

Intune también está totalmente integrado con asociados como Cisco ISE, Aruba Clear Pass y Citrix NetScaler. Con estos asociados, puede mantener los controles de acceso en función de la inscripción de Intune y el estado de cumplimiento de los dispositivos en estas otras plataformas.

Para obtener más información, consulte los vídeos siguientes:
- [Demostraciones del acceso condicional en detalle de Brad Anderson](https://youtu.be/8321obNofgM?t=547)  
- [Detalles adicionales de Endpoint Zone 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Propuesta de valor

Con el acceso condicional y la integración de ATP, se refuerza un componente fundamental de toda organización de TI: el acceso seguro a la nube.

En más del 63 % de todas las infracciones de datos, los atacantes obtienen acceso a la red de la organización por causa de credenciales de usuario poco seguras, predeterminadas o robadas. Dado que el acceso condicional se centra en la protección de la identidad del usuario, restringe el robo de credenciales. El acceso condicional administra y protege las identidades, tengan o no privilegios. No hay ninguna manera mejor de proteger los dispositivos y los datos que contienen.

Puesto que el acceso condicional es un componente principal de Enterprise Mobility + Security (EMS), no se necesitan instalaciones ni arquitecturas locales. Con Intune y Azure Active Directory (Azure AD), puede configurar rápidamente el acceso condicional en la nube. Si actualmente está usando Configuration Manager, puede ampliar fácilmente su entorno a la nube con la administración conjunta y empezar a usarlo ahora mismo.

Para más información sobre la integración con ATP, vea esta entrada de blog [Microsoft Defender ATP device risk score exposes new cyberattack, drives Conditional access to protect networks](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/) (La puntuación del riesgo de dispositivos de ATP de Microsoft Defender expone nuevos ataques cibernéticos e impulsa el acceso condicional para proteger las redes). Detalla cómo un grupo de hackers avanzados utilizó herramientas nunca antes vistas. La nube de Microsoft las detectó y las detuvo porque los usuarios seleccionados tenían acceso condicional. La intrusión activó la directiva de acceso condicional basado en riesgos del dispositivo. Aunque el atacante ya había establecido un punto de apoyo en la red, se restringió automáticamente el acceso de las máquinas explotadas a los servicios de la organización y los datos administrados por Azure AD.



## <a name="configure"></a>Configurar

El acceso condicional resulta fácil de usar cuando se [habilita la administración conjunta](how-to-enable.md). Requiere mover la carga de trabajo de las **directivas de cumplimiento** a Intune. Para más información, consulte [Cambiar las cargas de trabajo de Configuration Manager a Intune](how-to-switch-workloads.md). 

Para más información sobre el acceso condicional, consulte los artículos siguientes: 

- [Acceso condicional en Azure Active Directory](/azure/active-directory/conditional-access/overview)  

- [Introducción a las directivas de cumplimiento de dispositivos de Intune](/intune/device-compliance)  

- [Acceso condicional basado en aplicación con Intune](/intune/app-based-conditional-access-intune)  

> [!Note]  
> Las características de acceso condicional están disponibles de inmediato para dispositivos híbridos unidos a Azure AD. Estas características incluyen la autenticación multifactor y el control de acceso de unión a Azure AD. Este comportamiento se debe a que están basados en las propiedades de Azure AD. Para aprovechar la evaluación basada en configuración de Intune y Configuration Manager, habilite la administración conjunta. Esta configuración le brinda control de acceso directamente desde Intune para dispositivos compatibles. También le proporciona la característica de evaluación de las directivas de cumplimiento de Intune.