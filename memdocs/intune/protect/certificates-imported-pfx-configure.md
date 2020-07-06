---
title: 'Uso de certificados PFX importados en Microsoft Intune: Azure | Microsoft Docs'
description: Use certificados PKCS (Public Key Cryptography Standards) con Microsoft Intune. Importe certificados, configure plantillas de certificado, instale el conector de certificado PFX importado de Intune y cree un perfil de certificado PKCS importado.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/29/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda; rimarram
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bf55564cabce9a060c15100ad974c59bf858b15
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85591126"
---
# <a name="configure-and-use-imported-pkcs-certificates-with-intune"></a>Configuración y uso de certificados PKCS importados con Intune

Microsoft Intune admite el uso de certificados de pares de claves públicas (PKCS) importados, que se suelen usar para el cifrado S/MIME con perfiles de correo electrónico. Algunos perfiles de correo electrónico de Intune admiten una opción para habilitar S/MIME, donde puede definir un certificado de firma S/MIME y el certificado de cifrado S/MIME.

El cifrado S/MIME es complejo porque el correo electrónico está cifrado con un certificado específico:

- Debe tener la clave privada del certificado que cifró el correo electrónico en el dispositivo en el que lee el correo electrónico para que se pueda descifrar.
- Antes de que expire un certificado de un dispositivo, debe importar un nuevo certificado para que los dispositivos puedan continuar descifrando el correo electrónico nuevo. No se permite la renovación de estos certificados.
- Los certificados de cifrado se renuevan con regularidad, lo que significa que es posible que quiera conservar el certificado anterior en los dispositivos para asegurarse de que el correo electrónico antiguo se pueda seguir descifrando.  

Dado que se debe usar el mismo certificado en todos los dispositivos, no es posible usar perfiles de certificado [SCEP](certificates-scep-configure.md) o [PKCS](certficates-pfx-configure.md) para este propósito, ya que los mecanismos de entrega de certificados proporcionan certificados únicos por dispositivo.

Para más información sobre el uso de S/MIME con Intune, consulte [Uso de S/MIME para cifrar el correo electrónico](certificates-s-mime-encryption-sign.md).

## <a name="supported-platforms"></a>Plataformas compatibles

Intune admite la importación de certificados PFX para las plataformas siguientes:

- Android: Administrador de dispositivos
- Android Enterprise: Totalmente administrado
- Android Enterprise: Perfil de trabajo
- iOS/iPadOS
- macOS
- Windows 10

## <a name="requirements"></a>Requisitos

Para usar certificados PKCS importados con Intune, debe contar con esta infraestructura:

- **Conector de certificado PFX para Microsoft Intune**:

  Cada inquilino de Intune admite una única instancia de este conector. Puede instalar este conector en el mismo servidor que una instancia de Microsoft Intune Certificate Connector.

  El conector controla las solicitudes de archivos PFX importados en Intune para el cifrado de correo electrónico S/MIME para un usuario específico.

  Este conector pueda actualizarse automáticamente cuando estén disponibles nuevas versiones. Para utilizar la funcionalidad de actualización, asegúrese de que los firewalls están abiertos para permitir que el conector se ponga en contacto con **autoupdate.msappproxy.net** en el puerto **443**.

  Para más información, vea [Puntos de conexión de red de Microsoft Intune](../fundamentals/intune-endpoints.md) y [Ancho de banda y requisitos de configuración de red de Intune](../fundamentals/network-bandwidth-use.md).

