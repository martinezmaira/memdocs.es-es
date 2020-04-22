---
title: Instalación de la consola
titleSuffix: Configuration Manager
description: Instale la consola de Configuration Manager para conectarse a un sitio de administración central o a un sitio primario.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700803"
---
# <a name="install-the-configuration-manager-console"></a>Instalación de la consola de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los administradores usan la consola de Configuration Manager para administrar el entorno de Configuration Manager. Cada consola de Configuration Manager puede conectarse a un sitio de administración central (CAS) o a un sitio primario. No se puede conectar una consola de Configuration Manager a un sitio secundario.

La consola del Configuration Manager siempre se instala en el servidor del sitio para el sitio de administración central o un sitio primario. Para instalar la consola de forma independiente a la instalación del servidor de sitio, ejecute el instalador independiente.  



## <a name="prerequisites"></a>Requisitos previos

- Tiene derechos de **Administrador** local en el equipo de destino para la consola.  

- Tiene permisos de **Lectura** para la ubicación de los archivos de instalación de la consola de Configuration Manager.  



## <a name="source-paths"></a>Rutas de acceso de origen

Decida qué ruta de origen utilizar:  

- Carpeta ConsoleSetup en el servidor de sitio: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Al instalar un servidor de sitio, copia los archivos de instalación de la consola y los paquetes de idioma admitidos para el sitio en la subcarpeta **Tools\ConsoleSetup**. Opcionalmente, puede copiar la carpeta **ConsoleSetup** en una ubicación alternativa para iniciar la instalación. Cuando actualiza el sitio, mantiene siempre actualizada la versión local.  

- Medios de instalación de Configuration Manager: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Al instalar la consola de Configuration Manager desde el medio de instalación siempre se instala la versión en inglés. Este comportamiento se produce incluso si el servidor de sitio admite varios idiomas, o bien si el sistema operativo del equipo de destino está establecido en otro idioma.  

Cuando sea posible, inicie el instalador de la consola desde la carpeta **ConsoleSetup** en lugar de desde el soporte físico de origen.

> [!Important]  
> No instale la consola mediante los archivos de origen **CD.Latest**. Es un escenario no admitido y puede causar problemas con la instalación de la consola. Para obtener más información, vea [La carpeta CD.Latest](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Si crea un paquete para instalar la consola en otros equipos, asegúrese de que el paquete incluya los siguientes archivos:<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (a partir de la versión 1902)
- ConfigMgr.AC_Extension.amd64.cab (a partir de la versión 1902)



## <a name="use-the-setup-wizard"></a>Usar el Asistente para instalación  

1. Vaya a la ruta de acceso de origen y abra **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Instale siempre la consola mediante **ConsoleSetup.exe**. Aunque se puede instalar la consola de Configuration Manager con adminconsole.msi, este método no ejecuta los requisitos previos ni las comprobaciones de dependencia. Es posible que la instalación no se realice correctamente.  

2. En el asistente, haga clic en **Siguiente**.  

3. En la página **Servidor de sitio**, escriba el nombre de dominio completo (FQDN) del servidor de sitio al que se conecta la consola de Configuration Manager.  

4. En la página **Carpeta de instalación**, escriba la carpeta de instalación para la consola de Configuration Manager. La ruta de la carpeta no puede contener espacios finales ni caracteres Unicode.  

5. En la página **Programa para la mejora de la experiencia del usuario**, elija si quiere participar en dicho programa.  

    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

6. En la página **Preparado para instalar**, seleccione **Instalar**.  



## <a name="install-from-a-command-prompt"></a>Instalación desde un símbolo del sistema  

> [!TIP]  
> Al instalar la consola de Configuration Manager desde un símbolo del sistema siempre se instala la versión en inglés. Este comportamiento se produce incluso si el sistema operativo del equipo de destino está establecido en otro idioma. Para instalar la consola de Configuration Manager en un idioma que no sea inglés, [utilice el Asistente para la instalación](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Opciones de línea de comandos de ConsoleSetup.exe

#### <a name="q"></a>/q

Instala la consola de Configuration Manager desatendida. Las opciones **EnableSQM**, **TargetDir**y **DefaultSiteServerName** son obligatorias si usa esta opción.

#### <a name="uninstall"></a>/uninstall

Desinstala la consola de Configuration Manager. Especifique primero esta opción cuando la use con la opción **/q**.

#### <a name="langpackdir"></a>LangPackDir

Especifica la ruta de acceso a la carpeta que contiene los archivos de idioma. Puede usar el **Descargador del programa de instalación** para descargar los archivos de idioma. Si no utiliza esta opción, el programa de instalación busca la carpeta de idioma en la carpeta actual. Si no se encuentra la carpeta de idioma, el programa de instalación continúa con la instalación únicamente de la versión en inglés. Para obtener más información, consulte [Descargador del programa de instalación](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Especifica la carpeta de instalación para instalar la consola de Configuration Manager. Esta opción es obligatoria si usa la opción **/q** .

#### <a name="enablesqm"></a>EnableSQM

Especifica si se va a participar en el Programa para la mejora de la experiencia del usuario (CEIP). Use un valor de **1** para unirse al CEIP y un valor de **0** para no unirse al programa. Esta opción es obligatoria si usa la opción **/q** .

> [!Important]  
> A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto. El uso del parámetro hará que la instalación dé error.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Especifica el FQDN del servidor de sitio al que se conecta la consola cuando se abre. Esta opción es obligatoria si usa la opción **/q** .


### <a name="examples"></a>Ejemplos

> [!Important]  
> Para la versión 1802 y más recientes, no incluya el parámetro **EnableSQM**.

#### <a name="silent-install"></a>Instalación silenciosa

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Instalación silenciosa con paquetes de idioma

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Desinstalación silenciosa

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Vea también

Un administrador ve los objetos en la consola en función de los permisos asignados a su cuenta de usuario. Para obtener más información, vea [Aspectos básicos de la administración basada en roles](../../../understand/fundamentals-of-role-based-administration.md).

Para más información sobre los fundamentos de navegar por la consola Configuration Manager, consulte [Uso de la consola](../../manage/admin-console.md).
