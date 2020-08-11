---
title: Tutorial&#58; Habilitación de la administración conjunta para dispositivos de Internet
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar la administración conjunta para nuevos dispositivos Windows 10 basados en Internet con Configuration Manager y Microsoft Intune.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 742cd1e86ac0bff6563c0d3ee4edce7324629480
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/05/2020
ms.locfileid: "87815470"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Tutorial: Habilitación de la administración conjunta para nuevos dispositivos basados en Internet

Con la administración conjunta, puede mantener sus procesos estandarizados para el uso de Configuration Manager para administrar los equipos de su organización. Al mismo tiempo, está invirtiendo en la nube mediante el uso de Intune para la seguridad y el aprovisionamiento moderno.

En este tutorial, configura la administración conjunta de dispositivos Windows 10 en un entorno en el que utiliza tanto Azure Active Directory (AD) como un AD local, pero no tiene una instancia [híbrida de Azure Active Directory ](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD). El entorno de Configuration Manager incluye un único sitio principal con todos los roles de sistema de sitio ubicados en el mismo servidor: el servidor de sitio. Este tutorial comienza con la premisa de que sus dispositivos Windows 10 ya están inscritos en Intune. 

Si tiene una instancia híbrida de Azure AD que se une a su AD local con Azure AD, se recomienda seguir nuestro tutorial complementario [Habilitar la administración conjunta para los clientes existentes de Configuration Manager](tutorial-co-manage-clients.md).

Use este tutorial cuando:
  
- Tiene dispositivos Windows 10 en los que desea aplicar la administración conjunta. Estos dispositivos podrían haberse aprovisionado mediante Windows Autopilot o proceder directamente de su OEM de hardware.
- Tiene dispositivos Windows 10 en Internet que administra actualmente con Intune a los que desea agregar el cliente de Configuration Manager.

**En este tutorial aprenderá a:**  
> [!div class="checklist"]  
> * Revisar los requisitos previos para su entorno local y Azure
> * Solicitar un certificado público de SSL para Cloud Management Gateway (CMG)
> * Habilitar servicios de Azure en Configuration Manager
> * Implementar y configurar una instancia de Cloud Management Gateway  
> * Configurar el punto de administración y los clientes para usar CMG
> * Habilitar la administración conjunta en Configuration Manager
> * Configurar Intune para instalar el cliente de Configuration Manager

## <a name="prerequisites"></a>Requisitos previos  

### <a name="azure-services-and-environment"></a>Entorno y servicios de Azure

