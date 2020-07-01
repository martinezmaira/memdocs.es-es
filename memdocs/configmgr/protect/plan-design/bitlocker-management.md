---
title: Planeamiento de la administración de BitLocker
titleSuffix: Configuration Manager
description: Planeamiento de la administración de Cifrado de unidad BitLocker con Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c03d5d06dc6b49ceff6af8ce862eb19cb4a517a
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531475"
---
# <a name="plan-for-bitlocker-management"></a>Planeamiento de la administración de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!-- 3601034 -->

A partir de la versión 1910, use Configuration Manager para administrar el Cifrado de unidad BitLocker (BDE) para clientes Windows locales, que están unidos a Active Directory. No se admiten clientes de grupo de trabajo ni unidos a Azure Active Directory. Ofrece una administración completa del ciclo de vida de BitLocker que puede sustituir el uso de Microsoft BitLocker Administration and Monitoring (MBAM).

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Para obtener más información, vea [Información general de BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Para administrar el cifrado en dispositivos Windows 10 de administración conjunta con el servicio en la nube de Microsoft Endpoint Manager, cambie la [carga de trabajo de **Endpoint Protection**](../../comanage/workloads.md#endpoint-protection) a Intune. Para obtener más información sobre el uso de Intune, vea [Cifrado de Windows](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Funciones

Configuration Manager proporciona las siguientes capacidades de administración de Cifrado de unidad BitLocker:

### <a name="client-deployment"></a>Implementación de cliente

Implementación del cliente de BitLocker en dispositivos Windows administrados que ejecutan Windows 10 o Windows 8.1

### <a name="manage-encryption-policies"></a>Administración de directivas de cifrado

- Por ejemplo: elija cifrado de unidad e intensidad de cifrado, configurar directiva de exención de usuario y configuración de cifrado de la unidad de datos fija.

- Determine los algoritmos con los que se va a cifrar el dispositivo y los discos de destino para el cifrado.

- Obligue a los usuarios a que cumplan las nuevas directivas de seguridad antes de usar el dispositivo.

- Personalice el perfil de seguridad de su organización en función de cada dispositivo.

- Cuando un usuario desbloquea la unidad del sistema operativo, especifique si quiere desbloquear solo una unidad del sistema operativo o todas las unidades conectadas.

### <a name="compliance-reports"></a>Informes de cumplimiento

Informes integrados para:

- El estado de cifrado por volumen o por dispositivo.
- El usuario primario del dispositivo.
- Estado de cumplimiento
- Motivos de no cumplimiento

### <a name="administration-and-monitoring-website"></a>Sitio web de administración y supervisión

Permita que otros roles de su organización fuera de la consola de Configuration Manager ayuden con la recuperación de claves, incluida la rotación de claves y asistencia adicional relacionada con BitLocker. Por ejemplo, los administradores del departamento de soporte técnico pueden ayudar a los usuarios con la recuperación de claves.

### <a name="user-self-service-portal"></a>Portal de autoservicio del usuario

Permita que los usuarios se ayuden con una clave de un solo uso para desbloquear un dispositivo cifrado de BitLocker. Una vez que se usa esta clave, se genera una clave nueva para el dispositivo.

## <a name="prerequisites"></a>Requisitos previos

- Para crear una directiva de administración de BitLocker, necesita el rol de **Administrador total** en Configuration Manager.

- El servicio de recuperación de BitLocker requiere HTTPS para cifrar las claves de recuperación en toda la red desde el cliente de Configuration Manager al punto de administración. Hay dos opciones:

  - HTTPS: habilite el sitio web de IIS en el punto de administración que hospeda el servicio de recuperación. Esta opción solo se aplica a Configuration Manager, versión 2002.<!-- 5925660 -->

  - Configure el punto de administración para HTTPS. Esta opción se aplica a las versiones 1910 o 2002 de Configuration Manager.

  Para obtener más información, consulte el artículo [Cifrado de los datos de recuperación](../deploy-use/bitlocker/encrypt-recovery-data.md).

- Para usar los informes de administración de BitLocker, instale el rol de sistema de sitio del punto de servicios de informes. Para más información, consulte [Configuración de informes](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > Para que el **informe de auditoría de recuperación** funcione desde el sitio web de administración y supervisión, use solo un punto de servicios de informes en el sitio primario.

- Para usar el portal de autoservicio o el sitio web de administración y supervisión, necesita un servidor de Windows que ejecute IIS. Puede reutilizar un sistema de sitio de Configuration Manager o usar un servidor web independiente que tenga conectividad con el servidor de base de datos del sitio. Use una [versión de SO compatible para los servidores de sistema de sitio](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Instale solo el portal de autoservicio y el sitio web de administración y supervisión con una base de datos de sitio primario. En una jerarquía, instale estos sitios web para cada sitio primario.

- En el servidor web que hospedará el portal de autoservicio, instale [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4) y la característica .NET Framework 3.5 antes de iniciar el proceso de instalación. Otros roles y características de Windows Server necesarios se instalarán automáticamente durante el proceso de instalación del portal.

- La cuenta de usuario que ejecuta el script del instalador del portal necesita derechos **sysadmin** de SQL en el servidor de base de datos del sitio. Durante el proceso de configuración, el script establece el inicio de sesión, el usuario y los derechos de rol de SQL de la cuenta del equipo del servidor web. Puede quitar esta cuenta de usuario del rol sysadmin después de completar la instalación del portal de autoservicio y el sitio web de administración y supervisión.

- La administración de BitLocker no se admite en máquinas virtuales (VM) en sistemas operativos de servidor. Por este motivo, es posible que algunas características no funcionen según lo previsto en las máquinas virtuales o en sistemas operativos de servidor. Por ejemplo, en máquinas virtuales, la administración de BitLocker no iniciará el cifrado en unidades fijas de máquinas virtuales. Además, es posible que algunas unidades fijas en máquinas virtuales se muestren como compatibles, aunque no estén cifradas.

> [!TIP]
> De forma predeterminada, el paso de secuencia de tareas **Habilitar BitLocker** solo cifra el *espacio usado* en la unidad. La administración de BitLocker usa el cifrado de *disco completo*. Configure este paso de secuencia de tareas para habilitar la opción para **usar el cifrado de disco completo**. Para obtener más información, vea [Pasos de la secuencia de tareas - Habilitar BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Pasos siguientes

[Cifrado de los datos de recuperación](../deploy-use/bitlocker/encrypt-recovery-data.md) (un requisito previo opcional antes de implementar la directiva por primera vez)

[Implementación del cliente de administración de BitLocker](../deploy-use/bitlocker/deploy-management-agent.md)
