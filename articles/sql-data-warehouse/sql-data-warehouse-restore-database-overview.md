---
title: "aaaRestore un entrepôt de données Azure - local et géo-redondant | Documents Microsoft"
description: "Vue d’ensemble des options de restauration de base de données hello pour récupérer une base de données dans l’entrepôt de données SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="47aae-103">Restauration SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47aae-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="47aae-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="47aae-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="47aae-105">[Portail][Portal]</span><span class="sxs-lookup"><span data-stu-id="47aae-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="47aae-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="47aae-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="47aae-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="47aae-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="47aae-108">SQL Data Warehouse propose des restaurations locales et géographiques dans le cadre de ses fonctionnalités de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="47aae-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="47aae-109">Utilisez les données entrepôt sauvegardes toorestore votre entrepôt de données tooa restauration point dans la région principale de hello, ou utiliser des sauvegardes géo-redondant toorestore tooa autre région géographique.</span><span class="sxs-lookup"><span data-stu-id="47aae-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="47aae-110">Cet article explique les spécificités de hello de restauration d’un entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="47aae-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="47aae-111">Qu’est-ce qu’une restauration d’entrepôt de données ?</span><span class="sxs-lookup"><span data-stu-id="47aae-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="47aae-112">Une restauration d’entrepôt de données est un nouvel entrepôt de données créé à partir de la sauvegarde d’un entrepôt de données existant ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="47aae-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="47aae-113">l’entrepôt de données restaurées Hello recrée l’entrepôt de données sauvegardées hello à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="47aae-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="47aae-114">Comme SQL Data Warehouse est un système distribué, une restauration d’entrepôt de données est créée à partir de nombreux fichiers de sauvegarde stockés dans des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="47aae-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="47aae-115">La restauration de base de données est une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence, dans la mesure où elle recrée vos données après des corruptions et des suppressions accidentelles.</span><span class="sxs-lookup"><span data-stu-id="47aae-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="47aae-116">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="47aae-116">For more information, see:</span></span>

* [<span data-ttu-id="47aae-117">Sauvegardes SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47aae-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="47aae-118">Vue d’ensemble de la continuité des activités</span><span class="sxs-lookup"><span data-stu-id="47aae-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="47aae-119">Points de restauration SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47aae-119">Data warehouse restore points</span></span>
<span data-ttu-id="47aae-120">Un avantage de l’utilisation du stockage Azure Premium, SQL Data Warehouse utilise entrepôt de données primaire objet Blob de stockage Azure instantanés toobackup hello.</span><span class="sxs-lookup"><span data-stu-id="47aae-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="47aae-121">Chaque instantané dispose d’un point de restauration qui représente l’heure de hello instantané hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="47aae-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="47aae-122">toorestore un entrepôt de données, vous choisissez un point de restauration et émettez une commande de restauration.</span><span class="sxs-lookup"><span data-stu-id="47aae-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="47aae-123">SQL Data Warehouse restaure toujours hello tooa sauvegarde nouvel entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="47aae-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="47aae-124">Vous pouvez conserver l’entrepôt de données restaurées hello et hello actuel ou supprimez l’un d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="47aae-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="47aae-125">Si vous souhaitez tooreplace hello actuel data warehouse avec hello restaurée de l’entrepôt de données, vous pouvez la renommer.</span><span class="sxs-lookup"><span data-stu-id="47aae-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="47aae-126">Si vous avez besoin de toorestore un entrepôt de données supprimées ou en pause, vous pouvez [créer un ticket de support](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="47aae-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="47aae-127">Restauration géoredondante</span><span class="sxs-lookup"><span data-stu-id="47aae-127">Geo-redundant restore</span></span>
<span data-ttu-id="47aae-128">Vous pouvez restaurer votre région tooany de l’entrepôt de données prenant en charge de l’entrepôt de données SQL Azure à un niveau de performance choisis.</span><span class="sxs-lookup"><span data-stu-id="47aae-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="47aae-129">Veuillez noter que 9000 et 18000 DWU ne sont pas pris en charge dans toutes les régions préliminaire hello.</span><span class="sxs-lookup"><span data-stu-id="47aae-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="47aae-130">restauration tooperform une géo-redondant que vous ne devez pas avoir la participation de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="47aae-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="47aae-131">Chronologie de la restauration</span><span class="sxs-lookup"><span data-stu-id="47aae-131">Restore timeline</span></span>
<span data-ttu-id="47aae-132">Vous pouvez restaurer un point de restauration de base de données tooany dans hello sept derniers jours.</span><span class="sxs-lookup"><span data-stu-id="47aae-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="47aae-133">Instantanés de toutes les quatre heures tooeight et sont disponibles pour les sept jours.</span><span class="sxs-lookup"><span data-stu-id="47aae-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="47aae-134">Quand une capture instantanée a une ancienneté supérieure à sept jours, elle expire et son point de restauration n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="47aae-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="47aae-135">Coûts de la restauration</span><span class="sxs-lookup"><span data-stu-id="47aae-135">Restore costs</span></span>
<span data-ttu-id="47aae-136">frais de stockage Hello pour l’entrepôt de données restaurées hello sont facturée au tarif de stockage Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="47aae-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="47aae-137">Si vous suspendez un entrepôt de données restaurées, vous êtes facturé pour le stockage au tarif de stockage Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="47aae-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="47aae-138">Hello de la suspension d’avantage que vous n’êtes pas facturé pour les ressources de calcul DWU hello.</span><span class="sxs-lookup"><span data-stu-id="47aae-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="47aae-139">Pour plus d’informations sur la tarification de SQL Data Warehouse, consultez [SQL Data Warehouse Tarification](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="47aae-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="47aae-140">Utilisations de la restauration</span><span class="sxs-lookup"><span data-stu-id="47aae-140">Uses for restore</span></span>
<span data-ttu-id="47aae-141">Hello principale utilisation de restauration de l’entrepôt de données est toorecover données après la perte accidentelle de données ou d’altération.</span><span class="sxs-lookup"><span data-stu-id="47aae-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="47aae-142">Vous pouvez également utiliser la restauration tooretain une sauvegarde de données entrepôt pendant plus de sept jours.</span><span class="sxs-lookup"><span data-stu-id="47aae-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="47aae-143">Une fois la sauvegarde de hello est restaurée, vous disposez des entrepôt de données hello en ligne et pouvez la suspendre indéfiniment toosave les coûts de calcul.</span><span class="sxs-lookup"><span data-stu-id="47aae-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="47aae-144">base de données en pause Hello entraîne des frais de stockage au tarif de stockage Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="47aae-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="47aae-145">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="47aae-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="47aae-146">Scénarios</span><span class="sxs-lookup"><span data-stu-id="47aae-146">Scenarios</span></span>
* <span data-ttu-id="47aae-147">Pour une vue d’ensemble de la continuité des activités, consultez [Vue d’ensemble de la continuité des activités](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="47aae-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="47aae-148">tooperform un entrepôt de données de restauration, la restauration à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="47aae-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="47aae-149">Azure portail, consultez [restaurer un entrepôt de données à l’aide de hello portail Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="47aae-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="47aae-150">Applets de commande PowerShell : voir [Restaurer un entrepôt de données à l’aide d’applets de commande PowerShell](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="47aae-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="47aae-151">API REST, consultez [restaurer un entrepôt de données à l’aide des API REST de hello](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="47aae-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
