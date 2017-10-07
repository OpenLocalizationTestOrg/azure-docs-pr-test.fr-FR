---
title: effectue une boucle aaaLeverage T-SQL dans Azure SQL Data Warehouse | Documents Microsoft
description: "Conseils relatifs à l’utilisation de boucles Transact-SQL et au remplacement de curseurs dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="1038f-103">Boucles dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1038f-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="1038f-104">Entrepôt de données SQL prend en charge hello [pendant][tandis que] une boucle pour l’exécution répétée de blocs d’instructions.</span><span class="sxs-lookup"><span data-stu-id="1038f-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="1038f-105">Il en sera de tant que hello spécifiée conditions sont remplies ou jusqu'à ce que les code hello termine spécifiquement boucle hello à l’aide de hello `BREAK` (mot clé).</span><span class="sxs-lookup"><span data-stu-id="1038f-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="1038f-106">Les boucles sont particulièrement utiles pour remplacer des curseurs définis dans le code SQL.</span><span class="sxs-lookup"><span data-stu-id="1038f-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="1038f-107">Heureusement, presque tous les curseurs qui sont écrits dans le code SQL sont Hello rapide, en lecture uniquement diverses.</span><span class="sxs-lookup"><span data-stu-id="1038f-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="1038f-108">Par conséquent [tandis que] boucles sont une alternative intéressante si vous vous trouvez ayant tooreplace une.</span><span class="sxs-lookup"><span data-stu-id="1038f-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="1038f-109">Valorisation de boucles et remplacement de curseurs dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1038f-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="1038f-110">Toutefois, avant d’examiner en tête tout d’abord vous devez vous poser hello suivant la question : « ce curseur peut être réécrit toouse des opérations basées sur ? ».</span><span class="sxs-lookup"><span data-stu-id="1038f-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="1038f-111">Dans de nombreux cas, les réponses hello seront Oui et sont souvent hello meilleure approche.</span><span class="sxs-lookup"><span data-stu-id="1038f-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="1038f-112">Une opération basée sur un jeu s’exécute généralement beaucoup plus rapidement qu’une méthode itérative de type ligne par ligne.</span><span class="sxs-lookup"><span data-stu-id="1038f-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="1038f-113">Les curseurs à avance rapide et en lecture seule peuvent facilement être remplacés par des constructions en boucle.</span><span class="sxs-lookup"><span data-stu-id="1038f-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="1038f-114">Voici un exemple simple.</span><span class="sxs-lookup"><span data-stu-id="1038f-114">Below is a simple example.</span></span> <span data-ttu-id="1038f-115">Cet exemple de code met à jour les statistiques de hello pour chaque table dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="1038f-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="1038f-116">En effectuant une itération sur les tables de hello de boucle de hello nous est en mesure de tooexecute chaque commande dans la séquence.</span><span class="sxs-lookup"><span data-stu-id="1038f-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="1038f-117">Commencez par créer une table temporaire contenant une ligne unique numéro utilisé tooidentify hello des instructions individuelles :</span><span class="sxs-lookup"><span data-stu-id="1038f-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="1038f-118">En second lieu, initialiser boucle de hello hello variables tooperform requis :</span><span class="sxs-lookup"><span data-stu-id="1038f-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="1038f-119">Ensuite, effectuez une boucle avec les instructions, en les exécutant l’une après l’autre :</span><span class="sxs-lookup"><span data-stu-id="1038f-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="1038f-120">Enfin drop table temporaire de hello créée dans la première étape de hello</span><span class="sxs-lookup"><span data-stu-id="1038f-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="1038f-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1038f-121">Next steps</span></span>
<span data-ttu-id="1038f-122">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble sur le développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="1038f-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[tandis que]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
