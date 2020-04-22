---
title: Clúster de SQL Server
titleSuffix: Configuration Manager
description: Use un clúster de SQL Server para hospedar la base de datos de sitio de Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e731ef2d133c2187eb9eaa98c07afeed37645fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700853"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Uso de un clúster de SQL Server para la base de datos del sitio

*Se aplica a: Configuration Manager (rama actual)*

Puede usar un clúster de conmutación por error de SQL Server para hospedar la base de datos de sitio de Configuration Manager. Un clúster proporciona compatibilidad con la conmutación por error y mejora la confiabilidad de la base de datos del sitio, pero no ofrece un procesamiento adicional ni ventajas de equilibrio de carga. Además, un clúster de conmutación por error de SQL Server usa almacenamiento compartido y presenta un único punto de error. El rendimiento puede degradarse porque el servidor de sitio debe encontrar el nodo activo del clúster de SQL Server antes de conectarse a la base de datos del sitio.  

> [!IMPORTANT]  
> La configuración correcta de los clústeres de SQL Server se basa en la documentación y los procedimientos proporcionados en la biblioteca de documentación de SQL Server.  


Antes de instalar Configuration Manager, prepare el clúster de SQL Server para que admita Configuration Manager. Para obtener más información, vea [Preparar una instancia de SQL Server en clúster para la base de datos del sitio](#bkmk_prepare).

Durante la instalación de Configuration Manager, el escritor del Servicio de instantáneas de volumen de Windows se instala en cada nodo de equipo físico del clúster de Microsoft Windows Server. De este modo, este servicio admite la tarea de mantenimiento de **Copia de seguridad del servidor del sitio**.  

Una vez instalado el sitio, Configuration Manager comprueba cada hora los cambios que se producen en el nodo de clúster. Configuration Manager administra automáticamente los cambios que encuentre que afectan a sus instalaciones de componentes. Por ejemplo, un nodo de conmutación por error o la adición de un nuevo nodo al clúster de SQL Server.  



## <a name="supported-options"></a>Opciones admitidas

Se admiten las siguientes opciones para los clústeres de conmutación por error de SQL Server usados como base de datos del sitio:

- Clúster de instancia única  

- Varias configuraciones de instancias  

- Varios nodos activos  

- Instancia con nombre o instancia predeterminada  



## <a name="prerequisites"></a>Requisitos previos

Tenga en cuenta los siguientes requisitos previos:  

- La base de datos del sitio debe ser remota con respecto al servidor de sitio. El clúster no puede incluir el servidor de sistema de sitio.  

    > [!Note]  
    > A partir de la versión 1810, el proceso de instalación de Configuration Manager ya no impide la instalación del rol de servidor de sitio en un equipo con el rol de Windows para clústeres de conmutación por error. Anteriormente, no podía colocar la base de datos del sitio en el servidor de sitio. Con este cambio, puede crear un sitio de alta disponibilidad con menos servidores usando un clúster de SQL y un servidor de sitio en modo pasivo. Para obtener más información, vea [High availability options](high-availability-options.md) (Opciones de alta disponibilidad). <!--3607761, fka 1359132-->  

- Agregue la cuenta de equipo del servidor de sitio al grupo de **administradores** locales de cada servidor del clúster.  

- Para admitir la autenticación Kerberos, habilite el protocolo de comunicación de red **TCP/IP** para la conexión de red de cada nodo del clúster de SQL Server. No hace falta el protocolo de **canalizaciones con nombre**, pero puede usarse para solucionar problemas de autenticación Kerberos. Las opciones de protocolo de red se configuran en **Administrador de configuración de SQL Server**, en **Configuración de red de SQL Server**.  

- Si usa una infraestructura de clave pública (PKI), consulte [Requisitos de certificados PKI](../../../plan-design/network/pki-certificate-requirements.md). Hay requisitos de certificado específicos cuando se usa el clúster de SQL Server para la base de datos del sitio.  



## <a name="limitations"></a>Limitaciones

Tenga en cuenta las limitaciones siguientes:  


### <a name="installation-and-configuration"></a>Instalación y configuración

- Los sitios secundarios no pueden usar un clúster de SQL Server.  

- La opción de especificar ubicaciones de archivos no predeterminadas para la base de datos del sitio no está disponible cuando se especifica un clúster de SQL Server.  


### <a name="sms-provider"></a>Proveedor de SMS

No se puede instalar una instancia del proveedor de SMS en un clúster de SQL Server. Tampoco se admite en un equipo que se ejecuta como un nodo de SQL Server en clúster.  


### <a name="data-replication-options"></a>Opciones de replicación de datos

Si usa **vistas distribuidas**, no puede usar un clúster de SQL Server para hospedar la base de datos del sitio.  


### <a name="backup-and-recovery"></a>Copia de seguridad y recuperación

Configuration Manager no admite la copia de seguridad de Data Protection Manager (DPM) para un clúster de SQL Server que use una instancia con nombre. Sí admite la copia de seguridad de DPM en un clúster de SQL Server que use la instancia predeterminada de SQL Server.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a> Preparación de una instancia de SQL Server en clúster  

Estas son las principales tareas que debe llevar a cabo para preparar la base de datos del sitio:

- Cree el clúster virtual de SQL Server para hospedar la base de datos del sitio en un entorno de clúster de Windows Server existente. Para conocer pasos específicos para instalar y configurar un clúster de SQL Server, vea la documentación específica de la versión de SQL Server. Para obtener más información, consulte [Crear un nuevo clúster de conmutación por error](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- En cada equipo del clúster de SQL Server, coloque un archivo en la carpeta raíz de cada unidad en donde no quiere que Configuration Manager instale componentes del sitio. Ponga al archivo el nombre `NO_SMS_ON_DRIVE.SMS`. De forma predeterminada, Configuration Manager instala algunos componentes en cada nodo físico para admitir operaciones como la copia de seguridad.  

- Agregue la cuenta de equipo del servidor de sitio al grupo de **administradores** locales de cada equipo de nodo de clúster de Windows Server.  

- En la instancia virtual de SQL Server, asigne el rol **sysadmin** de SQL Server a la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar un sitio nuevo con un servidor de SQL Server en clúster  

Para instalar un sitio que usa una base de datos del sitio en clúster, ejecute el programa de instalación de Configuration Manager siguiendo el proceso normal para instalar un sitio, pero introduzca la modificación siguiente:  

- En la página **Información de base de datos** , especifique el nombre de la instancia virtual de clúster de SQL Server que hospedará la base de datos del sitio. La instancia virtual reemplaza el nombre del equipo que ejecuta SQL Server.  

    > [!IMPORTANT]  
    > Cuando escriba el nombre de la instancia virtual de clúster de SQL Server, no escriba el nombre virtual de Windows Server creado por el clúster de Windows Server. Si usa el nombre virtual de Windows Server, la base de datos del sitio se instala en la unidad de disco duro local del nodo de clúster activo de Windows Server. Esto impide que la conmutación por error se lleve a cabo correctamente si se produce un error en ese nodo.  
