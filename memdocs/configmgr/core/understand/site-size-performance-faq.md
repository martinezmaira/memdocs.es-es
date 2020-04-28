---
title: Preguntas más frecuentes sobre rendimiento y tamaño del sitio
titleSuffix: Configuration Manager
description: Respuestas a preguntas habituales de Configuration Manager sobre rendimiento y tamaño del sitio.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073269"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Preguntas más frecuentes sobre rendimiento y tamaño del sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este documento se abordan las preguntas más frecuentes sobre las instrucciones de ajuste de tamaño de sitios de Configuration Manager y problemas de rendimiento comunes.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Preguntas más frecuentes y ejemplos de configuración de equipos y discos

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>¿Cómo debo formatear los discos del servidor de sitio y SQL Server?

Separe las bandejas de entrada de Configuration Manager y los archivos SQL en al menos dos volúmenes distintos. Esta separación le permite optimizar los tamaños de asignación de clúster para los distintos tipos de operaciones de E/S que realizan. 

Para el volumen en el que se hospedan las bandejas de entrada del servidor de sitio, use NTFS con unidades de asignación de 4K u 8K. ReFS escribe 64k incluso para archivos pequeños. Configuration Manager tiene muchos archivos pequeños, por lo que ReFS puede generar una sobrecarga del disco innecesaria.

Para los discos que contienen archivos de base de datos SQL, use formato NTFS o ReFS, con unidades de asignación de 64K.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>¿Cómo y dónde debo diseñar los archivos de base de datos SQL?

Las matrices modernas de unidades de estado sólido (SSD) y Azure Premium Storage pueden ofrecer E/S por segundo elevada en un único volumen, con pocos discos. Normalmente, se agregan más unidades a una matriz para obtener almacenamiento adicional, no rendimiento adicional. Si usa discos físicos basados en cilindros, es posible que necesite más E/S por segundo de la que puede generar en un único volumen. Debe asignar el 60 % del total recomendado de E/S por segundo y espacio de disco al archivo *.mdf*, 20 % al archivo *.ldf* y 20 % a los archivos temporales de registro y datos. Los archivos *.ldf* y temporales pueden residir en un único volumen con un 40 % (20 % + 20 %) de la E/S por segundo asignada.

Los servidores SQL Server anteriores a SQL Server 2016 creaban de forma predeterminada un solo archivo de datos temporal. Debe crear más, para evitar bloqueos de SQL y esperas para acceder a un único archivo. Las opiniones de la comunidad varían con respecto al número óptimo de archivos de datos temporales que se deben crear, de cuatro a ocho. Las pruebas apenas revelan diferencias entre cuatro y ocho, por lo que puede crear cuatro archivos de datos temporales *del mismo tamaño*. Los archivos de datos tempdb deben tener hasta el 20-25 % del tamaño de la base de datos completa.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>¿Hay otras recomendaciones para la configuración de los discos?

Cuando se pueda configurar, establezca la asignación de memoria del controlador RAID en 70 % para las operaciones de escritura y en 30 % para las de lectura. En general, use una configuración de matriz RAID 10 para la base de datos. RAID 1 también se admite para sitios a pequeña escala con requisitos de E/S bajos, o si usa SSD rápidos. Con matrices de discos más grandes, configure discos de reserva para reemplazar de forma automática los discos con errores.

**Ejemplo: equipo físico con discos físicos** 

