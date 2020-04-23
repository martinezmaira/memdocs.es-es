---
title: Preguntas más frecuentes sobre productos y licencias
titleSuffix: Configuration Manager
description: Encuentre respuestas a las preguntas comunes sobre productos y licencias de Configuration Manager.
ms.date: 02/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63e53c502e67d2bfbfc5f8a706006c6ec14f8fcd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706843"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Preguntas más frecuentes sobre las licencias y ramas de Configuration Manager

*Se aplica a: Configuration Manager (rama actual) y System Center Configuration Manager (rama de mantenimiento a largo plazo)*

Estas preguntas más frecuentes tratan las preguntas comunes sobre licencias de la rama actual de Configuration Manager y las versiones de la rama de mantenimiento a largo plazo (LSTB), disponibles a través de los programas de Licencias por Volumen de Microsoft. Este artículo solo tiene fines informativos. No reemplaza ni sustituye ninguna documentación que trate sobre las licencias de Configuration Manager. Para obtener más información, consulte [Términos del producto](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). En las condiciones del producto se describen los términos de uso de todos los productos de Microsoft en las licencias por volumen.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a> ¿Qué es la rama actual?

La rama actual es la compilación lista para producción de Configuration Manager que proporciona un modelo de servicio activo. Este modelo de servicio es como la experiencia con Windows 10. Este enfoque es compatible con los clientes que se van a mover a una cadencia en la nube y quieren innovar más rápidamente. Con el modelo de servicio de la rama actual, sigue recibiendo nuevas funciones y características. Por esta razón, solo los clientes con Software Assurance activo en las licencias de Configuration Manager, o con derechos de suscripción equivalentes, pueden instalar y usar la rama actual de Configuration Manager.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a> ¿Qué es la rama de mantenimiento a largo plazo (LTSB)?  