- Suscripción de Azure ([evaluación gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Suscripción a Microsoft Intune
  > [!TIP]  
  > Una suscripción a Enterprise Mobility + Security (EMS) incluye Azure Active Directory Premium y Microsoft Intune. Una suscripción a EMS ([evaluación gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Intune está configurado para [la inscripción automática de dispositivos](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune).  

> [!TIP]
> Ya no es necesario comprar ni asignar licencias individuales de Intune o EMS a los usuarios. Para más información, vea [Preguntas más frecuentes sobre productos y licencias](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Infraestructura local

- Rama actual de Configuration Manager, versión 1810 o posterior.
  
  La versión 1810 introduce [HTTP mejorado](../core/plan-design/hierarchy/enhanced-http.md), que se usa en este tutorial para evitar requisitos de PKI más complejos. Mediante el uso de HTTP mejorado, el sitio primario que se usa para administrar los clientes debe configurarse para usar los certificados generados por Configuration Manager para sistemas de sitio HTTP.  

  La versión 1810 también introduce una línea de comandos más sencilla para la instalación basada en Internet del cliente de Configuration Manager.

- La autoridad de MDM debe estar configurada en Intune.  

### <a name="external-certificates"></a>Certificados externos

- certificado de autenticación de servidor CMG. Este certificado es un certificado SSL de un proveedor de certificados público y de confianza global. Por ejemplo, DigiCert, VeriSign o Thawte, entre otros. Exportará este certificado como un archivo .PFX con una clave privada.  

- Más adelante en este tutorial se proporcionan instrucciones sobre cómo configurar la solicitud para este certificado.

### <a name="permissions"></a>Permisos

A lo largo de este tutorial, use los siguientes permisos para completar las tareas:

- Una cuenta de *administrador global* de Azure Active Directory (Azure AD).
- Una cuenta que sea un *administrador de dominio* en su infraestructura local  
- Una cuenta que sea un *administrador total* para *todos* los ámbitos en Configuration Manager

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Solicitud de un certificado público para Cloud Management Gateway

Cuando los dispositivos están en Internet, la administración conjunta requiere Cloud Management Gateway (CMG) de Configuration Manager. La instancia de CMG permite a los dispositivos Windows 10 basados en Internet comunicarse con su implementación local de Configuration Manager. Para establecer una relación de confianza entre los dispositivos y su entorno de Configuration Manager, la instancia de CMG requiere un certificado SSL.

Este tutorial usa un certificado público denominado **certificado de autenticación de servidor CMG** que deriva de la autoridad de un proveedor de certificados de confianza global. Aunque es posible configurar la administración conjunta utilizando certificados que derivan de la autoridad de su entidad de certificación local de Microsoft, el uso de certificados autofirmados queda fuera del ámbito de este tutorial.

El **certificado de autenticación de servidor CMG** se utiliza para cifrar el tráfico de las comunicaciones entre el cliente de Configuration Manager y CMG. El certificado se remonta a una raíz de confianza para verificar la identidad del servidor con el cliente. El certificado público incluye una raíz de confianza en la que ya confían los clientes de Windows.

Acerca de este certificado: 

- Identifica un nombre único para el servicio CMG en Azure y, a continuación, especifica el nombre en la solicitud de certificado.  
- Genera la solicitud de certificado en un servidor específico y, a continuación, envía la solicitud a un proveedor de certificados público para obtener el certificado SSL necesario.  
- Importa en el sistema que generó la solicitud el certificado que reciba del proveedor. Usa el mismo equipo para exportar el certificado para su uso al implementar más adelante la instancia de CMG en Azure.  
- Cuando se instala la instancia de CMG, crea un servicio CMG en Azure con el nombre especificado en el certificado.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identificación de un nombre único para la instancia de Cloud Management Gateway en Azure

Cuando solicita el certificado de autenticación de servidor de CMG, especifica un nombre que debe ser único para identificar su *servicio en la nube (clásico)* en Azure. De forma predeterminada, la nube pública de Azure usa *cloudapp.net*, y la instancia de CMG se hospeda dentro del dominio cloudapp.net como *\<YourUniqueDnsName>.cloudapp.net*.  

> [!TIP]  
> En este tutorial, el **certificado de autenticación de servidor CMG** utiliza un FQDN que termina en *contoso.com*.  Después de crear la instancia de CMG, vamos a configurar un registro de nombre canónico (CNAME) en el DNS público de nuestra organización. Este registro crea un alias para la instancia de CMG que se asigna al nombre que usamos en el certificado público.  

Antes de solicitar el certificado público, confirme que el nombre que desea utilizar está disponible en Azure. No crea directamente el servicio en Azure. En su lugar, el nombre que se especifica en el certificado público de la solicitud se usa por Configuration Manager para crear el servicio en la nube cuando se instala la instancia de CMG.  

1. Inicie sesión en [Microsoft Azure Portal](https://portal.azure.com/).  

2. Seleccione **Crear un recurso**, elija la categoría **Proceso** y seleccione **Servicio en la nube**. Se abre la página del servicio en la nube (clásico).

3. Para **Nombre DNS**, especifique el nombre de prefijo para el servicio en la nube que usará. Este prefijo debe ser igual que el que usará más adelante cuando solicite un certificado de publicación para el certificado de autenticación de servidor de CMG. Usamos *MyCSG*, que crea el espacio de nombres *MyCSG.cloudapp.net*. La interfaz confirma si el nombre está disponible o si ya está en uso por otro servicio.  
 Después de confirmar el nombre que desea utilizar está disponible, está listo para enviar la solicitud de firma de certificado (CSR).

### <a name="request-the-certificate"></a>Solicitud del certificado

Use la siguiente información para enviar una solicitud de firma de certificado para su CMG a un proveedor de certificados públicos. Cambie los valores siguientes para que sea pertinente para su entorno.  

- *MyCMG* para identificar el nombre del servicio de Cloud Management Gateway
- *Contoso* como nombre de la empresa
- *Contoso.com* como dominio público

Se recomienda usar el servidor de sitio primario para generar las solicitudes de firma de certificado. Cuando reciba el certificado, debe inscribirlo en el mismo servidor que generó el CSR o no podrá exportar la clave privada de certificados, que es necesaria.  

Solicite un tipo de proveedor de claves de la versión 2 al generar un CSR. Se admiten solo los certificados de la versión 2.  

> [!TIP]  
> Cuando se implementa la instancia de CMG, también se instalará un punto de distribución de nube (CDP) al mismo tiempo. De manera predeterminada, al implementar una instancia de CMG, la opción **Permitir que CMG funcione como un punto de distribución en la nube y sirva contenido desde el almacenamiento de Azure** está activa. La ubicación conjunta del CDP en el servidor con el CMG elimina la necesidad de que los certificados y configuraciones sean independientes para admitir el CDP. Aunque el CDP no es necesario para usar la administración conjunta, es útil en la mayoría de los entornos.  
>
> Si usa cualquier CDP independiente adicional, debe solicitar certificados independientes para cada CDP adicional. Para solicitar un certificado púbico para un CDP, use los mismos detalles que para la CSR de Cloud Management Gateway. Solo necesita cambiar el nombre común para que sea único para cada CDP.
>
> El uso de un CDP independiente adicional está en desuso y ya no se recomienda. Para más información, vea [Deprecated Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features) (Características en desuso).

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Detalles para la CSR de Cloud Management Gateway

- **Nombre común**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Ejemplo: MyCSG.contoso.com  
- **Nombre alternativo del firmante**: igual que el nombre común (CN)  
- **Organización**:  el nombre de su organización  
- **Departamento**: de acuerdo con su organización  
- **Ciudad**: de acuerdo con su organización  
- **Estado**: de acuerdo con su organización  
- **País**: de acuerdo con su organización  
- **Tamaño de la clave: 2048**  
- **Proveedor: proveedor de servicios criptográficos de Microsoft RSA SChannel**  

### <a name="import-the-certificate"></a>Importación del certificado

Después de recibir el certificado público, impórtelo en el almacén de certificados local del equipo que creó la CSR. A continuación, exporte el certificado como un archivo .PFX para poder usarlo para su CMG en Azure.  

Los proveedores de certificados públicos normalmente proporcionan instrucciones para la importación del certificado. El proceso para importar el certificado debe ser similar al siguiente:  

1. En el equipo en el que se va a importar el certificado, busque el archivo .pfx del certificado.  

2. Haga clic con el botón derecho en el archivo y, después, seleccione **Instalar PFX**.  

3. Cuando se inicia el Asistente para importación de certificados, seleccione **Siguiente**.  

4. En la página **Archivo para importar**, seleccione **Siguiente**.

5. En la página **Contraseña**, escriba la contraseña de la clave privada en el cuadro Contraseña y, a continuación, seleccione **Siguiente**.  
  
   Seleccione la opción de hacer exportable la clave.

6. En la **página Almacén de certificados**, elija **Seleccionar automáticamente el almacén de certificados en base al tipo de certificado** y, a continuación, seleccione **Siguiente**.  

7. Seleccione **Finalizar**.

### <a name="export-the-certificate"></a>Exportación del certificado

Exporte el *certificado de autenticación de servidor de CMG* del servidor. La reexportación del certificado lo hace utilizable para su instancia de Cloud Management Gateway en Azure.  

1. En el servidor donde se ha importado el certificado público de SSL, ejecute **certlm.msc** para abrir la consola del administrador de certificados.  

2. En la consola del administrador de certificados, seleccione **Personal > Certificados**. A continuación, haga clic con el botón derecho en el *certificado de autenticación del servidor de CMG* inscrito en el procedimiento anterior y, a continuación, seleccione **Todas las tareas > Exportar**.  

3. En el Asistente para exportar certificado, seleccione **Siguiente**, **Exportar la clave privada** y **Siguiente**.  

4. En la página Formato de archivo de exportación, seleccione **Intercambio de información Personal: PKCS #12 (.PFX)** , seleccione **Siguiente** y proporcione una contraseña. Para el nombre de archivo, especifique un nombre como **C:\ConfigMgrCloudMGServer**. Deberá hacer referencia a este archivo cuando se crea la instancia de CMG en Azure.  

5. Seleccione **Siguiente** y, a continuación, confirme la configuración siguiente antes de seleccionar **Finalizar** para completar la exportación:  

   - Exportar claves = Sí  
   - Incluir todos los certificados en la ruta de certificación = Sí  
   - Formato de archivo = Intercambio de información personal (*.pfx)  

6. Después de completar la exportación, busque el archivo .pfx y coloque una copia en **C:\Certs** en el servidor de sitio primario de Configuration Manager que va a administrar los clientes basados en Internet. La carpeta Certs es una carpeta temporal que se usará al mover los certificados entre los servidores. Accede al archivo de certificado desde el servidor de sitio primario al implementar Cloud Management Gateway en Azure.  

Después de copiar el certificado en el servidor de sitio primario, puede eliminar el certificado del almacén de certificados personal en el servidor miembro.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Habilitación de servicios en la nube en Configuration Manager

Para configurar servicios de Azure desde la consola de Configuration Manager, use el Asistente para configurar servicios de Azure y cree dos aplicaciones de Azure Active Directory (Azure AD).  

- **Aplicación de servidor** : una *aplicación web* en Azure AD  
- **Aplicación cliente** : una aplicación *cliente nativa* en Azure AD  

Ejecute el siguiente procedimiento desde el servidor de sitio primario.  

1. Desde el servidor de sitio primario, abra la consola de Configuration Manager y vaya a **Administración > Cloud Services > Servicios de Azure** y seleccione **Configurar servicios de Azure**.  

   En la página Configurar servicios de Azure, especifique un nombre descriptivo para el servicio de administración en la nube que está configurando. Por ejemplo: *Mi servicio de administración en la nube*.

   A continuación, seleccione **Administración en la nube** y **Siguiente**.  

   > [!TIP]  
   > Para obtener más información acerca de las configuraciones que realiza en el asistente, consulte [Inicio del Asistente para servicios de Azure](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard).

2. En la página **Propiedades de la aplicación**, para **Aplicación web**, seleccione **Examinar** para abrir el cuadro de diálogo **Aplicación de servidor** y, a continuación, seleccione **Crear**. Configure los campos siguientes:

   - **Nombre de aplicación**: Especifique un nombre descriptivo para la aplicación, como *Aplicación web de administración en la nube*.  

   - **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.  

   - **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. Se encuentra en el token de acceso que usa el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.  

   A continuación, seleccione **Iniciar sesión** y especifique una cuenta de administrador global de Azure AD. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure.

   Después de iniciar sesión, se muestran los resultados. Seleccione **Aceptar** para cerrar el cuadro de diálogo Crear aplicación de servidor y volver a la página Propiedades de la aplicación.

3. Para **Aplicación cliente nativa**, seleccione **Examinar** para abrir el cuadro de diálogo **Aplicación cliente**.

4. Seleccione **Crear** para abrir el cuadro de diálogo **Crear aplicación cliente** y, a continuación, configure los siguientes campos:  

   - **Nombre de aplicación**: Especifique un nombre descriptivo para la aplicación, como *Aplicación cliente nativa de administración en la nube*.

   - **Dirección URL de respuesta**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrClient`.
   A continuación, seleccione **Iniciar sesión** y especifique una cuenta de administrador global de Azure AD. Al igual que la aplicación web, estas credenciales no se guardan y no requieren permisos en Configuration Manager.

   Después de iniciar sesión, se muestran los resultados. Seleccione **Aceptar** para cerrar el cuadro de diálogo Crear aplicación cliente y volver a la página Propiedades de la aplicación. Luego, seleccione **Siguiente** para continuar.

5. En la página **Configurar los valores de detección**, active la casilla para **Habilitar la detección de usuarios de Azure Active Directory**, seleccione **Siguiente** y, a continuación, complete la configuración de los cuadros de diálogo de detección para su entorno.  

6. Continúe con las páginas de resumen, progreso y finalización y, a continuación, cierre al asistente.  

   La detección de usuarios de servicios de Azure para Azure AD ahora está habilitada en Configuration Manager.  Deje abierta la consola por ahora.  

7. Abra un explorador e inicie sesión en [Azure Portal](https://portal.azure.com/).  

8. Seleccione **Todos los servicios > Azure Active Directory > Registros de aplicaciones** y, a continuación:

   1. Seleccione la aplicación web que creó.

   2. Vaya a **Permisos de API** > seleccione **Conceder consentimiento de administrador para** <your tenant> y elija **Sí**.  

   3. Seleccione la aplicación cliente nativa que creó.

   4. Vaya a **Permisos de API** > seleccione **Conceder consentimiento de administrador para** <your tenant> y elija **Sí**.

9. En la consola de Configuration Manager, vaya a **Administración > Información general > Cloud Services > Servicios de Azure** y seleccione su servicio de Azure. A continuación, haga doble clic en **Detección de usuarios de Azure Active Directory** y seleccione **Ejecutar detección completa ahora**. Seleccione **Sí** para confirmar la acción.  

10. En el servidor de sitio primario, abra **SMS_AZUREAD_DISCOVERY_AGENT.log** de Configuration Manager y busque la entrada siguiente para confirmar que la detección funciona:  *Successfully published UDX for Azure Active Directory users* (UDX publicado correctamente para los usuarios de Active Directory de Azure)  

    De forma predeterminada, el archivo de registro está en *%Program_Files%\Microsoft Configuration Manager\Logs*.  

## <a name="create-the-cloud-services-in-azure"></a>Creación de los servicios en la nube en Azure

**En esta sección del tutorial, aprenderá a**:

- Crear el servicio en la nube de CMG  
- Crear registros CNAME de DNS para ambos servicios  

### <a name="create-the-cmg"></a>Crear la instancia de CMG

Utilice este procedimiento para instalar una instancia de Cloud Management Gateway en la nube como un servicio en Azure. La instancia de CMG se instala en el sitio de nivel superior de la jerarquía. En este tutorial, seguiremos usando el sitio primario donde se han inscrito y exportado los certificados.

1. En el servidor de sitio primario, abra la consola de Configuration Manager y, a continuación, vaya **Administración > Información general > Cloud Services > Cloud Management Gateway**. Luego, seleccione **Crear instancia de Cloud Management Gateway**.  

2. En la página **General**:  

   1. Seleccione el entorno de nube para el **entorno de Azure**. En este tutorial se usa **AzurePublicCloud**.  

   2. Seleccione **Implementación de Azure Resource Manager**.  
  
   3. **Inicie sesión** en la suscripción a Azure. Configuration Manager rellena la información adicional según la información configurada al habilitar los servicios en la nube de Azure para Configuration Manager.  

   Seleccione **Siguiente** para continuar.  

3. En la página **Configuración**, busque y seleccione el archivo denominado **ConfigMgrCloudMGServer.pfx**, que es el archivo que exportó después de importar el certificado de autenticación de servidor de CMG. Después de especificar la contraseña, el **nombre del servicio** y **nombre de la implementación** se rellenan automáticamente, según los detalles del archivo de certificado .pfx.

4. Configure su **región**.

5. Para **Grupo de recursos**, use un grupo de recursos existente o cree un grupo con un nombre descriptivo sin espacios, como **CofigMgrCloudServices**. Si decide crear un grupo, el grupo se agrega como un grupo de recursos en Azure.  

6. A menos que esté listo para configurar a escala, use uno (1) para el número de **instancias de máquina virtual**. El número de instancias de máquina virtual permite que un único servicio de nube de Cloud Management Gateway (CMG) se escale horizontalmente para admitir más conexiones de cliente. Más adelante, puede usar la consola de Configuration Manager para volver y editar el número de instancias de máquina virtual que use.  

7. Active la casilla **Comprobar revocación de certificado de cliente**.

8. Active la casilla **Permitir a CMG funcionar como un punto de distribución de nube y servir contenido desde Azure Storage** si desea implementar un punto de distribución en la nube con la instancia de CMG.

9. Seleccione **Siguiente** para continuar.

10. Revise los valores de la página **Alerta** y, a continuación, seleccione **Siguiente**.

11. Revise la página **Resumen** y haga clic en **Siguiente** para crear el servicio en la nube de Cloud Management Gateway. Seleccione **Cerrar** para finalizar el asistente.  

12. En el nodo Cloud Management Gateway de la consola de Configuration Manager, ahora puede ver el nuevo servicio.  

### <a name="create-dns-cname-records"></a>Creación de registros CNAME de DNS

Cuando se crea una entrada DNS para la instancia de CMG, habilita los dispositivos Windows 10, tanto dentro como fuera de la red corporativa, para que usen la resolución de nombres a fin de encontrar el servicio en la nube de CMG en Azure.

En nuestro ejemplo de registro CNAME se usan los siguientes detalles:  

- Es el nombre de la compañía es **Contoso** con un espacio de nombres DNS público de ***Contoso.com***.  

- El nombre del servicio de CMG es **MyCMG**, que se convierte en ***MyCMG.CloudApp.Net*** en Azure.  

Ejemplo de registro CNAME: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Configuración del punto de administración y los clientes para usar CMG

Configure opciones que permiten a los clientes y puntos de administración locales usar Cloud Management Gateway.

Como usamos HTTP mejorado para las comunicaciones de cliente, no hay ninguna necesidad de usar un punto de administración de HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Creación del punto de conexión de CMG

Configure el sitio para que admita HTTP mejorado.  

1. En la consola de Configuration Manager, vaya a  **Administración> Información general> Configuración del sitio> Sitios** y abra las propiedades del sitio primario.  

2. En la pestaña **Comunicación de equipo cliente**, seleccione la opción *HTTPS o HTTP* para **Use los certificados generados por Configuration Manager en sistemas de sitios HTTP**, y luego seleccione **Aceptar** para guardar la configuración.

    > [!Note]
    > A partir de la versión 1906, esta pestaña se denomina **Communication Security** (Seguridad de la comunicación).<!-- SCCMDocs#1645 -->  

3. Ahora, vaya a **Administración > Información general > Configuración del sitio > Roles de sistema de sitio y servidores** y seleccione el servidor con un punto de administración donde desea instalar el punto de conexión de la instancia de Cloud Management Gateway.  

4. Seleccione **Agregar roles del sistema de sitio** y, a continuación, **Siguiente**> **Siguiente**.  

5. Seleccione el **Punto de conexión de Cloud Management Gateway** y, a continuación, seleccione **Siguiente** para continuar.  

6. Revise las selecciones predeterminadas en la página **Punto de conexión de Cloud Management Gateway** y asegúrese de que esté seleccionada la instancia de CMG correcta. Si tiene varias instancias de Cloud Management Gateway, puede usar la lista desplegable para especificar una instancia de CMG diferente. También puede cambiar la instancia de CMG en uso, después de la instalación. Seleccione **Siguiente** para continuar.

7. Seleccione **Siguiente** para iniciar la instalación y, a continuación, ver los resultados en la página de finalización.  Seleccione **Cerrar** para completar la instalación del punto de conexión.

8. Ahora, vaya a **Administración > Información general > Configuración del sitio > Roles de sistema de sitio y servidores** y abra las **Propiedades** del punto de administración en el que instaló el punto de conexión. En la pestaña **General**, active la casilla para **Permitir el tráfico de Cloud Management Gateway de Configuration Manager** y, a continuación, seleccione **Aceptar** para guardar la configuración.
   > [!TIP]  
   > Aunque no es necesario para habilitar la administración conjunta, se recomienda que use esta misma edición para los puntos de actualización de software.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Configuración del cliente para dirigir a los clientes al uso de la instancia de CMG

Use la configuración de cliente para configurar los clientes de Configuration Manager para que se comuniquen con la instancia de CMG.  

1. Abra **Consola de Configuration Manager > Administración > Información general > Configuración de cliente** y, luego, edite la **Configuración de cliente predeterminada**.  

2. Seleccione **Cloud Services**.

3. En la página **Configuración predeterminada**, establezca las siguientes opciones en = **Sí**.  

   - **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory**  

   - **Permite que los clientes usen una puerta de enlace de administración en la nube**

   - **Permitir acceso al punto de distribución de nube**

4. En la página **Directiva de cliente**, configure **Habilite solicitudes de directiva de usuario de clientes de Internet** = **Sí**.

5. Haga clic en **Aceptar** para guardar esta configuración.

## <a name="enable-co-management-in-configuration-manager"></a>Habilitación de la administración conjunta en Configuration Manager

Una vez establecidas las configuraciones de Azure, los roles del sistema de sitio y de cliente, puede configurar Configuration Manager para habilitar la administración conjunta. Sin embargo, todavía deberá realizar algunas configuraciones en Intune después de habilitar la administración conjunta antes de completar este tutorial. Una de esas tareas es configurar Intune para implementar el cliente de Configuration Manager. Esa tarea se hace más fácil al guardar la línea de comandos para la implementación del cliente que está disponible dentro del Asistente para la configuración de administración conjunta. Este es el motivo por el cual habilitamos ahora la administración conjunta, antes de completar las configuraciones para Intune.

> [!TIP]
> - Cuando habilite la administración conjunta, asignará una recopilación como un *grupo piloto*. Se trata de un grupo que contiene un número pequeño de clientes para probar sus configuraciones de administración conjunta. Se recomienda crear una colección adecuada antes de iniciar el procedimiento. A continuación, puede seleccionar esa colección sin salir del procedimiento para ello.
> - A partir de la versión 1906 de Configuration Manager, es posible que necesite varias recopilaciones, porque puede asignar un *grupo piloto* distinto para cada carga de trabajo.

### <a name="enable-co-management-starting-in-version-1906"></a>Habilitación de la administración conjunta a partir de la versión 1906

Para habilitar la administración conjunta a partir de la versión 1906 de Configuration Manager, siga estas instrucciones:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Habilitación de la administración conjunta en la versión 1902 y versiones anteriores

Para habilitar la administración conjunta para la versión 1902 y versiones anteriores de Configuration Manager, siga estas instrucciones:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Uso de Intune para implementar el cliente de Configuration Manager

Puede usar Intune para instalar el cliente de Configuration Manager en dispositivos Windows 10 que están actualmente solo administrados con Intune.  

A continuación, cuando inscriba un dispositivo Windows 10 anteriormente no administrado con Intune, se instalará automáticamente el cliente de Configuration Manager.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Creación de una aplicación de Intune para instalar el cliente de Configuration Manager

1. En el servidor de sitio principal, inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://endpoint.microsoft.com) y vaya a **Aplicaciones** > **Todas las aplicaciones** > **Agregar**.

2. Como tipo de aplicación, seleccione **Aplicación de línea de negocio** en **Otros**.

3. En **Archivo del paquete de aplicaciones**, vaya a la ubicación del archivo de Configuration Manager **ccmsetup.msi** y seleccione **Abrir > Aceptar**.
Por ejemplo, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*.

4. Seleccione **Información de la aplicación** y, a continuación, especifique los detalles siguientes:
   - **Descripción**: Cliente de Configuration Manager  

   - **Publicador**: Microsoft  

   - **Argumentos de la línea de comandos**: *\<Specify the **CCMSETUPCMD** command line. You can use the command line you saved from the* Enablement *page of the Co-management Configuration Wizard. This command line includes the names of your cloud service and additional values that enable devices to install the Configuration Manager client software.>*  

     La estructura de la línea de comandos debe ser similar a este ejemplo, usando solo los parámetros CCMSETUPCMD y SMSSiteCode:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Si no tiene la línea de comandos disponible, puede ver las propiedades de *CoMgmtSettingsProd* en la consola de Configuration Manager para obtener una copia de la línea de comandos.

5. Seleccione **Aceptar > Agregar**.  La aplicación se crea y pasa a estar disponible en la consola de Intune. Una vez que la aplicación está disponible, puede usar la siguiente sección para configurar Intune para asignarla a los dispositivos Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Asignación de una aplicación de Intune para instalar el cliente de Configuration Manager

El procedimiento siguiente implementa la aplicación para instalar el cliente de Configuration Manager que creó en el procedimiento anterior.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://endpoint.microsoft.com). Seleccione **Aplicaciones** > **Todas las aplicaciones** y elija **ConfigMgr Client Setup Bootstrap**, la aplicación que creó para implementar el cliente de Configuration Manager.  

2. Seleccione **Propiedades** y luego **Editar** para **Asignaciones**. Seleccione **Agregar grupo** en **Requerido** (asignaciones) para establecer los grupos de Azure Active Directory (AD) que tienen los usuarios y los dispositivos que quiere que participen en la administración conjunta.  

3. Seleccione **Revisar + guardar** y luego **Guardar** para guardar la configuración.
Ahora la aplicación es obligatoria para los usuarios y dispositivos que le asigne. Después de que la aplicación instale el cliente de Configuration Manager en un dispositivo, se administra mediante la administración conjunta.

## <a name="summary"></a>Resumen

Después de completar los pasos de configuración de este tutorial, puede empezar a administrar los dispositivos de forma conjunta.

## <a name="next-steps"></a>Pasos siguientes

- Revise el estado de los dispositivos administrados conjuntamente con el [panel de administración conjunta](how-to-monitor.md).
- Use [Windows Autopilot](quickstart-autopilot.md) para aprovisionar nuevos dispositivos.
- Use el [acceso condicional](quickstart-conditional-access.md) y las reglas de cumplimiento de Intune para administrar el acceso de los usuarios a los recursos corporativos.
