---
title: Ejemplo de implementación de certificados PKI
titleSuffix: Configuration Manager
description: Siga un ejemplo paso a paso para aprender a crear e implementar certificados PKI que se usan en Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7781c20ca542d19c562574c554a08c38493911f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700085"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Ejemplo paso a paso de implementación de los certificados PKI de Configuration Manager: Entidad de certificación de Windows Server 2008

*Se aplica a: Configuration Manager (rama actual)*

Esta implementación de ejemplo paso a paso, que usa una entidad de certificación (CA) de Windows Server 2008, contiene procedimientos que le muestran cómo crear e implementar los certificados de infraestructura de clave pública (PKI) que se usan en Configuration Manager. Estos procedimientos utilizan una entidad de certificación (CA) empresarial y plantillas de certificado. Los pasos son adecuados solo para una red de prueba, como una prueba de concepto.  

Al no haber un único método de implementación de los certificados requeridos, consulte su documentación de implementación de PKI específica para conocer los procedimientos necesarios y recomendados a la hora de implementar dichos certificados en un entorno de producción. Para información sobre los requisitos de certificado, consulte [Requisitos de certificados PKI para Configuration Manager](pki-certificate-requirements.md).  

> [!TIP]
> Puede aplicar las instrucciones de este tema a los sistemas operativos que no están documentados en la sección Requisitos de la red de prueba. Sin embargo, si se ejecuta la CA emisora en Windows Server 2012, no se le solicitará la versión de la plantilla de certificado. En su lugar, especifíquela en la pestaña **Compatibilidad** de las propiedades de la plantilla:  
>
> - **Entidad de certificación**: **Windows Server 2003**  
>   - **Destinatario del certificado**: **Windows XP / Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Requisitos de la red de prueba

Las instrucciones paso a paso tienen los siguientes requisitos:  

- La red de prueba ejecuta Servicios de dominio de Active Directory con Windows Server 2008 y se instala como un único dominio, un único bosque.  

- Dispone de un servidor miembro que ejecuta Windows Server 2008 Enterprise Edition, que tiene instalado el rol Servicios de certificados de Active Directory, y está configurado como una entidad de certificación raíz (CA) empresarial.  

- Dispone de un equipo que tiene Windows Server 2008 (Standard Edition o Enterprise Edition, R2 o posterior) instalado y está designado como servidor miembro, y en el que se ha instalado Internet Information Services (IIS). Este equipo será el servidor de sistema de sitio de Configuration Manager que configurará con un nombre de dominio completo (FQDN) de intranet para admitir conexiones de cliente en la intranet y un FQDN de Internet en caso de que sea necesario admitir dispositivos móviles inscritos por Configuration Manager y clientes de Internet.  

- Dispone de un cliente de Windows Vista que tiene el Service Pack más reciente instalado, y este equipo está configurado con un nombre de equipo en caracteres ASCII y está unido al dominio. Este equipo será un equipo cliente de Center Configuration Manager.  

- Puede iniciar sesión con una cuenta de administrador de dominio raíz o una cuenta de administrador de dominio de empresa y usar esta cuenta para todos los procedimientos en esta implementación de ejemplo.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Información general de los certificados

En la tabla siguiente se enumeran los tipos de certificados PKI que podrían ser necesarios para Configuration Manager y se describe cómo se usan.  

