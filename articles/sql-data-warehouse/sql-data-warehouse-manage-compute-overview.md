---
title: "Gestion de la puissance de calcul dans Azure SQL Data Warehouse (Vue d’ensemble) | Documents Microsoft"
description: "Capacités de montée en puissance des performances dans Azure SQL Data Warehouse. Montez en puissance en ajustant le nombre d’unités DWU ou suspendez et reprenez des ressources de calcul pour réduire les coûts."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="68f5f-104">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (Vue d’ensemble)</span><span class="sxs-lookup"><span data-stu-id="68f5f-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68f5f-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="68f5f-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="68f5f-106">Portail</span><span class="sxs-lookup"><span data-stu-id="68f5f-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="68f5f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68f5f-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="68f5f-108">REST</span><span class="sxs-lookup"><span data-stu-id="68f5f-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="68f5f-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="68f5f-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="68f5f-110">L’architecture de SQL Data Warehouse sépare le stockage du calcul, ce qui permet de les mettre à l’échelle indépendamment l’un de l’autre.</span><span class="sxs-lookup"><span data-stu-id="68f5f-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="68f5f-111">En conséquence, le calcul peut être mis à l’échelle pour répondre aux exigences de performance, indépendamment du volume de données.</span><span class="sxs-lookup"><span data-stu-id="68f5f-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="68f5f-112">Une conséquence naturelle de cette architecture est la séparation de la [facturation][billed] du calcul et du stockage.</span><span class="sxs-lookup"><span data-stu-id="68f5f-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="68f5f-113">Cette présentation décrit le fonctionnement de la mise à l’échelle avec SQL Data Warehouse. Elle explique également comment utiliser les fonctionnalités de mise en pause, de reprise et de mise à l’échelle de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68f5f-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="68f5f-114">Consultez la page sur les [Data Warehouse Units (DWU)][data warehouse units (DWUs)] pour en apprendre davantage sur les DWU et leurs performances.</span><span class="sxs-lookup"><span data-stu-id="68f5f-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="68f5f-115">Fonctionnement des opérations de gestion du calcul dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="68f5f-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="68f5f-116">L’architecture de SQL Data Warehouse consiste en un nœud de contrôle, des nœuds de calcul et la couche de stockage, le tout réparti sur 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="68f5f-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="68f5f-117">Au cours d’une session active normale dans SQL Data Warehouse, le nœud principal du système gère les métadonnées et contient l’optimiseur de requête distribuée.</span><span class="sxs-lookup"><span data-stu-id="68f5f-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="68f5f-118">Sous ce nœud principal, se trouvent les nœuds de calcul et la couche de stockage.</span><span class="sxs-lookup"><span data-stu-id="68f5f-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="68f5f-119">Pour une instance de 400 DWU, votre système possède un nœud principal, quatre nœuds de calcul et la couche de stockage, soit 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="68f5f-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="68f5f-120">Lorsque vous entreprenez une mise à l’échelle ou que vous interrompez l’opération, le système supprime tout d’abord toutes les requêtes entrantes, puis restaure les transactions pour garantir un état cohérent.</span><span class="sxs-lookup"><span data-stu-id="68f5f-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="68f5f-121">La mise à l’échelle intervient uniquement une fois la restauration des transactions effectuée.</span><span class="sxs-lookup"><span data-stu-id="68f5f-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="68f5f-122">Pour une opération de montée en puissance, le système configure le nombre de nœuds de calcul souhaité, puis commence le rattachement des nœuds de calcul à la couche de stockage.</span><span class="sxs-lookup"><span data-stu-id="68f5f-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="68f5f-123">Pour une opération de descente en puissance, les nœuds inutiles sont rendus disponibles et les nœuds de calcul restants sont rattachés au nombre de distributions approprié.</span><span class="sxs-lookup"><span data-stu-id="68f5f-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="68f5f-124">Pour une opération de mise en pause, tous les nœuds de calcul sont rendus disponibles et le système entreprend diverses opérations sur les métadonnées afin de garantir la stabilité du système final.</span><span class="sxs-lookup"><span data-stu-id="68f5f-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="68f5f-125">DWU</span><span class="sxs-lookup"><span data-stu-id="68f5f-125">DWU</span></span>  | <span data-ttu-id="68f5f-126">\# de nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="68f5f-126">\#of compute nodes</span></span> | <span data-ttu-id="68f5f-127">\# de distributions par nœud</span><span class="sxs-lookup"><span data-stu-id="68f5f-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="68f5f-128">100</span><span class="sxs-lookup"><span data-stu-id="68f5f-128">100</span></span>  | <span data-ttu-id="68f5f-129">1</span><span class="sxs-lookup"><span data-stu-id="68f5f-129">1</span></span>                  | <span data-ttu-id="68f5f-130">60</span><span class="sxs-lookup"><span data-stu-id="68f5f-130">60</span></span>                           |
| <span data-ttu-id="68f5f-131">200</span><span class="sxs-lookup"><span data-stu-id="68f5f-131">200</span></span>  | <span data-ttu-id="68f5f-132">2</span><span class="sxs-lookup"><span data-stu-id="68f5f-132">2</span></span>                  | <span data-ttu-id="68f5f-133">30</span><span class="sxs-lookup"><span data-stu-id="68f5f-133">30</span></span>                           |
| <span data-ttu-id="68f5f-134">300</span><span class="sxs-lookup"><span data-stu-id="68f5f-134">300</span></span>  | <span data-ttu-id="68f5f-135">3</span><span class="sxs-lookup"><span data-stu-id="68f5f-135">3</span></span>                  | <span data-ttu-id="68f5f-136">20</span><span class="sxs-lookup"><span data-stu-id="68f5f-136">20</span></span>                           |
| <span data-ttu-id="68f5f-137">400</span><span class="sxs-lookup"><span data-stu-id="68f5f-137">400</span></span>  | <span data-ttu-id="68f5f-138">4</span><span class="sxs-lookup"><span data-stu-id="68f5f-138">4</span></span>                  | <span data-ttu-id="68f5f-139">15</span><span class="sxs-lookup"><span data-stu-id="68f5f-139">15</span></span>                           |
| <span data-ttu-id="68f5f-140">500</span><span class="sxs-lookup"><span data-stu-id="68f5f-140">500</span></span>  | <span data-ttu-id="68f5f-141">5</span><span class="sxs-lookup"><span data-stu-id="68f5f-141">5</span></span>                  | <span data-ttu-id="68f5f-142">12</span><span class="sxs-lookup"><span data-stu-id="68f5f-142">12</span></span>                           |
| <span data-ttu-id="68f5f-143">600</span><span class="sxs-lookup"><span data-stu-id="68f5f-143">600</span></span>  | <span data-ttu-id="68f5f-144">6</span><span class="sxs-lookup"><span data-stu-id="68f5f-144">6</span></span>                  | <span data-ttu-id="68f5f-145">10</span><span class="sxs-lookup"><span data-stu-id="68f5f-145">10</span></span>                           |
| <span data-ttu-id="68f5f-146">1 000</span><span class="sxs-lookup"><span data-stu-id="68f5f-146">1000</span></span> | <span data-ttu-id="68f5f-147">10</span><span class="sxs-lookup"><span data-stu-id="68f5f-147">10</span></span>                 | <span data-ttu-id="68f5f-148">6</span><span class="sxs-lookup"><span data-stu-id="68f5f-148">6</span></span>                            |
| <span data-ttu-id="68f5f-149">1 200</span><span class="sxs-lookup"><span data-stu-id="68f5f-149">1200</span></span> | <span data-ttu-id="68f5f-150">12</span><span class="sxs-lookup"><span data-stu-id="68f5f-150">12</span></span>                 | <span data-ttu-id="68f5f-151">5</span><span class="sxs-lookup"><span data-stu-id="68f5f-151">5</span></span>                            |
| <span data-ttu-id="68f5f-152">1 500</span><span class="sxs-lookup"><span data-stu-id="68f5f-152">1500</span></span> | <span data-ttu-id="68f5f-153">15</span><span class="sxs-lookup"><span data-stu-id="68f5f-153">15</span></span>                 | <span data-ttu-id="68f5f-154">4</span><span class="sxs-lookup"><span data-stu-id="68f5f-154">4</span></span>                            |
| <span data-ttu-id="68f5f-155">2000</span><span class="sxs-lookup"><span data-stu-id="68f5f-155">2000</span></span> | <span data-ttu-id="68f5f-156">20</span><span class="sxs-lookup"><span data-stu-id="68f5f-156">20</span></span>                 | <span data-ttu-id="68f5f-157">3</span><span class="sxs-lookup"><span data-stu-id="68f5f-157">3</span></span>                            |
| <span data-ttu-id="68f5f-158">3000</span><span class="sxs-lookup"><span data-stu-id="68f5f-158">3000</span></span> | <span data-ttu-id="68f5f-159">30</span><span class="sxs-lookup"><span data-stu-id="68f5f-159">30</span></span>                 | <span data-ttu-id="68f5f-160">2</span><span class="sxs-lookup"><span data-stu-id="68f5f-160">2</span></span>                            |
| <span data-ttu-id="68f5f-161">6000</span><span class="sxs-lookup"><span data-stu-id="68f5f-161">6000</span></span> | <span data-ttu-id="68f5f-162">60</span><span class="sxs-lookup"><span data-stu-id="68f5f-162">60</span></span>                 | <span data-ttu-id="68f5f-163">1</span><span class="sxs-lookup"><span data-stu-id="68f5f-163">1</span></span>                            |

