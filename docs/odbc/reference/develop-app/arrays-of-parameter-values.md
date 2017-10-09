---
title: "Matrices de valores de parámetro | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a0bb497044e9800461b60021fc9a6c8db4e9cca
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="arrays-of-parameter-values"></a>Matrices de valores de parámetro
A menudo resulta útil para las aplicaciones pasar matrices de parámetros. Por ejemplo, con las matrices de parámetros y una con parámetros **insertar** instrucción, una aplicación puede insertar un número de filas a la vez. Hay varias ventajas con respecto al uso de matrices. En primer lugar, se reduce el tráfico de red porque los datos para muchas de las instrucciones se envían en un único paquete (si el origen de datos admite matrices de parámetros de forma nativa). En segundo lugar, algunos orígenes de datos pueden ejecutar instrucciones SQL con matrices más rápido que ejecutar el mismo número de instrucciones independientes de SQL. Por último, cuando los datos se almacenan en una matriz, como suele ser el caso de datos de pantalla, la aplicación puede enlazar todas las filas de una columna en particular con una sola llamada a **SQLBindParameter** y actualizarlos mediante la ejecución de una sola instrucción.  
  
 Por desgracia, no muchos orígenes de datos admiten las matrices de parámetros. Sin embargo, un controlador puede emular las matrices de parámetros mediante la ejecución de una instrucción SQL una vez para cada conjunto de valores de parámetro. Esto puede conducir a los aumentos de velocidad porque el controlador, a continuación, puede preparar la instrucción que va a ejecutar una vez para cada conjunto de parámetros. También podría dar lugar a un código de aplicación más simple.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Utilizar matrices de parámetros](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)