---
title: Crear perfiles de certificado PFX
titleSuffix: Configuration Manager
description: Aprenda a usar archivos PFX en Configuration Manager para generar certificados específicos del usuario que admitan el intercambio de datos cifrados.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724579"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Creación de perfiles de certificado PFX mediante una entidad de certificación

*Se aplica a: Configuration Manager (rama actual)*

Obtenga información sobre cómo crear un perfil de certificado que use una entidad de certificación para las credenciales. En este artículo se resalta información específica acerca de los perfiles de certificado de intercambio de información personal (PFX). Para obtener más información sobre cómo crear y configurar estos perfiles, consulte [perfiles de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager le permite crear un perfil de certificado PFX con las credenciales emitidas por una entidad de certificación. Puede elegir Microsoft o Entrust como entidad de certificación. Cuando se implementa en dispositivos de usuario, los archivos PFX generan certificados específicos del usuario para admitir el intercambio de datos cifrados.

Para importar las credenciales de certificado de archivos de certificado existentes, consulte [importación de perfiles de certificado pfx](import-pfx-certificate-profiles.md).

## <a name="prerequisites"></a>Prerrequisitos

Antes de empezar a crear un perfil de certificado, asegúrese de que los requisitos previos necesarios estén listos. Para obtener más información, consulte [Prerequisites for Certificate profiles](../../protect/plan-design/prerequisites-for-certificate-profiles.md). Por ejemplo, en el caso de los perfiles de certificado PFX, necesita un rol de sistema de sitio de [punto de registro de certificado](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) .

## <a name="create-a-profile"></a>Creación de un perfil  

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** , expanda **configuración de cumplimiento**, expanda **acceso a recursos**de la compañía y, a continuación, seleccione **perfiles de certificado**.

1. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear perfil de certificado**.

1. En la página **General** del **Asistente para crear Perfil de certificado**, especifique la información siguiente:  

    - **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

    - **Descripción**: proporcione una descripción general del perfil de certificado que le ayude a identificarlo en la consola de Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

1. Seleccione **intercambio de información personal: configuración de PKCS #12 (pfx): crear**. Esta opción solicita un certificado en nombre de un usuario de una entidad de certificación (CA) local conectada. Elija su entidad de certificación: **Microsoft** o **Entrust Datacard**.

    > [!NOTE]
    > La opción de **importación** obtiene información de un certificado existente para crear un perfil de certificado. Para más información, consulte [Importar perfiles de certificado PFX](import-pfx-certificate-profiles.md).

1. En la página **plataformas admitidas** , seleccione las versiones de sistema operativo compatibles con este perfil de certificado. Para obtener más información sobre las versiones de sistema operativo compatibles con su versión de Configuration Manager, consulte [versiones de sistema operativo compatibles con clientes y dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. En la página **entidades de certificación** , elija el punto de registro de certificado (CRP) para procesar los certificados pfx:

    1. **Sitio primario**: elija el servidor que contiene el rol de PRC para la CA.
    1. **Entidades de certificación**: seleccione la CA pertinente.

    Para más información, vea [Infraestructura de certificados](../../protect/deploy-use/certificate-infrastructure.md).

La configuración de la página **certificado pfx** varía en función de la CA seleccionada en la página **General** :

- [CA de Microsoft](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Configuración de **certificados pfx** para Microsoft CA

1. En el **nombre**de la plantilla de certificado, elija la plantilla de certificado.

1. Para usar el perfil de certificado para la firma o el cifrado de S/MIME, habilite el **uso de certificados**.

    Cuando se habilita esta opción, se entregan todos los certificados PFX asociados al usuario de destino a todos sus dispositivos. Si no habilita esta opción, cada dispositivo recibe un certificado único.  

1. Establezca **Formato de nombre de sujeto** en **Nombre común** o **Nombre completo**. Si no está seguro de cuál usar, póngase en contacto con el administrador de la entidad de certificación.

1. Para el **nombre alternativo del firmante**, habilite la **dirección de correo electrónico** y el **nombre principal de usuario (UPN)** según corresponda para la CA.

1. **Umbral de renovación**: determina cuándo se renuevan los certificados automáticamente, en función del porcentaje de tiempo restante antes de la expiración.

1. Establezca **Período de validez del certificado** en la duración del certificado.

1. Cuando el punto de registro de certificado especifique Active Directory credenciales, habilite la **publicación de Active Directory**.

1. Si seleccionó una o varias plataformas compatibles con Windows 10:

    1. Establezca el **almacén de certificados de Windows** en **usuario**. (La opción **equipo local** no implementa certificados, no la elija).

    1. Seleccione uno de los siguientes **proveedores de almacenamiento de claves (KSP)**:

        - **Instalar en Módulo de plataforma segura (TPM) si está presente**  
        - **Instalación en Módulo de plataforma segura (TPM); de lo contrario, error**
        - **Instalar en Windows Hello para empresas. de lo contrario, error**
        - **Instalar en proveedor de almacenamiento de claves de software**

1. Complete el asistente.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Configuración de **certificados pfx** para Entrust Datacard CA

1. Para la **configuración de ID. digital**, elija el perfil de configuración. El administrador de Entrust crea las opciones de configuración de ID. digital.

1. Para usar el perfil de certificado para la firma o el cifrado de S/MIME, habilite el **uso de certificados**.

    Cuando se habilita esta opción, se entregan todos los certificados PFX asociados al usuario de destino a todos sus dispositivos. Si no habilita esta opción, cada dispositivo recibe un certificado único.  

1. Para asignar los tokens de **formato de nombre de sujeto** de Entrust a Configuration Manager campos, seleccione **formato**.

    El cuadro de diálogo **Formato de nombre de sujeto de certificado** enumera las variables de configuración de identificador digital de Entrust. Para cada variable de Entrust, elija los campos de Configuration Manager adecuados.

1. Para asignar tokens de **nombre alternativo del firmante** de Entrust a variables LDAP compatibles, seleccione **formato**.

    El cuadro de diálogo **Formato de nombre de sujeto de certificado** enumera las variables de configuración de identificador digital de Entrust. Para cada variable de Entrust, elija la variable LDAP adecuada.

1. **Umbral de renovación**: determina cuándo se renuevan los certificados automáticamente, en función del porcentaje de tiempo restante antes de la expiración.

1. Establezca **Período de validez del certificado** en la duración del certificado.

1. Cuando el punto de registro de certificado especifique Active Directory credenciales, habilite la **publicación de Active Directory**.

1. Si seleccionó una o varias plataformas compatibles con Windows 10:

    1. Establezca el **almacén de certificados de Windows** en **usuario**. (La opción **equipo local** no implementa certificados, no la elija).

    1. Seleccione uno de los siguientes **proveedores de almacenamiento de claves (KSP)**:

        - **Instalar en Módulo de plataforma segura (TPM) si está presente**  
        - **Instalación en Módulo de plataforma segura (TPM); de lo contrario, error**
        - **Instalar en Windows Hello para empresas. de lo contrario, error**
        - **Instalar en proveedor de almacenamiento de claves de software**

1. Complete el asistente.

## <a name="deploy-the-profile"></a>Implementar el perfil

Después de crear un perfil de certificado, ahora está disponible en el nodo **perfiles de certificado** . Para obtener más información sobre cómo implementarla, consulte [implementación de perfiles de acceso de recursos](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Consulte también

[Crear un nuevo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md)

[Importar perfiles de certificado PFX](import-pfx-certificate-profiles.md)

[Implementación de perfiles de Wi-Fi, VPN, correo electrónico y certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
