---
title: Creación de aplicaciones Windows
titleSuffix: Configuration Manager
description: Obtenga más información sobre cómo crear e implementar aplicaciones Windows en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2712613eb6d03253c05a011037ac8492992e1f03
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695195"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Crear aplicaciones Windows en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Además de los otros requisitos y procedimientos de Configuration Manager para [crear una aplicación](../deploy-use/create-applications.md), tenga en cuenta también las consideraciones siguientes al crear e implementar aplicaciones para dispositivos Windows.  

## <a name="general-considerations"></a><a name="bkmk_general"></a> Consideraciones generales  

Configuration Manager admite la implementación de los formatos de paquete de aplicaciones (.appx) y lote de aplicaciones (.appxbundle) de Windows para dispositivos Windows 8.1 y Windows 10.

Al crear una aplicación en la consola de Configuration Manager, seleccione el **Tipo** de archivo de instalación de la aplicación como **Paquete de aplicación de Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** . Para obtener más información sobre cómo crear aplicaciones en general, consulte [Crear aplicaciones](../deploy-use/create-applications.md). Para obtener más información sobre el formato MSIX, consulte [Compatibilidad con formato MSIX](#bkmk_msix).

> [!Note]  
> Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a> Aprovisionar los paquetes de aplicación de Windows para todos los usuarios en un dispositivo
<!--1358310-->
Aprovisione una aplicación con un paquete de la aplicación de Windows para todos los usuarios del dispositivo. Un ejemplo común de este escenario es el aprovisionamiento de una aplicación de Microsoft Store para Empresas y Educación, como Minecraft: Education Edition, en todos los dispositivos que usan los alumnos de una escuela. Anteriormente, Configuration Manager solo admitía la instalación de estas aplicaciones por usuario. Tras iniciar sesión en un dispositivo nuevo, un estudiante tendría que esperar para obtener acceso a una aplicación. Ahora, al aprovisionarse la aplicación en el dispositivo para todos los usuarios, estos pueden empezar a trabajar más rápidamente.

> [!Important]  
> Tenga cuidado con la instalación, el aprovisionamiento y la actualización de versiones diferentes del mismo paquete de aplicación de Windows en un dispositivo, ya que puede producir resultados inesperados. Este comportamiento puede producirse si se usa Configuration Manager para aprovisionar la aplicación y, después, se permite a los usuarios actualizar la aplicación desde Microsoft Store. Para obtener más información, consulte las instrucciones del paso siguiente si [administra aplicaciones de Microsoft Store para Empresas](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Al implementar aplicaciones sin conexión en dispositivos Windows 10 con el cliente de Configuration Manager, no permita a los usuarios actualizar aplicaciones externas en implementaciones de Configuration Manager. El control de las actualizaciones de las aplicaciones sin conexión es especialmente importante en entornos de varios usuarios como clases. Para más información, consulte [Administración de aplicaciones desde Microsoft Store para Empresas y Educación con Configuration Manager](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).<!-- MEMDocs#316 -->

Configuration Manager admite el aprovisionamiento de aplicaciones en las versiones siguientes de Windows 10 admitidas.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Para configurar un tipo de implementación de aplicación de Windows para esta característica, habilite la opción **Provision this application for all users on the device** (Aprovisionar esta aplicación para todos los usuarios en el dispositivo). Para obtener más información, consulte [Create applications](../deploy-use/create-applications.md) (Creación de aplicaciones).

> [!Note]  
> Si necesita desinstalar una aplicación aprovisionada de dispositivos en los que los usuarios ya han iniciado sesión, deberá crear dos implementaciones de desinstalación. Dirija la primera instalación de desinstalación a una colección de dispositivos que contenga los dispositivos. Dirija la segunda implementación de desinstalación a una colección que contenga los usuarios que ya han iniciado sesión en los dispositivos que incluyan la aplicación aprovisionada. Cuando se desinstala una aplicación aprovisionada de un dispositivo, Windows no desinstala actualmente la aplicación para los usuarios.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a> Compatibilidad con formato MSIX
<!--1357427-->

Configuration Manager admite los formatos de paquete de aplicaciones (.msix) y lote de aplicaciones (.msixbundle) de Windows 10. Windows 10, versión 1809 o posteriores, admite estos formatos.

- Para obtener información general de MSIX, consulte [A closer look at MSIX](/archive/blogs/sgern/a-closer-look-at-msix) (Análisis exhaustivo de MSIX).  

- Para crear una aplicación MSIX, vea [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) (Compatibilidad de MSIX introducida en la compilación 17682 de Insider).  

### <a name="convert-applications-to-msix"></a>Conversión de aplicaciones a MSIX
<!--3607729, fka 1359029-->

Convierta las aplicaciones existentes de Windows Installer (.msi) al formato MSIX.

#### <a name="prerequisites-for-msix"></a>Requisitos previos para MSIX

- Un dispositivo de referencia que ejecuta Windows 10 versión 1809 o posterior  

- Inicie sesión en Windows en este dispositivo como un usuario con derechos administrativos locales.  

- Instale las siguientes aplicaciones en este dispositivo:  

  - Consola de Configuration Manager  

  - Instale la [herramienta de empaquetado MSIX](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) desde Microsoft Store.  

  - Instale el [controlador de la herramienta de empaquetado MSIX](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

No instale ningún otro servicio o aplicación en este dispositivo. Es el sistema de referencia.

#### <a name="process-to-convert-applications-to-msix-format"></a>Proceso para convertir aplicaciones al formato MSIX

1. Eleve la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2. Seleccione una aplicación que tenga un tipo de implementación de Windows Installer (.msi).  

    > [!Note]  
    > Debe ser capaz de acceder al contenido de origen de la aplicación desde el dispositivo de referencia.  
    >
    > El nombre de la aplicación no puede tener caracteres especiales. Configuration Manager usa el nombre de la aplicación como el nombre del archivo de salida.  
    >
    > No instale esta aplicación de antemano en el dispositivo de referencia.  

3. Seleccione **Convertir a .MSIX** en la cinta de opciones.

Una vez finalizado el asistente, la herramienta de empaquetado MSIX crea un archivo MSIX en la ubicación especificada en el asistente. Durante este proceso, Configuration Manager instala silenciosamente la aplicación en el dispositivo de referencia.

Si se produce un error en el proceso, la página de resumen apunta al archivo de registro con más información. Si se produce un error relacionado con la captura de estado de usuario, cierre la sesión de Windows. Iniciar sesión de nuevo puede resolver este problema.

Para usar esta aplicación MSIX, primero deberá firmarla digitalmente para que los clientes confíen en ella. Para más información sobre este proceso, vea los siguientes artículos:

- [MSIX – The MSIX Packaging Tool – signing the MSIX package](/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package) (MSIX; la herramienta de empaquetado MSIX: firma del paquete MSIX)
- [How to sign an app package using SignTool](/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool) (Cómo firmar un paquete de la aplicación con SignTool)

Una vez firmada la aplicación, cree un tipo de implementación en la aplicación en Configuration Manager. Para obtener más información, consulte [Crear tipos de implementación de la aplicación](../deploy-use/create-applications.md#bkmk_create-dt).

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a> Tipo de implementación de la secuencia de tareas

<!--3555953-->

> [!Note]  
> En esta versión de Configuration Manager, el tipo de implementación de secuencia de tareas es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../core/servers/manage/pre-release-features.md).  

A partir de la versión 2002, puede instalar aplicaciones complejas mediante secuencias de tareas a través del modelo de aplicación. Agregue un tipo de implementación de secuencia de tareas a una aplicación, para instalar o desinstalar la aplicación. Este tipo de implementación proporciona los comportamientos siguientes:

<!-- - Deploy an app task sequence to a user collection -->

- Mostrar la secuencia de tareas de aplicación con un icono en el Centro de software. Un icono facilita a los usuarios buscar e identificar la secuencia de tareas de aplicación.

- Definir metadatos adicionales para la secuencia de tareas de aplicación, incluida información localizada.

Solo se puede agregar una secuencia de tareas de implementación que no sea del sistema operativo como tipo de implementación en una aplicación. No se admiten las secuencias de tareas de gran impacto, de implementación del sistema operativo ni de actualización del sistema operativo. <!--A user-targeted deployment still runs in the user context of the local System account.-->

Al agregar este tipo de implementación a una aplicación, configure sus propiedades en la página **Secuencia de tareas**. Para obtener más información, vea las opciones [Tipo de implementación **Secuencia de tareas**](../deploy-use/create-applications.md#bkmk_dt-ts).

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Requisitos previos para un tipo de implementación de secuencia de tareas

Cree una secuencia de tareas personalizada:

- Use solo pasos de implementación que no sean de sistema operativo, por ejemplo: **Instalar paquete**, **Ejecutar línea de comandos** o **Ejecutar script de PowerShell**. Para más información, incluida la lista completa de pasos compatibles, vea [Crear una secuencia de tareas para implementaciones que no son de sistema operativo](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- En las propiedades de la secuencia de tareas, en la pestaña **Notificación de usuario**, no seleccione la opción para una secuencia de tareas de gran impacto.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

Al crear la aplicación, para agregar un tipo de implementación de secuencia de tareas, la cuenta de usuario necesita permiso para leer las secuencias de tareas.<!-- 6348976 --> Utilice una de las siguientes opciones para configurar estos permisos:

- Agregue la cuenta de usuario del administrador de la aplicación al rol de **Analista de solo lectura** integrado. Este rol permite ver todos los objetos de Configuration Manager.

- Copie el rol de **Administrador de aplicaciones** integrado para crear un rol personalizado. Agregue el permiso de **Lectura** en el objeto de **Paquete de secuencia de tareas**.

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Problemas conocidos de un tipo de implementación de secuencia de tareas

- Todavía no se puede implementar una secuencia de tareas de aplicación en una colección de usuarios.

- No siga el paso **Instalar aplicación** en esta secuencia de tareas. Para instalar aplicaciones, siga el paso [Instalar paquete](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage).

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a> Compatibilidad para aplicaciones para Plataforma universal de Windows (UWP)  

Los dispositivos Windows 10 no necesitan una clave de instalación de prueba para instalar las aplicaciones de línea de negocio. Pero para habilitar la instalación de prueba en Windows, la clave del Registro `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` debe tener un valor de **1**.  

Si no se configura esta clave del Registro, Configuration Manager establece este valor automáticamente en **1** la primera vez que se implemente una aplicación en el dispositivo. Si este valor se ha establecido en **0**, Configuration Manager no puede cambiarlo automáticamente y se produce un error en la implementación de las aplicaciones de línea de negocio.  

Firme digitalmente las aplicaciones de línea de negocio para UWP. Use un certificado de firma de código que sea de confianza en todos los dispositivos en los que se implemente la aplicación. Use certificados de la PKI de la organización, o bien compre un certificado de un proveedor de terceros cuyo certificado raíz público ya sea de confianza para Windows.  

Para firmar los paquetes de aplicaciones móviles, use la tabla siguiente para determinar el tipo de certificado de firma de código que se va a usar:

| Paquete  | Symantec  | Distinto de Symantec  |
|---------|---------|---------|
| Paquetes **.appx** universales en dispositivos Windows 10 Mobile | Sí | Sí |
| Paquetes **.xap** | Sí | No |
| Paquetes **.appx** creados para Windows Phone 8.1 para instalar en dispositivos Windows 10 Mobile | Sí | No |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a> Implementar aplicaciones de Windows Installer en equipos de Windows 10 inscritos con MDM  

El tipo de implementación **Windows Installer a través de MDM (\*.msi)** permite crear e implementar aplicaciones basadas en Windows Installer en dispositivos inscritos con MDM que ejecutan Windows 10.  

Cuando se usa este tipo de implementación, tenga en cuenta los aspectos siguientes:

- Solo se carga un único archivo con la extensión MSI.  

- Configuration Manager usa el código de producto y la versión del producto del archivo para la detección de la aplicación.  

- Windows usa el comportamiento de reinicio predeterminado de la aplicación. Configuration Manager no controla el comportamiento de reinicio de la aplicación.  

- Se instalan paquetes MSI por usuario para un solo usuario.  

- Se instalan paquetes MSI por equipo para todos los usuarios del dispositivo.  

- Configuration Manager admite las actualizaciones de aplicaciones. El código de producto MSI de cada versión debe ser el mismo.