Las [instrucciones de ajuste de tamaño](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para un servidor de sitio colocado y SQL server con **100 000** clientes son 1200 E/S por segundo para las bandejas de entrada del servidor de sitio y 5000 E/S por segundo para los archivos de SQL Server.

Es posible que la configuración de discos resultante tenga este aspecto:

| Unidades<sup>1</sup> | RAID | Formato | Contenido del volumen | Mínimo de E/S por segundo necesario| E/S por segundo aproximada proporcionada<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | Bandejas de entrada de Configuration Manager    |     1700            | 1751             |
| 12x15k         | 10        | ReFS de 64k    | Archivo .mdf de SQL             | 60 %*5000 = 3000     | 3476             |
| 8x15k          | 10        | ReFS de 64k    | Archivo .ldf de SQL, archivos temporales | 40 %*5000 = 2000     | 2322             |

1. No se incluyen los discos de reserva recomendados. 
2. Este valor es de [Configuraciones de disco de ejemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Uso Hyper-V en Windows Server. ¿Cómo tengo que configurar los discos de las máquinas virtuales de Configuration Manager para obtener el mejor rendimiento?

Hyper-V ofrece un rendimiento similar a un servidor físico, si los recursos de hardware (núcleos de CPU y almacenamiento de paso a través) están 100 % dedicados a la máquina virtual (VM). El uso de archivos de disco *.vhd* o *.vhdx* de tamaño fijo tiene un impacto de rendimiento de E/S mínimo de 1-5 %. El uso de archivos de disco *.vhd* o *.vhdx* de expansión dinámica tiene un impacto de rendimiento de E/S de hasta el 25 % para la carga de trabajo de Configuration Manager. Si necesita discos de expansión dinámica, lo puede compensar mediante la adición de un 25 % extra de rendimiento de E/S por segundo a la matriz.

Al ejecutar el servidor de sitio de Configuration Manager o SQL dentro de una máquina virtual, aísle las unidades de sistema operativo host Hyper-V de las unidades de sistema operativo de la máquina virtual y datos.

Para más información sobre la optimización de máquinas virtuales, vea [Optimización del rendimiento para servidores Hyper-V](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Ejemplo: Servidor de sitio basado en máquinas virtuales de Hyper-V** 

Las [instrucciones de ajuste de tamaño](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para un servidor de sitio colocado y SQL server con **150 000** clientes son 1800 E/S por segundo para las bandejas de entrada del servidor de sitio y 7400 E/S por segundo para los archivos de SQL Server.

Es posible que la configuración de discos resultante tenga este aspecto:

| Unidades<sup>1</sup> | RAID | Formato<sup>2</sup> | Contenido del volumen | Mínimo de E/S por segundo necesario| E/S por segundo aproximada proporcionada<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | SO del host de Hyper-V           | -                    | -                |
| 2x10k          | 1         | -              | SO del servidor de sitio (máquina virtual)       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | Bandejas de entrada de Configuration Manager (máquina virtual)    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | ReFS de 64k       | (VM) Host de SQL (todos los archivos) | 7400                 | 14346            |

1. No se incluyen los discos de reserva recomendados. 
2. Archivo *.vhdx* de paso a través y tamaño fijo para la unidad de la máquina virtual dedicada al volumen subyacente. 
3. Este valor es de [Configuraciones de disco de ejemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>¿Hay alguna sugerencia para los entornos de Configuration Manager en Microsoft Azure?

Para empezar, puede leer [Configuration Manager en Azure - Preguntas más frecuentes](configuration-manager-on-azure.md).

Las máquinas virtuales de infraestructura como servicio (IaaS) de Azure que aprovechan los discos basados en Premium Storage pueden tener un valor elevado de E/S por segundo. En estas máquinas virtuales, configure discos adicionales para las necesidades previstas de espacio de disco, en lugar de E/S por segundo adicional.

El almacenamiento de Azure es redundante de forma inherente y no requiere varios discos para lograr la disponibilidad. Puede seccionar los discos en el Administrador de discos o Espacios de almacenamiento para proporcionar rendimiento y espacio adicionales.

Para obtener más información y recomendaciones sobre cómo maximizar el rendimiento de Premium Storage y ejecutar servidores SQL Server en máquinas virtuales IaaS de Azure, vea:

- [Optimización del rendimiento de las aplicaciones](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Orientación sobre los discos](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Ejemplo: Servidor de sitio basado en Azure** 

Las [instrucciones de ajuste de tamaño](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para un servidor de sitio colocado y SQL server con **50 000** clientes son ocho núcleos, 32 GB y 1200 E/S por segundo para las bandejas de entrada del servidor de sitio, y 2800 E/S por segundo para los archivos de SQL Server.

Es posible que la máquina de Azure resultante sea de tipo DS13v2 (ocho núcleos, 56 GB) con la configuración de disco siguiente:

| Unidades | Formato | Contiene | Mínimo de E/S por segundo necesario| E/S por segundo aproximada proporcionada<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Estándar&gt; | -             | SO de servidor de sitio     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | Bandejas de entrada de Configuration Manager  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | ReFS de 64k      | SQL (todos los archivos<sup>2</sup>) | 2800                 | 3112             |

1. Este valor es de [Configuraciones de disco de ejemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. En las [instrucciones de Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) se permite colocar TempDB en la unidad *D:* local basada en SSD, siempre que no supere el espacio disponible y permita la distribución de E/S de disco adicional.

**Ejemplo: Servidor de sitio basado en Azure (para aumento de rendimiento instantáneo)** 

El rendimiento de discos de Azure está limitado por el tamaño de la máquina virtual. La configuración del ejemplo anterior de Azure puede limitar la expansión futura o el rendimiento adicional. Si agrega más discos durante la implementación inicial de la máquina virtual de Azure, en el futuro puede convertirla para tener una mayor capacidad de procesamiento, con una inversión inicial mínima. Es mucho más sencillo planear con antelación el aumento del rendimiento del sitio para adaptarse a los cambios de requisitos, en lugar de tener que realizar una migración más complicada después.

Cambie los discos del ejemplo anterior de Azure para ver cómo cambia el valor de E/S por segundo.

**DS13v2** 

| Unidades<sup>1</sup> | Formato | Contiene | Mínimo de E/S por segundo necesario| E/S por segundo aproximada proporcionada<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Estándar&gt; | -             | SO de servidor de sitio     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | Bandejas de entrada de Configuration Manager  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | ReFS de 64k      | SQL (todos los archivos<sup>3</sup>) | 2800                 | 3984             |

1. Los discos se seccionan mediante Espacios de almacenamiento.
2. Este valor es de [Configuraciones de disco de ejemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). El tamaño de la máquina virtual limita el rendimiento.
3. En las [instrucciones de Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) se permite colocar TempDB en la unidad *D:* local basada en SSD, siempre que no supere el espacio disponible y permita la distribución de E/S de disco adicional.

Si necesita más rendimiento en el futuro, puede convertir la máquina virtual en un modelo DS14v2, lo que duplicará la memoria y la CPU. El ancho de banda de disco adicional que aporta ese tamaño de máquina virtual también aumentará al instante la E/S por segundo de disco disponible en los discos configurados anteriormente.

**DS14v2**

| Unidades<sup>1</sup> | RAID | Formato | Contiene | Mínimo de E/S por segundo necesario| E/S por segundo aproximada proporcionada<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Estándar&gt; | -             | SO de servidor de sitio     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | Bandejas de entrada de Configuration Manager  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | ReFS de 64k      | SQL (todos los archivos<sup>3</sup>) | 2800                 | 6182             |

1. Los discos se seccionan mediante Espacios de almacenamiento.
2. Este valor es de [Configuraciones de disco de ejemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). El tamaño de la máquina virtual limita el rendimiento.
3. En las [instrucciones de Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) se permite colocar TempDB en la unidad *D:* local basada en SSD, siempre que no supere el espacio disponible y permita la distribución de E/S de disco adicional.

## <a name="other-common-sql-server-related-performance-questions"></a>Otras preguntas comunes relacionadas con el rendimiento de SQL Server 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>¿Es mejor ejecutar con SQL colocado con el servidor de sitio, o bien ejecutarlo en un servidor remoto?

En ambos casos el rendimiento es correcto, siempre que el servidor único tenga el tamaño adecuado, o bien haya conectividad de red suficiente entre los dos servidores.

SQL remoto requiere el coste operativo y por adelantado de un servidor adicional, pero es habitual entre la mayoría de los clientes a gran escala. Las ventajas de esta configuración son las siguientes:

- Mayores opciones de disponibilidad de sitio, como Always On de SQL
- Capacidad de ejecutar multitud de informes con menos sobrecarga para el procesamiento del sitio
- Recuperación ante desastres más sencilla en algunas situaciones
- Administración de seguridad más sencilla
- Separación de roles para la administración de SQL, como con un equipo DBA independiente

SQL colocado requiere un único servidor y es habitual para la mayoría de clientes a pequeña escala. Las ventajas de esta configuración son las siguientes:

- Reducción de costes de equipos, licencias y mantenimiento
- Reducción de los puntos de error en el sitio
- Control mejorado para planificar el tiempo de inactividad

### <a name="how-much-ram-should-i-allocate-for-sql"></a>¿Cuánta RAM debo asignar para SQL?

De forma predeterminada, SQL usa toda la memoria disponible en el servidor, y podría agotar completamente el sistema operativo y otros procesos del equipo. Para evitar posibles problemas de rendimiento, es importante asignar memoria para SQL de forma explícita. En los servidores de sitio que se colocan con servidores SQL Server, asegúrese de que el sistema operativo tenga RAM suficiente para el almacenamiento de los archivos en caché y otras operaciones. Asegúrese de que haya memoria RAM suficiente para SMSExec y otros procesos de Configuration Manager. Al ejecutar SQL en un servidor remoto, puede asignar la *mayor parte* de la memoria a SQL, pero no toda. Revise las [instrucciones de ajuste de tamaño](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para obtener instrucciones iniciales. 

La asignación de memoria de SQL Server se debe redondear a cantidades enteras de GB. Además, cuando la memoria RAM aumente a grandes cantidades, puede permitir que SQL tenga un porcentaje mayor. Por ejemplo, cuando se disponga de 256 GB de RAM o más, puede configurar SQL hasta el 95 %, ya que todavía se conservará una gran cantidad de memoria para el sistema operativo. La supervisión del archivo de paginación es una buena forma de asegurarse de que haya memoria suficiente para el sistema operativo y los procesos de Configuration Manager.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Hoy en día los núcleos son económicos. ¿Debo agregar simplemente un montón de ellos al servidor SQL?

Es posible que experimente problemas de contención de memoria si en SQL server hay más de 16 núcleos físicos y no hay suficiente memoria RAM. La carga de trabajo de Configuration Manager funciona mejor cuando al menos hay 3-4 GB de RAM por núcleo disponible para SQL. Al agregar núcleos a los servidores SQL, asegúrese de aumentar la RAM en cantidades proporcionales.

### <a name="will-sql-always-on-impact-my-performance"></a>¿Afectará Always On de SQL al rendimiento?

En general, Always On de SQL tiene un efecto insignificante en el rendimiento del sistema cuando hay redes suficientes disponibles entre los servidores de réplica SQL. En un entorno ocupado de Always On de SQL, los archivos *.ldf* de registro de base de datos pueden crecer rápidamente. Pero el espacio del archivo de registro se libera de forma automática después de una copia de seguridad correcta de la base de datos. Agregue un trabajo SQL para que la base de datos de Configuration Manager realice una copia de seguridad cada 24 horas, por ejemplo, y una copia de seguridad de *.ldf* cada 6. Para más información sobre Always On de SQL y Configuration Manager, incluidas las estrategias de copia de seguridad de SQL, vea [SQL Server Always On para una base de datos de sitio de alta disponibilidad](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="should-i-enable-sql-compression-on-my-database"></a>¿Debo habilitar la compresión de SQL en la base de datos?

La compresión de SQL no se recomienda para la base de datos de Configuration Manager. Aunque no hay ningún problema funcional con la habilitación de la compresión en una base de datos de Configuration Manager, los resultados de las pruebas no muestran un ahorro de tamaño significativo en comparación con el posible impacto del rendimiento para el sistema.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>¿Debo habilitar el cifrado de SQL en la base de datos?

Los secretos de la base de datos de Configuration Manager ya se almacenan de forma segura, pero la adición de cifrado de SQL puede agregar otra capa de seguridad. No hay ningún problema funcional con la habilitación del cifrado en la base de datos, pero puede haber una degradación del rendimiento de hasta el 25 %, en función de las tablas que decida cifrar y la versión de SQL que use. Por tanto, utilice el cifrado con precaución, especialmente en entornos a gran escala. Además, no olvide actualizar la copia de seguridad y los planes de recuperación para asegurarse de que los datos cifrados se puedan recuperar correctamente.

### <a name="what-version-of-sql-should-i-run"></a>¿Qué versión de SQL se debe ejecutar?

Para ver las versiones compatibles de SQL, vea [Versiones de SQL Server compatibles](../plan-design/configs/support-for-sql-server-versions.md). Desde la perspectiva del rendimiento, todas las versiones de SQL compatibles cumplen los criterios de rendimiento necesarios. Pero SQL 2012 y SQL 2016, o versiones más recientes, suelen superar el rendimiento de SQL 2014 en algunos aspectos de la carga de trabajo de Configuration Manager. Además, ejecutar SQL 2014 en el nivel de compatibilidad de SQL 2012 (110) mejora el rendimiento en general. Durante la instalación, las bases de datos de Configuration Manager que se ejecutan en SQL 2012 y SQL 2014 se establecen en el nivel de compatibilidad 110. SQL 2016 o versiones más recientes se establecen en el nivel de compatibilidad predeterminado de esa versión de SQL, por ejemplo, 130 para SQL 2016. La actualización de SQL en contexto no actualiza los niveles de compatibilidad hasta que se instale la siguiente versión principal de la rama actual de Configuration Manager. 

Si aprecia tiempos de expiración inusuales o lentitud en determinadas consultas SQL en SQL 2016 o versiones posteriores, por ejemplo al usar RBAC en la consola de administración, pruebe a cambiar el nivel de compatibilidad de SQL a 110 en la base de datos de Configuration Manager. La ejecución en el nivel de compatibilidad 110 de SQL en SQL 2014 y versiones más recientes es totalmente compatible. Para más información, vea [SQL query times out or console slow on certain Configuration Manager database queries](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d) (En algunas consultas de base de datos de Configuration Manager se agota el tiempo de espera de la consulta SQL o se ralentiza la consola).

A partir de enero de 2018, debe *evitar* las versiones de SQL siguientes, debido a diversos problemas conocidos relacionados con el rendimiento u otros posibles problemas:

- SQL 2012 SP3 CU1 a CU5
- SQL 2014 SP1 CU6 a SP2 CU2
- SQL 2016 RTM a CU3, SP1 CU3 a CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>¿Debo implementar tareas de indexación de SQL adicionales?

Sí, para mejorar el rendimiento de SQL, actualice los índices al menos una vez por semana y las estadísticas al menos una vez al día. Los scripts de terceros y la información adicional disponible en las comunidades de Configuration Manager y SQL pueden ayudar a optimizar estas tareas.

En sitios de gran tamaño, es posible que las tablas SQL, como CI\_CurrentComplianceStatusDetails, HinvChangeLog, sean grandes, en función de los patrones de uso. Es posible que tenga que reducir o modificar el enfoque de mantenimiento para ellas de forma individualizada.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>¿Cuándo debo usar la versión completa de SQL Server en lugar de SQL Express en los sitios secundarios?

SQL Express no tiene ninguna implicación de rendimiento significativa en los sitios secundarios, y es adecuado para la mayoría de los clientes. También es fácil de implementar y administrar, y es la configuración recomendada para casi todos los clientes de cualquier tamaño.

Hay una situación donde se podría necesitar una instalación completa de SQL Server. Si tiene un gran número de puntos de distribución y paquetes u orígenes en el entorno, es posible que se supere el límite de tamaño de 10 GB de SQL Express. Si el número de paquetes multiplicado por el número de puntos de distribución es más de 4 000 000, por ejemplo 2000 puntos de distribución con 2000 fragmentos de contenido, considere la posibilidad de usar la instalación completa de SQL Server en los sitios secundarios. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>¿Debo cambiar la configuración de MaxDOP en la base de datos?

En la mayoría de los casos, mantener la configuración en 0 (usar todos los procesadores disponibles) resulta óptimo para el rendimiento de procesamiento general.

Muchos administradores de Configuration Manager siguen las instrucciones descritas en [Recomendaciones y directrices para la opción de configuración "max degree of parallelism" en SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). En la mayoría del hardware moderno de gran tamaño, en estas instrucciones se sugiere un valor máximo de ocho. Pero si ejecuta muchas consultas más pequeñas en comparación con el número de procesadores, puede ser útil establecerlo en un número mayor. La limitación a ocho no es necesariamente la mejor configuración en sitios más grandes cuando hay más núcleos disponibles. 

En servidores SQL Server con más de ocho núcleos, comience con un valor de 0 y realice cambios solo si experimenta problemas de rendimiento o bloqueos excesivos. Si tiene que cambiar MaxDOP porque experimenta problemas de rendimiento con el valor 0, comience con un valor nuevo que como mínimo sea mayor o igual que el número mínimo recomendado de núcleos para el tamaño del servidor SQL de ese sitio. Cualquier valor inferior a este siempre tendrá implicaciones negativas en el rendimiento. Por ejemplo, un servidor SQL remoto para un sitio de 100 000 clientes necesita al menos 12 núcleos. Si el servidor SQL tiene 16 núcleos, comience a probar la configuración de MaxDOP con un valor de 12.

## <a name="other-common-performance-related-questions"></a>Otras preguntas comunes relacionadas con el rendimiento

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>¿Qué carpetas del servidor de sitio (o en otros roles) debería excluir del software antivirus?

Tenga cuidado al deshabilitar la protección antivirus en cualquier sistema. En entornos seguros y de gran volumen, se recomienda deshabilitar la *supervisión activa* para obtener un rendimiento óptimo.

Para más información sobre las exclusiones del antivirus recomendadas, vea [Recommended antivirus exclusions for Configuration Manager 2012 and Current Branch Site Servers, Site Systems, and Clients](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu) (Exclusiones del antivirus recomendadas para Configuration Manager 2012 y servidores de sitio, sistemas de sitio y clientes de la rama actual).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>¿Qué puedo hacer para mejorar el rendimiento de WSUS cuando se usa con Configuration Manager?

El cambio de algunos valores clave de IIS, como la longitud de cola y el límite de memoria privada de WsusPool, puede mejorar el rendimiento de WSUS, incluso en las instalaciones más pequeñas. Para más información, vea [Hardware recomendado](../plan-design/configs/recommended-hardware.md).

Además, asegúrese de que tiene las actualizaciones más recientes instaladas para el sistema operativo en el que se ejecuta WSUS:

- Windows Server 2012: cualquier actualización acumulativa que no sea de "Solo seguridad" publicada en octubre de 2017 o después. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: cualquier actualización acumulativa que no sea de "Solo seguridad" publicada en agosto de 2017 o después. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016: cualquier actualización acumulativa que no sea de "Solo seguridad" publicada en agosto de 2017 o después. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>¿Qué tipo de mantenimiento debo realizar en los servidores WSUS?

Vea [Guía completa sobre el mantenimiento de Microsoft WSUS y Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Me gustaría configurar la supervisión de rendimiento básica para el sitio. ¿Qué debo observar?

La supervisión de rendimiento del servidor tradicional funciona de manera eficaz para Configuration Manager en general. También puede aprovechar los distintos módulos de administración de System Center Operations Manager para Configuration Manager, SQL Server y Windows Server con el fin de supervisar el estado básico de los servidores. También puede supervisar de forma directa los contadores del Monitor de rendimiento de Windows (PerfMon) que proporciona Configuration Manager. Supervise los trabajos pendientes en las distintas bandejas de entrada para detectar señales de advertencia iniciales de posibles problemas de rendimiento de sitio o trabajos pendientes.

## <a name="see-also"></a>Vea también

- [Directrices de rendimiento y tamaño del sitio](../plan-design/configs/site-size-performance-guidelines.md)
- [Configuration Manager en Azure - Preguntas más frecuentes](configuration-manager-on-azure.md)
