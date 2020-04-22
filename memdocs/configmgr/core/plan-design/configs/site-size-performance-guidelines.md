---
title: Directrices de rendimiento y tamaño del sitio
titleSuffix: Configuration Manager
description: Instrucciones, metodología y resultados de pruebas de rendimiento relacionadas con el tamaño de sitio.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 7380621fdc7a7f4d26b4844df3ee9026f0997024
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688653"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Instrucciones sobre rendimiento y tamaño del sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager lidera la industria en escalabilidad y rendimiento. En otra documentación se describen los [límites máximos de escalabilidad admitida](size-and-scale-numbers.md) y las [instrucciones de hardware](recommended-hardware.md) para ejecutar sitios con los tamaños de entorno más grandes. En este artículo se proporcionan instrucciones de rendimiento adicionales para entornos de todos los tamaños. Estas instrucciones pueden ayudar a calcular con más precisión el hardware necesario para implementar Configuration Manager.

Este artículo se centra en el elemento que más contribuye a los cuellos de botella de rendimiento de Configuration Manager: el subsistema de entrada/salida de disco o IOPS. En el artículo:

- se presentan detalles y resultados de pruebas centrados en IOPS;
- se documenta cómo reproducir las pruebas con entornos y hardware propios;
- se sugieren requisitos de IOPS de disco para distintos entornos de tamaño. 

## <a name="performance-test-methodology"></a>Metodología de pruebas de rendimiento

Configuration Manager se puede implementar de diversas formas únicas, pero en cualquier descripción del ajuste de tamaño es importante comprender algunas variables. Una variable es el *intervalo de características*, como un ciclo de inventario. Otra variable es el número de usuarios, las implementaciones de software u otros *objetos* que el sistema implementa o a los que hace referencia. Las pruebas de rendimiento se aplican a estas variables como parte de una *carga*. La carga genera objetos a una velocidad típica para los clientes empresariales que usan implementaciones de producción en entornos de diferentes tamaños.

> [!NOTE] 
> Los datos de telemetría de cliente permiten probar las compilaciones de la actual rama con los escenarios, configuraciones y valores más comunes para la mayoría de los clientes. Las recomendaciones de este artículo se basan en estos promedios. Su experiencia puede variar en función de la configuración y el tamaño del entorno. Por lo general, Configuration Manager requiere sentido común en lo que a objetos e intervalos se refiere. Simplemente porque pueda recopilar todos los archivos de un sistema o establecer en un minuto el intervalo para un ciclo, no significa que deba hacerlo.

En las secciones siguientes se resaltan algunas configuraciones y opciones clave que se usan para probar y modelar las necesidades de procesamiento de las grandes empresas. Estas instrucciones permiten establecer expectativas básicas del rendimiento del sistema para los tamaños de hardware sugeridos.

### <a name="feature-intervals-settings"></a>Configuración de intervalos de características 
En la mayoría de las pruebas se deben usar intervalos predeterminados para los ciclos clave del sistema. Por ejemplo, las pruebas de inventario de hardware se realizan una vez por semana con un archivo *.mof* mayor que el predeterminado. Algunos intervalos de características periódicos, especialmente los ciclos de inventario de hardware y software, pueden tener efectos significativos en las características de rendimiento de un entorno. Los entornos que permiten intervalos predeterminados agresivos para la recopilación de datos necesitan hardware sobredimensionado directamente proporcional al aumento de la actividad. Por ejemplo, imagine que tiene 25 000 clientes de escritorio y quiere recopilar el inventario de hardware al doble de la velocidad del intervalo predeterminado. Para empezar, debería ajustar el tamaño del hardware del sitio como si tuviera 50 000 clientes.

### <a name="objects"></a>Objetos 
En las pruebas se debe usar la *media superior* de los objetos que las grandes empresas suelen utilizar con el sistema. Los valores típicos son miles de colecciones y aplicaciones que se implementan en cientos de miles de usuarios o sistemas. Las pruebas se deben ejecutar de forma simultánea con estos límites en *todos* los objetos del sistema. Muchos clientes aprovechan varias características, pero no suelen usar todas las del producto en estos límites máximos. Las pruebas que se realizan con todas las características del producto ayudan a garantizar el máximo rendimiento posible de todo el sistema y permiten agrupar las que algunos clientes puedan usar por encima de la media. 

