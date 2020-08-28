---
title: Requisitos de red de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre los requisitos de red para la implementación de Windows AutoPilot.
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
ms.openlocfilehash: 1b217f7b299447b53c760cbba85b873d0626d741
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993755"
---
# <a name="windows-autopilot-networking-requirements"></a>Requisitos de red de Windows AutoPilot

**Se aplica a: Windows 10**

Windows AutoPilot depende de una variedad de servicios basados en Internet. El acceso a estos servicios debe proporcionarse para que AutoPilot funcione correctamente. En el caso más simple, la habilitación de la funcionalidad correcta se puede lograr asegurándose de las siguientes condiciones:

- Garantizar la resolución de nombres de servicios de nombres de dominio (DNS) para nombres DNS de Internet
- Permitir el acceso a todos los hosts a través del puerto 80 (HTTP), 443 (HTTPS) y 123 (UDP/NTP)

Puede ser necesaria una configuración adicional para conceder acceso a los servicios necesarios en entornos que:
- tener acceso a Internet más restrictivo.
- requiere autenticación antes de poder obtener acceso a Internet. 

> [!NOTE]
> La autenticación basada en certificados y tarjetas inteligentes no se admite durante OOBE. Para obtener más información, consulte [tarjetas inteligentes y autenticación basada en certificados](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

Para obtener detalles adicionales acerca de cada uno de estos servicios y sus requisitos específicos, revise los detalles siguientes:

<table><th>Servicio<th>Información de
<tr><td><b>Servicio de implementación de Windows AutoPilot<b><td>Una vez que se haya establecido una conexión de red, cada dispositivo de Windows 10 se pondrá en contacto con el servicio de implementación de Windows AutoPilot. Con Windows 10 versión 1903 y versiones posteriores, se usan las direcciones URL siguientes: https://ztd.dds.microsoft.com , https://cs.dds.microsoft.com . <br>

<tr><td><b>Activación de Windows<b><td>Windows AutoPilot requiere servicios de activación de Windows. Para obtener más información acerca de las direcciones URL que deben ser accesibles para los servicios de activación, consulte <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">activación o validación de Windows error con el código de error 0x8004FE33</a>.<br>

<tr><td><b>Azure Active Directory<b><td>Azure Active Directory valida las credenciales de usuario y el dispositivo también puede unirse a Azure Active Directory. Para obtener más información, consulte <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">dirección IP y servicio Web de URL 365 de Office</a>.
<tr><td><b>Intune<b><td>Una vez autenticado, Azure Active Directory desencadenará la inscripción del dispositivo en el servicio de administración de dispositivos móviles (MDM) de Intune. Consulte el siguiente vínculo para obtener más información sobre los requisitos de comunicación de red: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">requisitos de configuración de red de Intune y ancho de banda</a>.
<tr><td><b>Windows Update<b><td>Durante el proceso de OOBE y después de la configuración del sistema operativo Windows 10, el servicio de Windows Update recupera las actualizaciones necesarias. Si hay problemas para conectarse a Windows Update, consulte <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">cómo solucionar problemas de conexión relacionados con Windows Update o Microsoft Update</a>.<br>

Si Windows Update es inaccesible, el proceso de AutoPilot seguirá continuando pero las actualizaciones críticas no estarán disponibles.

<tr><td><b>Optimización de distribución<b><td>AutoPilot se pone en contacto con el servicio de <a href="/windows/deployment/update/waas-delivery-optimization">optimización de entrega</a> al descargar las aplicaciones y las actualizaciones. Este contacto establece el uso compartido de contenido punto a punto para que solo unos pocos dispositivos necesiten descargarlo desde Internet.
- Windows Updates - Microsoft Store aplicaciones y actualizaciones de aplicaciones - actualización de Office actualizaciones de - aplicaciones de Win32 de Intune<br>

Si no se puede acceder al servicio de optimización de entrega, el proceso de AutoPilot seguirá continuando con las descargas de optimización de entrega desde la nube (sin punto de conexión).

<tr><td><b>Sincronización del Protocolo de tiempo de redes (NTP)<b><td>Cuando se inicia un dispositivo Windows, se comunica con un servidor horario de red para asegurarse de que la hora del dispositivo sea correcta. Asegúrese de que el puerto UDP 123 a time.windows.com sea accesible.
<tr><td><b>Servicios de nombres de dominio (DNS)<b><td>Para resolver los nombres DNS de todos los servicios, el dispositivo se comunica con un servidor DNS, normalmente proporcionado a través de DHCP. Este servidor DNS debe ser capaz de resolver nombres de Internet.
<tr><td><b>Datos de diagnóstico<b><td>A partir de Windows 10, 1903, la recopilación de datos de diagnóstico estará habilitada de forma predeterminada. Para deshabilitar el análisis de Windows y las capacidades de diagnóstico relacionadas, consulte <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">administrar el nivel de datos de diagnóstico empresarial</a>.<br>

Si no se pueden enviar datos de diagnóstico, el proceso de AutoPilot continúa. Sin embargo, los servicios que dependen de datos de diagnóstico, como Windows Analytics, no funcionarán.
<tr><td><b>Indicador de estado de conexión de red (NCSI)<b><td>Windows debe ser capaz de indicar que el dispositivo puede acceder a Internet. Para obtener más información, consulte <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">indicador de estado de conexión de red (NCSI)</a>.

<code>www.msftconnecttest.com</code> se debe poder resolver a través de DNS y estar accesible a través de HTTP.
<tr><td><b>Notification Services de Windows (WNS)<b><td>Este servicio se usa para permitir que Windows reciba notificaciones de aplicaciones y servicios. Para obtener más información, vea <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a>.<br>

Si los servicios de WNS no están disponibles, el proceso de AutoPilot seguirá continuando sin notificaciones.
<tr><td><b>Microsoft Store, Microsoft Store para empresas<b><td>Las aplicaciones del Microsoft Store pueden insertarse en el dispositivo, desencadenadas mediante Intune (MDM).También es posible que se necesiten actualizaciones de aplicaciones y otras aplicaciones cuando el usuario inicia sesión por primera vez. Para obtener más información, consulte <a href="/microsoft-store/prerequisites-microsoft-store-for-business">requisitos previos para Microsoft Store para empresas y educación</a> (también incluye Azure ad y Windows Notification Services).<br>

Si el Microsoft Store no es accesible, el proceso de AutoPilot seguirá continuando sin Microsoft Store aplicaciones.

<tr><td><b>Microsoft 365<b><td>Como parte de la configuración del dispositivo de Intune, es posible que sea necesaria la instalación de Microsoft 365 aplicaciones para la empresa. Para obtener más información, consulte <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">direcciones URL e intervalos de direcciones IP de Office 365</a>. En este artículo se incluyen todos los servicios de Office, nombres DNS y direcciones IP. También incluye Azure AD y otros servicios que pueden superponerse con los servicios mencionados anteriormente.
<tr><td><b>Listas de revocación de certificados (CRL)<b><td>Algunos de estos servicios también necesitarán comprobar las listas de revocación de certificados (CRL) para los certificados que se usan en los servicios.Para obtener una lista completa, consulte <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">direcciones URL e intervalos de direcciones IP de office 365</a> y <a href="https://aka.ms/o365chains">cadenas de certificados de Office 365</a>.
<tr><td><b>Unión a Azure AD híbrido<b><td>El dispositivo puede ser híbrido Azure AD Unido. El equipo debe estar en la red corporativa para que la Unión Azure AD híbrida funcione. Ver los detalles en <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">el modo controlado por el usuario de Windows AutoPilot</a>
<tr><td><b>Modo Autoimplementación AutoPilot y la guante blanca de autopiloto<b><td>Los dispositivos TPM de firmware, que solo son proporcionados por Intel, AMD o Qualcomm, no incluyen todos los certificados necesarios en el momento del arranque y deben ser capaces de recuperarlos del fabricante al usarse por primera vez. Los dispositivos con chips de TPM discretos (incluidos los dispositivos de cualquier otro fabricante) incluyen estos certificados preinstalados. Para obtener más información, vea <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">recomendaciones del TPM</a>. Para cada proveedor de TPM de firmware, asegúrese de que se pueda acceder a estas direcciones URL para que los certificados se puedan solicitar correctamente:

 <br>Procesador <code>https://ekop.intel.com/ekcertservice</code>
 <br>Qualcomm <code>https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1</code>
 <br>PowerNow <code>https://ftpm.amd.com/pki/aia</code>

</table>

**Pasos siguientes**

[Requisitos de licencia de Windows AutoPilot](licensing-requirements.md)