<span data-ttu-id="68f5f-164">Les trois principales fonctions pour la gestion du calcul sont :</span><span class="sxs-lookup"><span data-stu-id="68f5f-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="68f5f-165">Suspendre</span><span class="sxs-lookup"><span data-stu-id="68f5f-165">Pause</span></span>
2. <span data-ttu-id="68f5f-166">Reprendre</span><span class="sxs-lookup"><span data-stu-id="68f5f-166">Resume</span></span>
3. <span data-ttu-id="68f5f-167">Scale</span><span class="sxs-lookup"><span data-stu-id="68f5f-167">Scale</span></span>

<span data-ttu-id="68f5f-168">Chacune de ces opérations peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="68f5f-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="68f5f-169">Si vous effectuez une mise à l’échelle/mise en pause/reprise automatique, il vous faudra peut-être implémenter une logique pour vous assurer que certaines opérations sont bien terminées avant de passer à une autre action.</span><span class="sxs-lookup"><span data-stu-id="68f5f-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="68f5f-170">Nous vous conseillons de vérifier l’état de la base de données en différents points de terminaison afin d’automatiser correctement de telles opérations.</span><span class="sxs-lookup"><span data-stu-id="68f5f-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="68f5f-171">Si le portail vous informe de la fin d’une opération et de l’état actuel des bases de données, il ne vous permet pas de programmer la vérification de l’état.</span><span class="sxs-lookup"><span data-stu-id="68f5f-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="68f5f-172">La fonctionnalité de gestion du calcul n’existe pas sur tous les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="68f5f-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="68f5f-173">Suspendre/Reprendre</span><span class="sxs-lookup"><span data-stu-id="68f5f-173">Pause/Resume</span></span> | <span data-ttu-id="68f5f-174">Scale</span><span class="sxs-lookup"><span data-stu-id="68f5f-174">Scale</span></span> | <span data-ttu-id="68f5f-175">Vérifier l’état de la base de données</span><span class="sxs-lookup"><span data-stu-id="68f5f-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="68f5f-176">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="68f5f-176">Azure portal</span></span> | <span data-ttu-id="68f5f-177">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-177">Yes</span></span>          | <span data-ttu-id="68f5f-178">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-178">Yes</span></span>   | <span data-ttu-id="68f5f-179">**Non**</span><span class="sxs-lookup"><span data-stu-id="68f5f-179">**No**</span></span>               |
| <span data-ttu-id="68f5f-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68f5f-180">PowerShell</span></span>   | <span data-ttu-id="68f5f-181">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-181">Yes</span></span>          | <span data-ttu-id="68f5f-182">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-182">Yes</span></span>   | <span data-ttu-id="68f5f-183">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-183">Yes</span></span>                  |
| <span data-ttu-id="68f5f-184">API REST</span><span class="sxs-lookup"><span data-stu-id="68f5f-184">REST API</span></span>     | <span data-ttu-id="68f5f-185">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-185">Yes</span></span>          | <span data-ttu-id="68f5f-186">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-186">Yes</span></span>   | <span data-ttu-id="68f5f-187">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-187">Yes</span></span>                  |
| <span data-ttu-id="68f5f-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="68f5f-188">T-SQL</span></span>        | <span data-ttu-id="68f5f-189">**Non**</span><span class="sxs-lookup"><span data-stu-id="68f5f-189">**No**</span></span>       | <span data-ttu-id="68f5f-190">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-190">Yes</span></span>   | <span data-ttu-id="68f5f-191">Oui</span><span class="sxs-lookup"><span data-stu-id="68f5f-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="68f5f-192">Mise à l’échelle des ressources de calcul</span><span class="sxs-lookup"><span data-stu-id="68f5f-192">Scale compute</span></span>

