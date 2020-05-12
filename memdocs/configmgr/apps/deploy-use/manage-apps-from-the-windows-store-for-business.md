---
title: Aplicaciones de Microsoft Store
titleSuffix: Configuration Manager
description: Administre e implemente aplicaciones desde Microsoft Store para Empresas y Educación con Configuration Manager.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d6a61324f8c777ba5ed09dd26816152d6f17af9
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643219"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Administración de aplicaciones desde Microsoft Store para Empresas y Educación con Configuration Manager

[Microsoft Store para Empresas y Educación](https://docs.microsoft.com/microsoft-store/) es el lugar donde buscar y comprar aplicaciones de Windows para la organización. Cuando se conecta la tienda a Configuration Manager, después se sincroniza la lista de aplicaciones que se han comprado. Puede ver estas aplicaciones en la consola de Configuration Manager e implementarlas como cualquier otra aplicación.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a> Aplicaciones en línea y sin conexión

Microsoft Store para Empresas y Educación admite dos tipos de aplicaciones:

- **En línea**: este tipo de licencia necesita que los usuarios y dispositivos se conecten a la tienda para obtener una aplicación y su licencia. Los dispositivos Windows 10 deben estar unidos a Azure Active Directory (Azure AD) o unidos a Azure AD híbrido.  

- **Sin conexión**: este tipo permite almacenar las aplicaciones y licencias en caché para implementarlas directamente en la red local. No es necesario que los dispositivos se conecten a la tienda o tengan una conexión a Internet.

Para obtener más información, vea [Introducción a Microsoft Store para Empresas y Educación](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Resumen de funcionalidades

Configuration Manager admite la administración de aplicaciones de Microsoft Store para Empresas y Educación tanto en dispositivos de Windows 10 con el cliente de Configuration Manager como en dispositivos de Windows 10 inscritos en Microsoft Intune. Configuration Manager ofrece las funciones siguientes para las aplicaciones en línea y sin conexión:

|Capacidad|Aplicaciones sin conexión|Aplicaciones en línea|
|------------|------------|------------|
|Sincronizar datos de la aplicación en Configuration Manager<br>(la sincronización se produce cada 24 horas)|Sí|Sí|
|Crear aplicaciones de Configuration Manager desde las aplicaciones de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones gratuitas de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones de pago de la tienda|No|Sí<sup>[Nota 1](#bkmk_note1)</sup>|
|Compatibilidad con las implementaciones necesarias para las colecciones de usuarios o dispositivos|Sí|Sí|
|Compatibilidad con las implementaciones disponibles para las colecciones de usuarios o dispositivos|Sí|Sí|
|Compatibilidad con las aplicaciones de línea de negocio desde la tienda|Sí|Sí|
|Aprovisionamiento de una aplicación de la tienda para todos los usuarios en un dispositivo<sup>[Nota 2](#bkmk_note2)</sup><!--1358310-->|Sí|Sí|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a> Nota 1: Requisito de versión para aplicaciones con licencia en línea

Para implementar aplicaciones con licencia en línea en dispositivos con Windows 10 con el cliente de Configuration Manager, deben ejecutar Windows 10, versión 1703 o posterior.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a> Nota 2: Versión mínima de Configuration Manager

A partir de la versión 1806. Para obtener más información, vea [Creación de aplicaciones Windows](../get-started/creating-windows-applications.md#bkmk_provision).  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Implementación de aplicaciones en línea mediante Microsoft Store para Empresas y Educación en dispositivos que ejecutan el cliente de Configuration Manager

Antes de implementar aplicaciones de Microsoft Store para Empresas y Educación en dispositivos que ejecutan el cliente completo de Configuration Manager, tenga en cuenta lo siguiente:

- Para una funcionalidad completa, los dispositivos deben ejecutar Windows 10, versión 1703 o posterior.  

- Registre o una los dispositivos al mismo inquilino de Azure AD donde haya registrado Microsoft Store para Empresas y Educación como una herramienta de administración.  

- Cuando la cuenta de administrador local inicia sesión en el dispositivo, no puede acceder a las aplicaciones de Microsoft Store para Empresas y Educación.  

- Los dispositivos deben tener una conexión activa de Internet con Microsoft Store para Empresas y Educación. Para obtener más información, incluida la configuración de proxy, vea [Requisitos previos](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Notas para los dispositivos que ejecutan versiones anteriores de Windows 10

En los dispositivos con el cliente de Configuration Manager y en los que se ejecuta la versión 1607 de Windows 10 o una versión anterior, se aplica la funcionalidad siguiente:  

Cuando se fuerza la instalación de la aplicación en el dispositivo mediante uno de los métodos siguientes:  

- El usuario instala la aplicación.  

- La implementación alcanza su fecha límite de instalación.

- Reevaluación posterior a la instalación para las implementaciones requeridas.  

Después, se producen los comportamientos siguientes:  

- El cliente de Configuration Manager "fuerza" la aplicación al iniciar la aplicación de Microsoft Store.  

- El usuario debe completar la instalación desde la tienda.  

- En la consola de Configuration Manager, se muestra el siguiente error en los informes de estado de implementación de aplicaciones: “La aplicación de la Tienda Windows se abrió en el equipo cliente y está esperando a que el usuario complete la instalación”.  

En el siguiente ciclo de evaluación de la aplicación:  

- Si el usuario instaló la aplicación desde la tienda, la aplicación notifica el estado **Correcto**.  

- Si el usuario no ha intentado instalar la aplicación desde la tienda:  

  - Para las implementaciones necesarias, el cliente de Configuration Manager intenta volver a iniciar la aplicación de la tienda.  

  - Configuration Manager no vuelve a exigir las implementaciones disponibles

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Dispositivos que ejecutan versiones anteriores de Windows 10

- No se pueden implementar aplicaciones de línea de negocio desde Microsoft Store para Empresas y Educación.

- Al implementar aplicaciones de pago desde la tienda, los usuarios deben iniciar sesión en la tienda y comprarlas ellos mismos.  

- Si se implementa una directiva de grupo para deshabilitar el acceso a la versión de consumo de Microsoft Store, las implementaciones desde Microsoft Store para Empresas y Educación no funcionan. Este comportamiento se produce aunque habilite Microsoft Store para Empresas y Educación.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a> Configuración de la sincronización

Al sincronizar la lista de aplicaciones de Microsoft Store para Empresas y Educación compradas por la organización, las verá en la consola de Configuration Manager.

Conecte el sitio de Configuration Manager a Azure AD y Microsoft Store para Empresas y Educación. Para obtener más información y detalles de este proceso, vea [Configuración de servicios de Azure](../../core/servers/deploy/configure/azure-services-wizard.md). Cree una conexión al servicio **Microsoft Store para Empresas**.

Asegúrese de que el punto de conexión de servicio y los dispositivos de destino pueden acceder al servicio en la nube. Para obtener más información, vea [Requisitos previos de Microsoft Store para Empresas y Educación: configuración del proxy](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a> Configuración e información complementaria

En la página **Aplicación** del Asistente para servicios de Azure, configure en primer lugar **Entorno de Azure** y **Aplicación web**. Después, lea la sección **Más información** en la parte inferior de la página. Esta información incluye las acciones adicionales siguientes en el portal de Microsoft Store para Empresas y Educación:  

- Configurar Configuration Manager como la herramienta de administración de la tienda. Para obtener más información, vea [Configurar un proveedor de MDM](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Habilitar la compatibilidad con las aplicaciones con licencia sin conexión. Para obtener más información, vea [Distribuir aplicaciones sin conexión](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Comprar al menos una aplicación. Para obtener más información, vea [Buscar y comprar aplicaciones](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

En la página **Configuraciones** del Asistente para servicios de Azure, especifique la información siguiente:  

- **Ruta de acceso al almacenamiento de contenido de aplicaciones de Microsoft Store para Empresas**: especifique una ruta de red compartida, incluida la carpeta. Por ejemplo, `\\server\share\folder`. Cuando el servidor de sitio se sincronice con la tienda, almacena en caché el contenido en esta ubicación. Al crear una aplicación en Configuration Manager, el servidor de sitio copia el contenido de la aplicación de esta caché local a la biblioteca de contenido del sitio.  

- **Idiomas seleccionados**: seleccione los idiomas que se van a sincronizar desde la tienda y se mostrarán a los usuarios en el Centro de software. Por ejemplo, si el usuario configura Windows para el alemán, en el Centro de software se muestran cadenas en alemán para la aplicación de la tienda. Este comportamiento requiere que ese idioma se sincronice y exista para la aplicación específica.

- **Idioma predeterminado**: si el idioma del usuario no está disponible, seleccione el idioma predeterminado que se va a usar.  

> [!NOTE]
> Configuration Manager no sincroniza el icono de la aplicación desde el almacén. Si necesita que se muestre un icono para esta aplicación en el Centro de software, agréguelo manualmente en las propiedades de la aplicación. Para más información, vea [Especificar manualmente la información de la aplicación](create-applications.md#bkmk_manual-app).<!-- 2837053 -->

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a> Creación e implementación de la aplicación

Después de la sincronización, cree e implemente las aplicaciones de Microsoft Store para Empresas y Educación como cualquier otra de Configuration Manager.

1. En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y, luego, seleccione el nodo **Información de licencia para las aplicaciones de la Tienda**.  

2. Elija la aplicación que quiera implementar y, luego, seleccione **Crear aplicación** en la cinta.  

El sitio crea una aplicación de Configuration Manager que contiene la aplicación de Microsoft Store para Empresas y Educación.

Después, implemente y supervise esta aplicación como haría con cualquier otra de Configuration Manager. Vea los siguientes artículos para más información:  

- [Implementar aplicaciones](deploy-applications.md)
- [Supervisar aplicaciones desde la consola](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Pasos siguientes

En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y, después, seleccione el nodo **Información de licencia para las aplicaciones de la Tienda**.

Para cada aplicación de la tienda que administre, puede ver la información siguiente:

- Nombre de la aplicación
- Plataforma de la aplicación
- Número de licencias que posee para la aplicación
- Número de licencias disponibles

Después de implementar aplicaciones en línea, las actualizaciones de esa aplicación provienen directamente de Microsoft Store. Además, Configuration Manager no comprueba la compatibilidad de versión de las aplicaciones en línea, al igual que Windows informa de la aplicación como instalada.  

Al implementar aplicaciones sin conexión en dispositivos Windows 10 con el cliente de Configuration Manager, no permita a los usuarios actualizar aplicaciones externas en implementaciones de Configuration Manager. El control de las actualizaciones de las aplicaciones sin conexión es especialmente importante en entornos de varios usuarios como clases. Una opción para deshabilitar Microsoft Store es mediante la [directiva de grupo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy).

Después de que el administrador de Microsoft Store para Empresas y Educación compre una aplicación sin conexión, no publique la aplicación para los usuarios a través de la tienda. Esta configuración garantiza que los usuarios no puedan instalar ni actualizar en línea. Los usuarios solo reciben las actualizaciones de aplicaciones sin conexión a través de Configuration Manager.

## <a name="see-also"></a>Vea también

[Solución de problemas de integración de Microsoft Store para Empresas y Educación con Configuration Manager](troubleshoot-microsoft-store-for-business-integration.md)
