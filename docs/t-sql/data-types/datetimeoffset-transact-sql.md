---
title: DateTimeOffset (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetimeoffset_TSQL
- datetimeoffset
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a6c143380711d1af39a6c11f311e9ce3caf87c7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define una fecha que se combina con una hora del día con reconocimiento de zona horaria y basado en un reloj de 24 horas.
  
## <a name="datetimeoffset-description"></a>Descripción de DateTimeOffset
  
|Propiedad|Valor|  
|---|---|
|Sintaxis|**DateTimeOffset** [(*precisión de fracciones de segundo*)]|  
|Uso|DECLARAR @MyDatetimeoffset **datetimeoffset(7)**<br /><br /> Crear tabla Table1 (Column1 **datetimeoffset(7)** )|  
|Formatos de literal de cadena predeterminados (utilizados para el cliente de nivel inferior)|AAAA-MM-DD hh [.nnnnnnn] [{+ &#124;-} hh: mm]<br /><br /> Para obtener más información, vea la sección "Compatibilidad con versiones anteriores de clientes de nivel inferior" que sigue.|  
|Intervalo de fechas|De 0001-01-01 a 31.12.99<br /><br /> El 1 de enero de 1 CE hasta el 31 de diciembre de 9999 CE|  
|Intervalo de horas|00:00:00 a 23:59:59.9999999 (no se admiten las fracciones de segundo de Informatica)|  
|Intervalo de ajuste de zona horaria|-14:00 a + 14:00 (se omite el desplazamiento de zona horaria de Informatica)|  
|Intervalos de elementos|AAAA es una cifra de cuatro dígitos comprendida entre 0001 y 9999 que representa un año.<br /><br /> MM es una cifra de dos dígitos comprendido entre 01 y 12, que representa un mes del año especificado.<br /><br /> DD es cifra de dos dígitos comprendido entre 01 y 31 dependiendo del mes, que representa un día del mes especificado.<br /><br /> hh es una cifra de dos dígitos comprendida entre 00 y 23 que representa la hora.<br /><br /> mm es una cifra de dos dígitos comprendida entre 00 y 59 que representa los minutos.<br /><br /> s es una cifra de dos dígitos comprendida entre 00 y 59 que representa los segundos.<br /><br /> n* es una cifra de cero a siete dígitos comprendida entre 0 y 9999999 que representa las fracciones de segundos. No se admiten las fracciones de segundo de Informatica.<br /><br /> hh es una cifra de dos dígitos comprendida entre -14 y 14. Se omite el desplazamiento de zona horaria de Informatica.<br /><br /> mm es una cifra de dos dígitos comprendida entre 00 y 59. Se omite el desplazamiento de zona horaria de Informatica.|  
|Longitud en caracteres|26 posiciones como mínimo (aaaa-MM-DD hh {+ &#124;-} hh: mm) a 34 como máximo (. nnnnnnn aaaa-MM-DD {+ &#124;-} hh: mm)|  
|Precisión, escala|Vea la siguiente tabla.|  
|Tamaño de almacenamiento|10 bytes, fijo es el valor predeterminado con el valor predeterminado de 100 ns de precisión de fracciones de segundo.|  
|Precisión|100 nanosegundos|  
|Valor predeterminado|1900-01-01 00:00:00 00:00|  
|Calendario|Gregoriano|  
|Precisión de fracciones de segundo definida por el usuario|Sí|  
|Conservación y reconocimiento del ajuste de zona horaria|Sí|  
|Reconocimiento del horario de verano|No|  
  
|Escala especificada|Resultado (precisión, escala)|Longitud de la columna (bytes)|Precisión de fracciones de segundo|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**DateTimeOffset(0)**|(26,0)|8|0-2|  
|**DateTimeOffset(1)**|(28,1)|8|0-2|  
|**DateTimeOffset(2)**|(29,2)|8|0-2|  
|**DateTimeOffset(3)**|(30,3)|9|3-4|  
|**DateTimeOffset(4)**|(31,4)|9|3-4|  
|**DateTimeOffset(5)**|(32,5)|10|5-7|  
|**DateTimeOffset(6)**|(33,6)|10|5-7|  
|**DateTimeOffset(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>Admite los formatos de literal de cadena para datetimeoffset
En la tabla siguiente se enumera los compatibles formatos literales de cadena de ISO 8601 para **datetimeoffset**. Para obtener información acerca de los formatos alfabético, numéricos, sin separación y el tiempo para las partes de fecha y hora de **datetimeoffset**, consulte [inte &#40; Transact-SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) y [tiempo &#40; Transact-SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|AAAA-MM-ddTHH [.nnnnnnn] [{+ &#124;-} hh: mm]|Estos dos formatos no se ven afectados por la configuración regional de sesión de SET LANGUAGE y SET DATEFORMAT. No se permiten espacios entre el **datetimeoffset** y **datetime** partes.|  
|AAAA-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|Este formato de la definición de ISO indica la **datetime** parte se debe expresar en hora Universal coordinada (UTC). Por ejemplo, 1999-12-12 12:30:30.12345 -07: 00 se deberían representar como 1999-12-12 19:30:30.12345 Z.|  
  
## <a name="time-zone-offset"></a>Ajuste de zona horaria
Un desplazamiento de zona horaria especifica el desplazamiento de zona a la hora UTC para un **tiempo** o **datetime** valor. El ajuste de zona horaria se puede representar como [+ | -] hh:mm:
-   hh es una cifra de dos dígitos comprendidos entre 00 a 14 y representa el número de horas en el ajuste de zona horaria.  
-   mm es una cifra de dos dígitos comprendidos entre 00 a 59 y representa el número minutos adicionales en el ajuste de zona horaria.  
-   \+(más) o – (menos) es el inicio de sesión obligatorio para un desplazamiento de zona horaria. Esto indica si el ajuste de zona horaria se agrega o resta de la hora UTC para obtener la hora local. El intervalo válido de ajuste de zona horaria es de -14: 00 a +14: 00.  
  
El intervalo del ajuste de zona horaria sigue la norma de W3C XML para la definición del esquema XSD y es ligeramente diferente de la definición estándar de SQL 2003, de 12:59 a +14: 00.
  
El parámetro de tipo opcional *precisión de fracciones de segundo* especifica el número de dígitos para la parte fraccionaria de los segundos. Este valor puede ser un entero con 0 a 7 (100 nanosegundos). El valor predeterminado *precisión de fracciones de segundo* es 100 NS (siete dígitos para la parte fraccionaria de los segundos).
  
Los datos se almacenan en la base de datos y se procesan, comparan, ordena e indizan en el servidor como en UTC. El ajuste de zona horaria se conservará en la base de datos para la recuperación.
  
El desplazamiento de zona horaria determinada se asumirá que el horario de verano (DST) tenga en cuenta y se ajustará para cualquier **datetime** que se encuentra en el período de horario de verano.
  
Para **datetimeoffset** escriba UTC y local (para el desplazamiento de zona horaria persistente o convertido) **datetime** valor se validarán durante las operaciones de inserción, actualización, aritmética, convert o asignar. La detección de cualquier válido UTC o local (para el desplazamiento de zona horaria persistente o convertido) **datetime** valor, producirá un error de valor no válido. Por ejemplo, 9999-12-31 10:10:00 son válidos en UTC, pero se desbordan en la hora local al ajuste de zona horaria +13: 50.
  
Para convertir una fecha en su correspondiente **datetimeoffset** valor en un destino de la zona horaria, vea [AT TIME ZONE &#40; Transact-SQL &#41; ](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>Cumplimiento de normas ANSI e ISO 8601  
Las secciones de ANSI e ISO 8601 cumplimiento de la [fecha](../../t-sql/data-types/date-transact-sql.md) y [tiempo](../../t-sql/data-types/time-transact-sql.md) temas se aplican a **datetimeoffset**.
  
## <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidad con versiones anteriores de clientes de nivel inferior
Algunos clientes de nivel inferior no admiten la **tiempo**, **fecha**, **datetime2** y **datetimeoffset** tipos de datos. En la tabla siguiente se muestra la asignación de tipo entre una instancia de nivel superior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los clientes de nivel inferior.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de datos|El formato del literal de cadena predeterminado se pasó al cliente de nivel inferior|ODBC de nivel inferior|OLEDB de nivel inferior|JDBC de nivel inferior|SQLCLIENT de nivel inferior|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
|**datetimeoffset**|AAAA-MM-DD hh [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
  
## <a name="converting-date-and-time-data"></a>Convertir datos de fecha y hora
Cuando se convierte a los tipos de datos de fecha y hora, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechaza todos los valores que no reconoce como fechas u horas. Para obtener información acerca de cómo utilizar las funciones CAST y CONVERT con datos de fecha y hora, vea [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
Al convertir a **fecha**, se copian el año, mes y día. En el código siguiente se muestran los resultados de convertir un valor `datetimeoffset(4)` en un valor `date`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10 +01:00';  
DECLARE @date date= @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @date AS 'date';  
  
--Result  
--@datetimeoffset                date  
-------------------------------- ----------  
--2025-12-10 12:32:10.0000 +01:0 2025-12-10  
--  
--(1 row(s) affected)  
  
```  
  
Si la conversión es a **Time (n)**, nuestro, minuto, segundo y fracciones de segundo se copian. Se trunca el valor de zona horaria. Cuando la precisión de la **DateTimeOffset (n)** valor es mayor que la precisión de la **Time (n)** valor, el valor se redondea. En el código siguiente se muestran los resultados de convertir un valor `datetimeoffset(4)` en un valor `time(3)`.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @time time(3) = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @time AS 'time';  
  
--Result  
--@datetimeoffset                time  
-------------------------------- ------------  
-- 2025-12-10 12:32:10.1237 +01:00    12:32:10.124  
  
--  
--(1 row(s) affected)  
  
```  
  
Al convertir a**datetime**, los valores de fecha y hora se copian y se trunca la zona horaria. Cuando la precisión fraccionaria de los **DateTimeOffset (n)** valor es superior a tres dígitos, el valor se trunca. En el código siguiente se muestran los resultados de convertir un valor `datetimeoffset(4)` en un valor `datetime`.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @datetime AS 'datetime';  
  
--Result  
--@datetimeoffset                datetime  
-------------------------------- -----------------------  
--2025-12-10 12:32:10.1237 +01:0 2025-12-10 12:32:10.123  
--  
--(1 row(s) affected)  
```  
  
Para las conversiones a **smalldatetime**, se copian a la fecha y horas. Los minutos se redondean hacia arriba con respecto al valor de los segundos y los segundos se establecen en 0. En el código siguiente se muestran los resultados de convertir un valor `datetimeoffset(3)` en un valor `smalldatetime`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(3) = '1912-10-25 12:24:32 +10:0';  
DECLARE @smalldatetime smalldatetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetimeoffset                @smalldatetime  
-------------------------------- -----------------------  
--1912-10-25 12:24:32.000 +10:00 1912-10-25 12:25:00  
--  
--(1 row(s) affected)  
```  
  
Si la conversión es a **datetime2**, la fecha y hora se copian en el **datetime2** se trunca el valor y la zona horaria. Cuando la precisión de la **datetime2** valor es mayor que la precisión de la **DateTimeOffset (n)** valor, las fracciones de segundo se truncan para ajustarse. En el código siguiente se muestran los resultados de convertir un valor `datetimeoffset(4)` en un valor `datetime2(3)`.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1912-10-25 12:24:32.1277 +10:0';  
DECLARE @datetime2 datetime2(3)=@datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @datetime2 AS '@datetime2';  
  
--Result  
@datetimeoffset                    @datetime2  
---------------------------------- ----------------------  
1912-10-25 12:24:32.1277 +10:00    1912-10-25 12:24:32.12  
  
--(1 row(s) affected)  
```  
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>Conversión de tipo de datos datetimeoffset a otra fecha y tipos de tiempo
En la tabla siguiente describe lo que ocurre cuando un **datetimeoffset** tipo de dato se convierte a otros tipos de datos de fecha y hora.
  
### <a name="converting-string-literals-to-datetimeoffset"></a>Convertir literales de cadena a datetimeoffset
Las conversiones de literales de cadena en tipos de fecha y hora son posibles cuando todas las partes de las cadenas están en formatos válidos. En caso contrario, se generará un error en el tiempo de ejecución. Las conversiones implícitas o explícitas que no especifican un estilo (desde tipos de fecha y hora hasta literales de cadena) estarán en el formato predeterminado de la sesión actual. La siguiente tabla muestra las reglas para convertir una cadena literal la **datetimeoffset** tipo de datos.
  
|Literal de cadena de entrada|**DateTimeOffset (n)**|  
|---|---|
|DATE de ODBC|Literales de cadena ODBC se asignan a la **datetime** tipo de datos. Cualquier operación de asignación de literales de DATETIME de ODBC en **datetimeoffset** tipos provocará una conversión implícita entre **datetime** y este tipo de acuerdo con las reglas de conversión.|  
|TIME de ODBC|Vea la regla anterior de DATE de ODBC.|  
|DATETIME DE ODBC|Vea la regla anterior de DATE de ODBC.|  
|Solo DATE|La parte de TIME tiene como valor predeterminado 00:00:00. TIMEZONE tiene como valor predeterminado +00:00.|  
|Solo TIME|La parte de DATE tiene como valor predeterminado 1900-1-1. TIMEZONE tendrá como valor predeterminado +00:00.|  
|Solo TIMEZONE|Se proporcionan los valores predeterminados.|  
|DATE + TIME|TIMEZONE tiene como valor predeterminado +00:00.|  
|DATE + TIMEZONE|No permitido|  
|TIME + TIMEZONE|La parte de DATE tiene como valor predeterminado 1900-1-1.|  
|DATE + TIME + TIMEZONE|Trivial|  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se compara los resultados de convertir una cadena a cada uno de ellos **fecha** y **tiempo** tipo de datos.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset'  
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetimeoffset(7)) AS  
        'datetimeoffset IS08601';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|Tipo de datos|Salida|  
|---|---|
|**Time**|12:35:29. 1234567|  
|**Fecha**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**Fecha y hora**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**DateTimeOffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[EN la zona HORARIA &#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  
