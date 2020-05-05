---
title: Certificados para MDM local
titleSuffix: Configuration Manager
description: Configure certificados para comunicaciones de confianza con la administración local de dispositivos móviles (MDM) en Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724669"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Configuración de certificados para comunicaciones de confianza con MDM local

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager la administración de dispositivos móviles (MDM) local requiere que configure los roles de sistema de sitio para las comunicaciones de confianza con los dispositivos administrados. Necesita dos tipos de certificados:

- Un **certificado de servidor Web** en IIS en los servidores que hospedan los roles de sistema de sitio necesarios. Si un servidor hospeda varios roles de sistema de sitio, solo necesita un certificado para ese servidor. Si cada rol está en un servidor independiente, cada servidor necesita un certificado independiente.

- El **certificado raíz de confianza** de la entidad de certificación (CA) que emite los certificados de servidor Web. Instale este certificado raíz en todos los dispositivos que necesiten conectarse a los roles de sistema de sitio.

En el caso de los dispositivos Unidos a un dominio, si usa servicios de Certificate Server de Active Directory, puede instalar automáticamente estos certificados en todos los dispositivos. En el caso de los dispositivos no Unidos a un dominio, instale el certificado raíz de confianza por otros medios.

En el caso de los dispositivos inscritos de forma masiva, puede incluir el certificado en el paquete de inscripción. Para dispositivos inscritos por el usuario, debe agregar el certificado mediante correo electrónico, descarga web o algún otro método.

Si usa una entidad de certificación pública conocida como VeriSign o GoDaddy para emitir los certificados de servidor, puede evitar tener que instalar manualmente el certificado raíz de confianza en cada dispositivo. La mayoría de los dispositivos confían de forma nativa en estas entidades públicas. Este método es una alternativa útil para los dispositivos inscritos por el usuario, en lugar de instalar el certificado a través de otros medios.

