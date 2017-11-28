---
title: "aaaManage de calcul power dans l’entrepôt de données SQL Azure (aperçu) | Documents Microsoft"
description: "Capacités de montée en puissance des performances dans Azure SQL Data Warehouse. Montée en puissance parallèle en ajustant les Dwu ou suspendre et reprendre les coûts toosave de ressources de calcul."
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
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="afafa-104">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (Vue d’ensemble)</span><span class="sxs-lookup"><span data-stu-id="afafa-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afafa-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="afafa-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="afafa-106">Portail</span><span class="sxs-lookup"><span data-stu-id="afafa-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="afafa-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afafa-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="afafa-108">REST</span><span class="sxs-lookup"><span data-stu-id="afafa-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="afafa-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="afafa-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="afafa-110">architecture Hello de SQL Data Warehouse sépare le stockage et calcul, ce qui permet de chaque tooscale indépendamment.</span><span class="sxs-lookup"><span data-stu-id="afafa-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="afafa-111">Par conséquent, le calcul peut être les demandes de performances toomeet à l’échelle indépendante de la quantité de hello de données.</span><span class="sxs-lookup"><span data-stu-id="afafa-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="afafa-112">Une conséquence naturelle de cette architecture est la séparation de la [facturation][billed] du calcul et du stockage.</span><span class="sxs-lookup"><span data-stu-id="afafa-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="afafa-113">Cette présentation décrit comment monter en charge fonctionne avec SQL Data Warehouse et comment tooutilize hello suspendre, reprendre et des fonctionnalités de mise à l’échelle de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="afafa-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="afafa-114">Consultez hello [unités (Dwu) de l’entrepôt de données] [ data warehouse units (DWUs)] toolearn page Comment Dwu et les performances sont liés.</span><span class="sxs-lookup"><span data-stu-id="afafa-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="afafa-115">Fonctionnement des opérations de gestion du calcul dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="afafa-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="afafa-116">architecture Hello pour SQL Data Warehouse se compose d’un nœud de contrôle, le calcul des nœuds et une couche de stockage hello réparties sur les 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="afafa-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="afafa-117">Pendant une session active normale dans l’entrepôt de données SQL, nœud de tête de votre système gère les métadonnées hello et contient l’optimiseur de requête hello distribué.</span><span class="sxs-lookup"><span data-stu-id="afafa-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="afafa-118">Sous ce nœud principal, se trouvent les nœuds de calcul et la couche de stockage.</span><span class="sxs-lookup"><span data-stu-id="afafa-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="afafa-119">Pour une 400 DWU, votre système a un nœud principal, quatre nœuds de calcul et couche de stockage hello, consistant à 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="afafa-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="afafa-120">Lorsque vous subir une échelle ou interrompez l’opération, système de hello tout d’abord supprime toutes les requêtes entrantes et restaure les transactions tooensure un état cohérent.</span><span class="sxs-lookup"><span data-stu-id="afafa-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="afafa-121">La mise à l’échelle intervient uniquement une fois la restauration des transactions effectuée.</span><span class="sxs-lookup"><span data-stu-id="afafa-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="afafa-122">Pour une opération de montée en puissance parallèle, les dispositions de système de hello hello du nombre de nœuds de calcul supplémentaire souhaité et commence ensuite le rattachement de couche de stockage toohello hello calcul nœuds.</span><span class="sxs-lookup"><span data-stu-id="afafa-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="afafa-123">Pour une opération de réduction, hello nœuds inutiles sont publiées et autres nœuds de calcul hello eux-mêmes rattachement toohello le nombre approprié de distributions.</span><span class="sxs-lookup"><span data-stu-id="afafa-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="afafa-124">Pour une opération de pause, toutes les calcul nœuds sont publiées et votre système est soumises à une variété de tooleave des opérations de métadonnées de votre système final dans un état stable.</span><span class="sxs-lookup"><span data-stu-id="afafa-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="afafa-125">DWU</span><span class="sxs-lookup"><span data-stu-id="afafa-125">DWU</span></span>  | <span data-ttu-id="afafa-126">\# de nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="afafa-126">\#of compute nodes</span></span> | <span data-ttu-id="afafa-127">\# de distributions par nœud</span><span class="sxs-lookup"><span data-stu-id="afafa-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="afafa-128">100</span><span class="sxs-lookup"><span data-stu-id="afafa-128">100</span></span>  | <span data-ttu-id="afafa-129">1</span><span class="sxs-lookup"><span data-stu-id="afafa-129">1</span></span>                  | <span data-ttu-id="afafa-130">60</span><span class="sxs-lookup"><span data-stu-id="afafa-130">60</span></span>                           |
| <span data-ttu-id="afafa-131">200</span><span class="sxs-lookup"><span data-stu-id="afafa-131">200</span></span>  | <span data-ttu-id="afafa-132">2</span><span class="sxs-lookup"><span data-stu-id="afafa-132">2</span></span>                  | <span data-ttu-id="afafa-133">30</span><span class="sxs-lookup"><span data-stu-id="afafa-133">30</span></span>                           |
| <span data-ttu-id="afafa-134">300</span><span class="sxs-lookup"><span data-stu-id="afafa-134">300</span></span>  | <span data-ttu-id="afafa-135">3</span><span class="sxs-lookup"><span data-stu-id="afafa-135">3</span></span>                  | <span data-ttu-id="afafa-136">20</span><span class="sxs-lookup"><span data-stu-id="afafa-136">20</span></span>                           |
| <span data-ttu-id="afafa-137">400</span><span class="sxs-lookup"><span data-stu-id="afafa-137">400</span></span>  | <span data-ttu-id="afafa-138">4</span><span class="sxs-lookup"><span data-stu-id="afafa-138">4</span></span>                  | <span data-ttu-id="afafa-139">15</span><span class="sxs-lookup"><span data-stu-id="afafa-139">15</span></span>                           |
| <span data-ttu-id="afafa-140">500</span><span class="sxs-lookup"><span data-stu-id="afafa-140">500</span></span>  | <span data-ttu-id="afafa-141">5</span><span class="sxs-lookup"><span data-stu-id="afafa-141">5</span></span>                  | <span data-ttu-id="afafa-142">12</span><span class="sxs-lookup"><span data-stu-id="afafa-142">12</span></span>                           |
| <span data-ttu-id="afafa-143">600</span><span class="sxs-lookup"><span data-stu-id="afafa-143">600</span></span>  | <span data-ttu-id="afafa-144">6</span><span class="sxs-lookup"><span data-stu-id="afafa-144">6</span></span>                  | <span data-ttu-id="afafa-145">10</span><span class="sxs-lookup"><span data-stu-id="afafa-145">10</span></span>                           |
| <span data-ttu-id="afafa-146">1 000</span><span class="sxs-lookup"><span data-stu-id="afafa-146">1000</span></span> | <span data-ttu-id="afafa-147">10</span><span class="sxs-lookup"><span data-stu-id="afafa-147">10</span></span>                 | <span data-ttu-id="afafa-148">6</span><span class="sxs-lookup"><span data-stu-id="afafa-148">6</span></span>                            |
| <span data-ttu-id="afafa-149">1 200</span><span class="sxs-lookup"><span data-stu-id="afafa-149">1200</span></span> | <span data-ttu-id="afafa-150">12</span><span class="sxs-lookup"><span data-stu-id="afafa-150">12</span></span>                 | <span data-ttu-id="afafa-151">5</span><span class="sxs-lookup"><span data-stu-id="afafa-151">5</span></span>                            |
| <span data-ttu-id="afafa-152">1 500</span><span class="sxs-lookup"><span data-stu-id="afafa-152">1500</span></span> | <span data-ttu-id="afafa-153">15</span><span class="sxs-lookup"><span data-stu-id="afafa-153">15</span></span>                 | <span data-ttu-id="afafa-154">4</span><span class="sxs-lookup"><span data-stu-id="afafa-154">4</span></span>                            |
| <span data-ttu-id="afafa-155">2000</span><span class="sxs-lookup"><span data-stu-id="afafa-155">2000</span></span> | <span data-ttu-id="afafa-156">20</span><span class="sxs-lookup"><span data-stu-id="afafa-156">20</span></span>                 | <span data-ttu-id="afafa-157">3</span><span class="sxs-lookup"><span data-stu-id="afafa-157">3</span></span>                            |
| <span data-ttu-id="afafa-158">3000</span><span class="sxs-lookup"><span data-stu-id="afafa-158">3000</span></span> | <span data-ttu-id="afafa-159">30</span><span class="sxs-lookup"><span data-stu-id="afafa-159">30</span></span>                 | <span data-ttu-id="afafa-160">2</span><span class="sxs-lookup"><span data-stu-id="afafa-160">2</span></span>                            |
| <span data-ttu-id="afafa-161">6000</span><span class="sxs-lookup"><span data-stu-id="afafa-161">6000</span></span> | <span data-ttu-id="afafa-162">60</span><span class="sxs-lookup"><span data-stu-id="afafa-162">60</span></span>                 | <span data-ttu-id="afafa-163">1</span><span class="sxs-lookup"><span data-stu-id="afafa-163">1</span></span>                            |

