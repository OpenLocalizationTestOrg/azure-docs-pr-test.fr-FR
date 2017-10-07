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
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="66ade-103">Code SQL dynamique dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="66ade-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="66ade-104">Lors du développement de code d’application pour SQL Data Warehouse, vous pouvez peut-être toouse sql dynamique toohelp offrent des solutions flexibles, génériques et modulaires.</span><span class="sxs-lookup"><span data-stu-id="66ade-104">When developing application code for SQL Data Warehouse you may need toouse dynamic sql toohelp deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="66ade-105">SQL Data Warehouse ne prend pas en charge les données de type objet blob pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="66ade-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="66ade-106">Cela peut limiter la taille de hello vos chaînes en tant que types d’objets blob incluent les types varchar (max) et nvarchar (max).</span><span class="sxs-lookup"><span data-stu-id="66ade-106">This may limit hello size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="66ade-107">Si vous avez utilisé ces types dans votre code d’application lors de la génération de chaînes de très grande taille, vous devez code hello de toobreak en segments et de l’instruction use hello EXEC à la place.</span><span class="sxs-lookup"><span data-stu-id="66ade-107">If you have used these types in your application code when building very large strings, you will need toobreak hello code into chunks and use hello EXEC statement instead.</span></span>

<span data-ttu-id="66ade-108">Voici un exemple simple :</span><span class="sxs-lookup"><span data-stu-id="66ade-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="66ade-109">Si la chaîne de hello est courte, vous pouvez utiliser [sp_executesql] [ sp_executesql] normalement.</span><span class="sxs-lookup"><span data-stu-id="66ade-109">If hello string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="66ade-110">Instructions exécutées en tant que code SQL dynamique sera toujours les règles de validation d’objet tooall TSQL.</span><span class="sxs-lookup"><span data-stu-id="66ade-110">Statements executed as dynamic SQL will still be subject tooall TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="66ade-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66ade-111">Next steps</span></span>
<span data-ttu-id="66ade-112">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="66ade-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
