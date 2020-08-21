---
title: Introducción a los perfiles de certificado
titleSuffix: Configuration Manager
description: Aprenda cómo funcionan los perfiles de certificado de Configuration Manager con Servicios de certificados de Active Directory.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3598c95d1431915431d96b16c10c7c913741fe3d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700000"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Introducción a los perfiles de certificado en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los perfiles de certificado funcionan con Servicios de certificados de Active Directory y el Servicio de inscripción de dispositivos de red (NDES). Cree e implemente certificados de autenticación para dispositivos administrados para que los usuarios puedan acceder fácilmente a los recursos organizativos. Por ejemplo, puede crear e implementar perfiles de certificado para proporcionar los certificados necesarios para que los usuarios se conecten a redes VPN e inalámbricas.

Los perfiles de certificado pueden configurar automáticamente dispositivos de usuario para el acceso a recursos de la organización, como redes Wi-Fi y servidores VPN. Los usuarios pueden acceder a estos recursos sin tener que instalar manualmente los certificados o usar un proceso fuera de banda. Los perfiles de certificado ayudan a proteger los recursos, porque permiten usar una configuración más segura compatible con la infraestructura de clave pública (PKI). Por ejemplo, puede requerir la autenticación de servidor en todas las conexiones VPN y Wi-Fi, ya que ha implementado los certificados necesarios en los dispositivos administrados.

Los perfiles de certificado proporcionan las siguientes capacidades de administración:  

- Inscripción y renovación de certificados de una entidad de certificación (CA) para dispositivos que ejecutan distintos tipos y versiones de sistema operativo. Estos certificados se pueden usar en conexiones Wi-Fi y VPN.  

- Implementación de certificados de entidades de certificación raíz de confianza y de certificados de entidades de certificación intermedias. Estos certificados configuran una cadena de confianza en dispositivos para conexiones VPN y Wi-Fi cuando se requiere autenticación de servidor.  

- Supervisar los certificados instalados y notificar acerca de ellos.  

**Ejemplo 1**: todos los empleados necesitan conectarse a puntos de conexión Wi-Fi en varias ubicaciones corporativas. Para permitir una conexión de usuario sencilla, implemente primero los certificados necesarios para conectarse a Wi-Fi. Después, implemente los perfiles de Wi-Fi que hacen referencia al certificado.  

**Ejemplo 2:** : tiene una PKI. y quiere cambiar a un método más flexible y seguro de implementar certificados. Los usuarios tienen que acceder a los recursos de la organización desde sus dispositivos personales sin poner en peligro la seguridad. Configure perfiles de certificados con las opciones y los protocolos admitidos en la plataforma específica del dispositivo. Los dispositivos pueden solicitar automáticamente estos certificados desde un servidor de inscripción accesible desde Internet. Luego configure los perfiles de VPN para que usen estos certificados de modo que el dispositivo pueda acceder a los recursos organizativos.  

## <a name="types"></a>Tipos

Hay tres tipos de perfiles de certificado:  

- **Certificado de CA de confianza**: implemente un certificado de entidad de certificación raíz de confianza o un certificado de entidad de certificación intermedia. Estos certificados forman una cadena de confianza cuando el dispositivo debe autenticarse en un servidor.  

- **Protocolo de inscripción de certificados simple (SCEP)** : solicite un certificado para un dispositivo o usuario por medio del protocolo SCEP. Este tipo requiere el rol Servicio de inscripción de dispositivos de red (NDES) en un servidor que ejecuta Windows Server 2012 R2 o posterior.

    Para crear un perfil de certificado de **Protocolo de inscripción de certificados simple (SCEP)** , cree primero un perfil de **Certificado de CA de confianza**.

- **Intercambio de información personal (.pfx)** : solicite un certificado .pfx (también conocido como PKCS #12) para un dispositivo o usuario.<!--1321368--> Existen dos métodos para crear perfiles de certificados PFX:

  - [Importar credenciales](../../mdm/deploy-use/import-pfx-certificate-profiles.md) desde certificados existentes
  - [Definir una entidad de certificación](../../mdm/deploy-use/create-pfx-certificate-profiles.md) para procesar solicitudes

  > [!Note]  
  > Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  Puede usar Microsoft o Entrust como entidades de certificación de certificados **Intercambio de información personal (.pfx)** .

## <a name="requirements"></a>Requisitos

Para implementar perfiles de certificado que usen SCEP, instale el punto de registro de certificados en un servidor de sistema de sitio. Instale también un módulo de directivas para NDES, el módulo de directivas de Configuration Manager, en un servidor que ejecute Windows Server 2012 R2 o posterior. Este servidor requiere el rol de Servicios de certificados de Active Directory. También requiere un NDES de trabajo que sea accesible a los dispositivos que requieran los certificados. Si los dispositivos necesitan inscribirse para los certificados en Internet, el servidor de NDES debe ser accesible desde Internet. Por ejemplo, para habilitar de forma segura el tráfico hacia el servidor NDES desde Internet, puede usar [Azure Application Proxy](/azure/active-directory/manage-apps/application-proxy).

Los certificados PFX también requieren un punto de registro de certificados. Especifique también la entidad de certificación (CA) del certificado y las credenciales de acceso pertinentes. Puede especificar Microsoft o Entrust como entidades de certificación.  

Para obtener más información sobre la compatibilidad de NDES con un módulo de directivas para que Configuration Manager pueda implementar certificados, vea [Uso de un módulo de directivas con el Servicio de inscripción de dispositivos de red](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\)).

