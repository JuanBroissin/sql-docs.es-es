---
title: 'Extensión del lenguaje Java en SQL Server 2019: SQL Server Machine Learning Services'
description: Instalar, configurar y validar la extensión del lenguaje Java en SQL Server 2019 para los sistemas Linux y Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a18886ea4daff3fb87853a556b67ad0562c2efd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017841"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Extensión del lenguaje Java en SQL Server 2019 

A partir de SQL Server 2019 preview en Windows y Linux, puede ejecutar código de Java personalizado en el [marco de extensibilidad](../concepts/extensibility-framework.md) como complemento a la instancia del motor de base de datos. 

El marco de extensibilidad es una arquitectura para la ejecución de código externo: Java (a partir de SQL Server 2019), [Python (a partir de SQL Server 2017)](../concepts/extension-python.md), y [R (a partir de SQL Server 2016)](../concepts/extension-r.md). Ejecución de código está aislada de los procesos del motor principal, pero totalmente integrada con la ejecución de consultas de SQL Server. Esto significa que puede insertar los datos de cualquier consulta de SQL Server para el tiempo de ejecución externo y consumir o conservar los resultados de vuelta en SQL Server.

Al igual que con cualquier extensión del lenguaje de programación, el procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) es la interfaz para ejecutar código de Java compilado previamente.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>Requisitos previos

Se requiere una instancia de la versión preliminar de SQL Server 2019. Las versiones anteriores no tienen integración con Java.

Es compatible con Java 8. El requisito mínimo es de Java Runtime Environment (JRE), pero es útil si necesita el compilador de Java o los paquetes de desarrollo JDK. Dado el JDK es totalmente inclusivo, si instala el JDK y JRE no es necesario.

Puede usar su distribución preferida de Java 8. A continuación se muestran dos distribuciones sugeridas:

| Distribución | Versión de Java | Sistemas operativos | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows y Linux | Sí | Sí |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows y Linux | Sí | No |

En Linux, el **mssql-server-extensibilidad-java** paquete instala automáticamente el JRE 8 si ya no está instalado. Scripts de instalación también agregar la ruta de acceso JVM a una variable de entorno llamada JAVA_HOME.