<span data-ttu-id="68f5f-193">Les performances dans SQL Data Warehouse se mesurent en [Data Warehouse Units (DWU)][data warehouse units (DWUs)] qui sont une unité abstraite de ressources de calcul (processeur, mémoire et bande passante d’E/S).</span><span class="sxs-lookup"><span data-stu-id="68f5f-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="68f5f-194">Un utilisateur qui souhaite augmenter les performances de son système peut y parvenir de plusieurs façons, par exemple via le portail, T-SQL et les API REST.</span><span class="sxs-lookup"><span data-stu-id="68f5f-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="68f5f-195">Comment mettre à l’échelle les ressources de calcul ?</span><span class="sxs-lookup"><span data-stu-id="68f5f-195">How do I scale compute?</span></span>
<span data-ttu-id="68f5f-196">La puissance de calcul est gérée pour vous par SQL Data Warehouse en modifiant le paramètre DWU.</span><span class="sxs-lookup"><span data-stu-id="68f5f-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="68f5f-197">Les performances augmentent [de manière linéaire][linearly] à mesure que vous ajoutez des DWU pour certaines opérations.</span><span class="sxs-lookup"><span data-stu-id="68f5f-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="68f5f-198">Nous proposons des offres DWU qui vous garantissent une évolution notable de vos performances lorsque vous effectuez une montée ou une descente en puissance de votre système.</span><span class="sxs-lookup"><span data-stu-id="68f5f-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="68f5f-199">Pour ajuster les unités DWU, vous pouvez utiliser l’une des différentes méthodes suivantes.</span><span class="sxs-lookup"><span data-stu-id="68f5f-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="68f5f-200">[Mise à l’échelle de la puissance de calcul avec le portail Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="68f5f-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="68f5f-201">[Mise à l’échelle de la puissance de calcul avec PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="68f5f-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="68f5f-202">[Mise à l’échelle de la puissance de calcul avec les API REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="68f5f-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="68f5f-203">[Mise à l’échelle de la puissance de calcul avec TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="68f5f-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="68f5f-204">Combien d’unités DWU dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="68f5f-204">How many DWUs should I use?</span></span>

<span data-ttu-id="68f5f-205">Pour obtenir votre valeur DWU idéale, essayez d’augmenter et de réduire vos DWU et d’exécuter quelques requêtes après le chargement de vos données.</span><span class="sxs-lookup"><span data-stu-id="68f5f-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="68f5f-206">La mise à l’échelle étant rapide, vous pouvez essayer plusieurs niveaux de performances en une heure ou moins.</span><span class="sxs-lookup"><span data-stu-id="68f5f-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="68f5f-207">SQL Data Warehouse est conçu pour traiter de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="68f5f-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="68f5f-208">Pour étudier ses fonctionnalités de mise à l’échelle, en particulier sur les unités DWU de grande taille, nous vous conseillons d’utiliser un jeu de données qui avoisine ou dépasse 1 To.</span><span class="sxs-lookup"><span data-stu-id="68f5f-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="68f5f-209">Recommandations pour rechercher l’unité DWU la mieux adaptée à votre charge de travail :</span><span class="sxs-lookup"><span data-stu-id="68f5f-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="68f5f-210">Si vous disposez d’un entrepôt de données en développement, commencez par sélectionner un niveau de performances utilisant un nombre réduit d’unités DWU.</span><span class="sxs-lookup"><span data-stu-id="68f5f-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="68f5f-211">DW400 ou DW200 est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="68f5f-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="68f5f-212">Surveillez les performances de votre application, en observant notamment le nombre d’unités DWU sélectionné.</span><span class="sxs-lookup"><span data-stu-id="68f5f-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="68f5f-213">Déterminez le niveau de performances le mieux adapté aux exigences en modulant la capacité de votre système à l’aide d’une mise à l’échelle linéaire.</span><span class="sxs-lookup"><span data-stu-id="68f5f-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="68f5f-214">Augmentez ou diminuez le nombre de DWU en fonction de la performance de charge de travail dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="68f5f-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="68f5f-215">Continuez à effectuer des ajustements jusqu’à ce que vous atteigniez le niveau de performances requis par vos activités.</span><span class="sxs-lookup"><span data-stu-id="68f5f-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="68f5f-216">Si les travaux peuvent être fractionnés entre les nœuds de calcul, les performances des requêtes augmentent uniquement avec une parallélisation renforcée.</span><span class="sxs-lookup"><span data-stu-id="68f5f-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="68f5f-217">Si vous trouvez que la mise à l’échelle ne modifie pas les performances, consultez nos articles sur le réglage des performances et voyez si vos données sont distribuées de manière inégale ou si vous provoquez un déplacement trop important des données.</span><span class="sxs-lookup"><span data-stu-id="68f5f-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="68f5f-218">Quand dois-je mettre les unités DWU à l’échelle ?</span><span class="sxs-lookup"><span data-stu-id="68f5f-218">When should I scale DWUs?</span></span>
<span data-ttu-id="68f5f-219">La mise à l’échelle des unités DWU modifie les principaux scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="68f5f-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="68f5f-220">Modification linéaire des performances du système pour les analyses, les agrégations et les instructions CTAS</span><span class="sxs-lookup"><span data-stu-id="68f5f-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="68f5f-221">Augmentation du nombre de lecteurs et d’auteurs lors du chargement des données avec PolyBase</span><span class="sxs-lookup"><span data-stu-id="68f5f-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="68f5f-222">Nombre maximal de requêtes simultanées et d’emplacements concurrentiels</span><span class="sxs-lookup"><span data-stu-id="68f5f-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="68f5f-223">Recommandations sur le moment approprié pour mettre des unités DWU à l’échelle :</span><span class="sxs-lookup"><span data-stu-id="68f5f-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="68f5f-224">Avant d’exécuter une opération de chargement ou de transformation de données importante, vous pouvez augmenter le nombre d’unités DWU afin que vos données soient disponibles plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="68f5f-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="68f5f-225">Pendant les heures de pointe, envisagez une mise à l’échelle pour prendre en charge un nombre plus important de requêtes simultanées.</span><span class="sxs-lookup"><span data-stu-id="68f5f-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="68f5f-226">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="68f5f-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="68f5f-227">Pour suspendre une base de données, utilisez l’une des différentes méthodes suivantes.</span><span class="sxs-lookup"><span data-stu-id="68f5f-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="68f5f-228">[Suspension du calcul avec le portail Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="68f5f-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="68f5f-229">[Suspension du calcul avec PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="68f5f-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="68f5f-230">[Suspension du calcul avec des API REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="68f5f-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="68f5f-231">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="68f5f-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="68f5f-232">Pour reprendre une base de données, utilisez l’une des différentes méthodes suivantes.</span><span class="sxs-lookup"><span data-stu-id="68f5f-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="68f5f-233">[Reprise du calcul avec le portail Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="68f5f-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="68f5f-234">[Reprise du calcul avec PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="68f5f-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="68f5f-235">[Reprise du calcul avec des API REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="68f5f-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="68f5f-236">Vérifier l’état de la base de données</span><span class="sxs-lookup"><span data-stu-id="68f5f-236">Check database state</span></span> 

<span data-ttu-id="68f5f-237">Pour reprendre une base de données, utilisez l’une des différentes méthodes suivantes.</span><span class="sxs-lookup"><span data-stu-id="68f5f-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="68f5f-238">[Vérifier l’état de la base de données avec T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="68f5f-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="68f5f-239">[Vérifier l’état de la base de données avec PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="68f5f-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="68f5f-240">[Vérifier l’état de la base de données avec les API REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="68f5f-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="68f5f-241">Autorisations</span><span class="sxs-lookup"><span data-stu-id="68f5f-241">Permissions</span></span>

<span data-ttu-id="68f5f-242">La mise à l’échelle de la base de données requiert les autorisations décrites dans [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="68f5f-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="68f5f-243">La suspension et la reprise requièrent l’autorisation [SQL DB Contributor][SQL DB Contributor], notamment Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="68f5f-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="68f5f-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68f5f-244">Next steps</span></span>
<span data-ttu-id="68f5f-245">Consultez les articles suivants pour mieux comprendre certains concepts supplémentaires essentiels en matière de performances :</span><span class="sxs-lookup"><span data-stu-id="68f5f-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="68f5f-246">[Gestion des charges de travail et d’accès concurrentiel][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="68f5f-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="68f5f-247">[Vue d’ensemble de conception de table][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="68f5f-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="68f5f-248">[Distribution de tables][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="68f5f-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="68f5f-249">[Indexation de table][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="68f5f-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="68f5f-250">[Partitionnement de tables][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="68f5f-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="68f5f-251">[Statistiques de table][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="68f5f-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="68f5f-252">[Meilleures pratiques][Best practices]</span><span class="sxs-lookup"><span data-stu-id="68f5f-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
