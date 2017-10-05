---
title: "Affecter des variables dans SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="73e5d-103">Affecter des variables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="73e5d-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="73e5d-104">Dans SQL Data Warehouse, les variables sont définies au moyen de l’instruction `DECLARE` ou `SET`.</span><span class="sxs-lookup"><span data-stu-id="73e5d-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="73e5d-105">Pour définir une valeur de variable, il existe différentes méthodes, parfaitement valables :</span><span class="sxs-lookup"><span data-stu-id="73e5d-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="73e5d-106">Définition de variables via l’instruction DECLARE</span><span class="sxs-lookup"><span data-stu-id="73e5d-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="73e5d-107">Dans SQL Data Warehouse, l’initialisation de variables avec l’instruction DECLARE constitue l’une des méthodes les plus flexibles pour définir une valeur de variable.</span><span class="sxs-lookup"><span data-stu-id="73e5d-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="73e5d-108">De plus, vous pouvez utiliser cette instruction pour définir plusieurs variables à la fois.</span><span class="sxs-lookup"><span data-stu-id="73e5d-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="73e5d-109">En effet, vous ne pouvez pas utiliser les éléments `SELECT` et `UPDATE` pour exécuter ceci :</span><span class="sxs-lookup"><span data-stu-id="73e5d-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="73e5d-110">De plus, il n’est pas possible d’initialiser et d’utiliser une variable au sein de la même instruction DECLARE.</span><span class="sxs-lookup"><span data-stu-id="73e5d-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="73e5d-111">Illustrons notre propos : la commande de l’exemple ci-dessous n’est **pas** autorisée, car l’élément @p1 est initialisé, mais également utilisé dans la même instruction DECLARE.</span><span class="sxs-lookup"><span data-stu-id="73e5d-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="73e5d-112">Cela entraîne une erreur.</span><span class="sxs-lookup"><span data-stu-id="73e5d-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="73e5d-113">Définition de valeurs avec l’instruction SET</span><span class="sxs-lookup"><span data-stu-id="73e5d-113">Setting values with SET</span></span>
<span data-ttu-id="73e5d-114">L’instruction SET est très couramment utilisée pour définir une variable unique.</span><span class="sxs-lookup"><span data-stu-id="73e5d-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="73e5d-115">Tous les exemples ci-dessous illustrent des modes de définition d’une variable avec l’instruction SET, qui sont parfaitement valables :</span><span class="sxs-lookup"><span data-stu-id="73e5d-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="73e5d-116">Avec l’instruction SET, vous pouvez uniquement définir une variable à la fois.</span><span class="sxs-lookup"><span data-stu-id="73e5d-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="73e5d-117">Toutefois, comme indiqué ci-dessus, les opérateurs composés sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="73e5d-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="73e5d-118">Limitations</span><span class="sxs-lookup"><span data-stu-id="73e5d-118">Limitations</span></span>
<span data-ttu-id="73e5d-119">Vous ne pouvez pas utiliser les instructions SELECT et UPDATE pour attribuer des variables.</span><span class="sxs-lookup"><span data-stu-id="73e5d-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73e5d-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73e5d-120">Next steps</span></span>
<span data-ttu-id="73e5d-121">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="73e5d-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
