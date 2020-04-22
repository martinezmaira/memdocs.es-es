---
title: Configuración de Cloud Management Gateway
titleSuffix: Configuration Manager
description: Use este proceso paso a paso para configurar una instancia de Cloud Management Gateway (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: d087b3645de5e03936542e35c9261edd8609cd81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695293"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar puerta de enlace de administración en la nube para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este proceso se incluyen los pasos necesarios para configurar una instancia de Cloud Management Gateway (CMG).

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../../servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="before-you-begin"></a>Antes de comenzar

Empiece por leer el artículo [Plan for cloud management gateway](plan-cloud-management-gateway.md) (Plan para Cloud Management Gateway). Use ese artículo para determinar el diseño de CMG.

Use la lista de comprobación siguiente para asegurarse de que tiene la información necesaria y los requisitos previos para crear una instancia de CMG:  

- El entorno de Azure que se va a usar. Por ejemplo, la nube pública de Azure o la nube de Azure US Government.  

- Necesitará uno o varios certificados para CMG, en función del diseño. Para obtener más información, vea [Certificates for cloud management gateway](certificates-for-cloud-management-gateway.md) (Certificados para Cloud Management Gateway).  

- Necesitará los requisitos siguientes para una implementación de [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) de CMG:  

    - Integración con [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) para la **administración en la nube**. La detección de usuarios de Azure AD no es necesaria.  

    - El proveedor de recursos **Microsoft.ClassicCompute** & **Microsoft.Storage** debe estar registrado en la suscripción de Azure. Para obtener más información, vea [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - Un administrador de suscripciones debe iniciar sesión.  

- Un nombre único global para el servicio. Este nombre procede del [certificado de autenticación de servidor de CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Para habilitar CMG como punto de distribución en la nube, es necesario elegir el mismo nombre de servicio de CMG único globalmente, de modo que esté disponible como nombre de cuenta de almacenamiento único globalmente. Este nombre procede del [certificado de autenticación de servidor de CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- La región de Azure para esta implementación de CMG.  

- El número de instancias de máquina virtual necesarias para la escala y redundancia.  

- Si todavía necesita usar la implementación del servicio clásico de Azure en la versión 1810 o anteriores de Configuration Manager, necesita estos requisitos:  

    > [!Important]  
    > A partir de la versión 1810, las implementaciones de servicio clásico de Azure estarán en desuso en Configuration Manager. Use las implementaciones de Azure Resource Manager para Cloud Management Gateway. Para obtener más información, vea [Planear para Cloud Management Gateway](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > A partir de la versión 1902 de Configuration Manager, Azure Resource Manager es el único mecanismo de implementación para instancias nuevas de Cloud Management Gateway.<!-- 3605704 -->

    - Identificador de suscripción de Azure  

    - Certificado de administración de Azure  


## <a name="set-up-a-cmg"></a>Configurar una instancia de CMG

Realice este procedimiento en el sitio de nivel superior. Ese sitio es un sitio primario independiente, o bien el sitio de administración central.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios de nube** y seleccione **Cloud Management Gateway**.  

2. Seleccione **Crear instancia de Cloud Management Gateway** en la cinta de opciones.  

3. En la página General del asistente, seleccione **Iniciar sesión**. Autentíquese con una cuenta de administración de suscripción de Azure. El asistente rellena automáticamente los campos restantes con la información almacenada durante el requisito previo de integración de Azure AD. Si tiene varias suscripciones, seleccione el **Id. de suscripción** de la suscripción deseada que se va a usar.

    > [!Note]  
    > A partir de la versión 1810, las implementaciones de servicio clásico de Azure entraron en desuso en Configuration Manager. En la versión 1902 y versiones anteriores, seleccione la **implementación de Azure Resource Manager** como el método de implementación de CMG.
    >
    > Si necesita usar una implementación de servicio clásico, seleccione esa opción en esta página. Primero escriba su **id. de suscripción** de Azure. Después, haga clic en **Examinar** y elija el archivo .PFX para el certificado de administración de Azure.

4. Especifique el **entorno de Azure** para esta instancia de CMG. Las opciones de la lista desplegable pueden variar según el método de implementación.  

5. Seleccione **Siguiente**. Espere mientras el sitio prueba la conexión a Azure.  

6. En la página de configuración del asistente, seleccione primero **Examinar** y elija el archivo .PFX para el certificado de autenticación de servidor de CMG. El nombre de este certificado rellena los campos **FQDN de servicio** y **Nombre de servicio** necesarios.  

   > [!NOTE]  
   > El certificado de autenticación de servidor de CMG admite caracteres comodín. Si usa un certificado comodín, reemplace el asterisco (`*`) en el campo **FQDN de servicio** por el nombre de host deseado para la instancia de CMG.<!--491233-->  

7. Seleccione la lista desplegable **Región** para elegir la región de Azure para esta instancia de CMG.  

8. Seleccione una opción de **Grupo de recursos**.
   1. Si elige **Usar existente**, seleccione un grupo de recursos existente en la lista desplegable. El grupo de recursos seleccionado debe existir en ese momento en la región seleccionada en el paso 7. Si selecciona un grupo de recursos existente que se encuentre en una región distinta a la seleccionada previamente, se producirá un error de aprovisionamiento de CMG.
   2. Si elige **Crear nuevo**, escriba el nombre del nuevo grupo de recursos.

9. En el campo **Instancia de VM**, escriba el número de máquinas virtuales para este servicio. El valor predeterminado es uno, pero se puede escalar hasta 16 máquinas virtuales por instancia de CMG.  

10. Seleccione **Certificados** para agregar certificados raíz de confianza de cliente. Agregue todos los certificados de la cadena de confianza.  

    > [!Note]  
    > A partir de la versión 1806, para crear una instancia de CMG ya no es necesario proporcionar un certificado raíz de confianza en la página Configuración. Este certificado no es necesario cuando se usa Azure Active Directory (Azure AD) para la autenticación de cliente, pero solía ser necesario en el asistente. Si usa certificados de autenticación de cliente PKI, entonces todavía debe agregar un certificado raíz de confianza a la CMG.<!--SCCMDocs-pr issue #2872-->  
    >
    > En la versión 1902 y versiones anteriores, solo puede agregar dos CA raíz de confianza y cuatro CA intermedias (subordinadas).<!-- SCCMDocs-pr#4022 -->

11. De forma predeterminada, el asistente habilita la opción para **Comprobar revocación de certificado de cliente**. Para que esta verificación funcione, se debe publicar de manera pública una lista de revocación de certificados (CRL). Para obtener más información, vea [Publicar la lista de revocación de certificados](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. A partir de la versión 1906, puede **exigir TLS 1.2**. Esta configuración solo se aplica a una máquina virtual de servicio en la nube de Azure. No se aplica a ningún cliente ni servidor de sitio de Configuration Manager local. Para más información sobre TLS 1.2, consulte [Habilitación de TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. A partir de la versión 1806, de forma predeterminada, el asistente habilita la opción siguiente: **Permitir a CMG funcionar como un punto de distribución de nube y servir contenido desde Azure Storage**. Ahora una instancia de CMG también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure.  

14. Seleccione **Siguiente**.  

15. Para supervisar el tráfico de CMG con un umbral de 14 días, active la casilla para activar la alerta de umbral. Luego, especifique el umbral y el porcentaje en que desea elevar los distintos niveles de alerta. Elija **Siguiente** cuando termine.  

16. Revise la configuración y elija **Siguiente**. Configuration Manager comienza a configurar el servicio. Cuando cierre el asistente, se tardarán entre cinco y 15 minutos en aprovisionar totalmente el servicio en Azure. Compruebe la columna **Estado** de la nueva instancia de CMG para determinar si el servicio está listo.  

    > [!Note]  
    > Para solucionar problemas con las implementaciones de CMG, use **CloudMgr.log** y **CMGSetup.log**. Para obtener más información, vea [Archivos de registro](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurar un sitio primario para la autenticación de certificados de cliente

Si se usan [certificados de autenticación de cliente](certificates-for-cloud-management-gateway.md#bkmk_clientauth) para que los clientes se autentiquen con la instancia de CMG, siga estos pasos para configurar cada sitio primario.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda el nodo **Configuración del sitio** y haga clic en **Sitios**.  

2. Seleccione el sitio primario al que se asignan los clientes basados en Internet y haga clic en **Propiedades**.  

3. Cambie a la pestaña **Comunicación de equipo cliente** de la hoja de propiedades del sitio primario y active la casilla **Usar un certificado de cliente PKI (capacidad de autenticación de cliente) cuando esté disponible**.  

    > [!Note]
    > A partir de la versión 1906, esta pestaña se denomina **Communication Security** (Seguridad de la comunicación).<!-- SCCMDocs#1645 -->  

4. Si no se publica una CRL, desactive la opción **Los clientes comprueban la lista de revocación de certificados (CRL) para sistemas de sitio**.  


## <a name="add-the-cmg-connection-point"></a>Agregar el punto de conexión de CMG

El punto de conexión de CMG es el rol de sistema de sitio para comunicarse con la instancia de CMG. Para agregar el punto de conexión de CMG, siga las instrucciones generales para [instalar roles de sistema de sitio](../../../servers/deploy/configure/install-site-system-roles.md). En la página Selección de rol del sistema del Asistente para agregar roles de sistema de sitio, seleccione **Punto de conexión de Cloud Management Gateway**. Después, seleccione el **Nombre inst. de Cloud Management Gateway** a la que se conecta este servidor. El asistente muestra la región para la instancia de CMG seleccionada.

> [!Important]
> El punto de conexión de CMG debe tener un [certificado de autenticación de cliente](certificates-for-cloud-management-gateway.md#bkmk_clientauth) en algunos escenarios.

Para solucionar problemas de estado de CMG, use **CMGService.log** y **SMS_Cloud_ProxyConnector.log**. Para obtener más información, vea [Archivos de registro](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurar roles para el cliente para el tráfico de CMG

Configure los sistemas de sitio de punto de administración y punto de actualización de software para aceptar el tráfico de CMG. Siga estos pasos en el sitio primario, para todos los puntos de administración y de actualización de software que dan servicio a los clientes basados en Internet.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**. En la pestaña Inicio de la cinta de opciones, en el grupo Ver, seleccione **Servidores con rol**. Después seleccione **Punto de administración** en la lista.  

2. Seleccione el servidor de sistema de sitio que quiera configurar para el tráfico de CMG. Seleccione el rol **Punto de administración** en el panel de detalles y, después, seleccione **Propiedades** en la cinta.  

3. En la hoja Propiedades de punto de administración, en Conexiones de cliente, active la casilla situada junto a **Permitir tráfico de Cloud Management Gateway en Configuration Manager**.

    En función del diseño de CMG y la versión de Configuration Manager, es posible que sea necesario habilitar la opción **HTTPS**. Para obtener más información, vea [Enable management point for HTTPS](certificates-for-cloud-management-gateway.md#bkmk_mphttps) (Habilitar el punto de administración para HTTPS).  

4. Seleccione **Aceptar** para cerrar la ventana de propiedades del punto de administración.  

Repita estos pasos para otros puntos de administración según sea necesario y para cualquier punto de actualización de software.


## <a name="configure-boundary-groups"></a>Configurar grupos de límites

<!--3640932-->
A partir de la versión 1902, puede asociar una instancia de CMG con un grupo de límites. Esta configuración permite a los clientes predeterminar o recurrir a dicha puerta de enlace para la comunicación con el cliente de acuerdo con las relaciones de grupo de límites.

Para más información sobre los grupos de límites, consulte [Configuración de grupos de límites](../../../servers/deploy/configure/boundary-groups.md).

Cuando [cree o configure un grupo de límites](../../../servers/deploy/configure/boundary-group-procedures.md), en la pestaña **Referencias**, agregue una puerta de enlace de administración de la nube. Esta acción asocia la instancia de dicha puerta de enlace con este grupo de límites.


## <a name="configure-clients-for-cmg"></a>Configurar a clientes para CMG

Una vez en ejecución los roles de sistema de sitio y CMG, los clientes obtienen la ubicación del servicio CMG automáticamente en la siguiente solicitud de ubicación. Los clientes deben estar en la intranet para recibir la ubicación del servicio CMG, a menos que se [instalen y asignen clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](../../deploy/deploy-clients-cmg-azure.md). El ciclo de sondeo de las solicitudes de ubicación es cada 24 horas. Si no quiere esperar a la solicitud de ubicación normalmente programada, puede forzar la solicitud si reinicia el servicio Host de agente de SMS (ccmexec.exe) en el equipo.  

> [!Note]
> De forma predeterminada, todos los clientes reciben la directiva de CMG. Controle este comportamiento con la configuración de cliente, [Permitir que los clientes usen una instancia de Cloud Management Gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

El cliente de Configuration Manager determina automáticamente si está en la intranet o en Internet. Si el cliente se puede poner en contacto con un controlador de dominio o un punto de administración local, establece su tipo de conexión en **Actualmente intranet**. En caso contrario, cambia a **Actualmente Internet** y usa la ubicación del servicio CMG para comunicarse con el sitio.

>[!NOTE]
> Puede forzar a un cliente para que siempre use la instancia de CMG independientemente de si se encuentra en la intranet o en Internet. Esta configuración es útil con fines de prueba, o bien para los clientes a los que quiere forzar a usar siempre la instancia de CMG. Configure la siguiente clave del Registro en el cliente:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> También puede especificar esta opción durante la instalación de cliente mediante la propiedad [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf).
>
> Esta configuración se aplicará siempre, incluso si el cliente se mueve a una ubicación en la que las configuraciones del grupo de límites aprovecharían los recursos locales.


Para comprobar que los clientes tienen la directiva que especifica la instancia de CMG, abra un símbolo del sistema de Windows PowerShell como administrador en el equipo cliente y ejecute el comando siguiente: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Este comando muestra los puntos de administración basados en Internet que el cliente conoce. Aunque la instancia de CMG no es técnicamente un punto de administración basado en Internet, los clientes la perciben como tal.

> [!Note]  
> Para solucionar problemas de tráfico de cliente de CMG, use **CMGHttpHandler.log**, **CMGService.log** y **SMS_Cloud_ProxyConnector.log**. Para obtener más información, vea [Archivos de registro](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="modify-a-cmg"></a>Modificar una instancia de CMG

Después de crear una instancia de CMG, puede modificar algunas de sus configuraciones. Seleccione instancia de CMG en la consola de Configuration Manager y seleccione **Propiedades**. Configure opciones en las siguientes pestañas:  

#### <a name="general"></a>General

- **Certificado de administración de Azure**: cambiar el certificado de administración de Azure para la instancia de CMG. Esta opción es útil al actualizar el certificado antes de que caduque.  

#### <a name="settings"></a>Configuración

- **Archivo de certificado**: cambiar el certificado de autenticación de servidor para la instancia de CMG. Esta opción es útil al actualizar el certificado antes de que caduque.  

- **Instancia de VM**: cambiar el número de máquinas virtuales que usa el servicio en Azure. Esta configuración permite escalar horizontal o verticalmente el servicio de forma dinámica en función de consideraciones de uso o costo.  

- **Certificados**: agregar o quitar certificados de entidades de certificación raíz de confianza o intermedias. Esta opción es útil cuando se agregan nuevas entidades de certificación o se retiran los certificados caducados.  

- **Comprobar revocación de certificado de cliente**: si originalmente no se habilitó esta opción al crear la instancia de CMG, se puede habilitar posteriormente una vez que se publica la CRL. Para obtener más información, vea [Publicar la lista de revocación de certificados](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Permitir a CMG funcionar como un punto de distribución de nube y servir contenido desde Azure Storage**: a partir de la versión 1806, esta nueva opción está habilitada de forma predeterminada. Ahora una instancia de CMG también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure.<!--1358651-->  

#### <a name="alerts"></a>Alertas

Vuelva a configurar las alertas en cualquier momento después de crear la instancia de CMG.


### <a name="redeploy-the-service"></a>Volver a implementar el servicio

Los cambios más importantes, como las configuraciones siguientes, requieren volver a implementar el servicio:

- Método de implementación clásica en Azure Resource Manager
- Suscripción
- Nombre del servicio
- PKI privada a pública
- Región

Mantenga siempre al menos una instancia de CMG activa para que los clientes basados en Internet reciban la directiva actualizada. Los clientes basados en Internet no se pueden comunicar con una instancia de CMG que se ha quitado. Los clientes no saben que hay una nueva hasta que vuelven a la intranet. Al crear una segunda instancia de CMG para eliminar la primera, cree también otro punto de conexión de CMG.

De forma predeterminada, los clientes actualizan la directiva cada 24 horas, por lo que después de crear una instancia de CMG, espere al menos un día antes de eliminar la antigua. Si los clientes están apagados o sin conexión a Internet, debe esperar más.

Si tiene una instancia de CMG existente en el método de implementación clásico, debe implementar una instancia de CMG nueva para usar el método de implementación de Azure Resource Manager.<!--509753--> Hay dos opciones:  

- Si quiere reutilizar el mismo nombre de servicio:  

    1. En primer lugar, elimine la instancia de CMG clásica, teniendo en cuenta las instrucciones de tener siempre al menos una instancia de CMG activa para los clientes basados en Internet.  

    2. Cree una instancia de CMG mediante una implementación de Resource Manager. Reutilice el mismo certificado de autenticación de servidor.  

    3. Vuelva a configurar el punto de conexión de CMG para usar la nueva instancia de CMG.  

- Si quiere usar un nombre de servicio nuevo:  

    1. Cree una instancia de CMG mediante una implementación de Resource Manager. Use un certificado de autenticación de servidor nuevo.  

    2. Cree un punto de conexión de CMG y un vínculo con la nueva instancia de CMG.  

    3. Espere al menos un día para que los clientes basados en Internet reciban la directiva sobre la instancia de CMG nueva.  

    4. Elimine la instancia de CMG clásica.  

> [!Tip]  
> Para determinar el modelo de implementación actual de una instancia de CMG:<!--SCCMDocs issue #611-->  
>
> 1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Cloud Management Gateway**.  
> 2. Seleccione la instancia de CMG.  
> 3. En el panel de detalles de la parte inferior de la ventana, busque el atributo **Modelo de implementación**. Para implementar Resource Manager, este atributo es **Azure Resource Manager**. El modelo de implementación heredado con el certificado de administración de Azure se muestra como **Azure Service Manager**.
>
> También puede agregar el atributo **Modelo de implementación** como una columna a la vista de lista.  

### <a name="modifications-in-the-azure-portal"></a>Modificaciones en Azure Portal

Modifique la instancia de CMG solo desde la consola de Configuration Manager. No se permite realizar modificaciones en el servicio ni en las máquinas virtuales subyacentes directamente en Azure. Todos los cambios podrían perderse sin previo aviso. Como sucede con cualquier PaaS, el servicio puede volver a generar las máquinas virtuales en cualquier momento. Estas recompilaciones pueden ocurrir para el mantenimiento de hardware de back-end, o bien para aplicar actualizaciones al sistema operativo de la máquina virtual.

### <a name="delete-the-service"></a>Eliminar el servicio

Si tiene que eliminar la instancia de CMG, hágalo también desde la consola de Configuration Manager. Quitar manualmente cualquier componente en Azure hace que el sistema sea incoherente. Este estado deja información huérfana y se pueden producir comportamientos inesperados.


## <a name="next-steps"></a>Pasos siguientes

- [Supervisar clientes para la puerta de enlace de administración en la nube](monitor-clients-cloud-management-gateway.md)
- [Preguntas más frecuentes sobre Cloud Management Gateway](cloud-management-gateway-faq.md)
