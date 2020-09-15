---
title: 'Conectores de certificado C para Microsoft Intune: Azure | Microsoft Docs'
description: Obtenga información sobre los conectores de certificado para un Protocolo de inscripción de certificados simple (SCEP) y Public Key Cryptography Standards (PKCS) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428904"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Conector de certificado para Microsoft Intune

Para admitir el uso de certificados para la autenticación, y la firma y el cifrado del correo electrónico mediante S/MIME, Intune requiere el uso de un conector de certificado. Un conector de certificado es el software que se instala en un servidor local. El conector permite a los dispositivos administrados en la nube aprovisionar certificados desde la infraestructura local, como una entidad de certificación emisora.

En este artículo se describen los conectores disponibles, su duración, los requisitos previos para su uso y cómo mantenerlos actualizados.  

## <a name="available-connectors"></a>Conectores disponibles

Hay dos conectores de certificado para Intune. Cada uno tiene sus propios requisitos y usos.

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>Conector de certificado PFX para Microsoft Intune

El **conector de certificados PFX** admite la implementación de certificados para las solicitudes de certificados PCKS #12 y administra solicitudes de archivos PFX importados a Intune para el cifrado de correo electrónico S/MIME para un usuario específico.

> [!TIP]
> Antes de la actualización de este conector en agosto, las solicitudes de certificados PKCS #12 se administraban mediante el *Conector de certificado de Intune*. Con la actualización de agosto, la funcionalidad de todas las solicitudes del certificado PKCS se consolidó en el *conector de certificados PFX*, que admite la actualización automática del conector a nuevas versiones y requiere el uso de la versión de .NET Framework 4.7.2.
>
> La funcionalidad del conector de Microsoft Intune no está en desuso y se puede seguir utilizando con perfiles de certificado PKCS. Sin embargo, si no usa SCEP o requiere usar NDES, puede cambiar al conector de certificados PFX y quitar NDES de los servidores. 

**Conector de certificados PFX**:

