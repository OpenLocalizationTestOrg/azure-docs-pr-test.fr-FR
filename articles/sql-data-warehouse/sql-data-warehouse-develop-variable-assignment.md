---
title: "variables aaaAssign dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’affectation de variables Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="3a73a-103">Affecter des variables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3a73a-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="3a73a-104">Variables dans l’entrepôt de données SQL sont définies à l’aide de hello `DECLARE` instruction ou hello `SET` instruction.</span><span class="sxs-lookup"><span data-stu-id="3a73a-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="3a73a-105">Hello qui suit sont parfaitement valides tooset une valeur de variable :</span><span class="sxs-lookup"><span data-stu-id="3a73a-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="3a73a-106">Définition de variables via l’instruction DECLARE</span><span class="sxs-lookup"><span data-stu-id="3a73a-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="3a73a-107">Initialiser des variables avec DECLARE est hello plus souple façons tooset une valeur de variable dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="3a73a-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="3a73a-108">Vous pouvez également utiliser DECLARE tooset plus d’une variable à la fois.</span><span class="sxs-lookup"><span data-stu-id="3a73a-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="3a73a-109">Vous ne pouvez pas utiliser `SELECT` ou `UPDATE` toodo cela :</span><span class="sxs-lookup"><span data-stu-id="3a73a-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="3a73a-110">Vous ne peut pas initialiser et utiliser une variable dans hello même instruction DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3a73a-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="3a73a-111">tooillustrate hello point hello exemple ci-dessous est **pas** autorisé en tant que @p1 est initialisé et utilisé dans hello même instruction DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3a73a-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="3a73a-112">Cela entraîne une erreur.</span><span class="sxs-lookup"><span data-stu-id="3a73a-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="3a73a-113">Définition de valeurs avec l’instruction SET</span><span class="sxs-lookup"><span data-stu-id="3a73a-113">Setting values with SET</span></span>
<span data-ttu-id="3a73a-114">L’instruction SET est très couramment utilisée pour définir une variable unique.</span><span class="sxs-lookup"><span data-stu-id="3a73a-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="3a73a-115">Tous les exemples hello ci-dessous sont définissant une variable avec un jeu de méthodes valides :</span><span class="sxs-lookup"><span data-stu-id="3a73a-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="3a73a-116">Avec l’instruction SET, vous pouvez uniquement définir une variable à la fois.</span><span class="sxs-lookup"><span data-stu-id="3a73a-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="3a73a-117">Toutefois, comme indiqué ci-dessus, les opérateurs composés sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="3a73a-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="3a73a-118">Limitations</span><span class="sxs-lookup"><span data-stu-id="3a73a-118">Limitations</span></span>
<span data-ttu-id="3a73a-119">Vous ne pouvez pas utiliser les instructions SELECT et UPDATE pour attribuer des variables.</span><span class="sxs-lookup"><span data-stu-id="3a73a-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a73a-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a73a-120">Next steps</span></span>
<span data-ttu-id="3a73a-121">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="3a73a-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
