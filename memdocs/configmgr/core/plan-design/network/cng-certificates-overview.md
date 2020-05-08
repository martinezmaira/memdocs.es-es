---
title: Introducción a los certificados CNG
titleSuffix: Configuration Manager
description: Obtenga información sobre los certificados Cryptography Next Generation (CNG) para clientes y servidores de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: deb3108d492a955eb0ec6b1635e306dcb85e0062
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904209"
---
# <a name="cng-certificates-overview"></a>Introducción a los certificados CNG
<!-- 1356191 --> 

Configuration Manager tiene compatibilidad limitada con certificados Cryptography: Next Generation (CNG). Los clientes de Configuration Manager pueden usar un certificado de autenticación del cliente PKI con clave privada en el proveedor de almacenamiento de claves (KSP) de CNG. Gracias a la compatibilidad con KSP, los clientes de Configuration Manager admiten una clave privada basada en hardware, como el KSP de TPM para los certificados de autenticación de cliente PKI.

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede usar plantillas de certificado [Cryptography API: Next Generation (CNG)](https://docs.microsoft.com/windows/win32/seccng/cng-features) en los siguientes escenarios:

- Registro de cliente y comunicación con un punto de administración de HTTPS.   
- Distribución de software e implementación de aplicaciones con un punto de distribución de HTTPS.   
- Implementación de sistema operativo  
- SDK de mensajería de cliente (con la actualización más reciente) y proxy de ISV.   
- Configuración de Cloud Management Gateway  

A partir de la versión 1802, use certificados CNG para los siguientes roles de servidor habilitados para HTTPS: <!-- 1357314 -->   
- Punto de administración
- Punto de distribución
- Punto de actualización de software
- Punto de migración de estado     

A partir de la versión 1806, use certificados CNG para los siguientes roles de servidor habilitados para HTTPS:

- Punto de registro de certificados, incluido el servidor NDES con el módulo de directivas de Configuration Manager <!--1357314-->

> [!NOTE]
> CNG es compatible con Crypto API (CAPI). Los certificados CAPI siguen siendo compatibles, incluso cuando se habilita la compatibilidad con CNG en el cliente.

## <a name="unsupported-scenarios"></a>Escenarios no admitidos

Actualmente no se admiten los escenarios siguientes:

- Los roles de servidor siguientes no funcionan cuando se instalan en modo HTTPS con un certificado CNG enlazado al sitio web en Internet Information Services (IIS): 
    - Servicio web del catálogo de aplicaciones
    - Sitio web del catálogo de aplicaciones
    - Punto de inscripción  
    - Punto de proxy de inscripción  

- El Centro de software no muestra como disponibles los paquetes y las aplicaciones que se implementan en recopilaciones de grupos de usuarios o de usuarios.

- El uso de certificados CNG para crear un punto de distribución en la nube.

- Si el módulo de directivas de NDES usa un certificado CNG para la autenticación del cliente, se produce un error en la comunicación con el punto de registro de certificado. 
    - Se admite a partir de la versión 1806 de Configuration Manager.

- Si se especifica un certificado CNG al crear los medios de secuencia de tareas, el asistente no puede crear medios de arranque.
    - Se admite a partir de la versión 1806 de Configuration Manager.

## <a name="to-use-cng-certificates"></a>Uso de los certificados CNG

Para usar certificados CNG, la entidad de certificación (CA) debe proporcionar plantillas de certificado CNG para las máquinas de destino. Los detalles de la plantilla varían según el escenario; sin embargo, se requieren las siguientes propiedades:

- Pestaña **Compatibilidad**

    - La **entidad de certificación** debe ser Windows Server 2008 o posterior. (Se recomienda Windows Server 2012).

    - El **destinatario del certificado** debe ser Windows Vista o Server 2008 o posterior. (Se recomienda Windows 8/Windows Server 2012).

- Pestaña **Criptografía**

    - La **categoría del proveedor** debe ser **Proveedor de almacenamiento de claves**. (obligatorio)
    - **La solicitud debe usar uno de los siguientes proveedores:** debe ser **Proveedor de almacenamiento de claves (KSP) de Microsoft**. 

> [!NOTE]
> Los requisitos para su entorno u organización pueden ser diferentes. Póngase en contacto con su experto PKI. Hay que tener en cuenta un punto importante: una plantilla de certificado debe usar un proveedor de almacenamiento de claves para utilizar CNG.

Para obtener mejores resultados, se recomienda crear el nombre del sujeto a partir de la información de Active Directory. Use el nombre de DNS como **formato de nombre de sujeto** e inclúyalo en el nombre de sujeto alternativo. De lo contrario, tendrá que proporcionar esta información cuando el dispositivo se inscriba en el perfil de certificado.