|Requisito de certificado|Descripción del certificado|  
|-----------------------------|-----------------------------|  
|Certificado de servidor web para los sistemas de sitio que ejecutan IIS|Este certificado se utiliza para cifrar los datos y autenticar el servidor en los clientes. Se debe instalar externamente desde Configuration Manager en servidores de sistemas de sitio que ejecutan Internet Information Services (IIS) y que están configurados en Center Configuration Manager para usar HTTPS.<br /><br /> Para conocer los pasos para configurar e instalar este certificado, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](#BKMK_webserver2008_cm2012) en este tema.|  
|Certificado de servicio para clientes que se conectan a puntos de distribución basados en la nube|Para conocer los pasos para configurar e instalar este certificado, vea [Implementación del certificado de servicio para puntos de distribución basados en la nube](#BKMK_clouddp2008_cm2012) en este tema.<br /><br /> **Importante:** Este certificado se utiliza junto con el certificado de administración de Microsoft Azure. Para obtener más información sobre el certificado de administración, vea [Creación de un certificado de administración](/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) y [Adición de un certificado de administración a una suscripción de Microsoft Azure](/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate).|  
|Certificado de cliente para equipos Windows|Este certificado se usa para autenticar equipos cliente de Configuration Manager en sistemas de sitio que están configurados para usar HTTPS. También puede usarse para puntos de administración y puntos de migración de estado para supervisar su estado de funcionamiento cuando están configurados para usar HTTPS. Se debe instalar externamente en los equipos desde Configuration Manager.<br /><br /> Para conocer los pasos para configurar e instalar este certificado, vea [Implementación del certificado de cliente para equipos Windows](#BKMK_client2008_cm2012) en este tema.|  
|Certificado de cliente para puntos de distribución|Este certificado tiene dos propósitos:<br /><br /> El certificado se utiliza para autenticar el punto de distribución en un punto de administración habilitado para HTTPS antes de que el punto de distribución envíe mensajes de estado.<br /><br /> Cuando está seleccionada la opción de punto de distribución **Habilitar compatibilidad de PXE para clientes** , el certificado se envía a equipos con arranque PXE para que puedan conectarse a un punto de administración habilitado para HTTPS durante la implementación del sistema operativo.<br /><br /> Para conocer los pasos para configurar e instalar este certificado, vea [Implementación del certificado de cliente para puntos de distribución](#BKMK_clientdistributionpoint2008_cm2012) en este tema.|  
|Certificado de inscripción para dispositivos móviles|Este certificado se usa para autenticar a los clientes de dispositivos móviles de Configuration Manager en sistemas de sitio que están configurados para usar HTTPS. Debe instalarse como parte de la inscripción de dispositivos móviles en Configuration Manager, y se selecciona la plantilla de certificado configurada como un valor de cliente de dispositivo móvil.<br /><br /> Para conocer los pasos para configurar este certificado, vea [Implementación del certificado de inscripción para dispositivos móviles](#BKMK_mobiledevices2008_cm2012) en este tema.|  
|Certificado de cliente para equipos Mac|Puede solicitar e instalar este certificado desde un equipo Mac al usar la inscripción de Configuration Manager y seleccionar la plantilla de certificado configurada como un valor de cliente de dispositivo móvil.<br /><br /> Para conocer los pasos para configurar este certificado, vea [Implementación del certificado de cliente para equipos Mac](#BKMK_MacClient_SP1) en este tema.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS

Esta implementación de certificado consta de los siguientes procedimientos:  

- Crear y emitir la plantilla de certificado de servidor web en la entidad de certificación  

- Solicitar el certificado de servidor web  

- Configurar IIS para usar el certificado de servidor web  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Crear y emitir la plantilla de certificado de servidor web en la entidad de certificación

Mediante este procedimiento se crea una plantilla de certificado para sistemas de sitio de Configuration Manager y se agrega a la entidad de certificación.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de servidor web en la entidad de certificación

1.  Cree un grupo de seguridad denominado **Servidores IIS de Configuration Manager** que tenga los servidores miembro para instalar sistemas de sitio de Configuration Manager que ejecutarán IIS.  

2.  En el servidor miembro que tenga Servicios de servidor de certificados instalados, en la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y, después, pulse **Administrar** para cargar la consola **Plantillas de certificado**.  

3.  En el panel de resultados, haga clic con el botón derecho en la entrada que tiene **Servidor web** en la columna **Nombre para mostrar de plantilla** y, después, pulse **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla**, asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, después, pulse **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba el nombre de la plantilla, como **Certificado de servidor web de Configuration Manager**, para generar los certificados web que se usarán en los sistemas de sitio de Configuration Manager.  

6.  Pulse la pestaña **Nombre de sujeto** y asegúrese de que se haya seleccionado **Proporcionado por el solicitante**.  

7.  Pulse la pestaña **Seguridad** y, después, elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de empresa**.  

8.  Pulse **Agregar**, escriba **Servidores IIS de Configuration Manager** en el cuadro de texto y, después, pulse **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso de **lectura**.  

10. Pulse **Aceptar** y, después, cierre la **consola de plantillas de certificado**.  

11. En la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado**, pulse **Nueva** y, después, en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Certificado de servidor web de Configuration Manager** y, después, pulse **Aceptar**.  

13. Si no necesita crear y emitir más certificados, cierre la **Entidad de certificación**.  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Solicitar el certificado de servidor web  
 Este procedimiento permite especificar los valores de FQDN de la intranet y de Internet que se configurarán en las propiedades del servidor de sistema de sitio y, después, instala el certificado de servidor web en el servidor miembro que ejecuta IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Para solicitar el certificado de servidor web  

1.  Reinicie el servidor miembro que ejecuta IIS para asegurarse de que el equipo pueda acceder a la plantilla de certificado que ha creado mediante los permisos de **lectura** e **Inscribir** que ha configurado.  

2.  Pulse **Inicio**, seleccione **Ejecutar** y, después, escriba **mmc.exe**. En la consola vacía, pulse **Archivo** y, después, pulse **Agregar o quitar complemento**.  

3.  En el cuadro de diálogo **Agregar o quitar complementos**, seleccione **Certificados** en la lista de **Complementos disponibles** y, después, pulse **Agregar**.  

4.  En el cuadro de diálogo **Complemento de certificado**, seleccione **Cuenta de equipo** y, después, pulse **Siguiente**.  

5.  En el cuadro de diálogo **Seleccionar equipo**, asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, después, pulse **Finalizar**.  

6.  En el cuadro de diálogo **Agregar o quitar complementos**, pulse **Aceptar**.  

7.  En la consola, expanda **Certificados (equipo local)** y, después, pulse **Personal**.  

8.  Haga clic con el botón derecho en **Certificados**, pulse **Todas las tareas** y, después, pulse **Solicitar un nuevo certificado**.  

9. En la página **Antes de comenzar**, seleccione **Siguiente**.  

10. Si ve la página **Seleccionar directiva de inscripción de certificados**, pulse **Siguiente**.  

11. En la página **Solicitar certificados**, identifique el **Certificado de servidor web de Configuration Manager** en la lista de certificados disponibles y, después, seleccione **Se necesita más información para inscribir este certificado. Haga clic aquí para configurar los valores**.  

12. En el cuadro de diálogo **Propiedades de certificado**, en la pestaña **Sujeto**, no realice cambios en el **Nombre de sujeto**. Esto significa que el cuadro **Valor** de la sección **Nombre de sujeto** permanece en blanco. En su lugar, en la sección **Nombre alternativo**, pulse la lista desplegable **Tipo** y, después, seleccione **DNS**.  

13. En el cuadro **Valor**, indique los valores de FQDN que especificará en las propiedades del sistema de sitio de Configuration Manager y, después, elija **Aceptar** para cerrar el cuadro de diálogo **Propiedades de certificado**.  

     Ejemplos:  

    - Si el sistema de sitio solo va a aceptar conexiones de cliente de la intranet y el FQDN de la intranet del servidor de sistema de sitio es **server1.internal.contoso.com**, escriba **server1.internal.contoso.com** y, después, pulse **Agregar**.  

    - Si el sistema de sitio va a aceptar conexiones de cliente desde la intranet e Internet, y el FQDN de la intranet del servidor de sistema de sitio es **server1.internal.contoso.com** y el FQDN de Internet del servidor de sistema de sitio es **server.contoso.com**:  

        1.  Escriba **server1.internal.contoso.com** y, después, haga clic en **Agregar**.  

        2.  Escriba **server.contoso.com** y, después, pulse **Agregar**.  

        > [!NOTE]  
        >  Puede especificar los FQDN de Configuration Manager en cualquier orden. En cambio, compruebe que todos los dispositivos que van a usar el certificado, como dispositivos móviles y servidores proxy web, puedan usar un nombre alternativo del asunto del certificado (SAN) y varios valores en el SAN. Si los dispositivos tienen compatibilidad limitada con los valores de SAN en los certificados, tendrá que cambiar el orden de los FQDN o utilizar el valor Sujeto en su lugar.  

14. En la página **Solicitar certificados**, seleccione el **Certificado de servidor web de Configuration Manager** en la lista de certificados disponibles y, después, pulse **Inscribir**.  

15. En la página **Resultados de la instalación de certificados**, espere hasta que se instale el certificado y, después, pulse **Finalizar**.  

16. Cierre **Certificados (equipo local)** .  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Configurar IIS para usar el certificado de servidor web  
 Este procedimiento permite enlazar el certificado instalado con el **Sitio web predeterminado**de IIS.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Para configurar IIS para usar el certificado de servidor web  

1. En el servidor miembro que tiene IIS instalado, pulse **Inicio**, **Programas**, **Herramientas administrativas** y, después, pulse **Administrador de Internet Information Services (IIS)** .  

2. Expanda **Sitios**, haga clic con el botón derecho en **Sitio web predeterminado** y, después, seleccione **Modificar enlaces**.  

3. Pulse la entrada **https** y, después, en **Editar**.  

4. En el cuadro de diálogo **Modificar enlace de sitio**, seleccione el certificado que ha solicitado mediante la plantilla de certificados de servidor web de Configuration Manager y, después, pulse **Aceptar**.  

   > [!NOTE]  
   >  Si no está seguro de cuál es el certificado correcto, seleccione uno y, después, pulse **Ver**. Esto le permite comparar los detalles del certificado seleccionado con los certificados del complemento Certificados. Por ejemplo, el complemento de certificado muestra la plantilla de certificado que se ha usado para solicitar el certificado. A continuación podrá comparar la huella digital del certificado que se ha solicitado con la plantilla de certificados de servidor web de Configuration Manager con la huella digital del certificado actualmente seleccionado en el cuadro de diálogo **Modificar enlace de sitio**.  

5. Pulse **Aceptar** en el cuadro de diálogo **Modificar enlace de sitio** y, después, pulse **Cerrar**.  

6. Cierre el **Administrador de Internet Information Services (IIS)** .  

   El servidor miembro está configurado ahora con un certificado de servidor web de Configuration Manager.  

> [!IMPORTANT]  
>  Al instalar el servidor de sistema de sitio de Configuration Manager en este equipo, asegúrese de especificar los mismos FQDN en las propiedades del sistema de sitio que especificó al solicitar el certificado.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Implementación del certificado de servicio para puntos de distribución basados en la nube  

Esta implementación de certificado consta de los siguientes procedimientos:  

- [Crear y emitir una plantilla de certificado de servidor web personalizado en la entidad de certificación](#BKMK_clouddpcreating2008)  

- [Solicitar el certificado de servidor web personalizado](#BKMK_clouddprequesting2008)  

- [Exportar el certificado de servidor web personalizado para puntos de distribución basados en la nube](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Crear y emitir una plantilla de certificado de servidor web personalizado en la entidad de certificación  
 Este procedimiento crea una plantilla de certificado personalizado que se basa en la plantilla de certificado de servidor web. Se trata de un certificado para puntos de distribución basados en la nube de Configuration Manager y la clave privada debe ser exportable. La plantilla de certificado, una vez creada, se agrega a la entidad de certificación.  

> [!NOTE]
>  Este procedimiento usa una plantilla de certificado diferente a la plantilla de certificado de servidor web que ha creado para los sistemas de sitio que ejecutan IIS. Aunque ambos certificados necesitan la capacidad de autenticación de servidor, el certificado para los puntos de distribución basados en la nube requiere que escriba un valor definido por el usuario para el nombre de sujeto, y la clave privada debe exportarse. Como procedimiento recomendado de seguridad, no configure plantillas de certificado que permitan la exportación de la clave privada a menos que se requiera esta configuración. El punto de distribución basado en la nube requiere esta configuración porque debe importar el certificado como un archivo, en lugar de seleccionarlo en el almacén de certificados.  
> 
>  Cuando crea una nueva plantilla de certificado para este certificado, puede restringir los equipos que pueden solicitar un certificado cuya clave privada puede exportarse. En una red de producción, también podría agregar los siguientes cambios para este certificado:  
> 
> - Solicitar aprobación para instalar el certificado, para mayor seguridad.  
>   - Incrementar el periodo de validez del certificado. Como debe exportar e importar el certificado siempre antes de que expire, al incrementar el período de validez se reduce la frecuencia con la que debe repetir este procedimiento. En cambio, al incrementar el periodo de validez también se reduce la seguridad del certificado porque un atacante tendría más tiempo para descifrar la clave privada y robar el certificado.  
>   - Utilice un valor personalizado en el Nombre alternativo del sujeto (SAN) del certificado para ayudar a distinguir este certificado de los certificados de servidor web estándar que utiliza con IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de servidor web personalizado en la entidad de certificación  

1.  Cree un grupo de seguridad denominado **Servidores de sitio de Configuration Manager** que tenga los servidores miembros para instalar los servidores de sitio primario de Configuration Manager que administrarán los puntos de distribución basados en la nube.  

2.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y, después, pulse **Administrar** para cargar la consola de administración de las plantillas de certificado.  

3.  En el panel de resultados, haga clic con el botón derecho en la entrada que tiene **Servidor web** en la columna **Nombre para mostrar de plantilla** y, después, pulse **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla**, asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, después, pulse **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba un nombre de la plantilla, como **Certificado de puntos de distribución basados en la nube de Configuration Manager**, para generar el certificado de servidor web para puntos de distribución basados en la nube.  

6.  Pulse la pestaña **Control de solicitudes** y, después, seleccione **Permitir que la clave privada se pueda exportar**.  

7.  Pulse la pestaña **Seguridad** y, después, elimine el permiso **Inscribir** del grupo de seguridad **Administradores de empresa**.  

8.  Pulse **Agregar**, escriba **Servidores de sitio de Configuration Manager** en el cuadro de texto y, después, seleccione **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

10. Elija la pestaña **Criptografía** y asegúrese de que **Tamaño mínimo de clave** se haya establecido en **2048**.

11. Pulse **Aceptar** y, después, cierre la **Consola de plantillas de certificado**.  

12. En la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado**, pulse **Nueva** y, después, en **Plantilla de certificado que se va a emitir**.  

13. En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Certificado de puntos de distribución basados en la nube de Configuration Manager** y, después, pulse **Aceptar**.  

14. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Solicitar el certificado de servidor web personalizado  
 Este procedimiento solicita y, después, instala el certificado de servidor web personalizado en el servidor miembro que ejecutará el servidor de sitio.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Para solicitar el certificado de servidor web personalizado  

1.  Reinicie el servidor miembro después de crear y configurar el grupo de seguridad **Servidores de sitio de Configuration Manager** para asegurarse de que el equipo puede acceder a la plantilla de certificado que ha creado, mediante los permisos de **lectura** e **Inscribir** que ha configurado.  

2.  Pulse **Inicio**, **Ejecutar** y, después, escriba **mmc.exe**. En la consola vacía, pulse **Archivo** y, después, pulse **Agregar o quitar complemento**.  

3.  En el cuadro de diálogo **Agregar o quitar complementos**, seleccione **Certificados** en la lista de **Complementos disponibles** y, después, pulse **Agregar**.  

4.  En el cuadro de diálogo **Complemento de certificado**, seleccione **Cuenta de equipo** y, después, pulse **Siguiente**.  

5.  En el cuadro de diálogo **Seleccionar equipo**, asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, después, pulse **Finalizar**.  

6.  En el cuadro de diálogo **Agregar o quitar complementos**, pulse **Aceptar**.  

7.  En la consola, expanda **Certificados (equipo local)** y, después, pulse **Personal**.  

8.  Haga clic con el botón derecho en **Certificados**, pulse **Todas las tareas** y, después, pulse **Solicitar un nuevo certificado**.  

9. En la página **Antes de comenzar**, seleccione **Siguiente**.  

10. Si ve la página **Seleccionar directiva de inscripción de certificados**, pulse **Siguiente**.  

11. En la página **Solicitar certificados**, identifique el **Certificado de puntos de distribución basados en la nube de Configuration Manager** en la lista de certificados disponibles y, después, pulse **Se necesita más información para inscribir este certificado. Pulse aquí para configurar los valores**.  

12. En el cuadro de diálogo **Propiedades de certificado**, en la pestaña **Sujeto**, para el **Nombre de sujeto**, seleccione **Nombre común** como el **Tipo**.  

13. En el cuadro **Valor** , especifique el nombre de servicio que desee y su nombre de dominio con un formato FQDN. Por ejemplo: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Cree un nombre de servicio que sea único en su espacio de nombres. Utilizará DNS para crear un alias (registro CNAME) para asignar este nombre de servicio a un identificador generado automáticamente (GUID) y una dirección IP de Windows Azure.  

14. Pulse **Agregar** y, después, pulse **Aceptar** para cerrar el cuadro de diálogo **Propiedades de certificado**.  

15. En la página **Solicitar certificados**, seleccione el **Certificado de puntos de distribución basados en la nube de Configuration Manager** en la lista de certificados disponibles y, después, pulse **Inscribir**.  

16. En la página **Resultados de la instalación de certificados**, espere hasta que se instale el certificado y, después, pulse **Finalizar**.  

17. Cierre **Certificados (equipo local)** .  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Exportar el certificado de servidor web personalizado para puntos de distribución basados en la nube  
 Este procedimiento permite exportar el certificado de servidor web personalizado a un archivo, de modo que se pueda importar al crear el punto de distribución basado en la nube.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Para exportar el certificado de servidor web personalizado para puntos de distribución basados en la nube  

1. En la consola **Certificados (equipo local)** , haga clic con el botón derecho en el certificado que acaba de instalar, seleccione **Todas las tareas** y, después, pulse **Exportar**.  

2. En el Asistente para exportación de certificados, pulse **Siguiente**.  

3. En la página **Exportar la clave privada**, seleccione **Exportar la clave privada** y, después, pulse **Siguiente**.  

   > [!NOTE]  
   >  Si esta opción no está disponible, significa que el certificado se creó sin la opción de exportar la clave privada. En este escenario, no se puede exportar el certificado en el formato requerido. Debe configurar la plantilla de certificado para que permita la exportación de la clave privada y, después, solicitar el certificado de nuevo.  

4. En la página **Formato de archivo de exportación**, asegúrese de que está seleccionada la opción **Intercambio de información personal: PKCS #12 (.PFX)** .  

5. En la página **Contraseña**, especifique una contraseña segura para proteger el certificado exportado con su clave privada y, después, pulse **Siguiente**.  

6. En la página **Archivo para exportar**, especifique el nombre del archivo que quiere exportar y, después, pulse **Siguiente**.  

7. Para cerrar el Asistente, pulse **Finalizar** en la página **Asistente para exportación de certificados** y, después, pulse **Aceptar** en el cuadro de diálogo de confirmación.  

8. Cierre **Certificados (equipo local)** .  

9. Almacene el archivo de forma segura y asegúrese de que puede acceder a él desde la consola de Configuration Manager.  

   El certificado ya está listo para importarse al crear un punto de distribución basado en la nube.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Implementación del certificado de cliente para equipos Windows  
 Esta implementación de certificado consta de los siguientes procedimientos:  

- Crear y emitir la plantilla de certificado de autenticación de estación de trabajo en la entidad de certificación  

- Configurar la inscripción automática de la plantilla de autenticación de estación de trabajo mediante una directiva de grupo  

- Inscribir automáticamente el certificado de autenticación de estación de trabajo y comprobar su instalación en equipos  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Crear y emitir la plantilla de certificado de autenticación de estación de trabajo en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado para los equipos cliente de Configuration Manager y se agrega a la entidad de certificación.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de autenticación de estación de trabajo en la entidad de certificación  

1.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y, después, pulse **Administrar** para cargar la consola de administración de las plantillas de certificado.  

2.  En el panel de resultados, haga clic con el botón derecho en la entrada que tiene **Autenticación de estación de trabajo** en la columna **Nombre para mostrar de plantilla** y, después, pulse **Duplicar plantilla**.  

3.  En el cuadro de diálogo **Duplicar plantilla**, asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, después, pulse **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

4.  En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba el nombre de la plantilla, como **Certificado de cliente de Configuration Manager**, para generar los certificados de cliente que se usarán en los equipos cliente de Configuration Manager.  

5.  Pulse la pestaña **Seguridad**, seleccione el grupo **Equipos del dominio** y, después, seleccione los permisos adicionales de **lectura** e **Inscripción automática**. No desactive **Inscribir**.  

6.  Pulse **Aceptar** y, después, cierre la **Consola de plantillas de certificado**.  

7.  En la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado**, pulse **Nueva** y, después, en **Plantilla de certificado que se va a emitir**.  

8.  En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Certificado de cliente de Configuration Manager** y, después, pulse **Aceptar**.  

9. Si no necesita crear y emitir más certificados, cierre la **Entidad de certificación**.  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Configurar la inscripción automática de la plantilla de autenticación de estación de trabajo mediante una directiva de grupo  
 Este procedimiento configura una directiva de grupo para la inscripción automática del certificado de cliente en los equipos.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Para configurar la inscripción automática de la plantilla de autenticación de estación de trabajo mediante una directiva de grupo  

1.  En el controlador de dominio, pulse **Inicio**, pulse **Herramientas administrativas** y, después, **Administración de directivas de grupo**.  

2.  Vaya a su dominio, haga clic con el botón derecho en el dominio y, después, seleccione **Crear un GPO en este dominio y vincularlo aquí**.  

    > [!NOTE]  
    >  En este paso se utiliza el procedimiento recomendado de crear una nueva directiva de grupo para la configuración personalizada en lugar de modificar la directiva predeterminada de dominios que se instala con Servicios de dominio de Active Directory. Cuando asigna esta directiva de grupo a nivel de dominio, la aplicará a todos los equipos del dominio. En un entorno de producción, puede restringir la inscripción automática de manera que se inscriba solo en equipos seleccionados. Puede asignar la directiva de grupo en un nivel de unidad organizativa, o puede filtrar la directiva de grupo de dominio con un grupo de seguridad de manera que se aplique solo a los equipos del grupo. Si restringe la inscripción automática, no olvide incluir el servidor que está configurado como el punto de administración.  

3.  En el cuadro de diálogo **Nuevo GPO**, escriba un nombre para la directiva de grupo nueva, como **Certificados de inscripción automática** y, después, pulse **Aceptar**.  

4.  En el panel de resultados, en la pestaña **Objetos de directiva de grupo vinculados**, haga clic con el botón derecho en la directiva de grupo nueva y, después, pulse **Editar**.  

5.  En el cuadro de diálogo **Editor de administración de directivas de grupo**, expanda **Directivas** bajo **Configuración del equipo** y, después, vaya a **Configuración de Windows** / **Configuración de seguridad** / **Directivas de clave pública**.  

6.  Haga clic con el botón derecho en el tipo de objeto denominado **Cliente de Servicios de servidor de certificados - Inscripción automática** y, después, pulse **Propiedades**.  

7.  En la lista desplegable **Modelo de configuración**, seleccione **Habilitado**, seleccione **Renovar certificados expirados, actualizar certificados pendientes y quitar certificados revocados**, seleccione **Actualizar certificados que usan plantillas de certificado** y, después, pulse **Aceptar**.  

8.  Cierre **Administración de directivas de grupo**.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Inscribir automáticamente el certificado de autenticación de estación de trabajo y comprobar su instalación en equipos  
 Este procedimiento instala el certificado de cliente en los equipos y comprueba la instalación.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Para inscribir automáticamente el certificado de autenticación de estación de trabajo y comprobar su instalación en el equipo cliente  

1. Reinicie el equipo de estación de trabajo, y espere unos minutos antes de iniciar sesión.  

   > [!NOTE]  
   >  Reiniciar un equipo es el método más fiable para realizar correctamente la inscripción automática de certificados.  

2. Inicie sesión con una cuenta que tenga privilegios administrativos.  

3. En el cuadro de búsqueda, escriba **mmc.exe.** y, después, presione **Entrar**.  

4. En la consola de administración vacía, pulse **Archivo** y, después, pulse **Agregar o quitar complemento**.  

5. En el cuadro de diálogo **Agregar o quitar complementos**, seleccione **Certificados** en la lista de **Complementos disponibles** y, después, pulse **Agregar**.  

6. En el cuadro de diálogo **Complemento de certificado**, seleccione **Cuenta de equipo** y, después, pulse **Siguiente**.  

7. En el cuadro de diálogo **Seleccionar equipo**, asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, después, pulse **Finalizar**.  

8. En el cuadro de diálogo **Agregar o quitar complementos**, pulse **Aceptar**.  

9. En la consola, expanda **Certificados (equipo local)** , expanda **Personal** y, después, pulse **Certificados**.  

10. En el panel de resultados, confirme que un certificado tiene **Autenticación de cliente** en la columna **Propósito planteado**, y que aparece **Certificado de cliente de Configuration Manager** en la columna **Plantilla de certificado**.  

11. Cierre **Certificados (equipo local)** .  

12. Repita los pasos del 1 al 11 para el servidor miembro para comprobar que el servidor que se va a configurar como punto de administración también tiene un certificado de cliente.  

    El equipo está configurado ahora con un certificado cliente de Configuration Manager.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Implementación del certificado de cliente para puntos de distribución  

> [!NOTE]  
>  Este certificado también se puede utilizar para imágenes de medios que no utilicen el arranque PXE porque los requisitos del certificado son los mismos.  

 Esta implementación de certificado consta de los siguientes procedimientos:  

- Crear y emitir una plantilla de certificado de autenticación de estación de trabajo personalizada en la entidad de certificación  

- Solicitar el certificado de autenticación de estación de trabajo personalizado  

- Exportar el certificado de cliente para puntos de distribución  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Crear y emitir una plantilla de certificado de autenticación de estación de trabajo personalizada en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado personalizada para puntos de distribución de Configuration Manager de manera que la clave privada pueda exportarse, y se agrega la plantilla de certificado a la entidad de certificación.  

> [!NOTE]
>  Este procedimiento usa una plantilla de certificado diferente a la plantilla de certificado que ha creado para los equipos cliente. Aunque ambos certificados necesitan la capacidad de autenticación de cliente, el certificado de puntos de distribución necesita que la clave privada se exporte. Como procedimiento recomendado de seguridad, no configure plantillas de certificado que permitan la exportación de la clave privada a menos que se requiera esta configuración. El punto de distribución requiere esta configuración porque debe importar el certificado como un archivo, en lugar de seleccionarlo en el almacén de certificados.  
> 
>  Cuando crea una nueva plantilla de certificado para este certificado, puede restringir los equipos que pueden solicitar un certificado cuya clave privada puede exportarse. En nuestra implementación de ejemplo, este es el grupo de seguridad que creó anteriormente para los servidores de sistema de sitio de Configuration Manager que ejecutan IIS. En una red de producción que distribuye los roles del sistema de sitio de IIS, considere la creación de un grupo de seguridad nuevo para los servidores que ejecuten puntos de distribución; así, podrá restringir el certificado específicamente a estos servidores de sistema de sitio. También podría agregar las siguientes modificaciones para este certificado:  
> 
> - Solicitar aprobación para instalar el certificado, para mayor seguridad.  
>   - Incrementar el periodo de validez del certificado. Como debe exportar e importar el certificado siempre antes de que expire, al incrementar el período de validez se reduce la frecuencia con la que debe repetir este procedimiento. En cambio, al incrementar el periodo de validez también se reduce la seguridad del certificado porque un atacante tendría más tiempo para descifrar la clave privada y robar el certificado.  
>   - Utilice un valor personalizado en el campo Sujeto del certificado, o el nombre alternativo del sujeto (SAN, por sus siglas en inglés) para facilitar la identificación de este certificado entre los certificados de cliente estándar. Esto puede resultar especialmente útil si va a utilizar el mismo certificado para varios puntos de distribución.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de autenticación de estación de trabajo personalizada en la entidad de certificación  

1.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y, después, pulse **Administrar** para cargar la consola de administración de las plantillas de certificado.  

2.  En el panel de resultados, haga clic con el botón derecho en la entrada que tiene **Autenticación de estación de trabajo** en la columna **Nombre para mostrar de plantilla** y, después, pulse **Duplicar plantilla**.  

3.  En el cuadro de diálogo **Duplicar plantilla**, asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, después, pulse **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

4.  En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba un nombre para la plantilla, como **Certificado de punto de distribución de cliente de Configuration Manager**, para generar el certificado de autenticación de cliente para puntos de distribución.  

5.  Pulse la pestaña **Control de solicitudes** y, después, seleccione **Permitir que la clave privada se pueda exportar**.  

6.  Pulse la pestaña **Seguridad** y, después, elimine el permiso **Inscribir** del grupo de seguridad **Administradores de empresa**.  

7.  Pulse **Agregar**, escriba **Servidores IIS de Configuration Manager** en el cuadro de texto y, después, pulse **Aceptar**.  

8.  Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

9. Pulse **Aceptar** y, después, cierre la **Consola de plantillas de certificado**.  

10. En la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado**, pulse **Nueva** y, después, en **Plantilla de certificado que se va a emitir**.  

11. En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Certificado de punto de distribución de cliente de Configuration Manager** y, después, pulse **Aceptar**.  

12. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Solicitar el certificado de autenticación de estación de trabajo personalizado  
 Este procedimiento solicita y, después, instala el certificado de cliente personalizado en el servidor miembro que ejecuta IIS y que se configurará como punto de distribución.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Para solicitar el certificado de autenticación de estación de trabajo personalizado  

1.  Pulse **Inicio**, **Ejecutar** y, después, escriba **mmc.exe**. En la consola vacía, pulse **Archivo** y, después, pulse **Agregar o quitar complemento**.  

2.  En el cuadro de diálogo **Agregar o quitar complementos**, seleccione **Certificados** en la lista de **Complementos disponibles** y, después, pulse **Agregar**.  

3.  En el cuadro de diálogo **Complemento de certificado**, seleccione **Cuenta de equipo** y, después, pulse **Siguiente**.  

4.  En el cuadro de diálogo **Seleccionar equipo**, asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, después, pulse **Finalizar**.  

5.  En el cuadro de diálogo **Agregar o quitar complementos**, pulse **Aceptar**.  

6.  En la consola, expanda **Certificados (equipo local)** y, después, pulse **Personal**.  

7.  Haga clic con el botón derecho en **Certificados**, pulse **Todas las tareas** y, después, pulse **Solicitar un nuevo certificado**.  

8.  En la página **Antes de comenzar**, seleccione **Siguiente**.  

9. Si ve la página **Seleccionar directiva de inscripción de certificados**, pulse **Siguiente**.  

10. En la página **Solicitar certificados**, seleccione el **Certificado de punto de distribución de cliente de Configuration Manager** en la lista de certificados disponibles y, después, pulse **Inscribir**.  

11. En la página **Resultados de la instalación de certificados**, espere hasta que se instale el certificado y, después, pulse **Finalizar**.  

12. En el panel de resultados, confirme que un certificado tiene **Autenticación de cliente** en la columna **Propósito planteado**, y que aparece **Certificado de punto de distribución de cliente de Configuration Manager** en la columna **Plantilla de certificado**.  

13. No cierre **Certificados (equipo local)** .  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Exportar el certificado de cliente para puntos de distribución  
 Este procedimiento exporta el certificado de autenticación de estación de trabajo personalizado a un archivo para que se pueda importar en las propiedades del punto de distribución.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Para exportar el certificado de cliente para puntos de distribución  

1. En la consola **Certificados (equipo local)** , haga clic con el botón derecho en el certificado que acaba de instalar, seleccione **Todas las tareas** y, después, pulse **Exportar**.  

2. En el Asistente para exportación de certificados, pulse **Siguiente**.  

3. En la página **Exportar la clave privada**, seleccione **Exportar la clave privada** y, después, pulse **Siguiente**.  

   > [!NOTE]  
   >  Si esta opción no está disponible, significa que el certificado se creó sin la opción de exportar la clave privada. En este escenario, no se puede exportar el certificado en el formato requerido. Debe configurar la plantilla de certificado para que permita la exportación de la clave privada y, después, solicitar el certificado de nuevo.  

4. En la página **Formato de archivo de exportación**, asegúrese de que está seleccionada la opción **Intercambio de información personal: PKCS #12 (.PFX)** .  

5. En la página **Contraseña**, especifique una contraseña segura para proteger el certificado exportado con su clave privada y, después, pulse **Siguiente**.  

6. En la página **Archivo para exportar**, especifique el nombre del archivo que quiere exportar y, después, pulse **Siguiente**.  

7. Para cerrar el Asistente, pulse **Finalizar** en la página **Asistente para exportación de certificados** y pulse **Aceptar** en el cuadro de diálogo de confirmación.  

8. Cierre **Certificados (equipo local)** .  

9. Almacene el archivo de forma segura y asegúrese de que puede acceder a él desde la consola de Configuration Manager.  

   El certificado está ahora preparado para su importación cuando configure el punto de distribución.  

> [!TIP]  
>  Puede usar el mismo archivo de certificado cuando configure imágenes de medios para una implementación de sistema operativo que no use arranque PXE, y cuya secuencia de tareas de instalación de imagen deba ponerse en contacto con un punto de administración que requiera conexiones de cliente HTTPS.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Implementación del certificado de inscripción para dispositivos móviles  
 Esta implementación de certificado consta de un único procedimiento para crear y emitir la plantilla de certificado de inscripción en la entidad de certificación.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Crear y emitir la plantilla de certificado de inscripción en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado de inscripción para dispositivos móviles de Configuration Manager y se agrega a la entidad de certificación.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de inscripción en la entidad de certificación  

1. Cree un grupo de seguridad que tenga usuarios que vayan a inscribir dispositivos móviles en Configuration Manager.  

2. En el servidor miembro que tenga Servicios de servidor de certificados instalados, en la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y, después, pulse **Administrar** para cargar la consola de administración de las plantillas de certificado.  

3. En el panel de resultados, haga clic con el botón derecho en la entrada que tiene **Sesión autenticada** en la columna **Nombre para mostrar de plantilla** y, después, pulse **Duplicar plantilla**.  

4. En el cuadro de diálogo **Duplicar plantilla**, asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, después, pulse **Aceptar**.  

   > [!IMPORTANT]  
   >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5. En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba el nombre de la plantilla, por ejemplo, **Certificado de inscripción de dispositivos móviles de Configuration Manager**, para generar los certificados de inscripción para los dispositivos móviles que se administrarán en Configuration Manager.  

6. Pulse la pestaña **Nombre de sujeto**, asegúrese de que está seleccionado **Construido a partir de esta información de Active Directory**, seleccione **Nombre común** para el **Formato de nombre de sujeto** y, después, desactive **Nombre principal del usuario (UPN)** en **Incluir esta información en un nombre de sujeto alternativo**.  

7. Pulse la pestaña **Seguridad**, seleccione el grupo de seguridad que tiene usuarios que van a inscribir dispositivos móviles y, después, seleccione el permiso adicional de **Inscribir**. No desactive **Leer**.  

8. Pulse **Aceptar** y, después, cierre la **Consola de plantillas de certificado**.  

9. En la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado**, pulse **Nueva** y, después, en **Plantilla de certificado que se va a emitir**.  

10. En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Certificado de inscripción de dispositivos móviles de Configuration Manager** y, después, pulse **Aceptar**.  

11. Si no necesita crear y emitir más certificados, cierre la consola de entidad de certificación.  

    La plantilla de certificado de inscripción de dispositivos móviles se podrá seleccionar ahora cuando configure un perfil de inscripción de dispositivo móvil en la configuración de cliente.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Implementación del certificado de cliente para equipos Mac  

Esta implementación de certificado consta de un único procedimiento para crear y emitir la plantilla de certificado de inscripción en la entidad de certificación.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Crear y emitir una plantilla de certificado de cliente Mac en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado personalizada para los equipos Mac de Configuration Manager y se agrega la plantilla de certificado a la entidad de certificación.  

> [!NOTE]  
>  Este procedimiento utiliza una plantilla de certificado diferente de la plantilla de certificado que podría haber creado para los equipos cliente Windows o para puntos de distribución.  
>   
>  Cuando crea una nueva plantilla de certificado para este certificado, puede restringir la solicitud de certificado a los usuarios autorizados.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de cliente Mac en la entidad de certificación  

1. Cree un grupo de seguridad que tenga cuentas de usuario para los usuarios administrativos que vayan a inscribir el certificado en el equipo Mac mediante Configuration Manager.  

2. En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado** y, después, pulse **Administrar** para cargar la consola de administración de las plantillas de certificado.  

3. En el panel de resultados, haga clic con el botón derecho en la entrada que muestra **Sesión autenticada** en la columna **Nombre para mostrar de plantilla** y, después, pulse **Duplicar plantilla**.  

4. En el cuadro de diálogo **Duplicar plantilla**, asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, después, pulse **Aceptar**.  

   > [!IMPORTANT]  
   >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5. En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba el nombre de la plantilla, como **Certificado de cliente Mac de Configuration Manager**, para generar el certificado de cliente Mac.  

6. Pulse la pestaña **Nombre de sujeto**, asegúrese de que está seleccionado **Construido a partir de esta información de Active Directory**, seleccione **Nombre común** para el **Formato de nombre de sujeto** y, después, desactive **Nombre principal del usuario (UPN)** en **Incluir esta información en un nombre de sujeto alternativo**.  

7. Pulse la pestaña **Seguridad** y, después, elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de empresa**.  

8. Pulse **Agregar**, especifique el grupo de seguridad que ha creado en el paso uno y, después, pulse **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso de **lectura**.  

10. Pulse **Aceptar** y, después, cierre la **Consola de plantillas de certificado**.  

11. En la consola de entidad de certificación, haga clic con el botón derecho en **Plantillas de certificado**, pulse **Nueva** y, después, en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados**, seleccione la nueva plantilla que acaba de crear, **Certificado de cliente Mac de Configuration Manager** y, después, pulse **Aceptar**.  

13. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

    La plantilla de certificado de cliente Mac ya está lista para seleccionarse al configurar las opciones del cliente para la inscripción.