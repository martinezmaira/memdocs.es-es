---
title: Configuración de Windows Hello para empresas
titleSuffix: Configuration Manager
description: Aprenda a integrar Windows Hello para empresas con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4c8029cdda80d327cbed2a4c60c71ff1811e4723
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698704"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Configuración de Windows Hello para empresas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1245704-->
Configuration Manager se integra con Windows Hello para empresas. Esta característica se conocía anteriormente como Microsoft Passport for Work. Windows Hello para empresas es un método de inicio de sesión alternativo para dispositivos Windows 10. Usa Active Directory o una cuenta de Azure Active Directory (Azure AD) para reemplazar una contraseña, una tarjeta inteligente o una tarjeta inteligente virtual. Hello para empresas permite usar un *gesto de usuario* para iniciar sesión, en lugar de una contraseña. Un gesto de usuario puede ser un PIN, una autenticación biométrica o un dispositivo externo, como un lector de huellas digitales.

> [!Important]  
> A partir de la versión 1910, no se admite la autenticación basada en certificados con configuración de Windows Hello para empresas en Configuration Manager. Para obtener más información, vea [Características en desuso](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). La autenticación basada en claves sigue siendo válida.
>
> La implementación de Active Directory Federation Services Registration Authority (ADFS RA) es más sencilla, proporciona una mejor experiencia de usuario y tiene una experiencia de inscripción de certificados más determinista. Use ADFS RA para la autenticación basada en certificados con Windows Hello para empresas.
>
> En el caso de los dispositivos administrados conjuntamente, considere la posibilidad de mover la [carga de trabajo de las **directivas de acceso a recursos**](../../comanage/workloads.md#resource-access-policies) a Intune. Posteriormente, use las directivas de Intune para administrar estos certificados. Para más información, consulte el artículo sobre el [cambio de las cargas de trabajo](../../comanage/how-to-switch-workloads.md).

Para obtener más información, vea [Windows Hello para empresas](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Configuration Manager se integra con Windows Hello para empresas de las siguientes maneras:  

- Control de los gestos que los usuarios pueden y no pueden utilizar para iniciar sesión.  

- Almacene los certificados de autenticación en el proveedor de almacenamiento de claves (KSP) de Windows Hello para empresas. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  

- Creación e implementación de un perfil de Windows Hello para empresas para controlar su configuración en dispositivos de Windows 10 unidos a dominio que ejecutan el cliente de Configuration Manager. A partir de la versión 1910, no se puede usar la autenticación basada en certificados. Si usa autenticación basada en claves, no necesita implementar un perfil de certificado.

## <a name="configure-a-profile"></a>Configurar un perfil  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento**, expanda **Acceso a recursos de la compañía** y seleccione el nodo **Perfiles de Windows Hello para empresas**.

1. En la cinta de opciones, seleccione **Crear perfil de Windows Hello para empresas** para iniciar el asistente para perfiles.

1. En la página **General**, especifique un nombre y una descripción opcional para este perfil.

1. En la página **Plataformas compatibles**, seleccione las versiones de sistema operativo a las que se debe aplicar este perfil.

1. En la página **Configuración**, configure las siguientes opciones:

    - **Configurar Windows Hello para empresas**: Especifique si este perfil habilita, deshabilita o no configura Hello para empresas.

    - **Usar un Módulo de plataforma segura (TPM)** : Un chip de TPM ofrece una capa adicional de seguridad de datos. Elija uno de los siguientes valores:  

      - **Requerido**: Solo los dispositivos que tengan un TPM accesible pueden aprovisionar Windows Hello para empresas.  

      - **Preferido**: Los dispositivos intentan primero usar un TPM. Si no está disponible, pueden usar cifrado de software.

    - **Método de autenticación**: Establezca esta opción en **No configurado** o **Basado en claves**.

        > [!NOTE]
        > A partir de la versión 1910, no se admite la autenticación basada en certificados con configuración de Windows Hello para empresas en Configuration Manager.

    - **Configurar la longitud mínima del PIN**: Si quiere requerir una longitud mínima para el PIN del usuario, habilite esta opción y especifique un valor. Cuando la opción está habilitada, el valor predeterminado es `4`.

    - **Configurar la longitud máxima del PIN**: Si quiere requerir una longitud máxima para el PIN del usuario, habilite esta opción y especifique un valor. Cuando la opción está habilitada, el valor predeterminado es `127`.

    - **Requerir expiración de PIN (días)** : especifique el número de días antes de que el usuario deba cambiar el PIN del dispositivo.

    - **Impedir la reutilización de PIN anteriores**: No permita que los usuarios usen PIN que hayan usado previamente.

    - **Requerir letras en mayúscula en el PIN**: especifica si los usuarios deben incluir letras en mayúscula en el PIN de Windows Hello para empresas. Elija de entre las siguientes opciones:  

      - **Permitido**: los usuarios pueden usar caracteres en mayúscula en su PIN, aunque no es obligatorio.

      - **Requerido**: los usuarios deben incluir al menos un carácter en mayúscula en su PIN.  

      - **No permitido**: los usuarios no pueden usar caracteres en mayúscula en su PIN.  

    - **Requerir letras en minúscula en el PIN**: especifica si los usuarios deben incluir letras en minúscula en el PIN de Windows Hello para empresas. Elija de entre las siguientes opciones:  

      - **Permitido**: los usuarios pueden usar caracteres en minúscula en su PIN, aunque no es obligatorio.

      - **Requerido**: los usuarios deben incluir al menos un carácter en minúscula en su PIN.  

      - **No permitido**: los usuarios no pueden usar caracteres en minúscula en su PIN.  

    - **Configurar caracteres especiales**: Especifica el uso de caracteres especiales en el PIN. Elija de entre las siguientes opciones:  

        > [!NOTE]
        > Entre los caracteres especiales se incluye el conjunto siguiente:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Permitido**: los usuarios pueden usar caracteres especiales en su PIN, aunque no es obligatorio.  

      - **Requerido**: los usuarios deben incluir al menos un carácter especial en su PIN.  

      - **No permitido**: los usuarios no pueden usar caracteres especiales en su PIN. (Este es también el comportamiento si la opción aparece como **No configurada**).  

    - **Configurar el uso de dígitos en PIN**: especifica el uso de números en el PIN. Elija de entre las siguientes opciones:

      - **Permitido**: los usuarios pueden usar números en su PIN, aunque no es obligatorio.  

      - **Requerido**: los usuarios deben incluir al menos un número en su PIN.  

      - **No permitido**: los usuarios no pueden usar números en su PIN.

    - **Habilitar gestos de biometría**: usar la autenticación biométrica, como el reconocimiento o las huellas digitales. Estos modos son una alternativa a un PIN para Windows Hello para empresas. Los usuarios siguen configurando un PIN por si produce un error en la autenticación biométrica.  

      Si se establece en **Sí**, Windows Hello para empresas permite la autenticación biométrica. Si se establece en **No**, Windows Hello para empresas evita la autenticación biométrica para todos los tipos de cuenta.  

    - **Usar tecnología mejorada contra la suplantación de identidad**: configura la protección contra suplantación de identidad mejorada en dispositivos que lo admiten. Si se establece en **Sí**, donde se admita, Windows exige que todos los usuarios usen la protección contra la suplantación de identidad para las características faciales.  

    - **Usar inicio de sesión por teléfono**: configura la autenticación en dos fases con un teléfono móvil.

1. Complete el asistente.

La captura de pantalla siguiente es un ejemplo de configuración de perfil de Windows Hello para empresas:  

![Asistente para directivas de Windows Hello para empresas con la lista de configuraciones disponibles](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Configurar permisos

1. Como administrador de dominio o si tiene credenciales equivalentes, inicie sesión en una estación de trabajo administrativa segura que tenga instalada la siguiente característica opcional: RSAT: Herramientas de Servicios de dominio de Active Directory y Lightweight Directory Services.

1. Abra la consola **Usuarios y equipos de Active Directory**.

1. Seleccione el dominio, vaya al menú **Acción** y seleccione **Propiedades**.

1. Vaya a la pestaña **Seguridad** y seleccione **Opciones avanzadas**.

    > [!TIP]
    > Si no ve la pestaña **Security**, cierre la ventana de propiedades. Vaya al menú **Ver** y seleccione **Características avanzadas**.

1. Seleccione **Agregar**.

1. Elija **Seleccionar una entidad de seguridad** y escriba `Key Admins`.

1. En la lista **Se aplica a**, seleccione **Descendant User objects** (Objetos de usuario descendiente).

1. En la parte inferior de la página, seleccione **Borrar todo**.

1. En la sección **Propiedades**, seleccione **Read msDS-KeyCredentialLink** (Leer msDS-KeyCredentialLink).

1. Seleccione **Aceptar** para guardar los cambios y cerrar todas las ventanas.

## <a name="next-steps"></a>Pasos siguientes

[Perfiles de certificado](introduction-to-certificate-profiles.md)