> [!IMPORTANT]  
> Hay muchas maneras de configurar los certificados para las comunicaciones de confianza entre los dispositivos y los servidores de sistema de sitio para MDM local. La información de este artículo es un ejemplo de una manera de hacerlo. Este método requiere Active Directory servicios de Certificate Server, con una entidad de certificación y el rol de inscripción Web de entidad de certificación. Para obtener más información, consulte [Active Directory servicios de Certificate Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>Publicar la CRL

De forma predeterminada, el Active Directory entidad de certificación (CA) utiliza listas de revocación de certificados (CRL) basadas en LDAP. Permite conexiones a la CRL para dispositivos Unidos a un dominio. Para permitir que los dispositivos que no están Unidos a un dominio confíen en los certificados emitidos por la CA, agregue una CRL basada en HTTP.

1. En el servidor que ejecuta la entidad de certificación de su sitio, vaya al menú **Inicio** , seleccione **herramientas administrativas**y elija **entidad de certificación**.

1. En la consola entidad de certificación, haga clic con el botón secundario en **CertificateAuthority**y seleccione **propiedades**.

1. En propiedades de CertificateAuthority, cambie a la pestaña **extensiones** . Asegúrese de que **seleccionar extensión** está establecido en **punto de distribución de CRL (CDP)**.

1. Seleccione `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. A continuación, seleccione las siguientes opciones:

    - **Incluir en CRL. los clientes lo usan para buscar ubicaciones de diferencias CRL.**

    - **Incluir en la extensión CDP de los certificados emitidos.**

    - **Incluir en la extensión IDP de CRL emitidas**

1. Cambie a la pestaña **módulo de salida** . Seleccione **propiedades**y, a continuación, seleccione permitir que **los certificados se publiquen en el sistema de archivos**. Verá un aviso para reiniciar Active Directory servicios de Certificate Server.

1. Haga clic con el botón derecho en **certificados revocados**, seleccione **todas las tareas**y, a continuación, elija **publicar**.

1. En la ventana publicar CRL, seleccione **solo diferencias CRL**y, a continuación, seleccione **Aceptar** para cerrar la ventana.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Crear la plantilla de certificado

La entidad de certificación usa la plantilla de certificado de servidor web para emitir certificados para los servidores que hospedan los roles de sistema de sitio. Estos servidores serán puntos de conexión SSL para las comunicaciones de confianza entre los roles de sistema de sitio y los dispositivos inscritos.

1. Cree un grupo de seguridad de dominio denominado **servidores MDM de Configuration Manager**. Agregue al grupo las cuentas de equipo de los servidores de sistema de sitio.

1. En la consola entidad de certificación, haga clic con el botón derecho en **plantillas de certificado**y elija **administrar**. Esta acción carga la consola de plantillas de certificado.

1. En el panel de resultados, haga clic con el botón derecho en la entrada que muestra **servidor Web** en la columna **nombre para mostrar plantilla** y, a continuación, seleccione **duplicar plantilla**.

1. En la ventana de **plantilla duplicada** , seleccione **Windows 2003 Server, Enterprise edition** o **Windows 2008 Server, Enterprise Edition**y, a continuación, seleccione **Aceptar**.

    > [!TIP]
    > Configuration Manager es compatible con las plantillas de certificado de servidor de Windows 2008, también conocidas como certificados V3 o Cryptography: Next Generation (CNG). Para obtener más información, consulte [Introducción a los certificados CNG](../../core/plan-design/network/cng-certificates-overview.md).

    Si la CA se ejecuta en Windows Server 2012 o posterior, esta ventana no muestra la opción para la versión de la plantilla de certificado. Después de duplicar la plantilla, seleccione la versión en la pestaña **compatibilidad** de las propiedades de la plantilla.

1. En la ventana **propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla. La entidad de certificación usa este nombre para generar los certificados web que se utilizarán en los sistemas de sitio Configuration Manager. Por ejemplo, escriba **servidor Web MDM de ConfigMgr**.

1. Cambie a la pestaña **nombre de sujeto** y seleccione **compilar a partir de Active Directory información**. En el formato de nombre de sujeto, especifique el **nombre DNS**. Si **nombre principal del usuario (UPN)** está seleccionado, deshabilite la opción para el nombre de sujeto alternativo.

1. Cambie a la pestaña **seguridad** .

    1. Quite el permiso **inscribir** de los grupos de seguridad **Admins** . del dominio y **administradores de organización** .

    1. Seleccione **Agregar**y escriba el nombre del grupo de seguridad. Por ejemplo, **servidores MDM de Configuration Manager**. Seleccione **Aceptar** para cerrar la ventana.

    1. Seleccione el permiso **inscribir** para este grupo. No quite el permiso de **lectura** .

1. Seleccione **Aceptar** para guardar los cambios y cierre la consola de plantillas de certificado.

1. En la consola entidad de certificación, haga clic con el botón secundario en **plantillas de certificado**, seleccione **nuevo**y, a continuación, elija **plantilla de certificado para emitir**.

1. En la ventana **Habilitar plantillas de certificados** , seleccione la nueva plantilla. Por ejemplo, **servidor Web MDM de ConfigMgr**. Después, seleccione **Aceptar** para guardar y cerrar la ventana.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Solicitar el certificado

Este proceso describe cómo solicitar el certificado de servidor web para IIS. Realice este proceso para cada servidor de sistema de sitio que hospede uno de los roles para MDM local.

1. En el servidor de sistema de sitio que hospeda uno de los roles, abra un símbolo del sistema como administrador. Escriba `mmc` para abrir una consola de administración de Microsoft vacía.

1. En la ventana de la consola, vaya al menú **archivo** y seleccione **Agregar o quitar complemento**.

    1. Elija **certificados** en la lista de complementos disponibles y seleccione **Agregar**.

    1. En la ventana del complemento certificados, elija **cuenta de equipo**. Seleccione **siguiente**y, después, haga clic en **Finalizar** para administrar el equipo local.

    1. Seleccione **Aceptar** para salir de la ventana Agregar o quitar complemento.

1. Expanda **certificados (equipo local)** y seleccione el almacén **personal** . Vaya al menú **acción** , seleccione **todas las tareas**y elija **solicitar nuevo certificado**. Esta acción se comunica con Active Directory servicios de Certificate Server para crear un nuevo certificado con la plantilla que ha creado anteriormente.

    1. En el Asistente para inscripción de certificados, en la página antes de comenzar, seleccione **siguiente**.

    1. En la página seleccionar Directiva de inscripción de certificados, seleccione **Active Directory Directiva de inscripción**y, a continuación, seleccione **siguiente**.

    1. Seleccione la plantilla de certificado de servidor Web (**CONFIGMGR MDM Web Server**) y, a continuación, seleccione **inscribir**.

    1. Después de solicitar el certificado, seleccione **Finalizar**.

Cada servidor necesita un certificado de servidor Web único. Repita este proceso para cada servidor que hospede uno de los roles de sistema de sitio necesarios. Si un servidor hospeda todos los roles de sistema de sitio, solo será necesario solicitar un certificado de servidor web.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Enlazar el certificado

El siguiente paso consiste en enlazar el nuevo certificado al servidor Web. Siga este proceso para cada servidor que hospede los roles de sistema de sitio de punto de *inscripción* y *punto de proxy de inscripción* . Si un servidor hospeda todos los roles de sistema de sitio, solo necesita realizar este proceso una vez.

> [!NOTE]
> No es necesario que realice este proceso para los roles de sistema de sitio de punto de distribución y punto de administración de dispositivos. Reciben automáticamente el certificado necesario durante la inscripción.

1. En el servidor que hospeda el punto de inscripción o el punto de proxy de inscripción, vaya al menú **Inicio** , seleccione **herramientas administrativas**y elija **Administrador de IIS**.

1. En la lista de conexiones, seleccione el **sitio web predeterminado**y, a continuación, seleccione **Editar enlaces**.

    1. En la ventana enlaces de sitios, seleccione **https**y, a continuación, seleccione **Editar**.

    1. En la ventana Editar enlace de sitio, seleccione el certificado que se acaba de inscribir para el **certificado SSL**. Seleccione **Aceptar** para guardar y, a continuación, seleccione **cerrar**.

1. En la consola del administrador de IIS, en la lista de conexiones, seleccione el servidor Web. En el panel acción, en el lado derecho, seleccione **reiniciar**. Esta acción reinicia el servicio servidor Web.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Exportar el certificado raíz de confianza

Active Directory servicios de Certificate Server instala automáticamente el certificado necesario de la entidad de certificación en todos los dispositivos Unidos a un dominio. Para obtener el certificado necesario para que los dispositivos que no están Unidos a un dominio se comuniquen con los roles de sistema de sitio, expórtelo desde el certificado enlazado al servidor Web.

1. En el administrador de IIS, seleccione el **sitio web predeterminado**. En el panel acción, en el lado derecho, seleccione **enlaces**.

1. En la ventana enlaces de sitios, seleccione **https**y, a continuación, seleccione **Editar**.

1. Seleccione el certificado de servidor Web y seleccione **Ver**.

1. En las propiedades del certificado de servidor Web, cambie a la pestaña **ruta de certificación** . Seleccione la raíz de la ruta de certificación y seleccione **Ver certificado**.

1. En las propiedades del certificado raíz, cambie a la pestaña **detalles** y, a continuación, seleccione **copiar a archivo**.

1. En el Asistente para exportación de certificados, en la página de bienvenida, seleccione **siguiente**.

1. Seleccione **der binario codificado X. 509 (. CER)** como formato y seleccione **siguiente**.

1. Escriba una ruta de acceso y un nombre de archivo para identificar este certificado raíz de confianza. Como nombre de archivo, haga clic en **examinar...**, elija una ubicación para guardar el archivo de certificado, asigne un nombre al archivo y seleccione **siguiente**.

1. Revise la configuración y haga clic en **Finalizar** para exportar el certificado a un archivo.

En función del diseño de la entidad de certificación, puede que necesite exportar certificados raíz de CA subordinados adicionales. Repita este proceso para exportar los otros certificados de la ruta de certificación del certificado de servidor Web.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configurar la inscripción de dispositivos](set-up-device-enrollment-on-premises-mdm.md)
