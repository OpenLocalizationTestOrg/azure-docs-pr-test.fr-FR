---
title: aaaDynamic SQL dans SQL Data Warehouse | Documents Microsoft
description: "Conseils relatifs à l’utilisation de code SQL dynamique dans Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>Code SQL dynamique dans SQL Data Warehouse
Lors du développement de code d’application pour SQL Data Warehouse, vous pouvez peut-être toouse sql dynamique toohelp offrent des solutions flexibles, génériques et modulaires. SQL Data Warehouse ne prend pas en charge les données de type objet blob pour l’instant. Cela peut limiter la taille de hello vos chaînes en tant que types d’objets blob incluent les types varchar (max) et nvarchar (max). Si vous avez utilisé ces types dans votre code d’application lors de la génération de chaînes de très grande taille, vous devez code hello de toobreak en segments et de l’instruction use hello EXEC à la place.

Voici un exemple simple :

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Si la chaîne de hello est courte, vous pouvez utiliser [sp_executesql] [ sp_executesql] normalement.

> [!NOTE]
> Instructions exécutées en tant que code SQL dynamique sera toujours les règles de validation d’objet tooall TSQL.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
