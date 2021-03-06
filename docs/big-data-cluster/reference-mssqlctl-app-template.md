---
title: referencia de plantillas de aplicación mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artículo de referencia para los comandos de plantilla de aplicación mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 16583ba970bfc13312864ea2e9d2571b04c20fcb
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527228"
---
# <a name="mssqlctl-app-template"></a>plantilla de aplicación mssqlctl

El siguiente artículo proporciona la referencia para la **plantilla de aplicación** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [list](#list) | Obtener plantillas compatibles. |
| [pull](#pull) | Descargue plantillas compatibles. |

## <a id="list"></a> lista de plantillas de aplicación mssqlctl

Obtener plantillas compatibles.

```
mssqlctl app template list
   --url
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--url -u** | Especifique una ubicación de repositorio de plantillas diferentes. Valor predeterminado: https://github.com/Microsoft/sql-server-samples.git. |

### <a name="examples"></a>Ejemplos

Capturar todas las plantillas en la ubicación predeterminada del repositorio de plantillas.

```
mssqlctl app template list
```

Capturar todas las plantillas en una ubicación de otro repositorio.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

## <a id="pull"></a> incorporación de cambios de plantilla de aplicación de mssqlctl

Descargue plantillas compatibles.

```
mssqlctl app template pull
   --destination
   --name
   --url
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--destino -d** | Dónde colocar la plantilla de aplicación esqueleto.  Valor predeterminado:. / plantillas. |
| **--name -n** | Nombre de la plantilla. Para obtener una lista completa desactivar los nombres de plantilla admitidos, ejecute `mssqlctl app template list`. |
| **--url -u** | Especifique una ubicación de repositorio de plantillas diferentes. Predeterminado:
https://github.com/Microsoft/sql-server-samples.git  |

### <a name="examples"></a>Ejemplos

Descargar todas las plantillas en la ubicación predeterminada del repositorio de plantillas.

```
mssqlctl app template pull
```

Descargar todas las plantillas en una ubicación de otro repositorio.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

Descargar plantilla individual por nombre.

```
mssqlctl app template pull --name ssis
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).