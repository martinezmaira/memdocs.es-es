---
title: Preguntas más frecuentes sobre Windows AutoPilot
ms.reviewer: This topic provides OEMs, partners, administrators, and end users with answers to some frequently asked questions about deploying Windows 10 with Windows Autopilot.
manager: laurawi
description: Información de soporte técnico para Windows AutoPilot
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: af7b7f3a871683f7b75583292df5cb3d6e5de4c4
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993219"
---
# <a name="windows-autopilot-faq"></a>Preguntas más frecuentes sobre Windows AutoPilot

**Se aplica a: Windows 10**

En este artículo se proporcionan a los OEM, asociados, administradores y usuarios finales respuestas a algunas de las preguntas más frecuentes sobre la implementación de Windows 10 con Windows AutoPilot. 

Al final, se proporciona un [Glosario](#glossary) de abreviaturas que se usan en este artículo.


## <a name="microsoft-partner-center"></a>Centro de partners de Microsoft

| Pregunta | Respuesta |
| --- | --- |
| En el centro de Partners, ¿es necesario proporcionar el ID. de inquilino con cada carga de archivos de dispositivo? ¿Es necesario permitir que el cliente empresarial tenga acceso a sus dispositivos en Microsoft Store para empresas (MSfB)?     | No. Proporcionar el identificador de inquilino es una entrada de un solo uso en el centro de partners que se puede reutilizar con futuras cargas de dispositivos. |
| ¿Cómo sabe el cliente o el inquilino que sus dispositivos están listos para ser reclamados en MSfB?    |  Una vez completada la carga de archivos del dispositivo en el centro de Partners, el inquilino puede ver los dispositivos disponibles para la configuración de Windows AutoPilot en MSfB. El OEM debe aconsejar al inquilino acceso a MSfB. Se está desarrollando la notificación de MSfB al inquilino.  |
| ¿Cómo autoriza un cliente a un OEM o un asociado de canal para que registre dispositivos AutoPilot en el nombre del cliente?   |  Antes de que un OEM o un asociado de canal pueda registrar un dispositivo para el piloto automático en nombre de un cliente, el cliente debe dar su consentimiento en primer lugar.  El proceso de consentimiento comienza con el OEM o el asociado de canal enviando un vínculo al cliente que dirige al cliente a una página de consentimiento en MSfB.  Para obtener más información, consulte [registro](registration-auth.md).  |
|  ¿Hay alguna restricción si un cliente empresarial tiene dispositivos registrados en MSfB y después quiere que los dispositivos se administren mediante un proveedor de soluciones en la nube (CSP) mediante el centro de Partners? | Los dispositivos deberán ser eliminados por el cliente de la empresa antes de que el CSP pueda cargarlos y administrarlos en el centro de Partners. | 
| ¿Admite Windows AutoPilot la eliminación de la opción para habilitar una cuenta de administrador local?    |  Windows AutoPilot no admite la eliminación de la cuenta de administrador local. Sin embargo, admite la restricción del usuario que realiza la Unión al dominio Azure Active Directory (Azure AD) en OOBE a una cuenta estándar (en lugar de una cuenta de administrador de forma predeterminada).|
| ¿Cómo se puede probar el archivo CSV de Windows AutoPilot en el centro de Partners?    |  Solo los asociados de CSP tienen acceso al portal del centro de Partners. Si es un CSP, puede crear una cuenta de usuario del agente de ventas que tenga acceso a los dispositivos para probar el archivo. Esto se puede hacer hoy mismo en el centro de Partners. <br><br>Para obtener más información, vea [crear cuentas de usuario y establecer permisos](https://msdn.microsoft.com/partner-center/create-user-accounts-and-set-permissions). |
|  ¿Es necesario que se convierta en un CSP para participar en Windows AutoPilot? | Esto no es necesario para los OEM del volumen superior porque pueden usar la API directa de OEM.  Todos los demás usuarios que decidan usar MPC para registrar dispositivos deben convertirse en CSP para tener acceso a MPC.  |
| ¿Los distintos niveles de CSP tienen las mismas funcionalidades en lo que respecta a Windows AutoPilot?   |  Para los fines de Windows AutoPilot, hay tres tipos diferentes de CSP, cada uno con distintos niveles de autoridad y acceso: <br><br>1. <b>CSP directo</b>: obtiene la autorización directa del cliente para registrar dispositivos. <br><br>2. <b>proveedor de CSP indirecto</b>: obtiene el permiso implícito para registrar los dispositivos a través de la relación que tiene su asociado de revendedor de CSP con el cliente.  Los proveedores de CSP indirectos registran dispositivos a través del centro de Partners de Microsoft. <br><br>3. <b>revendedor de CSP indirecto</b>: obtiene la autorización directa del cliente para registrar dispositivos.  Al mismo tiempo, su asociado de proveedor CSP indirecto también obtiene la autorización, lo que significa que el proveedor indirecto o el revendedor indirecto pueden registrar los dispositivos del cliente.  Sin embargo, el revendedor de CSP indirecto debe registrar los dispositivos a través de la interfaz de usuario de MPC (cargar manualmente el archivo CSV), mientras que el proveedor de CSP indirecto tiene la opción de registrar dispositivos mediante las API de MPC. |
| ¿Hay alguna cuenta de CSP en todo el mundo?   |  No. Las regiones de ventas de CSP dependen de la ubicación del inquilino de (AzureAD).  Un asociado de CSP solo puede vender o administrar clientes que tengan un inquilino ubicado en la misma región de CSP que el asociado inscrito como CSP (la ubicación del inquilino que el asociado de CSP está usando para Transact). Si el inquilino del cliente se creó en EE. UU., solo un asociado que tenga una inscripción de CSP en EE. UU. puede establecer una relación de revendedor con este cliente. En lo que respecta al AutoPilot & Intune, no importa dónde se encuentre el dispositivo o el usuario final. Un dispositivo usado por un empleado que se encuentra en Alemania puede inscribirse mediante el perfil AutoPilot creado en el inquilino de EE. UU. y se puede administrar mediante la instancia de servicio de Intune en Estados Unidos. El usuario de Alemania también se autenticará en la instancia de AzureAD de EE. UU. Si un asociado desea administrar a los clientes globalmente, deben tener una presencia global. Deben tener varias inscripciones de CSP en cada una de las regiones de ventas de CSP donde desean llevar a cabo negocios. Tampoco es posible crear cuentas de usuario que tengan acceso a todos los inquilinos de CSP; Este escenario se traducirá en 18 cuentas de usuario para un agente de administración de CSP que quiera ser capaz de administrar todos los clientes de todo el mundo. En Resumen, la ubicación del usuario y los dispositivos no importa. La ubicación del inquilino del cliente es importante. El registro de dispositivos entre bordes no es el problema. el problema son las ventas entre bordes a través de CSP. |

## <a name="manufacturing"></a>Fabricación

| Pregunta | Respuesta |
| --- | --- |
| ¿Qué cambios deben realizarse en la imagen del sistema operativo de fábrica para las opciones de configuración del cliente?     |No se requieren cambios en la fábrica para habilitar la implementación de Windows AutoPilot.  |
| ¿Qué versión de la herramienta OA3 cumple los requisitos de implementación de Windows AutoPilot?     | Windows AutoPilot puede funcionar con cualquier versión de la herramienta OA3. Se recomienda usar una versión compatible del canal semianual de Windows 10 para generar el hash de hardware de 4K.    |
|  En el momento en que se realiza un pedido, los clientes deben tener el estado ¿si quieren usar o no las opciones de Windows AutoPilot?   | Sí, si quieren Windows AutoPilot, querrán una versión compatible del canal semianual de Windows 10. Además, querrán recibir el archivo CSV o hacer que la carga de archivos (es decir, el registro) se complete en su nombre.    |
|  ¿El OEM necesita administrar o recopilar archivos de imágenes personalizadas de los clientes y realizar cualquier carga de imágenes a Microsoft?   | Sin cambios, los OEM solo envían el CBRs como de costumbre a Microsoft. No se envía ninguna imagen a Microsoft para habilitar Windows AutoPilot.  Windows AutoPilot solo Personaliza OOBE y permite configuraciones de directivas (deshabilita la cuenta de administrador, por ejemplo).  |
|  ¿Hay algún impacto en el cliente en la actualización de Windows 8 a Windows 10?    | Los dispositivos deben ejecutar una versión compatible del canal semianual de Windows 10 para inscribirse en la implementación de Windows AutoPilot. De lo contrario, no habrá ningún impacto.    |
| ¿Habrá algún cambio en el hash de hardware de CBR con 4K existente?    | No.  |
| ¿Qué nueva información se debe enviar del OEM a Microsoft?    | Nada, a menos que el OEM opte por registrar el dispositivo en nombre del cliente, en cuyo caso cargaría el identificador de dispositivo mediante un archivo CSV en el centro de Partners de Microsoft o usaría la API directa de OEM.  |
| ¿Hay algún contrato o modificación de un OEM para participar en la implementación de Windows AutoPilot?    | No.  |

## <a name="csv-schema"></a>Esquema CSV

| Pregunta | Respuesta |
| --- | --- |
|  ¿Se puede usar una coma en el archivo CSV? | No.   |
| ¿Qué mensajes de error puede esperar que un usuario vea en el centro de Partners o MSfB al cargar un archivo?    | Consulte la sección en Microsoft Store para empresas de esta guía.  |
| ¿Hay un límite en el número de dispositivos que se pueden enumerar en el archivo CSV?    | Sí, el archivo CSV solo puede contener 1.000 dispositivos para aplicarlos a un solo perfil. Si es necesario aplicar más de 1.000 dispositivos a un perfil, los dispositivos deben cargarse a través de varios archivos CSV.    |
| ¿Microsoft tiene recomendaciones sobre el modo en que un OEM debe proporcionar el archivo CSV a sus clientes?    |  Se recomienda cifrar el archivo CSV al enviarlo al cliente empresarial para registrar automáticamente sus dispositivos de Windows AutoPilot (ya sea a través de MPC, MSfB o Intune).   |


## <a name="hardware-hash"></a>Hash de hardware

| Pregunta | Respuesta |
| --- | --- |
| Cada hash de hardware que envíe el OEM debe contener el UUID de SMBIOS (identificador único universal), la dirección MAC (Media Access Control) y el número de serie de disco único (si se usa la herramienta de activación 3,0 de Windows 10 OEM)?    | Sí. Puesto que Windows AutoPilot se basa en la capacidad de identificar de forma exclusiva los dispositivos que se aplican a la configuración de la nube, es fundamental enviar hashes de hardware que cumplan los requisitos descritos.   |
| ¿Cuál es el motivo por el que necesita el UUID de SMBIOS, la dirección MAC y el número de serie de disco en los detalles del hash de hardware?    | Para crear el hash de hardware, estos son los campos que son necesarios para identificar un dispositivo, ya que se agregan o se quitan partes del dispositivo. Como no tenemos un identificador único para dispositivos Windows, esta es la mejor lógica para identificar un dispositivo.    |
| ¿Qué diferencia hay entre el hash de hardware de OA3, el hash de hardware de 4K y el hash de hardware de Windows AutoPilot?    | Ninguno.  Son nombres diferentes para lo mismo.  La salida de la herramienta OA3 se denomina hash OA3, que es 4K de tamaño, que se puede usar para el escenario de implementación de Windows AutoPilot. Nota: cuando se usa una versión de Windows anterior y no compatible OA3Tool, se obtiene un hash de tamaño diferente, que no se puede usar para la implementación de Windows AutoPilot.  |
|  ¿Cuál es la idea de sustitución y reparación de piezas para la NIC (controlador de interfaz de red) y el disco? ¿El hash de hardware deja de ser válido?   |  Sí.  Si reemplaza partes, debe recopilar el nuevo hash de hardware, aunque depende de lo que se reemplace y de las características de los elementos. Por ejemplo, si reemplaza TPM o la placa base, es un dispositivo nuevo y debe tener un nuevo hash de hardware. Si reemplaza una tarjeta de red, probablemente no sea un dispositivo nuevo y el dispositivo funcionará con el hash de hardware anterior.  Sin embargo, como práctica recomendada, debe suponer que el hash de hardware anterior no es válido y obtener un nuevo hash de hardware después de cualquier cambio de hardware. Se recomienda siempre que se reemplacen partes. |

## <a name="motherboard-replacement"></a>Reemplazo de la placa base

| Pregunta | Respuesta |
| --- | --- |
| ¿Cómo controla AutoPilot los escenarios de reemplazo de la placa base?  |  El reemplazo de la placa base está fuera del ámbito de AutoPilot. Cualquier dispositivo que se haya reparado o que tenga servicio de forma que modifique la capacidad de identificar el dispositivo para Windows AutoPilot debe pasar por el proceso de OOBE normal y seleccionar manualmente la configuración correcta o aplicar una imagen personalizada, como es el caso actual.  <br><br>Para volver a usar el mismo dispositivo para Windows AutoPilot después de un reemplazo de la placa base, el dispositivo debe eliminarse del registro automático, se ha reemplazado la placa base, se ha reemplazado una nueva 4K HH y, a continuación, se ha vuelto a registrar con el nuevo hash de hardware de 4K (o el identificador de dispositivo). <br><br>**Nota**: un OEM no podrá usar la API directa de OEM para volver a registrar el dispositivo, ya que la API directa de OEM solo acepta una TUPLA o pkid.  En este caso, el OEM tendría que enviar la nueva información de hash de hardware de 4K mediante un archivo CSV al cliente y dejar que el cliente vuelva a registrar el dispositivo con MSfB o Intune.|

## <a name="smbios"></a>SMBIOS

| Pregunta | Respuesta |
| --- | --- |
| ¿Hay algún requisito específico para el UUID de SMBIOS?    | Debe ser único como se especifica en los requisitos de hardware de Windows 10.    |
| ¿Cuál es el requisito en la tabla de SMBIOS para cumplir las necesidades de hash de hardware de Windows AutoPilot?    | Debe cumplir todos los requisitos de hardware de Windows 10.  Puede encontrar más detalles [aquí](/previous-versions/windows/hardware/cert-program/windows-hardware-certification-requirements-for-client-and-server-systems).    |
| Si el SMBIOS es compatible con el número de serie y el UUID, ¿es suficiente para que la herramienta OA3 genere el hash de hardware?    | No.  Como mínimo, los siguientes campos de SMBIOS deben rellenarse con valores únicos: ProductKeyID SmbiosSystemManufacturer SmbiosSystemProductName SmbiosSystemSerialNumber SmbiosSkuNumber SmbiosSystemFamily MacAddress SmbiosUuid DiskSerialNumber TPM EkPub |

## <a name="technical-interface"></a>Interfaz técnica

| Pregunta | Respuesta |
| --- | --- |
|  ¿Cuál es la interfaz para obtener la dirección MAC y el número de serie del disco? ¿Cómo obtiene la herramienta OA MAC y el número de serie de disco?   | El número de serie del disco se encuentra en IOCTL_STORAGE_QUERY_PROPERTY con StorageDeviceProperty/PropertyStandardQuery.   La dirección MAC de red se IOCTL_NDIS_QUERY_GLOBAL_STATS de OID_802_3_PERMANENT_ADDRESS.  Sin embargo, el método para realizar esta operación varía en función del escenario.  |
| Explicación de seguimiento: si tenemos 2-3 equipos Mac en el sistema, ¿cómo elige la herramienta OA qué dirección MAC y número de serie de disco están en el sistema, ya que hay varias instancias de cada una? Si una plataforma tiene LAN y WLAN, ¿qué equipo MAC se elige?     |  En Resumen, se usan todos los valores disponibles.  En detalle, puede haber reglas de uso específicas. El número de serie del disco del sistema es más importante que los demás discos disponibles. Las interfaces de red que son extraíbles no deben usarse si se detectan porque son extraíbles. LAN frente a WLAN no deben importarse, ya que se usarán ambos.  |

## <a name="the-end-user-experience"></a>Experiencia del usuario final

|Pregunta|Respuesta|
|----|-----|
|¿Cómo sabe que he recibido AutoPilot?|Puede indicar que ha recibido Windows AutoPilot (como en el dispositivo ha recibido una configuración pero aún no la ha aplicado) cuando omite la página de selección (como se muestra a continuación) y se toma inmediatamente en una página de inicio de sesión genérica o personalizada.|
|Windows AutoPilot no funcionó, ¿qué hago ahora?| Preguntas y acciones para ayudar en la solución de problemas: ¿no se ha omitido la pantalla?   ¿El usuario finalizó como administrador cuando se configuró como no? Recuerde que Azure AD administradores serán administradores locales independientemente de si Windows AutoPilot está configurado para deshabilitar la información de la colección de administradores locales: ejecute licensingdiag.exe y envíe el archivo. cab (Cabinet) que se genera a AutopilotHelp@microsoft.com . Si es posible, recopile un ETL de la grabadora de rendimiento de Windows (WPR). A menudo, en estos casos, los usuarios no inician sesión en el Azure AD inquilino correcto o están creando cuentas de usuario locales.  Para obtener una lista completa de las opciones de soporte técnico, consulte [compatibilidad con Windows AutoPilot](autopilot-support.md). |
| Si un administrador realiza cambios en un perfil existente, ¿los cambios surtirán efecto en los dispositivos que tienen ese perfil asignado que ya se han implementado? |No. Los perfiles de Windows AutoPilot no residen en el dispositivo. Se descargan durante la OOBE, se aplica la configuración definida en el momento. Después, el perfil se descarta en el dispositivo. Si se restablece o se restablece la imagen inicial del dispositivo, la nueva configuración de perfil surtirá efecto la próxima vez que el dispositivo pase a través de OOBE.|
|¿Cuál es la experiencia si un dispositivo no está registrado o si un administrador de ti no configura Windows AutoPilot antes de que un usuario final intente realizar la implementación automática? |Si el dispositivo no está registrado, no recibirá la experiencia de Windows AutoPilot y el usuario final pasará a través de OOBE normal. Las configuraciones de Windows AutoPilot no se aplicarán hasta que el usuario vuelva a ejecutarse a través de OOBE, después del registro. Si se inicia un dispositivo antes de que se cree un perfil de MDM, el dispositivo pasará a la experiencia estándar de OOBE.  A continuación, el administrador de ti tendría que inscribir manualmente el dispositivo en la MDM, tras lo cual la próxima vez que se restablezca el dispositivo, pasará a través de la experiencia de OOBE de Windows AutoPilot.|
|¿Por qué no se ha recibido una pantalla de inicio de sesión personalizada durante el AutoPilot? |La personalización de marca de inquilinos debe estar configurada en portal.azure.com para recibir una experiencia de inicio de sesión personalizada.|
|¿Qué ocurre si un dispositivo está registrado con Azure AD pero no tiene asignado un perfil de Windows AutoPilot?                                |La Azure AD OOBE normal se producirá porque no se asignó ningún perfil de Windows AutoPilot al dispositivo.|
|¿Cómo puedo recopilar registros en AutoPilot?|La mejor manera de recopilar registros en el rendimiento de Windows AutoPilot es recopilar un seguimiento de WPR durante OOBE. El archivo XML (extensión WPRP) de este seguimiento se puede proporcionar a petición.|

## <a name="mdm"></a>MDM

| Pregunta | Respuesta |
| --- | --- |
| ¿Se debe usar Intune para la MDM?  |  No, cualquier MDM funcionará con AutoPilot, pero es probable que otros no tengan el mismo conjunto completo de características de Windows AutoPilot que Intune.  Obtendrá la mejor experiencia de Intune. |
| ¿Puede Intune admitir preinstalaciones de aplicaciones Win32?  | Sí.  A partir de la actualización de octubre de Windows 10 (versión 1809), Intune admite aplicaciones Win32 con contenedores. msi y. msix.  |
| ¿Qué es administración conjunta?  | La administración conjunta es cuando se usa una combinación de una herramienta MDM en la nube (Intune) y una herramienta de configuración local como Microsoft Endpoint Configuration Manager. Solo tiene que usar el Configuration Manager si Intune no admite lo que desea hacer con el perfil.  Si opta por la administración conjunta mediante Intune + Configuration Manager, puede hacerlo incluyendo un agente de Configuration Manager en el perfil de Intune. Cuando el perfil se inserte en el dispositivo, el dispositivo verá el agente de Configuration Manager y se desplazará al Configuration Manager para extraer cualquier configuración de perfil adicional. |
| ¿Se debe usar el punto de conexión de Microsoft Configuration Manager para Windows AutoPilot?  |  No.  La administración conjunta (descrita anteriormente) es opcional. |


## <a name="features"></a>Características

| Pregunta | Respuesta |
| --- | --- |
| Modo de auto-implementación  | Una nueva versión de Windows AutoPilot en la que el usuario solo enciende el dispositivo y nada más.  Es útil para escenarios en los que no se necesita una cuenta de usuario estándar (por ejemplo, dispositivos compartidos o dispositivos de pantalla completa).  |
| Unión Azure Active Directory híbrida  |  Permite que los dispositivos Windows AutoPilot se conecten a un controlador de dominio de Active Directory local (además de estar Azure AD Unidos). |
| Restablecimiento de Windows AutoPilot  | Quita las aplicaciones de usuario y la configuración de un dispositivo, pero mantiene Azure AD la Unión a un dominio y la inscripción de MDM.  Resulta útil cuando se transfiere un dispositivo de un usuario a otro.  |
| Personalización  | Agrega lo siguiente a la experiencia de OOBE: se puede crear un mensaje de bienvenida personalizado. Una sugerencia de nombre de usuario puede agregarse el texto de la página de inicio de sesión se puede personalizar. Se puede incluir el logotipo de la compañía |
| [Autopilot para dispositivos existentes](existing-devices.md)  |  Ofrece una ruta de actualización a Windows AutoPilot para todos los dispositivos existentes basados en Windows 7 y Windows 8. |



## <a name="general"></a>General

|Pregunta|Respuesta
|------------------|-----------------|
| Si elimino el equipo y reinicio, ¿seguiré recibiendo Windows AutoPilot?|Sí, si el dispositivo todavía está registrado para Windows AutoPilot y está ejecutando una versión compatible del canal semianual de Windows 10, recibirá la experiencia de Windows AutoPilot.|
| ¿Puedo recopilar la huella digital del dispositivo en las máquinas existentes?|Sí, si el dispositivo está ejecutando una versión compatible del canal semianual de Windows 10, puede recopilar huellas digitales del dispositivo para el registro. No hay planes de reportar la funcionalidad a las versiones heredadas y no se pueden recopilar en dispositivos que ejecuten versiones no compatibles de Windows.|
| Windows AutoPilot es compatible con otras SKU, por ejemplo, Surface Hub, HoloLens y Windows Mobile.|No, Windows AutoPilot no es compatible con otras SKU.|
| ¿Windows AutoPilot funciona después de la reinstalación de MBR o Image? | Sí. Para obtener más información, consulte la guía del escenario de sustitución de la [placa de Windows AutoPilot](autopilot-mbr.md). |
| ¿Es posible que los dispositivos que se han rescrito en imágenes varias veces pasen por el piloto automático? ¿Qué significa el mensaje de error "este usuario no está autorizado a inscribirse"? Código de error 801c0003. |Existen límites en cuanto al número de dispositivos que puede inscribir un usuario Azure AD determinado en Azure AD, así como el número de dispositivos que se admiten por usuario en Intune.  Se pueden configurar, pero no infinitas.  Encontrará este error con frecuencia si vuelve a usar los dispositivos, o incluso si revierte a las instantáneas de máquina virtual anteriores.|
| ¿Qué ocurre si un dispositivo está registrado en un agente malintencionado? | Por diseño, Windows AutoPilot no aplica un perfil hasta que el usuario inicia sesión con el inquilino correspondiente para el perfil configurado mediante el proceso de inicio de sesión Azure AD.  Por ejemplo, si badguys.com registra un dispositivo propiedad de contoso.com, en el peor de los usuarios se le dirigirá al usuario para que inicie sesión en badguys.com. Cuando el usuario escribe su correo electrónico y contraseña, la información de inicio de sesión se redirige a través de Azure AD a la autenticación de Azure AD adecuada y se solicita al usuario que inicie sesión en contoso.com. Como contoso.com no coincide con badguys.com como inquilino, el perfil de Windows AutoPilot no se aplicará y se producirá el Azure AD OOBE normal.|
| ¿Dónde se almacenan los datos de Windows AutoPilot?  |Los datos del programa piloto de Windows se almacenan en el Estados Unidos (EE. UU.), no en una nube soberano, incluso cuando el inquilino de Azure AD está registrado en una nube soberano. Esto es aplicable a todos los datos de Windows AutoPilot, independientemente del portal aprovechado para implementar AutoPilot.|
| ¿Por qué los datos de Windows AutoPilot se almacenan en Estados Unidos y no en una nube soberano?| Los datos del cliente no se almacenan, solo los datos empresariales que permiten a Microsoft proporcionar un servicio, por lo que es conveniente que los datos residan en Estados Unidos. Los clientes pueden dejar de suscribirse al servicio en cualquier momento. En ese caso, Microsoft quita los datos empresariales. AutoPilot no se admite actualmente en ninguna nube soberano. |
| Cuántas maneras hay que registrar un dispositivo para Windows AutoPilot|Hay seis maneras de registrar un dispositivo, en función de quién esté realizando el registro: <br><br>1. OEM Direct API (solo disponible para TVOs) <br>2. MPC mediante la API MPC (debe ser un CSP) <br>3. MPC mediante la carga manual del archivo CSV en la interfaz de usuario (debe ser un CSP) <br>4. MSfB mediante la carga de archivos CSV <br>5. Intune mediante la carga de archivos CSV <br>6. Microsoft 365 Empresa portal Premium mediante la carga de archivos CSV|
|¿Cuántas formas hay para crear un perfil de Windows AutoPilot?|Hay cuatro maneras de crear y asignar un perfil de Windows AutoPilot: <br><br>1. mediante MPC (debe ser un CSP) <br>2. a través de MSfB <br>3. a través de Intune (u otro MDM) <br>4. Microsoft 365 Empresa portal Premium <br><br>Microsoft recomienda la creación y asignación de perfiles a través de Intune.  |
| ¿Cuáles son algunas causas comunes de errores de registro? |1. las entradas de hash de hardware incorrectas o que faltan pueden dar lugar a intentos de registro erróneos <br>2. caracteres especiales ocultos en archivos CSV.  <br><br>Para evitar este problema, después de crear el archivo CSV, ábralo en el Bloc de notas para buscar caracteres ocultos o espacios finales u otros daños.|
|  ¿Se admite AutoPilot en dispositivos IoT? |  AutoPilot no es compatible con los dispositivos IoT Core y actualmente no hay ningún plan para agregar esta compatibilidad. AutoPilot es compatible con dispositivos Windows 10 IoT Enterprise SAC. AutoPilot es compatible con Windows 10 Enterprise LTSC 2019 y versiones posteriores. no se admite en versiones anteriores de LTSC.|
|  ¿Se admite AutoPilot en todas las regiones o países? |  AutoPilot solo es compatible con clientes que usan Azure global. Azure global no incluye las tres entidades que se enumeran a continuación:<br>-Azure Germany <br>-Azure China 21Vianet<br>-Azure Government<br>Por lo tanto, si un cliente se configura en Azure global, no hay restricciones de región. Por ejemplo, si Contoso usa Azure global pero tiene empleados que trabajan en China, los empleados de Contoso que trabajan en China podrán usar AutoPilot para implementar dispositivos. Si Contoso usa Azure China 21Vianet, los empleados de Contoso no podrán usar AutoPilot.|

## <a name="glossary"></a>Glosario

| Término | Significado |
| --- | --- |
| CSV  | Valores separados por comas (tipo de archivo similar a la hoja de cálculo de Excel)  |
| MPC  | Centro de partners de Microsoft   |
| MDM  | Administración de dispositivos móviles   |
| OEM  | Fabricante de equipo original   |
| CSP  |  Proveedor de soluciones en la nube  |
| MSfB  | Microsoft Store para Empresas   |
| Azure AD  | Azure Active Directory   |
| 4K HH  |  hash de hardware de 4K |
| CBR  | Informe de compilación de equipos  |
| EC  |  Comercio empresarial  |
| DDS  | Servicio de directorio de dispositivos    |
| OOBE  | Experiencia rápida   |
| UUID  | Identificador único universal   |