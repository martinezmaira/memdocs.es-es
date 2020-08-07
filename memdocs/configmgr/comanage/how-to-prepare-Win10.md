---
title: Administración conjunta de dispositivos basados en Internet
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo preparar los dispositivos Windows 10 basados en Internet para la administración conjunta.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/06/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 076a4b6d1bf5773287d4a0b32109023039a3b399
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546423"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Preparación de dispositivos basados en Internet para la administración conjunta

Este artículo se centra en la segunda ruta a la administración conjunta, para los dispositivos nuevos basados en Internet. Este escenario se da cuando tiene dispositivos Windows 10 nuevos que se unen a Azure AD y se inscriben automáticamente en Intune. Puede instalar el cliente de Configuration Manager para alcanzar un estado de administración conjunta.  

## <a name="windows-autopilot"></a>Windows Autopilot

En los dispositivos Windows 10 nuevos, puede usar el servicio Autopilot para definir la configuración rápida (OOBE). Este proceso incluye unir el dispositivo a Azure AD e inscribir el dispositivo en Intune.  

Para más información, consulte [Resumen de Windows Autopilot](../../autopilot/windows-autopilot.md).

Para configurar los dispositivos para que se inscriban automáticamente en Intune al unirse a Azure AD, consulte  [Configuración de la inscripción de dispositivos Windows](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Recopilación de información desde Configuration Manager

Use Configuration Manager para recopilar y entregar la información de dispositivo que requiere Intune. Esta información incluye el número de serie del dispositivo, el identificador de producto de Windows y un identificador de hardware. Se usa para registrar el dispositivo en Intune para admitir Windows AutoPilot.

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda el nodo **Generación de informes**, expanda **Informes** y seleccione el nodo **Hardware - General**.  

2. Ejecute el informe, **Información de dispositivo Windows Autopilot** y observe los resultados.  

3. En el visor de informes, seleccione el icono **Exportar** y elija la opción **CSV (delimitado por comas)** .  

4. Después de guardar el archivo, cargue los datos en Intune.  

Para más información, consulte [Agregar dispositivos en Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Autopilot para dispositivos existentes
<!--1358333-->

[Windows Autopilot para los dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponible en Windows 10, versión 1809 o posterior. Esta característica permite volver a crear una imagen y aprovisionar un dispositivo de Windows 7 para el [modo controlado por el usuario de Windows Autopilot](../../autopilot/user-driven.md) mediante una única secuencia de tareas nativa de Configuration Manager.

Para más información, consulte el artículo sobre [Windows Autopilot para la secuencia de tareas de dispositivos existentes](../../autopilot/existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Instalación del cliente de Configuration Manager

Para los dispositivos basados en Internet en la segunda ruta, debe crear una aplicación en Intune. Implemente una aplicación en dispositivos Windows 10 que todavía no son clientes de Configuration Manager.

> [!NOTE]
> Antes de asignar esta aplicación a los dispositivos de Intune, asegúrese de que los dispositivos confían en el certificado de autenticación del servidor de CMG. Para obtener más información, vea [Certificado raíz de confianza de CMG para clientes](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Si hay un dispositivo que no confía en el certificado de autenticación del servidor de CMG, verá el error WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA en el registro ccmsetup.log del cliente.

### <a name="get-the-command-line-from-configuration-manager"></a>Obtención de la línea de comandos desde Configuration Manager

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  

2. Seleccione el objeto de administración conjunta y, después, elija **Propiedades** en la cinta.  

3. En la pestaña **Habilitación**, copie la línea de comandos. Péguela en el Bloc de notas para guardarla para el proceso siguiente.  

La línea de comandos siguiente es un ejemplo: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Decida qué propiedades de línea de comandos necesita para su entorno:  

- Las siguientes propiedades de línea de comandos son necesarias en todos los escenarios:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- Las propiedades siguientes son necesarias al usar Azure AD para la autenticación de cliente en lugar de certificados de autenticación de cliente basada en PKI:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Si el cliente vuelve a la intranet, use la propiedad siguiente:
  - SMSMP  

- Si usa su propio certificado de PKI y su CRL no está publicada en Internet, será necesario el parámetro siguiente:  
  - /noCRLCheck  

    Para obtener más información, consulte el artículo sobre el [planeamiento de CRL](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- A partir de la versión 2002, use la siguiente propiedad para arrancar una secuencia de tareas inmediatamente después del registro del cliente:
  - PROVISIONTS

    Para obtener más información, consulte [Acerca de los parámetros y propiedades de instalación de cliente: PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

El sitio publica información adicional de Azure AD para Cloud Management Gateway (CMG). Un cliente unido a Azure AD obtiene esta información de la instancia de CMG durante el proceso de ccmsetup, mediante el mismo inquilino al que está unido. Este comportamiento simplifica más la inscripción de dispositivos en la administración conjunta de un entorno con más de un inquilino de Azure AD. Las dos únicas propiedades de ccmsetup necesarias son **CCMHOSTNAME** y **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Si ya implementa el cliente de Configuration Manager desde Intune, actualice la aplicación de Intune con una línea de comandos nueva y un MSI nuevo. <!-- SCCMDocs-pr issue 3084 -->

En el ejemplo siguiente se incluyen todas estas propiedades:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Para obtener más información, vea [Acerca de las propiedades de instalación de clientes](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Creación de la aplicación en Intune

1. Vaya al [Centro de administración de Microsoft Endpoint Manager](https://endpoint.microsoft.com) y expanda el panel de navegación izquierdo.  

2. Seleccione **Aplicaciones** > **Todas las aplicaciones** > **Agregar**.  

3. En **Otros**, seleccione **Aplicación de línea de negocio**.  

4. Cargue el archivo de paquete de aplicación **ccmsetup.msi**. Busque este archivo en la carpeta siguiente en el servidor del sitio de Configuration Manager: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Cuando actualice el sitio, asegúrese de actualizar también esta aplicación en Intune.  

5. Una vez que se actualiza la aplicación, configure la información de la aplicación con la línea de comandos que copió desde Configuration Manager.  

> [!IMPORTANT]
> Si personaliza esta línea de comandos, asegúrese de que no tenga más de 1024 caracteres. Cuando la línea de comandos tiene más 1024 caracteres, se produce un error en la instalación del cliente.
