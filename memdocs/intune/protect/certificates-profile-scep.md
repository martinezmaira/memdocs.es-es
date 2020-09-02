---
title: 'Uso de perfiles de certificado SCEP con Microsoft Intune: Azure | Microsoft Docs'
description: Cree y asigne perfiles de certificado de Protocolo de inscripción de certificados simple (SCEP) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5126f2e5cc145e864fb4f56e472dba7a5179540f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915592"
---
# <a name="create-and-assign-scep-certificate-profiles-in-intune"></a>Creación y asignación de perfiles de certificado SCEP en Intune

Después de [configurar la infraestructura](certificates-scep-configure.md) para admitir certificados de Protocolo de inscripción de certificados simple (SCEP), puede crear y luego asignar perfiles de certificado SCEP a usuarios y dispositivos en Intune.

> [!IMPORTANT]
> Para que los dispositivos usen un perfil de certificado SCEP, deben confiar en la entidad de certificación (CA) raíz de confianza. La confianza de la entidad de certificación raíz se establece mejor si se implementa un [perfil de certificado de confianza](../protect/certificates-configure.md#create-trusted-certificate-profiles) en el mismo grupo que recibe el perfil de certificado SCEP. Los perfiles de certificado de confianza aprovisionan el certificado de entidad de certificación raíz de confianza.

## <a name="create-a-scep-certificate-profile"></a>Creación de un perfil de certificado SCEP

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione y vaya a **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Escriba las propiedades siguientes:
   - **Plataforma**: seleccione la plataforma de los dispositivos.
   - **Perfil**: Seleccione **SCEP certificate** (Certificado SCEP).

     Para la plataforma **Android Enterprise**, *Tipo de perfil* se divide en dos categorías: *Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado* y *Solo perfil de trabajo*. Asegúrese de seleccionar el perfil de certificado de SCEP correcto para los dispositivos que administra.  

     Los perfiles de certificado SCEP para el *Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado* tienen las limitaciones siguientes:

      1. En Supervisión, la creación de informes de certificados no está disponible para los perfiles de certificado de SCEP de propietario del dispositivo.

      2. Intune no se puede usar para revocar certificados aprovisionados por perfiles de certificado SCEP para los propietarios de dispositivos. La revocación se puede administrar a través de un proceso externo o directamente con la entidad de certificación.

      3. En el caso de dispositivos Android Enterprise dedicados, los perfiles de certificado SCEP solo se admiten para la configuración de red Wi-Fi, VPN y la autenticación. Los perfiles de certificado SCEP en dispositivos Android Enterprise dedicados no se admiten para la autenticación de aplicación.

4. Seleccione **Crear**.

5. En **Básico**, escriba las propiedades siguientes:
   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil sería *Perfil de SCEP en toda la empresa*.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. Seleccione **Configuración** y, después, realice las siguientes configuraciones:

   - **Tipo de certificado**:

     *(Se aplica a:  Android, Android Enterprise, iOS/iPadOS, macOS, Windows 8.1 y versiones posteriores, y Windows 10 y versiones posteriores).*

     Seleccione un tipo en función de cómo vaya a usar el perfil de certificado:

     - **Usuario**: los certificados *Usuario* pueden contener atributos de usuario y dispositivo en el asunto y SAN del certificado.  
     - **Dispositivo**:  Los certificados *Dispositivo* solo pueden contener atributos de dispositivo en el asunto y SAN del certificado.

       Use **Dispositivo** para escenarios como, por ejemplo, dispositivos sin usuario (como quioscos) o dispositivos Windows. En los dispositivos Windows, el certificado se coloca en el almacén de certificados del equipo local.

     > [!NOTE]
     > En macOS, los certificados que se aprovisionan con SCEP siempre se colocan en la cadena de claves del sistema (almacén del sistema) del dispositivo.
 
   - **Formato de nombre del sujeto**:

     seleccione cómo Intune crea automáticamente el nombre del sujeto en la solicitud de certificado. Las opciones para el formato de nombre del firmante dependen del tipo de certificado que seleccione: **Usuario** o **Dispositivo**.

     > [!NOTE]
     > Existe un [problema conocido](#avoid-certificate-signing-requests-with-escaped-special-characters) en el uso de SCEP para obtener certificados cuando el nombre del firmante en la solicitud de firma de certificado (CSR) resultante incluye uno de los siguientes caracteres como carácter de escape (precedido por una barra diagonal inversa \\):
     > - \+
     > - ;
     > - ,
     > - =

     - **Tipo de certificado de usuario**

       Las opciones de formato para el *Formato de nombre del firmante* incluyen las siguientes:

       - **No configurado**.
       - **Nombre común**
       - **Nombre común, incluyendo la dirección de correo electrónico**
       - **Nombre común como correo electrónico**
       - **IMEI (Identidad de equipo móvil internacional)**
       - **Número de serie**
       - **Personalizado**: cuando se selecciona esta opción, se muestra también un cuadro de texto **Personalizado**. Use este campo para escribir un formato de nombre del firmante personalizado, incluidas las variables. El formato personalizado admite dos variables: **Nombre común (CN)** y **dirección de correo electrónico (E)** . **Nombre común (CN)** se puede establecer en cualquiera de las siguientes variables:

         - **CN={{UserName}}** : nombre de usuario del usuario, como janedoe.
         - **CN={{UserPrincipalName}}** : nombre principal de usuario del usuario, como janedoe@contoso.com.\*
         - **CN={{AAD_Device_ID}}** : identificador asignado al registrar un dispositivo en Azure Active Directory (AD). Este identificador normalmente se usa para autenticarse en Azure AD.
         - **CN={{SERIALNUMBER}}** : número de serie (SN) único que normalmente usa el fabricante para identificar un dispositivo.
         - **CN={{IMEINumber}}** : número exclusivo de identidad de equipo móvil internacional (IMEI) usado para identificar un teléfono móvil.
         - **CN={{OnPrem_Distinguished_Name}}** : Secuencia de nombres distintivos relativos separados por comas, como *CN=Jane Doe,OU=UserAccounts,DC=corp,DC=contoso,DC=com*.

           Para usar la variable *{{OnPrem_Distinguished_Name}}* , asegúrese de sincronizar el atributo de usuario *onpremisesdistinguishedname* mediante [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) con la instancia de Azure AD.

         - **CN={{onPremisesSamAccountName}}** : los administradores pueden sincronizar el atributo samAccountName de Active Directory con Azure AD mediante Azure AD Connect en un atributo llamado *onPremisesSamAccountName*. Intune puede sustituir esa variable como parte de una solicitud de emisión de certificado en el asunto de un certificado. El atributo samAccountName es el nombre de inicio de sesión del usuario que se utiliza para admitir clientes y servidores de una versión anterior de Windows (anterior a Windows 2000). El formato de nombre de inicio de sesión de usuario es el siguiente: *NombreDeDominio\usuario de prueba*, o bien solo *usuario de prueba*.

            Para usar la variable *{{onPremisesSamAccountName}}* , asegúrese de sincronizar el atributo de usuario *onPremisesSamAccountName* mediante [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) con la instancia de Azure AD.

         Mediante una combinación de una o muchas de estas variables y cadenas estáticas, puede crear un formato de nombre de firmante personalizado como este:  
         - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**

         Ese ejemplo incluye un formato de nombre de firmante en el que se usan las variables CN y E, y cadenas para los valores Unidad organizativa, Organización, Ubicación, Estado y País. [CertStrToName](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea) describe esta función y sus cadenas admitidas.
         
         \* En el caso de los perfiles de Android Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado, el valor **CN={{UserPrincipalName}}** no funcionará. Los perfiles de Android Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado se pueden usar con dispositivos sin usuario, por lo que este perfil no podrá obtener el nombre principal de usuario del usuario. Si realmente necesita esta opción para dispositivos con usuarios, puede usar una solución alternativa como la siguiente: **CN={{NombreDeUsuario}}\@contoso.com**. Proporcionará el nombre de usuario y el dominio que haya agregado manualmente, como janedoe@contoso.com.

      - **Tipo de certificado de dispositivo**

        Las opciones de formato para el formato de nombre del firmante incluyen las variables siguientes:

        - **{{AAD_Device_ID}}** o **{{AzureADDeviceId}}** : cualquiera de las variables se puede usar para identificar un dispositivo por su identificador de Azure AD.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}** *(Solo aplicable para dispositivos Windows y unidos a dominio)*
        - **{{MEID}}**

        Puede especificar estas variables, seguidas del texto de la variable, en el cuadro de texto. Por ejemplo, el nombre común de un dispositivo denominado *Dispositivo1* se puede agregar como **CN={{DeviceName}}Dispositivo1**.

        > [!IMPORTANT]
        > - Al especificar una variable, incluya el nombre de la variable entre corchetes { } como se muestra en el ejemplo, para evitar un error.  
        > - Una persona con acceso al dispositivo podría suplantar las propiedades del dispositivo que se usan en el *asunto* o *SAN*, como **IMEI**, **SerialNumber** y **FullyQualifiedDomainName**.
        > - Un dispositivo debe admitir todas las variables especificadas en un perfil de certificado para que ese perfil se instale en ese dispositivo.  Por ejemplo, si se usa **{{IMEI}}** en el nombre del firmante de un perfil SCEP y se asigna a un dispositivo que no tiene un número IMEI, se producirá un error en la instalación del perfil.

   - **Nombre alternativo del firmante**: seleccione cómo Intune crea de forma automática el nombre alternativo del firmante (SAN) en la solicitud de certificado. Las opciones para el formato de SAN dependen del tipo de certificado que haya seleccionado: **Usuario** o **Dispositivo**.

      - **Tipo de certificado de usuario**

        Seleccione entre los atributos disponibles:

        - **Dirección de correo electrónico**
        - **Nombre principal de usuario (UPN)**

        Por ejemplo, los tipos de certificado de usuario pueden incluir el nombre principal de usuario (UPN) en el nombre alternativo del firmante. Si un certificado de cliente se usa para autenticar un servidor de directivas de redes, establezca el nombre alternativo del firmante en el UPN.

      - **Tipo de certificado de dispositivo**

        Use la lista desplegable **Atributo** y seleccione un atributo, asigne un **Valor** y **agréguelo** al perfil de certificado. Puede agregar varios valores si selecciona atributos adicionales.

        Entre los atributos disponibles se incluyen los siguientes:

        - **Dirección de correo electrónico**
        - **Nombre principal de usuario (UPN)**
        - **DNS**

        Con el tipo de certificado *Dispositivo*, puede usar estas variables de certificado de dispositivo para el valor:

        - **{{AAD_Device_ID}}** o **{{AzureADDeviceId}}** : cualquiera de las variables se puede usar para identificar un dispositivo por su identificador de Azure AD.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}**
        - **{{MEID}}**

        Para especificar un valor para un atributo, incluya el nombre de la variable entre llaves, seguido del texto de esa variable. Por ejemplo, se puede agregar un valor para el atributo DNS **{{AzureADDeviceId}}.domain.com**, donde *.domain.com* es el texto. Para un usuario llamado *Usuario1*, una dirección de correo electrónico podría aparecer como {{FullyQualifiedDomainName}}User1@Contoso.com.

        > [!IMPORTANT]
        > - Cuando use una variable de certificado de dispositivo, incluya el nombre de la variable entre llaves { }.
        > - No use llaves **{ }** , símbolos de barra vertical **|** ni puntos y coma **;** en el texto que sigue a la variable.
        > - Una persona con acceso al dispositivo podría suplantar las propiedades del dispositivo que se usan en el *asunto* o *SAN*, como **IMEI**, **SerialNumber** y **FullyQualifiedDomainName**.
        > - Un dispositivo debe admitir todas las variables especificadas en un perfil de certificado para que ese perfil se instale en ese dispositivo.  Por ejemplo, si se usa **{{IMEI}}** en el SAN de un perfil SCEP y se asigna a un dispositivo que no tiene un número IMEI, se producirá un error en la instalación del perfil.

   - **Período de validez del certificado**:

     Puede especificar un valor inferior al período de validez de la plantilla de certificado, pero no uno superior. Si ha configurado la plantilla de certificado para [admitir un valor personalizado que se puede establecer desde la consola de Intune](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template), use esta opción para especificar la cantidad de tiempo restante antes de que expire el certificado.

     Por ejemplo, si el período de validez del certificado en la plantilla de certificado es de dos años, puede especificar un valor de un año, pero no un valor de cinco años. El valor también debe ser menor que el período de validez restante del certificado de la CA emisora.

   - **Proveedor de almacenamiento de claves (KSP)** :

     *(Se aplica a:  Windows 8.1 y versiones posteriores, y Windows 10 y versiones posteriores)*

     Especifique dónde se almacena la clave del certificado. Elija entre los valores siguientes:

     - **Inscribirse en KSP Módulo de plataforma segura (TPM) si está presente, si no en KSP Software**
     - **Inscribirse en KSP del Módulo de plataforma segura (TPM) o se producirá un error**
     - **Inscribirse en Passport o se producirá un error (Windows 10 y versiones posteriores)**
     - **Inscribirse en el KSP Software**

   - **Uso de la clave**:

     Seleccione las opciones de uso de la clave para el certificado:

     - **Firma digital**: permite el intercambio de claves solo si una firma digital protege la clave.
     - **Cifrado de clave**: permite el intercambio de claves solo si la clave está cifrada.

   - **Tamaño de la clave (bits)** :

     seleccione el número de bits que contiene la clave.

   - **Algoritmo hash**:

     *(se aplica a Android, Android Enterprise, Windows 8.1 y Windows 10 y versiones posteriores)*

     Seleccione uno de los tipos de algoritmos hash disponibles para usar con este certificado. Seleccione el nivel máximo de seguridad que admiten los dispositivos de conexión.

   - **Certificado raíz**:

     Seleccione el *perfil de certificado de confianza* que ha configurado y asignado antes a los usuarios y dispositivos correspondientes para este perfil de certificado SCEP. El perfil de certificado de confianza se usa para aprovisionar usuarios y dispositivos con el certificado de entidad de certificación raíz de confianza. Para obtener información sobre el perfil de certificado de confianza, vea [Exportación del certificado de entidad de certificación raíz de confianza](certificates-configure.md#export-the-trusted-root-ca-certificate) y [Creación de perfiles de certificado de confianza](certificates-configure.md#create-trusted-certificate-profiles) en *Uso de certificados para la autenticación en Intune*. Si tiene una entidad de certificación raíz y una entidad de certificación emisora, seleccione el perfil de certificado raíz de confianza que valida la segunda.
     > [!NOTE]
     > En dispositivos iOS y iPadOS, si tiene una entidad de certificación raíz y una entidad de certificación emisora, seleccione el perfil de certificado raíz de confianza que valida la segunda. 

   - **Uso mejorado de clave**:

     Agregue valores para la finalidad prevista del certificado. En la mayoría de los casos, el certificado requiere *autenticación de cliente* para que el usuario o dispositivo se pueda autenticar en un servidor. Puede agregar usos de la clave adicionales según sea necesario.

   - **Umbral de renovación (%)** :

     especifique qué porcentaje de la duración del certificado tiene que quedar para que el dispositivo solicite la renovación del certificado. Por ejemplo, si escribe 20, se intentará la renovación del certificado cuando haya caducado al 80 %. Los intentos de renovación proseguirán hasta que la renovación sea correcta. La renovación genera un certificado nuevo, lo que da como resultado un nuevo par de claves pública y privada.

   - **Direcciones URL de servidor SCEP**:

     especifique una o varias direcciones URL para los servidores SCEP que emiten certificados mediante SCEP. Por ejemplo, escriba algo parecido a `https://ndes.contoso.com/certsrv/mscep/mscep.dll`.

     Puede agregar direcciones URL de SCEP adicionales para el equilibrio de carga según sea necesario. Los dispositivos realizan tres llamadas independientes al servidor NDES: para obtener las capacidades de los servidores, para obtener una clave pública y, luego, para enviar una solicitud de firma. Si usa varias direcciones URL, es posible que el equilibrio de carga tenga como resultado que se use una dirección URL diferente para las llamadas posteriores a un servidor NDES. Si se contacta con un servidor diferente para una llamada posterior durante la misma solicitud, se producirá un error en la solicitud.

     El comportamiento para administrar la dirección URL del servidor NDES es específico de cada plataforma de dispositivo:

     - **Android**: el dispositivo aleatoriza la lista de direcciones URL recibidas en la directiva de SCEP y recorre la lista hasta que encuentra un servidor NDES accesible. Después, el dispositivo usa la misma dirección URL y el mismo servidor durante todo el proceso. Si el dispositivo no puede acceder a ninguno de los servidores NDES, se produce un error en el proceso.
     - **iOS/iPadOS**: Intune vuelve a aleatorizar las direcciones URL y proporciona una sola dirección URL a un dispositivo. Si el dispositivo no puede acceder al servidor NDES, se produce un error en la solicitud de SCEP.
     - **Windows**: la lista de direcciones URL de NDES se aleatoriza y, luego, se pasa al dispositivo Windows, que las prueba en el orden recibido hasta encontrar una disponible. Si el dispositivo no puede acceder a ninguno de los servidores NDES, se produce un error en el proceso.

     Si un dispositivo no puede acceder al mismo servidor NDES correctamente durante alguna de las tres llamadas al servidor NDES, se produce un error en la solicitud de SCEP. Esto puede ocurrir, por ejemplo, cuando una solución de equilibrio de carga proporciona una dirección URL diferente para la segunda o la tercera llamada al servidor NDES, o bien cuando proporciona un servidor NDES real distinto en función de una dirección URL virtualizada para NDES. Después de una solicitud con error, el dispositivo intenta llevar a cabo el proceso de nuevo en el siguiente ciclo de la directiva, empezando por la lista aleatorizada de direcciones URL de NDES (o por una dirección URL única para iOS/iPadOS).  

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

   Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione el usuario o los grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

    Seleccione **Siguiente**.

11. (*Se aplica solo a Windows 10*) En **Reglas de aplicación**, especifique las reglas de aplicación para restringir la asignación de este perfil. Puede elegir asignar o no asignar el perfil en función de la edición del sistema operativo o la versión de un dispositivo.

   Para más información, consulte [Reglas de aplicabilidad](../configuration/device-profile-create.md#applicability-rules) en *Creación de un perfil de dispositivo en Microsoft Intune*.

12. En **Revisar y crear**, revise la configuración. Si selecciona Crear, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

### <a name="avoid-certificate-signing-requests-with-escaped-special-characters"></a>Evitar solicitudes de firma de certificado con caracteres de escape especiales

Existe un problema conocido con las solicitudes de certificado SCEP y PKCS que incluyen un nombre del firmante (CN) con uno o varios de los siguientes caracteres especiales como carácter de escape. Los nombres de firmante que incluyen uno de los caracteres especiales como un carácter de escape dan como resultado un CSR con un nombre de firmante incorrecto. Un nombre de sujeto incorrecto produce un error de validación de desafío de SCEP de Intune y no se emite ningún certificado.

Los caracteres especiales son:
- \+
- ,
- ;
- =

Cuando el nombre del firmante incluya uno de los caracteres especiales, use una de las siguientes opciones para solucionar esta limitación:

- Encapsula el valor de CN que contiene el carácter especial entre comillas.  
- Quite el carácter especial del valor de CN.

**Por ejemplo**, tiene un nombre del firmante que aparece como *Test User (TestCompany, LLC*).  Un CSR que incluya un CN con la coma entre *TestCompany* y *LLC* presenta un problema.  Para evitar el problema se puede poner el CN entero ente comillas o se puede quitar la coma que hay entre *TestCompany* y *LLC*:

- **Agregar comillas**: *CN="Test User (TestCompany, LLC)",OU=UserAccounts,DC=corp,DC=contoso,DC=com*
- **Quitar la coma**: *CN=Test User (TestCompany LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

 Sin embargo, al intentar usar un carácter de barra diagonal inversa para escapar la coma, se producirá un error en los registros de CRP:
 
- **Coma de escape**: *CN=Test User (TestCompany\\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

El error es similar al siguiente:

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## <a name="assign-the-certificate-profile"></a>Asignar el perfil de certificado

Los perfiles de certificado SCEP se asignan de la misma manera que [se implementan perfiles de dispositivo](../configuration/device-profile-assign.md) para otros fines.

Para usar un perfil de certificado SCEP, un dispositivo debe haber recibido también el perfil de certificado de confianza que lo aprovisiona con el certificado de entidad de certificación raíz de confianza. Se recomienda implementar el perfil de certificado raíz de confianza y el perfil de certificado SCEP. en los mismos grupos.

Antes de continuar, tenga en cuenta lo siguiente:

- Cuando asigna perfiles de certificado SCEP a grupos, el archivo de certificado de la entidad de certificación raíz de confianza (según lo especificado en el *perfil de certificado de confianza*) se instala en el dispositivo. El dispositivo usa el perfil de certificado SCEP para crear una solicitud de certificado para ese certificado de entidad de certificación raíz de confianza.

- El perfil de certificado SCEP solo se instala en los dispositivos que ejecutan la plataforma que ha especificado al crear el perfil de certificado.

- Puede asignar perfiles de certificado en recopilaciones de usuarios o en recopilaciones de dispositivos.

- Para publicar rápidamente un certificado en un dispositivo una vez inscrito el dispositivo, asigne el perfil de certificado en un grupo de usuarios (no en un grupo de dispositivos). Si lo asigna en un grupo de dispositivos, deberá efectuar un registro completo del dispositivo para que el dispositivo reciba directivas.

- Si usa la administración conjunta para Intune y Configuration Manager, en Configuration Manager, [establezca el control deslizante de la carga de trabajo](/configmgr/comanage/how-to-switch-workloads) de las directivas de acceso a los recursos en **Intune** o **Intune piloto**. Esta configuración permite que los clientes de Windows 10 inicien el proceso de solicitar el certificado.

> [!NOTE]
> - En los dispositivos iOS/iPadOS, cuando hay un perfil de certificado SCEP o PKCS asociado con un perfil adicional, como uno de Wi-Fi o VPN, el dispositivo recibe un certificado para cada uno de esos perfiles adicionales. Esto hace que la solicitud de certificado SCEP o PKCS entregue varios certificados al dispositivo iOS/iPadOS. 
> 
>   Los certificados entregados por SCEP son únicos. Los certificados entregados por PKCS son el mismo certificado, pero aparecen de forma distinta, ya que cada instancia de perfil se representa mediante una línea independiente en el perfil de administración.
> - En iOS 13 y macOS 10.15, hay algunos [requisitos de seguridad adicionales documentados por Apple](https://support.apple.com/HT210176) que se deben tener en cuenta.  


## <a name="next-steps"></a>Pasos siguientes

[Asignación de perfiles](../configuration/device-profile-assign.md)

[Solución de problemas de implementación de perfiles de certificado SCEP](../protect/troubleshoot-scep-certificate-profiles.md)