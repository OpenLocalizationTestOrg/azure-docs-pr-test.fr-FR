---
title: "aaaMigrate toopremium stockage de l’entrepôt de données Azure existantes | Documents Microsoft"
description: "Instructions pour la migration des données existantes de l’entrepôt de stockage de toopremium"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="6fa65-103">Migrer votre stockage de toopremium de l’entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="6fa65-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="6fa65-104">Azure SQL Data Warehouse propose depuis peu le [stockage Premium pour améliorer la prévisibilité des performances][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="6fa65-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="6fa65-105">Les données existantes entrepôts actuellement sur le stockage standard peuvent être migré toopremium stockage.</span><span class="sxs-lookup"><span data-stu-id="6fa65-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="6fa65-106">Vous pouvez tirer parti de la migration automatique, ou si vous préférez toocontrol lorsque toomigrate (qui implique aucun temps d’arrêt), vous pouvez effectuer hello migration vous-même.</span><span class="sxs-lookup"><span data-stu-id="6fa65-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="6fa65-107">Si vous avez plusieurs entrepôts de données, utilisez hello [planification de la migration automatique] [ automatic migration schedule] toodetermine lorsqu’elle est également migrée.</span><span class="sxs-lookup"><span data-stu-id="6fa65-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="6fa65-108">Déterminer le type de stockage</span><span class="sxs-lookup"><span data-stu-id="6fa65-108">Determine storage type</span></span>
<span data-ttu-id="6fa65-109">Si vous avez créé un entrepôt de données avant de hello suivant de dates, vous utilisez actuellement le stockage standard.</span><span class="sxs-lookup"><span data-stu-id="6fa65-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="6fa65-110">**Région**</span><span class="sxs-lookup"><span data-stu-id="6fa65-110">**Region**</span></span> | <span data-ttu-id="6fa65-111">**Entrepôt de données créé avant cette date**</span><span class="sxs-lookup"><span data-stu-id="6fa65-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="6fa65-112">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="6fa65-112">Australia East</span></span> |<span data-ttu-id="6fa65-113">Stockage Premium non encore disponible</span><span class="sxs-lookup"><span data-stu-id="6fa65-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="6fa65-114">Chine orientale</span><span class="sxs-lookup"><span data-stu-id="6fa65-114">China East</span></span> |<span data-ttu-id="6fa65-115">1er novembre 2016</span><span class="sxs-lookup"><span data-stu-id="6fa65-115">November 1, 2016</span></span> |
| <span data-ttu-id="6fa65-116">Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="6fa65-116">China North</span></span> |<span data-ttu-id="6fa65-117">1er novembre 2016</span><span class="sxs-lookup"><span data-stu-id="6fa65-117">November 1, 2016</span></span> |
| <span data-ttu-id="6fa65-118">Centre de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="6fa65-118">Germany Central</span></span> |<span data-ttu-id="6fa65-119">1er novembre 2016</span><span class="sxs-lookup"><span data-stu-id="6fa65-119">November 1, 2016</span></span> |
| <span data-ttu-id="6fa65-120">Nord-Est de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="6fa65-120">Germany Northeast</span></span> |<span data-ttu-id="6fa65-121">1er novembre 2016</span><span class="sxs-lookup"><span data-stu-id="6fa65-121">November 1, 2016</span></span> |
| <span data-ttu-id="6fa65-122">Inde-Ouest</span><span class="sxs-lookup"><span data-stu-id="6fa65-122">India West</span></span> |<span data-ttu-id="6fa65-123">Stockage Premium non encore disponible</span><span class="sxs-lookup"><span data-stu-id="6fa65-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="6fa65-124">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="6fa65-124">Japan West</span></span> |<span data-ttu-id="6fa65-125">Stockage Premium non encore disponible</span><span class="sxs-lookup"><span data-stu-id="6fa65-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="6fa65-126">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="6fa65-126">North Central US</span></span> |<span data-ttu-id="6fa65-127">10 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="6fa65-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="6fa65-128">Détails sur la migration automatique</span><span class="sxs-lookup"><span data-stu-id="6fa65-128">Automatic migration details</span></span>
<span data-ttu-id="6fa65-129">Par défaut, nous allons migrer votre base de données pour vous entre 6 h 00 et 6 h 00 heure locale de votre région pendant hello [planification de la migration automatique][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="6fa65-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="6fa65-130">Lors de la migration de hello votre entrepôt de données existant est inutilisable.</span><span class="sxs-lookup"><span data-stu-id="6fa65-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="6fa65-131">migration de Hello prendra environ une heure par téraoctet de stockage par l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="6fa65-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="6fa65-132">Vous ne serez pas facturé au cours d’une partie de la migration automatique hello.</span><span class="sxs-lookup"><span data-stu-id="6fa65-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="6fa65-133">Lors de la migration de hello est terminée, votre entrepôt de données sera précédent en ligne et utilisable.</span><span class="sxs-lookup"><span data-stu-id="6fa65-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="6fa65-134">Microsoft prend hello après la migration de hello toocomplete étapes (ils ne nécessitent pas d’intervention de votre part).</span><span class="sxs-lookup"><span data-stu-id="6fa65-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="6fa65-135">Dans cet exemple, imaginez que votre entrepôt de données sur le stockage standard s’appelle « MyDW ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="6fa65-136">Microsoft renomme « MyDW » trop « MyDW_DO_NOT_USE_ [Timestamp] ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="6fa65-137">Microsoft interrompt « MyDW_ DO_NOT_USE_ [Horodatage] ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="6fa65-138">Une sauvegarde est effectuée pendant ce temps.</span><span class="sxs-lookup"><span data-stu-id="6fa65-138">During this time, a backup is taken.</span></span> <span data-ttu-id="6fa65-139">En cas de problème, il se peut que le processus s’interrompe et se relance plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="6fa65-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="6fa65-140">Microsoft crée un nouvel entrepôt de données nommé « MyDW » sur le stockage premium à partir de la sauvegarde de hello effectuée à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="6fa65-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="6fa65-141">« MyDW » n’apparaissent qu’après que la restauration hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="6fa65-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="6fa65-142">Une fois hello restauré, « MyDW » renvoie toohello unités de l’entrepôt de données mêmes et l’état (actif ou en pause) où elle se trouvait avant la migration de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa65-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="6fa65-143">Une fois la migration de hello terminée, Microsoft supprime « MyDW_DO_NOT_USE_ [Timestamp] ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="6fa65-144">Hello paramètres suivants ne s’appliquent pas dans le cadre de la migration de hello :</span><span class="sxs-lookup"><span data-stu-id="6fa65-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="6fa65-145">L’audit au niveau de base de données hello doit toobe réactivé.</span><span class="sxs-lookup"><span data-stu-id="6fa65-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="6fa65-146">Règles de pare-feu au niveau de base de données hello doivent toobe rajouté.</span><span class="sxs-lookup"><span data-stu-id="6fa65-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="6fa65-147">Règles de pare-feu au niveau du serveur hello ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="6fa65-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="6fa65-148">Planification de la migration automatique</span><span class="sxs-lookup"><span data-stu-id="6fa65-148">Automatic migration schedule</span></span>
<span data-ttu-id="6fa65-149">Migrations automatiques de se produisent entre 6 h 00 et 6 h 00 (heure locale par région) au cours de hello suivant la planification de la panne.</span><span class="sxs-lookup"><span data-stu-id="6fa65-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="6fa65-150">**Région**</span><span class="sxs-lookup"><span data-stu-id="6fa65-150">**Region**</span></span> | <span data-ttu-id="6fa65-151">**Date de début estimée**</span><span class="sxs-lookup"><span data-stu-id="6fa65-151">**Estimated start date**</span></span> | <span data-ttu-id="6fa65-152">**Date de fin estimée**</span><span class="sxs-lookup"><span data-stu-id="6fa65-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6fa65-153">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="6fa65-153">Australia East</span></span> |<span data-ttu-id="6fa65-154">Pas encore déterminée</span><span class="sxs-lookup"><span data-stu-id="6fa65-154">Not determined yet</span></span> |<span data-ttu-id="6fa65-155">Pas encore déterminée</span><span class="sxs-lookup"><span data-stu-id="6fa65-155">Not determined yet</span></span> |
| <span data-ttu-id="6fa65-156">Chine orientale</span><span class="sxs-lookup"><span data-stu-id="6fa65-156">China East</span></span> |<span data-ttu-id="6fa65-157">9 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-157">January 9, 2017</span></span> |<span data-ttu-id="6fa65-158">13 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-158">January 13, 2017</span></span> |
| <span data-ttu-id="6fa65-159">Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="6fa65-159">China North</span></span> |<span data-ttu-id="6fa65-160">9 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-160">January 9, 2017</span></span> |<span data-ttu-id="6fa65-161">13 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-161">January 13, 2017</span></span> |
| <span data-ttu-id="6fa65-162">Centre de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="6fa65-162">Germany Central</span></span> |<span data-ttu-id="6fa65-163">9 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-163">January 9, 2017</span></span> |<span data-ttu-id="6fa65-164">13 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-164">January 13, 2017</span></span> |
| <span data-ttu-id="6fa65-165">Nord-Est de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="6fa65-165">Germany Northeast</span></span> |<span data-ttu-id="6fa65-166">9 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-166">January 9, 2017</span></span> |<span data-ttu-id="6fa65-167">13 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-167">January 13, 2017</span></span> |
| <span data-ttu-id="6fa65-168">Inde-Ouest</span><span class="sxs-lookup"><span data-stu-id="6fa65-168">India West</span></span> |<span data-ttu-id="6fa65-169">Pas encore déterminée</span><span class="sxs-lookup"><span data-stu-id="6fa65-169">Not determined yet</span></span> |<span data-ttu-id="6fa65-170">Pas encore déterminée</span><span class="sxs-lookup"><span data-stu-id="6fa65-170">Not determined yet</span></span> |
| <span data-ttu-id="6fa65-171">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="6fa65-171">Japan West</span></span> |<span data-ttu-id="6fa65-172">Pas encore déterminée</span><span class="sxs-lookup"><span data-stu-id="6fa65-172">Not determined yet</span></span> |<span data-ttu-id="6fa65-173">Pas encore déterminée</span><span class="sxs-lookup"><span data-stu-id="6fa65-173">Not determined yet</span></span> |
| <span data-ttu-id="6fa65-174">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="6fa65-174">North Central US</span></span> |<span data-ttu-id="6fa65-175">9 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-175">January 9, 2017</span></span> |<span data-ttu-id="6fa65-176">13 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="6fa65-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="6fa65-177">Stockage de toopremium la migration automatique.</span><span class="sxs-lookup"><span data-stu-id="6fa65-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="6fa65-178">Si vous souhaitez toocontrol lorsque le temps mort se produit, vous pouvez utiliser hello suivant les étapes toomigrate un entrepôt de données existant sur toopremium de stockage standard.</span><span class="sxs-lookup"><span data-stu-id="6fa65-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="6fa65-179">Si vous choisissez cette option, vous devez effectuer la migration automatique hello avant le début de la migration automatique hello dans cette région.</span><span class="sxs-lookup"><span data-stu-id="6fa65-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="6fa65-180">Cela garantit que vous évitez tout risque de la migration automatique hello provoque un conflit (consultez toohello [planification de la migration automatique][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="6fa65-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="6fa65-181">Instructions relatives à la migration ponctuelle</span><span class="sxs-lookup"><span data-stu-id="6fa65-181">Self-migration instructions</span></span>
<span data-ttu-id="6fa65-182">toomigrate vos données de l’entrepôt vous-même, utilisent hello sauvegarde et restauration fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="6fa65-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="6fa65-183">partie de restauration Hello de migration de hello est attendu tootake environ une heure par téraoctet de stockage par l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="6fa65-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="6fa65-184">Si vous souhaitez hello tookeep même nom une fois la migration terminée, suivez hello [toorename d’étapes lors de la migration][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="6fa65-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="6fa65-185">[Suspendez][Pause] votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="6fa65-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="6fa65-186">Cela déclenche une sauvegarde automatique.</span><span class="sxs-lookup"><span data-stu-id="6fa65-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="6fa65-187">[Effectuez une restauration][Restore] à partir de votre instantané le plus récent.</span><span class="sxs-lookup"><span data-stu-id="6fa65-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="6fa65-188">Supprimez votre entrepôt de données sur le stockage standard.</span><span class="sxs-lookup"><span data-stu-id="6fa65-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="6fa65-189">**Si vous ne parvenez pas toodo cette étape, vous serez facturé pour les entrepôts de données.**</span><span class="sxs-lookup"><span data-stu-id="6fa65-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="6fa65-190">Hello paramètres suivants ne s’appliquent pas dans le cadre de la migration de hello :</span><span class="sxs-lookup"><span data-stu-id="6fa65-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="6fa65-191">L’audit au niveau de base de données hello doit toobe réactivé.</span><span class="sxs-lookup"><span data-stu-id="6fa65-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="6fa65-192">Règles de pare-feu au niveau de base de données hello doivent toobe rajouté.</span><span class="sxs-lookup"><span data-stu-id="6fa65-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="6fa65-193">Règles de pare-feu au niveau du serveur hello ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="6fa65-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="6fa65-194">Renommer l’entrepôt de données pendant la migration (facultatif)</span><span class="sxs-lookup"><span data-stu-id="6fa65-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="6fa65-195">Deux bases de données sur le même serveur logique ne peut pas avoir de hello hello le même nom.</span><span class="sxs-lookup"><span data-stu-id="6fa65-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="6fa65-196">Entrepôt de données SQL prend désormais en charge la possibilité de hello toorename un entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="6fa65-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="6fa65-197">Dans cet exemple, imaginez que votre entrepôt de données sur le stockage standard s’appelle « MyDW ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="6fa65-198">Renommez « MyDW » à l’aide de hello suivant de la commande ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="6fa65-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="6fa65-199">(Dans cet exemple, nous allons renommer « MyDW_BeforeMigration ».)  Cette commande arrête toutes les transactions existantes et doit être effectuée dans toosucceed de base de données master hello.</span><span class="sxs-lookup"><span data-stu-id="6fa65-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="6fa65-200">[Suspendez][Pause] « MyDW_BeforeMigration ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="6fa65-201">Cela déclenche une sauvegarde automatique.</span><span class="sxs-lookup"><span data-stu-id="6fa65-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="6fa65-202">[Restaurer] [ Restore] à partir d’une base de données avec le nom de hello votre instantané le plus récent, il utilisé toobe (par exemple, « MyDW »).</span><span class="sxs-lookup"><span data-stu-id="6fa65-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="6fa65-203">Supprimez « MyDW_BeforeMigration ».</span><span class="sxs-lookup"><span data-stu-id="6fa65-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="6fa65-204">**Si vous ne parvenez pas toodo cette étape, vous serez facturé pour les entrepôts de données.**</span><span class="sxs-lookup"><span data-stu-id="6fa65-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="6fa65-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fa65-205">Next steps</span></span>
<span data-ttu-id="6fa65-206">Hello modifier toopremium stockage, vous avez également un nombre accru de fichiers de base de données blob dans l’architecture sous-jacente de hello de votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="6fa65-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="6fa65-207">toomaximize des gains de performance hello de cette modification, reconstruisez les index columnstore en cluster à l’aide de hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="6fa65-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="6fa65-208">script de Hello fonctionne en forçant certaines de vos objets supplémentaires BLOB de données toohello existante.</span><span class="sxs-lookup"><span data-stu-id="6fa65-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="6fa65-209">Si vous ne prenez aucune action, les données de salutation redistribue naturellement au fil du temps comme vous chargez davantage de données dans vos tables.</span><span class="sxs-lookup"><span data-stu-id="6fa65-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="6fa65-210">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="6fa65-210">**Prerequisites:**</span></span>

- <span data-ttu-id="6fa65-211">Hello l’entrepôt de données doit s’exécuter avec des unités de l’entrepôt de données 1 000 ou plus (voir [montée en puissance de calcul power][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="6fa65-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="6fa65-212">utilisateur qui exécute le script de hello Hello doit être Bonjour [mediumrc rôle] [ mediumrc role] ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6fa65-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="6fa65-213">tooadd un rôle d’utilisateur toothis, exécutez la commande suivante hello :````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="6fa65-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="6fa65-214">Si vous rencontrez des problèmes avec votre entrepôt de données, [créer un ticket de support] [ create a support ticket] et faire référence à la migration toopremium « stockage » comme cause possible de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa65-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
