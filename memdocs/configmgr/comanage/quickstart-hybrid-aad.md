---
title: Uso de Azure AD para la administración conjunta
titleSuffix: Configuration Manager
description: Con Azure AD puede aprovechar la productividad mejorada para sus usuarios y la seguridad para sus recursos, tanto en la nube como en los entornos locales.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84247482ddece88208e83fec545afc5e953a070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691293"
---
# <a name="use-azure-ad-for-co-management"></a>Uso de Azure AD para la administración conjunta

En la nube, la identidad es el nuevo plano de control. Azure Active Directory (Azure AD) le permite vincular usuarios, dispositivos y aplicaciones en entornos de nube y locales. El registro de sus dispositivos en Azure AD le permite mejorar la productividad de sus usuarios y la seguridad de sus recursos. Tener dispositivos en Azure AD es la base para la administración conjunta y el acceso condicional basado en dispositivos.

Para obtener más información sobre el acceso condicional basado en dispositivos, consulte [Instrucciones: Uso obligatorio de dispositivos administrados para el acceso a aplicaciones en la nube mediante el acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

En el siguiente vídeo, el Jefe de Programas Senior Sandeep Deo y el Jefe de Marketing de Productos Adam Harbour debaten sobre Azure AD y demuestran su funcionalidad para la administración conjunta:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD ofrece dos opciones para que los dispositivos propiedad de la empresa se adapten a las necesidades de su organización:  

- **Dispositivo unido a Azure AD**: unir sus dispositivos de Windows 10 a Azure AD sin necesidad de unirlos a su Active Directory local  

  - Es compatible con Windows 10.

  - Configúrelo sin necesidad de detallar valores específicos para los entornos locales.  

  - Al habilitar algunas opciones de configuración de Azure AD, puede permitir que los usuarios unan dispositivos a Azure AD a través de la experiencia de instalación de Windows (OOBE).  

  - Para obtener más información consulte el tema [How to: Planeación de la implementación de la unión a Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Dispositivo híbrido unido a Azure AD**: unir los dispositivos existentes unidos a dominio a Azure AD  

  - Es compatible con Windows 10, Windows 8.1 y Windows 7.

  - Configúrelo para el uso de notificaciones de AD FS o Azure AD Connect.  

  - En el caso de Windows 10, la unión tiene lugar en el contexto del equipo, por lo que los usuarios no tienen que realizar pasos adicionales.  

  - Para obtener más información, vea [Planeamiento de la implementación de la unión a Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).  

Ambas opciones ofrecen una funcionalidad similar para los usuarios. Es flexible para que pueda elegir cualquiera de ellas en función de sus necesidades. Por ejemplo, puede [acceder a los recursos locales](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) desde equipos unidos a AD de Azure aunque no estén unidos a Active Directory.

Puede unir dispositivos a Azure AD en varios entornos, sin importar su [método de autenticación](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn). Por ejemplo, autenticación federada o autenticación en la nube.

Si ya tiene una instancia local de Active Directory, configurar cualquiera de las opciones es sencillo.

## <a name="benefits"></a>Ventajas

La unión de dispositivos a Azure AD proporciona las siguientes ventajas a su organización:

### <a name="single-sign-on-to-cloud-resources"></a>Inicio de sesión único a los recursos de nube

En los dispositivos unidos a Azure AD, obtendrá una experiencia integrada de acceso a cualquier recurso local o en la nube. Una vez que inicie sesión en una máquina de Windows que esté unida a Azure AD, obtendrá un inicio de sesión único para todas las aplicaciones sin que haya más peticiones de inicio de sesión.  

### <a name="windows-hello-for-business"></a>Windows Hello para empresas

Windows Hello para empresas ofrece una autenticación sin contraseña segura a Windows 10. Al unir sus dispositivos a Azure AD, puede habilitar Windows Hello para empresas en su base de usuarios para recursos locales y en la nube. Windows Hello para empresas elimina el problema de tener que recordar contraseñas complejas o de exponerlas involuntariamente. Su proceso de inicio de sesión es sencillo y seguro.

Para obtener más información, vea [Windows Hello para empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Acceso condicional basado en dispositivos

Habilite el acceso condicional basado en el estado del dispositivo para proteger mejor los datos de su organización. El acceso condicional basado en dispositivos requiere un dispositivo administrado. Este dispositivo debe ser un dispositivo compatible o un dispositivo híbrido unido a Azure AD. En el caso de los dispositivos unidos a Azure AD, necesita Intune para marcar el dispositivo como compatible. En el caso de los dispositivos híbridos unidos a Azure AD, por el contrario, se usa el propio estado del dispositivo para evaluar el acceso condicional. La administración conjunta le brinda la ventaja adicional de evaluar el cumplimiento a través de Intune para dispositivos híbridos unidos a Azure AD. Esta característica garantiza que la configuración del dispositivo está intacta.

Para obtener más información sobre el acceso condicional basado en dispositivos, consulte [Instrucciones: Uso obligatorio de dispositivos administrados para el acceso a aplicaciones en la nube mediante el acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)  

### <a name="automatic-device-licensing"></a>Concesión de licencias automática para dispositivos

Todos los dispositivos de Windows 10 unidos a Azure AD se someten a la verificación de licencias. Estas comprobaciones le permiten actualizarlas automáticamente de Pro a Enterprise a través de la nube de Microsoft. Cuando quita la suscripción correspondiente al usuario, el dispositivo degrada automáticamente su licencia. Esta característica proporciona un único panel de control para la administración de licencias de Windows, sin complicados procesos o sistemas locales.

### <a name="self-service-functionality"></a>Funcionalidad de autoservicio

La funcionalidad de autoservicio incluye el restablecimiento de contraseñas de autoservicio y la clave de recuperación de BitLocker. Azure AD también le brinda opciones directas para restablecer su contraseña o acceder a las claves de recuperación de BitLocker. Puede usar Azure AD para restablecer su contraseña directamente desde la pantalla de bloqueo de Windows, en lugar de hacerlo desde un navegador web. Estas características reducen la fricción para los usuarios y ayudan a reducir los costos del servicio de asistencia para su organización.  

Para obtener más información, consulte [Tutorial: Habilitación del autoservicio de restablecimiento de contraseña de Azure Active Directory para que los usuarios puedan desbloquear su cuenta o restablecer contraseñas](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Enterprise State Roaming

Todos los dispositivos unidos a Azure AD pueden sincronizar su configuración en la nube. Cualquier dispositivo en el que un usuario inicie sesión sincroniza todas sus configuraciones para una experiencia más productiva.  

## <a name="value-proposition"></a>Propuesta de valor

Unir los dispositivos a Azure AD a través de cualquiera de estos métodos acelera su transformación digital. Amplía la funcionalidad proporcionada por Microsoft 365. Tendrá una mejor experiencia y mayor seguridad para los datos.

Azure AD proporciona varias opciones para facilitar la carga de trabajo, por ejemplo:

- Administrar todas las identidades de dispositivo de su organización desde un único lugar.  

- Reducir los costos del departamento de soporte técnico al habilitar el restablecimiento de contraseña de autoservicio. De este modo, los usuarios pueden restablecer su contraseña desde la pantalla de bloqueo de Windows 10 en el dispositivo en cualquier momento.  

## <a name="configure"></a>Configurar

Si ya tiene un entorno de Active Directory local y desea unir sus dispositivos unidos a un dominio a Azure AD, configure los dispositivos híbridos unidos a Azure AD. Para obtener más información, consulte [Instrucciones: Planeamiento de la implementación de la unión a Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager tiene una configuración de cliente para [registrar automáticamente nuevos dispositivos unidos a un dominio de Windows 10 con Azure AD](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Para obtener más información sobre cómo configurar estas opciones de cliente, vea [Cómo configurar el cliente](../core/clients/deploy/configure-client-settings.md).

Si desea configurar la unión a Azure AD para sus dispositivos sin unirlos también a su dominio local, revise las consideraciones para la unión a Azure AD en su entorno. Una vez que haya decidido unirse a Azure AD, tiene muchas opciones para implementarlo según las necesidades de su organización. Vea los siguientes artículos para más información:

- [Procedimiento: Planeación de la implementación de la unión a Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Explicación de las opciones de aprovisionamiento](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  