### <a name="loads"></a>Cargas 
Las pruebas también se deben ejecutar en cargas de *día normal* mayores a las estándar mediante la realización de simulaciones que generen picos de demanda de uso en el sistema. Un ejemplo consiste en simular los lanzamientos de Patch Tuesday, para asegurarse de que el sistema pueda devolver datos de cumplimiento actualizados de forma puntual durante estos días de máxima actividad. Otro ejemplo es simular la actividad del sitio durante un ataque de malware generalizado, para garantizar la capacidad de respuesta y notificación a tiempo. Aunque en un día concreto los equipos implementados del tamaño recomendado se puedan infrautilizar, las situaciones más extremas requieren un búfer de procesamiento.

### <a name="configurations"></a>Configuraciones
Ejecute las pruebas en una combinación de hardware físico, Hyper-V y Azure, con una mezcla de sistemas operativos y versiones de SQL Server. Valide siempre los peores casos para la configuración admitida. Por lo general, Hyper-V y Azure devuelven resultados de rendimiento comparables al hardware físico equivalente cuando se configuran de forma similar. Los sistemas operativos de servidor más recientes suelen tener el mismo rendimiento o mejor que los sistemas operativos admitidos más antiguos. Mientras todas las plataformas admitidas cumplan los requisitos mínimos, normalmente las versiones más recientes de productos complementarios como Windows y SQL ofrecen un rendimiento incluso mejor. 

La mayor variación procede de las versiones de SQL Server en uso. Para más información sobre las versiones de SQL Server, vea [¿Qué versión de SQL se debe ejecutar?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run) 

## <a name="key-performance-determinants"></a>Factores determinantes clave de rendimiento

Puede probar y medir el rendimiento de Configuration Manager con una variedad de opciones, de maneras diferentes y con distintos tamaños de sitio. Los valores y objetos siguientes pueden afectar al rendimiento de forma drástica. Asegúrese de tenerlos en cuenta cuando pruebe y modele el rendimiento en el entorno.

> [!CAUTION]
> Mientras que algunos aspectos de Configuration Manager tienen valores máximos oficiales o límites de la interfaz de usuario que impiden el uso excesivo, superar las instrucciones puede tener efectos adversos significativos sobre el rendimiento de un sitio. Para superar los niveles recomendados o ignorar las instrucciones de ajuste de tamaño normalmente se requiere hardware de mayor tamaño, y es posible que el entorno no se pueda mantener hasta que se reduzca la frecuencia o el recuento de diversos objetos.

### <a name="hardware-inventory"></a>Inventario de hardware
Para probar el rendimiento de línea de base, establezca la recopilación de inventario de hardware a una vez por semana, con el tamaño de archivo *.mof* predeterminado y aproximadamente un 20 % de propiedades adicionales. No habilite todas las propiedades y recopile solo las que necesite realmente. Preste especial atención al recopilar propiedades, como la memoria virtual disponible, que *siempre* cambiarán con *cada* ciclo de inventario. La recopilación de estas propiedades puede provocar un exceso de renovación en todos los ciclos de inventario de todos los clientes.

### <a name="software-inventory"></a>Inventario de software
Para probar el rendimiento de línea base, establezca la recopilación de inventario de software en una vez por semana, *solo* con detalles de productos. La recopilación de muchos archivos puede generar una tensión significativa en el subsistema de inventario. Evite la especificación de filtros que podrían acabar recopilando miles de archivos entre muchos clientes, como *\*.exe* o *\*.dll*.

### <a name="collections"></a>Recopilaciones
Las pruebas de rendimiento de línea de base pueden incluir varias miles de recopilaciones con diferentes valores de ámbito, tamaño, complejidad y actualización. El rendimiento del sitio no es una función directa de la mera cantidad de colecciones de un sitio. El rendimiento también es un producto cruzado de la complejidad de consulta de las colecciones, de actualizaciones completas e incrementales, y la frecuencia de cambio, las dependencias entre las colecciones y los números de clientes en las colecciones.

Siempre que sea posible, minimice las colecciones que tengan consultas de regla dinámica complicadas o costosas. Para las colecciones que requieren estos tipos de reglas, establezca intervalos y horas de actualización adecuados para minimizar el impacto de la reevaluación de las colecciones en el sistema. Por ejemplo, actualice a medianoche en lugar de hacerlo a las 8:00.

