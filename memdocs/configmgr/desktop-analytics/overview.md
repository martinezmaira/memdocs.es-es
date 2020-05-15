---
title: Análisis de escritorio
titleSuffix: Configuration Manager
description: Información general del servicio Análisis de escritorio integrado con Configuration Manager.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 23af311a78058240e6ebf8a2ca3c9e0fcdaf711f
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268562"
---
# <a name="what-is-desktop-analytics"></a>¿Qué es Análisis de escritorio?

Análisis de escritorio es un servicio basado en la nube que se integra con Configuration Manager. Este servicio proporciona información detallada e inteligente para que pueda tomar decisiones más fundamentadas sobre la preparación de actualizaciones de sus clientes Windows. Combina datos de su organización con datos agregados de millones de dispositivos conectados a servicios en la nube de Microsoft.

Use Análisis de escritorio con Configuration Manager para:  

- Crear un inventario de las aplicaciones que se ejecutan en su organización  

- Evaluar la compatibilidad de aplicaciones con las últimas actualizaciones de características de Windows 10  

- Identificar problemas de compatibilidad y recibir sugerencias de mitigación basadas en la información de datos habilitados para la nube  

- Crear grupos piloto que representen todo el estado de la aplicación y el controlador en un conjunto mínimo de dispositivos.  

- Implementar Windows 10 en dispositivos piloto y administrados por producción  

![Captura de pantalla de la página principal de Análisis de escritorio.](media/portal-home.png)

