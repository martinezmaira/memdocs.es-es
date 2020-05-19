---
title: Creación de un laboratorio en Azure
titleSuffix: Configuration Manager
description: Automatización de la creación de un laboratorio de Configuration Manager Technical Preview o de un laboratorio de evaluación de la rama actual con plantillas de Azure
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 23cc7d0c642637a310f53280bafed6a2a28d2834
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406682"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Creación de un laboratorio de Configuration Manager en Azure

*Se aplica a: Configuration Manager (rama actual, rama de Technical Preview)*

<!--3556017-->

En esta guía se describe cómo crear un entorno de laboratorio de Configuration Manager en Microsoft Azure. Usa plantillas de Azure para simplificar y automatizar la creación de un laboratorio con recursos de Azure. Se proporcionan dos plantillas de Azure: 

- La plantilla de Azure de la rama Technical Preview de Configuration Manager instala la versión más reciente de la rama Technical Preview de Configuration Manager.
- La plantilla de Azure de la rama actual de Configuration Manager instala la evaluación de la versión más reciente de la rama actual de Configuration Manager. 

Para más información, consulte [Configuration Manager en Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Requisitos previos

Para este proceso se necesita una suscripción de Azure en la que poder crear estos objetos: 
- Dos máquinas virtuales Standard_B2s para el controlador de dominio, en el punto de administración y el punto de distribución.
- Una máquina virtual Standard_B2ms para el servidor de sitio primario y el servidor de SQL Database.
- Cuenta de almacenamiento Standard_LRS

> [!Tip]  
> Para poder determinar los costos potenciales, vea la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/).  



## <a name="process"></a>Proceso

1. Vaya a [la plantilla de la rama Technical Preview de Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) o [la plantilla de la rama actual de Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Seleccione **Implementar en Azure** y se abrirá Azure Portal.  

3. Rellene la plantilla de inicio rápido de Azure con esta información:

    - Aspectos básicos  

        - **Suscripción**: nombre de la suscripción en la que se van a crear las máquinas virtuales  

        - **Grupo de recursos**: seleccione un grupo de recursos para usarlo para estas máquinas virtuales  

        - **Ubicación**: seleccione un centro de datos de Azure para hospedar este entorno de laboratorio  

    - Configuración  

        - **Prefijo**: nombre de prefijo de las máquinas. Para más información, vea [Información de máquina virtual de Azure](#azure-vm-info).  

        - **Nombre de usuario de administrador**: nombre de un usuario en las máquinas virtuales con derechos administrativos. Este usuario se usa para iniciar sesión en las máquinas virtuales.  

        - **Contraseña de administrador**: la contraseña debe cumplir los requisitos de complejidad de Azure. Para más información, vea [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Para Azure se necesita la siguiente configuración. Use los valores predeterminados. No cambie estos valores.  
    > 
    > - **\_Ubicación de artefactos**: ubicación de los scripts de esta plantilla <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_Token de SAS de ubicación de artefactos**: se necesita el token de SAS para acceder a la ubicación de artefactos  
    > 
    > - **Ubicación**: ubicación de todos los recursos

4. Lea los términos y condiciones. Si acepta, seleccione **Acepto los términos y condiciones indicados anteriormente**. Después, seleccione **Comprar** para continuar. 

Azure valida la configuración y, después, empieza la implementación. Compruebe el estado de la implementación en Azure Portal. 

> [!NOTE]
> El proceso puede tardar entre dos y cuatro horas. Aunque en Azure Portal se muestre que la implementación se ha realizado correctamente, los scripts de configuración siguen ejecutándose. No reinicie las máquinas virtuales durante el proceso.

Para ver el estado de los scripts de configuración, conéctese al servidor de `<prefix>PS1` y vea este archivo: `%windir%\TEMP\ProvisionScript\PS1.json`. Si muestra que todos los pasos se han completado, entonces el proceso ha finalizado.

Para conectarse a las máquinas virtuales, consiga primero de Azure Portal las direcciones IP públicas de cada máquina virtual. Cuando se conecta a la máquina virtual, el nombre de dominio es `contoso.com`. Use las credenciales que especificó en la plantilla de implementación. Para más información, vea [Conexión a una máquina virtual de Azure donde se ejecuta Windows e inicio de sesión en ella](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Información de máquina virtual de Azure

Las tres máquinas virtuales tienen estas especificaciones:
- 150 GB de espacio en disco
- Una dirección IP pública y una privada. Las direcciones IP públicas se encuentran en un grupo de seguridad de red que solo permite conexiones a Escritorio remoto en el puerto TCP 3389. 

El prefijo que especificó en la plantilla de implementación es el prefijo de nombre de la máquina virtual. Por ejemplo, si establece el prefijo "contoso", el nombre de la máquina de controlador de dominio es `contosoDC`.


### `<prefix>DC01`

- Controlador de dominio de Active Directory
- Standard_B2s, con dos procesadores y 4 GB de memoria
- Windows Server 2019, Datacenter Edition

#### <a name="windows-features-and-roles"></a>Roles y características de Windows
- Active Directory Domain Services (ADDS)
- .NET
- Compresión diferencial remota (RDC)


### `<prefix>PS01`

- Standard_B2ms, con dos procesadores y 8 GB de memoria
- Windows Server 2016, Datacenter Edition
- SQL Server
- Windows 10 ADK con Windows PE 
- Sitio primario de Configuration Manager

#### <a name="windows-features-and-roles"></a>Roles y características de Windows
- .NET
- Compresión diferencial remota (RDC) 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- Standard_B2s, con dos procesadores y 4 GB de memoria
- Windows Server 2019, Datacenter Edition
- Punto de distribución
- Punto de administración

#### <a name="windows-features-and-roles"></a>Roles y características de Windows
- .NET
- Compresión diferencial remota (RDC) 
- Internet Information Service (IIS)
- Servicio de transferencia inteligente en segundo plano (BITS)

### `<prefix>CL01`

- Solo para la plantilla de evaluación de la rama actual de Configuration Manager
- Windows 10
- Cliente de Configuration Manager