Habilitar las actualizaciones incrementales en las colecciones garantiza actualizaciones rápidas y puntuales de la pertenencia a las colecciones. Pero aunque las actualizaciones incrementales son eficaces, siguen agregando carga al sistema. Equilibre la frecuencia de cambios que anticipa con la necesidad de las actualizaciones casi en tiempo real de la pertenencia. Por ejemplo, imagine que espera una elevada renovación de los miembros de la colección, pero no necesita actualizaciones casi en tiempo real de la pertenencia. Actualizar la colección con una actualización programada completa según un intervalo es más eficaz y genera menos carga en el sistema que habilitar las actualizaciones incrementales. 

Al habilitar las actualizaciones incrementales, reduzca las actualizaciones programadas completas en las mismas colecciones. Son solo un método de evaluación de respaldo, ya que las actualizaciones incrementales deben mantener actualizada la pertenencia a la colección casi en tiempo real. En [Procedimientos recomendados para las colecciones](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) se recomienda un número máximo de colecciones totales para las actualizaciones incrementales, pero como se indica en el artículo, su experiencia puede variar en función de muchos factores.

Las colecciones que solo tienen reglas de pertenencia directa y con una recopilación de restricción que no realiza actualizaciones incrementales no necesitan actualizaciones completas programadas. Deshabilite las programaciones de actualización para estos tipos de colecciones para evitar una carga innecesaria en el sistema. Si la recopilación de restricción usa actualizaciones incrementales, es posible que las colecciones con solo reglas de pertenencia directa no reflejen las actualizaciones de pertenencia durante un máximo de 24 horas, o bien hasta que se produzca una actualización programada.

Aunque no sea un procedimiento recomendado, algunas organizaciones crean cientos o incluso miles de colecciones como parte de distintos procesos empresariales. Si usa la automatización para crear colecciones, es importante habilitar de forma correcta todas las actualizaciones incrementales. Minimice y distribuya las programaciones de actualización completa para evitar zonas activas de evaluación de recopilación durante un período de tiempo único. Establezca un proceso de limpieza periódico para eliminar las colecciones sin usar, en especial si crea colecciones de forma automática que ya no necesitará más tarde.

Recuerde que Configuration Manager crea directivas para todos los objetos de las colecciones cuando se destinan a tareas como las implementaciones. Los cambios de pertenencia, ya sea a través de actualizaciones programadas o incrementales, pueden generar gran cantidad de trabajo adicional para el sistema. Las compilaciones más recientes de la rama actual tienen optimizaciones de directiva especiales para las recopilaciones Todos los sistemas y Todos los usuarios. Cuando el destino es toda la empresa, use las recopilaciones integradas en lugar de un clon de estas.

