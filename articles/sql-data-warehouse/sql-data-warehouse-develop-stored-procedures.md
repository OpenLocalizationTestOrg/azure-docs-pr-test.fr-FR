---
title: "Procédures stockées dans SQL Data Warehouse | Microsoft Docs"
description: "Conseils relatifs à l’implémentation de procédures stockées dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="d8390-103">Procédures stockées dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d8390-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="d8390-104">SQL Data Warehouse prend en charge plusieurs fonctionnalités Transact-SQL proposées par SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d8390-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="d8390-105">Plus important encore, il existe différentes fonctions, spécifiques à la montée en charge, que nous voulons exploiter pour optimiser les performances de notre solution.</span><span class="sxs-lookup"><span data-stu-id="d8390-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="d8390-106">Toutefois, pour assurer la mise à l’échelle et les performances de SQL Data Warehouse, il existe divers mécanismes et fonctions dont le comportement présente des différences, ainsi que d’autres qui ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d8390-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="d8390-107">Cet article explique comment implémenter des procédures stockées dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8390-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="d8390-108">Présentation des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="d8390-108">Introducing stored procedures</span></span>
<span data-ttu-id="d8390-109">Une procédure stockée est un excellent moyen d’encapsuler votre code SQL, en le stockant à un emplacement proche de vos données au sein de l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="d8390-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="d8390-110">En encapsulant le code sous la forme d’unités pouvant être facilement gérées, les procédures stockées aident les développeurs à modulariser leurs solutions, afin d’optimiser la réutilisation du code.</span><span class="sxs-lookup"><span data-stu-id="d8390-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="d8390-111">Chaque procédure stockée peut également accepter des paramètres, ce qui les rend encore plus flexibles.</span><span class="sxs-lookup"><span data-stu-id="d8390-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="d8390-112">SQL Data Warehouse fournit une implémentation simplifiée et rationalisée pour les procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="d8390-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="d8390-113">La plus grande différence par rapport à SQL Server est le fait que la procédure stockée ne correspond pas à du code précompilé.</span><span class="sxs-lookup"><span data-stu-id="d8390-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="d8390-114">Dans les entrepôts de données, nous nous préoccupons généralement moins souvent de la durée de la compilation.</span><span class="sxs-lookup"><span data-stu-id="d8390-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="d8390-115">Ce qui importe, c’est que le code de la procédure stockée soit optimisé comme il convient lorsqu’il est exécuté sur de grands volumes de données.</span><span class="sxs-lookup"><span data-stu-id="d8390-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="d8390-116">Le gain de temps recherché se compte en heures, en minutes et en secondes, et non en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="d8390-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="d8390-117">De ce fait, il est plus utile de considérer les procédures stockées comme des conteneurs de logique SQL.</span><span class="sxs-lookup"><span data-stu-id="d8390-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="d8390-118">Lorsque SQL Data Warehouse exécute votre procédure stockée, les instructions SQL sont analysées, traduites et optimisées au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d8390-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="d8390-119">Lors de ce processus, chaque instruction est convertie en différentes requêtes distribuées.</span><span class="sxs-lookup"><span data-stu-id="d8390-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="d8390-120">Le code SQL réellement appliqué aux données est différent de la requête envoyée.</span><span class="sxs-lookup"><span data-stu-id="d8390-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="d8390-121">Imbrication des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="d8390-121">Nesting stored procedures</span></span>
<span data-ttu-id="d8390-122">Lorsque les procédures stockées appellent d’autres procédures stockées ou exécutent un code SQL dynamique, la procédure stockée ou procédure d’appel de code centrale est considérée comme « imbriquée ».</span><span class="sxs-lookup"><span data-stu-id="d8390-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="d8390-123">SQL Data Warehouse prend en charge un maximum de 8 niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="d8390-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="d8390-124">En cela, il diffère légèrement de SQL Server,</span><span class="sxs-lookup"><span data-stu-id="d8390-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="d8390-125">qui prend en charge 32 niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="d8390-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="d8390-126">L’appel de procédure stockée de premier niveau correspond au niveau d’imbrication 1.</span><span class="sxs-lookup"><span data-stu-id="d8390-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="d8390-127">Si la procédure stockée effectue également un autre appel EXEC, le niveau d’imbrication passe à 2.</span><span class="sxs-lookup"><span data-stu-id="d8390-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="d8390-128">Si la deuxième procédure exécute du code SQL dynamique, ce niveau monte à 3.</span><span class="sxs-lookup"><span data-stu-id="d8390-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="d8390-129">Notez que SQL Data Warehouse ne prend pas en charge @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="d8390-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="d8390-130">Vous devez conserver vous-même une trace de votre niveau d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="d8390-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="d8390-131">Il est peu probable que vous atteigniez le niveau d’imbrication 8. Cependant, si tel est le cas, vous devez modifier votre code et l’« aplatir », afin qu’il respecte cette limite.</span><span class="sxs-lookup"><span data-stu-id="d8390-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="d8390-132">INSERT... EXECUTE</span><span class="sxs-lookup"><span data-stu-id="d8390-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="d8390-133">SQL Data Warehouse ne vous permet pas d’utiliser le jeu de résultats d’une procédure stockée avec une instruction INSERT.</span><span class="sxs-lookup"><span data-stu-id="d8390-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="d8390-134">Toutefois, vous pouvez utiliser une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="d8390-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="d8390-135">Voir [Tables temporaires dans SQL Data Warehouse] pour consulter des exemples, afin de savoir comment procéder.</span><span class="sxs-lookup"><span data-stu-id="d8390-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="d8390-136">Limitations</span><span class="sxs-lookup"><span data-stu-id="d8390-136">Limitations</span></span>
<span data-ttu-id="d8390-137">Certains aspects des procédures stockées Transact-SQL ne sont pas implémentés dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8390-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="d8390-138">Les voici :</span><span class="sxs-lookup"><span data-stu-id="d8390-138">They are:</span></span>

