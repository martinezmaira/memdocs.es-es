---
title: Más información sobre la seguridad del script de PowerShell
titleSuffix: Configuration Manager
description: Recursos para obtener más información sobre la seguridad del script de PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a0edf83c736c2737f4af2f040159a71bb0348aee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689313"
---
# <a name="learn-more-about-powershell-script-security"></a>Más información sobre la seguridad del script de PowerShell

*Se aplica a: Configuration Manager (rama actual)*

Es responsabilidad del administrador validar el uso propuesto de PowerShell y los parámetros de PowerShell en el entorno. Aquí se muestran algunos recursos útiles para ayudar a educar a los administradores sobre la eficacia de PowerShell y los riesgos posibles. Esto sirve para ayudar a mitigar posibles riesgos y permitir que se usen scripts seguros.

## <a name="powershell-script-security"></a>Seguridad del script de PowerShell
Integrada en Ejecutar scripts, hay una característica para revisar y aprobar visualmente los scripts que se solicitan para ejecutarse en el entorno. Los administradores deben tener en cuenta que los scripts de PowerShell pueden contener scripts ofuscados: scripts malintencionados y difíciles de detectar mediante inspección visual durante el proceso de aprobación de los scripts. Como procedimiento recomendado, el uso de ciertas herramientas de inspección, además de la revisión visual de los scripts de PowerShell, ayudará a detectar problemas de scripts sospechosos. Estas herramientas no siempre pueden determinar la intención del autor de PowerShell, pero pueden llamar la atención sobre un script sospechoso. Pero las herramientas requerirán que el administrador juzgue si se trata de una sintaxis de script malintencionada o intencionada.

## <a name="recommendations"></a>Recomendaciones
- Familiarícese con los procedimientos recomendados de seguridad de PowerShell mediante los vínculos que se muestran a continuación.
- **Firmar los scripts**: otro método para mantener la seguridad de los scripts consiste en inspeccionarlos y después firmarlos, antes de importarlos para su uso.
- No almacene secretos (como contraseñas) en los scripts de PowerShell y obtenga más información sobre cómo administrar los secretos.


## <a name="general-information-about-powershell-security-best-practices"></a>Información general sobre los procedimientos recomendados de seguridad de PowerShell

Se ha elegido esta colección de vínculos para proporcionar a los administradores de Configuration Manager un punto de partida para obtener información sobre los procedimientos recomendados de seguridad de PowerShell.  

[Introduction to PowerShell Security Best Practices](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ ) (Introducción a los procedimientos recomendados de seguridad de PowerShell)

[PowerPoint de procedimientos recomendados de seguridad de PowerShell](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Defending Against PowerShell Attacks, PowerShell team blog](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/) (Defensa contra los ataques a PowerShell, blog del equipo de PowerShell)

[Defending Against PowerShell Attacks twitter, from a Microsoft PowerShell and Security advocate Lee Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208) (Defensa contra los ataques a PowerShell, Twitter de Lee Holmes, defensor de Microsoft PowerShell y seguridad)

[Protecting Against Malicious Code Injection](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/) (Protección contra la inserción de código malintencionado)

[PowerShell The Blue Team, discusses Deep Script block logging, Protected Event Logging, Antimalware Scan Interface, Secure Code Generation APIs](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/) (Blue Team de PowerShell analiza el registro de bloques Deep Script, el registro de eventos protegido, la interfaz de examen antimalware y las API de generación de código seguro)

[Para Windows 10, hay una API para una interfaz de examen antimalware](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Seguridad de los parámetros de PowerShell
Pasar parámetros es una manera de disponer de flexibilidad con los scripts y delegar las decisiones hasta el tiempo de ejecución. También abre otra superficie de riesgo. Los procedimientos recomendados para evitar parámetros malintencionados o la inserción de scripts son:

- Permitir únicamente el uso de parámetros predefinidos.
- Usar la característica de expresión regular para validar los parámetros que se permiten.
    - Ejemplo: Si solo se permite un intervalo determinado de valores, use una expresión regular para comprobar únicamente los caracteres o valores que pueden formar el intervalo.
    - La validación de parámetros puede ayudar a evitar que los usuarios intenten usar determinados caracteres que se pueden escapar, como las comillas. Tenga en cuenta que puede haber varios tipos de comillas, por lo que el uso de expresiones regulares para validar los caracteres que se han elegido como permitidos a menudo es más fácil que intentar definir todas las entradas que no se permiten.
- Aprovechar el módulo de PowerShell ["injection hunter"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) (cazador de inserciones) de la Galería de PowerShell.
    - Puede haber falsos positivos, por lo que cuando algo se marque como sospechoso, busque la intención para determinar si se trata de un problema real o no. 
- Microsoft Visual Studio tiene un analizador de scripts, que puede ayudar con la comprobación de la sintaxis de PowerShell.
- En este vídeo, titulado “DEF CON 25 - Lee Holmes - Get $pwned: Attacking Battle Hardened Windows Server” (atacar una instancia de Windows Server preparada para la batalla), se proporciona información general sobre los tipos de problemas para los que puede protegerse (especialmente, la sección de 12:20 a 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Recomendaciones de entorno
Recomendaciones generales para los administradores de PowerShell.
1. Implemente la versión más reciente de PowerShell, como la versión 5 o superior, integrada en Windows 10. Como alternativa, puede implementar [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616). 
2. Habilite y recopile registros de PowerShell, incluyendo de forma opcional el registro de eventos protegido. Incorpore estos registros a los flujos de trabajo de firma, búsqueda y respuesta a incidentes.
3. Implemente Just Enough Administration en sistemas de gran valor para eliminar o reducir el acceso administrativo sin restricciones a esos sistemas.
4. Implemente directivas de control de aplicaciones de Windows Defender para permitir que las tareas administrativas aprobadas previamente usen todas las funciones del lenguaje de PowerShell, a la vez que se limita el uso interactivo y no aprobado a un subconjunto limitado del lenguaje de PowerShell.
5. Implemente Windows 10 para proporcionar al proveedor de antivirus acceso completo a todo el contenido (incluido el contenido generado o desofuscado en tiempo de ejecución) procesado por Windows Scripting Hosts incluido PowerShell.