<span data-ttu-id="afafa-164">trois fonctions principales Hello pour la gestion de compute sont :</span><span class="sxs-lookup"><span data-stu-id="afafa-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="afafa-165">Suspendre</span><span class="sxs-lookup"><span data-stu-id="afafa-165">Pause</span></span>
2. <span data-ttu-id="afafa-166">Reprendre</span><span class="sxs-lookup"><span data-stu-id="afafa-166">Resume</span></span>
3. <span data-ttu-id="afafa-167">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="afafa-167">Scale</span></span>

<span data-ttu-id="afafa-168">Chacune de ces opérations peut-être prendre plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="afafa-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="afafa-169">Si vous êtes mise à l’échelle, suspension/reprise automatiquement, vous souhaiterez tooensure de logique de tooimplement que certaines opérations ont été effectuées avant de procéder à une autre action.</span><span class="sxs-lookup"><span data-stu-id="afafa-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="afafa-170">Vérification de l’état de base de données hello via différents points de terminaison vous permettra de toocorrectly implémenter l’automatisation de ces opérations.</span><span class="sxs-lookup"><span data-stu-id="afafa-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="afafa-171">portail de Hello fournira une notification à la fin d’un état actuel de bases de données opération et hello mais n’autorise pas de vérification de la programmation de l’état.</span><span class="sxs-lookup"><span data-stu-id="afafa-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="afafa-172">La fonctionnalité de gestion du calcul n’existe pas sur tous les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="afafa-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="afafa-173">Suspendre/Reprendre</span><span class="sxs-lookup"><span data-stu-id="afafa-173">Pause/Resume</span></span> | <span data-ttu-id="afafa-174">Scale</span><span class="sxs-lookup"><span data-stu-id="afafa-174">Scale</span></span> | <span data-ttu-id="afafa-175">Vérifier l’état de la base de données</span><span class="sxs-lookup"><span data-stu-id="afafa-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="afafa-176">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="afafa-176">Azure portal</span></span> | <span data-ttu-id="afafa-177">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-177">Yes</span></span>          | <span data-ttu-id="afafa-178">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-178">Yes</span></span>   | <span data-ttu-id="afafa-179">**Non**</span><span class="sxs-lookup"><span data-stu-id="afafa-179">**No**</span></span>               |
| <span data-ttu-id="afafa-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afafa-180">PowerShell</span></span>   | <span data-ttu-id="afafa-181">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-181">Yes</span></span>          | <span data-ttu-id="afafa-182">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-182">Yes</span></span>   | <span data-ttu-id="afafa-183">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-183">Yes</span></span>                  |
| <span data-ttu-id="afafa-184">API REST</span><span class="sxs-lookup"><span data-stu-id="afafa-184">REST API</span></span>     | <span data-ttu-id="afafa-185">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-185">Yes</span></span>          | <span data-ttu-id="afafa-186">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-186">Yes</span></span>   | <span data-ttu-id="afafa-187">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-187">Yes</span></span>                  |
| <span data-ttu-id="afafa-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="afafa-188">T-SQL</span></span>        | <span data-ttu-id="afafa-189">**Non**</span><span class="sxs-lookup"><span data-stu-id="afafa-189">**No**</span></span>       | <span data-ttu-id="afafa-190">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-190">Yes</span></span>   | <span data-ttu-id="afafa-191">Oui</span><span class="sxs-lookup"><span data-stu-id="afafa-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="afafa-192">Mise à l’échelle des ressources de calcul</span><span class="sxs-lookup"><span data-stu-id="afafa-192">Scale compute</span></span>

