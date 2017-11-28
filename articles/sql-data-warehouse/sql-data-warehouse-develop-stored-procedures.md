---
title: "procédures d’aaaStored dans l’entrepôt de données SQL | Documents Microsoft"
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
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="deb06-103">Procédures stockées dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="deb06-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="deb06-104">Entrepôt de données SQL prend en charge plusieurs fonctionnalités hello Transact-SQL dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="deb06-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="deb06-105">Il n’y a plus important encore montée en charge des fonctionnalités spécifiques que nous voudrons performances de hello tooleverage toomaximize de votre solution.</span><span class="sxs-lookup"><span data-stu-id="deb06-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="deb06-106">Toutefois, l’échelle de toomaintain hello et il les performances de l’entrepôt de données SQL sont également certaines fonctions et fonctionnalités qui ont des différences de comportement et d’autres qui ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="deb06-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="deb06-107">Cet article explique comment tooimplement procédures au sein de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="deb06-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="deb06-108">Présentation des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="deb06-108">Introducing stored procedures</span></span>
<span data-ttu-id="deb06-109">Les procédures stockées sont un excellent moyen d’encapsuler votre code SQL. stocker les données tooyour Fermer dans l’entrepôt de données hello.</span><span class="sxs-lookup"><span data-stu-id="deb06-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="deb06-110">En encapsulant les code hello en unités gérables, procédures stockées aident les développeurs modulariser leurs solutions. faciliter une plus grande réutilisation du code.</span><span class="sxs-lookup"><span data-stu-id="deb06-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="deb06-111">Chaque procédure stockée peut également accepter des paramètres toomake les encore plus flexible.</span><span class="sxs-lookup"><span data-stu-id="deb06-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="deb06-112">SQL Data Warehouse fournit une implémentation simplifiée et rationalisée pour les procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="deb06-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="deb06-113">Hello plus grande différence par rapport tooSQL Server est que hello la procédure stockée n’est pas code précompilé.</span><span class="sxs-lookup"><span data-stu-id="deb06-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="deb06-114">Dans les entrepôts de données nous intéresse généralement moins avec le temps de compilation hello.</span><span class="sxs-lookup"><span data-stu-id="deb06-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="deb06-115">Il est plus important que code de la procédure stockée hello est optimisé pour correctement lorsqu’il fonctionne sur gros volumes de données.</span><span class="sxs-lookup"><span data-stu-id="deb06-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="deb06-116">Hello vise toosave heures, minutes et secondes pas les millisecondes.</span><span class="sxs-lookup"><span data-stu-id="deb06-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="deb06-117">Il est donc plus utile toothink des procédures stockées en tant que conteneurs pour la logique SQL.</span><span class="sxs-lookup"><span data-stu-id="deb06-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="deb06-118">Lors de l’exécution de SQL Data Warehouse votre procédure stockée hello instructions SQL sont analysées, traduites et optimisées au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="deb06-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="deb06-119">Lors de ce processus, chaque instruction est convertie en différentes requêtes distribuées.</span><span class="sxs-lookup"><span data-stu-id="deb06-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="deb06-120">Hello code SQL réellement exécuté sur les données de salutation est requête toohello différents soumise.</span><span class="sxs-lookup"><span data-stu-id="deb06-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="deb06-121">Imbrication des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="deb06-121">Nesting stored procedures</span></span>
<span data-ttu-id="deb06-122">Lorsque des procédures stockées appellent d’autres procédures stockées ou exécuter des sql dynamique interne de hello de procédure stockée ou d’appel de code est dite toobe imbriqués.</span><span class="sxs-lookup"><span data-stu-id="deb06-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="deb06-123">SQL Data Warehouse prend en charge un maximum de 8 niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="deb06-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="deb06-124">Il s’agit de légèrement tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="deb06-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="deb06-125">niveau d’imbrication Hello dans SQL Server est 32.</span><span class="sxs-lookup"><span data-stu-id="deb06-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="deb06-126">appel de procédure stockée de niveau supérieur Hello équivaut toonest niveau 1</span><span class="sxs-lookup"><span data-stu-id="deb06-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="deb06-127">Si hello stockée procédure effectue également un autre EXEC appel puis Cela augmentera too2 au niveau de hello imbrication</span><span class="sxs-lookup"><span data-stu-id="deb06-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="deb06-128">Si la deuxième procédure de hello puis exécute des instructions sql dynamiques puis Cela augmentera too3 au niveau de hello imbrication</span><span class="sxs-lookup"><span data-stu-id="deb06-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="deb06-129">Notez que SQL Data Warehouse ne prend pas en charge @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="deb06-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="deb06-130">Vous devez vous-même tookeep un suivi de votre niveau d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="deb06-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="deb06-131">Il est improbable que vous atteignez limite de niveau d’imbrication hello 8. Toutefois, si vous vous aura besoin professionnel toore votre code et de « aplatir » afin qu’il tienne dans cette limite.</span><span class="sxs-lookup"><span data-stu-id="deb06-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="deb06-132">INSERT... EXECUTE</span><span class="sxs-lookup"><span data-stu-id="deb06-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="deb06-133">SQL Data Warehouse n’autorise pas jeu de résultats tooconsume hello d’une procédure stockée avec une instruction INSERT.</span><span class="sxs-lookup"><span data-stu-id="deb06-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="deb06-134">Toutefois, vous pouvez utiliser une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="deb06-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="deb06-135">Reportez-vous toohello l’article suivant [tables temporaires] pour obtenir un exemple sur la façon de toodo cela.</span><span class="sxs-lookup"><span data-stu-id="deb06-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="deb06-136">Limites</span><span class="sxs-lookup"><span data-stu-id="deb06-136">Limitations</span></span>
<span data-ttu-id="deb06-137">Certains aspects des procédures stockées Transact-SQL ne sont pas implémentés dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deb06-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="deb06-138">Les voici :</span><span class="sxs-lookup"><span data-stu-id="deb06-138">They are:</span></span>