La LTSB es una compilación lista para producción de Configuration Manager. Se ha pensado para aquellos clientes que permiten que Software Assurance o derechos de suscripción equivalentes expiren. Comparada con la rama actual, la LTSB tiene una [funcionalidad reducida](introduction-to-the-ltsb.md#features-that-arent-available). Los clientes que permiten que Software Assurance o derechos de suscripción equivalentes expiren, deben desinstalar la rama actual de Configuration Manager. Los clientes que tengan derechos de licencia perpetuos para Configuration Manager pueden instalar y usar la compilación de LTSB de la versión de Configuration Manager que esté vigente en el momento de la expiración.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a> ¿Qué significan los acrónimos *SA* y *L&SA* con respecto a Configuration Manager?

Tanto **Software Assurance** (SA) como **Licencia y Software Assurance** (L&SA) son opciones de licencia que conceden derechos para usar Configuration Manager. SA es una opción para un cliente que está renovando la cobertura de SA de un contrato anterior. L&SA es una opción para un cliente que compra una licencia nueva y cobertura de SA.

- **Software Assurance (SA)** : los clientes necesitan tener SA activo en las licencias de Configuration Manager, o derechos de suscripción equivalentes, para instalar y usar la opción de rama actual de Configuration Manager.

  Aunque SA es opcional para algunos productos de Microsoft, la única manera de obtener derechos para usar la rama actual de Configuration Manager es con SA *(o derechos de suscripción equivalentes)* . Para más información, consulte [Preguntas más frecuentes sobre Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Licencia y Software Assurance (L&SA) de Microsoft:** Los clientes que compran licencias nuevas para Configuration Manager necesitan comprar L&SA (la licencia y la cobertura de SA).

  - SA concede derechos para usar la rama actual.

  - Si el SA expira y todavía tiene una licencia de Configuration Manager, ya no podrá usar la rama actual. Para obtener más información, vea la pregunta [Si mi SA expira y tenía L&SA, ¿qué obtengo?](#bkmk_sa-expires)

Para obtener más información sobre las ofertas de licencias, consulte [Formas comprar](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) y [Términos de licencia del producto](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a> ¿Qué son las *suscripciones equivalentes*?

Las suscripciones equivalentes hacen referencia a programas como [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) o [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Pueden existir otros, pero estos programas son los más comunes. Los términos del producto de las Licencias por Volumen de Microsoft se refieren a esos programas como licencias equivalentes de las licencias de administración.

Configuration Manager se incluye en los planes siguientes:

- Licencia de suscripción de usuario (USL) de Intune
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F1

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager no está incluido en el plan [Microsoft 365 Empresa](https://www.microsoft.com/microsoft-365/business).

### <a name="does-anything-change-with-the-rebrand-to-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> ¿Ha cambiado algo con el cambio de personalización de marca a Microsoft Endpoint Manager?

Sí. A partir del 1 de diciembre de 2019, si ya tiene una licencia de Configuration Manager, también se le concederá automáticamente una licencia de Intune para inscribir equipos Windows en la [administración conjunta](../../comanage/overview.md). Este cambio facilita la administración de dispositivos con Microsoft Endpoint Manager.

Ahora hay disponible una nueva licencia con la que los clientes de Configuration Manager con Software Assurance obtendrán derechos de administración de equipos de Intune sin tener que adquirir una licencia de Intune adicional para la administración conjunta. Ya no es necesario comprar ni asignar licencias individuales de Intune a los usuarios.

- Los dispositivos administrados por Configuration Manager e inscritos en la administración conjunta tienen casi los mismos derechos que un equipo administrado de manera independiente de Intune, pero después de un restablecimiento no se pueden volver a aprovisionar con AutoPilot.

- Los dispositivos Windows 10 inscritos en Intune mediante otros medios requieren licencias de Intune completas.

- Si quiere usar Intune para administrar dispositivos iOS, Android o macOS, necesitará la suscripción a Intune adecuada a través de una licencia de Intune independiente, Enterprise Mobility + Security (EMS) o Microsoft 365.

- La licencia que tenía anteriormente para System Center Configuration Manager seguirá siendo válida en Microsoft Endpoint Configuration Manager. Si instala un nuevo sitio, use las claves de producto existentes.

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a> Tengo Enterprise Mobility + Security y ha expirado, ¿qué debo hacer ahora?  

EMS concede derechos para usar Configuration Manager (rama actual y rama de mantenimiento a largo plazo). Cuando estos derechos expiran, ya no tiene derechos para usar ninguna rama y debe realizar la desinstalación.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a> Si mi SA expira y tenía L&SA, ¿qué obtengo?

Si su SA ha expirado después del 1 de octubre de 2016, dependiendo de bajo qué programa haya adquirido L&SA, puede conservar una licencia perpetua para usar la LTSB. Si en estos momentos usa la rama actual, debe desinstalarla y, después, instalar la LTSB. No existe ninguna compatibilidad de migración ni de conversión desde la rama actual a LTSB.

Si su SA ha expirado antes del 1 de octubre de 2016 y conservaba una licencia perpetua de Configuration Manager, entonces su única opción para un uso continuado es instalar y usar System Center 2012 R2 Configuration Manager y sus Service Packs disponibles. Se le pide desinstalar la rama actual cuando su SA expire, y volver a instalar esa versión anterior del producto. No existe ninguna compatibilidad de migración ni de cambiar de la rama actual de Configuration Manager a versiones anteriores de Configuration Manager.

Si usa System Center Endpoint Protection y su SA expira, debe desinstalarlo. System Center Endpoint Protection no ofrece derechos *L (licencia)* ni derechos perpetuos.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a> ¿La rama actual es de mi propiedad?

No. Tiene la licencia para usar la rama actual mientras tenga SA activo. Por ejemplo, mediante *L&SA*, cuando *SA* expira, entonces solo tiene derechos *L (Licencia)* , que no incluye derechos para usar la rama actual. Si su L proporciona derechos perpetuos, puede usar la LTSB de Configuration Manager en lugar de la rama actual. Si su SA expiró antes del 1 de octubre de 2016, también puede usar System Center 2012 R2 Configuration Manager.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a> ¿Puedo comprar Configuration Manager independiente sin SA?

No. La única manera de obtener derechos para usar Configuration Manager es adquirir una licencia con SA o a través de una suscripción equivalente. Existen programas de desarrolladores (como MSDN) donde Configuration Manager se ofrece con fines de pruebas y desarrollo, pero no para un uso de producción.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> ¿Un entorno que no es de producción para pruebas o desarrollo requiere una licencia explícita?

<!-- SCCMDocs#1848 -->

- Si usa el mismo software de rama actual que el entorno de producción, necesita una licencia explícita. Consulte a su equipo de cuentas para determinar si el contrato de licencia específico incluye varias instancias en varios entornos.

- Algunos programas de desarrolladores, como MSDN, ofrecen productos como Configuration Manager con fines de pruebas y desarrollo, pero no para un uso de producción.

- Para un entorno temporal, puede usar la [versión de evaluación](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) durante 180 días.

- Para un entorno de laboratorio, puede usar la [rama de Technical Preview](../get-started/technical-preview.md). Technical Preview tiene la misma funcionalidad que la rama actual, pero cuenta con algunas limitaciones en cuanto a escala y plataformas admitidas.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> ¿Tengo derechos para instalar cualquier actualización en la consola de Configuration Manager?

Si tiene un *SA* activo, los tiene.

Si no tiene un SA activo, desinstale la rama actual y, después, puede instalar la LTSB de Configuration Manager. La LTSB no recibe actualizaciones para las versiones incrementales de Configuration Manager, pero recibe actualizaciones de seguridad según el ciclo de vida de soporte técnico.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a> He adquirido EMS o Microsoft 365 a través de un proveedor de soluciones en la nube (CSP), ¿tengo que derechos para usar Configuration Manager?

Sí, tiene derechos para usar Configuration Manager para administrar clientes cubiertos por la licencia de EMS. En primer lugar descargue e instale el [software de evaluación](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Luego póngase en contacto con el Soporte técnico de Microsoft para obtener la clave de licencia.<!--issue472--> Cuando hable con el Soporte técnico de Microsoft, pídales que consulten el artículo interno con identificador 4033838.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a> ¿La fecha de finalización de mi suscripción es lo mismo que una fecha de expiración de SA?

Si *SA* o su suscripción está activa, tiene derechos de uso de la rama actual de Configuration Manager. Una suscripción activa equivale a tener un *SA* activo, pero no una *"L" (licencia)* perpetua. Una vez que su suscripción haya expirado, desinstale la rama actual. En este momento, no tiene derechos para usar la LTSB.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a> ¿Cuáles son los derechos de uso asociados con la tecnología SQL proporcionada con Configuration Manager?

Configuration Manager incluye tecnología SQL Server. Los términos de licencia de Microsoft relativos a estos productos permiten usar tecnología SQL Server solo para admitir componentes de Configuration Manager. No se requieren licencias de acceso de cliente SQL Server para ese uso.

Los derechos de uso aprobados para las funcionalidades de SQL con Configuration Manager incluyen:

- Rol de base de datos de sitio
- Windows Server Update Services (WSUS) para el rol de punto de actualización de software
- SQL Server Reporting Services (SSRS) para el rol de punto de informes
- Rol de punto de servicio de almacenamiento de datos
- Réplicas de bases de datos para roles de puntos de administración

La licencia de SQL Server que se incluye con Configuration Manager es compatible con cada instancia de SQL Server que instale para hospedar una base de datos para Configuration Manager. Sin embargo, solo las bases de datos para Configuration Manager de la lista anterior pueden ejecutarse en ese servidor SQL Server cuando se utiliza esta licencia. Si una base de datos de cualquier producto adicional de Microsoft o de terceros comparte la instancia de SQL Server, debe tener una licencia independiente para esa instancia de SQL Server.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a> ¿La administración local de dispositivos móviles (MDM) requiere una suscripción a Intune?

En las versiones 1806 y anteriores, para empezar a usar la administración local de dispositivos móviles, necesita una suscripción a Microsoft Intune. La suscripción solo es necesaria para realizar el seguimiento de las licencias de los dispositivos y no se usa para administrar ni almacenar la información de administración de los dispositivos. La totalidad de la administración se almacena en la organización a través de la infraestructura local de Configuration Manager.  

A partir de la versión 1810, ya no se necesita una conexión a Intune para las nuevas implementaciones de MDM locales.<!--3607730, fka 1359124--> La organización sigue necesitando licencias de Intune para usar esta característica. Para más información, vea la [entrada del blog de soporte técnico de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).