<span data-ttu-id="afafa-193">Les performances dans SQL Data Warehouse se mesurent en [Data Warehouse Units (DWU)][data warehouse units (DWUs)] qui sont une unité abstraite de ressources de calcul (processeur, mémoire et bande passante d’E/S).</span><span class="sxs-lookup"><span data-stu-id="afafa-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="afafa-194">Un utilisateur qui souhaite tooscale les performances de leur système pouvez le faire par différents moyens, par exemple via le portail de hello, T-SQL et les API REST.</span><span class="sxs-lookup"><span data-stu-id="afafa-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="afafa-195">Comment mettre à l’échelle les ressources de calcul ?</span><span class="sxs-lookup"><span data-stu-id="afafa-195">How do I scale compute?</span></span>
<span data-ttu-id="afafa-196">La puissance de calcul est gérée pour vous SQL Data Warehouse en modifiant la valeur dwu hello.</span><span class="sxs-lookup"><span data-stu-id="afafa-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="afafa-197">Les performances augmentent [de manière linéaire][linearly] à mesure que vous ajoutez des DWU pour certaines opérations.</span><span class="sxs-lookup"><span data-stu-id="afafa-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="afafa-198">Nous proposons des offres DWU qui vous garantissent une évolution notable de vos performances lorsque vous effectuez une montée ou une descente en puissance de votre système.</span><span class="sxs-lookup"><span data-stu-id="afafa-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="afafa-199">tooadjust Dwu, vous pouvez utiliser une de ces méthodes individuelles.</span><span class="sxs-lookup"><span data-stu-id="afafa-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="afafa-200">[Mise à l’échelle de la puissance de calcul avec le portail Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="afafa-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="afafa-201">[Mise à l’échelle de la puissance de calcul avec PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="afafa-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="afafa-202">[Mise à l’échelle de la puissance de calcul avec les API REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="afafa-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="afafa-203">[Mise à l’échelle de la puissance de calcul avec TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="afafa-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="afafa-204">Combien d’unités DWU dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="afafa-204">How many DWUs should I use?</span></span>

<span data-ttu-id="afafa-205">toounderstand votre valeur DWU idéale est, essayez d’et vers le bas jusqu'à la mise à l’échelle et des requêtes en cours d’exécution après le chargement de vos données.</span><span class="sxs-lookup"><span data-stu-id="afafa-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="afafa-206">La mise à l’échelle étant rapide, vous pouvez essayer plusieurs niveaux de performances en une heure ou moins.</span><span class="sxs-lookup"><span data-stu-id="afafa-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="afafa-207">Entrepôt de données SQL est conçu tooprocess de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="afafa-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="afafa-208">toosee ses fonctionnalités trues pour la mise à l’échelle, surtout au plus grand Dwu, que vous souhaitez toouse un jeu de données volumineux qui approche ou dépasse 1 To.</span><span class="sxs-lookup"><span data-stu-id="afafa-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="afafa-209">Recommandations relatives à la recherche hello meilleures DWU de votre charge de travail :</span><span class="sxs-lookup"><span data-stu-id="afafa-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="afafa-210">Si vous disposez d’un entrepôt de données en développement, commencez par sélectionner un niveau de performances utilisant un nombre réduit d’unités DWU.</span><span class="sxs-lookup"><span data-stu-id="afafa-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="afafa-211">DW400 ou DW200 est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="afafa-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="afafa-212">Surveiller les performances de votre application, en observant nombre hello de Dwu sélectionné par rapport performances toohello que vous observez.</span><span class="sxs-lookup"><span data-stu-id="afafa-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="afafa-213">Déterminez la quantité accélérer ou ralentir les performances pour vous tooreach hello niveau de performance optimal pour les besoins de votre par en supposant que l’échelle linéaire.</span><span class="sxs-lookup"><span data-stu-id="afafa-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="afafa-214">Augmentez ou diminuez le nombre de hello Dwu dans toohow proportion beaucoup plus rapide ou plus lent vous voulez tooperform de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="afafa-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="afafa-215">Continuez à effectuer des ajustements jusqu’à ce que vous atteigniez le niveau de performances requis par vos activités.</span><span class="sxs-lookup"><span data-stu-id="afafa-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="afafa-216">Performances des requêtes augmentent avec plus de parallélisation uniquement si le travail de hello peut être répartis entre les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="afafa-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="afafa-217">Si vous trouvez que la mise à l’échelle ne change pas les performances, consultez nos articles toocheck si vos données sont distribuées inégalement ou si vous introduisez une grande quantité de déplacement des données de réglage des performances.</span><span class="sxs-lookup"><span data-stu-id="afafa-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="afafa-218">Quand dois-je mettre les unités DWU à l’échelle ?</span><span class="sxs-lookup"><span data-stu-id="afafa-218">When should I scale DWUs?</span></span>
<span data-ttu-id="afafa-219">Mise à l’échelle Dwu modifie hello scénarios importants suivants :</span><span class="sxs-lookup"><span data-stu-id="afafa-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="afafa-220">Modification linéaire des performances du système hello pour les analyses, les agrégations et les instructions de SACT</span><span class="sxs-lookup"><span data-stu-id="afafa-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="afafa-221">Nombre de hello croissant de lecteurs et writers lors du chargement avec PolyBase</span><span class="sxs-lookup"><span data-stu-id="afafa-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="afafa-222">Nombre maximal de requêtes simultanées et d’emplacements concurrentiels</span><span class="sxs-lookup"><span data-stu-id="afafa-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="afafa-223">Quand tooscale Dwu :</span><span class="sxs-lookup"><span data-stu-id="afafa-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="afafa-224">Avant d’exécuter une opération de chargement ou de transformation de données importante, vous pouvez augmenter le nombre d’unités DWU afin que vos données soient disponibles plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="afafa-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="afafa-225">Pendant les heures de pointe, l’échelle tooaccommodate plus grand nombre de requêtes simultanées.</span><span class="sxs-lookup"><span data-stu-id="afafa-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="afafa-226">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="afafa-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="afafa-227">toopause une base de données, utilisez une de ces méthodes individuelles.</span><span class="sxs-lookup"><span data-stu-id="afafa-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="afafa-228">[Suspension du calcul avec le portail Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="afafa-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="afafa-229">[Suspension du calcul avec PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="afafa-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="afafa-230">[Suspension du calcul avec des API REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="afafa-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="afafa-231">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="afafa-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="afafa-232">tooresume une base de données, utilisez une de ces méthodes individuelles.</span><span class="sxs-lookup"><span data-stu-id="afafa-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="afafa-233">[Reprise du calcul avec le portail Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="afafa-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="afafa-234">[Reprise du calcul avec PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="afafa-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="afafa-235">[Reprise du calcul avec des API REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="afafa-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="afafa-236">Vérifier l’état de base de données</span><span class="sxs-lookup"><span data-stu-id="afafa-236">Check database state</span></span> 

<span data-ttu-id="afafa-237">tooresume une base de données, utilisez une de ces méthodes individuelles.</span><span class="sxs-lookup"><span data-stu-id="afafa-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="afafa-238">[Vérifier l’état de la base de données avec T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="afafa-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="afafa-239">[Vérifier l’état de la base de données avec PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="afafa-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="afafa-240">[Vérifier l’état de la base de données avec les API REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="afafa-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="afafa-241">Autorisations</span><span class="sxs-lookup"><span data-stu-id="afafa-241">Permissions</span></span>

<span data-ttu-id="afafa-242">Base de données de mise à l’échelle hello nécessite des autorisations de hello décrites dans [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="afafa-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="afafa-243">Suspendre et reprendre nécessitent hello [SQL DB collaborateur] [ SQL DB Contributor] autorisation, spécifiquement Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="afafa-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="afafa-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="afafa-244">Next steps</span></span>
<span data-ttu-id="afafa-245">Consultez toohello suivant toohelp articles vous comprenez certains concepts de performance clés supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="afafa-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="afafa-246">[Gestion des charges de travail et d’accès concurrentiel][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="afafa-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="afafa-247">[Vue d’ensemble de conception de table][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="afafa-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="afafa-248">[Distribution de tables][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="afafa-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="afafa-249">[Indexation de table][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="afafa-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="afafa-250">[Partitionnement de tables][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="afafa-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="afafa-251">[Statistiques de table][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="afafa-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="afafa-252">[Meilleures pratiques][Best practices]</span><span class="sxs-lookup"><span data-stu-id="afafa-252">[Best practices][Best practices]</span></span>

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
