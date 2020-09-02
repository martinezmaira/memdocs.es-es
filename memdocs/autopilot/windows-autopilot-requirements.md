---
title: Requisitos de Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre el software, las redes, las licencias y los requisitos de configuración para la implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 37d249c75f18d52f7fa17a0e271f45b17465da1a
ms.sourcegitcommit: 9d5c7a5e6ec430dc02d6d345028f6b29f6579b20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385337"
---
# <a name="windows-autopilot-requirements"></a>Requisitos de Windows Autopilot

**Se aplica a: Windows 10**

Windows AutoPilot depende de las capacidades específicas disponibles en los servicios de Windows 10, Azure Active Directory y MDM como Microsoft Intune.  Para poder usar Windows AutoPilot y aprovechar estas capacidades, se deben cumplir algunos requisitos.

**Nota**: para obtener una lista de los OEM que admiten actualmente Windows AutoPilot, consulte la sección de fabricantes de dispositivos participantes en [Windows AutoPilot](https://aka.ms/windowsAutopilot).

## <a name="software-requirements"></a>Requisitos de software

- Se requiere una [versión compatible](/windows/release-information/) del canal semianual de Windows 10. También se admite el canal de mantenimiento a largo plazo (LTSC) de Windows 10 2019 Enterprise.
- Se admiten las siguientes ediciones:
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education
  - Windows 10 Enterprise 2019 LTSC

>[!NOTE]
>Los procedimientos para implementar Windows AutoPilot pueden hacer referencia a productos y versiones específicos. La inclusión de estos productos en este contenido no implica una extensión de la compatibilidad con una versión que supere su ciclo de vida de soporte técnico. Windows AutoPilot no admite productos que superan su ciclo de vida de soporte técnico. Para más información, consulte [Directiva de ciclo de vida de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).

## <a name="networking-requirements"></a>Requisitos de red

Windows AutoPilot depende de una variedad de servicios basados en Internet. El acceso a estos servicios debe proporcionarse para que AutoPilot funcione correctamente. En el caso más simple, la habilitación de la funcionalidad correcta se puede lograr asegurándose de lo siguiente:

- Garantizar la resolución de nombres DNS para los nombres DNS de Internet
- Permitir el acceso a todos los hosts a través del puerto 80 (HTTP), 443 (HTTPS) y 123 (UDP/NTP)

En entornos que tengan acceso a Internet más restrictivo, o para los que requieran autenticación antes de que se pueda obtener acceso a Internet, puede ser necesaria una configuración adicional para permitir el acceso a los servicios necesarios. 

> [!NOTE]
> La autenticación basada en certificados y tarjetas inteligentes no se admite durante OOBE. Para obtener más información, consulte [tarjetas inteligentes y autenticación basada en certificados](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

Para obtener detalles adicionales acerca de cada uno de estos servicios y sus requisitos específicos, revise los detalles siguientes:

<table><th>Servicio<th>Information
<tr><td><b>Servicio de implementación de Windows AutoPilot<b><td>Una vez que se haya establecido una conexión de red, cada dispositivo de Windows 10 se pondrá en contacto con el servicio de implementación de Windows AutoPilot.  Con Windows 10 versión 1903 y versiones posteriores, se usan las direcciones URL siguientes: https://ztd.dds.microsoft.com , https://cs.dds.microsoft.com . <br>

<tr><td><b>Activación de Windows<b><td>Windows AutoPilot también requiere servicios de activación de Windows. Consulte <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">activación o validación de Windows error con el código de error 0x8004FE33</a> para obtener más información sobre las direcciones URL que deben ser accesibles para los servicios de activación.<br>

<tr><td><b>Azure Active Directory<b><td>Azure Active Directory valida las credenciales de usuario y el dispositivo también puede unirse a Azure Active Directory. Para obtener más información <a href="/office365/enterprise/office-365-ip-web-service">, consulte dirección IP y servicio Web de URL 365 de Office</a> .
<tr><td><b>Intune<b><td>Una vez autenticado, Azure Active Directory desencadenará la inscripción del dispositivo en el servicio MDM de Intune. Consulte el siguiente vínculo para obtener más información sobre los requisitos de comunicación de red: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">requisitos de configuración de red de Intune y ancho de banda</a>.
<tr><td><b>Windows Update<b><td>Durante el proceso de OOBE, así como después de configurar completamente el sistema operativo Windows 10, se aprovecha el servicio de Windows Update para recuperar las actualizaciones necesarias. Si hay problemas para conectarse a Windows Update, consulte <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">cómo solucionar problemas de conexión relacionados con Windows Update o Microsoft Update</a>.<br>

Si no se puede obtener acceso a Windows Update, el proceso de AutoPilot seguirá continuando pero las actualizaciones críticas no estarán disponibles.

<tr><td><b>Optimización de distribución<b><td>Al descargar actualizaciones de Windows, Microsoft Store aplicaciones y actualizaciones de aplicaciones, actualizaciones de Office y aplicaciones de Win32 de Intune, se Contacta con el servicio de <a href="/windows/deployment/update/waas-delivery-optimization">optimización de entrega</a> para permitir el uso compartido de contenido de punto a punto para que solo unos pocos dispositivos necesiten descargarlo desde Internet.<br>

Si no se puede acceder al servicio de optimización de entrega, el proceso de AutoPilot seguirá continuando con las descargas de optimización de entrega desde la nube (sin punto de conexión).

<tr><td><b>Sincronización del Protocolo de tiempo de redes (NTP)<b><td>Cuando se inicia un dispositivo Windows, se comunica con un servidor horario de red para asegurarse de que la hora del dispositivo sea precisa. Asegúrese de que el puerto UDP 123 a time.windows.com sea accesible.
<tr><td><b>Servicios de nombres de dominio (DNS)<b><td>Para resolver los nombres DNS de todos los servicios, el dispositivo se comunica con un servidor DNS, normalmente proporcionado a través de DHCP.Este servidor DNS debe ser capaz de resolver nombres de Internet.
<tr><td><b>Datos de diagnóstico<b><td>A partir de Windows 10, 1903, la recopilación de datos de diagnóstico estará habilitada de forma predeterminada. Para deshabilitar el análisis de Windows y las capacidades de diagnóstico relacionadas, consulte <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">administrar el nivel de datos de diagnóstico empresarial</a>.<br>

Si no se pueden enviar datos de diagnóstico, el proceso de AutoPilot seguirá continuando, pero los servicios que dependen de datos de diagnóstico, como Windows Analytics, no funcionarán.
<tr><td><b>Indicador de estado de conexión de red (NCSI)<b><td>Windows debe ser capaz de indicar que el dispositivo puede acceder a Internet. Para obtener más información, consulte <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">indicador de estado de conexión de red (NCSI)</a>.

<code>www.msftconnecttest.com</code> se debe poder resolver a través de DNS y estar accesible a través de HTTP.
<tr><td><b>Notification Services de Windows (WNS)<b><td>Este servicio se usa para permitir que Windows reciba notificaciones de aplicaciones y servicios. Consulte <a href="/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a> para obtener más información.<br>

Si los servicios de WNS no están disponibles, el proceso de AutoPilot seguirá continuando sin notificaciones.
<tr><td><b>Microsoft Store, Microsoft Store para empresas<b><td>Las aplicaciones del Microsoft Store pueden insertarse en el dispositivo, desencadenadas mediante Intune (MDM).También es posible que se necesiten actualizaciones de aplicaciones y otras aplicaciones cuando el usuario inicia sesión por primera vez. Para obtener más información, consulte <a href="/microsoft-store/prerequisites-microsoft-store-for-business">requisitos previos para Microsoft Store para empresas y educación</a> (también incluye Azure ad y Windows Notification Services).<br>

Si el Microsoft Store no es accesible, el proceso de AutoPilot seguirá continuando sin Microsoft Store aplicaciones.

<tr><td><b>Microsoft 365<b><td>Como parte de la configuración del dispositivo de Intune, es posible que sea necesaria la instalación de Microsoft 365 aplicaciones para la empresa. Para obtener más información, consulte <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">direcciones URL e intervalos de direcciones IP de office 365</a> (incluye todos los servicios de Office, nombres DNS, direcciones IP; incluye Azure ad y otros servicios que pueden superponerse con los mencionados anteriormente).
<tr><td><b>Listas de revocación de certificados (CRL)<b><td>Algunos de estos servicios también necesitarán comprobar las listas de revocación de certificados (CRL) para los certificados que se usan en los servicios.Una lista completa de estos se documenta en <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">office 365 URL e intervalos de direcciones IP</a> y <a href="https://aka.ms/o365chains">cadenas de certificados de Office 365</a>.
<tr><td><b>Unión híbrida de AAD<b><td>El dispositivo puede estar unido a una AAD híbrida. El equipo debe estar en la red corporativa para que la Unión de AAD híbrida funcione. Ver los detalles en <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">el modo controlado por el usuario de Windows AutoPilot</a>
<tr><td><b>Modo Autoimplementación AutoPilot y la guante blanca de autopiloto<b><td>Los dispositivos TPM de firmware, que solo son proporcionados por Intel, AMD o Qualcomm, no incluyen todos los certificados necesarios en el momento del arranque y deben ser capaces de recuperarlos del fabricante al usarse por primera vez. Los dispositivos con chips de TPM discretos (incluidos los dispositivos de cualquier otro fabricante) incluyen estos certificados preinstalados. Consulte las <a href="/windows/security/information-protection/tpm/tpm-recommendations">recomendaciones de TPM</a> para obtener más detalles. Asegúrese de que se puede acceder a estas direcciones URL para cada proveedor de TPM de firmware para que los certificados se puedan solicitar correctamente: 

  <br>Intel- https://www.intel.com/  <br>Qualcomm- https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1  <br>PowerNow https://ftpm.amd.com/pki/aia

</table>

## <a name="licensing-requirements"></a>Requisitos de concesión de licencia

Windows AutoPilot depende de las capacidades específicas disponibles en Windows 10 y Azure Active Directory. También requiere un servicio MDM como Microsoft Intune. Estas funcionalidades pueden obtenerse a través de varias ediciones y programas de suscripción:

Para proporcionar los Azure Active Directory necesarios (características de inscripción automática de MDM y de personalización de marca de empresa) y la funcionalidad de MDM, se requiere uno de los siguientes:
- [Suscripción a Microsoft 365 Empresa Premium](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 suscripción F1 o F3](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 la suscripción Academic a1, a3 o A5](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise suscripción a E3 o E5](https://www.microsoft.com/microsoft-365/enterprise), que incluye todas las características de Windows 10, Office 365 y em + S (Azure ad e Intune).
- [Enterprise Mobility + Security suscripción a E3 o E5](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), que incluye todas las características necesarias de Azure ad e Intune.
- [Intune for Education suscripción](/intune-education/what-is-intune-for-education), que incluye todas las características necesarias de Azure ad e Intune.
- [Azure Active Directory Premium P1 o P2](https://azure.microsoft.com/services/active-directory/) y [Microsoft Intune suscripción](https://www.microsoft.com/cloud-platform/microsoft-intune) (o un servicio MDM alternativo).

> [!NOTE]
> Incluso cuando se usa Microsoft 365 suscripciones, todavía es necesario [asignar licencias de Intune a los usuarios](/intune/fundamentals/licenses-assign).

Además, también se recomiendan los siguientes elementos (pero no son obligatorios):
- [Microsoft 365 aplicaciones para la empresa](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), que se pueden implementar fácilmente a través de Intune (u otros servicios de MDM).
- [Activación de suscripciones de Windows](/windows/deployment/windows-10-enterprise-subscription-activation), para subir automáticamente los dispositivos de Windows 10 Pro a Windows 10 Enterprise.

## <a name="configuration-requirements"></a>Requisitos de configuración

Antes de poder usar Windows AutoPilot, es necesario realizar algunas tareas de configuración para admitir los escenarios comunes de la prueba piloto.  

- Configure Azure Active Directory la inscripción automática.  Para obtener Microsoft Intune, consulte [habilitación de la inscripción automática de Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment) para obtener más información.  Si usa otro servicio MDM, póngase en contacto con el proveedor para obtener las direcciones URL específicas o la configuración necesaria para esos servicios.
- Configure Azure Active Directory la personalización de marca personalizada.  Para mostrar una página de inicio de sesión específica de la organización durante el proceso de AutoPilot, Azure Active Directory se debe configurar con las imágenes y el texto que se deben mostrar.  Consulte [Inicio rápido: agregar personalización de marca de empresa a la página de inicio de sesión en Azure ad](/azure/active-directory/fundamentals/customize-branding) para obtener más detalles.  Tenga en cuenta que el "logotipo cuadrado" y el "texto de la página de inicio de sesión" son los elementos clave de AutoPilot, así como el nombre del inquilino de Azure Active Directory (se configura por separado en las propiedades del inquilino Azure AD).
- Habilite la activación de la [suscripción de Windows](/windows/deployment/windows-10-enterprise-subscription-activation) si lo desea, para pasar automáticamente de Windows 10 Pro a Windows 10 Enterprise.

Los escenarios específicos tendrán requisitos adicionales.  Por lo general, hay dos tareas específicas:

- Registro de dispositivos.  Los dispositivos deben agregarse a Windows AutoPilot para admitir la mayoría de los escenarios de Windows AutoPilot.  Consulte [Agregar dispositivos a Windows AutoPilot](add-devices.md) para obtener más detalles.
- Configuración del perfil.  Una vez que se han agregado dispositivos a Windows AutoPilot, es necesario aplicar un perfil de configuración a cada dispositivo.  Consulte [configuración de perfiles de AutoPilot](profiles.md) para más información.  Tenga en cuenta que Microsoft Intune puede automatizar esta asignación de perfil; para obtener más información, consulte [crear un grupo de dispositivos AutoPilot](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) y [asignar un perfil de AutoPilot Deployment a un grupo de dispositivos](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group) .

Consulte [escenarios de Windows AutoPilot](windows-Autopilot-scenarios.md) para obtener más detalles.

Para ver un tutorial sobre algunos de estos pasos relacionados, consulte este vídeo:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


No hay ningún requisito de hardware adicional para usar Windows 10 AutoPilot, más allá de los [requisitos para ejecutar Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

## <a name="related-topics"></a>Temas relacionados

[Información general de Windows AutoPilot](windows-Autopilot.md)