El siguiente vídeo es una sesión de Ignite 2019, que incluye más información sobre Análisis de escritorio:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Uso de Análisis de escritorio y de Configuration Manager para reducir el costo total de propiedad de Windows mediante información basada en datos para la administración, mantenimiento y soporte técnico](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Vaya al minuto 10:00 para obtener una demostración detallada.

> [!Note]  
> Análisis de escritorio es el sucesor de Windows Analytics, que se retiró el 31 de enero de 2020.
>
> Las funcionalidades de Windows Analytics se combinan en el servicio Análisis de escritorio. Análisis de escritorio también está integrado en mayor medida con Configuration Manager. Para obtener más información, consulte las [preguntas más frecuentes para clientes de Windows Analytics](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Ventajas

Muchos clientes tienen dificultades para estar siempre actualizados con Windows 10. El principal desafío es la prueba de las aplicaciones. Este proceso suele ser manual. Para los administradores de TI y los propietarios de aplicaciones, se tarda mucho tiempo en analizar continuamente las aplicaciones existentes. Además, tienen que corregir luego los problemas que surjan.

Análisis de escritorio ofrece las siguientes ventajas:

- **Inventario de hardware y software**: inventario de factores clave, como aplicaciones y versiones de Windows.  

- **Identificación de piloto**: identificación del conjunto más pequeño de dispositivos que proporcionan la más amplia cobertura de factores. Se centra en los factores que son más importantes para una prueba piloto de las actualizaciones de Windows. Al tener la seguridad de que el piloto es más satisfactorio, puede seguir ampliando con rapidez y confianza las implementaciones en producción.  

- **Identificación de problemas**: con los datos de mercado agregados en combinación con los datos de su entorno, el servicio predice posibles problemas para estar siempre actualizado con Windows. Luego, sugiere posibles mitigaciones.  

- **Integración de Configuration Manager**: el servicio habilita para la nube la infraestructura local existente. Use estos datos y análisis para implementar y administrar Windows en sus dispositivos.  

## <a name="prerequisites"></a>Requisitos previos

Para usar Análisis de escritorio, asegúrese de que el entorno cumple los requisitos previos siguientes.

### <a name="technical"></a>Técnicos

- Una suscripción de Azure global activa, con permisos de [administrador global](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions). No se admiten [cuentas Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts).  

    > [!Important]  
    > Actualmente, Análisis de escritorio requiere la implementación de un servicio de Office 365 en su inquilino de Azure AD. Esto no será un requisito en el futuro.

    - Permisos de **propietario del área de trabajo** para **configurar el área de trabajo** y los roles siguientes:  

      - Rol de [**administrador de Análisis de escritorio**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions).

      - [**Colaborador de Log Analytics**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) y [**administrador de acceso de usuario** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) en el grupo de recursos para usar un área de trabajo existente o crear una nueva área de trabajo en un grupo de recursos existente.

      - Permisos de [**propietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), o [**colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) y [**administrador de acceso de usuario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) en la suscripción para crear un área de trabajo en un nuevo grupo de recursos.  

    - Para acceder al portal después de la incorporación, necesita:

      - El rol de [**administrador de Desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) y los permisos de [**propietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) o [**colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) en el grupo de recursos donde se creó el área de trabajo.

- Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571), o posterior Para obtener más información, vea [Actualización de Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    - Rol de [**administrador total**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) en Configuration Manager  

    > [!NOTE]
    > Análisis de escritorio admite varias jerarquías de Configuration Manager que informan a un único inquilino de Azure AD.<!-- 4814075 --> Si tiene varias jerarquías en su entorno, tiene las siguientes opciones:
    >
    > - Use diferentes identificadores comerciales e inquilinos de Azure AD.
    > - Configure ambas jerarquías para que usen el mismo identificador comercial para compartir el inquilino de Azure AD y la instancia de Análisis de escritorio.

- Dispositivos que ejecutan Windows 7, Windows 8.1 o Windows 10  

    - Instale las actualizaciones más recientes. Para obtener más información, consulte [Actualización de dispositivos](enroll-devices.md#update-devices).  

    - Los dispositivos necesitan también el cliente Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571), o posterior. Para obtener más información, vea [Actualización de Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    > [!Note]  
    > Análisis de escritorio no es compatible con las actualizaciones al canal de mantenimiento a largo plazo (LTSC) de Windows 10. Para más información, consulte [Administración de Windows como servicio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Análisis de escritorio está diseñado para ofrecer el mejor respaldo a las actualizaciones en contexto. Si necesita realizar cambios importantes, como, por ejemplo, pasar de la arquitectura de 32 bits a 64 bits, utilice un escenario de creación de imágenes. Aunque la información de Análisis de escritorio sigue siendo valiosa en estos escenarios de implementación de sistema operativo clásicos, se pueden omitir las instrucciones específicas de la actualización local. Para obtener más información, consulte [Escenarios para implementar sistemas operativos de empresa con Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Datos de diagnósticos de Windows. Vea los siguientes artículos para más información:  

    - [Niveles de datos de diagnóstico](enable-data-sharing.md#diagnostic-data-levels)  

    - [Privacidad de Análisis de escritorio](privacy.md)  

- Conectividad de red desde dispositivos a la nube pública de Microsoft. Para más información, consulte [Habilitación del uso compartido de datos](enable-data-sharing.md).  

> [!Important]
> Microsoft está firmemente comprometido a proporcionar las herramientas y los recursos que le sitúan al mando de su privacidad. Como resultado, Microsoft no recopila los datos siguientes de los dispositivos ubicados en países europeos (EEE y Suiza):
>
> - Datos de diagnóstico de Windows desde dispositivos Windows 8.1
> - Datos de uso de aplicaciones para Windows 7

### <a name="licensing-and-costs"></a>Licencias y costes

- Suscripción activa de Azure global

    > [!NOTE]
    > La mayoría de las suscripciones equivalentes para Configuration Manager también incluyen Azure AD. Por ejemplo, vea los [planes de Microsoft 365](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) y las [licencias de Enterprise Mobility + Security](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Los dispositivos inscritos en Análisis de escritorio necesitan una licencia válida de Configuration Manager. Para obtener más información, vea [Licencia de Configuration Manager](../core/understand/product-and-licensing-faq.md).

- Los usuarios del dispositivo necesitan una de estas licencias:

  - Windows 10 Enterprise E3 o E5 (incluido en Microsoft 365 F3, E3 o E5)

  - Windows 10 Education A3 o A5 (incluido en Microsoft 365 A3 o A5)

  - Acceso a Windows Virtual Desktop E3 o E5  

> [!NOTE]
> Además del costo de suscripción de estas licencias, no hay ningún costo adicional por el uso de Azure Log Analytics. Los tipos de datos ingeridos por Análisis de escritorio no tienen ningún cargo por ingesta y retención de datos de Log Analytics. Como son tipos de datos no facturables, estos datos tampoco están sujetos a ningún límite de ingesta diaria de datos de Log Analytics. Para obtener más información, vea [Uso y costo de Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="next-steps"></a>Pasos siguientes

En el siguiente tutorial se proporciona una guía paso a paso para empezar a trabajar con Análisis de escritorio y Configuration Manager:
  
> [!div class="nextstepaction"]
> [Implementación de Windows 10 en el piloto](tutorial-windows10.md)
