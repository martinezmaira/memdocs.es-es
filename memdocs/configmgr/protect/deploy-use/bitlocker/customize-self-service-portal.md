---
title: Personalización del portal de autoservicio
titleSuffix: Configuration Manager
description: Agregue información personalizada específica de la organización al portal de autoservicio de administración de BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f4fdb0d6a41c2b40c9e35840dfc27261a42e68b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693503"
---
# <a name="customize-the-self-service-portal"></a>Personalización del portal de autoservicio

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Después de [instalar el portal de autoservicio de BitLocker](setup-websites.md), puede personalizarlo para la organización. Agregue un aviso personalizado, el nombre de la organización y otra información específica de esta.

## <a name="branding"></a>Personalización de marca

Personalice el portal de autoservicio con el nombre de la organización, la dirección URL del departamento de soporte técnico y el texto de aviso.

1. En el servidor web en el que se hospeda el portal de autoservicio, inicie sesión como administrador.

1. Inicie el **Administrador de Internet Information Services (IIS)** (ejecute **inetmgr.exe**).

1. Expanda **Sitios**, expanda **Sitio web predeterminado** y seleccione el nodo **SelfService**. En el panel de detalles, en el grupo **ASP.NET**, abra **Configuración de la aplicación**.

    [![Captura de pantalla de ejemplo de Configuración de la aplicación SelfService en el Administrador de IIS](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Seleccione el elemento que quiera cambiar y, en el panel **Acciones**, seleccione **Editar**. Cambie el **Valor** por el nuevo nombre que quiera usar.

    > [!CAUTION]
    > No cambie los valores **Nombre**. Por ejemplo, no cambie `CompanyName`, sino `Contoso IT`. Si cambia los valores **Nombre**, el portal de autoservicio dejará de funcionar.

Los cambios tienen efecto inmediatamente.

### <a name="supported-branding-values"></a>Valores de personalización de marca admitidos

Para ver los valores que puede establecer, consulte la tabla siguiente:

|Nombre|Descripción|Default&nbsp;value|
|--- |--- |--- |
|CompanyName|El nombre de la organización que el portal de autoservicio muestra como un encabezado en la parte superior de todas las páginas.|`Contoso IT`|
|DisplayNotice|Se muestra un aviso inicial que el usuario tiene que confirmar.|`true`|
|HelpdeskText|Cadena del panel de la derecha, debajo de "Para todos los demás problemas relacionados".|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|Vínculo para la cadena HelpdeskText.|(vacío)|
|NoticeTextPath|Texto del aviso inicial que el usuario tiene que confirmar. De forma predeterminada, la ruta de acceso completa del archivo en el servidor web es `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`. Edite y guarde el archivo en un editor de texto sin formato. Este valor de ruta de acceso es relativo a la aplicación SelfService.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Para obtener una captura de pantalla del portal de autoservicio predeterminado, vea [Portal de autoservicio de BitLocker](self-service-portal.md).

> [!TIP]
> Si es necesario, puede localizar algunas de estas cadenas para que se muestren en distintos idiomas. Para obtener más información, vea [Localización](#bkmk_localize).

## <a name="session-time-out"></a>Tiempo de espera de la sesión

Para asegurarse de que la sesión del usuario expire tras un periodo de inactividad concreto, puede cambiar la configuración de tiempo de espera de sesión para el portal de autoservicio.

1. En el servidor web en el que se hospeda el portal de autoservicio, inicie sesión como administrador.

1. Inicie el **Administrador de Internet Information Services (IIS)** (ejecute **inetmgr.exe**).

1. Expanda **Sitios**, expanda **Sitio web predeterminado** y seleccione el nodo **SelfService**. En el panel de detalles, en el grupo **ASP.NET**, abra **Estado de la sesión**.

1. En el grupo **Configuración de cookies**, cambie el valor **Tiempo de espera (en minutos)** . Es el número de minutos después del que expirará la sesión del usuario. El valor predeterminado es `5`. Para deshabilitar el valor de modo que no haya ningún tiempo de espera, establézcalo en `0`.

1. En el panel **Acciones**, seleccione **Aplicar**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a> Localización del texto y la dirección URL del departamento de soporte técnico

Puede configurar versiones localizadas de la instrucción `HelpdeskText` y el vínculo `HelpdeskUrl` del portal de autoservicio. Esta cadena informa a los usuarios sobre cómo obtener ayuda adicional cuando utilizan el portal. Si configura texto localizado, en el portal se muestra la versión localizada para los exploradores web en ese idioma. Si no encuentra una versión localizada, muestra el valor predeterminado de las opciones `HelpdeskText` y `HelpdeskUrl`.

1. En el servidor web en el que se hospeda el portal de autoservicio, inicie sesión como administrador.

1. Inicie el **Administrador de Internet Information Services (IIS)** (ejecute **inetmgr.exe**).

1. Expanda **Sitios**, expanda **Sitio web predeterminado** y seleccione el nodo **SelfService**. En el panel de detalles, en el grupo **ASP.NET**, abra **Configuración de la aplicación**.

1. En el panel **Acciones**, seleccione **Agregar**.

1. En la ventana **Agregar configuración de aplicaciones**, configure los valores siguientes:

    - **Nombre**: escriba `HelpdeskText_<language>`, donde `<language>` es el código de idioma del texto.

      Por ejemplo, para crear una instrucción `HelpdeskText` localizada en Español (España), el nombre es `HelpdeskText_es-es`.

    - **Valor**: la cadena localizada que se va a mostrar en el panel derecho del portal de autoservicio, debajo de "Para todos los demás problemas relacionados".

1. Seleccione **Aceptar** para guardar la nueva configuración.

1. Repita este proceso para agregar una nueva configuración de la aplicación para `HelpdeskUrl_<language>` que coincida con el valor `HelpdeskText_<language>` asociado.

Repita este proceso para agregar un par de opciones para todos los idiomas que se admitan en la organización.

## <a name="localize-the-notice-file"></a>Localización del archivo de aviso

Puede configurar versiones localizadas del aviso inicial que el usuario tiene que confirmar en el portal de autoservicio. De forma predeterminada, la ruta de acceso completa del archivo en el servidor web es `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`.

Para mostrar el texto de aviso localizado, cree un archivo notice.txt localizado. Después, guárdelo en una carpeta de idioma específica. Por ejemplo: `Self Service Website\es-es\Notice.txt` para Español (España).

En el portal de autoservicio se muestra el texto del aviso según las reglas siguientes:

- Si falta el archivo de aviso predeterminado, el portal muestra un mensaje que lo indica.

- Si crea un archivo de aviso localizado en la carpeta de idioma correspondiente, muestra el texto de aviso localizado.

- Si el servidor web no encuentra una versión localizada del archivo de aviso, muestra el aviso predeterminado.

- Si el usuario establece el explorador en un idioma que no tiene un aviso localizado, en el portal se muestra el aviso predeterminado.

### <a name="create-a-localized-notice-file"></a>Creación de un archivo de aviso localizado

1. En el servidor web en el que se hospeda el portal de autoservicio, inicie sesión como administrador.

1. Cree una carpeta `<language>` para cada idioma admitido en la ruta de acceso de la aplicación `Self Service Website`. Por ejemplo, `es-es` para Español (España). De forma predeterminada, la ruta de acceso completa es `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`.

    Para obtener una lista de los códigos de idioma válidos que puede usar, vea [Referencia de API National Language Support (NLS)](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers).

    > [!TIP]
    > El nombre de la carpeta de idioma también puede ser el nombre neutro del idioma. Por ejemplo, **es** para Español, en lugar de **es-es** para Español (España) y **es-ar** para Español (Argentina). Si el usuario establece el explorador en **es-es** y esa carpeta de idioma no existe, el servidor web comprueba de forma recursiva la carpeta de configuración regional principal (**es**). Las configuraciones regionales principales se definen en .NET. Por ejemplo, `Self Service Website\es\Notice.txt`. Esta reserva recursiva imita las reglas de carga de recursos de .NET.

1. Cree una copia del archivo de aviso predeterminado con el texto localizado. Guárdelo en la carpeta del código de idioma. Por ejemplo, para Español (España), la ruta de acceso completa es `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`de forma predeterminada.

Repita este proceso para agregar un archivo de aviso localizado para todos los idiomas que se admitan en la organización.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha instalado y personalizado el portal de autoservicio, pruébelo. Para obtener más información, vea [Portal de autoservicio de BitLocker](self-service-portal.md).
