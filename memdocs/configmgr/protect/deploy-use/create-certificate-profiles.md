---
title: Creación de perfiles de certificado SCEP
titleSuffix: Configuration Manager
description: Aprenda a usar perfiles de certificado para aprovisionar dispositivos administrados con los certificados que necesitan
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 159afbf2c5aae9516fc5244ee06a2aa484290c20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705773"
---
# <a name="create-certificate-profiles"></a>Crear perfiles de certificado

*Se aplica a: Configuration Manager (rama actual)*

Use perfiles de certificado de Configuration Manager para aprovisionar dispositivos administrados con los certificados que necesitan para acceder a los recursos de empresa. Antes de crear perfiles de certificado, configure la infraestructura de certificados como se explica en [Configuración de la infraestructura de certificados](certificate-infrastructure.md).  

> [!TIP]
> En el caso de los dispositivos administrados conjuntamente, considere la posibilidad de mover la [carga de trabajo de las **directivas de acceso a recursos**](../../comanage/workloads.md#resource-access-policies) a Intune. Posteriormente, use las directivas de Intune para administrar estos certificados. Para más información, consulte el artículo sobre el [cambio de las cargas de trabajo](../../comanage/how-to-switch-workloads.md).

En este artículo se describe cómo crear perfiles de certificado raíz de confianza y del Protocolo de inscripción de certificados simple (SCEP). Si quiere crear perfiles de certificado PFX, consulte [Create PFX certificate profiles](../../mdm/deploy-use/create-pfx-certificate-profiles.md) (Crear perfiles de certificado PFX).

Para crear un perfil de certificado, siga estos pasos:

1. Inicie el Asistente para crear perfil de certificado.
1. Proporcione información general sobre el certificado.
1. Configure un certificado de entidad de certificación (CA) de confianza.  
1. Configure la información del certificado SCEP.  
1. Especifique las plataformas admitidas del perfil de certificado.

## <a name="start-the-wizard"></a>Inicio del asistente  

Para iniciar Crear perfil de certificado:

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía** y seleccione el nodo **Perfiles de certificado**.  

1. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear perfil de certificado**.  

## <a name="general"></a>General

En la página **General** del Asistente para crear perfil de certificado, especifique la información siguiente:  

- **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

- **Descripción**: proporcione una descripción que ofrezca una visión general del perfil de certificado. Incluya también otra información pertinente que le ayude a identificarlo en la consola de Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

- Especifique el tipo de perfil de certificado que quiere crear:

  - **Certificado de CA de confianza**: seleccione este tipo para implementar un certificado de entidad de certificación (CA) raíz de confianza o un certificado de CA intermedio para formar una cadena de confianza si el dispositivo o el usuario deben autenticar otro dispositivo. Por ejemplo, el dispositivo puede ser un servidor de Servicio de autenticación remota telefónica de usuario (RADIUS) o un servidor de red privada virtual (VPN).
  
    Además configure un perfil de certificado de CA de confianza para crear un perfil de certificado SCEP. En este caso, el certificado de CA de confianza debe ser para la CA que emitirá el certificado para el usuario o el dispositivo.  

  - **Configuración de Protocolo de inscripción de certificados simple (SCEP)** : seleccione este tipo para solicitar un certificado para un dispositivo o usuario con el Protocolo de inscripción de certificados simple y el servicio de rol Servicio de inscripción de dispositivos de red (NDES).

  - **Intercambio de información personal – configuración de PKCS #12 (PFX) – importar**: seleccione esta opción para importar un certificado PFX. Para más información, consulte [Importar perfiles de certificado PFX](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - **Intercambio de información personal – configuración de PKCS #12 (PFX) – crear**: seleccione esta opción para procesar los certificados PFX mediante una entidad de certificación. Para obtener más información, vea [Crear perfiles de certificado PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## <a name="trusted-ca-certificate"></a>Certificado de CA de confianza  

> [!IMPORTANT]  
> Antes de crear un perfil de certificado SCEP, configure al menos un perfil de certificado de CA de confianza.
>
> Una vez implementado el certificado, si cambia cualquiera de estos valores, se solicita un nuevo certificado:
>
> - Proveedor de almacenamiento de claves
> - Nombre de plantilla de certificado
> - Tipo de certificado
> - Formato de nombre del sujeto
> - Nombre alternativo del firmante
> - Período de validez del certificado
> - Uso de claves
> - Tamaño de la clave
> - Uso mejorado de clave
> - Certificado de CA raíz

1. En la página **Certificado de CA de confianza** del Asistente para crear perfil de certificado, especifique la información siguiente:  

    - **Archivo de certificado**: seleccione **Importar** y busque el archivo de certificado.  

    - **Almacén de destino**: Para los dispositivos que tienen más de un almacén de certificados, seleccione dónde quiere almacenar el certificado. Para los dispositivos que solo tienen un almacén, este valor se omite.  

2. Use el valor de **Huella digital de certificado** para comprobar que ha importado el certificado correcto.  

## <a name="scep-certificates"></a>Certificados SCEP

### <a name="1-scep-servers"></a>1. Servidores SCEP

En la página **SCEP Servers** del Asistente para crear perfil de certificado, especifique las direcciones URL para los servidores de NDES que emitirán certificados a través de SCEP. Puede asignar automáticamente una dirección URL de NDES basada en la configuración del punto de registro de certificados, o bien agregar direcciones URL manualmente.  

### <a name="2-scep-enrollment"></a>2. Inscripción de SCEP

Complete la página **Inscripción de SCEP** del Asistente para crear perfil de certificado.

- **Reintentos**: especifique el número de veces que el dispositivo intenta enviar automáticamente la solicitud de certificado al servidor NDES. Este valor es compatible con el escenario en el que un administrador de CA debe aprobar una solicitud de certificado para que sea aceptada. Esta opción se utiliza normalmente en entornos de alta seguridad o si tiene una CA emisora independiente en vez de una CA empresarial. También puede utilizar este valor para realizar pruebas, de forma que pueda examinar las opciones de la solicitud de certificado antes de que la CA emisora procese la solicitud de certificado. Utilice esta opción con el valor **Intervalo entre reintentos (minutos)** .  

- **Intervalo entre reintentos (minutos)** : especifique el intervalo en minutos entre cada intento de inscripción cuando se utiliza la aprobación del administrador de CA antes de que la CA emisora procese la solicitud de certificado. Si usa la aprobación del administrador para realizar pruebas, especifique un valor bajo. De este modo, no tendrá que esperar mucho tiempo a que el dispositivo reintente la solicitud de certificado después de aprobarla.

    Si usa la aprobación del administrador en una red de producción, especifique un valor mayor. Este comportamiento otorgará al administrador de CA tiempo suficiente para aprobar o denegar las aprobaciones pendientes.  

- **Umbral de renovación (%)** : Especifique qué porcentaje de la duración del certificado tiene que quedar para que el dispositivo solicite la renovación del certificado.  

- **Proveedor de almacenamiento de claves (KSP)** : Especifique dónde se almacena la clave del certificado. Elija uno de los siguientes valores:  

  - **Instalar en Módulo de plataforma segura (TPM) si está presente**: instala la clave en el TPM. Si el TPM no está presente, la clave se instala en el proveedor de almacenamiento de la clave de software.  

  - **Instalar en Módulo de plataforma segura (TPM) o se producirá un error**: instala la clave en el TPM. Si el módulo TPM no está presente, se producirá un error en la instalación.  

  - **Instalar en Windows Hello para empresas o generar un error**: esta opción está disponible para dispositivos Windows 10. Permite almacenar el certificado en la tienda de Windows Hello para empresas, que está protegida con autenticación multifactor. Para obtener más información, vea [Windows Hello para empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Esta opción no admite el inicio de sesión con tarjeta inteligente para el uso mejorado de clave en la página Propiedades del certificado.

  - **Instalar en Proveedor de almacenamiento de claves de software**: instala la clave en el proveedor de almacenamiento de la clave de software.  

- **Dispositivos para la inscripción de certificados**: si implementa el perfil de certificado en una recopilación de usuarios, permita la inscripción de certificados solo en el dispositivo primario del usuario o en cualquier dispositivo en el que el usuario inicie sesión.

    Si implementa el perfil de certificado en una recopilación de dispositivos, permita la inscripción de certificado solo al usuario primario del dispositivo o a todos los usuarios que inicien sesión en el dispositivo.  

### <a name="3-certificate-properties"></a>3. Propiedades de certificado

En la página **Propiedades de certificado** del Asistente para crear perfil de certificado, especifique la información siguiente:  

- **Nombre de plantilla de certificado**: seleccione el nombre de una plantilla de certificado que haya configurado en NDES y que haya agregado a una CA emisora. Para examinar correctamente las plantillas de certificado, la cuenta de usuario debe tener permisos de **lectura** en la plantilla de certificado. Si no puede usar **Examinar** para buscar el certificado, escriba su nombre.  

  > [!IMPORTANT]
  > Si el nombre de la plantilla de certificado contiene caracteres que no son ASCII, el certificado no se implementará. (Un ejemplo de estos caracteres son los del alfabeto chino). Para asegurarse de que el certificado está implementado, cree primero una copia de la plantilla de certificado en la entidad de certificación. Después, cambie el nombre de la copia mediante el uso de caracteres ASCII.  

  - Si *explora* para seleccionar el nombre de la plantilla de certificado, algunos campos de la página se rellenan automáticamente a partir de la plantilla de certificado. En algunos casos, estos valores no se pueden cambiar a menos que se elija otra plantilla de certificado.  

  - Si *escribe* el nombre de la plantilla de certificado, asegúrese de que coincida exactamente con el de una de las plantillas de certificado. Debe coincidir con uno de los nombres que aparecen en el registro del servidor NDES. Asegúrese de especificar el nombre de la plantilla de certificado y no su nombre para mostrar.  

    Para buscar los nombres de plantillas de certificado, vaya a la clave del Registro siguiente: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP`. Enumera las plantillas de certificado como los valores de **EncryptionTemplate**, **GeneralPurposeTemplate** y **SignatureTemplate**. De forma predeterminada, el valor de las tres plantillas de certificado es **IPSECIntermediateOffline**, que se asigna al nombre de plantilla para mostrar **IPSEC (solicitud sin conexión)** .  

    > [!WARNING]  
    > Cuando escriba el nombre de la plantilla de certificado, Configuration Manager no puede comprobar el contenido de la plantilla. Es posible que pueda seleccionar opciones no compatibles con la plantilla de certificado, lo que podría dar lugar a una solicitud de certificado con errores. Cuando se produce este comportamiento, se ve un mensaje de error de w3wp.exe en el archivo CPR.log que indica que el nombre de la plantilla en la solicitud de firma de certificado (CSR) y el desafío no coinciden.  
    >
    > Cuando escriba el nombre de la plantilla de certificado especificado para el valor **GeneralPurposeTemplate**, seleccione las opciones **Cifrado de clave** y **Firma digital** de este perfil de certificado. Si quiere habilitar solamente la opción **Cifrado de clave** de este perfil de certificado, especifique el nombre de la plantilla de certificado de la clave **EncryptionTemplate**. De igual forma, si desea habilitar solamente la opción **Firma digital** en este perfil de certificado, especifique el nombre de la plantilla de certificado para la clave de **SignatureTemplate** .  

- **Tipo de certificado**: seleccione si va a implementar el certificado en un dispositivo o en un usuario.  

- **Formato de nombre del sujeto**: seleccione cómo Configuration Manager crea de forma automática el nombre del firmante en la solicitud de certificado. Si el certificado es para un usuario, también puede incluir la dirección de correo electrónico del usuario en el nombre del sujeto.

    > [!NOTE]  
    > Si selecciona **Número IMEI** o **Número de serie**, puede diferenciar entre distintos dispositivos que pertenecen al mismo usuario. Por ejemplo, esos dispositivos pueden compartir un nombre común, pero no un número IMEI o número de serie. Si el dispositivo no notifica un número de serie o IMEI, el certificado se emite con el nombre común.

- **Nombre alternativo del firmante**: especifique cómo Configuration Manager crea de forma automática los valores del nombre alternativo del firmante (SAN) en la solicitud de certificado. Por ejemplo, si seleccionó un tipo de certificado de usuario, puede incluir el nombre principal de usuario (UPN) en el nombre alternativo del sujeto. Si el certificado de cliente va a autenticar un servidor de directivas de redes, establezca el nombre alternativo del firmante en el UPN.  

- **Período de validez del certificado**: si establece un período de validez personalizado en la CA emisora, especifique la cantidad de tiempo que queda antes de que expire el certificado.

    > [!TIP]
    > Establezca un período de validez personalizado con la siguiente línea de comandos: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`.
    > Para obtener más información sobre este comando, consulte [Infraestructura de certificados](certificate-infrastructure.md).  

    Puede especificar un valor inferior al período de validez de la plantilla de certificado especificada, pero no superior. Por ejemplo, si el período de validez del certificado de la plantilla de certificado es de dos años, puede especificar un valor de un año, pero no de cinco años. El valor también debe ser menor que el período de validez restante del certificado de la CA emisora.  

- **Uso de claves**: Especifique las opciones de uso de claves para el certificado. Elija entre las siguientes opciones:  

  - **Cifrado de clave**: permite el intercambio de claves solo si la clave está cifrada.  

  - **Firma digital**: permite el intercambio de claves solo si una firma digital protege la clave.  

  Si ha buscado una plantilla de certificado mediante Examinar, no podrá cambiar esta configuración a menos que seleccione otra plantilla de certificado.  

  Configure la plantilla de certificado seleccionada como mínimo con una de las dos opciones de uso de clave anteriores. Si no es así, verá este mensaje en el archivo de registro de punto de registro de certificados, **Crp.log**: **El uso de la clave en la CSR y en el desafío no coinciden**  

- **Tamaño de la clave (bits)** : Seleccione el tamaño de la clave, en bits.  

- **Uso mejorado de clave**: Agregue valores para la finalidad prevista del certificado. En la mayoría de los casos, el certificado requiere **Autenticación de cliente** para que el usuario o dispositivo pueda autenticarse en un servidor. Puede agregar otros usos clave según sea necesario.  

- **Algoritmo hash**: Seleccione uno de los tipos de algoritmos hash disponibles para usar con este certificado. Seleccione el nivel máximo de seguridad que admiten los dispositivos de conexión.  

  > [!NOTE]  
  > **SHA-2** admite SHA-256, SHA-384 y SHA-512. **SHA-3** solo admite SHA-3.  

- **Certificado de CA raíz**: elija un perfil de certificado de CA raíz que previamente haya configurado e implementado para el usuario o dispositivo. Este certificado de CA debe ser el certificado raíz de la entidad de certificación que va a emitir el certificado que va a configurar en este perfil de certificado.  

  > [!IMPORTANT]  
  > Si especifica un certificado de CA raíz que no se haya implementado en el usuario o dispositivo, Configuration Manager no inicia la solicitud de certificado que está configurando en este perfil de certificado.  

## <a name="supported-platforms"></a>Plataformas compatibles  

En la página **Plataformas admitidas** del Asistente para crear perfil de certificado, seleccione las versiones de SO donde quiere instalar el perfil de certificado. Seleccione **Seleccionar todo** para instalar el perfil de certificado en todos los sistemas operativos disponibles.

## <a name="next-steps"></a>Pasos siguientes

El nuevo perfil de certificado se muestra en el nodo **Perfiles de certificado** en el área de trabajo **Activos y compatibilidad**. Está listo para su implementación en usuarios o dispositivos. Para obtener más información, vea [Cómo implementar perfiles](deploy-wifi-vpn-email-cert-profiles.md).
