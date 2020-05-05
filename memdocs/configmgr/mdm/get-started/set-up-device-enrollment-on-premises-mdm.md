---
title: Configuración de la inscripción para MDM local
titleSuffix: Configuration Manager
description: Conceda permiso a los usuarios para inscribir sus dispositivos para la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724689"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Configuración de la inscripción de dispositivos para MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

El último paso para configurar la administración local de dispositivos móviles (MDM) consiste en permitir que los usuarios inscriban sus dispositivos. Use Configuration Manager configuración de cliente para conceder permiso a los usuarios para inscribir dispositivos en MDM local.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> Crear un perfil de inscripción

Para enviar la configuración necesaria para permitir a los usuarios inscribir dispositivos móviles, agregue un nuevo perfil de inscripción a la configuración de cliente predeterminada. Este perfil se aplica a todos los usuarios del sitio Configuration Manager.

> [!NOTE]
> Este proceso usa la **configuración de cliente predeterminada**, que se aplicará automáticamente a todos los dispositivos y usuarios. Como alternativa, puede crear una configuración de cliente personalizada y, a continuación, implementarla en las recopilaciones de su elección. Este método alternativo requiere al menos dos configuraciones de cliente personalizadas, una para la configuración de *dispositivo* y otra para la configuración de *usuario* . Para obtener más información, vea [Cómo configurar el cliente](../../core/clients/deploy/configure-client-settings.md).

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **configuración de cliente** . Abra la **configuración de cliente predeterminada** y seleccione el grupo de **inscripción** .

1. En configuración del dispositivo, especifique el **intervalo de sondeo para dispositivos modernos (minutos)**. De forma predeterminada, este intervalo es de 60 minutos.

1. En configuración de usuario, habilite la opción para **permitir a los usuarios inscribir dispositivos modernos**.

1. En el **Perfil de inscripción de dispositivos modernos**, seleccione **establecer perfil**. En la ventana Perfil de inscripción, seleccione **crear**.

1. En la ventana Crear Perfil de inscripción, especifique la información siguiente:

    - Un **nombre** único y descriptivo para el perfil de inscripción.

    - Una **Descripción** opcional para proporcionar información adicional sobre el perfil.

    - Elija el **código de sitio de administración** que contiene el punto de administración de dispositivos. Seleccione **Aceptar** para guardar y cerrar.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Configurar opciones de cliente adicionales

Hay más opciones de configuración de cliente para configurar los dispositivos después de que se hayan inscrito. Para obtener más información general, consulte [How to Configure Client Settings](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager admite la siguiente configuración de cliente para MDM local:

- **Directiva de cliente**: esta configuración especifica la frecuencia de descarga de la Directiva de cliente en el dispositivo. También puede habilitar la configuración de la Directiva de usuario. Para obtener más información, vea [acerca de la configuración de cliente: Directiva de cliente](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Implementación de software**: establezca el intervalo para evaluar las implementaciones de software. Para obtener más información, consulte [About Client Settings-software Deployment](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > En el caso de MDM local, la configuración de implementación de software solo se puede usar como configuración de cliente predeterminada.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Detectar usuarios

Para que los usuarios reciban la configuración de cliente con el perfil de inscripción para MDM local, el sitio detecta su cuenta de usuario en Active Directory. Para asegurarse de que todos los usuarios que necesiten el perfil de inscripción lo obtengan, ejecute la detección para usuarios de Active Directory. Para obtener más información, vea [Active Directory la detección de usuarios](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Instalar el certificado raíz de confianza

Los dispositivos Unidos a un dominio obtienen el certificado raíz de confianza para la comunicación de confianza con los servidores que hospedan los roles de sistema de sitio. Active Directory servicios de Certificate Server distribuye automáticamente el certificado raíz de confianza. Los equipos y dispositivos móviles que no están Unidos a un dominio necesitan este certificado instalado a través de otros medios para permitir la inscripción.

> [!NOTE]
> Si una entidad de certificación pública emite los certificados de servidor Web, la mayoría de los dispositivos ya confían en estas CA. Si el diseño incluye el uso de una de estas entidades de certificación públicas, no es necesario realizar este paso.

Después de [exportar el certificado raíz de confianza](set-up-certificates-on-premises-mdm.md#bkmk_exportCert), debe instalarlo en los dispositivos que lo necesiten para inscribirse. Por ejemplo, los dispositivos que no están Unidos al dominio y no pueden obtenerlo automáticamente desde Active Directory. El proceso que use dependerá de los siguientes factores:

- Tipos de dispositivos y capacidades técnicas específicos
- Versión del SO
- Requisitos empresariales, de seguridad y de experiencia del usuario

La lista siguiente incluye algunos métodos de ejemplo para enviar e instalar el certificado raíz de confianza en los dispositivos:

- Recurso compartido de archivos

- Datos adjuntos de correo electrónico

- Tarjeta de memoria

- Dispositivo anclado a red

- Almacenamiento en la nube (por ejemplo, OneDrive)

- Conexión NFC (transmisión de datos en proximidad)

- Escáner de código de barras

- Paquete de aprovisionamiento de configuración rápida (OOBE)

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Instalación manual del certificado raíz de confianza en Windows

1. En el dispositivo que se va a inscribir, busque en el explorador de archivos el archivo de certificado raíz de confianza (. cer) y **ábralo** .

1. En la ventana certificado, seleccione **instalar certificado**.

1. En el Asistente para importación de certificados, seleccione **equipo local**y, a continuación, seleccione **siguiente** para continuar como administrador.

1. En la página almacén de certificados, seleccione **colocar todos los certificados en el siguiente almacén**y, a continuación, seleccione **examinar**.

1. En la ventana Seleccionar almacén de certificados, seleccione **entidades de certificación raíz de confianza**y haga clic en **Aceptar**.

1. Complete y el asistente.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Inscribir dispositivos](../deploy-use/enroll-devices-on-premises-mdm.md)