En Windows, se recomienda instalar el JDK en el valor predeterminado `/Program Files/` carpeta si es posible. En caso contrario, se requiere configuración adicional para conceder permisos a los archivos ejecutables. Para obtener más información, consulte el [conceder permisos (Windows)](#perms-nonwindows) sección en este documento.

> [!Note]
> Dado que Java es compatible con versiones anteriores, las versiones anteriores podrían funcionar, pero la versión compatible y probada para esta versión CTP anterior es Java 8. 

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Instalación en Linux

Puede instalar el [bases de datos motor y la extensión de Java juntos](../../linux/sql-server-linux-setup-machine-learning.md#install-all), o agregar compatibilidad con Java en una instancia existente. Los ejemplos siguientes agregue la extensión de Java a una instalación existente.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# SUSE install commands
sudo zypper install mssql-server-extensibility-java
```

Al instalar **mssql-server-extensibilidad-java**, el paquete instala automáticamente el JRE 8 si ya no está instalado. También agregará la ruta de acceso JVM para una variable de entorno llamada JAVA_HOME.

Después de completar la instalación, el siguiente paso es [configurar ejecución de scripts externos](#configure-script-execution).

> [!Note]
> En un dispositivo conectado a internet, las dependencias del paquete se descargó e instaló como parte de la instalación del paquete principal. Para obtener más detalles, el programa de instalación sin conexión, consulte [instalar SQL Server Machine Learning en Linux](../../linux/sql-server-linux-setup-machine-learning.md).

### <a name="grant-permissions-on-linux"></a>Conceder permisos en Linux

Para proporcionar permisos para ejecutar las clases de Java a SQL Server, deberá establecer los permisos.

Para conceder acceso y ejecución para jar de archivos o archivos de clase, ejecute el siguiente **chmod** comando en cada archivo de clase o el archivo jar. Se recomienda colocar los archivos de clase en un archivo jar cuando se trabaja con SQL Server. Para obtener ayuda acerca de la creación de un archivo jar, consulte [cómo crear un archivo jar](#create-jar).

```cmd
chmod ug+rx <MyJarFile.jar>
```
También deberá conceder permisos de mssql_satellite en el archivo del directorio o archivo jar para lectura y ejecución.

* Si se llama a archivos de clase de SQL Server, mssql_satellite necesita leer/ejecutará los permisos en *cada* directorio en la jerarquía de carpetas, desde la raíz hasta el elemento primario directo.

* Si se llama a un archivo jar desde SQL Server, es suficiente para ejecutar el comando en el propio archivo jar.

```cmd
chown mssql_satellite:mssql_satellite <directory>
```

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>Instalar en Windows

1. Asegúrese de que se instala una versión compatible de Java. Para obtener más información, consulte el [requisitos previos](#prerequisites).

2. [Ejecute el programa de instalación](../install/sql-machine-learning-services-windows-install.md) para instalar SQL Server 2019.

3. Cuando llegue a la selección de características, elija **Machine Learning Services (en bases de datos)**. 

   Aunque la integración de Java no se incluye con bibliotecas de aprendizaje automático, esta es la opción de instalación que proporciona el marco de extensibilidad. Si lo desea puede omitir R y Python.

4. Finalizar al Asistente para instalación y, a continuación, continúe con las siguientes dos tareas.

### <a name="add-the-javahome-variable"></a>Agregue la variable JAVA_HOME

JAVA_HOME es una variable de entorno que especifica la ubicación del intérprete de Java. En este paso, creará una variable de entorno del sistema para él en Windows.

1. Busque y copie la ruta de acceso JDK y JRE (por ejemplo, `C:\Program Files\Java\jdk1.8.0_201`).

    Dependiendo de su distribución preferida de Java, la ubicación del JDK o JRE puede ser diferente de la ruta de acceso de ejemplo anterior.

2. En el Panel de Control, abra **sistema y seguridad**, abra **sistema**y haga clic en **propiedades avanzadas de sistema**.

3. Haga clic en **Variables de entorno**.

4. Crear una nueva variable del sistema para `JAVA_HOME` con el valor de la ruta de acceso JDK y JRE (que se encuentra en el paso 1).

5. Reiniciar [Launchpad](../concepts/extensibility-framework.md#launchpad).

    1. Abra el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).

    2. En servicios de SQL Server, haga clic en Launchpad de SQL Server y seleccione **reiniciar**.

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>Conceder acceso a la carpeta JDK no predeterminada (solo Windows)

Puede omitir este paso si ha instalado el JDK y JRE en la carpeta predeterminada. 

Una instalación de la carpeta no predeterminada, ejecute el **icacls** comandos desde un *con privilegios elevados* línea para conceder acceso a la **SQLRUsergroup** y cuentas de servicio de SQL Server (en  **ALL_APPLICATION_PACKAGES**) para acceder a la JVM y el classpath de Java. Los comandos realizará de forma recursiva conceder acceso a todos los archivos y carpetas bajo la ruta de acceso del directorio dado.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup permisos

Para una instancia con nombre, anexe el nombre de instancia al SQLRUsergroup (por ejemplo, `SQLRUsergroupINSTANCENAME`).

```cmd
icacls "<PATH TO CLASS or JAR FILES>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

#### <a name="appcontainer-permissions"></a>Permisos de AppContainer

```cmd
icacls "PATH to JDK/JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>Configurar la ejecución del script

En este momento, está casi listo para ejecutar código de Java en Linux o Windows. Como último paso, cambiar a SQL Server Management Studio u otra herramienta que se ejecuta el script de Transact-SQL para habilitar la ejecución de scripts externos.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>Comprobar la instalación

Para confirmar la instalación está operativa, crear y ejecutar un [aplicación de ejemplo](java-first-sample.md) utilizando el JDK que se ha instalado, la colocación de los archivos en la ruta de clase que configuró anteriormente.

## <a name="differences-in-ctp-23"></a>Diferencias en CTP 2.3

Si ya está familiarizado con Machine Learning Services, ha cambiado el modelo de autorización y aislamiento para las extensiones en esta versión. Para obtener más información, consulte [diferencias en una instalación de SQL Server Machine Learning de 2019 Services](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-23"></a>Limitaciones en CTP 2.3

* No puede superar el número de valores de los búferes de entrada y salidos `MAX_INT (2^31-1)` , ya que es el número máximo de elementos que se pueden asignar en una matriz en Java.

* Parámetros de salida [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) no se admiten en esta versión.

* Streaming con el parámetro sp_execute_external_script @r_rowsPerRead no se admite en esta versión de CTP.

* Creación de particiones mediante el parámetro sp_execute_external_script @input_data_1_partition_by_columns no se admite en esta versión de CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Cómo crear un archivo jar desde archivos de clase

Navegue hasta la carpeta que contiene el archivo de clase y ejecute este comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Asegúrese de que la ruta de acceso **jar.exe** forma parte de la variable de ruta de acceso del sistema. Como alternativa, especifique la ruta de acceso completa al archivo jar que se encuentra en/bin en la carpeta JDK: `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)