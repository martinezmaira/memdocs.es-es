---
title: Cifrado de los datos de recuperación
titleSuffix: Configuration Manager
description: Cifre claves de recuperación de BitLocker, paquetes de recuperación y hashes de contraseñas de TPM a través de la red y en la base de datos de Configuration Manager.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709353"
---
# <a name="encrypt-recovery-data"></a>Cifrado de los datos de recuperación

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Al crear una directiva de administración de BitLocker, Configuration Manager implementa el servicio de recuperación en un punto de administración. En la página **Administración de cliente** de la directiva de administración de BitLocker, al **configurar los servicios de administración de BitLocker**, el cliente realiza una copia de seguridad de la información de recuperación de claves en la base de datos del sitio. Esta información incluye claves de recuperación de BitLocker, paquetes de recuperación y hashes de contraseña de TPM. Cuando los usuarios estén bloqueados en su dispositivo protegido, puede usar esta información para ayudarles a recuperar el acceso al dispositivo.

Dado el carácter confidencial de esta información, debe protegerla en las siguientes circunstancias:

- Configuration Manager requiere una conexión HTTPS entre el cliente y el servicio de recuperación para cifrar los datos en tránsito a través de la red. Hay dos opciones:

  - HTTPS: habilite el sitio web de IIS en el punto de administración que hospeda el servicio de recuperación, no en todo el rol de punto de administración. Esta opción solo se aplica a Configuration Manager, versión 2002.<!-- 5925660 -->

  - Configure el punto de administración para HTTPS. En las propiedades del punto de administración, la configuración de **Conexiones de cliente** debe ser **HTTPS**. Esta opción se aplica a las versiones 1910 o 2002 de Configuration Manager.

    > [!NOTE]
    > Actualmente no admite HTTP mejorado.

- Considere también la posibilidad de cifrar estos datos cuando se almacenan en la base de datos del sitio. Puede usar el cifrado de nivel de celda de SQL Server con su propio certificado.

    Si no quiere crear un certificado de cifrado de administración de BitLocker, opte por el almacenamiento en texto sin formato de los datos de recuperación. Al crear una directiva de administración de BitLocker, habilite la opción **Permite que la información de recuperación se almacene en texto sin formato**.

    > [!NOTE]
    > Otra capa de seguridad consiste en cifrar toda la base de datos del sitio. Si habilita el cifrado en la base de datos, no habrá ningún problema funcional en Configuration Manager.
    >
    > Use el cifrado con precaución, especialmente en entornos a gran escala. En función de las tablas que cifre y de la versión de SQL, es posible que observe una degradación del rendimiento de hasta un 25 %. Actualice los planes de recuperación y copia de seguridad para poder recuperar correctamente los datos cifrados.

## <a name="certificate-requirements"></a>Requisitos de certificados

### <a name="https-server-authentication-certificate"></a>Certificado de autenticación de servidor HTTPS

<!--5925660-->

En la rama actual de Configuration Manager, versión 1910, para integrar el servicio de recuperación de BitLocker se necesita un punto de administración habilitado para HTTPS. La conexión HTTPS es necesaria para cifrar las claves de recuperación en la red desde el cliente de Configuration Manager al punto de administración. La configuración del punto de administración y de todos los clientes para HTTPS puede resultar complicada para muchos clientes.

A partir de la versión 2002, el requisito de HTTPS es para el sitio web de IIS que hospeda el servicio de recuperación, no para todo el rol de punto de administración. Este cambio reduce los requisitos de certificado, pero sigue cifrando las claves de recuperación en tránsito.

Ahora la propiedad **Conexiones de cliente** del punto de administración puede ser **HTTP** o **HTTPS**. Si el punto de administración está configurado para **HTTP**, para admitir el servicio de recuperación de BitLocker:

1. Adquiera un certificado de autenticación de servidor. Enlace el certificado al sitio web de IIS en el punto de administración que hospeda el servicio de recuperación de BitLocker.

2. Configure los clientes de modo que confíen en el certificado de autenticación de servidor. Hay dos métodos para conseguir esta relación de confianza:

    - Usar un certificado de un proveedor de certificados público y de confianza global. Por ejemplo, DigiCert, VeriSign o Thawte, entre otros. Los clientes de Windows incluyen entidades de certificación raíz de confianza (CA) de estos proveedores. Al usar un certificado de autenticación de servidor emitido por uno de estos proveedores, los clientes deben confiar automáticamente en él.

    - Use un certificado emitido por una entidad de certificación de la infraestructura de clave pública (PKI) de la organización. La mayoría de las implementaciones de PKI agregan las entidades de certificación raíz de confianza a clientes Windows. Por ejemplo, mediante el uso de Servicios de certificados de Active Directory con una directiva de grupo. Si emite el certificado de autenticación de servidor desde una entidad de certificación en la que los clientes no confían automáticamente, agregue el certificado raíz de confianza de la entidad de certificación a los clientes.