Para investigar aún más el rendimiento de las recopilaciones, puede usar Collection Evaluation Viewer (CEViewer) en el [Kit de herramientas de Configuration Manager](https://www.microsoft.com/download/details.aspx?id=50012).

### <a name="discovery-methods"></a>Métodos de detección
Para las pruebas de rendimiento de línea de base, ejecute métodos de detección basados en el servidor una vez por semana, lo que permite la detección de diferencias según resulte apropiado para mantener los datos actualizados durante la semana. Las pruebas deben detectar una cantidad de objetos proporcional al tamaño empresarial simulado. La prueba de línea de base de rendimiento para la detección de latidos también se debe ejecutar una vez por semana.

Los datos de detección son datos globales. Un problema común relacionado con el rendimiento es la configuración incorrecta de métodos de detección basados en el servidor en una jerarquía, lo que provoca duplicados de los mismos recursos de varios sitios primarios. Configure con atención los métodos de detección para optimizar la comunicación con el servicio de destino, como controladores de dominio de Active Directory, al tiempo que evita la duplicación del mismo ámbito de detección en varios sitios primarios.

## <a name="general-sizing-guidelines"></a>Instrucciones generales de ajuste de tamaño 

En función de la [metodología de pruebas de rendimiento](#performance-test-methodology) anterior, en la tabla siguiente se proporcionan instrucciones generales de requisitos de hardware *mínimos* para cantidades específicas de clientes administrados. Estos valores deben permitir que la mayoría de los clientes con el número especificado de clientes procesen objetos con la rapidez suficiente para administrar el sitio especificado. El precio de la potencia de computación sigue bajando cada año, y algunos de los requisitos siguientes son menores en cuanto a las configuraciones de hardware de servidor moderno se refiere. El hardware que supera las instrucciones siguientes aumenta proporcionalmente el rendimiento de los sitios que requieren capacidad de procesamiento adicional, o que tienen patrones de uso de productos especiales. 

| Clientes de escritorio  | Tipo de sitio/Rol  | Núcleos<sup>1</sup>   | Memoria (GB)   | Asignación de memoria SQL  | IOPS:  Bandejas de entrada<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Espacio de almacenamiento necesario (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Sitio primario o CAS con rol de sitio de base de datos en el mismo servidor   | 6   | 24  | 65 % | 600  | 1700 | 350  |
| 25k  | Sitio primario o CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | SQL remoto                                                  | 4   | 16  | 70 % |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50k  | Sitio primario o CAS con rol de sitio de base de datos en el mismo servidor   | 8   | 32  | 70 % | 1200 | 2800 | 600  |
| 50k  | Sitio primario o CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | SQL remoto                                                  | 8   | 24  | 70 % |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100k | Sitio primario o CAS con rol de sitio de base de datos en el mismo servidor   | 12  | 64  | 70 % | 1200 | 5000 | 1100 |
| 100k | Sitio primario o CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | SQL remoto                                                  | 12  | 48  | 80 % |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Sitio primario o CAS con rol de sitio de base de datos en el mismo servidor   | 16  | 96  | 70 % | 1800 | 7400 | 1600 |
| 150k | Sitio primario o CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | SQL remoto                                       | 16  | 72   | 90 % |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | CAS con rol de sitio de base de datos en el mismo servidor   | Más de 20 | Más de 128 | 80 % | Más de 1800 | Más de 9000   | Más de 5000 |
| 700k | CAS                                              | Más de 8  | Más de 16  |     | Más de 1800 |         | Más de 500  |
|      | SQL remoto                                       | Más de 16 | Más de 96  | 90 % |       | Más de 9000   | Más de 4500 |
|      |                                                             |     |     |     |      |      |      |
| 5k   | Sitio secundario                                   | 4   | 8    |     | 500   | -       | 200   |
| 15k  | Sitio secundario                                   | 8   | 16   |     | 500   | -       | 300   |

**Notas**

1. **Núcleos**: Configuration Manager realiza muchos procesos simultáneos, por lo que necesita un número mínimo de núcleos de CPU para diversos tamaños de sitio. Aunque cada año los núcleos son más rápidos, es importante asegurarse de que un número mínimo de núcleos funcionan en paralelo. Por lo general, cualquier CPU de nivel de servidor fabricada después de 2015 cumple las necesidades de rendimiento básico para los núcleos especificados en la tabla. Configuration Manager aprovecha las ventajas de los núcleos adicionales más allá de las recomendaciones, pero por lo general, una vez que tenga los núcleos mínimos sugeridos, debe priorizar la inversión en recursos de CPU para aumentar la velocidad de los núcleos existentes, no agregar más núcleos más lentos. Por ejemplo, Configuration Manager funcionará mejor en tareas de procesamiento clave con 16 núcleos rápidos que con 24 núcleos más lentos, siempre que haya disponibles otros recursos del sistema como IOPS de disco.
   
   La relación entre los núcleos y la memoria también es importante. Por lo general, tener menos de 3-4 GB de RAM por núcleo reduce la capacidad de procesamiento total de los servidores SQL. Necesitará más RAM por núcleo cuando SQL se coloque con los componentes de servidor de sitio.
   
   > [!NOTE]
   > Todas las pruebas establecen planes de energía automáticos para permitir el máximo consumo de energía y rendimiento de CPU.
   
2. **IOPS: bandejas de entrada e IOPS: SQL** hacen referencia a las necesidades de E/S por segundo para las unidades lógicas de Configuration Manager y SQL. En la columna **IOPS: bandejas de entrada** se muestran los requisitos de IOPS para la unidad lógica donde residen los directorios de la bandeja de entrada de Configuration Manager. En la columna **IOPS: SQL** se muestra el total de E/S por segundo que se necesita para las unidades lógicas que usan los distintos archivos SQL. Estas columnas son diferentes porque las dos unidades deben tener un formato distinto. Para obtener más información y ejemplos de configuraciones de disco SQL sugeridas y procedimientos recomendados de archivo, incluidos detalles sobre la división de archivos entre varios volúmenes, vea las [Preguntas más frecuentes sobre rendimiento y tamaño del sitio](../../understand/site-size-performance-faq.md).
   
   En estas dos columnas IOPS se usan datos de la herramienta estándar del sector, *Diskspd*. Vea [Procedimientos para medir el rendimiento de disco](#how-to-measure-disk-performance) para obtener instrucciones sobre cómo duplicar estas mediciones. Por lo general, una vez que se cumplen los requisitos básicos de memoria y CPU, el subsistema de almacenamiento tiene el mayor impacto sobre el rendimiento del sitio y las mejoras en este sentido ofrecen el mejor retorno para la inversión.
   
3.  **Espacio de almacenamiento necesario:** estos valores reales pueden diferir de otras recomendaciones documentadas. Estas cifras solo se proporcionan como una instrucción general; los requisitos individuales pueden variar ampliamente. Planee cuidadosamente las necesidades de espacio en disco antes de la instalación del sitio. Asuma que cierta cantidad de este almacenamiento permanecerá como espacio libre en disco la mayoría del tiempo. Puede usar este espacio de búfer en un escenario de recuperación, o bien para escenarios de actualización en los que es necesario liberar espacio en disco para la expansión de paquetes de instalación. Es posible que el sitio requiera almacenamiento adicional para grandes cantidades de recopilación de datos, períodos de retención de datos más prolongados y grandes cantidades de contenido de distribución de software. También puede almacenar estos elementos en volúmenes independientes y de rendimiento inferior.

## <a name="how-to-measure-disk-performance"></a>Cómo medir el rendimiento del disco 

Puede usar la herramienta estándar de la industria *Diskspd* para proporcionar sugerencias estandarizadas para la E/S por segundo que requieren los entornos de Configuration Manager de distintos tamaños. Aunque no sea de forma exhaustiva, en los siguientes pasos de prueba y líneas de comandos se proporciona una manera sencilla y reproducible de calcular el rendimiento del subsistema de discos de los servidores. Puede comparar los resultados con la E/S por segundo mínima recomendada en la tabla de [instrucciones generales de ajuste de tamaño](#general-sizing-guidelines). 

Vea [Configuraciones de disco de ejemplo](#example-disk-configurations) para obtener resultados de pruebas en una variedad de configuraciones de hardware en entornos de laboratorio. Puede usar los datos como punto de partida aproximado cuando diseñe desde cero el subsistema de almacenamiento para un entorno nuevo.

### <a name="to-test-disk-iops"></a>Para probar E/S por segundo disco  
1. Descargue la utilidad *Diskspd* aquí: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Asegúrese de que tiene al menos 100 GB de espacio libre en disco. Deshabilite todas las aplicaciones que podrían interferir o causar una carga adicional en el disco, como el análisis antivirus activo del directorio, SQL o SMSExec.
   
1. Ejecute *Diskspd* desde un símbolo del sistema con privilegios elevados. 
   
   Ejecute la herramienta dos veces seguidas para el volumen que quiera probar. La primera prueba realiza operaciones aleatorias de escritura de 64k durante un minuto. Esta prueba garantiza la carga de caché de controlador y la asignación de espacio en disco, en caso de que el volumen sea de expansión dinámica. Descarte los resultados de la primera prueba. La segunda prueba debería seguir *inmediatamente* a la primera, y realizar la misma carga durante cinco minutos.
   
   Por ejemplo, use las líneas de comandos específicas siguientes para probar el volumen G:\\.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Revise el resultado de la segunda prueba para buscar el total de E/S por segundo en la columna **I/O per s** (E/S por segundo). En el ejemplo siguiente, el número total de IOPS es **3929,18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Configuraciones de disco de ejemplo

En las tablas siguientes se muestran los resultados de la ejecución de los pasos de prueba de [Cómo medir el rendimiento de disco](#how-to-measure-disk-performance) con varias configuraciones de laboratorio de prueba. Use estos datos como punto de partida *aproximado* cuando diseñe desde cero el subsistema de almacenamiento para un entorno nuevo. 

### <a name="physical-machines-and-hyper-v"></a>Máquinas físicas e Hyper-V 
El hardware siempre mejora. Puede esperar que las nuevas generaciones de hardware y las combinaciones de hardware diferente, como SSD y SAN, superen el rendimiento que se indica a continuación. Estos resultados son un punto de partida básico que tener en cuenta al diseñar un servidor o hablar con el fabricante del hardware.

En la tabla siguiente se muestran los resultados de pruebas en diversos subsistemas de disco, incluidos disco duros basados en SSD y cilindros, en varias configuraciones de laboratorio de prueba. Todas las configuraciones dan formato a los discos con clústeres de 64k y los adjuntan a un controlador de disco de clase empresarial. Además del número de discos de las matrices RAID, cada uno tiene al menos un disco de reserva.

| Tipo de disco   | Número de discos, sin incluir 1 disco de reserva adicional | RAID     | Medición de IOPS  |
|------------------|----------------------------------------------------|---------------|---------------|
| SAS 15k          | 2                                                  |           1   | 620           |
| SAS 15k          | 4                                                  |           10  | 1206          |
| SAS 15k          | 6                                                  |           10  | 1751          |
| SAS 15k          | 8                                                  |           10  | 2322          |
| SAS 15k          | 10                                                 |           10  | 2882          |
| SAS 15k          | 12                                                 |           10  | 3476          |
| SAS 15k          | 16                                                 |           10  | 4236          |
| SAS 15k          | 20                                                 |           10  | 5148          |
| SAS 15k          | 30                                                 |           10  | 7398          |
| SAS 15k          | 40                                                 |           10  | 9913          |
| SATA SSD         | 2                                                  |           1   | 3300          |
| SATA SSD         | 4                                                  |           10  | 5542          |
| SATA SSD         | 6                                                  |           10  | 7201          |
| SAS SSD          | 2                                                  |           1   | 7539          |
| SAS SSD          | 4                                                  |           10  | 14346         |
| SAS SSD          | 6                                                  |           10  | 15607         |

Estos son los dispositivos que se usan en el ejemplo. Esta información no es una recomendación para ningún fabricante o modelo de hardware específico. 

| Tipo de disco    | Modelo      | Controlador RAID | Memoria caché y configuración |
|-------------------|-----------------|----------------------|-------------------------------------|
| HD SAS 15000 RPM    | HP EH0300JDYTH  | Smart Array P822     | 2 GB, 20 % lectura / 80 % escritura           |
| SATA SSD          | ATA MK0200GCTYV | Smart Array P420i    | 1 GB, 20 % lectura / 80 % escritura           |
| SAS SSD           | HP MO0800 JEFPB | Smart Array P420i    | 1 GB, 20 % lectura / 80 % escritura           |

### <a name="azure-machine-and-disk-performance"></a>Rendimiento de disco y máquinas de Azure 
El rendimiento de disco de Azure depende de varios factores, como el tamaño de la máquina virtual de Azure y el número y tipo de discos que usa. Azure también agrega constantemente nuevos tipos de máquina y velocidades de disco diferentes a los del gráfico siguiente. Para más información sobre la ejecución de Configuration Manager en Azure y obtener información adicional sobre la E/S de disco de en Azure, vea [Configuration Manager en Azure - Preguntas más frecuentes](../../understand/configuration-manager-on-azure.md).

Todos los discos tienen el formato NTFS con clústeres de 64k de tamaño, y las filas con más de un disco se configuran como volúmenes seccionados mediante la utilidad Administración de discos de Windows.

| VM de Azure| Disco de Azure| Número de discos | Espacio disponible | Medición de IOPS   | Factor de limitación   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Tamaño de VM de Azure   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Tamaño de la máquina virtual de Azure   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Tamaño de la máquina virtual de Azure   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Tamaño de VM de Azure   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1994  | Tamaño de VM de Azure   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1024 MB                   | 1992  | Tamaño de VM de Azure   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1024 MB                   | 1993  | Tamaño de VM de Azure   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2048 MB                   | 1992  | Tamaño de VM de Azure   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2334  | Disco P20        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1024 MB                   | 3984  | Tamaño de VM de Azure   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1536 MB                   | 3984  | Tamaño de VM de Azure   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1024 MB                   | 3112  | Disco P30        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2048 MB                   | 3984  | Tamaño de VM de Azure   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3072 MB                   | 3996  | Tamaño de VM de Azure   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2335  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1024 MB                   | 4639  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1536 MB                   | 6913  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2048 MB                   | 7966  | Tamaño de VM de Azure   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1024 MB                   | 3112  | Disco P30        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2048 MB                   | 6182  | Disco P30        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3072 MB                   | 7963  | Tamaño de VM de Azure   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4096 MB                   | 7968  | Tamaño de VM de Azure   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | Disco P30        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | Disco P30        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | Disco P30        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Tamaño de VM de Azure   |

## <a name="see-also"></a>Vea también

- [Preguntas más frecuentes sobre rendimiento y tamaño del sitio](../../understand/site-size-performance-faq.md)
- [Configuration Manager en Azure - Preguntas más frecuentes](../../understand/configuration-manager-on-azure.md)
- [Números de tamaño y escala](size-and-scale-numbers.md)
- [Hardware recomendado](recommended-hardware.md)

