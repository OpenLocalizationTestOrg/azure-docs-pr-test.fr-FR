---
title: "toouse aaaHow le traitement par lot des performances de l’application tooimprove base de données SQL Azure"
description: "Hello rubrique constitue une preuve que le traitement par lot de base de données operations considérablement imroves hello vitesse et l’évolutivité de vos applications de base de données SQL Azure. Bien que ces techniques de traitement par lot de travail pour une base de données SQL Server, hello se concentre sur l’article de hello sur Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="b8f95-104">Comment toouse le traitement par lot des performances des applications de base de données SQL tooimprove</span><span class="sxs-lookup"><span data-stu-id="b8f95-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="b8f95-105">Le traitement par lot des opérations tooAzure de la base de données SQL considérablement améliore les performances de hello et de l’évolutivité de vos applications.</span><span class="sxs-lookup"><span data-stu-id="b8f95-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="b8f95-106">Dans l’ordre toounderstand hello d’avantages hello première partie de cet article traite des résultats de test qui comparent des demandes séquentielles et par lot tooa base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="b8f95-107">Hello reste de l’article de hello montre des techniques de hello, scénarios et considérations toohelp toouse de traitement par lot avec succès dans vos applications Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f95-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="b8f95-108">Pourquoi le traitement par lots est-il important pour une base de données SQL ?</span><span class="sxs-lookup"><span data-stu-id="b8f95-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="b8f95-109">Le traitement par lot des appels tooa le service distant est une stratégie connue pour améliorer les performances et l’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="b8f95-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="b8f95-110">Il existe des fixes traitement des coûts des interactions de tooany avec un service distant, telles que la sérialisation, le transfert de réseau et la désérialisation.</span><span class="sxs-lookup"><span data-stu-id="b8f95-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="b8f95-111">L’empaquetage de plusieurs transactions distinctes dans un seul lot contribue à réduire ces coûts.</span><span class="sxs-lookup"><span data-stu-id="b8f95-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="b8f95-112">Dans ce document, nous souhaitons tooexamine différents scénarios et les stratégies de traitement par lot de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="b8f95-113">Bien que ces stratégies soient également importantes pour les applications locales qui utilisent SQL Server, il existe plusieurs raisons pour mettre en surbrillance utilisez hello du traitement par lot pour la base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="b8f95-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="b8f95-114">Est potentiellement plus grande latence du réseau l’accès à la base de données SQL, en particulier si vous accédez à base de données SQL à partir de l’extérieur hello même centre de données Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f95-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="b8f95-115">caractéristiques d’architecture mutualisée Hello signifie que de base de données SQL qui hello l’efficacité des données de hello toohello de corrélation de couche d’accès évolutivité globale de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="b8f95-116">Base de données SQL doit empêcher un locataire/utilisateur de monopoliser détriment de toohello de ressources de base de données d’autres clients.</span><span class="sxs-lookup"><span data-stu-id="b8f95-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="b8f95-117">Dans toousage réponse dépassant les quotas prédéfinis, base de données SQL réduit le débit ou répond avec les exceptions de limitation.</span><span class="sxs-lookup"><span data-stu-id="b8f95-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="b8f95-118">L’efficacité, telles que le traitement par lot, activez vous toodo plus de travail sur la base de données SQL avant d’atteindre ces limites.</span><span class="sxs-lookup"><span data-stu-id="b8f95-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="b8f95-119">Le traitement par lots est également efficace pour les architectures qui utilisent plusieurs bases de données (partitionnement).</span><span class="sxs-lookup"><span data-stu-id="b8f95-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="b8f95-120">Hello efficacité de votre interaction avec chaque unité de base de données est toujours un facteur clé dans votre évolutivité globale.</span><span class="sxs-lookup"><span data-stu-id="b8f95-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="b8f95-121">Un des avantages de hello d’à l’aide de la base de données SQL est que vous n’avez pas les serveurs hello toomanage cette base de données hôte hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="b8f95-122">Toutefois, cette infrastructure managée signifie également que vous avez toothink différemment sur les optimisations de la base de données.</span><span class="sxs-lookup"><span data-stu-id="b8f95-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="b8f95-123">Vous ne pouvez plus chercher infrastructure de matériel ou de réseau la base de données des hello tooimprove.</span><span class="sxs-lookup"><span data-stu-id="b8f95-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="b8f95-124">Ces environnements sont directement contrôlés par Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f95-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="b8f95-125">Hello principal de la zone que vous pouvez contrôler est la façon dont votre application interagit avec la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="b8f95-126">Le traitement par lots constitue l’une de ces optimisations.</span><span class="sxs-lookup"><span data-stu-id="b8f95-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="b8f95-127">Hello première partie du livre de hello examine différentes techniques de traitement par lot pour les applications .NET qui utilisent la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="b8f95-128">Hello deux dernières sections couvrent des instructions de traitement par lot et des scénarios.</span><span class="sxs-lookup"><span data-stu-id="b8f95-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="b8f95-129">Stratégies de traitement par lots</span><span class="sxs-lookup"><span data-stu-id="b8f95-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="b8f95-130">Remarque relative aux résultats de minutage fournis dans cette rubrique</span><span class="sxs-lookup"><span data-stu-id="b8f95-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="b8f95-131">Résultats ne sont pas des points de référence, mais sont destinées à tooshow **performances relatives**.</span><span class="sxs-lookup"><span data-stu-id="b8f95-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="b8f95-132">Les minutages reposent sur une moyenne calculée à partir d’au moins 10 séries de tests.</span><span class="sxs-lookup"><span data-stu-id="b8f95-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="b8f95-133">Les opérations consistent en des insertions dans une table vide.</span><span class="sxs-lookup"><span data-stu-id="b8f95-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="b8f95-134">Ces tests ont été mesurés pre-V12, et ils ne correspondent pas nécessairement toothroughput que vous pouvez rencontrer dans une base de données V12 à l’aide de nouveau hello [niveaux de service](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="b8f95-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="b8f95-135">avantage relatif de Hello Hello technique de traitement par lot doit être similaire.</span><span class="sxs-lookup"><span data-stu-id="b8f95-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="b8f95-136">Transactions</span><span class="sxs-lookup"><span data-stu-id="b8f95-136">Transactions</span></span>
<span data-ttu-id="b8f95-137">Il semble étrange toobegin une revue du traitement par lots en traitant des transactions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="b8f95-138">Mais utilisez hello des transactions côté client a un effet de traitement par lot côté serveur subtil qui améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="b8f95-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="b8f95-139">Et les transactions peuvent être ajoutées avec seulement quelques lignes de code, afin de fournir des performances des opérations séquentielles tooimprove rapidement.</span><span class="sxs-lookup"><span data-stu-id="b8f95-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="b8f95-140">Envisagez de hello suivant de code c# qui contient une séquence d’insertion et mettre à jour des opérations sur une table simple.</span><span class="sxs-lookup"><span data-stu-id="b8f95-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="b8f95-141">Hello suivant de manière séquentielle code ADO.NET effectue ces opérations.</span><span class="sxs-lookup"><span data-stu-id="b8f95-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="b8f95-142">Hello meilleures toooptimize de façon à ce code est tooimplement une forme de traitement côté client de ces appels.</span><span class="sxs-lookup"><span data-stu-id="b8f95-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="b8f95-143">Mais il existe une méthode simple tooincrease hello des performances de ce code en encapsulant simplement la séquence hello d’appels dans une transaction.</span><span class="sxs-lookup"><span data-stu-id="b8f95-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="b8f95-144">Voici hello même code qui utilise une transaction.</span><span class="sxs-lookup"><span data-stu-id="b8f95-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="b8f95-145">Les transactions sont en fait utilisées dans ces deux exemples.</span><span class="sxs-lookup"><span data-stu-id="b8f95-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="b8f95-146">Dans le premier exemple de hello, chaque appel individuel est une transaction implicite.</span><span class="sxs-lookup"><span data-stu-id="b8f95-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="b8f95-147">Dans le deuxième exemple de hello, une transaction explicite encapsule tous les appels hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="b8f95-148">Par documentation hello pour hello [journal des transactions à écriture anticipée](https://msdn.microsoft.com/library/ms186259.aspx), les enregistrements de journal sont vidées toohello disque lors de la validation de la transaction hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="b8f95-149">Par conséquent, en incluant davantage d’appels dans une transaction, hello journal des transactions toohello écriture peut retarder jusqu'à hello transaction est validée.</span><span class="sxs-lookup"><span data-stu-id="b8f95-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="b8f95-150">En effet, vous activez le traitement par lot pour le journal des transactions du serveur toohello hello écritures.</span><span class="sxs-lookup"><span data-stu-id="b8f95-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="b8f95-151">Hello tableau suivant montre des résultats des tests ad hoc.</span><span class="sxs-lookup"><span data-stu-id="b8f95-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="b8f95-152">effectuer les tests de Hello hello que même séquentiel insère avec et sans transactions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="b8f95-153">Pour plus de perspective, hello premier ensemble de tests a été exécuté à distance à partir d’une base de données portable toohello dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f95-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="b8f95-154">Hello deuxième ensemble de tests a été exécuté à partir d’un service cloud et de la base de données qui résidaient dans hello même centre de données Microsoft Azure (ouest des États-Unis).</span><span class="sxs-lookup"><span data-stu-id="b8f95-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="b8f95-155">Hello tableau suivant affiche hello durée en millisecondes des insertions séquentielles avec et sans transactions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="b8f95-156">**Local tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="b8f95-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="b8f95-157">Opérations</span><span class="sxs-lookup"><span data-stu-id="b8f95-157">Operations</span></span> | <span data-ttu-id="b8f95-158">Sans transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-158">No Transaction (ms)</span></span> | <span data-ttu-id="b8f95-159">Avec transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f95-160">1</span><span class="sxs-lookup"><span data-stu-id="b8f95-160">1</span></span> |<span data-ttu-id="b8f95-161">130</span><span class="sxs-lookup"><span data-stu-id="b8f95-161">130</span></span> |<span data-ttu-id="b8f95-162">402</span><span class="sxs-lookup"><span data-stu-id="b8f95-162">402</span></span> |
| <span data-ttu-id="b8f95-163">10</span><span class="sxs-lookup"><span data-stu-id="b8f95-163">10</span></span> |<span data-ttu-id="b8f95-164">1 208</span><span class="sxs-lookup"><span data-stu-id="b8f95-164">1208</span></span> |<span data-ttu-id="b8f95-165">1 226</span><span class="sxs-lookup"><span data-stu-id="b8f95-165">1226</span></span> |
| <span data-ttu-id="b8f95-166">100</span><span class="sxs-lookup"><span data-stu-id="b8f95-166">100</span></span> |<span data-ttu-id="b8f95-167">12 662</span><span class="sxs-lookup"><span data-stu-id="b8f95-167">12662</span></span> |<span data-ttu-id="b8f95-168">10 395</span><span class="sxs-lookup"><span data-stu-id="b8f95-168">10395</span></span> |
| <span data-ttu-id="b8f95-169">1 000</span><span class="sxs-lookup"><span data-stu-id="b8f95-169">1000</span></span> |<span data-ttu-id="b8f95-170">128 852</span><span class="sxs-lookup"><span data-stu-id="b8f95-170">128852</span></span> |<span data-ttu-id="b8f95-171">102 917</span><span class="sxs-lookup"><span data-stu-id="b8f95-171">102917</span></span> |

<span data-ttu-id="b8f95-172">**Azure tooAzure (même centre de données)**:</span><span class="sxs-lookup"><span data-stu-id="b8f95-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="b8f95-173">Opérations</span><span class="sxs-lookup"><span data-stu-id="b8f95-173">Operations</span></span> | <span data-ttu-id="b8f95-174">Sans transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-174">No Transaction (ms)</span></span> | <span data-ttu-id="b8f95-175">Avec transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f95-176">1</span><span class="sxs-lookup"><span data-stu-id="b8f95-176">1</span></span> |<span data-ttu-id="b8f95-177">21</span><span class="sxs-lookup"><span data-stu-id="b8f95-177">21</span></span> |<span data-ttu-id="b8f95-178">26</span><span class="sxs-lookup"><span data-stu-id="b8f95-178">26</span></span> |
| <span data-ttu-id="b8f95-179">10</span><span class="sxs-lookup"><span data-stu-id="b8f95-179">10</span></span> |<span data-ttu-id="b8f95-180">220</span><span class="sxs-lookup"><span data-stu-id="b8f95-180">220</span></span> |<span data-ttu-id="b8f95-181">56</span><span class="sxs-lookup"><span data-stu-id="b8f95-181">56</span></span> |
| <span data-ttu-id="b8f95-182">100</span><span class="sxs-lookup"><span data-stu-id="b8f95-182">100</span></span> |<span data-ttu-id="b8f95-183">2 145</span><span class="sxs-lookup"><span data-stu-id="b8f95-183">2145</span></span> |<span data-ttu-id="b8f95-184">341</span><span class="sxs-lookup"><span data-stu-id="b8f95-184">341</span></span> |
| <span data-ttu-id="b8f95-185">1 000</span><span class="sxs-lookup"><span data-stu-id="b8f95-185">1000</span></span> |<span data-ttu-id="b8f95-186">21 479</span><span class="sxs-lookup"><span data-stu-id="b8f95-186">21479</span></span> |<span data-ttu-id="b8f95-187">2 756</span><span class="sxs-lookup"><span data-stu-id="b8f95-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="b8f95-188">Les résultats ne représentent pas des valeurs de référence.</span><span class="sxs-lookup"><span data-stu-id="b8f95-188">Results are not benchmarks.</span></span> <span data-ttu-id="b8f95-189">Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="b8f95-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="b8f95-190">Selon les résultats des tests précédents hello, une seule opération d’habillage dans une transaction réellement réduit les performances.</span><span class="sxs-lookup"><span data-stu-id="b8f95-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="b8f95-191">Mais lorsque vous augmentez le nombre de hello d’opérations dans une transaction unique, amélioration des performances hello devient plus marquée.</span><span class="sxs-lookup"><span data-stu-id="b8f95-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="b8f95-192">différence de performances Hello est également plus apparente lorsque toutes les opérations se produisent dans le centre de données de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="b8f95-193">Hello de l’utilisation de la base de données SQL à partir du centre de données de Microsoft Azure hello en dehors de la latence accrue masque en partie le gain de performances hello de l’utilisation de transactions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="b8f95-194">Bien que l’utilisation de hello des transactions peut accroître les performances, continuer trop[observer les meilleures pratiques pour les connexions et transactions](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8f95-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="b8f95-195">Conserver la transaction hello autant que la connexion de base de données hello possible et fermer après la fin du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="b8f95-196">Bonjour à l’aide de la déclaration dans l’exemple précédent de hello garantit que hello est déconnecté lors de la fin du bloc de code suivant hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="b8f95-197">Hello précédente montre que vous pouvez ajouter un code ADO.NET tooany transaction locale avec deux lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="b8f95-198">Les transactions offrent un moyen rapide de performances de hello tooimprove du code qui effectue séquentiel insérer, mettre à jour et les opérations de suppression.</span><span class="sxs-lookup"><span data-stu-id="b8f95-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="b8f95-199">Toutefois, pour des performances accrues de hello, pensez à hello code supplémentaire tootake parti du traitement par lots côté client, telles que des paramètres table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="b8f95-200">Pour plus d’informations sur les transactions dans ADO.NET, consultez [Transactions locales dans ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="b8f95-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="b8f95-201">Paramètres table</span><span class="sxs-lookup"><span data-stu-id="b8f95-201">Table-valued parameters</span></span>
<span data-ttu-id="b8f95-202">Les paramètres table prennent en charge les types de tables définis par l’utilisateur en tant que paramètres dans les instructions Transact-SQL, en tant que procédures stockées et en tant que fonctions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="b8f95-203">Cette technique de traitement par lot côté client vous permet de toosend plusieurs lignes de données dans le paramètre de table hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="b8f95-204">Paramètres table toouse, d’abord définir un type de table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="b8f95-205">Hello instruction Transact-SQL suivante crée un type de table nommé **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="b8f95-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="b8f95-206">Dans le code, vous créez un **DataTable** avec hello exactement les mêmes noms et types hello du type de table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="b8f95-207">Transférez ce **DataTable** dans un paramètre via une requête texte ou un appel de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b8f95-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="b8f95-208">Hello exemple suivant illustre cette technique :</span><span class="sxs-lookup"><span data-stu-id="b8f95-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="b8f95-209">Dans l’exemple précédent de hello, hello **SqlCommand** objet insère des lignes à partir d’un paramètre table,  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="b8f95-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="b8f95-210">Hello précédemment créé **DataTable** objet reçoit le paramètre toothis avec hello **SqlCommand.Parameters.Add** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8f95-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="b8f95-211">Traitement par lot insertions hello dans un appellent considérablement augmente hello des performances sur les insertions séquentielles.</span><span class="sxs-lookup"><span data-stu-id="b8f95-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="b8f95-212">tooimprove hello exemple précédent, utilisez une procédure stockée au lieu d’une commande de texte.</span><span class="sxs-lookup"><span data-stu-id="b8f95-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="b8f95-213">Hello commande de Transact-SQL suivante crée une procédure stockée qui accepte hello **SimpleTestTableType** paramètre table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="b8f95-214">Puis modifiez hello **SqlCommand** déclaration dans hello précédent code exemple toohello suivant de l’objet.</span><span class="sxs-lookup"><span data-stu-id="b8f95-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="b8f95-215">Dans la plupart des cas, les paramètres table présentent des performances équivalentes ou supérieures à celles des autres techniques de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="b8f95-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="b8f95-216">Les paramètres table sont souvent préférables car ils apportent davantage de flexibilité que les autres options.</span><span class="sxs-lookup"><span data-stu-id="b8f95-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="b8f95-217">Par exemple, les autres techniques, telles que de copie en bloc SQL, n’autorisent insertion hello de nouvelles lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="b8f95-218">Mais avec des paramètres table, vous pouvez utiliser la logique de toodetermine de procédure stockée hello les lignes qui sont mises à jour et d’insertions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="b8f95-219">type de table Hello peut également être modifié toocontain une colonne « Opération » qui indique si hello spécifiée ligne doit être inséré, mis à jour ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="b8f95-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="b8f95-220">Hello tableau suivant indique les résultats des tests ad hoc pour une utilisation hello de paramètres table en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="b8f95-221">Opérations</span><span class="sxs-lookup"><span data-stu-id="b8f95-221">Operations</span></span> | <span data-ttu-id="b8f95-222">On-Premises tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="b8f95-223">Azure (même centre de données)</span><span class="sxs-lookup"><span data-stu-id="b8f95-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f95-224">1</span><span class="sxs-lookup"><span data-stu-id="b8f95-224">1</span></span> |<span data-ttu-id="b8f95-225">124</span><span class="sxs-lookup"><span data-stu-id="b8f95-225">124</span></span> |<span data-ttu-id="b8f95-226">32</span><span class="sxs-lookup"><span data-stu-id="b8f95-226">32</span></span> |
| <span data-ttu-id="b8f95-227">10</span><span class="sxs-lookup"><span data-stu-id="b8f95-227">10</span></span> |<span data-ttu-id="b8f95-228">131</span><span class="sxs-lookup"><span data-stu-id="b8f95-228">131</span></span> |<span data-ttu-id="b8f95-229">25</span><span class="sxs-lookup"><span data-stu-id="b8f95-229">25</span></span> |
| <span data-ttu-id="b8f95-230">100</span><span class="sxs-lookup"><span data-stu-id="b8f95-230">100</span></span> |<span data-ttu-id="b8f95-231">338</span><span class="sxs-lookup"><span data-stu-id="b8f95-231">338</span></span> |<span data-ttu-id="b8f95-232">51</span><span class="sxs-lookup"><span data-stu-id="b8f95-232">51</span></span> |
| <span data-ttu-id="b8f95-233">1 000</span><span class="sxs-lookup"><span data-stu-id="b8f95-233">1000</span></span> |<span data-ttu-id="b8f95-234">2 615</span><span class="sxs-lookup"><span data-stu-id="b8f95-234">2615</span></span> |<span data-ttu-id="b8f95-235">382</span><span class="sxs-lookup"><span data-stu-id="b8f95-235">382</span></span> |
| <span data-ttu-id="b8f95-236">10000</span><span class="sxs-lookup"><span data-stu-id="b8f95-236">10000</span></span> |<span data-ttu-id="b8f95-237">23 830</span><span class="sxs-lookup"><span data-stu-id="b8f95-237">23830</span></span> |<span data-ttu-id="b8f95-238">3 586</span><span class="sxs-lookup"><span data-stu-id="b8f95-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="b8f95-239">Les résultats ne représentent pas des valeurs de référence.</span><span class="sxs-lookup"><span data-stu-id="b8f95-239">Results are not benchmarks.</span></span> <span data-ttu-id="b8f95-240">Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="b8f95-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="b8f95-241">le gain de performances Hello du traitement par lot est visible immédiatement.</span><span class="sxs-lookup"><span data-stu-id="b8f95-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="b8f95-242">Dans le test séquentiel précédent de hello, 1000 opérations a nécessité 129 secondes hello en dehors de centre de données et 21 secondes dans le centre de données hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="b8f95-243">Cependant, avec les paramètres table, les opérations de 1000 uniquement 2,6 secondes en dehors du centre de données hello et 0,4 seconde dans le centre de données hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="b8f95-244">Pour plus d’informations sur les paramètres table, consultez [Paramètres table](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8f95-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="b8f95-245">Copie en bloc SQL</span><span class="sxs-lookup"><span data-stu-id="b8f95-245">SQL bulk copy</span></span>
<span data-ttu-id="b8f95-246">Copie en bloc SQL est une autre façon tooinsert grandes quantités de données dans une base de données cible.</span><span class="sxs-lookup"><span data-stu-id="b8f95-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="b8f95-247">Applications .NET peuvent utiliser hello **SqlBulkCopy** opérations d’insertion en bloc tooperform de classe.</span><span class="sxs-lookup"><span data-stu-id="b8f95-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="b8f95-248">**SqlBulkCopy** est similaire dans l’outil de ligne de commande de fonction toohello, **Bcp.exe**, ou instruction Transact-SQL, de hello **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="b8f95-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="b8f95-249">Hello exemple de code suivant montre comment les lignes dans la source de hello hello de copie toobulk **DataTable**, table, table de destination toohello dans SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="b8f95-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="b8f95-250">Il existe quelques cas où la copie en bloc est préférable à l’utilisation des paramètres table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="b8f95-251">Consultez le tableau de comparaison hello de paramètres table et les opérations BULK INSERT dans la rubrique de hello [paramètres table](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8f95-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="b8f95-252">Hello résultats des tests ad hoc suivants montrent les performances de hello du traitement par lot avec **SqlBulkCopy** en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="b8f95-253">Opérations</span><span class="sxs-lookup"><span data-stu-id="b8f95-253">Operations</span></span> | <span data-ttu-id="b8f95-254">On-Premises tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="b8f95-255">Azure (même centre de données)</span><span class="sxs-lookup"><span data-stu-id="b8f95-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f95-256">1</span><span class="sxs-lookup"><span data-stu-id="b8f95-256">1</span></span> |<span data-ttu-id="b8f95-257">433</span><span class="sxs-lookup"><span data-stu-id="b8f95-257">433</span></span> |<span data-ttu-id="b8f95-258">57</span><span class="sxs-lookup"><span data-stu-id="b8f95-258">57</span></span> |
| <span data-ttu-id="b8f95-259">10</span><span class="sxs-lookup"><span data-stu-id="b8f95-259">10</span></span> |<span data-ttu-id="b8f95-260">441</span><span class="sxs-lookup"><span data-stu-id="b8f95-260">441</span></span> |<span data-ttu-id="b8f95-261">32</span><span class="sxs-lookup"><span data-stu-id="b8f95-261">32</span></span> |
| <span data-ttu-id="b8f95-262">100</span><span class="sxs-lookup"><span data-stu-id="b8f95-262">100</span></span> |<span data-ttu-id="b8f95-263">636</span><span class="sxs-lookup"><span data-stu-id="b8f95-263">636</span></span> |<span data-ttu-id="b8f95-264">53</span><span class="sxs-lookup"><span data-stu-id="b8f95-264">53</span></span> |
| <span data-ttu-id="b8f95-265">1 000</span><span class="sxs-lookup"><span data-stu-id="b8f95-265">1000</span></span> |<span data-ttu-id="b8f95-266">2 535</span><span class="sxs-lookup"><span data-stu-id="b8f95-266">2535</span></span> |<span data-ttu-id="b8f95-267">341</span><span class="sxs-lookup"><span data-stu-id="b8f95-267">341</span></span> |
| <span data-ttu-id="b8f95-268">10000</span><span class="sxs-lookup"><span data-stu-id="b8f95-268">10000</span></span> |<span data-ttu-id="b8f95-269">21 605</span><span class="sxs-lookup"><span data-stu-id="b8f95-269">21605</span></span> |<span data-ttu-id="b8f95-270">2 737</span><span class="sxs-lookup"><span data-stu-id="b8f95-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="b8f95-271">Les résultats ne représentent pas des valeurs de référence.</span><span class="sxs-lookup"><span data-stu-id="b8f95-271">Results are not benchmarks.</span></span> <span data-ttu-id="b8f95-272">Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="b8f95-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="b8f95-273">Dans le traitement par lots plus petits, les paramètres table hello utilisez obtenu les meilleures performances hello **SqlBulkCopy** classe.</span><span class="sxs-lookup"><span data-stu-id="b8f95-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="b8f95-274">Toutefois, **SqlBulkCopy** effectuée 12-31 % plus rapide que les paramètres table pour les tests hello de 1 000 et 10 000 lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="b8f95-275">Comme les paramètres table, **SqlBulkCopy** est une bonne option pour les insertions traitées par lot, en particulier lors de la comparaison toohello les performances des opérations de non-batch.</span><span class="sxs-lookup"><span data-stu-id="b8f95-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="b8f95-276">Pour plus d’informations sur la copie en bloc dans ADO.NET, consultez [Opérations de copie en bloc dans SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8f95-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="b8f95-277">Instructions INSERT paramétrables sur plusieurs lignes</span><span class="sxs-lookup"><span data-stu-id="b8f95-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="b8f95-278">Pour les lots de petite taille consiste tooconstruct un grand paramétrables instruction INSERT qui insère plusieurs lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="b8f95-279">Hello, exemple de code suivant illustre cette technique.</span><span class="sxs-lookup"><span data-stu-id="b8f95-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="b8f95-280">Cet exemple est destiné le concept de base tooshow hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="b8f95-281">Un scénario plus réaliste effectuerait une boucle simultanément via la chaîne de requête hello requis entités tooconstruct hello et paramètres de commande hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="b8f95-282">Vous êtes limité total tooa 2100 des paramètres de requête, cela limite le nombre total de hello de lignes qui peuvent être traitées de cette manière.</span><span class="sxs-lookup"><span data-stu-id="b8f95-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="b8f95-283">Hello suivant ad-hoc résultats afficher hello les performances des tests de ce type d’instruction d’insertion en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="b8f95-284">Opérations</span><span class="sxs-lookup"><span data-stu-id="b8f95-284">Operations</span></span> | <span data-ttu-id="b8f95-285">Paramètres table (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="b8f95-286">Instruction INSERT unique (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f95-287">1</span><span class="sxs-lookup"><span data-stu-id="b8f95-287">1</span></span> |<span data-ttu-id="b8f95-288">32</span><span class="sxs-lookup"><span data-stu-id="b8f95-288">32</span></span> |<span data-ttu-id="b8f95-289">20</span><span class="sxs-lookup"><span data-stu-id="b8f95-289">20</span></span> |
| <span data-ttu-id="b8f95-290">10</span><span class="sxs-lookup"><span data-stu-id="b8f95-290">10</span></span> |<span data-ttu-id="b8f95-291">30</span><span class="sxs-lookup"><span data-stu-id="b8f95-291">30</span></span> |<span data-ttu-id="b8f95-292">25</span><span class="sxs-lookup"><span data-stu-id="b8f95-292">25</span></span> |
| <span data-ttu-id="b8f95-293">100</span><span class="sxs-lookup"><span data-stu-id="b8f95-293">100</span></span> |<span data-ttu-id="b8f95-294">33</span><span class="sxs-lookup"><span data-stu-id="b8f95-294">33</span></span> |<span data-ttu-id="b8f95-295">51</span><span class="sxs-lookup"><span data-stu-id="b8f95-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="b8f95-296">Les résultats ne représentent pas des valeurs de référence.</span><span class="sxs-lookup"><span data-stu-id="b8f95-296">Results are not benchmarks.</span></span> <span data-ttu-id="b8f95-297">Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="b8f95-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="b8f95-298">Cette approche peut être légèrement plus rapide pour les lots comportant moins de 100 lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="b8f95-299">Bien que l’amélioration de hello est petite, cette technique est une autre option qui peut fonctionner dans votre scénario d’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="b8f95-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="b8f95-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="b8f95-300">DataAdapter</span></span>
<span data-ttu-id="b8f95-301">Hello **DataAdapter** classe vous permet de toomodify un **DataSet** de l’objet, puis soumettez les modifications hello en tant qu’opérations INSERT, UPDATE et DELETE.</span><span class="sxs-lookup"><span data-stu-id="b8f95-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="b8f95-302">Si vous utilisez hello **DataAdapter** de cette manière, il est important de toonote qui séparent les appels sont effectués pour chaque opération distincte.</span><span class="sxs-lookup"><span data-stu-id="b8f95-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="b8f95-303">tooimprove des performances, utilisez hello **UpdateBatchSize** nombre toohello de propriété d’opérations qui doivent être traités par lot à la fois.</span><span class="sxs-lookup"><span data-stu-id="b8f95-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="b8f95-304">Pour plus d’informations, consultez [Exécution de traitements par lots à l’aide de DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8f95-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="b8f95-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="b8f95-305">Entity framework</span></span>
<span data-ttu-id="b8f95-306">Entity Framework ne prend pas actuellement en charge le traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="b8f95-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="b8f95-307">Différents développeurs de la Communauté de hello ont tenté de solutions de contournement toodemonstrate comme remplacement hello **SaveChanges** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8f95-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="b8f95-308">Mais hello solutions sont généralement complexes et adaptées toohello application et le modèle de données.</span><span class="sxs-lookup"><span data-stu-id="b8f95-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="b8f95-309">projet de codeplex Entity Framework Hello possède actuellement une page de discussion sur cette demande de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b8f95-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="b8f95-310">tooview cette discussion, consultez [2 août 2012 - Notes de réunion conception](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="b8f95-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="b8f95-311">XML</span><span class="sxs-lookup"><span data-stu-id="b8f95-311">XML</span></span>
<span data-ttu-id="b8f95-312">Par souci d’exhaustivité, nous pensons qu’il est important tootalk à propos de XML en tant qu’une stratégie de traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="b8f95-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="b8f95-313">Toutefois, utilisez hello XML a aucun avantage par rapport autres méthodes et plusieurs inconvénients.</span><span class="sxs-lookup"><span data-stu-id="b8f95-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="b8f95-314">approche de Hello est tootable table des paramètres similaires, mais un fichier XML ou une chaîne est passée de procédure stockée de tooa au lieu d’une table définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8f95-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="b8f95-315">procédure stockée Hello analyse les commandes de hello dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="b8f95-316">Il existe plusieurs inconvénients toothis approche :</span><span class="sxs-lookup"><span data-stu-id="b8f95-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="b8f95-317">L’utilisation de XML peut s’avérer fastidieuse et sujette aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="b8f95-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="b8f95-318">Analyse hello XML sur la base de données hello peut être gourmande en ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="b8f95-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="b8f95-319">Dans la plupart des cas, cette méthode est plus lente que celle des paramètres table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="b8f95-320">Pour ces raisons, utilisation de la hello de XML pour les requêtes de traitement par lots n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="b8f95-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="b8f95-321">Remarques relatives au traitement par lots</span><span class="sxs-lookup"><span data-stu-id="b8f95-321">Batching considerations</span></span>
<span data-ttu-id="b8f95-322">Hello les sections suivantes fournit plus d’informations pour une utilisation hello du traitement par lots dans les applications de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="b8f95-323">Compromis</span><span class="sxs-lookup"><span data-stu-id="b8f95-323">Tradeoffs</span></span>
<span data-ttu-id="b8f95-324">En fonction de votre architecture, le traitement par lots peut vous obliger à faire un compromis entre performances et résilience.</span><span class="sxs-lookup"><span data-stu-id="b8f95-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="b8f95-325">Par exemple, considérez le scénario hello où votre rôle rencontre une défaillance inattendue.</span><span class="sxs-lookup"><span data-stu-id="b8f95-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="b8f95-326">Si vous perdez une ligne de données, l’impact de hello est inférieure à impact hello de perdre un grand lot de lignes non envoyées.</span><span class="sxs-lookup"><span data-stu-id="b8f95-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="b8f95-327">Il existe un risque plus élevé lorsque le tampon de lignes avant de les envoyer toohello de base de données dans une fenêtre de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="b8f95-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="b8f95-328">En raison de ce compromis, évaluez le type hello des opérations de ce lot vous.</span><span class="sxs-lookup"><span data-stu-id="b8f95-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="b8f95-329">Optez pour une approche plus agressive (lots plus volumineux et intervalles plus longs) pour les données moins critiques.</span><span class="sxs-lookup"><span data-stu-id="b8f95-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="b8f95-330">Taille du lot</span><span class="sxs-lookup"><span data-stu-id="b8f95-330">Batch size</span></span>
<span data-ttu-id="b8f95-331">Dans nos tests, il a été généralement aucun avantage toobreaking grands lots en plus petits.</span><span class="sxs-lookup"><span data-stu-id="b8f95-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="b8f95-332">En fait, cette sous-division s’est souvent traduite par des performances plus lentes que celles obtenues avec l’envoi d’un seul lot plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="b8f95-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="b8f95-333">Par exemple, considérez un scénario où vous souhaitez tooinsert 1000 lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="b8f95-334">Hello tableau suivant montre combien il prend les paramètres table toouse tooinsert 1000 lignes lorsqu’ils sont divisés en lots plus petits.</span><span class="sxs-lookup"><span data-stu-id="b8f95-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="b8f95-335">Taille du lot</span><span class="sxs-lookup"><span data-stu-id="b8f95-335">Batch size</span></span> | <span data-ttu-id="b8f95-336">Itérations</span><span class="sxs-lookup"><span data-stu-id="b8f95-336">Iterations</span></span> | <span data-ttu-id="b8f95-337">Paramètres table (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f95-338">1 000</span><span class="sxs-lookup"><span data-stu-id="b8f95-338">1000</span></span> |<span data-ttu-id="b8f95-339">1</span><span class="sxs-lookup"><span data-stu-id="b8f95-339">1</span></span> |<span data-ttu-id="b8f95-340">347</span><span class="sxs-lookup"><span data-stu-id="b8f95-340">347</span></span> |
| <span data-ttu-id="b8f95-341">500</span><span class="sxs-lookup"><span data-stu-id="b8f95-341">500</span></span> |<span data-ttu-id="b8f95-342">2</span><span class="sxs-lookup"><span data-stu-id="b8f95-342">2</span></span> |<span data-ttu-id="b8f95-343">355</span><span class="sxs-lookup"><span data-stu-id="b8f95-343">355</span></span> |
| <span data-ttu-id="b8f95-344">100</span><span class="sxs-lookup"><span data-stu-id="b8f95-344">100</span></span> |<span data-ttu-id="b8f95-345">10</span><span class="sxs-lookup"><span data-stu-id="b8f95-345">10</span></span> |<span data-ttu-id="b8f95-346">465</span><span class="sxs-lookup"><span data-stu-id="b8f95-346">465</span></span> |
| <span data-ttu-id="b8f95-347">50</span><span class="sxs-lookup"><span data-stu-id="b8f95-347">50</span></span> |<span data-ttu-id="b8f95-348">20</span><span class="sxs-lookup"><span data-stu-id="b8f95-348">20</span></span> |<span data-ttu-id="b8f95-349">630</span><span class="sxs-lookup"><span data-stu-id="b8f95-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="b8f95-350">Les résultats ne représentent pas des valeurs de référence.</span><span class="sxs-lookup"><span data-stu-id="b8f95-350">Results are not benchmarks.</span></span> <span data-ttu-id="b8f95-351">Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="b8f95-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="b8f95-352">Vous pouvez voir que des performances optimales hello pour 1 000 lignes soient toosubmit les tous en même temps.</span><span class="sxs-lookup"><span data-stu-id="b8f95-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="b8f95-353">Dans d’autres tests (non illustrés ici) s’est un toobreak de gain de performances un lot de 10 000 lignes et deux lots de 5 000 lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="b8f95-354">Mais le schéma de la table hello pour ces tests est relativement simple, vous devez réaliser des tests sur vos données et spécifiques tooverify des tailles de lot ces conclusions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="b8f95-355">Un autre facteur tooconsider est que si le lot total de hello devient trop volumineux, base de données SQL peut limiter et refuser le traitement par lots de toocommit hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="b8f95-356">Pour de meilleurs résultats de hello, test toodetermine de votre scénario spécifique, s’il existe une taille de lot idéale.</span><span class="sxs-lookup"><span data-stu-id="b8f95-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="b8f95-357">Rendre la taille de lot hello configurable au runtime tooenable rapides réglages basés sur les performances ou des erreurs.</span><span class="sxs-lookup"><span data-stu-id="b8f95-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="b8f95-358">Enfin, équilibrez taille hello du lot de hello hello les risques associés au traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="b8f95-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="b8f95-359">Si des erreurs temporaires ou hello rôle échoue, envisagez les conséquences hello d’une nouvelle tentative d’opération de hello ou de perte de données hello dans un lot de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="b8f95-360">Traitement en parallèle</span><span class="sxs-lookup"><span data-stu-id="b8f95-360">Parallel processing</span></span>
<span data-ttu-id="b8f95-361">Que se passe-t-il si vous a duré approche hello de réduction de la taille de lot hello mais utilisé plusieurs threads tooexecute hello travail ?</span><span class="sxs-lookup"><span data-stu-id="b8f95-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="b8f95-362">Là encore, nos tests ont montré que plusieurs petits lots multithreads produisaient de moins bonnes performances que celles obtenues avec un seul lot plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="b8f95-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="b8f95-363">Hello test suivant tente de tooinsert 1000 lignes dans un ou plusieurs traitements parallèles.</span><span class="sxs-lookup"><span data-stu-id="b8f95-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="b8f95-364">Il montre comment un plus grand nombre de lots simultanés affecte les performances.</span><span class="sxs-lookup"><span data-stu-id="b8f95-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="b8f95-365">Taille de lot [itérations]</span><span class="sxs-lookup"><span data-stu-id="b8f95-365">Batch size [Iterations]</span></span> | <span data-ttu-id="b8f95-366">Deux threads (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-366">Two threads (ms)</span></span> | <span data-ttu-id="b8f95-367">Quatre threads (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-367">Four threads (ms)</span></span> | <span data-ttu-id="b8f95-368">Six threads (ms)</span><span class="sxs-lookup"><span data-stu-id="b8f95-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b8f95-369">1 000 [1]</span><span class="sxs-lookup"><span data-stu-id="b8f95-369">1000 [1]</span></span> |<span data-ttu-id="b8f95-370">277</span><span class="sxs-lookup"><span data-stu-id="b8f95-370">277</span></span> |<span data-ttu-id="b8f95-371">315</span><span class="sxs-lookup"><span data-stu-id="b8f95-371">315</span></span> |<span data-ttu-id="b8f95-372">266</span><span class="sxs-lookup"><span data-stu-id="b8f95-372">266</span></span> |
| <span data-ttu-id="b8f95-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="b8f95-373">500 [2]</span></span> |<span data-ttu-id="b8f95-374">548</span><span class="sxs-lookup"><span data-stu-id="b8f95-374">548</span></span> |<span data-ttu-id="b8f95-375">278</span><span class="sxs-lookup"><span data-stu-id="b8f95-375">278</span></span> |<span data-ttu-id="b8f95-376">256</span><span class="sxs-lookup"><span data-stu-id="b8f95-376">256</span></span> |
| <span data-ttu-id="b8f95-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="b8f95-377">250 [4]</span></span> |<span data-ttu-id="b8f95-378">405</span><span class="sxs-lookup"><span data-stu-id="b8f95-378">405</span></span> |<span data-ttu-id="b8f95-379">329</span><span class="sxs-lookup"><span data-stu-id="b8f95-379">329</span></span> |<span data-ttu-id="b8f95-380">265</span><span class="sxs-lookup"><span data-stu-id="b8f95-380">265</span></span> |
| <span data-ttu-id="b8f95-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="b8f95-381">100 [10]</span></span> |<span data-ttu-id="b8f95-382">488</span><span class="sxs-lookup"><span data-stu-id="b8f95-382">488</span></span> |<span data-ttu-id="b8f95-383">439</span><span class="sxs-lookup"><span data-stu-id="b8f95-383">439</span></span> |<span data-ttu-id="b8f95-384">391</span><span class="sxs-lookup"><span data-stu-id="b8f95-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="b8f95-385">Les résultats ne représentent pas des valeurs de référence.</span><span class="sxs-lookup"><span data-stu-id="b8f95-385">Results are not benchmarks.</span></span> <span data-ttu-id="b8f95-386">Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="b8f95-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="b8f95-387">Il existe plusieurs raisons potentielles à une dégradation des performances hello tooparallelism échéance :</span><span class="sxs-lookup"><span data-stu-id="b8f95-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="b8f95-388">Exécution de plusieurs appels réseau simultanés au lieu d’un seul.</span><span class="sxs-lookup"><span data-stu-id="b8f95-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="b8f95-389">Plusieurs opérations sur une seule table peuvent entraîner une contention et un blocage.</span><span class="sxs-lookup"><span data-stu-id="b8f95-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="b8f95-390">Surcharges associées multithreading.</span><span class="sxs-lookup"><span data-stu-id="b8f95-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="b8f95-391">dépenses Hello d’ouvrir plusieurs connexions compense avantage hello du traitement parallèle.</span><span class="sxs-lookup"><span data-stu-id="b8f95-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="b8f95-392">Si vous ciblez différentes tables ou bases de données, il est possible toosee des performances gain avec cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="b8f95-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="b8f95-393">Le partitionnement ou les fédérations de bases de données constitue un scénario possible pour une telle approche.</span><span class="sxs-lookup"><span data-stu-id="b8f95-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="b8f95-394">Partitionnement utilise plusieurs bases de données et les itinéraires différents tooeach de données.</span><span class="sxs-lookup"><span data-stu-id="b8f95-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="b8f95-395">Si chaque petit lot est tooa autre base de données, puis en effectuant les opérations hello en parallèle peut être plus efficace.</span><span class="sxs-lookup"><span data-stu-id="b8f95-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="b8f95-396">Toutefois, gain de performances hello n’est pas assez important toouse comme base hello pour un partitionnement de base de données arbre de décision toouse dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="b8f95-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="b8f95-397">Dans certains modèles, l’exécution parallèle de lots plus petits peut entraîner une amélioration du débit des demandes dans un système sous charge.</span><span class="sxs-lookup"><span data-stu-id="b8f95-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="b8f95-398">Dans ce cas, même s’il est plus rapide tooprocess un seul grand traitement, le traitement de plusieurs lots en parallèle peut être plus efficace.</span><span class="sxs-lookup"><span data-stu-id="b8f95-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="b8f95-399">Si vous n’utilisez pas l’exécution en parallèle, envisagez le nombre maximal de contrôle hello de threads de travail.</span><span class="sxs-lookup"><span data-stu-id="b8f95-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="b8f95-400">Un plus petit nombre peut réduire la contention et accélérer la durée d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b8f95-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="b8f95-401">Envisagez également de charge supplémentaire hello sur la base de données cible hello dans les connexions et transactions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="b8f95-402">Facteurs de performances associés</span><span class="sxs-lookup"><span data-stu-id="b8f95-402">Related performance factors</span></span>
<span data-ttu-id="b8f95-403">Les conseils classiques sur les performances de base de données s’appliquent également au traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="b8f95-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="b8f95-404">Par exemple, les performances d’insertion sont réduites pour les tables qui ont une grande clé primaire ou de nombreux index non ordonnés en clusters.</span><span class="sxs-lookup"><span data-stu-id="b8f95-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="b8f95-405">Si les paramètres table utilisent une procédure stockée, vous pouvez utiliser la commande hello **SET NOCOUNT ON** au début de hello de procédure de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="b8f95-406">Cette instruction supprime le retour hello du nombre de hello de lignes hello affectée dans la procédure de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="b8f95-407">Toutefois, dans nos tests, hello utilisation de **SET NOCOUNT ON** n’avait aucun effet ou une diminution des performances.</span><span class="sxs-lookup"><span data-stu-id="b8f95-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="b8f95-408">Hello procédure stockée de test était simple avec un seul **insérer** du paramètre de table hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="b8f95-409">Il est possible que les procédures stockées plus complexes puissent bénéficier de cette instruction.</span><span class="sxs-lookup"><span data-stu-id="b8f95-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="b8f95-410">Mais ne supposez pas que l’ajout **SET NOCOUNT ON** tooyour stockée procédure automatiquement améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="b8f95-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="b8f95-411">toounderstand hello effet, testez votre procédure stockée avec et sans hello **SET NOCOUNT ON** instruction.</span><span class="sxs-lookup"><span data-stu-id="b8f95-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="b8f95-412">Scénarios de traitement par lots</span><span class="sxs-lookup"><span data-stu-id="b8f95-412">Batching scenarios</span></span>
<span data-ttu-id="b8f95-413">Hello sections suivantes décrivent comment les paramètres table toouse dans trois scénarios d’application.</span><span class="sxs-lookup"><span data-stu-id="b8f95-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="b8f95-414">premier scénario de Hello montre comment la mémoire tampon et le traitement par lots peuvent collaborer.</span><span class="sxs-lookup"><span data-stu-id="b8f95-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="b8f95-415">deuxième scénario de Hello améliore les performances en effectuant les opérations maître / détails dans un appel de procédure stockée unique.</span><span class="sxs-lookup"><span data-stu-id="b8f95-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="b8f95-416">Hello scénario final montre comment les paramètres table toouse dans une opération « UPSERT ».</span><span class="sxs-lookup"><span data-stu-id="b8f95-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="b8f95-417">Mise en mémoire tampon</span><span class="sxs-lookup"><span data-stu-id="b8f95-417">Buffering</span></span>
<span data-ttu-id="b8f95-418">Bien que certains scénarios apparaissent comme des candidats évidents pour le traitement par lots, il existe de nombreux scénarios qui peuvent tirer parti des avantages d’un traitement par lots différé.</span><span class="sxs-lookup"><span data-stu-id="b8f95-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="b8f95-419">Toutefois, également le traitement différé a un plus grand risque que les données de salutation sont perdues au cours de l’événement hello d’une défaillance inattendue.</span><span class="sxs-lookup"><span data-stu-id="b8f95-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="b8f95-420">Il est important toounderstand ce risque et prendre en compte les conséquences hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="b8f95-421">Par exemple, considérez une application web qui effectue le suivi de l’historique de navigation hello de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8f95-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="b8f95-422">Sur chaque demande de page, application hello peut rendre une base de données appel toorecord hello page Affichage de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8f95-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="b8f95-423">Mais les performances et évolutivité supérieures peuvent être obtenues en mise en mémoire tampon des opérations de navigation des utilisateurs hello et en envoyant cette base de données toohello de données dans des lots.</span><span class="sxs-lookup"><span data-stu-id="b8f95-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="b8f95-424">Vous pouvez déclencher la mise à jour de la base de données hello par temps écoulé et/ou taille de mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="b8f95-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="b8f95-425">Par exemple, une règle peut spécifier que ce lot hello doit être traité après 20 secondes ou lorsque la mémoire tampon de hello atteint 1 000 éléments.</span><span class="sxs-lookup"><span data-stu-id="b8f95-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="b8f95-426">code Hello suivant utilise [Extensions réactives - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess mis en mémoire tampon les événements déclenchés par une classe d’analyse.</span><span class="sxs-lookup"><span data-stu-id="b8f95-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="b8f95-427">Hello lorsque les remplissages de la mémoire tampon ou un délai d’attente est atteint, lot hello de données utilisateur est envoyé de la base de données toohello avec un paramètre table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="b8f95-428">Bonjour les détails de la navigation NavHistoryData classe modèles hello utilisateur suivants.</span><span class="sxs-lookup"><span data-stu-id="b8f95-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="b8f95-429">Il contient des informations de base comme identificateur d’utilisateur hello, hello URL accessible et hello temps d’accès.</span><span class="sxs-lookup"><span data-stu-id="b8f95-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="b8f95-430">Hello NavHistoryDataMonitor classe est responsable de la mise en mémoire tampon de base de données de navigation données toohello hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8f95-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="b8f95-431">Elle contient une méthode appelée RecordUserNavigationEntry qui répond en déclenchant un événement **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="b8f95-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="b8f95-432">Hello de code suivant montre la logique du constructeur hello qui utilise Rx toocreate une collection observable selon les événements hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="b8f95-433">Elle s’abonne ensuite toothis les collection observable avec la méthode de tampon hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="b8f95-434">surcharge de Hello Spécifie que cette mémoire tampon hello doit être envoyée à toutes les 20 secondes ou 1 000 entrées.</span><span class="sxs-lookup"><span data-stu-id="b8f95-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="b8f95-435">Hello Gestionnaire convertit tous les éléments de hello mis en mémoire tampon en un type de table incluse, mais cette procédure tooa stocké de type ce lot hello de processus.</span><span class="sxs-lookup"><span data-stu-id="b8f95-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="b8f95-436">Hello de code suivant montre définition complète de hello pour hello NavHistoryDataEventArgs et classes de NavHistoryDataMonitor hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="b8f95-437">toouse cette classe mise en mémoire tampon, l’application hello crée un objet NavHistoryDataMonitor statique.</span><span class="sxs-lookup"><span data-stu-id="b8f95-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="b8f95-438">Chaque fois un utilisateur accède à une page, application hello appelle la méthode de NavHistoryDataMonitor.RecordUserNavigationEntry hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="b8f95-439">Hello logique de mise en mémoire tampon déroule tootake administration de l’envoi de ces bases de données de toohello entrées par lots.</span><span class="sxs-lookup"><span data-stu-id="b8f95-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="b8f95-440">Maître/détail</span><span class="sxs-lookup"><span data-stu-id="b8f95-440">Master detail</span></span>
<span data-ttu-id="b8f95-441">Les paramètres table sont utiles pour les scénarios INSERT simples.</span><span class="sxs-lookup"><span data-stu-id="b8f95-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="b8f95-442">Toutefois, il peut être plus difficiles insertions toobatch qui impliquent, et plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="b8f95-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="b8f95-443">scénario de « maître/détail » Hello est un bon exemple.</span><span class="sxs-lookup"><span data-stu-id="b8f95-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="b8f95-444">table principale de Hello identifie l’entité principale de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="b8f95-445">Une ou plusieurs tables de détails stockent des données sur les entités hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="b8f95-446">Dans ce scénario, les relations de clé étrangères appliquent la relation de hello de détails tooa seule entité principale.</span><span class="sxs-lookup"><span data-stu-id="b8f95-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="b8f95-447">Imaginez une version simplifiée d’une table PurchaseOrder et de sa table OrderDetail associée.</span><span class="sxs-lookup"><span data-stu-id="b8f95-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="b8f95-448">Hello suivant Transact-SQL crée la table de PurchaseOrder hello avec quatre colonnes : OrderID, OrderDate, CustomerID et état.</span><span class="sxs-lookup"><span data-stu-id="b8f95-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="b8f95-449">Chaque commande contient un ou plusieurs achats de produits.</span><span class="sxs-lookup"><span data-stu-id="b8f95-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="b8f95-450">Ces informations sont capturées dans la table PurchaseOrderDetail de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="b8f95-451">Hello suivant Transact-SQL crée la table PurchaseOrderDetail de hello avec cinq colonnes : OrderID, OrderDetailID, ProductID, UnitPrice et OrderQty.</span><span class="sxs-lookup"><span data-stu-id="b8f95-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="b8f95-452">colonne de OrderID Hello dans la table PurchaseOrderDetail de hello doit faire référence à une commande à partir de la table de PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="b8f95-453">Hello définition d’une clé étrangère applique cette contrainte.</span><span class="sxs-lookup"><span data-stu-id="b8f95-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="b8f95-454">Dans l’ordre toouse les paramètres table, vous devez disposer d’un type de table défini par l’utilisateur pour chaque table cible.</span><span class="sxs-lookup"><span data-stu-id="b8f95-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="b8f95-455">Vous devez ensuite définir ensuite une procédure stockée qui accepte les tables de ces types.</span><span class="sxs-lookup"><span data-stu-id="b8f95-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="b8f95-456">Cette procédure permet à un lot d’application toolocally un ensemble de commandes et les détails de la commande dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="b8f95-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="b8f95-457">Hello Transact-SQL suivant fournit déclaration de procédure stockée complète hello pour cet exemple de bon de commande.</span><span class="sxs-lookup"><span data-stu-id="b8f95-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="b8f95-458">Dans cet exemple, hello définies localement @IdentityLink table stocke les valeurs OrderID réels hello à partir des lignes de hello qui vient d’être inséré.</span><span class="sxs-lookup"><span data-stu-id="b8f95-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="b8f95-459">Ces identificateurs de commande sont différents des valeurs de OrderID temporaires hello Bonjour @orders et @details paramètres table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="b8f95-460">Pour cette raison, hello @IdentityLink table connecte ensuite les valeurs OrderID hello de hello @orders toohello réel OrderID valeurs de paramètre pour les nouvelles lignes de hello dans la table de PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="b8f95-461">Après cette étape, hello @IdentityLink table facilitent l’insertion détails de la commande hello avec hello OrderID réelle qui satisfait à la contrainte de clé étrangère hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="b8f95-462">Cette procédure stockée peut être utilisée à partir d’un code ou d’autres appels Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="b8f95-463">Consultez la section de paramètres table hello de ce document pour obtenir un exemple de code.</span><span class="sxs-lookup"><span data-stu-id="b8f95-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="b8f95-464">Hello Transact-SQL de suivant montre comment toocall hello sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="b8f95-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="b8f95-465">Cette solution permet à chaque toouse lot un ensemble de valeurs OrderID qui commencent à 1.</span><span class="sxs-lookup"><span data-stu-id="b8f95-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="b8f95-466">Ces valeurs OrderID temporaires décrivent les relations hello dans un lot de hello, mais les valeurs OrderID réelles hello sont déterminées lors de l’opération d’insertion hello hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="b8f95-467">Vous pouvez exécuter hello mêmes instructions dans l’exemple précédent de hello à plusieurs reprises et générer des commandes uniques dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="b8f95-468">Vous devez donc penser à ajouter plus de code ou de logique de base de données pour éviter les doublons lorsque vous utilisez cette technique de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="b8f95-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="b8f95-469">Cet exemple montre que les opérations de base de données encore plus complexes, telles que les opérations maître/détail, peuvent être traitées par lots à l’aide des paramètres table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="b8f95-470">Opération UPSERT</span><span class="sxs-lookup"><span data-stu-id="b8f95-470">UPSERT</span></span>
<span data-ttu-id="b8f95-471">Un autre scénario de traitement par lots implique la mise à jour simultanée de lignes existantes et l’insertion de nouvelles lignes.</span><span class="sxs-lookup"><span data-stu-id="b8f95-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="b8f95-472">Cette opération est parfois désignée tooas une opération « UPSERT » (update + insert).</span><span class="sxs-lookup"><span data-stu-id="b8f95-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="b8f95-473">Plutôt que d’effectuer des appels distincts tooINSERT et mise à jour, instruction de fusion hello est mieux adapté toothis tâche.</span><span class="sxs-lookup"><span data-stu-id="b8f95-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="b8f95-474">Hello instruction MERGE peut effectuer les deux insérer et mettre à jour des opérations dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="b8f95-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="b8f95-475">Paramètres table peuvent servir hello fusion instruction tooperform mises à jour et insertions.</span><span class="sxs-lookup"><span data-stu-id="b8f95-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="b8f95-476">Par exemple, supposons une table d’employé simplifiée qui contient hello suivant colonnes : EmployeeID, FirstName, LastName, SocialSecurityNumber :</span><span class="sxs-lookup"><span data-stu-id="b8f95-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="b8f95-477">Dans cet exemple, vous pouvez utiliser des faits hello que hello SocialSecurityNumber est unique tooperform une fusion de plusieurs employés.</span><span class="sxs-lookup"><span data-stu-id="b8f95-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="b8f95-478">Tout d’abord, créez les type de table défini par l’utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="b8f95-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="b8f95-479">Ensuite, créez une procédure stockée ou écrire du code qui utilise hello mise à jour de fusion instruction tooperform hello et insert.</span><span class="sxs-lookup"><span data-stu-id="b8f95-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="b8f95-480">Hello exemple suivant utilise hello instruction MERGE sur un paramètre table, @employees, de type EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="b8f95-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="b8f95-481">Hello contenu Hello @employees table ne sont pas affichés ici.</span><span class="sxs-lookup"><span data-stu-id="b8f95-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="b8f95-482">Pour plus d’informations, consultez la documentation de hello et des exemples pour l’instruction de fusion hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="b8f95-483">Bien que hello même travail puisse être effectué dans en plusieurs étapes stockées appel de procédure avec les opérations INSERT et UPDATE distinctes, hello instruction MERGE est plus efficace.</span><span class="sxs-lookup"><span data-stu-id="b8f95-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="b8f95-484">Code de base de données peut également construire des appels Transact-SQL qui utilisent l’instruction MERGE de hello directement sans avoir recours à deux appels de base de données pour INSERT et UPDATE.</span><span class="sxs-lookup"><span data-stu-id="b8f95-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="b8f95-485">Résumé des recommandations</span><span class="sxs-lookup"><span data-stu-id="b8f95-485">Recommendation summary</span></span>
<span data-ttu-id="b8f95-486">Hello liste suivante fournit un résumé de hello le traitement par lot les recommandations décrites dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="b8f95-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="b8f95-487">Utilisez la mise en mémoire tampon et de traitement par lot des performances de hello tooincrease et l’évolutivité des applications de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f95-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="b8f95-488">Comprendre les compromis de hello entre le traitement par lot/mise en mémoire tampon et la résilience.</span><span class="sxs-lookup"><span data-stu-id="b8f95-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="b8f95-489">Lors d’une défaillance de rôle, risque hello de perdre un lot non traité de données critiques peut-être dépasser le gain de performances hello du traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="b8f95-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="b8f95-490">Tentative de tookeep de base de données de tous les appels toohello au sein d’une latence tooreduce de centre de données unique.</span><span class="sxs-lookup"><span data-stu-id="b8f95-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="b8f95-491">Si vous choisissez une technique de traitement par lot, les paramètres table offrent une souplesse et des performances optimales hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="b8f95-492">Pourquoi plus rapide insérer les performances, suivez ces recommandations générales, mais votre scénario de test :</span><span class="sxs-lookup"><span data-stu-id="b8f95-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="b8f95-493">Pour moins de 100 lignes, utilisez une seule commande INSERT paramétrable.</span><span class="sxs-lookup"><span data-stu-id="b8f95-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="b8f95-494">Pour moins de 1 000 lignes, utilisez des paramètres table.</span><span class="sxs-lookup"><span data-stu-id="b8f95-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="b8f95-495">Au-delà de 1 000 lignes, utilisez SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="b8f95-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="b8f95-496">Pour mettre à jour et les opérations de suppression, utiliser des paramètres table avec logique de la procédure stockée qui détermine le bon fonctionnement de hello sur chaque ligne de paramètre de table hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="b8f95-497">Conseils relatifs à la taille de lot :</span><span class="sxs-lookup"><span data-stu-id="b8f95-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="b8f95-498">Utilisez hello plus grandes tailles de lot qui ont un sens pour votre application et les besoins de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="b8f95-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="b8f95-499">Le gain de performances de hello solde de grands lots avec des risques de hello de défaillances temporaires ou catastrophiques.</span><span class="sxs-lookup"><span data-stu-id="b8f95-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="b8f95-500">Quelle est la conséquence de hello de nouvelles tentatives ou de perte de données hello dans un lot de hello ?</span><span class="sxs-lookup"><span data-stu-id="b8f95-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="b8f95-501">Test hello plus grand lot taille tooverify que base de données SQL ne rejette pas.</span><span class="sxs-lookup"><span data-stu-id="b8f95-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="b8f95-502">Créer des paramètres de configuration qui contrôle le traitement par lot, telles que la taille de lot hello ou de la fenêtre de temps de mise en mémoire tampon hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="b8f95-503">Ces paramètres garantissent la flexibilité.</span><span class="sxs-lookup"><span data-stu-id="b8f95-503">These settings provide flexibility.</span></span> <span data-ttu-id="b8f95-504">Vous pouvez modifier hello le traitement par lot de comportement en production sans redéployer le service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="b8f95-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="b8f95-505">Évitez l’exécution parallèle de lots qui s’exécutent sur une seule table dans une base de données unique.</span><span class="sxs-lookup"><span data-stu-id="b8f95-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="b8f95-506">Si vous choisissez toodivide un lot unique sur plusieurs threads de travail, exécutez les tests toodetermine hello nombre idéal de threads.</span><span class="sxs-lookup"><span data-stu-id="b8f95-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="b8f95-507">Après un seuil non spécifié, un plus grand nombre de threads aura pour effet de diminuer les performances au lieu de les augmenter.</span><span class="sxs-lookup"><span data-stu-id="b8f95-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="b8f95-508">Envisagez la mise en mémoire tampon sur la taille et l’heure comme un moyen d’implémenter le traitement par lot pour d’autres scénarios.</span><span class="sxs-lookup"><span data-stu-id="b8f95-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8f95-509">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8f95-509">Next steps</span></span>
<span data-ttu-id="b8f95-510">Cet article consacré à la conception de base de données et les techniques de codage liées toobatching peut améliorer vos performances de l’application et l’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="b8f95-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="b8f95-511">Mais cet aspect ne représente qu’un facteur parmi d’autres dans votre stratégie globale.</span><span class="sxs-lookup"><span data-stu-id="b8f95-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="b8f95-512">Pour plus de performances tooimprove de méthodes et de l’évolutivité, consultez [Guide des performances de base de données SQL Azure pour les bases de données uniques](sql-database-performance-guidance.md) et [considérations de prix et de performances pour un pool élastique](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="b8f95-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

