---
title: Administración de Endpoint Protection con directivas de grupo
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar Endpoint Protection con directivas de grupo.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d028dc6149ae1fee2d61634b96ccf450fc8f4b24
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700606"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>Uso de la configuración de directiva de grupo para administrar Endpoint Protection en versiones anteriores de Windows

**Se aplica a:**

- [Protección contra amenazas avanzada de Microsoft Defender (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center Endpoint Protection en los siguientes dispositivos de nivel inferior:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

Puede tener varios dispositivos Windows de nivel inferior o heredados que estén habilitados con Endpoint Protection, pero que estén fuera de la jerarquía de Configuration Manager. Por ejemplo, dispositivos en una zona desmilitarizada o dispositivos que se integran mediante fusiones y adquisiciones. 

Puede administrar Endpoint Protection en estos dispositivos con la configuración de directiva de grupo, que se describe a continuación:

- [Copia de definiciones de directiva de Endpoint Protection](#copy-endpoint-protection-policy-definitions)
- Cargue las definiciones de directiva de Endpoint Protection en cualquiera de las siguientes ubicaciones:
    - [Almacén central en un controlador de dominio (recomendado)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Dispositivo local](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Para obtener información sobre cómo usar la configuración de directiva de grupo para administrar el Antivirus de Microsoft Defender en Windows 10, Windows Server 2019 y Windows Server 2016, vea [Usar la configuración de directiva de grupo para configurar y administrar Antivirus de Microsoft Defender](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## <a name="copy-endpoint-protection-policy-definitions"></a>Copia de definiciones de directiva de Endpoint Protection

En un dispositivo Windows de nivel inferior administrado por Endpoint Protection, copie los archivos de definición de directivas de Endpoint Protection.

1. Vaya a **C:\Archivos de programa\Microsoft Security Client\Admx**. 

2. Comprima los siguientes archivos en un archivo ZIP, por ejemplo **SCEP_admx.zip**:
    - **EndPointProtection.adml**
    - **EndPointProtection.admx**
3. Copie el archivo ZIP en una carpeta temporal. Por ejemplo, **C:\temp_SCEP_GPO_admx**.
4. Extrae el archivo. 

> [!NOTE]
> Las claves del Registro para configurar la directiva de Endpoint Protection se encuentran en **Hkey_Local_Machine\Software\Policies\Microsoft\Microsoft Antimalware**.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Carga de la configuración de directiva de grupo de Endpoint Protection en un almacén central de un controlador de dominio

Si usa un [almacén central de plantillas administrativas de la directiva de grupo](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), realice los pasos siguientes para cargar y configurar la directiva de grupo de Endpoint Protection. Éste es el método recomendado.

1. Vaya a la carpeta donde extrajo los archivos de definición de directiva de Endpoint Protection.
2. Copie los archivos .admx y .adml en la carpeta **PolicyDefinitions** del controlador de dominio:
    1. Copie **EndPointProtection.admx** en **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions**. 
    2. Copie **EndPointProtection.adml** en **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions\\en-US**.  

    Por ejemplo:
    
    - Copie **EndPointProtection.admx** en **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Copie **EndPointProtection.adml** en **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US**.
    
    donde **DC** es el nombre del controlador de dominio y **contoso.com** es su dominio.

3. Abra la [Consola de administración de directivas de grupo](/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) y cree un objeto de directiva de grupo (GPO) en el dominio; por ejemplo, **Endpoint Protection**.
4. Haga clic con el botón derecho en el GPO para Endpoint Protection y haga clic en **Editar**.
5. En el Editor de administración de directivas de grupo, vaya a **Configuración del equipo** > **Directivas** > **Plantillas administrativas: Definiciones de directiva** > **Componentes de Windows** > **Endpoint Protection**.

   Se muestra la lista de directivas de grupo de Endpoint Protection.

6. Expanda la sección que contiene la configuración que desea realizar, haga doble clic en la opción para abrirla y realice los cambios de configuración.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Carga de la configuración de directiva de grupo de Endpoint Protection en el dispositivo local

En lugar de usar el almacén central para cargar las definiciones de directiva de Endpoint Protection, puede almacenarlas localmente en el dispositivo.

1. Vaya a la carpeta donde extrajo los archivos de definición de directiva de Endpoint Protection.
2. Copie los archivos .admx y .adml en la carpeta PolicyDefinitions local.
    1. Copie **EndPointProtection.admx** en **%SystemRoot%/PolicyDefinitions**. 
    2. Copie **EndPointProtection.adml** en **%SystemRoot%/PolicyDefinitions/en-US**.
    
    Por ejemplo:

    - Copie **EndPointProtection.admx** en **C:\Windows\PolicyDefinitions**.
    - Copie **EndPointProtection.adml** en **C:\Windows\PolicyDefinitions\en-US**.
    
3. Abre el Editor de directivas de grupo local.
4. Vaya a **Configuración del equipo** > **Plantillas administrativas** > **Componentes de Windows** > **Endpoint Protection**.

    Se muestra la lista de directivas de grupo de Endpoint Protection.

5. Expanda la sección que contiene la configuración que desea realizar, haga doble clic en la opción para abrirla y realice los cambios de configuración.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener información general sobre Endpoint Protection, vea [Endpoint Protection](endpoint-protection.md).
- Para obtener información sobre la configuración manual de Endpoint Protection en un cliente independiente, vea [Configuración de Endpoint Protection en un cliente independiente](endpoint-protection-configure-standalone-client.md).