* <span data-ttu-id="d8390-139">Procédures stockées temporaires</span><span class="sxs-lookup"><span data-stu-id="d8390-139">temporary stored procedures</span></span>
* <span data-ttu-id="d8390-140">Procédures stockées numérotées</span><span class="sxs-lookup"><span data-stu-id="d8390-140">numbered stored procedures</span></span>
* <span data-ttu-id="d8390-141">Procédures stockées étendues</span><span class="sxs-lookup"><span data-stu-id="d8390-141">extended stored procedures</span></span>
* <span data-ttu-id="d8390-142">Procédures stockées CLR</span><span class="sxs-lookup"><span data-stu-id="d8390-142">CLR stored procedures</span></span>
* <span data-ttu-id="d8390-143">Option de chiffrement</span><span class="sxs-lookup"><span data-stu-id="d8390-143">encryption option</span></span>
* <span data-ttu-id="d8390-144">Option de réplication</span><span class="sxs-lookup"><span data-stu-id="d8390-144">replication option</span></span>
* <span data-ttu-id="d8390-145">Paramètres table</span><span class="sxs-lookup"><span data-stu-id="d8390-145">table-valued parameters</span></span>
* <span data-ttu-id="d8390-146">Paramètres en lecture seule</span><span class="sxs-lookup"><span data-stu-id="d8390-146">read-only parameters</span></span>
* <span data-ttu-id="d8390-147">Paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="d8390-147">default parameters</span></span>
* <span data-ttu-id="d8390-148">Contextes d’exécution</span><span class="sxs-lookup"><span data-stu-id="d8390-148">execution contexts</span></span>
* <span data-ttu-id="d8390-149">Instruction RETURN</span><span class="sxs-lookup"><span data-stu-id="d8390-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8390-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8390-150">Next steps</span></span>
<span data-ttu-id="d8390-151">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="d8390-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
<span data-ttu-id="d8390-152">[Tables temporaires dans SQL Data Warehouse]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span><span class="sxs-lookup"><span data-stu-id="d8390-152">[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span></span>
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
