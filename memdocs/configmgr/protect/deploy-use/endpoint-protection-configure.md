---
title: Configurar Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar Configuration Manager para actualizar y distribuir definiciones de malware de Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704523"
---
# <a name="configure-endpoint-protection"></a>Configurar Endpoint Protection

*Se aplica a: Configuration Manager (rama actual)*

Para poder usar Endpoint Protection para administrar la seguridad y el malware en equipos cliente de Configuration Manager, debe seguir los pasos de configuración que se detallan en este artículo.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Cómo configurar Endpoint Protection en Configuration Manager  
 Endpoint Protection en Configuration Manager tiene dependencias externas y dependencias en el producto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Pasos para configurar Endpoint Protection en Configuration Manager  
 La tabla siguiente proporciona pasos, detalles y más información sobre el procedimiento para configurar Endpoint Protection.  

> [!IMPORTANT]  
>  Si administra Endpoint Protection para equipos Windows 10, debe configurar Configuration Manager para actualizar y distribuir las definiciones de malware de Windows Defender. Windows Defender se incluye en Windows 10, pero aun así se tiene que instalar SCEPInstall y se necesita la configuración de cliente personalizada de Endpoint Protection (consulte el **paso 5** más adelante). </br> </br>
> A partir de Configuration Manager 1802, no es necesario que los dispositivos Windows 10 tengan instalado el Agente de Endpoint Protection (SCEPInstall). Si ya está instalado en los dispositivos Windows 10, Configuration Manager no lo quitará. Los administradores pueden quitar el Agente de Endpoint Protection en los dispositivos Windows 10 en los que se ejecute como mínimo la versión 1802 del cliente. Es posible que SCEPInstall.exe siga presente en C:\Windows\ccmsetup en algunos equipos, pero no se debe descargar en las instalaciones de cliente nuevas. Las opciones de cliente personalizadas para Endpoint Protection (**Paso 5** a continuación) siguen siendo necesarias. <!--503654-->

|Pasos|Detalles|  
|-----------|-------------|  
|**Paso 1:** [Crear un rol de sistema de sitio de punto de Endpoint Protection](endpoint-protection-site-role.md)|El rol de sistema de sitio de punto de Endpoint Protection debe estar instalado para poder usar Endpoint Protection. Se debe instalar en un solo servidor de sistema de sitio y en la parte superior de la jerarquía en un sitio de administración central o un sitio primario independiente. |  
|**Paso 2:** [Configuración de alertas para Endpoint Protection](endpoint-configure-alerts.md)|Las alertas informan al administrador si se han producido eventos específicos, como una infección de malware. Las alertas se muestran en el nodo **Alertas** del área de trabajo **Supervisión** o, de forma alternativa, pueden enviarse por correo electrónico a los usuarios especificados. |  
|**Paso 3:** [Configurar orígenes de actualizaciones de definiciones para clientes de Endpoint Protection](endpoint-definition-updates.md)|Es posible configurar Endpoint Protection para que use diversos orígenes para la descarga de actualizaciones de definiciones. |  
|**Paso 4:** [Configurar la directiva antimalware predeterminada y crear directivas antimalware personalizadas](endpoint-antimalware-policies.md)|La directiva antimalware predeterminada se aplica si está instalado el cliente de Endpoint Protection. Toda directiva personalizada que haya implementado se aplica de forma predeterminada, en los 60 minutos posteriores a la implementación del cliente. Asegúrese de que configuró las directivas antimalware antes de implementar el cliente de Endpoint Protection. |  
|**Paso 5:** [Establecer una configuración de cliente personalizada para Endpoint Protection](endpoint-protection-configure-client.md)|Use las opciones de cliente personalizadas con el fin de configurar las opciones de Endpoint Protection para las recopilaciones de equipos de la jerarquía.<br /><br /> Nota: No configure las opciones de cliente personalizadas de Endpoint Protection a menos que esté seguro de que quiere aplicarlas a todos los equipos de la jerarquía. |  
