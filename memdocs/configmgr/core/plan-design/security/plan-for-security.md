---
title: Planear la seguridad
titleSuffix: Configuration Manager
description: Obtenga los procedimientos recomendados y otra información sobre la seguridad en Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b15b3017dd49c75f4281a3c0bfd1c8a695ab8bae
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526005"
---
# <a name="plan-for-security-in-configuration-manager"></a>Planeación de la seguridad en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se describen los conceptos para tener en cuenta al planear la seguridad con la implementación de Configuration Manager. Se incluyen las secciones siguientes:  

- [Planificación de certificados (autofirmados y PKI)](#BKMK_PlanningForCertificates)  
  - [Certificados Cryptography: Next Generation (CNG)](#bkmk_plan-cng)  
  - [HTTP mejorado](#bkmk_plan-ehttp)  
  - [Certificados para CMG y CDP](#bkmk_plan-cmgcdp)  
  - [El certificado de firma de servidor de sitio (autofirmado)](#bkmk_plansitesign)  
  - [Revocación de certificados PKI](#BKMK_PlanningForCRLs)  
  - [Los certificados raíz de confianza PKI y la lista de emisores de certificados](#BKMK_PlanningForRootCAs)  
  - [Selección de certificados de cliente PKI](#BKMK_PlanningForClientCertificateSelection)  
  - [Una estrategia de transición para los certificados PKI y la administración de cliente basada en Internet](#BKMK_PlanningForPKITransition)  

- [Planeación de la clave raíz confiable](#BKMK_PlanningForRTK)  

- [Planeación de la firma y el cifrado](#BKMK_PlanningForSigningEncryption)  

- [Planeación de la administración basada en roles](#BKMK_PlanningForRBA)  

- [Planeación de Azure Active Directory](#bkmk_planazuread)  

- [Plan para la autenticación del proveedor de SMS](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Planear certificados (autofirmados y PKI)  

Configuration Manager usa una combinación de certificados autofirmados y certificados de infraestructura de clave pública (PKI).  

Use los certificados PKI siempre que sea posible. Para obtener más información, vea [Requisitos de certificados PKI](../network/pki-certificate-requirements.md). Cuando Configuration Manager solicita los certificados PKI durante la inscripción de dispositivos móviles, se debe usar Active Directory Domain Services y una entidad de certificación empresarial. Los demás certificados PKI se deben implementar y administrar independientemente de Configuration Manager. 

Los certificados PKI son necesarios cuando los equipos cliente se conectan a sistemas de sitio basados en internet. En algunos escenarios con Cloud Management Gateway y el punto de distribución de nube también se requieren los certificados PKI. Para más información, vea [Administrar clientes en Internet](../../clients/manage/manage-clients-internet.md).

Cuando usa PKI, también puede usar IPsec para proteger la comunicación de servidor a servidor entre sistemas de sitio en un sitio, entre sitios, y para otras transferencias de datos entre equipos. La implementación de IPsec es independiente de Configuration Manager.  

Si no hay certificados PKI disponibles, Configuration Manager genera certificados autofirmados de forma automática. Algunos certificados de Configuration Manager siempre son autofirmados. En la mayoría de los casos, Configuration Manager administra automáticamente los certificados autofirmados y no es necesario tomar medidas adicionales. Un ejemplo es el certificado de firma de servidor de sitio. Este certificado siempre es autofirmado. Se asegura de que las directivas que los clientes descargan del punto de administración se enviaron desde el servidor de sitio y no se han alterado.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a> Certificados Cryptography: Next Generation (CNG)  

Configuration Manager admite los certificados Cryptography: Next Generation (CNG). Los clientes de Configuration Manager pueden usar un certificado de autenticación del cliente PKI con clave privada en el proveedor de almacenamiento de claves (KSP) de CNG. Gracias a la compatibilidad con KSP, los clientes de Configuration Manager admiten una clave privada basada en hardware, como el KSP de TPM para los certificados de autenticación de cliente PKI. Para obtener más información, consulte [Introducción a los certificados CNG](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a> HTTP mejorado  

Se recomienda usar la comunicación HTTPS para todas las vías de comunicación de Configuration Manager, pero puede ser un reto para algunos clientes debido a la sobrecarga de administración de los certificados PKI. La introducción de la integración de Azure Active Directory (Azure AD) reduce algunos requisitos de certificado, pero no todos. A partir de la versión 1806, puede habilitar el sitio para usar **HTTP mejorado**. Esta configuración admite HTTPS en los sistemas de sitio mediante una combinación de certificados autofirmados y Azure AD. No requiere PKI. Para obtener más información, vea [HTTP mejorado](../hierarchy/enhanced-http.md).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a> Certificados para CMG y CDP

La administración de clientes en Internet a través de Cloud Management Gateway (CMG) y el punto de distribución de nube (CDP) requiere el uso de certificados. El número y tipo de certificados varía en función de cada escenario. Vea los siguientes artículos para más información:
- [Certificados para Cloud Management Gateway](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Certificados para el punto de distribución de nube](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a> Planificación del certificado de firma de servidor de sitio (autofirmado)  

Los clientes pueden obtener de forma segura una copia del certificado de firma de servidor de sitio a través de Active Directory Domain Service y de la instalación de inserción de cliente. Si los clientes no pueden obtener una copia de este certificado mediante uno de estos mecanismos, instálelo al instalar el cliente. Este proceso es especialmente importante si la primera comunicación del cliente se establece con un punto de administración basado en Internet. Como este servidor está conectado a una red de confianza, es más vulnerable a los ataques. Si no se realiza este paso adicional, los clientes descargan automáticamente una copia del certificado de firma de servidor de sitio desde el punto de administración.  

Los clientes no pueden obtener de forma segura una copia del certificado de servidor de sitio en los escenarios siguientes:  

- No se instala el cliente mediante la inserción del cliente, y:  

  - No se ha ampliado el esquema de Active Directory para Configuration Manager.  

  - No se ha publicado el sitio del cliente en Active Directory Domain Services.  

  - El cliente pertenece a un grupo de trabajo o un bosque que no es de confianza.  

- Se usa la administración de clientes basada en Internet y el cliente se instala cuando está en Internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes con una copia del certificado de firma de servidor de sitio  

1.  Busque el certificado de firma de servidor de sitio en el servidor de sitio primario. El certificado se almacena en el almacén de certificados **SMS** de Windows. Tiene el nombre de sujeto **Servidor de sitio** y el nombre descriptivo **Certificado de firma de servidor de sitio**.  

2.  Exporte el certificado sin la clave privada, almacene el archivo de forma segura y acceda a él solo desde un canal seguro.  

3.  Instale el cliente con la propiedad de client.msi siguiente: `SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Planear la revocación de certificados PKI  

Cuando se usan certificados PKI con Configuration Manager, planifique el uso de una lista de revocación de certificados (CRL). Los dispositivos usan la CRL para comprobar el certificado en el equipo que realiza la conexión. La CRL es un archivo creado y firmado por una entidad de certificación (CA). Tiene una lista de certificados que la entidad de certificación ha emitido pero revocado. Cuando un administrador de certificados revoca los certificados, su huella digital se agrega a la CRL. Por ejemplo, si se sabe o se sospecha que un certificado emitido se ha puesto en peligro.

> [!IMPORTANT]  
> Como la ubicación de la CRL se agrega al certificado cuando lo emite la CA, asegúrese de planificar la CRL antes de implementar los certificados PKI que usa Configuration Manager.  

IIS comprueba siempre la CRL de los certificados de cliente, y esta configuración no se puede cambiar en Configuration Manager. De forma predeterminada, los clientes de Configuration Manager siempre comprueban la CRL para sistemas de sitio. Para deshabilitar esta configuración, especifique una propiedad del sitio y una propiedad de CCMSetup.  

Los equipos en los que se usa la comprobación de revocación de certificados pero que no pueden encontrar la CRL se comportan como si todos los certificados de la cadena de certificación estuvieran revocados. Esto se debe a que no pueden comprobar que los certificados estén en la lista de revocación de certificados. En este escenario, se produce un error en todas las conexiones que requieren certificados e incorporan la comprobación de la CRL. Al validar que la CRL esté disponible navegando hasta su ubicación HTTP, es importante tener en cuenta que el cliente de Configuration Manager se ejecuta como sistema local. Por lo tanto, la prueba de accesibilidad de la CRL con un navegador web ejecutado en el contexto del usuario puede realizarse correctamente, aunque es posible que la cuenta del ordenador se bloquee al intentar realizar una conexión HTTP a la misma URL de CRL debido a la solución de filtrado web interna. En esta situación, puede que deba agregar la URL de la CRL a la lista de direcciones permitidas de todas las soluciones de filtrado web.

La comprobación de la CRL cada vez que se usa un certificado proporciona mayor seguridad que usar un certificado que se ha revocado. Pero supone un retraso en la conexión y procesamiento adicional en el cliente. Es posible que la organización requiera esta comprobación de seguridad adicional para los clientes que están en Internet o en una red que no es de confianza.  

Consulte con los administradores de PKI antes de decidir si los clientes de Configuration Manager deben comprobar la CRL. Después, considere la posibilidad de mantener esta opción habilitada en Configuration Manager cuando se cumplan las dos condiciones siguientes:  

- La infraestructura de PKI admite una CRL, y está publicada donde todos los clientes de Configuration Manager puedan encontrarla. Es posible que estos clientes incluyan dispositivos en Internet y en bosques que no son de confianza.  

- El requisito de comprobar la CRL para cada conexión a un sistema de sitio que está configurado para usar un certificado PKI es mayor que los requisitos siguientes:  
  - Conexiones más rápidas  
  - Procesamiento eficaz en el cliente  
  - El riesgo de que los clientes no puedan conectarse a los servidores si no se puede encontrar la CRL  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Planear los certificados raíz de confianza PKI y la lista de emisores de certificados  

Si en los sistemas de sitio de IIS se usan certificados de cliente PKI para la autenticación de cliente a través de HTTP, o bien para la autenticación de cliente y el cifrado a través de HTTPS, es posible que tenga que importar los certificados de CA raíz como una propiedad de sitio. Estos son los dos escenarios:  

- Se implementan los sistemas operativos mediante el uso de Configuration Manager y los puntos de administración solo aceptan conexiones de cliente HTTPS.  

- Se usan certificados de cliente PKI que no están vinculados a un certificado raíz de confianza para los puntos de administración.  

  > [!NOTE]  
  > Cuando se emiten certificados PKI de cliente desde la misma jerarquía de CA que emite los certificados de servidor que se usan para los puntos de administración, no es necesario especificar este certificado de CA raíz. Pero si usa varias jerarquías de CA y no está seguro de si tienen confianza mutua, importe la CA raíz de la jerarquía de entidades de certificación de los clientes.  

Si debe importar los certificados de CA raíz para Configuration Manager, expórtelos desde la CA emisora o desde el equipo cliente. Si exporta el certificado desde la CA emisora que también es la CA raíz, asegúrese de que no exporta la clave privada. Almacene el archivo de certificado exportado en una ubicación segura para evitar que sea alterado. Necesita acceso al archivo al configurar el sitio. Si accede al archivo a través de la red, asegúrese de que la comunicación está protegida contra alteraciones mediante IPsec.  

Si cualquier certificado de CA raíz que importa se renueva, debe importar el certificado renovado.  

Estos certificados de CA raíz importados y el certificado de CA raíz de cada punto de administración forman la lista de emisores de certificados que los equipos de Configuration Manager usan de las siguientes maneras:  

- Cuando los clientes se conectan a puntos de administración, el punto de administración comprueba que el certificado de cliente esté vinculado a un certificado raíz de confianza de la lista de emisores de certificados del sitio. Si no es así, se rechaza el certificado y se produce un error en la conexión de PKI.  

- Cuando los clientes seleccionan un certificado PKI y tienen una lista de emisores de certificados, seleccionan un certificado vinculado a un certificado raíz de confianza de la lista de emisores de certificados. Si no hay ninguna coincidencia, el cliente no selecciona un certificado PKI. Para obtener más información, vea [Planificación de la revocación de certificados PKI](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planear la selección de certificados de cliente PKI  

Si en los sistemas de sitio de IIS se usan certificados de cliente PKI para la autenticación de cliente a través de HTTP o para la autenticación de cliente y el cifrado a través de HTTPS, planifique cómo seleccionan los clientes de Windows el certificado que se va a usar para Configuration Manager.  

> [!NOTE]  
> Algunos dispositivos no admiten un método de selección de certificado. En su lugar, seleccionan automáticamente el primer certificado que cumple los requisitos de certificados. Por ejemplo, los clientes de equipos y dispositivos móviles Mac no admiten un método de selección de certificado.  

En muchos casos, la configuración y el comportamiento predeterminados son suficientes. El cliente de Configuration Manager en equipos de Windows filtra varios certificados mediante estos criterios en este orden:  

1.  La lista de emisores de certificados: El certificado está vinculado a una CA raíz que es confiable para el punto de administración.  

2.  El certificado se encuentra en el almacén de certificados predeterminado **Personal**.  

3.  El certificado es válido, no se revocó y no expiró. La comprobación de validez también comprueba que la clave privada es accesible.  

4.  El certificado tiene la capacidad de autenticación de cliente.

5.  El nombre del firmante del certificado contiene el nombre del equipo local como una subcadena.  

6.  El certificado tiene el periodo de validez más largo.  

Configure los clientes para que usen la lista de emisores de certificados mediante los mecanismos siguientes:  

- Publíquela con información de sitio de Configuration Manager en Active Directory Domain Services.  

- Instale los clientes mediante la inserción del cliente.  

- Los clientes la descargan desde el punto de administración después de ser asignados correctamente a su sitio.  

- Especifíquela durante la instalación del cliente, como una propiedad client.msi CCMSetup de CCMCERTISSUERS.  

Los clientes que no tienen la lista de emisores de certificados cuando se instalan por primera vez y todavía no están asignados al sitio, omiten esta comprobación. Cuando los clientes tienen la lista de emisores de certificados y no tienen un certificado PKI vinculado a un certificado raíz de confianza de la lista de emisores de certificados, se produce un error en la selección del certificado. Los clientes no continúan con los demás criterios de selección de certificados.  

En la mayoría de los casos, el cliente de Configuration Manager identifica correctamente un certificado PKI exclusivo y adecuado. Pero si este comportamiento no es así, en lugar de seleccionar el certificado en función de la capacidad de autenticación de cliente, puede configurar dos métodos de selección alternativos:  

- Una coincidencia de cadena parcial del nombre de sujeto del certificado de cliente. Este método es una coincidencia que no distingue mayúsculas de minúsculas. Es adecuado si se usa el nombre de dominio completo (FQDN) de un equipo en el campo del asunto y se quiere basar la selección de certificados en el sufijo del dominio, por ejemplo **contoso.com**. Pero este método de selección se puede usar para identificar cualquier cadena de caracteres secuenciales del nombre de sujeto del certificado que permita distinguirlo de los demás en el almacén de certificados de cliente.  

  > [!NOTE]
  > No se puede usar la coincidencia de cadena parcial con el nombre alternativo del firmante (SAN) como configuración de sitio. Aunque se puede especificar una coincidencia de cadena parcial para el SAN mediante CCMSetup, las propiedades de sitio la sobrescribirán en los escenarios siguientes:  
  > 
  > - Los clientes recuperan información del sitio que está publicada en Active Directory Domain Services.  
  >   - Los clientes se instalan mediante la instalación de inserción de cliente.  
  > 
  >   Use una coincidencia de cadena parcial del SAN solo cuando instale los clientes manualmente y cuando estos no recuperen la información del sitio desde Active Directory Domain Services. Por ejemplo, estas condiciones se aplican a los clientes solo de Internet.  

- Una coincidencia de los valores de atributo del nombre de firmante del certificado de cliente o de los valores de atributo del nombre alternativo del firmante (SAN). Este método es una coincidencia que distingue mayúsculas de minúsculas. Es adecuado si se usan un nombre distintivo X500 o identificadores de objetos (OID) equivalentes conforme a RFC 3280, y se quiere basar la selección de certificados en los valores de atributo. Puede especificar sólo los atributos, con sus valores, que necesita para identificar de manera exclusiva o validar el certificado y distinguirlo de los demás certificados del almacén de certificados de cliente.  

En la siguiente tabla aparecen los valores de atributo que Configuration Manager admite para los criterios de selección de certificados de cliente.  

|Atributo OID|Atributo de nombre distintivo|Definición de atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente de dominio|  
|1.2.840.113549.1.9.1|E o E-mail|Dirección de correo electrónico|  
|2.5.4.3|CN|Nombre común|  
|2.5.4.4|SN|Nombre de sujeto|  
|2.5.4.5|SERIALNUMBER|Número de serie|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidad|  
|2.5.4.8|S o ST|Nombre de estado o provincia|  
|2.5.4.9|STREET|Dirección|  
|2.5.4.10|O|Nombre de la organización|  
|2.5.4.11|OU|Unidad organizativa|  
|2.5.4.12|T o Title|Título|  
|2.5.4.42|G o GN o GivenName|Nombre dado|  
|2.5.4.43|I o Initials|Iniciales|  
|2.5.29.17|(ningún valor)|Nombre alternativo del sujeto| 

  > [!NOTE]
  > Si configura cualquiera de los métodos de selección de certificados alternativos anteriores, no es necesario que el nombre del firmante del certificado contenga el nombre del equipo local.

Si se encuentra más de un certificado adecuado después de aplicar los criterios de selección, se puede invalidar la configuración predeterminada para seleccionar el certificado que tenga el periodo de validez más largo y, en su lugar, especificar que no se seleccione ningún certificado. En este escenario, el cliente no podrá comunicarse con los sistemas de sitio de IIS con un certificado PKI. El cliente envía un mensaje de error al punto de estado de reserva asignado para alertar acerca del error de selección de certificados de manera que se puedan cambiar o refinar los criterios de selección de certificados. El comportamiento del cliente luego dependerá de si la conexión con errores era HTTPS o HTTP:  

- Si la conexión con errores era HTTPS: El cliente intenta establecer una conexión a través de HTTP y usa el certificado autofirmado del cliente.  

- Si la conexión con errores era HTTP: El cliente intenta establecer otra conexión a través de HTTP con el certificado autofirmado del cliente.  

Para que sea más fácil identificar un certificado de cliente PKI exclusivo, también puede especificar un almacén personalizado distinto al almacén predeterminado **Personal** del almacén del **Equipo**. Pero debe crear este almacén independientemente de Configuration Manager. Debe poder implementar certificados en este almacén personalizado y renovarlos antes de que expire el periodo de validez.  

Para obtener más información, vea [Configurar opciones de certificados PKI de cliente](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Planificación de una estrategia de transición para certificados PKI y administración de cliente basada en Internet  

Las opciones de configuración flexible de Configuration Manager permiten llevar a cabo una transición gradual en los clientes y el sitio hacia el uso de los certificados PKI para proteger los extremos de cliente. Los certificados PKI proporcionan mejor seguridad y permiten administrar los clientes de Internet.  

Debido al número de opciones de configuración de Configuration Manager, no existe una única manera de llevar a cabo la transición de un sitio para que todos los clientes usen conexiones HTTPS. Sin embargo, puede seguir estos pasos como guía:  

1. Instale el sitio de Configuration Manager y configúrelo para que los sistemas de sitio acepten conexiones de cliente a través de HTTPS y HTTP.  

2. Configure la pestaña **Comunicación de equipo cliente** de las propiedades del sitio de modo que la **Configuración de sistema de sitio** sea **HTTP o HTTPS**, y seleccione **Usar un certificado de cliente PKI (capacidad de autenticación de cliente) cuando esté disponible**.  Para obtener más información, vea [Configurar opciones de certificados PKI de cliente](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > A partir de la versión 1906, esta pestaña se denomina **Communication Security** (Seguridad de la comunicación).<!-- SCCMDocs#1645 -->  

3. Lleve a cabo una implementación de PKI para certificados de cliente. Para obtener un ejemplo de implementación, vea [Implementación del certificado de cliente para equipos Windows](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. Instale los clientes mediante el método de instalación de inserción de cliente. Para obtener más información, vea [Cómo instalar clientes de Configuration Manager mediante la inserción de cliente](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

5. Supervise la implementación y el estado de los clientes mediante los informes y la información de la consola de Configuration Manager.  

6. Para realizar el seguimiento del número de clientes que utilizan un certificado PKI de cliente, consulte la columna **Certificado de cliente** del área de trabajo **Activos y compatibilidad** , nodo **Dispositivos** .  

    También puede implementar la herramienta de evaluación de preparación de HTTPS de Configuration Manager (**cmHttpsReadiness.exe**) en los equipos. Después, use los informes para ver cuántos equipos pueden usar un certificado PKI de cliente con Configuration Manager.  

   > [!NOTE]
   >  Cuando se instala el cliente de Configuration Manager, se instala la herramienta **CMHttpsReadiness.exe** en la carpeta `%windir%\CCM`. Al ejecutar esta herramienta, dispone de las opciones de línea de comandos siguientes:  
   > 
   > - `/Store:<name>`: esta opción es la misma que la propiedad de client.msi **CCMCERTSTORE**  
   > - `/Issuers:<list>`: esta opción es la misma que la propiedad de client.msi **CCMCERTISSUERS**    
   > - `/Criteria:<criteria>`: esta opción es la misma que la propiedad de client.msi **CCMCERTSEL**    
   > - `/SelectFirstCert`: esta opción es la misma que la propiedad de client.msi **CCMFIRSTCERT**    
   > 
   >   Para obtener más información, vea [Información sobre las propiedades de instalación de clientes](../../clients/deploy/about-client-installation-properties.md).  

7. Cuando esté seguro de que un número suficiente de los clientes usa correctamente su certificado PKI de cliente para la autenticación a través de HTTP, siga estos pasos:  

   1.  Implemente un certificado de servidor web PKI en un servidor miembro que ejecute un punto de administración adicional para el sitio, y configure ese certificado en IIS. Para obtener más información, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Instale el rol de punto de administración en este servidor y configure la opción **Conexiones de cliente** de las propiedades del punto de administración para **HTTPS**.  

8. Compruebe que los clientes que tienen un certificado PKI utilizan el nuevo punto de administración mediante HTTPS. Puede usar el registro de IIS o los contadores de rendimiento para comprobarlo.  

9. Vuelva a configurar otros roles de sistema de sitio para utilizar conexiones de cliente HTTPS. Si quiere administrar clientes en Internet, asegúrese de que los sistemas de sitio tienen un nombre de dominio completo de Internet. Configure puntos de administración individuales y puntos de distribución para aceptar conexiones de cliente desde Internet.  

    > [!IMPORTANT]  
    > Antes de configurar los roles de sistema de sitio para que acepten conexiones de Internet, revise la información de planeación y los requisitos previos de la administración de cliente basada en Internet. Para obtener más información, vea [Communications between endpoints](../hierarchy/communications-between-endpoints.md) (Comunicaciones entre puntos de conexión).  

10. Amplíe la implementación de certificados PKI para clientes y sistemas de sitio que ejecutan IIS. Configure los roles de sistema de sitio para las conexiones de cliente HTTPS y las conexiones a Internet, según sea necesario.  

11. Para obtener la máxima seguridad: Cuando esté seguro de que todos los clientes usan un certificado PKI de cliente para la autenticación y el cifrado, cambie las propiedades del sitio para que se use solamente HTTPS.  

    Este plan presenta primero los certificados PKI para la autenticación solo a través de HTTP y, después, para la autenticación y el cifrado a través de HTTPS. Al seguir este plan para introducir gradualmente estos certificados, se reduce el riesgo de que los clientes se conviertan en no administrados. También se beneficiará de la máxima seguridad que Configuration Manager admite.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Planear la clave raíz confiable  

La clave raíz confiable de Configuration Manager proporciona a los clientes de Configuration Manager un mecanismo para comprobar que los sistemas de sitio pertenecen a su jerarquía. Cada servidor de sitio genera una clave de intercambio de sitio para comunicarse con otros sitios. La clave de intercambio de sitio del sitio de nivel superior de la jerarquía se denomina clave raíz confiable.  

La función de la clave raíz confiable en Configuration Manager es similar a un certificado raíz en una infraestructura de clave pública. Todo lo que esté firmado por la clave privada de la clave raíz confiable se considerará confiable en los niveles inferiores de la jerarquía. Los clientes almacenan una copia de la clave raíz confiable en el espacio de nombres de WMI **root\ccm\locationservices**. 

Por ejemplo, el sitio emite un certificado para el punto de administración, que lo firma con la clave privada de la clave raíz confiable. El sitio comparte con los clientes la clave pública de su clave raíz confiable. Después, los clientes pueden distinguir entre los puntos de administración que están en su jerarquía y los que no.   

Los clientes recuperan automáticamente la copia pública de la clave raíz confiable mediante dos mecanismos:  

- Se extiende el esquema de Active Directory para Configuration Manager, y el sitio se publica en Active Directory Domain Services. Después, los clientes recuperan la información de este sitio desde un servidor de catálogo global. Para más información, vea [Preparar Active Directory para la publicación de sitios](../network/extend-the-active-directory-schema.md).  

- Al instalar los clientes mediante el método de instalación de inserción de cliente. Para obtener más información, vea [Instalación de inserción de cliente](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

Si los clientes no pueden recuperar la clave raíz confiable mediante uno de estos mecanismos, confiarán en la clave raíz confiable proporcionada por el primer punto de administración con el que se comuniquen. En este escenario, un cliente podría ser dirigido erróneamente al punto de administración de un atacante, donde recibiría una directiva del punto de administración no autorizado. Esta acción requiere un atacante sofisticado. Este ataque se limita al breve periodo antes de que el cliente recupere la clave raíz confiable desde un punto de administración válido. Para reducir el riesgo de que un atacante dirija erróneamente a los clientes a un punto de administración no autorizado, aprovisione los clientes previamente con la clave raíz confiable.  

Use los siguientes procedimientos para aprovisionar previamente un cliente de Configuration Manager y comprobar su clave raíz confiable:  

- [Aprovisionamiento previo de un cliente con la clave raíz confiable mediante un archivo](#bkmk_trk-provision-file)  

- [Aprovisionamiento previo de un cliente con la clave raíz confiable sin usar un archivo](#bkmk_trk-provision-nofile)  

- [Comprobación de la clave raíz confiable de un cliente](#bkmk_trk-verify)  

- [Eliminación o reemplazo de la clave raíz confiable](#bkmk_trk-reset)  

  > [!NOTE]  
  > Si los clientes pueden obtener la clave raíz confiable de Active Directory Domain Services o la inserción de cliente, no tendrá que realizar el aprovisionamiento previo. 
  > 
  > Cuando los clientes usan la comunicación HTTPS con los puntos de administración, no tendrá que aprovisionar previamente la clave raíz confiable. Establecen la confianza mediante el uso de los certificados PKI.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a> Aprovisionamiento previo de un cliente con la clave raíz confiable mediante un archivo  

1.  En el servidor de sitio, abra el archivo siguiente en un editor de texto: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Busque la entrada, **SMSPublicRootKey=** . Copie la clave de esa línea y cierre el archivo sin realizar ningún cambio.  

3.  Cree un nuevo archivo de texto y pegue la información de la clave copiada del archivo mobileclient.tcf.  

4.  Guarde el archivo en una ubicación donde todos los equipos tengan acceso a él, pero donde esté protegido para evitar alteraciones.  

5.  Instale el cliente mediante cualquier método de instalación que acepte las propiedades de client.msi. Especifique la propiedad siguiente: `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > Cuando se especifica la clave raíz confiable durante la instalación de cliente, especifique también el código de sitio. Use la propiedad de client.msi siguiente: `SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a> Aprovisionamiento previo de un cliente con la clave raíz confiable sin usar un archivo  

1.  En el servidor de sitio, abra el archivo siguiente en un editor de texto: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Busque la entrada, **SMSPublicRootKey=** . Copie la clave de esa línea y cierre el archivo sin realizar ningún cambio.  

3.  Instale el cliente mediante cualquier método de instalación que acepte las propiedades de client.msi. Especifique la propiedad de client.msi siguiente: `SMSPublicRootKey=<key>` donde `<key>` es la cadena que se ha copiado de mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Cuando se especifica la clave raíz confiable durante la instalación de cliente, especifique también el código de sitio. Use la propiedad de client.msi siguiente: `SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a> Comprobación de la clave raíz confiable de un cliente  

1. Abra una consola de Windows PowerShell como administrador.  

2. Ejecute el comando siguiente:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

La cadena devuelta es la clave raíz confiable. Compruebe que coincide con el valor de **SMSPublicRootKey** del archivo mobileclient.tcf en el servidor de sitio.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a> Eliminación o reemplazo de la clave raíz confiable  

Quite la clave raíz confiable de un cliente mediante la propiedad de client.msi **RESETKEYINFORMATION = TRUE**. 

Para reemplazar la clave raíz confiable, vuelva a instalar al cliente junto con la nueva clave raíz confiable. Por ejemplo, use la inserción de cliente, o bien especifique la propiedad de client.msi **SMSPublicRootKey**.  

Para obtener más información sobre estas propiedades de instalación, vea [Acerca de los parámetros y propiedades de instalación de cliente](../../clients/deploy/about-client-installation-properties.md).



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Planear la firma y el cifrado  
 
Cuando se usan certificados PKI para todas las comunicaciones de cliente, no es necesario planear la firma y el cifrado para proteger la comunicación de datos de cliente. Si configura sistemas de sitio que ejecutan IIS para permitir las conexiones de cliente HTTP, decida cómo proteger la comunicación de cliente del sitio.  

Para proteger los datos que los clientes envían a los puntos de administración, puede requerir que los clientes firmen los datos. También puede requerir el algoritmo SHA-256 para la firma. Esta configuración es más segura, pero no requiera SHA-256 a menos que todos los clientes lo admitan. Muchos sistemas operativos admiten este algoritmo de forma nativa, pero es posible que en sistemas operativos anteriores se necesite una actualización o revisión. 

Aunque la firma permite proteger los datos contra la manipulación, el cifrado permite protegerlos contra la divulgación de información. Puede habilitar el cifrado 3DES para los mensajes de estado y datos de inventario que los clientes envían a los puntos de administración del sitio. No es necesario instalar ninguna actualización en los clientes para admitir esta opción. Los clientes y los puntos de administración requieren el uso de CPU adicionales para cifrado y descifrado.  

Para obtener más información sobre cómo configurar las opciones para la firma y el cifrado, vea [Configurar la firma y el cifrado](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Planear la administración basada en roles  

Para obtener más información, vea [Aspectos básicos de la administración basada en roles](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a> Planeación de Azure Active Directory

Configuration Manager se integra con Azure Active Directory (Azure AD) para permitir que el sitio y los clientes usen la autenticación moderna. La incorporación del sitio con Azure AD admite los siguientes escenarios de Configuration Manager:

**Cliente**  

- [Administración de clientes en Internet a través de Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Administración de los dispositivos unidos a un dominio en la nube](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Administración conjunta](../../../comanage/overview.md)  

- [Implementación de aplicaciones disponibles para el usuario](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Aplicaciones en línea de Microsoft Store para Empresas](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Reduzca los requisitos de infraestructura. Por ejemplo, [Centro de software con el punto de administración](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) en lugar del catálogo de aplicaciones  

- [Administrar Aplicaciones de Microsoft 365 para empresas](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Servidor**  

- [Análisis de escritorio](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [Centro de comunidad](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Punto de distribución de nube](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Detección de usuarios](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Para obtener más información sobre cómo conectar el sitio a Azure AD, vea [Configuración de servicios de Azure](../../servers/deploy/configure/azure-services-wizard.md).


Para obtener más información sobre Azure AD, vea la [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a> Plan para la autenticación del proveedor de SMS
<!--1357013--> 

A partir de la versión 1810, puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. Se aplica a todos los componentes que acceden al proveedor de SMS. Por ejemplo, la consola de Configuration Manager, los métodos del SDK y los cmdlets de Windows PowerShell. 

Esta opción es una configuración de toda la jerarquía. Antes de cambiar esta configuración, asegúrese de que todos los administradores de Configuration Manager pueden iniciar sesión en Windows con el nivel de autenticación requerido. 

Están disponibles los siguientes niveles:

- **Autenticación de Windows**: requiere la autenticación con credenciales de dominio de Active Directory.   

- **Autenticación de certificado**: requiere la autenticación con un certificado válido emitido por una entidad de certificación PKI de confianza.  

- **Autenticación de Windows Hello para empresas**: requiere la autenticación sólida en dos fases vinculada a un dispositivo y usa biometrías o un PIN.  

Para más información, vea [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth) (Planear el proveedor de SMS). 



## <a name="see-also"></a>Vea también
- [Seguridad y privacidad para los clientes de Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurar la seguridad](configure-security.md)  

- [Comunicaciones entre puntos de conexión](../hierarchy/communications-between-endpoints.md)  

- [Referencia técnica de controles criptográficos](cryptographic-controls-technical-reference.md)  

- [Requisitos de certificados PKI](../network/pki-certificate-requirements.md)  