> [!TIP]
> Los únicos clientes que necesitan comunicarse con el servicio de recuperación son aquellos a los que se planea destinar una directiva de administración de BitLocker que incluye una regla de **Administración de cliente**.

En el cliente, use **BitLockerManagementHandler.log** para solucionar problemas de esta conexión. En el caso de la conectividad con el servicio de recuperación, el registro muestra la dirección URL que el cliente está usando. Busque una entrada que comience por `Checking for Recovery Service at`.

> [!NOTE]
> Si el sitio tiene más de un punto de administración, habilite HTTPS en todos los puntos de administración del sitio con los que un cliente administrado por BitLocker podría comunicarse potencialmente. Si el punto de administración de HTTPS no está disponible, el cliente podría conmutar por error a un punto de administración de HTTP y, posteriormente, no poder realizar la custodia de su clave de recuperación.
>
> Esta recomendación se aplica a ambas opciones: habilitar el punto de administración para HTTPS o habilitar el sitio web de IIS que hospeda el servicio de recuperación en el punto de administración.

### <a name="sql-encryption-certificate"></a>Certificado de cifrado de SQL

Use este certificado para habilitar el cifrado de nivel de celda de SQL Server de los datos de recuperación de BitLocker. Puede usar su propio proceso para crear e implementar el certificado de cifrado de administración de BitLocker, siempre que cumpla los siguientes requisitos:

- El nombre del certificado de cifrado de administración de BitLocker debe ser `BitLockerManagement_CERT`.

- Cifre este certificado con una clave maestra de base de datos.

- Los siguientes usuarios de SQL necesitan permisos de **control** en el certificado:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Implemente el mismo certificado en todas las bases de datos del sitio de la jerarquía.

- Cree el certificado con la versión más reciente de SQL Server en su entorno. Por ejemplo:
  - Los certificados creados con SQL Server 2016 o versiones posteriores son compatibles con SQL Server 2014 o versiones anteriores.
  - Los certificados creados con SQL Server 2014 o versiones anteriores no son compatibles con SQL Server 2016 o versiones posteriores.

## <a name="example-scripts"></a>Scripts de ejemplo

Estos scripts SQL son ejemplos para crear e implementar un certificado de cifrado de administración de BitLocker en la base de datos del sitio de Configuration Manager.

### <a name="create-certificate"></a>Creación de certificado

Este script de ejemplo realiza las siguientes acciones:

- Crea un certificado
- Establece los permisos
- Crea una clave maestra de base de datos

Antes de usar este script en un entorno de producción, cambie los valores siguientes:

- Nombre de la base de datos del sitio (`CM_ABC`)
- Contraseña para crear la clave maestra (`MyMasterKeyPassword`)
- Fecha de expiración de certificado (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Copia de seguridad del certificado

Este script de ejemplo hace una copia de seguridad de un certificado. Al guardar el certificado en un archivo, puede [restaurarlo](#restore-certificate) en otras bases de datos en la jerarquía del sitio.

Antes de usar este script en un entorno de producción, cambie los valores siguientes:

- Nombre de la base de datos del sitio (`CM_ABC`)
- Ruta y nombre de archivo (`C:\BitLockerManagement_CERT_KEY`)
- Contraseña de la clave de exportación (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Almacene el archivo de certificado exportado y la contraseña asociada en una ubicación segura.

### <a name="restore-certificate"></a>Restauración de certificados

Este script de ejemplo restaura un certificado desde un archivo. Utilice este proceso para implementar un certificado creado en otra base de datos del sitio.

Antes de usar este script en un entorno de producción, cambie los valores siguientes:

- Nombre de la base de datos del sitio (`CM_ABC`)
- Contraseña de clave maestra (`MyMasterKeyPassword`)
- Ruta y nombre de archivo (`C:\BitLockerManagement_CERT_KEY`)
- Contraseña de la clave de exportación (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Comprobación de certificado

Use este script SQL para comprobar que SQL ha creado correctamente el certificado con los permisos necesarios.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Si el certificado es válido, el script devuelve un valor de `1`.

## <a name="see-also"></a>Vea también

Para obtener más información sobre estos comandos SQL, consulte los siguientes artículos:

- [SQL Server y claves de cifrado de base de datos (motor de base de datos)](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Creación de certificado](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [Copia de seguridad de certificado](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [Creación de clave maestra](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [Copia de seguridad de clave maestra](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [GRANT (permisos de certificado de Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