* <span data-ttu-id="deb06-139">Procédures stockées temporaires</span><span class="sxs-lookup"><span data-stu-id="deb06-139">temporary stored procedures</span></span>
* <span data-ttu-id="deb06-140">Procédures stockées numérotées</span><span class="sxs-lookup"><span data-stu-id="deb06-140">numbered stored procedures</span></span>
* <span data-ttu-id="deb06-141">Procédures stockées étendues</span><span class="sxs-lookup"><span data-stu-id="deb06-141">extended stored procedures</span></span>
* <span data-ttu-id="deb06-142">Procédures stockées CLR</span><span class="sxs-lookup"><span data-stu-id="deb06-142">CLR stored procedures</span></span>
* <span data-ttu-id="deb06-143">Option de chiffrement</span><span class="sxs-lookup"><span data-stu-id="deb06-143">encryption option</span></span>
* <span data-ttu-id="deb06-144">Option de réplication</span><span class="sxs-lookup"><span data-stu-id="deb06-144">replication option</span></span>
* <span data-ttu-id="deb06-145">Paramètres table</span><span class="sxs-lookup"><span data-stu-id="deb06-145">table-valued parameters</span></span>
* <span data-ttu-id="deb06-146">Paramètres en lecture seule</span><span class="sxs-lookup"><span data-stu-id="deb06-146">read-only parameters</span></span>
* <span data-ttu-id="deb06-147">Paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="deb06-147">default parameters</span></span>
* <span data-ttu-id="deb06-148">Contextes d’exécution</span><span class="sxs-lookup"><span data-stu-id="deb06-148">execution contexts</span></span>
* <span data-ttu-id="deb06-149">Instruction RETURN</span><span class="sxs-lookup"><span data-stu-id="deb06-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="deb06-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="deb06-150">Next steps</span></span>
<span data-ttu-id="deb06-151">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="deb06-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[tables temporaires]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