Según cuáles sean los requisitos, Configuration Manager admite la implementación de certificados en distintos almacenes de certificados de varios tipos de dispositivo y sistemas operativos. Se admiten los dispositivos y los sistemas operativos siguientes:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Use MDM local de Configuration Manager para administrar Windows Phone 8.1 y Windows 10 Mobile. Para obtener más información, vea [MDM local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Un escenario típico para Configuration Manager es instalar certificados de una entidad certificadora (CA) raíz de confianza para autenticar servidores Wi-Fi y VPN. Las conexiones típicas usan los siguientes protocolos:

- Protocolos de autenticación: EAP-TLS, EAP-TTLS y PEAP
- Protocolos de túnel VPN: IKEv2, L2TP/IPsec y Cisco IPsec

Debe haber instalado un certificado de entidad de certificación raíz empresarial en el dispositivo para que este pueda solicitar certificados por medio del perfil de certificado de SCEP.  

Puede especificar opciones de configuración en un perfil de certificado de SCEP para solicitar los certificados personalizados para distintos entornos o requisitos de conectividad. El **Asistente para crear perfil de certificado** tiene dos páginas para parámetros de inscripción. La primera, **Inscripción de SCEP**, contiene la configuración de la solicitud de inscripción y la ubicación de instalación del certificado. La segunda, **Propiedades de certificado**, describe el certificado solicitado.  

## <a name="deploy"></a>Implementar

Cuando se implementa un perfil de certificado SCEP, el cliente de Configuration Manager procesa la directiva. Posteriormente, solicita una contraseña de desafío de SCEP desde el punto de administración. El dispositivo crea un par de claves pública y privada y genera una solicitud de firma de certificado (CSR). Envía esta solicitud al servidor NDES. El servidor NDES reenvía la solicitud al sistema del sitio de punto de registro de certificados a través del módulo de directivas de NDES. El punto de registro de certificados valida la solicitud, comprueba la contraseña de desafío de SCEP y comprueba que la solicitud no haya sufrido manipulaciones. Después, aprueba o deniega la solicitud. Si se aprueba, el servidor NDES envía la solicitud de firma a la entidad de certificación (CA) conectada para firmar. La entidad de certificación firma la solicitud y, posteriormente, devuelve el certificado al dispositivo peticionario.

Implemente perfiles de certificado en recopilaciones de dispositivos o usuarios. Puede especificar el almacén de destino de cada certificado. Las reglas de aplicación determinan si el dispositivo puede instalar el certificado.

Cuando se implementa un perfil de certificado en una colección de usuarios, la [afinidad de usuario](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) determina el dispositivo del usuario que instala los certificados. Cuando se implementa un perfil de certificado con un certificado de usuario en una colección de usuarios, de forma predeterminada, cada uno de los dispositivos principales de los usuarios instala los certificados. Para instalar el certificado en cualquiera de los dispositivos de los usuarios, cambie este comportamiento en la página **Inscripción de SCEP** del **Asistente para crear perfil de certificado**. Si los dispositivos están en un grupo de trabajo, Configuration Manager no implementa certificados de usuario.  

## <a name="monitor"></a>Supervisión

Puede supervisar las implementaciones de perfil de certificado viendo los informes o resultados de cumplimiento. Para más información, vea [Cómo supervisar perfiles de certificado](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Revocación automática

Configuration Manager revoca automáticamente los certificados de usuario y de equipo implementados mediante perfiles de certificado en las circunstancias siguientes:  

- El dispositivo se retira de la administración de Configuration Manager.  

- El dispositivo se bloquea de la jerarquía de Configuration Manager.  

Para revocar los certificados, el servidor de sitio envía un comando de revocación a la entidad de certificación emisora. El motivo de la revocación es **Cese de operación**.

> [!NOTE]
> Para revocar correctamente un certificado, la cuenta de equipo para el sitio de nivel superior de la jerarquía necesita el permiso para **emitir y administrar certificados** en la CA.
>
> Para mejorar la seguridad, también puede restringir los administradores de entidad certificadora en la CA. Posteriormente, conceda solo los permisos de esta cuenta en la plantilla de certificado específica que use para los perfiles de SCEP en el sitio.

## <a name="next-steps"></a>Pasos siguientes

- [Crear perfiles de certificado](create-certificate-profiles.md)

- [Configuración de la infraestructura de certificados](certificate-infrastructure.md)