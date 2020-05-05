---
title: Cómo inscribir dispositivos en masa
titleSuffix: Configuration Manager
description: Inscripción masiva de dispositivos de forma automática con la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724619"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Cómo inscribir dispositivos en masa con MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La inscripción masiva en Configuration Manager la administración de dispositivos móviles (MDM) local es un método automatizado para inscribir dispositivos. El otro método es la inscripción de usuario, que requiere que los usuarios escriban sus credenciales para inscribir el dispositivo. La inscripción masiva usa un paquete de inscripción para autenticar el dispositivo durante la inscripción. El paquete es un archivo. ppkg, que también puede contener perfiles de certificados y Wi-Fi para admitir la inscripción.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Crear un perfil de certificado

Incluya un perfil de certificado para instalar automáticamente un certificado raíz de confianza en el dispositivo. Este certificado raíz es necesario para la comunicación de confianza entre los dispositivos y los roles de sistema de sitio necesarios para la MDM local.

Al preparar el sitio para MDM local, exporte el certificado raíz de confianza. Use este certificado en el perfil de certificado del paquete de inscripción. Para obtener más información sobre cómo obtener el certificado raíz de confianza, vea [exportar el certificado raíz de confianza](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Use el certificado exportado para crear un perfil de certificado. Para obtener más información, vea [Cómo crear perfiles de certificado](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Crear un perfil de Wi-Fi

Otro componente del paquete de inscripción masiva es un perfil de Wi-Fi. Este perfil puede asegurarse de que el dispositivo tiene la conectividad de red para admitir la inscripción.

Para obtener más información sobre cómo crear un perfil de Wi-Fi en Configuration Manager, consulte [Cómo crear perfiles de Wi-Fi](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Limitaciones del perfil de Wi-Fi

Cuando cree un perfil de Wi-Fi para la inscripción masiva de MDM local, revise las siguientes limitaciones.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Configuraciones de seguridad de Wi-Fi para MDM local

La rama actual de Configuration Manager solo admite las siguientes configuraciones de seguridad de Wi-Fi para MDM local:

- Tipos de seguridad: **WPA2 Enterprise** o **WPA2 Personal**

- Tipos de cifrado: **AES** o **TKIP**

- Tipos de EAP: **Tarjeta inteligente u otro certificado** o **PEAP**

#### <a name="proxy-server"></a>Servidor proxy

Aunque Configuration Manager tiene un valor de configuración para la información del servidor proxy en el perfil de Wi-Fi, no configura el proxy cuando se inscribe el dispositivo. Si necesita configurar un servidor proxy en dispositivos inscritos de forma masiva:

- Implemente la configuración mediante elementos de configuración una vez que se inscriban los dispositivos.

- Cree un segundo paquete mediante el diseñador de imágenes y configuraciones de Windows (ICD) y, a continuación, impleméntelo junto con el paquete de inscripción masiva.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Crear un perfil de inscripción

El perfil de inscripción permite especificar la configuración necesaria para la inscripción de dispositivos. Esta configuración incluye un [Perfil de certificado](#bkmk_createCert) y un [Perfil de Wi-Fi](#CreateWifi).

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** , expanda **todos los dispositivos propiedad de la empresa**, expanda **Windows**y seleccione el nodo **perfiles de inscripción** .

1. En la cinta de opciones, seleccione **crear Perfil de inscripción**.

1. En la página **General** del Asistente para crear Perfil de inscripción, especifique la información siguiente:

    - **Nombre**: un nombre único para identificar el perfil.

    - **Descripción**: un campo opcional para describir más detalladamente el perfil

    - **Entidad de administración**: seleccione solo **local**

1. En la página **asignación de sitio** , seleccione el código del sitio de **Administración** con un punto de administración de dispositivos.

1. En la página **Seleccionar punto de proxy de inscripción** , seleccione solo la **intranet**y, a continuación, seleccione uno o más puntos de proxy de inscripción. El dispositivo usará estos servidores para iniciar el proceso de inscripción.

1. En la página **seleccionar certificado raíz de confianza** , seleccione el perfil de certificado que contiene el certificado raíz de confianza.

1. En la página **perfiles de Wi-Fi** , seleccione el perfil de Wi-Fi que contiene la configuración de red necesaria para que los dispositivos se conecten.

    > [!TIP]
    > Si no usa un perfil de Wi-Fi para el paquete de inscripción, omita este paso.

1. Complete el asistente.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>Crear un paquete de inscripción

El paquete de inscripción (ppkg) es el archivo que se usa para la inscripción masiva de dispositivos para MDM local. Cree este archivo con Configuration Manager. Aunque puede crear tipos similares de paquetes con Windows ICD, solo los paquetes que cree en Configuration Manager se pueden usar para inscribir dispositivos para MDM local. Un paquete que se crea con Windows ICD solo puede proporcionar el nombre principal de usuario (UPN) necesario para la inscripción, no puede iniciar el proceso de inscripción real.

El proceso para crear el paquete de inscripción requiere Windows Assessment and Deployment Kit (ADK) para Windows 10. En el equipo que ejecuta la consola de Configuration Manager, instale la versión más reciente de Windows ADK. Seleccione la característica del **Diseñador de imágenes y configuración (ICD)** y las dependencias. (Esta versión no tiene que coincidir con la versión usada para la implementación del sistema operativo en el sitio de Configuration Manager). Para obtener más información, consulte [Descargar Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install).

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** , expanda **todos los dispositivos propiedad de la empresa**, expanda **Windows**y seleccione el nodo **perfiles de inscripción** .

1. Seleccione un perfil de inscripción existente. En la cinta de opciones, seleccione **exportar**.

1. En la ventana exportar paquete de inscripción, especifique la información siguiente:

    - **Período de validez (días)**: de forma predeterminada, Configuration Manager establece que el paquete de inscripción expire en dos semanas (14 días). No puede usar el paquete para la inscripción de dispositivos después de que expire el período de validez. Escriba un número entero entre 1 y 30.

    - **Archivo de paquete**: especifique una ruta de acceso de archivo local o de red y un nombre para el archivo. ppkg.

    - **Cifrar paquete**: habilite esta opción para proteger con contraseña el paquete. Después de exportar el paquete, Configuration Manager muestra la contraseña generada. Copie y guarde la contraseña en una ubicación segura. No se puede usar el paquete de inscripción exportado sin la contraseña.

        > [!IMPORTANT]
        > Configuration Manager no guarda la contraseña y no se puede personalizar ni cambiar. Una vez que se cierra la ventana que muestra la contraseña, no hay forma de recuperar la contraseña.

1. Seleccione **Exportar**. Configuration Manager usa Windows ADK para crear el paquete de inscripción.

Configuration Manager realiza un seguimiento de los paquetes de inscripción válidos. En la consola de, expanda el nodo **Perfil de inscripción** y seleccione **paquetes exportados**.

> [!TIP]
> Si quita un paquete de inscripción de la consola de Configuration Manager, no podrá usarlo para inscribir dispositivos. Use este método para administrar paquetes de inscripción que no desea que otros usuarios usen para la inscripción masiva.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>Inscripción masiva de un dispositivo

Puede usar un paquete para inscribir dispositivos antes o después del proceso de la experiencia rápida (OOBE) del dispositivo. El paquete de inscripción también se puede incluir como parte del paquete de aprovisionamiento de un fabricante de equipos originales (OEM).

Para usar el paquete para la inscripción masiva, debe entregarlo físicamente al dispositivo. Hay varios métodos en función de sus necesidades, por ejemplo:

- Copiar del sistema de archivos

- Adjuntar a un correo electrónico

- Copia a través de una conexión de transmisión de campos en proximidad (NFC)

- Copiar desde una tarjeta de memoria

- Escanear un código de barras

- Copia desde un dispositivo anclado a red

- Incluir en un paquete de aprovisionamiento de OEM

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Inscribir un dispositivo con un paquete de inscripción masiva

1. En un dispositivo, abra el archivo. ppkg. Ejecute como administrador si es necesario.

1. Windows pregunta si el paquete proviene de una fuente de confianza, seleccione **sí**.

Se inicia el proceso de inscripción.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>Comprobar la inscripción

### <a name="verify-bulk-enrollment-on-the-device"></a>Comprobar la inscripción masiva en el dispositivo

1. En el dispositivo, Abra **configuración**.

1. Seleccione **cuentas**y, a continuación, **acceso profesional o educativo**. Cuando la inscripción se realiza correctamente, verá una cuenta en **empresa**.

1. Seleccione la cuenta y, a continuación, seleccione **sincronizar**. Esta acción inicia la administración con Configuration Manager.

### <a name="verify-enrollment-in-the-console"></a>Comprobación de la inscripción en la consola

Use la consola de Configuration Manager para comprobar que los dispositivos están inscritos correctamente. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione **Dispositivos**. Examine o busque el dispositivo inscrito en la lista de dispositivos.