- **Windows Server**:

  Utilice una instancia de Windows Server para hospedar el conector de certificado PFX para Microsoft Intune.  El conector se usa para procesar solicitudes de los certificados importados a Intune.
  
  El conector requiere acceso a los mismos puertos que se han detallado para los dispositivos administrados, como se indica en el [contenido de punto de conexión de dispositivo](https://docs.microsoft.com/intune/fundamentals/intune-endpoints#access-for-managed-devices).

  Intune admite la instalación de *Microsoft Intune Certificate Connector* en el mismo servidor que el *conector de certificado PFX para Microsoft Intune*.

  Para admitir el conector, el servidor debe ejecutar .NET Framework 4.6, o una versión posterior. Si .NET Framework 4.6 no está instalado al iniciar la instalación del conector, se instalará automáticamente con el conector.

- **Visual Studio 2015 o posterior** (opcional):

  Use Visual Studio para compilar el módulo asistente de PowerShell con cmdlets para la importación de certificados PFX en Microsoft Intune. Para obtener los cmdlets de PowerShell del asistente, consulte [PFXImport PowerShell Project en GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="how-it-works"></a>Cómo funciona

Al utilizar Intune para implementar un **certificado PFX importado** para un usuario, hay dos componentes en juego además del dispositivo:

- **Servicio Intune**: Almacena los certificados PFX en un estado cifrado y controla la implementación del certificado en el dispositivo del usuario.  Las contraseñas que protegen las claves privadas de los certificados se cifran antes de que se carguen mediante un módulo de seguridad de hardware (HSM) o la criptografía de Windows, asegurándose de que Intune no pueda acceder a la clave privada en ningún momento.

- **Conector de certificado PFX para Microsoft Intune**: Cuando un dispositivo solicita un certificado PFX que se importó en Intune, la contraseña cifrada, el certificado y la clave pública del dispositivo se envían al conector.  El conector descifra la contraseña mediante la clave privada local y, a continuación, vuelve a cifrar la contraseña (y cualquier perfil de archivo plist si usa iOS) con la clave del dispositivo antes de volver a enviar el certificado a Intune.  Intune envía entonces el certificado al dispositivo y este puede descifrarlo con la clave privada del dispositivo e instalar el certificado.

## <a name="download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune"></a>Descarga, instalación y configuración del conector de certificado PFX para Microsoft Intune

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Administración de inquilinos** > **Conectores y tokens** > **Conectores de certificados** > **Agregar**.

   ![Descarga del conector de certificado PFX para Microsoft Intune](./media/certificates-imported-pfx-configure/download-imported-pfxconnector.png)

3. Siga las instrucciones para descargar el *conector de certificado PFX para Microsoft Intune* a una ubicación a la que se pueda acceder desde el servidor donde va a instalar el conector.

4. Una vez finalizada la descarga, inicie sesión en el servidor y ejecute el instalador (PfxCertificateConnectorBootstrapper.exe).  
   - Cuando acepta la ubicación de instalación predeterminada, el conector se instala en `Program Files\Microsoft Intune\PFXCertificateConnector`.
   - El servicio de conector se ejecuta en la cuenta de sistema local. Si se requiere un servidor proxy para el acceso a Internet, confirme que la cuenta de servicio local puede acceder a la configuración de proxy en el servidor.

5. El Conector de certificado PFX para Microsoft Intune se abre en la pestaña **Inscripción** después de la instalación. Para habilitar la conexión con Intune, **inicie sesión**, y escriba una cuenta con permisos de administrador global de Azure o de Intune.

   > [!WARNING]
   > De forma predeterminada, en Windows Server, la opción **Configuración de seguridad mejorada de Internet Explorer** está establecida en **Activada**, lo que puede causar problemas con el inicio de sesión en Office 365.

6. Cierre la ventana.

7. En el Centro de administración de Microsoft Endpoint Manager, vuelva a **Administración de inquilinos** > **Conectores y tokens** > **Conectores de certificado**. En unos minutos, se muestra una marca de verificación verde y se actualiza el estado de la conexión. El servidor del conector puede comunicarse ahora con Intune.

## <a name="import-pfx-certificates-to-intune"></a>Importación de certificados PFX en Intune

Use [Microsoft Graph](https://docs.microsoft.com/graph) para importar los certificados PFX de los usuarios en Intune. El asistente [PFXImport PowerShell Project en GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell) proporciona cmdlets para realizar las operaciones con facilidad.

Si prefiere usar su propia solución personalizada con Graph, use el [tipo de recurso userPFXCertificate](https://docs.microsoft.com/graph/api/resources/intune-raimportcerts-userpfxcertificate?view=graph-rest-beta).

### <a name="build-pfximport-powershell-project-cmdlets"></a>Compilación de cmdlets de "PFXImport PowerShell Project"

Para usar los cmdlets de PowerShell, puede compilar el proyecto con Visual Studio. El proceso es sencillo y, mientras puede ejecutarse en el servidor, se recomienda ejecutarlo en la estación de trabajo.  

1. Vaya a la raíz del repositorio [Intune-Resource-Access](https://github.com/microsoft/Intune-Resource-Access) en GitHub y, a continuación, descargue o clone el repositorio con Git en la máquina.

   ![Botón de descarga de GitHub](./media/certificates-imported-pfx-configure/github-download.png)

2. Vaya a `.\Intune-Resource-Access-develop\src\PFXImportPowershell\` y abra el proyecto con Visual Studio mediante el archivo **PFXImportPS.sln**.

3. En la parte superior, cambie de **Depurar** a **Liberar**.

4. Vaya a **Compilar** y seleccione **Build PFXImportPS**. En unos instantes, verá que aparece un mensaje de confirmación de **Compilación correcta** en la parte inferior izquierda de Visual Studio.

   ![Opción de compilación de Visual Studio](./media/certificates-imported-pfx-configure/vs-build-release.png)

5. En el proceso de compilación se crea una nueva carpeta con el módulo de PowerShell en `.\Intune-Resource-Access-develop\src\PFXImportPowershell\PFXImportPS\bin\Release`.

   Usará la carpeta **Release** para los pasos siguientes.

### <a name="create-the-encryption-public-key"></a>Creación de la clave pública de cifrado

Importe los certificados PFX y sus claves privadas a Intune. La contraseña que protege la clave privada se cifra con una clave pública, que se almacena de forma local. Puede usar la criptografía de Windows, un módulo de seguridad de hardware u otro tipo de criptografía para generar y almacenar los pares de claves pública y privada.  Según el tipo de cifrado utilizado, el par de claves pública y privada se puede exportar en un formato de archivo para realizar copias de seguridad.

El módulo de PowerShell proporciona métodos para crear una clave mediante la criptografía de Windows. También puede usar otras herramientas para crear una clave.  

#### <a name="to-create-the-encryption-key-using-windows-cryptography"></a>Para crear la clave de cifrado mediante la criptografía de Windows

1. Copie la carpeta *Release* creada por Visual Studio en el servidor donde instaló el **conector de certificado PFX para Microsoft Intune**. Este carpeta contiene el módulo de PowerShell.

2. En el servidor, abra *PowerShell* como administrador y vaya a la carpeta *Release* que contiene el módulo de PowerShell.

3. Para importar el módulo, ejecute `Import-Module .\IntunePfxImport.psd1`.

4. A continuación, ejecute `Add-IntuneKspKey -ProviderName "Microsoft Software Key Storage Provider" -KeyName "PFXEncryptionKey"`.

   > [!TIP]
   > El proveedor que usa debe volver a seleccionarse al importar los certificados PFX. Puede utilizar el **proveedor de almacenamiento de claves de software de Microsoft**, aunque también puede usar otro proveedor. Como ejemplo, también se proporciona el nombre de clave y puede usar el nombre de clave diferente de su elección.

   Si tiene previsto importar el certificado desde la estación de trabajo, puede exportar esta clave a un archivo con el comando `Export-IntunePublicKey -ProviderName "<ProviderName>" -KeyName "<KeyName>" -FilePath "<File path\Filename.PFX>"`.

   Se debe importar la clave privada en el servidor que hospeda el conector de certificado PFX para Microsoft Intune para que los certificados PFX importados se puedan procesar correctamente.

#### <a name="to-use-a-hardware-security-module-hsm"></a>Para usar un módulo de seguridad de hardware (HSM)

Puede usar un módulo de seguridad de hardware (HSM) para generar y almacenar el par de claves pública y privada. Para más información, consulte la documentación del proveedor de HSM.

### <a name="import-pfx-certificates"></a>Importación de certificados PFX

En el proceso siguiente se usan los cmdlets de PowerShell como ejemplo de cómo importar los certificados PFX. Puede elegir distintas opciones en función de sus necesidades.

Las opciones son:

- Propósito planteado (agrupa los certificados basados en una etiqueta):
  - unassigned
  - smimeEncryption
  - smimeSigning

- Esquema de relleno:
  - oaepSha256
  - oaepSha384
  - oaepSha512

Seleccione el proveedor de almacenamiento de claves que coincida con el proveedor que utilizó para crear la clave.

#### <a name="to-import-the-pfx-certificate"></a>Para importar el certificado PFX  

1. Exporte los certificados desde cualquier entidad de certificación siguiendo la documentación del proveedor.  Para los Servicios de certificados de Microsoft Active Directory, puede usar [este script de ejemplo](https://gallery.technet.microsoft.com/Export-CMPfxCertificatesFro-d55f687b).

2. En el servidor, abra *PowerShell* como administrador y vaya a la carpeta *Release* que contiene el módulo de PowerShell.

3. Para importar el módulo, ejecute `Import-Module .\IntunePfxImport.psd1`.

4. Para autenticarse en Graph de Intune, ejecute `Set-IntuneAuthenticationToken  -AdminUserName "<Admin-UPN>"`.

   > [!NOTE]
   > Como la autenticación se ejecuta en Graph, debe proporcionar permisos a AppID. Si es la primera vez que usa esta utilidad, se requiere un *administrador global*. Los cmdlets de PowerShell usan el mismo AppID que el que se usa con los [ejemplos de Intune de PowerShell](https://github.com/microsoftgraph/powershell-intune-samples).

5. Convierta la contraseña de cada archivo PFX que se va a importar en una cadena segura mediante la ejecución de `$SecureFilePassword = ConvertTo-SecureString -String "<PFXPassword>" -AsPlainText -Force`.

6. Para crear un objeto **UserPFXCertificate**, ejecute `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>"`.

   Por ejemplo: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "C:\temp\userA.pfx" $SecureFilePassword "userA@contoso.com" "Microsoft Software Key Storage Provider" "PFXEncryptionKey" "smimeEncryption"`

   > [!NOTE]
   > Cuando importe el certificado desde un sistema que no sea el servidor en el que está instalado el conector, tiene que usar el comando siguiente, que incluye la ruta de acceso del archivo de claves `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>" "<PaddingScheme>" "<File path to public key file>"`.
   >
   > El valor *VPN* no se admite como IntendedPurpose. 


7. Importe el objeto **UserPFXCertificate** a Intune mediante la ejecución de `Import-IntuneUserPfxCertificate -CertificateList $userPFXObject`.

8. Para validar que el certificado se ha importado, ejecute `Get-IntuneUserPfxCertificate -UserList "<UserUPN>"`.

9.  Ejecute `Remove-IntuneAuthenticationToken` para llevar a cabo el procedimiento recomendado a fin de limpiar la memoria caché de tokens de AAD sin esperar a que expire.

Para más información sobre otros comandos disponibles, consulte el archivo Léame en [PFXImport PowerShell Project en GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="create-a-pkcs-imported-certificate-profile"></a>Creación de un perfil de certificado PKCS importado

Después de importar los certificados en Intune, cree un perfil de **certificado PKCS importado** y asígnelo a los grupos de Azure Active Directory.

> [!NOTE]
> Después de crear un perfil de certificado PKCS importado, los valores **Propósito planteado** y **Proveedor de almacenamiento de claves** (KSP) del perfil son de solo lectura y no se pueden editar. Si necesita un valor diferente para cualquiera de estas opciones, cree e implemente un nuevo perfil. 

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione y vaya a **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Escriba las propiedades siguientes:
   - **Plataforma**: seleccione la plataforma de los dispositivos.
   - **Perfil**: seleccione **PKCS imported certificate** (Certificado PKCS importado).

4. Seleccione **Crear**.

5. En **Básico**, escriba las propiedades siguientes:
   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es *Perfil de certificado PKCS importado en toda la empresa*.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En **Opciones de configuración**, escriba las siguientes propiedades:

   - **Propósito planteado**: Especifique el propósito planteado de los certificados que se importan para este perfil. Los administradores pueden importar los certificados con otros propósitos planteados (como firma S/MIME o cifrado S/MIME). El propósito planteado seleccionado en el perfil de certificado coincide con el perfil de certificado con los certificados importados adecuados. El propósito planteado es una etiqueta para agrupar los certificados importados y no garantiza que los certificados importados con esa etiqueta cumplan dicho propósito.  

   <!-- Not in new UI:
   - **Certificate validity period**: Unless the validity period was changed in the certificate template, this option defaults to one year.
   -->
   - **Proveedor de almacenamiento de claves (KSP)** : en el caso de Windows, seleccione la ubicación del dispositivo en la que quiera almacenar las claves.

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

   Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione el usuario o los grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

    Seleccione **Siguiente**.

11. (*Se aplica solo a Windows 10*) En **Reglas de aplicación**, especifique las reglas de aplicación para restringir la asignación de este perfil. Puede elegir asignar o no asignar el perfil en función de la edición del sistema operativo o la versión de un dispositivo.

    Para más información, consulte [Reglas de aplicabilidad](../configuration/device-profile-create.md#applicability-rules) en *Creación de un perfil de dispositivo en Microsoft Intune*.

    Seleccione **Siguiente**.

12. En **Revisar y crear**, revise la configuración. Si selecciona Crear, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="support-for-third-party-partners"></a>Compatibilidad con asociados de terceros

Los siguientes asociados proporcionan métodos o herramientas compatibles que puede usar para importar certificados PFX en Intune.

### <a name="digicert"></a>DigiCert

Si usa el servicio de la plataforma PKI DigiCert, puede usar la **herramienta de importación de certificados S/MIME para Intune de DigiCert** con el fin de importar los certificados PFX en Intune. El uso de esta herramienta permite obviar las instrucciones de la sección [Importación de certificados PFX en Intune](#import-pfx-certificates-to-intune) que se detallaron anteriormente en este artículo.

Para obtener más información sobre la herramienta de importación de DigiCert y cómo obtenerla, consulte https://knowledge.digicert.com/tutorials/microsoft-intune.html en la base de conocimiento de DigiCert.

### <a name="keytalk"></a>KeyTalk

Si usa el servicio KeyTalk, puede configurarlo para importar los certificados PFX a Intune. Tras finalizar la integración, no necesitará seguir las instrucciones de la sección [Importación de certificados PFX en Intune](#import-pfx-certificates-to-intune) que se detallaron anteriormente en este artículo.

Para más información sobre la integración de KeyTalk con Intune, consulte https://keytalk.com/support en la base de conocimiento de KeyTalk.

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero todavía no hace nada. [Asigne](../configuration/device-profile-assign.md) el nuevo perfil de dispositivo.
