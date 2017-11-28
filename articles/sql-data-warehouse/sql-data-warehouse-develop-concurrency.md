---
title: "gestion des aaaConcurrency et de la charge de travail dans l’entrepôt de données SQL | Documents Microsoft"
description: "Décrit la gestion de la concurrence et des charges de travail dans Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="2db72-103">Gestion de la concurrence et des charges de travail dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2db72-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="2db72-104">toodeliver des performances prévisibles à grande échelle, Microsoft Azure SQL Data Warehouse vous permet de contrôler les niveaux d’accès concurrentiel et les affectations de ressources mémoire et la priorité de l’UC.</span><span class="sxs-lookup"><span data-stu-id="2db72-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="2db72-105">Cet article vous présente les concepts de toohello de gestion d’accès concurrentiel et la charge de travail, expliquant comment ces deux fonctionnalités ont été implémentées, et comment vous pouvez les contrôler dans votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="2db72-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="2db72-106">Gestion de la charge de travail de l’entrepôt de données SQL est prévue toohelp prend en charge les environnements multi-utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2db72-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="2db72-107">Elle n’est pas destinée aux charges de travail multilocataires.</span><span class="sxs-lookup"><span data-stu-id="2db72-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="2db72-108">Limites de concurrence</span><span class="sxs-lookup"><span data-stu-id="2db72-108">Concurrency limits</span></span>
<span data-ttu-id="2db72-109">Entrepôt de données SQL permet les too1, 024 connexions simultanées.</span><span class="sxs-lookup"><span data-stu-id="2db72-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="2db72-110">Les 1024 connexions peuvent soumettre des requêtes simultanément.</span><span class="sxs-lookup"><span data-stu-id="2db72-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="2db72-111">Débit toooptimize, entrepôt de données SQL peut cependant, file d’attente certaines tooensure de requêtes que chaque requête reçoit une allocation de mémoire minimale.</span><span class="sxs-lookup"><span data-stu-id="2db72-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="2db72-112">La mise en file d’attente se produit lors de l’exécution de la requête.</span><span class="sxs-lookup"><span data-stu-id="2db72-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="2db72-113">Par les files d’attente des requêtes lors de la concurrence limite est atteinte, l’entrepôt de données SQL peut augmenter débit total en vous assurant que les requêtes actives obtiennent accès toocritically nécessaire de ressources mémoire.</span><span class="sxs-lookup"><span data-stu-id="2db72-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="2db72-114">Les limites de concurrence sont régies par deux concepts : les *requêtes simultanées* et les *emplacements de concurrence*.</span><span class="sxs-lookup"><span data-stu-id="2db72-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="2db72-115">Pour une requête tooexecute, il doit s’exécuter au sein de la limite de simultanéité des requêtes hello et de répartition des créneaux hello d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="2db72-116">Requêtes simultanées sont des requêtes hello l’exécution à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="2db72-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="2db72-117">Entrepôt de données SQL prend en charge les requêtes simultanées de too32 sur plus volumineux DWU hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="2db72-118">Les emplacements de concurrence sont alloués en fonction de la DWU.</span><span class="sxs-lookup"><span data-stu-id="2db72-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="2db72-119">Chaque DWU100 fournit 4 emplacements de concurrence.</span><span class="sxs-lookup"><span data-stu-id="2db72-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="2db72-120">Par exemple, une DW100 alloue 4 emplacements de concurrence et une DW1000 en alloue 40.</span><span class="sxs-lookup"><span data-stu-id="2db72-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="2db72-121">Chaque requête consomme un ou plusieurs d’accès concurrentiel des emplacements dépendantes hello [classe de ressource](#resource-classes) de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="2db72-122">Les requêtes s’exécutant dans une classe de ressource smallrc hello consomment un emplacement d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="2db72-123">Les requêtes en cours d’exécution dans une classe de ressource supérieure consomment plusieurs emplacements de concurrence.</span><span class="sxs-lookup"><span data-stu-id="2db72-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="2db72-124">Hello tableau suivant décrit les limites de hello pour les requêtes simultanées et les emplacements d’accès concurrentiel à hello différentes tailles DWU.</span><span class="sxs-lookup"><span data-stu-id="2db72-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="2db72-125">Limites de concurrence</span><span class="sxs-lookup"><span data-stu-id="2db72-125">Concurrency limits</span></span>
| <span data-ttu-id="2db72-126">DWU</span><span class="sxs-lookup"><span data-stu-id="2db72-126">DWU</span></span> | <span data-ttu-id="2db72-127">Nombre maximal de requêtes simultanées</span><span class="sxs-lookup"><span data-stu-id="2db72-127">Max concurrent queries</span></span> | <span data-ttu-id="2db72-128">Emplacements de concurrence alloués</span><span class="sxs-lookup"><span data-stu-id="2db72-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="2db72-129">DW100</span><span class="sxs-lookup"><span data-stu-id="2db72-129">DW100</span></span> |<span data-ttu-id="2db72-130">4</span><span class="sxs-lookup"><span data-stu-id="2db72-130">4</span></span> |<span data-ttu-id="2db72-131">4</span><span class="sxs-lookup"><span data-stu-id="2db72-131">4</span></span> |
| <span data-ttu-id="2db72-132">DW200</span><span class="sxs-lookup"><span data-stu-id="2db72-132">DW200</span></span> |<span data-ttu-id="2db72-133">8</span><span class="sxs-lookup"><span data-stu-id="2db72-133">8</span></span> |<span data-ttu-id="2db72-134">8</span><span class="sxs-lookup"><span data-stu-id="2db72-134">8</span></span> |
| <span data-ttu-id="2db72-135">DW300</span><span class="sxs-lookup"><span data-stu-id="2db72-135">DW300</span></span> |<span data-ttu-id="2db72-136">12</span><span class="sxs-lookup"><span data-stu-id="2db72-136">12</span></span> |<span data-ttu-id="2db72-137">12</span><span class="sxs-lookup"><span data-stu-id="2db72-137">12</span></span> |
| <span data-ttu-id="2db72-138">DW400</span><span class="sxs-lookup"><span data-stu-id="2db72-138">DW400</span></span> |<span data-ttu-id="2db72-139">16</span><span class="sxs-lookup"><span data-stu-id="2db72-139">16</span></span> |<span data-ttu-id="2db72-140">16</span><span class="sxs-lookup"><span data-stu-id="2db72-140">16</span></span> |
| <span data-ttu-id="2db72-141">DW500</span><span class="sxs-lookup"><span data-stu-id="2db72-141">DW500</span></span> |<span data-ttu-id="2db72-142">20</span><span class="sxs-lookup"><span data-stu-id="2db72-142">20</span></span> |<span data-ttu-id="2db72-143">20</span><span class="sxs-lookup"><span data-stu-id="2db72-143">20</span></span> |
| <span data-ttu-id="2db72-144">DW600</span><span class="sxs-lookup"><span data-stu-id="2db72-144">DW600</span></span> |<span data-ttu-id="2db72-145">24</span><span class="sxs-lookup"><span data-stu-id="2db72-145">24</span></span> |<span data-ttu-id="2db72-146">24</span><span class="sxs-lookup"><span data-stu-id="2db72-146">24</span></span> |
| <span data-ttu-id="2db72-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="2db72-147">DW1000</span></span> |<span data-ttu-id="2db72-148">32</span><span class="sxs-lookup"><span data-stu-id="2db72-148">32</span></span> |<span data-ttu-id="2db72-149">40</span><span class="sxs-lookup"><span data-stu-id="2db72-149">40</span></span> |
| <span data-ttu-id="2db72-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="2db72-150">DW1200</span></span> |<span data-ttu-id="2db72-151">32</span><span class="sxs-lookup"><span data-stu-id="2db72-151">32</span></span> |<span data-ttu-id="2db72-152">48</span><span class="sxs-lookup"><span data-stu-id="2db72-152">48</span></span> |
| <span data-ttu-id="2db72-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="2db72-153">DW1500</span></span> |<span data-ttu-id="2db72-154">32</span><span class="sxs-lookup"><span data-stu-id="2db72-154">32</span></span> |<span data-ttu-id="2db72-155">60</span><span class="sxs-lookup"><span data-stu-id="2db72-155">60</span></span> |
| <span data-ttu-id="2db72-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="2db72-156">DW2000</span></span> |<span data-ttu-id="2db72-157">32</span><span class="sxs-lookup"><span data-stu-id="2db72-157">32</span></span> |<span data-ttu-id="2db72-158">80</span><span class="sxs-lookup"><span data-stu-id="2db72-158">80</span></span> |
| <span data-ttu-id="2db72-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="2db72-159">DW3000</span></span> |<span data-ttu-id="2db72-160">32</span><span class="sxs-lookup"><span data-stu-id="2db72-160">32</span></span> |<span data-ttu-id="2db72-161">120</span><span class="sxs-lookup"><span data-stu-id="2db72-161">120</span></span> |
| <span data-ttu-id="2db72-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="2db72-162">DW6000</span></span> |<span data-ttu-id="2db72-163">32</span><span class="sxs-lookup"><span data-stu-id="2db72-163">32</span></span> |<span data-ttu-id="2db72-164">240</span><span class="sxs-lookup"><span data-stu-id="2db72-164">240</span></span> |

<span data-ttu-id="2db72-165">Lorsque l’un de ces seuils est atteint, les nouvelles requêtes sont mises en file d’attente et exécutées sur la base du modèle premier entré, premier sorti.</span><span class="sxs-lookup"><span data-stu-id="2db72-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="2db72-166">Comme des requêtes est terminée et nombre de hello de requêtes et des emplacements tombe en dessous des limites de hello, les requêtes en file d’attente sont libérés.</span><span class="sxs-lookup"><span data-stu-id="2db72-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="2db72-167">*Sélectionnez* requêtes exécution exclusivement sur vues de gestion dynamiques (DMV) ou les vues de catalogue ne sont pas soumis à des limites d’accès concurrentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="2db72-168">Vous pouvez surveiller le système hello, quelle que soit le nombre de hello de requêtes s’exécutant sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="2db72-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="2db72-169">Classes de ressources</span><span class="sxs-lookup"><span data-stu-id="2db72-169">Resource classes</span></span>
<span data-ttu-id="2db72-170">Les classes de ressources vous permettent de contrôler l’allocation de mémoire et les cycles de processeur tooa requête.</span><span class="sxs-lookup"><span data-stu-id="2db72-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="2db72-171">Vous pouvez attribuer deux types d’utilisateur de tooa de classes de ressources sous forme de hello des rôles de base de données.</span><span class="sxs-lookup"><span data-stu-id="2db72-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="2db72-172">Hello deux types de classes de ressources sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2db72-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="2db72-173">Classes de ressources dynamiques (**smallrc, mediumrc, largerc, xlargerc**) allouer une quantité de mémoire en fonction de hello variable DWU actuelle.</span><span class="sxs-lookup"><span data-stu-id="2db72-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="2db72-174">Cela signifie que lorsque vous faites évoluer tooa DWU plus grand, vos requêtes automatiquement obtenir davantage de mémoire.</span><span class="sxs-lookup"><span data-stu-id="2db72-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="2db72-175">Classes de ressources statiques (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allouer hello même quantité de mémoire, indépendamment du hello DWU actuelle (sous réserve que hello DWU lui-même dispose de suffisamment de mémoire).</span><span class="sxs-lookup"><span data-stu-id="2db72-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="2db72-176">Cela signifie que sur les DWU volumineuses, vous pouvez exécuter davantage de requêtes simultanées dans chaque classe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2db72-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="2db72-177">La quantité de mémoire allouée aux utilisateurs de **smallrc** et **staticrc10** étant inférieure, ils peuvent profiter d’une plus grande concurrence.</span><span class="sxs-lookup"><span data-stu-id="2db72-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="2db72-178">En revanche, les utilisateurs affectés trop**xlargerc** ou **staticrc80** reçoivent de grandes quantités de mémoire, et par conséquent, moins de leurs requêtes peuvent s’exécuter simultanément.</span><span class="sxs-lookup"><span data-stu-id="2db72-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="2db72-179">Par défaut, chaque utilisateur est un membre de classe de ressource le plus petit hello, **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="2db72-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="2db72-180">Hello procédure `sp_addrolemember` est utilisé de classe de ressource tooincrease hello, et `sp_droprolemember` est utilisé de classe de ressource toodecrease hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="2db72-181">Par exemple, cette commande augmenterait classe de ressource hello de loaduser trop**largerc**:</span><span class="sxs-lookup"><span data-stu-id="2db72-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="2db72-182">Requêtes qui ne tiennent pas compte des classes de ressources</span><span class="sxs-lookup"><span data-stu-id="2db72-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="2db72-183">Certains types de requêtes ne bénéficient pas d’une allocation de mémoire supérieure.</span><span class="sxs-lookup"><span data-stu-id="2db72-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="2db72-184">système de Hello ignore leur allocation de classe de ressource et toujours exécute ces requêtes dans la classe de ressource le plus petit hello à la place.</span><span class="sxs-lookup"><span data-stu-id="2db72-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="2db72-185">Si ces requêtes s’exécutent toujours dans la classe de ressource le plus petit hello, ils peuvent exécuter lorsque les emplacements d’accès concurrentiel sont sous pression et elles ne consomment des emplacements plus que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2db72-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="2db72-186">Consultez [Exceptions de classe de ressources](#query-exceptions-to-concurrency-limits) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2db72-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="2db72-187">Détails concernant l’affectation des classes de ressources</span><span class="sxs-lookup"><span data-stu-id="2db72-187">Details on resource class assignment</span></span>


<span data-ttu-id="2db72-188">Voici quelques autres détails concernant la classe de ressources :</span><span class="sxs-lookup"><span data-stu-id="2db72-188">A few more details on resource class:</span></span>

* <span data-ttu-id="2db72-189">*Modifier le rôle* l’autorisation est requise classe de ressource hello toochange d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2db72-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="2db72-190">Bien que vous pouvez ajouter un tooone utilisateur ou plusieurs des classes de ressources hello plus élevés, les classes de ressources dynamiques sont prioritaires sur les classes de ressources statiques.</span><span class="sxs-lookup"><span data-stu-id="2db72-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="2db72-191">Autrement dit, si un utilisateur est assigné tooboth **mediumrc**(dynamique) et **staticrc80**(statique), **mediumrc** est la classe de ressource hello est honoré.</span><span class="sxs-lookup"><span data-stu-id="2db72-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="2db72-192">Lorsqu’un utilisateur est affecté toomore que la classe d’une ressource dans un type de classe de ressource spécifique (plus d’une classe de ressource dynamique ou plus d’une classe de ressource statique), la classe de ressource la plus élevée hello est respecté.</span><span class="sxs-lookup"><span data-stu-id="2db72-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="2db72-193">Autrement dit, si un utilisateur est assigné largerc et tooboth mediumrc, la classe de ressource supérieur hello (largerc) est respectée.</span><span class="sxs-lookup"><span data-stu-id="2db72-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="2db72-194">Et si un utilisateur est assigné tooboth **staticrc20** et **statirc80**, **staticrc80** est honoré.</span><span class="sxs-lookup"><span data-stu-id="2db72-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="2db72-195">classe de ressource Hello hello d’administration d’utilisateur du système ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="2db72-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="2db72-196">Pour obtenir un exemple détaillé, consultez [Exemple de modification d’une classe de ressources utilisateur](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="2db72-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="2db72-197">Allocation de mémoire</span><span class="sxs-lookup"><span data-stu-id="2db72-197">Memory allocation</span></span>
<span data-ttu-id="2db72-198">Il existe tooincreasing leurs avantages et inconvénients de classe de ressource d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2db72-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="2db72-199">L’augmentation d’une classe de ressource pour un utilisateur donne leurs requêtes toomore mémoire, ce qui peut signifier que les requêtes s’exécutent plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="2db72-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="2db72-200">Toutefois, les classes de ressources plus élevées également réduisent nombre hello de requêtes simultanées qui peuvent s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="2db72-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="2db72-201">Il s’agit de compromis hello allouer de grandes quantités de requête unique tooa de mémoire ou d’autoriser les autres requêtes, ce qui a également besoin d’allocations de mémoire, toorun simultanément.</span><span class="sxs-lookup"><span data-stu-id="2db72-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="2db72-202">Si un utilisateur se voit accorder haute allocations de mémoire pour une requête, les autres utilisateurs n’auront pas accès toothat toorun mémoire même une requête.</span><span class="sxs-lookup"><span data-stu-id="2db72-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="2db72-203">Hello tableau suivant mappe la mémoire hello allouée tooeach distribution par classe DWU et des ressources.</span><span class="sxs-lookup"><span data-stu-id="2db72-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="2db72-204">Allocations de mémoire par distribution pour les classes de ressources dynamiques (Mo)</span><span class="sxs-lookup"><span data-stu-id="2db72-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="2db72-205">DWU</span><span class="sxs-lookup"><span data-stu-id="2db72-205">DWU</span></span> | <span data-ttu-id="2db72-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="2db72-206">smallrc</span></span> | <span data-ttu-id="2db72-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="2db72-207">mediumrc</span></span> | <span data-ttu-id="2db72-208">largerc</span><span class="sxs-lookup"><span data-stu-id="2db72-208">largerc</span></span> | <span data-ttu-id="2db72-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="2db72-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="2db72-210">DW100</span><span class="sxs-lookup"><span data-stu-id="2db72-210">DW100</span></span> |<span data-ttu-id="2db72-211">100</span><span class="sxs-lookup"><span data-stu-id="2db72-211">100</span></span> |<span data-ttu-id="2db72-212">100</span><span class="sxs-lookup"><span data-stu-id="2db72-212">100</span></span> |<span data-ttu-id="2db72-213">200</span><span class="sxs-lookup"><span data-stu-id="2db72-213">200</span></span> |<span data-ttu-id="2db72-214">400</span><span class="sxs-lookup"><span data-stu-id="2db72-214">400</span></span> |
| <span data-ttu-id="2db72-215">DW200</span><span class="sxs-lookup"><span data-stu-id="2db72-215">DW200</span></span> |<span data-ttu-id="2db72-216">100</span><span class="sxs-lookup"><span data-stu-id="2db72-216">100</span></span> |<span data-ttu-id="2db72-217">200</span><span class="sxs-lookup"><span data-stu-id="2db72-217">200</span></span> |<span data-ttu-id="2db72-218">400</span><span class="sxs-lookup"><span data-stu-id="2db72-218">400</span></span> |<span data-ttu-id="2db72-219">800</span><span class="sxs-lookup"><span data-stu-id="2db72-219">800</span></span> |
| <span data-ttu-id="2db72-220">DW300</span><span class="sxs-lookup"><span data-stu-id="2db72-220">DW300</span></span> |<span data-ttu-id="2db72-221">100</span><span class="sxs-lookup"><span data-stu-id="2db72-221">100</span></span> |<span data-ttu-id="2db72-222">200</span><span class="sxs-lookup"><span data-stu-id="2db72-222">200</span></span> |<span data-ttu-id="2db72-223">400</span><span class="sxs-lookup"><span data-stu-id="2db72-223">400</span></span> |<span data-ttu-id="2db72-224">800</span><span class="sxs-lookup"><span data-stu-id="2db72-224">800</span></span> |
| <span data-ttu-id="2db72-225">DW400</span><span class="sxs-lookup"><span data-stu-id="2db72-225">DW400</span></span> |<span data-ttu-id="2db72-226">100</span><span class="sxs-lookup"><span data-stu-id="2db72-226">100</span></span> |<span data-ttu-id="2db72-227">400</span><span class="sxs-lookup"><span data-stu-id="2db72-227">400</span></span> |<span data-ttu-id="2db72-228">800</span><span class="sxs-lookup"><span data-stu-id="2db72-228">800</span></span> |<span data-ttu-id="2db72-229">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-229">1,600</span></span> |
| <span data-ttu-id="2db72-230">DW500</span><span class="sxs-lookup"><span data-stu-id="2db72-230">DW500</span></span> |<span data-ttu-id="2db72-231">100</span><span class="sxs-lookup"><span data-stu-id="2db72-231">100</span></span> |<span data-ttu-id="2db72-232">400</span><span class="sxs-lookup"><span data-stu-id="2db72-232">400</span></span> |<span data-ttu-id="2db72-233">800</span><span class="sxs-lookup"><span data-stu-id="2db72-233">800</span></span> |<span data-ttu-id="2db72-234">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-234">1,600</span></span> |
| <span data-ttu-id="2db72-235">DW600</span><span class="sxs-lookup"><span data-stu-id="2db72-235">DW600</span></span> |<span data-ttu-id="2db72-236">100</span><span class="sxs-lookup"><span data-stu-id="2db72-236">100</span></span> |<span data-ttu-id="2db72-237">400</span><span class="sxs-lookup"><span data-stu-id="2db72-237">400</span></span> |<span data-ttu-id="2db72-238">800</span><span class="sxs-lookup"><span data-stu-id="2db72-238">800</span></span> |<span data-ttu-id="2db72-239">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-239">1,600</span></span> |
| <span data-ttu-id="2db72-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="2db72-240">DW1000</span></span> |<span data-ttu-id="2db72-241">100</span><span class="sxs-lookup"><span data-stu-id="2db72-241">100</span></span> |<span data-ttu-id="2db72-242">800</span><span class="sxs-lookup"><span data-stu-id="2db72-242">800</span></span> |<span data-ttu-id="2db72-243">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-243">1,600</span></span> |<span data-ttu-id="2db72-244">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-244">3,200</span></span> |
| <span data-ttu-id="2db72-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="2db72-245">DW1200</span></span> |<span data-ttu-id="2db72-246">100</span><span class="sxs-lookup"><span data-stu-id="2db72-246">100</span></span> |<span data-ttu-id="2db72-247">800</span><span class="sxs-lookup"><span data-stu-id="2db72-247">800</span></span> |<span data-ttu-id="2db72-248">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-248">1,600</span></span> |<span data-ttu-id="2db72-249">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-249">3,200</span></span> |
| <span data-ttu-id="2db72-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="2db72-250">DW1500</span></span> |<span data-ttu-id="2db72-251">100</span><span class="sxs-lookup"><span data-stu-id="2db72-251">100</span></span> |<span data-ttu-id="2db72-252">800</span><span class="sxs-lookup"><span data-stu-id="2db72-252">800</span></span> |<span data-ttu-id="2db72-253">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-253">1,600</span></span> |<span data-ttu-id="2db72-254">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-254">3,200</span></span> |
| <span data-ttu-id="2db72-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="2db72-255">DW2000</span></span> |<span data-ttu-id="2db72-256">100</span><span class="sxs-lookup"><span data-stu-id="2db72-256">100</span></span> |<span data-ttu-id="2db72-257">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-257">1,600</span></span> |<span data-ttu-id="2db72-258">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-258">3,200</span></span> |<span data-ttu-id="2db72-259">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-259">6,400</span></span> |
| <span data-ttu-id="2db72-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="2db72-260">DW3000</span></span> |<span data-ttu-id="2db72-261">100</span><span class="sxs-lookup"><span data-stu-id="2db72-261">100</span></span> |<span data-ttu-id="2db72-262">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-262">1,600</span></span> |<span data-ttu-id="2db72-263">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-263">3,200</span></span> |<span data-ttu-id="2db72-264">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-264">6,400</span></span> |
| <span data-ttu-id="2db72-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="2db72-265">DW6000</span></span> |<span data-ttu-id="2db72-266">100</span><span class="sxs-lookup"><span data-stu-id="2db72-266">100</span></span> |<span data-ttu-id="2db72-267">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-267">3,200</span></span> |<span data-ttu-id="2db72-268">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-268">6,400</span></span> |<span data-ttu-id="2db72-269">12 800</span><span class="sxs-lookup"><span data-stu-id="2db72-269">12,800</span></span> |

<span data-ttu-id="2db72-270">Hello tableau suivant mappe la mémoire hello allouée tooeach distribution par DWU et de la classe de ressource statique.</span><span class="sxs-lookup"><span data-stu-id="2db72-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="2db72-271">Notez que les classes de ressources supérieurs hello ont leur mémoire réduit les limites de DWU globales toohonor hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="2db72-272">Allocations de mémoire par distribution pour les classes de ressources statiques (Mo)</span><span class="sxs-lookup"><span data-stu-id="2db72-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="2db72-273">DWU</span><span class="sxs-lookup"><span data-stu-id="2db72-273">DWU</span></span> | <span data-ttu-id="2db72-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="2db72-274">staticrc10</span></span> | <span data-ttu-id="2db72-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="2db72-275">staticrc20</span></span> | <span data-ttu-id="2db72-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="2db72-276">staticrc30</span></span> | <span data-ttu-id="2db72-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="2db72-277">staticrc40</span></span> | <span data-ttu-id="2db72-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="2db72-278">staticrc50</span></span> | <span data-ttu-id="2db72-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="2db72-279">staticrc60</span></span> | <span data-ttu-id="2db72-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="2db72-280">staticrc70</span></span> | <span data-ttu-id="2db72-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="2db72-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2db72-282">DW100</span><span class="sxs-lookup"><span data-stu-id="2db72-282">DW100</span></span> |<span data-ttu-id="2db72-283">100</span><span class="sxs-lookup"><span data-stu-id="2db72-283">100</span></span> |<span data-ttu-id="2db72-284">200</span><span class="sxs-lookup"><span data-stu-id="2db72-284">200</span></span> |<span data-ttu-id="2db72-285">400</span><span class="sxs-lookup"><span data-stu-id="2db72-285">400</span></span> |<span data-ttu-id="2db72-286">400</span><span class="sxs-lookup"><span data-stu-id="2db72-286">400</span></span> |<span data-ttu-id="2db72-287">400</span><span class="sxs-lookup"><span data-stu-id="2db72-287">400</span></span> |<span data-ttu-id="2db72-288">400</span><span class="sxs-lookup"><span data-stu-id="2db72-288">400</span></span> |<span data-ttu-id="2db72-289">400</span><span class="sxs-lookup"><span data-stu-id="2db72-289">400</span></span> |<span data-ttu-id="2db72-290">400</span><span class="sxs-lookup"><span data-stu-id="2db72-290">400</span></span> |
| <span data-ttu-id="2db72-291">DW200</span><span class="sxs-lookup"><span data-stu-id="2db72-291">DW200</span></span> |<span data-ttu-id="2db72-292">100</span><span class="sxs-lookup"><span data-stu-id="2db72-292">100</span></span> |<span data-ttu-id="2db72-293">200</span><span class="sxs-lookup"><span data-stu-id="2db72-293">200</span></span> |<span data-ttu-id="2db72-294">400</span><span class="sxs-lookup"><span data-stu-id="2db72-294">400</span></span> |<span data-ttu-id="2db72-295">800</span><span class="sxs-lookup"><span data-stu-id="2db72-295">800</span></span> |<span data-ttu-id="2db72-296">800</span><span class="sxs-lookup"><span data-stu-id="2db72-296">800</span></span> |<span data-ttu-id="2db72-297">800</span><span class="sxs-lookup"><span data-stu-id="2db72-297">800</span></span> |<span data-ttu-id="2db72-298">800</span><span class="sxs-lookup"><span data-stu-id="2db72-298">800</span></span> |<span data-ttu-id="2db72-299">800</span><span class="sxs-lookup"><span data-stu-id="2db72-299">800</span></span> |
| <span data-ttu-id="2db72-300">DW300</span><span class="sxs-lookup"><span data-stu-id="2db72-300">DW300</span></span> |<span data-ttu-id="2db72-301">100</span><span class="sxs-lookup"><span data-stu-id="2db72-301">100</span></span> |<span data-ttu-id="2db72-302">200</span><span class="sxs-lookup"><span data-stu-id="2db72-302">200</span></span> |<span data-ttu-id="2db72-303">400</span><span class="sxs-lookup"><span data-stu-id="2db72-303">400</span></span> |<span data-ttu-id="2db72-304">800</span><span class="sxs-lookup"><span data-stu-id="2db72-304">800</span></span> |<span data-ttu-id="2db72-305">800</span><span class="sxs-lookup"><span data-stu-id="2db72-305">800</span></span> |<span data-ttu-id="2db72-306">800</span><span class="sxs-lookup"><span data-stu-id="2db72-306">800</span></span> |<span data-ttu-id="2db72-307">800</span><span class="sxs-lookup"><span data-stu-id="2db72-307">800</span></span> |<span data-ttu-id="2db72-308">800</span><span class="sxs-lookup"><span data-stu-id="2db72-308">800</span></span> |
| <span data-ttu-id="2db72-309">DW400</span><span class="sxs-lookup"><span data-stu-id="2db72-309">DW400</span></span> |<span data-ttu-id="2db72-310">100</span><span class="sxs-lookup"><span data-stu-id="2db72-310">100</span></span> |<span data-ttu-id="2db72-311">200</span><span class="sxs-lookup"><span data-stu-id="2db72-311">200</span></span> |<span data-ttu-id="2db72-312">400</span><span class="sxs-lookup"><span data-stu-id="2db72-312">400</span></span> |<span data-ttu-id="2db72-313">800</span><span class="sxs-lookup"><span data-stu-id="2db72-313">800</span></span> |<span data-ttu-id="2db72-314">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-314">1,600</span></span> |<span data-ttu-id="2db72-315">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-315">1,600</span></span> |<span data-ttu-id="2db72-316">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-316">1,600</span></span> |<span data-ttu-id="2db72-317">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-317">1,600</span></span> |
| <span data-ttu-id="2db72-318">DW500</span><span class="sxs-lookup"><span data-stu-id="2db72-318">DW500</span></span> |<span data-ttu-id="2db72-319">100</span><span class="sxs-lookup"><span data-stu-id="2db72-319">100</span></span> |<span data-ttu-id="2db72-320">200</span><span class="sxs-lookup"><span data-stu-id="2db72-320">200</span></span> |<span data-ttu-id="2db72-321">400</span><span class="sxs-lookup"><span data-stu-id="2db72-321">400</span></span> |<span data-ttu-id="2db72-322">800</span><span class="sxs-lookup"><span data-stu-id="2db72-322">800</span></span> |<span data-ttu-id="2db72-323">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-323">1,600</span></span> |<span data-ttu-id="2db72-324">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-324">1,600</span></span> |<span data-ttu-id="2db72-325">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-325">1,600</span></span> |<span data-ttu-id="2db72-326">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-326">1,600</span></span> |
| <span data-ttu-id="2db72-327">DW600</span><span class="sxs-lookup"><span data-stu-id="2db72-327">DW600</span></span> |<span data-ttu-id="2db72-328">100</span><span class="sxs-lookup"><span data-stu-id="2db72-328">100</span></span> |<span data-ttu-id="2db72-329">200</span><span class="sxs-lookup"><span data-stu-id="2db72-329">200</span></span> |<span data-ttu-id="2db72-330">400</span><span class="sxs-lookup"><span data-stu-id="2db72-330">400</span></span> |<span data-ttu-id="2db72-331">800</span><span class="sxs-lookup"><span data-stu-id="2db72-331">800</span></span> |<span data-ttu-id="2db72-332">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-332">1,600</span></span> |<span data-ttu-id="2db72-333">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-333">1,600</span></span> |<span data-ttu-id="2db72-334">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-334">1,600</span></span> |<span data-ttu-id="2db72-335">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-335">1,600</span></span> |
| <span data-ttu-id="2db72-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="2db72-336">DW1000</span></span> |<span data-ttu-id="2db72-337">100</span><span class="sxs-lookup"><span data-stu-id="2db72-337">100</span></span> |<span data-ttu-id="2db72-338">200</span><span class="sxs-lookup"><span data-stu-id="2db72-338">200</span></span> |<span data-ttu-id="2db72-339">400</span><span class="sxs-lookup"><span data-stu-id="2db72-339">400</span></span> |<span data-ttu-id="2db72-340">800</span><span class="sxs-lookup"><span data-stu-id="2db72-340">800</span></span> |<span data-ttu-id="2db72-341">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-341">1,600</span></span> |<span data-ttu-id="2db72-342">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-342">3,200</span></span> |<span data-ttu-id="2db72-343">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-343">3,200</span></span> |<span data-ttu-id="2db72-344">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-344">3,200</span></span> |
| <span data-ttu-id="2db72-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="2db72-345">DW1200</span></span> |<span data-ttu-id="2db72-346">100</span><span class="sxs-lookup"><span data-stu-id="2db72-346">100</span></span> |<span data-ttu-id="2db72-347">200</span><span class="sxs-lookup"><span data-stu-id="2db72-347">200</span></span> |<span data-ttu-id="2db72-348">400</span><span class="sxs-lookup"><span data-stu-id="2db72-348">400</span></span> |<span data-ttu-id="2db72-349">800</span><span class="sxs-lookup"><span data-stu-id="2db72-349">800</span></span> |<span data-ttu-id="2db72-350">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-350">1,600</span></span> |<span data-ttu-id="2db72-351">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-351">3,200</span></span> |<span data-ttu-id="2db72-352">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-352">3,200</span></span> |<span data-ttu-id="2db72-353">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-353">3,200</span></span> |
| <span data-ttu-id="2db72-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="2db72-354">DW1500</span></span> |<span data-ttu-id="2db72-355">100</span><span class="sxs-lookup"><span data-stu-id="2db72-355">100</span></span> |<span data-ttu-id="2db72-356">200</span><span class="sxs-lookup"><span data-stu-id="2db72-356">200</span></span> |<span data-ttu-id="2db72-357">400</span><span class="sxs-lookup"><span data-stu-id="2db72-357">400</span></span> |<span data-ttu-id="2db72-358">800</span><span class="sxs-lookup"><span data-stu-id="2db72-358">800</span></span> |<span data-ttu-id="2db72-359">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-359">1,600</span></span> |<span data-ttu-id="2db72-360">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-360">3,200</span></span> |<span data-ttu-id="2db72-361">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-361">3,200</span></span> |<span data-ttu-id="2db72-362">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-362">3,200</span></span> |
| <span data-ttu-id="2db72-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="2db72-363">DW2000</span></span> |<span data-ttu-id="2db72-364">100</span><span class="sxs-lookup"><span data-stu-id="2db72-364">100</span></span> |<span data-ttu-id="2db72-365">200</span><span class="sxs-lookup"><span data-stu-id="2db72-365">200</span></span> |<span data-ttu-id="2db72-366">400</span><span class="sxs-lookup"><span data-stu-id="2db72-366">400</span></span> |<span data-ttu-id="2db72-367">800</span><span class="sxs-lookup"><span data-stu-id="2db72-367">800</span></span> |<span data-ttu-id="2db72-368">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-368">1,600</span></span> |<span data-ttu-id="2db72-369">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-369">3,200</span></span> |<span data-ttu-id="2db72-370">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-370">6,400</span></span> |<span data-ttu-id="2db72-371">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-371">6,400</span></span> |
| <span data-ttu-id="2db72-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="2db72-372">DW3000</span></span> |<span data-ttu-id="2db72-373">100</span><span class="sxs-lookup"><span data-stu-id="2db72-373">100</span></span> |<span data-ttu-id="2db72-374">200</span><span class="sxs-lookup"><span data-stu-id="2db72-374">200</span></span> |<span data-ttu-id="2db72-375">400</span><span class="sxs-lookup"><span data-stu-id="2db72-375">400</span></span> |<span data-ttu-id="2db72-376">800</span><span class="sxs-lookup"><span data-stu-id="2db72-376">800</span></span> |<span data-ttu-id="2db72-377">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-377">1,600</span></span> |<span data-ttu-id="2db72-378">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-378">3,200</span></span> |<span data-ttu-id="2db72-379">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-379">6,400</span></span> |<span data-ttu-id="2db72-380">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-380">6,400</span></span> |
| <span data-ttu-id="2db72-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="2db72-381">DW6000</span></span> |<span data-ttu-id="2db72-382">100</span><span class="sxs-lookup"><span data-stu-id="2db72-382">100</span></span> |<span data-ttu-id="2db72-383">200</span><span class="sxs-lookup"><span data-stu-id="2db72-383">200</span></span> |<span data-ttu-id="2db72-384">400</span><span class="sxs-lookup"><span data-stu-id="2db72-384">400</span></span> |<span data-ttu-id="2db72-385">800</span><span class="sxs-lookup"><span data-stu-id="2db72-385">800</span></span> |<span data-ttu-id="2db72-386">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-386">1,600</span></span> |<span data-ttu-id="2db72-387">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-387">3,200</span></span> |<span data-ttu-id="2db72-388">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-388">6,400</span></span> |<span data-ttu-id="2db72-389">12 800</span><span class="sxs-lookup"><span data-stu-id="2db72-389">12,800</span></span> |

<span data-ttu-id="2db72-390">À partir de hello tableau précédent, vous pouvez voir qu’une requête en cours d’exécution sur un DW2000 Bonjour **xlargerc** classe de ressource aurait accès too6, 400 Mo de mémoire dans chacune des bases de données distribuées hello 60.</span><span class="sxs-lookup"><span data-stu-id="2db72-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="2db72-391">Dans SQL Data Warehouse, il existe 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="2db72-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="2db72-392">Par conséquent, l’allocation de mémoire totale toocalculate hello pour une requête dans une classe de ressource donné, le hello au-dessus des valeurs doit être multipliée par 60.</span><span class="sxs-lookup"><span data-stu-id="2db72-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="2db72-393">Allocations de mémoire à l’échelle du système (Go)</span><span class="sxs-lookup"><span data-stu-id="2db72-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="2db72-394">DWU</span><span class="sxs-lookup"><span data-stu-id="2db72-394">DWU</span></span> | <span data-ttu-id="2db72-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="2db72-395">smallrc</span></span> | <span data-ttu-id="2db72-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="2db72-396">mediumrc</span></span> | <span data-ttu-id="2db72-397">largerc</span><span class="sxs-lookup"><span data-stu-id="2db72-397">largerc</span></span> | <span data-ttu-id="2db72-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="2db72-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="2db72-399">DW100</span><span class="sxs-lookup"><span data-stu-id="2db72-399">DW100</span></span> |<span data-ttu-id="2db72-400">6</span><span class="sxs-lookup"><span data-stu-id="2db72-400">6</span></span> |<span data-ttu-id="2db72-401">6</span><span class="sxs-lookup"><span data-stu-id="2db72-401">6</span></span> |<span data-ttu-id="2db72-402">12</span><span class="sxs-lookup"><span data-stu-id="2db72-402">12</span></span> |<span data-ttu-id="2db72-403">23</span><span class="sxs-lookup"><span data-stu-id="2db72-403">23</span></span> |
| <span data-ttu-id="2db72-404">DW200</span><span class="sxs-lookup"><span data-stu-id="2db72-404">DW200</span></span> |<span data-ttu-id="2db72-405">6</span><span class="sxs-lookup"><span data-stu-id="2db72-405">6</span></span> |<span data-ttu-id="2db72-406">12</span><span class="sxs-lookup"><span data-stu-id="2db72-406">12</span></span> |<span data-ttu-id="2db72-407">23</span><span class="sxs-lookup"><span data-stu-id="2db72-407">23</span></span> |<span data-ttu-id="2db72-408">47</span><span class="sxs-lookup"><span data-stu-id="2db72-408">47</span></span> |
| <span data-ttu-id="2db72-409">DW300</span><span class="sxs-lookup"><span data-stu-id="2db72-409">DW300</span></span> |<span data-ttu-id="2db72-410">6</span><span class="sxs-lookup"><span data-stu-id="2db72-410">6</span></span> |<span data-ttu-id="2db72-411">12</span><span class="sxs-lookup"><span data-stu-id="2db72-411">12</span></span> |<span data-ttu-id="2db72-412">23</span><span class="sxs-lookup"><span data-stu-id="2db72-412">23</span></span> |<span data-ttu-id="2db72-413">47</span><span class="sxs-lookup"><span data-stu-id="2db72-413">47</span></span> |
| <span data-ttu-id="2db72-414">DW400</span><span class="sxs-lookup"><span data-stu-id="2db72-414">DW400</span></span> |<span data-ttu-id="2db72-415">6</span><span class="sxs-lookup"><span data-stu-id="2db72-415">6</span></span> |<span data-ttu-id="2db72-416">23</span><span class="sxs-lookup"><span data-stu-id="2db72-416">23</span></span> |<span data-ttu-id="2db72-417">47</span><span class="sxs-lookup"><span data-stu-id="2db72-417">47</span></span> |<span data-ttu-id="2db72-418">94</span><span class="sxs-lookup"><span data-stu-id="2db72-418">94</span></span> |
| <span data-ttu-id="2db72-419">DW500</span><span class="sxs-lookup"><span data-stu-id="2db72-419">DW500</span></span> |<span data-ttu-id="2db72-420">6</span><span class="sxs-lookup"><span data-stu-id="2db72-420">6</span></span> |<span data-ttu-id="2db72-421">23</span><span class="sxs-lookup"><span data-stu-id="2db72-421">23</span></span> |<span data-ttu-id="2db72-422">47</span><span class="sxs-lookup"><span data-stu-id="2db72-422">47</span></span> |<span data-ttu-id="2db72-423">94</span><span class="sxs-lookup"><span data-stu-id="2db72-423">94</span></span> |
| <span data-ttu-id="2db72-424">DW600</span><span class="sxs-lookup"><span data-stu-id="2db72-424">DW600</span></span> |<span data-ttu-id="2db72-425">6</span><span class="sxs-lookup"><span data-stu-id="2db72-425">6</span></span> |<span data-ttu-id="2db72-426">23</span><span class="sxs-lookup"><span data-stu-id="2db72-426">23</span></span> |<span data-ttu-id="2db72-427">47</span><span class="sxs-lookup"><span data-stu-id="2db72-427">47</span></span> |<span data-ttu-id="2db72-428">94</span><span class="sxs-lookup"><span data-stu-id="2db72-428">94</span></span> |
| <span data-ttu-id="2db72-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="2db72-429">DW1000</span></span> |<span data-ttu-id="2db72-430">6</span><span class="sxs-lookup"><span data-stu-id="2db72-430">6</span></span> |<span data-ttu-id="2db72-431">47</span><span class="sxs-lookup"><span data-stu-id="2db72-431">47</span></span> |<span data-ttu-id="2db72-432">94</span><span class="sxs-lookup"><span data-stu-id="2db72-432">94</span></span> |<span data-ttu-id="2db72-433">188</span><span class="sxs-lookup"><span data-stu-id="2db72-433">188</span></span> |
| <span data-ttu-id="2db72-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="2db72-434">DW1200</span></span> |<span data-ttu-id="2db72-435">6</span><span class="sxs-lookup"><span data-stu-id="2db72-435">6</span></span> |<span data-ttu-id="2db72-436">47</span><span class="sxs-lookup"><span data-stu-id="2db72-436">47</span></span> |<span data-ttu-id="2db72-437">94</span><span class="sxs-lookup"><span data-stu-id="2db72-437">94</span></span> |<span data-ttu-id="2db72-438">188</span><span class="sxs-lookup"><span data-stu-id="2db72-438">188</span></span> |
| <span data-ttu-id="2db72-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="2db72-439">DW1500</span></span> |<span data-ttu-id="2db72-440">6</span><span class="sxs-lookup"><span data-stu-id="2db72-440">6</span></span> |<span data-ttu-id="2db72-441">47</span><span class="sxs-lookup"><span data-stu-id="2db72-441">47</span></span> |<span data-ttu-id="2db72-442">94</span><span class="sxs-lookup"><span data-stu-id="2db72-442">94</span></span> |<span data-ttu-id="2db72-443">188</span><span class="sxs-lookup"><span data-stu-id="2db72-443">188</span></span> |
| <span data-ttu-id="2db72-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="2db72-444">DW2000</span></span> |<span data-ttu-id="2db72-445">6</span><span class="sxs-lookup"><span data-stu-id="2db72-445">6</span></span> |<span data-ttu-id="2db72-446">94</span><span class="sxs-lookup"><span data-stu-id="2db72-446">94</span></span> |<span data-ttu-id="2db72-447">188</span><span class="sxs-lookup"><span data-stu-id="2db72-447">188</span></span> |<span data-ttu-id="2db72-448">375</span><span class="sxs-lookup"><span data-stu-id="2db72-448">375</span></span> |
| <span data-ttu-id="2db72-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="2db72-449">DW3000</span></span> |<span data-ttu-id="2db72-450">6</span><span class="sxs-lookup"><span data-stu-id="2db72-450">6</span></span> |<span data-ttu-id="2db72-451">94</span><span class="sxs-lookup"><span data-stu-id="2db72-451">94</span></span> |<span data-ttu-id="2db72-452">188</span><span class="sxs-lookup"><span data-stu-id="2db72-452">188</span></span> |<span data-ttu-id="2db72-453">375</span><span class="sxs-lookup"><span data-stu-id="2db72-453">375</span></span> |
| <span data-ttu-id="2db72-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="2db72-454">DW6000</span></span> |<span data-ttu-id="2db72-455">6</span><span class="sxs-lookup"><span data-stu-id="2db72-455">6</span></span> |<span data-ttu-id="2db72-456">188</span><span class="sxs-lookup"><span data-stu-id="2db72-456">188</span></span> |<span data-ttu-id="2db72-457">375</span><span class="sxs-lookup"><span data-stu-id="2db72-457">375</span></span> |<span data-ttu-id="2db72-458">750</span><span class="sxs-lookup"><span data-stu-id="2db72-458">750</span></span> |

<span data-ttu-id="2db72-459">À partir de cette table d’allocations de mémoire système, vous pouvez voir qu’une requête en cours d’exécution sur un DW2000 dans la classe de ressource xlargerc hello est allouée à un total de 375 Go de mémoire (distributions de 6 400 Mo * 60 / 1 024 tooconvert tooGB) sur l’intégralité de hello de votre entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2db72-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="2db72-460">Hello même calcul s’applique toostatic des classes de ressources.</span><span class="sxs-lookup"><span data-stu-id="2db72-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="2db72-461">Consommation des emplacements de concurrence</span><span class="sxs-lookup"><span data-stu-id="2db72-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="2db72-462">SQL Data Warehouse accorde plus tooqueries de mémoire en cours d’exécution dans les classes de ressources plus élevées.</span><span class="sxs-lookup"><span data-stu-id="2db72-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="2db72-463">La mémoire est une ressource fixe.</span><span class="sxs-lookup"><span data-stu-id="2db72-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="2db72-464">Par conséquent, hello davantage de mémoire allouée par requête, hello moins de requêtes simultanées peuvent exécuter.</span><span class="sxs-lookup"><span data-stu-id="2db72-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="2db72-465">Hello tableau suivant réitère tous les concepts de précédente hello dans une seule vue qui affiche le nombre de hello d’emplacements d’accès concurrentiel disponibles par DWU et emplacements hello consommées par chaque classe de ressource.</span><span class="sxs-lookup"><span data-stu-id="2db72-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="2db72-466">Allocation et consommation des emplacements de concurrence pour les classes de ressources dynamiques</span><span class="sxs-lookup"><span data-stu-id="2db72-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="2db72-467">DWU</span><span class="sxs-lookup"><span data-stu-id="2db72-467">DWU</span></span> | <span data-ttu-id="2db72-468">Nombre maximal de requêtes concurrentes</span><span class="sxs-lookup"><span data-stu-id="2db72-468">Maximum concurrent queries</span></span> | <span data-ttu-id="2db72-469">Emplacements de concurrence alloués</span><span class="sxs-lookup"><span data-stu-id="2db72-469">Concurrency slots allocated</span></span> | <span data-ttu-id="2db72-470">Emplacements utilisés par smallrc</span><span class="sxs-lookup"><span data-stu-id="2db72-470">Slots used by smallrc</span></span> | <span data-ttu-id="2db72-471">Emplacements utilisés par mediumrc</span><span class="sxs-lookup"><span data-stu-id="2db72-471">Slots used by mediumrc</span></span> | <span data-ttu-id="2db72-472">Emplacements utilisés par largerc</span><span class="sxs-lookup"><span data-stu-id="2db72-472">Slots used by largerc</span></span> | <span data-ttu-id="2db72-473">Emplacements utilisés par xlargerc</span><span class="sxs-lookup"><span data-stu-id="2db72-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2db72-474">DW100</span><span class="sxs-lookup"><span data-stu-id="2db72-474">DW100</span></span> |<span data-ttu-id="2db72-475">4</span><span class="sxs-lookup"><span data-stu-id="2db72-475">4</span></span> |<span data-ttu-id="2db72-476">4</span><span class="sxs-lookup"><span data-stu-id="2db72-476">4</span></span> |<span data-ttu-id="2db72-477">1</span><span class="sxs-lookup"><span data-stu-id="2db72-477">1</span></span> |<span data-ttu-id="2db72-478">1</span><span class="sxs-lookup"><span data-stu-id="2db72-478">1</span></span> |<span data-ttu-id="2db72-479">2</span><span class="sxs-lookup"><span data-stu-id="2db72-479">2</span></span> |<span data-ttu-id="2db72-480">4</span><span class="sxs-lookup"><span data-stu-id="2db72-480">4</span></span> |
| <span data-ttu-id="2db72-481">DW200</span><span class="sxs-lookup"><span data-stu-id="2db72-481">DW200</span></span> |<span data-ttu-id="2db72-482">8</span><span class="sxs-lookup"><span data-stu-id="2db72-482">8</span></span> |<span data-ttu-id="2db72-483">8</span><span class="sxs-lookup"><span data-stu-id="2db72-483">8</span></span> |<span data-ttu-id="2db72-484">1</span><span class="sxs-lookup"><span data-stu-id="2db72-484">1</span></span> |<span data-ttu-id="2db72-485">2</span><span class="sxs-lookup"><span data-stu-id="2db72-485">2</span></span> |<span data-ttu-id="2db72-486">4</span><span class="sxs-lookup"><span data-stu-id="2db72-486">4</span></span> |<span data-ttu-id="2db72-487">8</span><span class="sxs-lookup"><span data-stu-id="2db72-487">8</span></span> |
| <span data-ttu-id="2db72-488">DW300</span><span class="sxs-lookup"><span data-stu-id="2db72-488">DW300</span></span> |<span data-ttu-id="2db72-489">12</span><span class="sxs-lookup"><span data-stu-id="2db72-489">12</span></span> |<span data-ttu-id="2db72-490">12</span><span class="sxs-lookup"><span data-stu-id="2db72-490">12</span></span> |<span data-ttu-id="2db72-491">1</span><span class="sxs-lookup"><span data-stu-id="2db72-491">1</span></span> |<span data-ttu-id="2db72-492">2</span><span class="sxs-lookup"><span data-stu-id="2db72-492">2</span></span> |<span data-ttu-id="2db72-493">4</span><span class="sxs-lookup"><span data-stu-id="2db72-493">4</span></span> |<span data-ttu-id="2db72-494">8</span><span class="sxs-lookup"><span data-stu-id="2db72-494">8</span></span> |
| <span data-ttu-id="2db72-495">DW400</span><span class="sxs-lookup"><span data-stu-id="2db72-495">DW400</span></span> |<span data-ttu-id="2db72-496">16</span><span class="sxs-lookup"><span data-stu-id="2db72-496">16</span></span> |<span data-ttu-id="2db72-497">16</span><span class="sxs-lookup"><span data-stu-id="2db72-497">16</span></span> |<span data-ttu-id="2db72-498">1</span><span class="sxs-lookup"><span data-stu-id="2db72-498">1</span></span> |<span data-ttu-id="2db72-499">4</span><span class="sxs-lookup"><span data-stu-id="2db72-499">4</span></span> |<span data-ttu-id="2db72-500">8</span><span class="sxs-lookup"><span data-stu-id="2db72-500">8</span></span> |<span data-ttu-id="2db72-501">16</span><span class="sxs-lookup"><span data-stu-id="2db72-501">16</span></span> |
| <span data-ttu-id="2db72-502">DW500</span><span class="sxs-lookup"><span data-stu-id="2db72-502">DW500</span></span> |<span data-ttu-id="2db72-503">20</span><span class="sxs-lookup"><span data-stu-id="2db72-503">20</span></span> |<span data-ttu-id="2db72-504">20</span><span class="sxs-lookup"><span data-stu-id="2db72-504">20</span></span> |<span data-ttu-id="2db72-505">1</span><span class="sxs-lookup"><span data-stu-id="2db72-505">1</span></span> |<span data-ttu-id="2db72-506">4</span><span class="sxs-lookup"><span data-stu-id="2db72-506">4</span></span> |<span data-ttu-id="2db72-507">8</span><span class="sxs-lookup"><span data-stu-id="2db72-507">8</span></span> |<span data-ttu-id="2db72-508">16</span><span class="sxs-lookup"><span data-stu-id="2db72-508">16</span></span> |
| <span data-ttu-id="2db72-509">DW600</span><span class="sxs-lookup"><span data-stu-id="2db72-509">DW600</span></span> |<span data-ttu-id="2db72-510">24</span><span class="sxs-lookup"><span data-stu-id="2db72-510">24</span></span> |<span data-ttu-id="2db72-511">24</span><span class="sxs-lookup"><span data-stu-id="2db72-511">24</span></span> |<span data-ttu-id="2db72-512">1</span><span class="sxs-lookup"><span data-stu-id="2db72-512">1</span></span> |<span data-ttu-id="2db72-513">4</span><span class="sxs-lookup"><span data-stu-id="2db72-513">4</span></span> |<span data-ttu-id="2db72-514">8</span><span class="sxs-lookup"><span data-stu-id="2db72-514">8</span></span> |<span data-ttu-id="2db72-515">16</span><span class="sxs-lookup"><span data-stu-id="2db72-515">16</span></span> |
| <span data-ttu-id="2db72-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="2db72-516">DW1000</span></span> |<span data-ttu-id="2db72-517">32</span><span class="sxs-lookup"><span data-stu-id="2db72-517">32</span></span> |<span data-ttu-id="2db72-518">40</span><span class="sxs-lookup"><span data-stu-id="2db72-518">40</span></span> |<span data-ttu-id="2db72-519">1</span><span class="sxs-lookup"><span data-stu-id="2db72-519">1</span></span> |<span data-ttu-id="2db72-520">8</span><span class="sxs-lookup"><span data-stu-id="2db72-520">8</span></span> |<span data-ttu-id="2db72-521">16</span><span class="sxs-lookup"><span data-stu-id="2db72-521">16</span></span> |<span data-ttu-id="2db72-522">32</span><span class="sxs-lookup"><span data-stu-id="2db72-522">32</span></span> |
| <span data-ttu-id="2db72-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="2db72-523">DW1200</span></span> |<span data-ttu-id="2db72-524">32</span><span class="sxs-lookup"><span data-stu-id="2db72-524">32</span></span> |<span data-ttu-id="2db72-525">48</span><span class="sxs-lookup"><span data-stu-id="2db72-525">48</span></span> |<span data-ttu-id="2db72-526">1</span><span class="sxs-lookup"><span data-stu-id="2db72-526">1</span></span> |<span data-ttu-id="2db72-527">8</span><span class="sxs-lookup"><span data-stu-id="2db72-527">8</span></span> |<span data-ttu-id="2db72-528">16</span><span class="sxs-lookup"><span data-stu-id="2db72-528">16</span></span> |<span data-ttu-id="2db72-529">32</span><span class="sxs-lookup"><span data-stu-id="2db72-529">32</span></span> |
| <span data-ttu-id="2db72-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="2db72-530">DW1500</span></span> |<span data-ttu-id="2db72-531">32</span><span class="sxs-lookup"><span data-stu-id="2db72-531">32</span></span> |<span data-ttu-id="2db72-532">60</span><span class="sxs-lookup"><span data-stu-id="2db72-532">60</span></span> |<span data-ttu-id="2db72-533">1</span><span class="sxs-lookup"><span data-stu-id="2db72-533">1</span></span> |<span data-ttu-id="2db72-534">8</span><span class="sxs-lookup"><span data-stu-id="2db72-534">8</span></span> |<span data-ttu-id="2db72-535">16</span><span class="sxs-lookup"><span data-stu-id="2db72-535">16</span></span> |<span data-ttu-id="2db72-536">32</span><span class="sxs-lookup"><span data-stu-id="2db72-536">32</span></span> |
| <span data-ttu-id="2db72-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="2db72-537">DW2000</span></span> |<span data-ttu-id="2db72-538">32</span><span class="sxs-lookup"><span data-stu-id="2db72-538">32</span></span> |<span data-ttu-id="2db72-539">80</span><span class="sxs-lookup"><span data-stu-id="2db72-539">80</span></span> |<span data-ttu-id="2db72-540">1</span><span class="sxs-lookup"><span data-stu-id="2db72-540">1</span></span> |<span data-ttu-id="2db72-541">16</span><span class="sxs-lookup"><span data-stu-id="2db72-541">16</span></span> |<span data-ttu-id="2db72-542">32</span><span class="sxs-lookup"><span data-stu-id="2db72-542">32</span></span> |<span data-ttu-id="2db72-543">64</span><span class="sxs-lookup"><span data-stu-id="2db72-543">64</span></span> |
| <span data-ttu-id="2db72-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="2db72-544">DW3000</span></span> |<span data-ttu-id="2db72-545">32</span><span class="sxs-lookup"><span data-stu-id="2db72-545">32</span></span> |<span data-ttu-id="2db72-546">120</span><span class="sxs-lookup"><span data-stu-id="2db72-546">120</span></span> |<span data-ttu-id="2db72-547">1</span><span class="sxs-lookup"><span data-stu-id="2db72-547">1</span></span> |<span data-ttu-id="2db72-548">16</span><span class="sxs-lookup"><span data-stu-id="2db72-548">16</span></span> |<span data-ttu-id="2db72-549">32</span><span class="sxs-lookup"><span data-stu-id="2db72-549">32</span></span> |<span data-ttu-id="2db72-550">64</span><span class="sxs-lookup"><span data-stu-id="2db72-550">64</span></span> |
| <span data-ttu-id="2db72-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="2db72-551">DW6000</span></span> |<span data-ttu-id="2db72-552">32</span><span class="sxs-lookup"><span data-stu-id="2db72-552">32</span></span> |<span data-ttu-id="2db72-553">240</span><span class="sxs-lookup"><span data-stu-id="2db72-553">240</span></span> |<span data-ttu-id="2db72-554">1</span><span class="sxs-lookup"><span data-stu-id="2db72-554">1</span></span> |<span data-ttu-id="2db72-555">32</span><span class="sxs-lookup"><span data-stu-id="2db72-555">32</span></span> |<span data-ttu-id="2db72-556">64</span><span class="sxs-lookup"><span data-stu-id="2db72-556">64</span></span> |<span data-ttu-id="2db72-557">128</span><span class="sxs-lookup"><span data-stu-id="2db72-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="2db72-558">Allocation et consommation des emplacements de concurrence pour les classes de ressources statiques</span><span class="sxs-lookup"><span data-stu-id="2db72-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="2db72-559">DWU</span><span class="sxs-lookup"><span data-stu-id="2db72-559">DWU</span></span> | <span data-ttu-id="2db72-560">Nombre maximal de requêtes concurrentes</span><span class="sxs-lookup"><span data-stu-id="2db72-560">Maximum concurrent queries</span></span> | <span data-ttu-id="2db72-561">Emplacements de concurrence alloués</span><span class="sxs-lookup"><span data-stu-id="2db72-561">Concurrency slots allocated</span></span> |<span data-ttu-id="2db72-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="2db72-562">staticrc10</span></span> | <span data-ttu-id="2db72-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="2db72-563">staticrc20</span></span> | <span data-ttu-id="2db72-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="2db72-564">staticrc30</span></span> | <span data-ttu-id="2db72-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="2db72-565">staticrc40</span></span> | <span data-ttu-id="2db72-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="2db72-566">staticrc50</span></span> | <span data-ttu-id="2db72-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="2db72-567">staticrc60</span></span> | <span data-ttu-id="2db72-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="2db72-568">staticrc70</span></span> | <span data-ttu-id="2db72-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="2db72-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2db72-570">DW100</span><span class="sxs-lookup"><span data-stu-id="2db72-570">DW100</span></span> |<span data-ttu-id="2db72-571">4</span><span class="sxs-lookup"><span data-stu-id="2db72-571">4</span></span> |<span data-ttu-id="2db72-572">4</span><span class="sxs-lookup"><span data-stu-id="2db72-572">4</span></span> |<span data-ttu-id="2db72-573">1</span><span class="sxs-lookup"><span data-stu-id="2db72-573">1</span></span> |<span data-ttu-id="2db72-574">2</span><span class="sxs-lookup"><span data-stu-id="2db72-574">2</span></span> |<span data-ttu-id="2db72-575">4</span><span class="sxs-lookup"><span data-stu-id="2db72-575">4</span></span> |<span data-ttu-id="2db72-576">4</span><span class="sxs-lookup"><span data-stu-id="2db72-576">4</span></span> |<span data-ttu-id="2db72-577">4</span><span class="sxs-lookup"><span data-stu-id="2db72-577">4</span></span> |<span data-ttu-id="2db72-578">4</span><span class="sxs-lookup"><span data-stu-id="2db72-578">4</span></span> |<span data-ttu-id="2db72-579">4</span><span class="sxs-lookup"><span data-stu-id="2db72-579">4</span></span> |<span data-ttu-id="2db72-580">4</span><span class="sxs-lookup"><span data-stu-id="2db72-580">4</span></span> |
| <span data-ttu-id="2db72-581">DW200</span><span class="sxs-lookup"><span data-stu-id="2db72-581">DW200</span></span> |<span data-ttu-id="2db72-582">8</span><span class="sxs-lookup"><span data-stu-id="2db72-582">8</span></span> |<span data-ttu-id="2db72-583">8</span><span class="sxs-lookup"><span data-stu-id="2db72-583">8</span></span> |<span data-ttu-id="2db72-584">1</span><span class="sxs-lookup"><span data-stu-id="2db72-584">1</span></span> |<span data-ttu-id="2db72-585">2</span><span class="sxs-lookup"><span data-stu-id="2db72-585">2</span></span> |<span data-ttu-id="2db72-586">4</span><span class="sxs-lookup"><span data-stu-id="2db72-586">4</span></span> |<span data-ttu-id="2db72-587">8</span><span class="sxs-lookup"><span data-stu-id="2db72-587">8</span></span> |<span data-ttu-id="2db72-588">8</span><span class="sxs-lookup"><span data-stu-id="2db72-588">8</span></span> |<span data-ttu-id="2db72-589">8</span><span class="sxs-lookup"><span data-stu-id="2db72-589">8</span></span> |<span data-ttu-id="2db72-590">8</span><span class="sxs-lookup"><span data-stu-id="2db72-590">8</span></span> |<span data-ttu-id="2db72-591">8</span><span class="sxs-lookup"><span data-stu-id="2db72-591">8</span></span> |
| <span data-ttu-id="2db72-592">DW300</span><span class="sxs-lookup"><span data-stu-id="2db72-592">DW300</span></span> |<span data-ttu-id="2db72-593">12</span><span class="sxs-lookup"><span data-stu-id="2db72-593">12</span></span> |<span data-ttu-id="2db72-594">12</span><span class="sxs-lookup"><span data-stu-id="2db72-594">12</span></span> |<span data-ttu-id="2db72-595">1</span><span class="sxs-lookup"><span data-stu-id="2db72-595">1</span></span> |<span data-ttu-id="2db72-596">2</span><span class="sxs-lookup"><span data-stu-id="2db72-596">2</span></span> |<span data-ttu-id="2db72-597">4</span><span class="sxs-lookup"><span data-stu-id="2db72-597">4</span></span> |<span data-ttu-id="2db72-598">8</span><span class="sxs-lookup"><span data-stu-id="2db72-598">8</span></span> |<span data-ttu-id="2db72-599">8</span><span class="sxs-lookup"><span data-stu-id="2db72-599">8</span></span> |<span data-ttu-id="2db72-600">8</span><span class="sxs-lookup"><span data-stu-id="2db72-600">8</span></span> |<span data-ttu-id="2db72-601">8</span><span class="sxs-lookup"><span data-stu-id="2db72-601">8</span></span> |<span data-ttu-id="2db72-602">8</span><span class="sxs-lookup"><span data-stu-id="2db72-602">8</span></span> |
| <span data-ttu-id="2db72-603">DW400</span><span class="sxs-lookup"><span data-stu-id="2db72-603">DW400</span></span> |<span data-ttu-id="2db72-604">16</span><span class="sxs-lookup"><span data-stu-id="2db72-604">16</span></span> |<span data-ttu-id="2db72-605">16</span><span class="sxs-lookup"><span data-stu-id="2db72-605">16</span></span> |<span data-ttu-id="2db72-606">1</span><span class="sxs-lookup"><span data-stu-id="2db72-606">1</span></span> |<span data-ttu-id="2db72-607">2</span><span class="sxs-lookup"><span data-stu-id="2db72-607">2</span></span> |<span data-ttu-id="2db72-608">4</span><span class="sxs-lookup"><span data-stu-id="2db72-608">4</span></span> |<span data-ttu-id="2db72-609">8</span><span class="sxs-lookup"><span data-stu-id="2db72-609">8</span></span> |<span data-ttu-id="2db72-610">16</span><span class="sxs-lookup"><span data-stu-id="2db72-610">16</span></span> |<span data-ttu-id="2db72-611">16</span><span class="sxs-lookup"><span data-stu-id="2db72-611">16</span></span> |<span data-ttu-id="2db72-612">16</span><span class="sxs-lookup"><span data-stu-id="2db72-612">16</span></span> |<span data-ttu-id="2db72-613">16</span><span class="sxs-lookup"><span data-stu-id="2db72-613">16</span></span> |
| <span data-ttu-id="2db72-614">DW500</span><span class="sxs-lookup"><span data-stu-id="2db72-614">DW500</span></span> | <span data-ttu-id="2db72-615">20</span><span class="sxs-lookup"><span data-stu-id="2db72-615">20</span></span>| <span data-ttu-id="2db72-616">20</span><span class="sxs-lookup"><span data-stu-id="2db72-616">20</span></span>| <span data-ttu-id="2db72-617">1</span><span class="sxs-lookup"><span data-stu-id="2db72-617">1</span></span>| <span data-ttu-id="2db72-618">2</span><span class="sxs-lookup"><span data-stu-id="2db72-618">2</span></span>| <span data-ttu-id="2db72-619">4</span><span class="sxs-lookup"><span data-stu-id="2db72-619">4</span></span>| <span data-ttu-id="2db72-620">8</span><span class="sxs-lookup"><span data-stu-id="2db72-620">8</span></span>| <span data-ttu-id="2db72-621">16</span><span class="sxs-lookup"><span data-stu-id="2db72-621">16</span></span>| <span data-ttu-id="2db72-622">16</span><span class="sxs-lookup"><span data-stu-id="2db72-622">16</span></span>| <span data-ttu-id="2db72-623">16</span><span class="sxs-lookup"><span data-stu-id="2db72-623">16</span></span>| <span data-ttu-id="2db72-624">16</span><span class="sxs-lookup"><span data-stu-id="2db72-624">16</span></span>|
| <span data-ttu-id="2db72-625">DW600</span><span class="sxs-lookup"><span data-stu-id="2db72-625">DW600</span></span> | <span data-ttu-id="2db72-626">24</span><span class="sxs-lookup"><span data-stu-id="2db72-626">24</span></span>| <span data-ttu-id="2db72-627">24</span><span class="sxs-lookup"><span data-stu-id="2db72-627">24</span></span>| <span data-ttu-id="2db72-628">1</span><span class="sxs-lookup"><span data-stu-id="2db72-628">1</span></span>| <span data-ttu-id="2db72-629">2</span><span class="sxs-lookup"><span data-stu-id="2db72-629">2</span></span>| <span data-ttu-id="2db72-630">4</span><span class="sxs-lookup"><span data-stu-id="2db72-630">4</span></span>| <span data-ttu-id="2db72-631">8</span><span class="sxs-lookup"><span data-stu-id="2db72-631">8</span></span>| <span data-ttu-id="2db72-632">16</span><span class="sxs-lookup"><span data-stu-id="2db72-632">16</span></span>| <span data-ttu-id="2db72-633">16</span><span class="sxs-lookup"><span data-stu-id="2db72-633">16</span></span>| <span data-ttu-id="2db72-634">16</span><span class="sxs-lookup"><span data-stu-id="2db72-634">16</span></span>| <span data-ttu-id="2db72-635">16</span><span class="sxs-lookup"><span data-stu-id="2db72-635">16</span></span>|
| <span data-ttu-id="2db72-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="2db72-636">DW1000</span></span> | <span data-ttu-id="2db72-637">32</span><span class="sxs-lookup"><span data-stu-id="2db72-637">32</span></span>| <span data-ttu-id="2db72-638">40</span><span class="sxs-lookup"><span data-stu-id="2db72-638">40</span></span>| <span data-ttu-id="2db72-639">1</span><span class="sxs-lookup"><span data-stu-id="2db72-639">1</span></span>| <span data-ttu-id="2db72-640">2</span><span class="sxs-lookup"><span data-stu-id="2db72-640">2</span></span>| <span data-ttu-id="2db72-641">4</span><span class="sxs-lookup"><span data-stu-id="2db72-641">4</span></span>| <span data-ttu-id="2db72-642">8</span><span class="sxs-lookup"><span data-stu-id="2db72-642">8</span></span>| <span data-ttu-id="2db72-643">16</span><span class="sxs-lookup"><span data-stu-id="2db72-643">16</span></span>| <span data-ttu-id="2db72-644">32</span><span class="sxs-lookup"><span data-stu-id="2db72-644">32</span></span>| <span data-ttu-id="2db72-645">32</span><span class="sxs-lookup"><span data-stu-id="2db72-645">32</span></span>| <span data-ttu-id="2db72-646">32</span><span class="sxs-lookup"><span data-stu-id="2db72-646">32</span></span>|
| <span data-ttu-id="2db72-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="2db72-647">DW1200</span></span> | <span data-ttu-id="2db72-648">32</span><span class="sxs-lookup"><span data-stu-id="2db72-648">32</span></span>| <span data-ttu-id="2db72-649">48</span><span class="sxs-lookup"><span data-stu-id="2db72-649">48</span></span>| <span data-ttu-id="2db72-650">1</span><span class="sxs-lookup"><span data-stu-id="2db72-650">1</span></span>| <span data-ttu-id="2db72-651">2</span><span class="sxs-lookup"><span data-stu-id="2db72-651">2</span></span>| <span data-ttu-id="2db72-652">4</span><span class="sxs-lookup"><span data-stu-id="2db72-652">4</span></span>| <span data-ttu-id="2db72-653">8</span><span class="sxs-lookup"><span data-stu-id="2db72-653">8</span></span>| <span data-ttu-id="2db72-654">16</span><span class="sxs-lookup"><span data-stu-id="2db72-654">16</span></span>| <span data-ttu-id="2db72-655">32</span><span class="sxs-lookup"><span data-stu-id="2db72-655">32</span></span>| <span data-ttu-id="2db72-656">32</span><span class="sxs-lookup"><span data-stu-id="2db72-656">32</span></span>| <span data-ttu-id="2db72-657">32</span><span class="sxs-lookup"><span data-stu-id="2db72-657">32</span></span>|
| <span data-ttu-id="2db72-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="2db72-658">DW1500</span></span> | <span data-ttu-id="2db72-659">32</span><span class="sxs-lookup"><span data-stu-id="2db72-659">32</span></span>| <span data-ttu-id="2db72-660">60</span><span class="sxs-lookup"><span data-stu-id="2db72-660">60</span></span>| <span data-ttu-id="2db72-661">1</span><span class="sxs-lookup"><span data-stu-id="2db72-661">1</span></span>| <span data-ttu-id="2db72-662">2</span><span class="sxs-lookup"><span data-stu-id="2db72-662">2</span></span>| <span data-ttu-id="2db72-663">4</span><span class="sxs-lookup"><span data-stu-id="2db72-663">4</span></span>| <span data-ttu-id="2db72-664">8</span><span class="sxs-lookup"><span data-stu-id="2db72-664">8</span></span>| <span data-ttu-id="2db72-665">16</span><span class="sxs-lookup"><span data-stu-id="2db72-665">16</span></span>| <span data-ttu-id="2db72-666">32</span><span class="sxs-lookup"><span data-stu-id="2db72-666">32</span></span>| <span data-ttu-id="2db72-667">32</span><span class="sxs-lookup"><span data-stu-id="2db72-667">32</span></span>| <span data-ttu-id="2db72-668">32</span><span class="sxs-lookup"><span data-stu-id="2db72-668">32</span></span>|
| <span data-ttu-id="2db72-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="2db72-669">DW2000</span></span> | <span data-ttu-id="2db72-670">32</span><span class="sxs-lookup"><span data-stu-id="2db72-670">32</span></span>| <span data-ttu-id="2db72-671">80</span><span class="sxs-lookup"><span data-stu-id="2db72-671">80</span></span>| <span data-ttu-id="2db72-672">1</span><span class="sxs-lookup"><span data-stu-id="2db72-672">1</span></span>| <span data-ttu-id="2db72-673">2</span><span class="sxs-lookup"><span data-stu-id="2db72-673">2</span></span>| <span data-ttu-id="2db72-674">4</span><span class="sxs-lookup"><span data-stu-id="2db72-674">4</span></span>| <span data-ttu-id="2db72-675">8</span><span class="sxs-lookup"><span data-stu-id="2db72-675">8</span></span>| <span data-ttu-id="2db72-676">16</span><span class="sxs-lookup"><span data-stu-id="2db72-676">16</span></span>| <span data-ttu-id="2db72-677">32</span><span class="sxs-lookup"><span data-stu-id="2db72-677">32</span></span>| <span data-ttu-id="2db72-678">64</span><span class="sxs-lookup"><span data-stu-id="2db72-678">64</span></span>| <span data-ttu-id="2db72-679">64</span><span class="sxs-lookup"><span data-stu-id="2db72-679">64</span></span>|
| <span data-ttu-id="2db72-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="2db72-680">DW3000</span></span> | <span data-ttu-id="2db72-681">32</span><span class="sxs-lookup"><span data-stu-id="2db72-681">32</span></span>| <span data-ttu-id="2db72-682">120</span><span class="sxs-lookup"><span data-stu-id="2db72-682">120</span></span>| <span data-ttu-id="2db72-683">1</span><span class="sxs-lookup"><span data-stu-id="2db72-683">1</span></span>| <span data-ttu-id="2db72-684">2</span><span class="sxs-lookup"><span data-stu-id="2db72-684">2</span></span>| <span data-ttu-id="2db72-685">4</span><span class="sxs-lookup"><span data-stu-id="2db72-685">4</span></span>| <span data-ttu-id="2db72-686">8</span><span class="sxs-lookup"><span data-stu-id="2db72-686">8</span></span>| <span data-ttu-id="2db72-687">16</span><span class="sxs-lookup"><span data-stu-id="2db72-687">16</span></span>| <span data-ttu-id="2db72-688">32</span><span class="sxs-lookup"><span data-stu-id="2db72-688">32</span></span>| <span data-ttu-id="2db72-689">64</span><span class="sxs-lookup"><span data-stu-id="2db72-689">64</span></span>| <span data-ttu-id="2db72-690">64</span><span class="sxs-lookup"><span data-stu-id="2db72-690">64</span></span>|
| <span data-ttu-id="2db72-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="2db72-691">DW6000</span></span> | <span data-ttu-id="2db72-692">32</span><span class="sxs-lookup"><span data-stu-id="2db72-692">32</span></span>| <span data-ttu-id="2db72-693">240</span><span class="sxs-lookup"><span data-stu-id="2db72-693">240</span></span>| <span data-ttu-id="2db72-694">1</span><span class="sxs-lookup"><span data-stu-id="2db72-694">1</span></span>| <span data-ttu-id="2db72-695">2</span><span class="sxs-lookup"><span data-stu-id="2db72-695">2</span></span>| <span data-ttu-id="2db72-696">4</span><span class="sxs-lookup"><span data-stu-id="2db72-696">4</span></span>| <span data-ttu-id="2db72-697">8</span><span class="sxs-lookup"><span data-stu-id="2db72-697">8</span></span>| <span data-ttu-id="2db72-698">16</span><span class="sxs-lookup"><span data-stu-id="2db72-698">16</span></span>| <span data-ttu-id="2db72-699">32</span><span class="sxs-lookup"><span data-stu-id="2db72-699">32</span></span>| <span data-ttu-id="2db72-700">64</span><span class="sxs-lookup"><span data-stu-id="2db72-700">64</span></span>| <span data-ttu-id="2db72-701">128</span><span class="sxs-lookup"><span data-stu-id="2db72-701">128</span></span>|

<span data-ttu-id="2db72-702">À partir de ces tableaux, vous pouvez constater que SQL Data Warehouse s’exécutant comme DW1000 alloue au maximum 32 requêtes simultanées et un total de 40 emplacements de concurrence.</span><span class="sxs-lookup"><span data-stu-id="2db72-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="2db72-703">Si tous les utilisateurs étaient en cours d’exécution dans smallrc, 32 requêtes simultanées seraient alors autorisées car chaque requête consommerait un emplacement de concurrence.</span><span class="sxs-lookup"><span data-stu-id="2db72-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="2db72-704">Si tous les utilisateurs sur un DW1000 en cours d’exécution dans mediumrc, chaque requête est allouée 800 Mo par distribution pour une allocation de mémoire totale de 47 Go par la requête et concurrence serait limitée too5 utilisateurs (les emplacements d’accès concurrentiel 40 / 8 emplacements par mediumrc utilisateur).</span><span class="sxs-lookup"><span data-stu-id="2db72-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="2db72-705">Sélection d’une classe de ressources appropriée</span><span class="sxs-lookup"><span data-stu-id="2db72-705">Selecting proper resource class</span></span>  
<span data-ttu-id="2db72-706">Une bonne pratique est la classe de ressource tooa toopermanently affecter les utilisateurs, plutôt que de la modification de leurs classes de ressources.</span><span class="sxs-lookup"><span data-stu-id="2db72-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="2db72-707">Par exemple, tables de charge tooclustered columnstore créer des index de meilleure qualité lors de l’allocation de mémoire.</span><span class="sxs-lookup"><span data-stu-id="2db72-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="2db72-708">tooensure que charges ont accès toohigher mémoire, créez un utilisateur en particulier pour charger les données et définitivement affecter cette classe de ressource utilisateur tooa plus élevée.</span><span class="sxs-lookup"><span data-stu-id="2db72-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="2db72-709">Il existe quelques meilleures toofollow pratiques ici.</span><span class="sxs-lookup"><span data-stu-id="2db72-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="2db72-710">Comme nous l’avons vu précédemment, SQL DW prend en charge deux types de classes de ressources : les classes de ressources statiques et les classes de ressources dynamiques.</span><span class="sxs-lookup"><span data-stu-id="2db72-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="2db72-711">Bonnes pratiques de chargement</span><span class="sxs-lookup"><span data-stu-id="2db72-711">Loading best practices</span></span>
1.  <span data-ttu-id="2db72-712">Si les attentes de hello sont des charges régulières quantité de données, une classe de ressource statique est un bon choix.</span><span class="sxs-lookup"><span data-stu-id="2db72-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="2db72-713">Ultérieurement, lors de la mise à l’échelle des tooget plus de puissance de calcul, de l’entrepôt de données hello pourront toorun plu interroge out-of-the-box, comme utilisateur de charge hello ne consomme pas plus de mémoire.</span><span class="sxs-lookup"><span data-stu-id="2db72-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="2db72-714">Si les prévisions de hello sont des charges plus grandes dans certains cas, une classe de ressource dynamique est un bon choix.</span><span class="sxs-lookup"><span data-stu-id="2db72-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="2db72-715">Ultérieurement, lors de la mise à l’échelle des tooget plus de puissance de calcul, hello charge utilisateur obtient plus mémoire out-of-the-box, par conséquent, ce qui permet hello charge tooperform plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="2db72-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="2db72-716">Hello mémoire nécessaire tooprocess charges efficacement dépend hello nature du tableau hello chargé et quantité hello de traitement des données.</span><span class="sxs-lookup"><span data-stu-id="2db72-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="2db72-717">Par exemple, le chargement des données dans les tables CCI requiert que certains groupes de lignes de mémoire toolet CCI atteint Optimalité.</span><span class="sxs-lookup"><span data-stu-id="2db72-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="2db72-718">Pour plus d’informations, consultez les index Columnstore hello - Guide de chargement des données.</span><span class="sxs-lookup"><span data-stu-id="2db72-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="2db72-719">Comme meilleure pratique, nous vous recommandons de toouse au moins 200 Mo de mémoire pour les charges.</span><span class="sxs-lookup"><span data-stu-id="2db72-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="2db72-720">Bonnes pratiques de requête</span><span class="sxs-lookup"><span data-stu-id="2db72-720">Querying best practices</span></span>
<span data-ttu-id="2db72-721">Les exigences sur le plan des requêtes varient en fonction de leur complexité.</span><span class="sxs-lookup"><span data-stu-id="2db72-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="2db72-722">Augmentation de la mémoire par requête ou d’accroître la simultanéité de hello sont les deux tooaugment de méthodes valides pour le débit global en fonction des besoins de requête hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="2db72-723">Si les prévisions de hello sont des requêtes régulières complexes (par exemple, toogenerate rapports quotidiens et hebdomadaires) et n’avez pas besoin d’avantage tootake de l’accès concurrentiel, une classe de ressource dynamique est un bon choix.</span><span class="sxs-lookup"><span data-stu-id="2db72-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="2db72-724">Si le système de hello possède plusieurs tooprocess de données, mise à l’échelle de l’entrepôt de données hello par conséquent automatiquement fournira plus de mémoire toohello utilisateur exécutant la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="2db72-725">Si les prévisions de hello sont les modèles d’accès concurrentiel diurnes ou variable (par exemple si la base de données hello est interrogé via une interface utilisateur largement accessible web), une classe de ressource statique est un bon choix.</span><span class="sxs-lookup"><span data-stu-id="2db72-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="2db72-726">Ultérieurement, lors de la mise à l’échelle toodata entrepôt, utilisateur hello associé à la classe de ressource statique hello est automatiquement être toorun en mesure de requêtes simultanées plus.</span><span class="sxs-lookup"><span data-stu-id="2db72-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="2db72-727">En sélectionnant accorder appropriée de la mémoire en fonction de la nécessité de hello de votre requête est non trivial, car il dépend de nombreux facteurs, tels que quantité hello de données interrogées, hello nature des schémas de table hello et différentes jointure, la sélection et les prédicats de groupe.</span><span class="sxs-lookup"><span data-stu-id="2db72-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="2db72-728">À partir d’un point de vue général, allouez davantage de mémoire toocomplete de requêtes plus rapidement, mais elle réduit de manière hello d’accès concurrentiel global.</span><span class="sxs-lookup"><span data-stu-id="2db72-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="2db72-729">Si la concurrence n’est pas un problème, une allocation excessive de mémoire n’est pas dommageable.</span><span class="sxs-lookup"><span data-stu-id="2db72-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="2db72-730">ajuster les toofine débit, la tentative de différentes versions de classes de ressources peut être nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2db72-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="2db72-731">Vous pouvez utiliser suivante hello stockées toofigure procédure out octroi d’accès concurrentiel et la mémoire par la classe de ressource à une donnée SLO et hello plus proche meilleures classe de ressource pour les opérations CCI nécessitant de mémoire sur la table CCI non partitionnée à une classe de ressource donné :</span><span class="sxs-lookup"><span data-stu-id="2db72-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="2db72-732">Description :</span><span class="sxs-lookup"><span data-stu-id="2db72-732">Description:</span></span>  
<span data-ttu-id="2db72-733">Voici l’objectif hello de cette procédure stockée :</span><span class="sxs-lookup"><span data-stu-id="2db72-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="2db72-734">figure toohelp utilisateur out octroi d’accès concurrentiel et la mémoire par la classe de ressource à un objectif du contrat donné.</span><span class="sxs-lookup"><span data-stu-id="2db72-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="2db72-735">Utilisateur doit tooprovide NULL pour le schéma et tablename pour ce comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2db72-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="2db72-736">l’utilisateur toohelp trouver hello meilleures ressources classe la plus proche pour hello mémoire intensed opérations CCI (charger, table de copie, reconstruire les index, etc.) non partitionnée table CCI à une classe de ressource donné.</span><span class="sxs-lookup"><span data-stu-id="2db72-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="2db72-737">stockée Hello proc utilise toofind de schéma de table à l’allocation de mémoire requise hello pour cela.</span><span class="sxs-lookup"><span data-stu-id="2db72-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="2db72-738">Dépendances et restrictions :</span><span class="sxs-lookup"><span data-stu-id="2db72-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="2db72-739">Cette procédure stockée n’est pas conçue toocalculate mémoire requise pour les table cci partitionnée.</span><span class="sxs-lookup"><span data-stu-id="2db72-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="2db72-740">Cette procédure stockée ne prend pas d’exigence de mémoire en compte pour la partie SELECT de hello de INSERT/SACT-sélectionnez et il suppose toobe une instruction SELECT simple.</span><span class="sxs-lookup"><span data-stu-id="2db72-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="2db72-741">Cette procédure stockée utilise une table temporaire pour ce peut être utilisé dans la session de hello où cette procédure stockée a été créée.</span><span class="sxs-lookup"><span data-stu-id="2db72-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="2db72-742">Cette procédure stockée dépend d’offres actuelles de hello (par exemple, configuration matérielle, DMS config) et si un des qui modifie ensuite cette procédure stockée ne fonctionnera pas correctement.</span><span class="sxs-lookup"><span data-stu-id="2db72-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="2db72-743">Cette procédure stockée dépend de la limite de concurrence offerte existante et si celle-ci change, cette procédure stockée ne fonctionnera pas correctement.</span><span class="sxs-lookup"><span data-stu-id="2db72-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="2db72-744">Cette procédure stockée dépend des offres de classes de ressources existantes et si celles-ci changent, cette procédure stockée ne fonctionnera pas correctement.</span><span class="sxs-lookup"><span data-stu-id="2db72-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="2db72-745">Si vous n’obtenez pas de sortie après l’exécution de la procédure stockée avec les paramètres fournis, il est possible que vous soyez confronté à l’un des deux cas suivants :</span><span class="sxs-lookup"><span data-stu-id="2db72-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="2db72-746">1. Un paramètre DW contient une valeur SLO non valide.</span><span class="sxs-lookup"><span data-stu-id="2db72-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="2db72-747">2. OU il n’existe aucune classe de ressources correspondante pour l’opération ICC si le nom de la table a été fourni.</span><span class="sxs-lookup"><span data-stu-id="2db72-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="2db72-748">Par exemple, à DW100, allocation de mémoire disponible la plus élevée est de 400 Mo et si le schéma de la table est large suffisamment toocross hello exigence de 400 Mo.</span><span class="sxs-lookup"><span data-stu-id="2db72-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="2db72-749">Exemple d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="2db72-749">Usage example:</span></span>
<span data-ttu-id="2db72-750">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="2db72-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="2db72-751">@DWU:Vous devez attribuer un tooextract de paramètre NULL hello DWU actuelle à partir de la BD DW de hello ou fournir une prise en charge DWU sous forme de hello de 'DW100'</span><span class="sxs-lookup"><span data-stu-id="2db72-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="2db72-752">@SCHEMA_NAME:Fournissez un nom de schéma de table de hello</span><span class="sxs-lookup"><span data-stu-id="2db72-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="2db72-753">@TABLE_NAME:Fournissez un nom de table d’intérêt de hello</span><span class="sxs-lookup"><span data-stu-id="2db72-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="2db72-754">Exemples d’exécution de cette procédure stockée :</span><span class="sxs-lookup"><span data-stu-id="2db72-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="2db72-755">Table1 utilisé Bonjour exemples ci-dessus pourrait être créée comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2db72-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="2db72-756">Voici la définition de la procédure stockée hello :</span><span class="sxs-lookup"><span data-stu-id="2db72-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="2db72-757">Importance de la requête</span><span class="sxs-lookup"><span data-stu-id="2db72-757">Query importance</span></span>
<span data-ttu-id="2db72-758">SQL Data Warehouse implémente des classes de ressources à l’aide de groupes de charges de travail.</span><span class="sxs-lookup"><span data-stu-id="2db72-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="2db72-759">Il existe un total de huit groupes de charges de travail qui contrôlent le comportement de hello de classes de ressources hello sur hello différentes tailles DWU.</span><span class="sxs-lookup"><span data-stu-id="2db72-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="2db72-760">Pour n’importe quel DWU, SQL Data Warehouse utilise quatre groupes de charges de travail de huit hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="2db72-761">Cela est logique car chaque groupe de charge de travail est affecté tooone de quatre classes de ressources : smallrc, mediumrc, largerc, ou xlargerc.</span><span class="sxs-lookup"><span data-stu-id="2db72-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="2db72-762">Bonjour importance de la présentation des groupes de charges de travail hello est que certains de ces groupes de charges de travail sont définis toohigher *importance*.</span><span class="sxs-lookup"><span data-stu-id="2db72-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="2db72-763">L’importance est utilisée pour la planification du processeur.</span><span class="sxs-lookup"><span data-stu-id="2db72-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="2db72-764">Les requêtes exécutées avec une importance élevée obtiennent trois fois plus de cycles processeur que celles exécutées avec une importance moyenne.</span><span class="sxs-lookup"><span data-stu-id="2db72-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="2db72-765">Ainsi, les mappages d’emplacements de concurrence déterminent également la priorité du processeur.</span><span class="sxs-lookup"><span data-stu-id="2db72-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="2db72-766">Quand une requête utilise 16 emplacements ou plus, elle s’exécute avec une importance élevée.</span><span class="sxs-lookup"><span data-stu-id="2db72-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="2db72-767">Hello tableau suivant montre les mappages d’importance hello pour chaque groupe de charges de travail.</span><span class="sxs-lookup"><span data-stu-id="2db72-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="2db72-768">Importance et les emplacements de la charge de travail groupe mappages tooconcurrency</span><span class="sxs-lookup"><span data-stu-id="2db72-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="2db72-769">Groupes de charges de travail</span><span class="sxs-lookup"><span data-stu-id="2db72-769">Workload groups</span></span> | <span data-ttu-id="2db72-770">Mappage d’emplacement de concurrence</span><span class="sxs-lookup"><span data-stu-id="2db72-770">Concurrency slot mapping</span></span> | <span data-ttu-id="2db72-771">Mo / Distribution</span><span class="sxs-lookup"><span data-stu-id="2db72-771">MB / Distribution</span></span> | <span data-ttu-id="2db72-772">Mappage d’importance</span><span class="sxs-lookup"><span data-stu-id="2db72-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="2db72-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="2db72-773">SloDWGroupC00</span></span> |<span data-ttu-id="2db72-774">1</span><span class="sxs-lookup"><span data-stu-id="2db72-774">1</span></span> |<span data-ttu-id="2db72-775">100</span><span class="sxs-lookup"><span data-stu-id="2db72-775">100</span></span> |<span data-ttu-id="2db72-776">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-776">Medium</span></span> |
| <span data-ttu-id="2db72-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="2db72-777">SloDWGroupC01</span></span> |<span data-ttu-id="2db72-778">2</span><span class="sxs-lookup"><span data-stu-id="2db72-778">2</span></span> |<span data-ttu-id="2db72-779">200</span><span class="sxs-lookup"><span data-stu-id="2db72-779">200</span></span> |<span data-ttu-id="2db72-780">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-780">Medium</span></span> |
| <span data-ttu-id="2db72-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="2db72-781">SloDWGroupC02</span></span> |<span data-ttu-id="2db72-782">4</span><span class="sxs-lookup"><span data-stu-id="2db72-782">4</span></span> |<span data-ttu-id="2db72-783">400</span><span class="sxs-lookup"><span data-stu-id="2db72-783">400</span></span> |<span data-ttu-id="2db72-784">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-784">Medium</span></span> |
| <span data-ttu-id="2db72-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-785">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-786">8</span><span class="sxs-lookup"><span data-stu-id="2db72-786">8</span></span> |<span data-ttu-id="2db72-787">800</span><span class="sxs-lookup"><span data-stu-id="2db72-787">800</span></span> |<span data-ttu-id="2db72-788">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-788">Medium</span></span> |
| <span data-ttu-id="2db72-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="2db72-789">SloDWGroupC04</span></span> |<span data-ttu-id="2db72-790">16</span><span class="sxs-lookup"><span data-stu-id="2db72-790">16</span></span> |<span data-ttu-id="2db72-791">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-791">1,600</span></span> |<span data-ttu-id="2db72-792">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-792">High</span></span> |
| <span data-ttu-id="2db72-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="2db72-793">SloDWGroupC05</span></span> |<span data-ttu-id="2db72-794">32</span><span class="sxs-lookup"><span data-stu-id="2db72-794">32</span></span> |<span data-ttu-id="2db72-795">3 200</span><span class="sxs-lookup"><span data-stu-id="2db72-795">3,200</span></span> |<span data-ttu-id="2db72-796">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-796">High</span></span> |
| <span data-ttu-id="2db72-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="2db72-797">SloDWGroupC06</span></span> |<span data-ttu-id="2db72-798">64</span><span class="sxs-lookup"><span data-stu-id="2db72-798">64</span></span> |<span data-ttu-id="2db72-799">6 400</span><span class="sxs-lookup"><span data-stu-id="2db72-799">6,400</span></span> |<span data-ttu-id="2db72-800">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-800">High</span></span> |
| <span data-ttu-id="2db72-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="2db72-801">SloDWGroupC07</span></span> |<span data-ttu-id="2db72-802">128</span><span class="sxs-lookup"><span data-stu-id="2db72-802">128</span></span> |<span data-ttu-id="2db72-803">12 800</span><span class="sxs-lookup"><span data-stu-id="2db72-803">12,800</span></span> |<span data-ttu-id="2db72-804">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-804">High</span></span> |

<span data-ttu-id="2db72-805">À partir de hello **Allocation et la consommation d’emplacements de concurrence** graphique, vous pouvez constater qu’un DW500 utilise 1, 4, 8 ou les emplacements d’accès concurrentiel 16 pour smallrc, mediumrc, largerc et xlargerc, respectivement.</span><span class="sxs-lookup"><span data-stu-id="2db72-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="2db72-806">Vous pouvez rechercher ces valeurs Bonjour précédant l’importance de hello toofind graphique pour chaque classe de ressource.</span><span class="sxs-lookup"><span data-stu-id="2db72-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="2db72-807">Mappage de DW500 de tooimportance de classes de ressources</span><span class="sxs-lookup"><span data-stu-id="2db72-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="2db72-808">classe de ressources</span><span class="sxs-lookup"><span data-stu-id="2db72-808">Resource class</span></span> | <span data-ttu-id="2db72-809">Groupe de charges de travail</span><span class="sxs-lookup"><span data-stu-id="2db72-809">Workload group</span></span> | <span data-ttu-id="2db72-810">Emplacements de concurrence utilisés</span><span class="sxs-lookup"><span data-stu-id="2db72-810">Concurrency slots used</span></span> | <span data-ttu-id="2db72-811">Mo / Distribution</span><span class="sxs-lookup"><span data-stu-id="2db72-811">MB / Distribution</span></span> | <span data-ttu-id="2db72-812">importance</span><span class="sxs-lookup"><span data-stu-id="2db72-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="2db72-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="2db72-813">smallrc</span></span> |<span data-ttu-id="2db72-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="2db72-814">SloDWGroupC00</span></span> |<span data-ttu-id="2db72-815">1</span><span class="sxs-lookup"><span data-stu-id="2db72-815">1</span></span> |<span data-ttu-id="2db72-816">100</span><span class="sxs-lookup"><span data-stu-id="2db72-816">100</span></span> |<span data-ttu-id="2db72-817">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-817">Medium</span></span> |
| <span data-ttu-id="2db72-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="2db72-818">mediumrc</span></span> |<span data-ttu-id="2db72-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="2db72-819">SloDWGroupC02</span></span> |<span data-ttu-id="2db72-820">4</span><span class="sxs-lookup"><span data-stu-id="2db72-820">4</span></span> |<span data-ttu-id="2db72-821">400</span><span class="sxs-lookup"><span data-stu-id="2db72-821">400</span></span> |<span data-ttu-id="2db72-822">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-822">Medium</span></span> |
| <span data-ttu-id="2db72-823">largerc</span><span class="sxs-lookup"><span data-stu-id="2db72-823">largerc</span></span> |<span data-ttu-id="2db72-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-824">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-825">8</span><span class="sxs-lookup"><span data-stu-id="2db72-825">8</span></span> |<span data-ttu-id="2db72-826">800</span><span class="sxs-lookup"><span data-stu-id="2db72-826">800</span></span> |<span data-ttu-id="2db72-827">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-827">Medium</span></span> |
| <span data-ttu-id="2db72-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="2db72-828">xlargerc</span></span> |<span data-ttu-id="2db72-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="2db72-829">SloDWGroupC04</span></span> |<span data-ttu-id="2db72-830">16</span><span class="sxs-lookup"><span data-stu-id="2db72-830">16</span></span> |<span data-ttu-id="2db72-831">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-831">1,600</span></span> |<span data-ttu-id="2db72-832">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-832">High</span></span> |
| <span data-ttu-id="2db72-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="2db72-833">staticrc10</span></span> |<span data-ttu-id="2db72-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="2db72-834">SloDWGroupC00</span></span> |<span data-ttu-id="2db72-835">1</span><span class="sxs-lookup"><span data-stu-id="2db72-835">1</span></span> |<span data-ttu-id="2db72-836">100</span><span class="sxs-lookup"><span data-stu-id="2db72-836">100</span></span> |<span data-ttu-id="2db72-837">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-837">Medium</span></span> |
| <span data-ttu-id="2db72-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="2db72-838">staticrc20</span></span> |<span data-ttu-id="2db72-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="2db72-839">SloDWGroupC01</span></span> |<span data-ttu-id="2db72-840">2</span><span class="sxs-lookup"><span data-stu-id="2db72-840">2</span></span> |<span data-ttu-id="2db72-841">200</span><span class="sxs-lookup"><span data-stu-id="2db72-841">200</span></span> |<span data-ttu-id="2db72-842">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-842">Medium</span></span> |
| <span data-ttu-id="2db72-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="2db72-843">staticrc30</span></span> |<span data-ttu-id="2db72-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="2db72-844">SloDWGroupC02</span></span> |<span data-ttu-id="2db72-845">4</span><span class="sxs-lookup"><span data-stu-id="2db72-845">4</span></span> |<span data-ttu-id="2db72-846">400</span><span class="sxs-lookup"><span data-stu-id="2db72-846">400</span></span> |<span data-ttu-id="2db72-847">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-847">Medium</span></span> |
| <span data-ttu-id="2db72-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="2db72-848">staticrc40</span></span> |<span data-ttu-id="2db72-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-849">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-850">8</span><span class="sxs-lookup"><span data-stu-id="2db72-850">8</span></span> |<span data-ttu-id="2db72-851">800</span><span class="sxs-lookup"><span data-stu-id="2db72-851">800</span></span> |<span data-ttu-id="2db72-852">Moyenne</span><span class="sxs-lookup"><span data-stu-id="2db72-852">Medium</span></span> |
| <span data-ttu-id="2db72-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="2db72-853">staticrc50</span></span> |<span data-ttu-id="2db72-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-854">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-855">16</span><span class="sxs-lookup"><span data-stu-id="2db72-855">16</span></span> |<span data-ttu-id="2db72-856">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-856">1,600</span></span> |<span data-ttu-id="2db72-857">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-857">High</span></span> |
| <span data-ttu-id="2db72-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="2db72-858">staticrc60</span></span> |<span data-ttu-id="2db72-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-859">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-860">16</span><span class="sxs-lookup"><span data-stu-id="2db72-860">16</span></span> |<span data-ttu-id="2db72-861">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-861">1,600</span></span> |<span data-ttu-id="2db72-862">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-862">High</span></span> |
| <span data-ttu-id="2db72-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="2db72-863">staticrc70</span></span> |<span data-ttu-id="2db72-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-864">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-865">16</span><span class="sxs-lookup"><span data-stu-id="2db72-865">16</span></span> |<span data-ttu-id="2db72-866">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-866">1,600</span></span> |<span data-ttu-id="2db72-867">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-867">High</span></span> |
| <span data-ttu-id="2db72-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="2db72-868">staticrc80</span></span> |<span data-ttu-id="2db72-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="2db72-869">SloDWGroupC03</span></span> |<span data-ttu-id="2db72-870">16</span><span class="sxs-lookup"><span data-stu-id="2db72-870">16</span></span> |<span data-ttu-id="2db72-871">1 600</span><span class="sxs-lookup"><span data-stu-id="2db72-871">1,600</span></span> |<span data-ttu-id="2db72-872">Élevé</span><span class="sxs-lookup"><span data-stu-id="2db72-872">High</span></span> |

<span data-ttu-id="2db72-873">Vous pouvez utiliser hello suivant toolook de requête DMV différences hello dans l’allocation des ressources mémoire en détail à partir de la perspective hello du gouverneur de ressources hello ou tooanalyze actives et historiques d’utilisation des groupes de charges de travail hello lors du dépannage.</span><span class="sxs-lookup"><span data-stu-id="2db72-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="2db72-874">Requêtes qui honorent les limites de concurrence</span><span class="sxs-lookup"><span data-stu-id="2db72-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="2db72-875">La plupart des requêtes sont régies par des classes de ressource.</span><span class="sxs-lookup"><span data-stu-id="2db72-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="2db72-876">Ces requêtes doivent tenir à l’intérieur de requêtes simultanées hello et seuils d’emplacement d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="2db72-877">Un utilisateur ne peut pas choisir tooexclude une requête à partir du modèle d’emplacement hello d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="2db72-878">tooreiterate, hello classes de ressources d’honorer les instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2db72-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="2db72-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="2db72-879">INSERT-SELECT</span></span>
* <span data-ttu-id="2db72-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="2db72-880">UPDATE</span></span>
* <span data-ttu-id="2db72-881">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="2db72-881">DELETE</span></span>
* <span data-ttu-id="2db72-882">SELECT (lors de l’interrogation des tables d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="2db72-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="2db72-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="2db72-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="2db72-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="2db72-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="2db72-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="2db72-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="2db72-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="2db72-886">CREATE INDEX</span></span>
* <span data-ttu-id="2db72-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="2db72-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="2db72-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="2db72-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="2db72-889">Chargement de données</span><span class="sxs-lookup"><span data-stu-id="2db72-889">Data loading</span></span>
* <span data-ttu-id="2db72-890">Opérations de déplacement de données effectuées par hello Service de déplacement des données (DMS)</span><span class="sxs-lookup"><span data-stu-id="2db72-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="2db72-891">Requête exceptions tooconcurrency limites</span><span class="sxs-lookup"><span data-stu-id="2db72-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="2db72-892">Certaines requêtes ne tiennent pas compte des ressources de hello classe toowhich hello utilisateur est affecté.</span><span class="sxs-lookup"><span data-stu-id="2db72-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="2db72-893">Ces exceptions toohello les limites d’accès concurrentiel sont effectuées lorsque hello des ressources nécessaires pour une commande particulière est faible, souvent parce que la commande hello est une opération de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="2db72-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="2db72-894">Hello ces exceptions vise tooavoid les allocations de mémoire supérieure pour les requêtes qui n’auront jamais besoin les.</span><span class="sxs-lookup"><span data-stu-id="2db72-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="2db72-895">Dans ces cas, hello par défaut de la classe de ressource le plus petit (smallrc) est toujours utilisé, quelle que soit la classe attribué toohello utilisateur hello ressource réelle.</span><span class="sxs-lookup"><span data-stu-id="2db72-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="2db72-896">Par exemple, `CREATE LOGIN` s’exécute toujours dans smallrc.</span><span class="sxs-lookup"><span data-stu-id="2db72-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="2db72-897">Hello ressources requises toofulfill cette opération étant très faible, il n’effectue aucune requête de sens tooinclude hello dans le modèle d’emplacement hello d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="2db72-898">Également ces requêtes ne sont pas limités par limite de hello 32 utilisateur d’accès concurrentiel, limite de la session toohello de 1 024 sessions peut exécuter un nombre illimité de ces requêtes.</span><span class="sxs-lookup"><span data-stu-id="2db72-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="2db72-899">suivant les instructions de Hello n’honorent pas ces classes de ressources :</span><span class="sxs-lookup"><span data-stu-id="2db72-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="2db72-900">CREATE ou DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="2db72-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="2db72-901">ALTER TABLE ... SWITCH, SPLIT ou MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="2db72-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="2db72-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="2db72-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="2db72-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="2db72-903">DROP INDEX</span></span>
* <span data-ttu-id="2db72-904">CREATE, UPDATE ou DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="2db72-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="2db72-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="2db72-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="2db72-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="2db72-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="2db72-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="2db72-907">CREATE LOGIN</span></span>
* <span data-ttu-id="2db72-908">CREATE, ALTER ou DROP USER</span><span class="sxs-lookup"><span data-stu-id="2db72-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="2db72-909">CREATE, ALTER ou DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="2db72-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="2db72-910">CREATE ou DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="2db72-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="2db72-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="2db72-911">INSERT VALUES</span></span>
* <span data-ttu-id="2db72-912">SELECT à partir des affichages système et des DMV</span><span class="sxs-lookup"><span data-stu-id="2db72-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="2db72-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="2db72-913">EXPLAIN</span></span>
* <span data-ttu-id="2db72-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="2db72-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="2db72-915"><a name="changing-user-resource-class-example"></a> Exemple de modification d’une classe de ressources utilisateur</span><span class="sxs-lookup"><span data-stu-id="2db72-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="2db72-916">**Créer une connexion :** ouvrir une connexion tooyour **master** hello serveur SQL Server hébergeant la base de données de l’entrepôt de données SQL de base de données et exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="2db72-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="2db72-917">Il est une bonne idée de toocreate un utilisateur dans la base de données master hello pour les utilisateurs d’Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2db72-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="2db72-918">Création d’un utilisateur dans master permet une toologin d’utilisateur à l’aide des outils tels que SSMS sans spécifier un nom de base de données.</span><span class="sxs-lookup"><span data-stu-id="2db72-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="2db72-919">Cela leur permet également toouse hello objet explorer tooview toutes les bases de données sur un serveur SQL server.</span><span class="sxs-lookup"><span data-stu-id="2db72-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="2db72-920">Pour plus d’informations sur la création et la gestion des utilisateurs, consultez [Sécuriser une base de données dans SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2db72-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="2db72-921">**Créer un utilisateur de l’entrepôt de données SQL :** ouvrir une connexion toohello **SQL Data Warehouse** de base de données et exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="2db72-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="2db72-922">**Accorder des autorisations :** hello suivant accorde de l’exemple `CONTROL` sur hello **SQL Data Warehouse** base de données.</span><span class="sxs-lookup"><span data-stu-id="2db72-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="2db72-923">`CONTROL`à hello au niveau de la base de données est hello équivalent db_owner dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2db72-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="2db72-924">**Augmenter la classe de ressource :** tooadd de requête suivante de hello d’utiliser un rôle de gestion de la charge de travail supérieure utilisateur tooa.</span><span class="sxs-lookup"><span data-stu-id="2db72-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="2db72-925">**Diminuer la classe de ressource :** tooremove de requête suivante de hello d’utiliser un utilisateur à partir d’un rôle de gestion de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="2db72-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="2db72-926">Il n’est pas possible de tooremove un utilisateur à partir de smallrc.</span><span class="sxs-lookup"><span data-stu-id="2db72-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="2db72-927">Détection des requêtes en file d’attente et autres vues de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="2db72-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="2db72-928">Vous pouvez utiliser hello `sys.dm_pdw_exec_requests` requêtes DMV tooidentify qui sont en attente dans une file d’attente d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="2db72-929">Les requêtes en attente pour un emplacement de concurrence auront le statut **suspendu**.</span><span class="sxs-lookup"><span data-stu-id="2db72-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="2db72-930">Vous pouvez afficher les rôles de gestion des charges de travail avec `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="2db72-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="2db72-931">Hello suivant la requête indique quel rôle est affecté à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2db72-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="2db72-932">SQL Data Warehouse a hello suivante de types d’attente :</span><span class="sxs-lookup"><span data-stu-id="2db72-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="2db72-933">**LocalQueriesConcurrencyResourceType**: les requêtes qui se trouvent en dehors de l’infrastructure d’emplacement hello d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="2db72-934">Les requêtes DMV et les fonctions système telles que `SELECT @@VERSION` sont des exemples de requête locale.</span><span class="sxs-lookup"><span data-stu-id="2db72-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="2db72-935">**UserConcurrencyResourceType**: les requêtes qui se trouvent à l’intérieur d’infrastructure d’emplacement hello d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="2db72-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="2db72-936">Les requêtes exécutées sur des tables d’utilisateurs finaux sont des exemples de requêtes qui doivent utiliser ce type de ressource.</span><span class="sxs-lookup"><span data-stu-id="2db72-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="2db72-937">**DmsConcurrencyResourceType**: attentes résultant d’opérations de déplacement de données.</span><span class="sxs-lookup"><span data-stu-id="2db72-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="2db72-938">**BackupConcurrencyResourceType**: cette attente indique qu’une base de données est en cours de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="2db72-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="2db72-939">valeur maximale de Hello pour ce type de ressource est 1.</span><span class="sxs-lookup"><span data-stu-id="2db72-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="2db72-940">Si plusieurs sauvegardes ont été demandés au hello simultanément, hello d’autres file d’attente.</span><span class="sxs-lookup"><span data-stu-id="2db72-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="2db72-941">Hello `sys.dm_pdw_waits` DMV peut être utilisé toosee les ressources auxquelles une demande en attente pour.</span><span class="sxs-lookup"><span data-stu-id="2db72-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="2db72-942">Hello `sys.dm_pdw_resource_waits` DMV affiche uniquement les attentes de ressources hello consommées par une requête donnée.</span><span class="sxs-lookup"><span data-stu-id="2db72-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="2db72-943">Temps d’attente de ressources mesure uniquement le temps de hello en attente de toobe de ressources fourni, comme toosignal opposé délai, qui est le temps de hello nécessaire pour hello sous-jacent serveurs tooschedule hello la requête SQL sur les UC hello.</span><span class="sxs-lookup"><span data-stu-id="2db72-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="2db72-944">Hello `sys.dm_pdw_wait_stats` DMV peut être utilisé pour l’analyse des tendances historiques d’attentes.</span><span class="sxs-lookup"><span data-stu-id="2db72-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="2db72-945">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2db72-945">Next steps</span></span>
<span data-ttu-id="2db72-946">Pour plus d’informations sur la gestion de la sécurité et des utilisateurs de base de données, consultez [Sécuriser une base de données dans SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2db72-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="2db72-947">Pour plus d’informations sur les classes de ressources la plus grande peut améliorer la qualité d’index cluster columnstore, consultez [la reconstruction de qualité de segment index tooimprove].</span><span class="sxs-lookup"><span data-stu-id="2db72-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[la reconstruction de qualité de segment index tooimprove]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
