---
title: 'Inicio rápido: Conectarse y consultar una base de datos SQL de Azure'
titleSuffix: Azure Data Studio
description: En este tutorial rápido se muestra cómo usar Azure Data Studio para conectarse a una base de datos SQL y ejecutar una consulta
ms.custom: seodec18
ms.date: 12/21/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: d368f38589530f27db98c3c61b9cec4610818ae4
ms.sourcegitcommit: a11e733bd417905150567dfebc46a137df85a2fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991818"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Inicio rápido: Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse y consultar la base de datos SQL de Azure

En este tutorial, usará [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a un servidor de base de datos de SQL Azure. A continuación, se va a ejecutar las instrucciones de Transact-SQL (T-SQL) para crear y consultar la base de datos TutorialDB que se usa en otros [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

## <a name="prerequisites"></a>Requisitos previos

Para completar el estudio de este tutorial rápido, necesitará [!INCLUDE[name-sos](../includes/name-sos-short.md)]y un servidor de base de datos de SQL Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

Si no tiene un servidor SQL Azure, complete uno de los siguientes inicios rápidos de Azure SQL Database. Recuerde el nombre completo del servidor e inicie sesión en las credenciales para los pasos posteriores:

- [Crear base de datos: Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Creación de base de datos: CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Creación de base de datos: PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectarse al servidor de base de datos de SQL Azure

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión al servidor de Azure SQL Database.

1. La primera vez que ejecute [!INCLUDE[name-sos](../includes/name-sos-short.md)] el **conexión** debe abrir la página. Si no ve el **conexión** página, seleccione **Agregar conexión**, o el **nueva conexión** icono en el **servidores** sidebar:
   
   ![Nuevo icono de conexión](media/quickstart-sql-database/new-connection-icon.png)

2. En este artículo usa inicio de sesión de SQL, pero también admite la autenticación de Windows. Rellene los campos siguientes con el nombre del servidor, el nombre de usuario y la contraseña para el servidor SQL de Azure:

   | Parámetro       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | Algo como: **nombreDeServidor.baseDeDatos.Windows.NET**. |
   | **Autenticación** | Inicio de sesión de SQL| Este tutorial usa autenticación de SQL. |
   | **Nombre de usuario.** | El nombre de usuario de cuenta de administrador de servidor | El nombre de usuario de la cuenta usada para crear el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | La contraseña de cuenta de administrador de servidor | La contraseña de la cuenta usada para crear el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Seleccione **Sí** si no desea escribir la contraseña cada vez. |
   | **Nombre de la base de datos** | *Deje en blanco* | Se conecta sólo a este servidor. |
   | **Grupo de servidores** | Seleccione <Default> | Puede establecer este campo a un grupo de servidores específicos que creó. | 

   ![Nuevo icono de conexión](media/quickstart-sql-database/new-connection-screen.png)  

3. Seleccione **Conectar**.

4. Si el servidor no tiene una regla de firewall que permita Studio de datos de Azure para conectarse, el **crear nueva regla de firewall** se abrirá el formulario. Complete el formulario para crear una nueva regla de firewall. Para obtener más información, consulte [reglas de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-database/firewall.png)  

Después de conectarse correctamente, el servidor se abre en el **servidores** barra lateral.

## <a name="create-the-tutorial-database"></a>Crear la base de datos tutorial

Las secciones siguientes creación la base de datos TutorialDB que se usa en otros [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

1. Haga doble clic en el servidor SQL de Azure en el **servidores** barra lateral y seleccione **nueva consulta**.

1. Pegue este SQL en el editor de consultas.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. En la barra de herramientas, seleccione **ejecutar**. Las notificaciones aparecen en la **mensajes** panel que muestra el progreso de la consulta.

## <a name="create-a-table"></a>Creación de una tabla

El editor de consultas está conectado a la **maestro** base de datos, pero si desea crear una tabla en la **TutorialDB** base de datos. 

1. Conectarse a la **TutorialDB** base de datos.

   ![Cambio de contexto](media/quickstart-sql-database/change-context2.png)



1. Crear un `Customers` tabla. 

   Reemplace la consulta anterior en el editor de consultas con ésta y seleccione **ejecutar**.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>Insertar filas en la tabla

Reemplace la consulta anterior con ésta y seleccione **ejecutar**.

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>Ver el resultado

Reemplace la consulta anterior con ésta y seleccione **ejecutar**.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

Mostrarán los resultados de consulta:

   ![Seleccione los resultados](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>Limpiar recursos

Los artículos de inicio rápido posteriores se basan en los recursos creados aquí. Si tiene previsto trabajar con estos artículos, asegúrese de no eliminar estos recursos. En caso contrario, en el portal de Azure, elimine los recursos que ya no necesita. Para obtener más información, consulte [limpiar recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Pasos siguientes

Ahora que se ha conectado correctamente a una base de datos SQL de Azure y ejecutar una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).