- Admite varias instancias de este conector para cada inquilino de Intune. Cada instancia del conector debe instalarse en un servidor de Windows y tener acceso a la clave privada que se usa para cifrar las contraseñas de los archivos PFX cargados.
- Se puede instalar en el mismo servidor que hospeda el *conector de Microsoft Intune*.
- Admite [actualizaciones automáticas](#automatic-update) a nuevas versiones. Para que las nuevas versiones se instalen automáticamente, el equipo que hospeda el conector debe contactar con **autoupdate.msappproxy.net** en el puerto **443**. Si el conector no se actualiza automáticamente, puede actualizar manualmente el conector.
- Admite la revocación de certificados (requiere la ejecución del conector versión **6.2008.60.607** o posterior).
- Tiene los mismos requisitos de red que los [dispositivos administrados](../fundamentals/intune-endpoints.md#access-for-managed-devices).

  Para más información, vea [Puntos de conexión de red de Microsoft Intune](../fundamentals/intune-endpoints.md) y [Ancho de banda y requisitos de configuración de red de Intune](../fundamentals/network-bandwidth-use.md).

**El servidor de Windows donde se instala el conector**:

- Debe ejecutar Windows Server 2012 R2 o versiones posteriores.
- Debe ejecutar .NET Framework 4.7.2.  

**Para instalar el conector de certificados PFX**:

Para una instalación guiada del conector, vea [Descarga, instalación y configuración del conector de certificados PFX](certficates-pfx-configure.md).

### <a name="microsoft-intune-connector"></a>Conector de Microsoft Intune

A veces, el **conector de Microsoft Intune** se denomina *Microsoft Intune Certificate Connector*. Este conector admite la implementación de certificados cuando usa el *Protocolo de inscripción de certificados simple* (SCEP) y una entidad de certificación de Servicios de certificados de Active Directory (CA). Este tipo de entidad de certificación también se conoce como *CA de Microsoft*.

Al usar SCEP con una CA de Microsoft, también debe configurar el **servicio de inscripción de dispositivos de red** (NDES). Por ese motivo, a menudo se hace referencia a este conector como *conector de certificado de NDES*.

Si usa una [entidad de certificación de terceros](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), no es necesario usar este conector ni NDES.

**Conector de Microsoft Intune**:

- Se instala en un servidor de Windows, que también puede hospedar una instancia del *conector de certificados PFX*.
- Admite hasta cien instancias de este conector por inquilino, con cada una de ellas en un servidor Windows independiente. Cuando se usan varios conectores:
  - Todas las instancias del *conector de Microsoft Intune* de su entorno deben tener la misma versión.
  - Su infraestructura admite redundancia y equilibrio de carga, ya que cualquier instancia del conector disponible puede procesar las solicitudes de certificado.
- Requiere una [actualización manual](#manual-update) para instalar la nueva versión del conector. Para realizar una actualización manual, hay que desinstalar el conector actual y después instalar la nueva versión del conector. No es necesario realizar acciones adicionales.
- Admite el modo del *Estándar federal de procesamiento de información* (FIPS). No se requiere FIPS. Cuando FIPS está habilitado, puede emitir y revocar certificados.
- Tiene los mismos requisitos de red que los [dispositivos administrados](../fundamentals/intune-endpoints.md#access-for-managed-devices).

  Para más información, vea [Puntos de conexión de red de Microsoft Intune](../fundamentals/intune-endpoints.md) y [Ancho de banda y requisitos de configuración de red de Intune](../fundamentals/network-bandwidth-use.md).

**El servidor de Windows donde se instala el conector**:

- Debe ejecutar Windows Server 2012 R2 o versiones posteriores.
- Debe ejecutar .NET Framework 4.5. Cuando este conector se instala en el mismo servidor que el *conector de certificados PFX*, debe usar .NET 4.7.2 Framework, ya que es un requisito del conector PFX.
- No puede ser el mismo servidor que hospeda la entidad de certificación (CA) emisora.
- Cuando se usa para SCEP con una CA de Microsoft, requiere acceso a un servidor que ejecuta NDES. NDES se ejecuta en un servidor de Windows y puede ejecutarse en el mismo servidor que este conector.

**Cuando se requiere NDES**:

- La configuración de seguridad mejorada de Internet Explorer [debe estar deshabilitada en el servidor en el que se hospeda NDES](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) y el servidor que hospeda el *conector de Microsoft Intune*.
- El conector requiere configuraciones adicionales para comunicarse con NDES. Encontrará los procedimientos para instalar y configurar NDES con los procedimientos para instalar el *conector de Microsoft Intune*.

  Para más información sobre NDES, vea [Orientación para el Servicio de inscripción de dispositivos de red](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

**Para instalar el conector de Microsoft Intune**:

Para instrucciones sobre la instalación de este conector, vea [Configuración de la infraestructura para admitir SCEP con Intune](certificates-scep-configure.md).

## <a name="connector-lifecycle"></a>Ciclo de vida del conector

Se publican versiones actualizadas de los conectores del certificado con regularidad. Los anuncios de nuevas versiones del conector se publican el artículo [Novedades](../fundamentals/whats-new.md) para Intune y en la sección [Novedades sobre los conectores](#whats-new-for-connectors) del final de este artículo.

Cuando se publica una nueva versión, la versión anterior deja de ser compatible con un período de gracia limitado para su uso continuado. Una vez finalizado el período de gracia, finaliza la compatibilidad con esa versión en desuso y puede dejar de funcionar en cualquier momento. El período de gracia es de seis meses.

Actualice el conector a la versión más reciente lo más pronto posible. Cada conector tiene una ruta de acceso de actualización diferente:

- **Conector de certificados PFX para Microsoft Intune**: admite actualizaciones automáticas.
- **Conector de Microsoft Intune** : requiere una actualización manual.

### <a name="automatic-update"></a>Actualización automática

Cuando el tipo de conector y el entorno lo admiten, Intune puede actualizar automáticamente el conector a la versión más reciente poco después de que se lance la versión del conector.  

Para llevar a cabo una actualización automática, el servidor que hospeda el conector debe acceder al **servicio de actualización de Azure**:

- Puerto: **443**
- Punto de conexión: **autoupdate.msappproxy.net**

Cuando los firewalls, la infraestructura o las configuraciones de red limitan el acceso para la actualización automática, puede resolver los problemas de bloqueo o actualizar manualmente el conector a la nueva versión.

### <a name="manual-update"></a>Actualización manual

El proceso para actualizar manualmente un conector de certificado es el mismo que para reinstalar un conector.

Puede actualizar manualmente un conector de certificado, aunque este admita las actualizaciones automáticas. Por ejemplo, puede hacerlo cuando la configuración de red bloquee una actualización automática.  

### <a name="to-reinstall-a-certificate-connector"></a>Para reinstalar un conector de certificado:

1. En el servidor de Windows que hospeda el conector, use **Aplicaciones y características de Windows** para desinstalar el conector.

2. Para instalar la nueva versión, use el procedimiento para instalar una nueva versión del conector. Al instalar una versión más reciente de un conector, asegúrese de comprobar los requisitos previos nuevos o actualizados:
   - SCEP: [Configuración de la infraestructura para admitir SCEP con Intune](certificates-scep-configure.md)
   - PKCS: [Descarga, instalación y configuración del conector de certificados PFX para Microsoft Intune](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>Estado y versión del conector

En el centro de administración de Microsoft Endpoint Manager, puede seleccionar un conector de certificado para ver información sobre su estado y confirmar su versión:

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vaya a **Administración de inquilinos** > **Conectores y tokens** > **Conectores de certificados**.

3. Seleccione un conector para ver su estado.

Al ver el estado del conector:

- Los conectores en desuso se mostrarán con una **advertencia**. Después del período de gracia de seis meses, la advertencia cambia a error.
- Los conectores que superan el período de gracia, muestran un error. Estos conectores ya no se admiten y pueden dejar de funcionar en cualquier momento.

## <a name="whats-new-for-connectors"></a>Novedades para los conectores

Se publican actualizaciones para los dos conectores de certificados con regularidad. Cuando actualizamos un conector, informamos aquí sobre los cambios realizados.

### <a name="pfx-certificate-connector-release-history"></a>Historial de versiones del conector de certificados PFX

El *conector de certificados PFX para Microsoft Intune* [admite las actualizaciones automáticas](#automatic-update).

#### <a name="august-26-2020"></a>26 de agosto de 2020

**Versión 6.2008.60.607**. Cambios de esta versión:

- Requiere .NET Framework versión 4.7.2 RC.
- Reemplaza el uso del *conector de Microsoft Intune* para su uso con perfiles de certificado PKCS. El *conector de certificados PFX* es ahora el único conector necesario para usar PCKS #12 o certificados PFX importados.
- Agrega compatibilidad para usar perfiles del certificado PKCS con todas las plataformas admitidas excepto Windows 8.1.
- Agrega compatibilidad para la revocación de certificados para Outlook S/MIME.

#### <a name="november-18-2019"></a>18 de noviembre de 2019

**Versión: 6.1911.11.602**. Cambios de esta versión:

- Se ha agregado compatibilidad con S/MIME para la importación de PFX.  

#### <a name="may-17-2019"></a>17 de mayo de 2019

**Versión 6.1905.0.404**. Cambios de esta versión:

- Se ha corregido un problema por el que los certificados PFX existentes se siguen procesando, lo que provoca que el conector deje de procesar solicitudes nuevas. 

#### <a name="may-6-2019"></a>6 de mayo de 2019

**Versión 6.1905.0.402**. Cambios de esta versión:

- El intervalo de sondeo para el conector se ha reducido de 5 minutos a 30 segundos.

#### <a name="april-2-2019"></a>2 de abril de 2019

**Versión 6.1904.0.401**. Cambios de esta versión:

- Ahora este conector admite la actualización automática.
- Se ha corregido un problema que podría producir que el conector no se inscriba en Intune después de iniciar sesión en el conector con una cuenta de administrador global.

### <a name="microsoft-intune-connector-release-history"></a>Historial de versiones del conector de Microsoft Intune

#### <a name="april-2-2019"></a>2 de abril de 2019

**Versión 6.1904.1.0**. Cambios de esta versión:  

- Se ha corregido un problema que podría producir que el conector no se inscriba en Intune después de iniciar sesión en el conector con una cuenta de administrador global.
- Incluye correcciones de fiabilidad para la revocación de certificados.
- Incluye correcciones de rendimiento para aumentar la rapidez con la que se procesan las solicitudes de certificado PKCS.

## <a name="next-steps"></a>Pasos siguientes

Cree perfiles de certificado SCEP, PKCS o PKCS importados para cada plataforma que quiera usar. Para continuar, vea los artículos siguientes:

- [Configuración de la infraestructura para admitir certificados SCEP con Intune](certificates-scep-configure.md)  
- [Configuración y administración de certificados PKCS con Intune](certficates-pfx-configure.md)  
- [Creación de un perfil de certificado PKCS importado](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
