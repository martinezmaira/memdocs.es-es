---
title: Requisitos previos de perfil de Wi-Fi y VPN
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos previos para administrar perfiles de Wi-Fi y perfiles de VPN en Configuration Manager
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706073"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Requisitos previos de perfil de Wi-Fi y VPN en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los perfiles de Wi-Fi y VPN de Configuration Manager solo tienen dependencias dentro del producto.

Debe tener los permisos de seguridad siguientes para administrar la configuración de acceso a los recursos de la empresa, como perfiles de certificado, perfiles de Wi-Fi y perfiles de VPN:  

- Para ver y administrar alertas e informes para Wi-Fi y perfiles: **Crear**, **Eliminar**, **Modificar**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Alertas**.  

- Para crear y administrar perfiles de certificado: **Directiva de autor**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Perfil de certificado**.  

- Para administrar implementaciones de perfiles de Wi-Fi, de certificado y de VPN: **Implementar directivas de configuración**, **Modificar alerta de estado de cliente**, **Leer** y **Leer recurso** para el objeto **Recopilación**.  

- Para administrar todas las directivas de configuración: **Crear**, **Eliminar**, **Modificar**, **Leer** y **Establecer ámbito de seguridad** para el objeto **Directiva de configuración**.  

- Para ejecutar consultas relacionadas con perfiles de Wi-Fi y VPN: permiso **Leer** para el objeto **Consulta**.  

- Para ver la información de perfiles de Wi-Fi y VPN en la consola de Configuration Manager: Permiso de **Lectura** para el objeto **Sitio**.  

- Para ver los mensajes de estado para los perfiles de Wi-Fi y VPN: permiso **Leer** para el objeto **Mensajes de estado**.  

- Para crear y modificar el perfil de certificado de CA de confianza: **Directiva de autor**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Perfil de certificado de CA de confianza**.  

- Para crear y administrar perfiles de VPN: **Directiva de autor**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Perfil de VPN**.  

- Para crear y administrar perfiles de Wi-Fi: **Directiva de autor**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Perfil de Wi-Fi**.  

El rol de seguridad integrado **Administrador de acceso a los recursos de la empresa** incluye estos permisos que son necesarios para administrar los perfiles de Wi-Fi en Configuration Manager. Para más información, consulte [Configuración de la seguridad](../../core/plan-design/security/configure-security.md).
