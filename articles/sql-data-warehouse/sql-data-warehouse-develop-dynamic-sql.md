---
title: "Code SQL dynamique dans SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 29228676373aee8dbc7b1b2a7d92ffc978333804
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="ad7e5-103">Code SQL dynamique dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ad7e5-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="ad7e5-104">Quand vous développez le code d’une application pour SQL Data Warehouse, vous pouvez avoir besoin d’utiliser un code SQL dynamique de façon à offrir des solutions flexibles, génériques et modulaires.</span><span class="sxs-lookup"><span data-stu-id="ad7e5-104">When developing application code for SQL Data Warehouse you may need to use dynamic sql to help deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="ad7e5-105">SQL Data Warehouse ne prend pas en charge les données de type objet blob pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="ad7e5-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="ad7e5-106">Cette restriction peut limiter la taille de vos chaînes, car les types d’objet blob comprennent les types varchar(max) et nvarchar(max).</span><span class="sxs-lookup"><span data-stu-id="ad7e5-106">This may limit the size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="ad7e5-107">Si vous avez utilisé ces types dans votre code d’application pendant la création de chaînes de très grande taille, vous devez segmenter le code et utiliser plutôt l’instruction EXEC.</span><span class="sxs-lookup"><span data-stu-id="ad7e5-107">If you have used these types in your application code when building very large strings, you will need to break the code into chunks and use the EXEC statement instead.</span></span>

<span data-ttu-id="ad7e5-108">Voici un exemple simple :</span><span class="sxs-lookup"><span data-stu-id="ad7e5-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="ad7e5-109">Si la chaîne est courte, vous pouvez utiliser [sp_executesql][sp_executesql] normalement.</span><span class="sxs-lookup"><span data-stu-id="ad7e5-109">If the string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="ad7e5-110">Les instructions exécutées en tant qu'instructions SQL dynamiques sont toujours soumises à l'ensemble des règles de validation TSQL.</span><span class="sxs-lookup"><span data-stu-id="ad7e5-110">Statements executed as dynamic SQL will still be subject to all TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ad7e5-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad7e5-111">Next steps</span></span>
<span data-ttu-id="ad7e5-112">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="ad7e5-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
