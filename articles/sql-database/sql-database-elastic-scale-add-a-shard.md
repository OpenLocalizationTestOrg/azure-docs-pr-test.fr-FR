---
title: "Ajout d’une partition à l’aide des outils de base de données élastique | Microsoft Docs"
description: "Utilisation des API avec infrastructure élastique pour ajouter de nouvelles partitions à un ensemble de partitions."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6a91ea2251ea3b748faba5c97765bfded9c00234
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="50a99-103">Ajout d’une partition à l’aide des outils de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="50a99-103">Adding a shard using Elastic Database tools</span></span>
## <a name="to-add-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="50a99-104">Pour ajouter une partition pour une nouvelle plage ou clé</span><span class="sxs-lookup"><span data-stu-id="50a99-104">To add a shard for a new range or key</span></span>
<span data-ttu-id="50a99-105">Souvent, les applications n'ont qu'à ajouter de nouvelles partitions pour gérer des données prévues à partir de nouvelles clés ou plages de clés, pour une carte de partitions qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="50a99-105">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="50a99-106">Par exemple, une application partitionnée par un ID de client peut requérir l'approvisionnement d'une nouvelle partition pour un nouveau client, ou des données partitionnées mensuellement peuvent requérir l'approvisionnement d'une nouvelle partition avant le début de chaque mois.</span><span class="sxs-lookup"><span data-stu-id="50a99-106">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="50a99-107">Si la nouvelle plage de valeurs de clé n’appartient pas déjà à un mappage existant, il est très simple d’ajouter la nouvelle partition et d’associer la nouvelle clé ou la plage à cette partition.</span><span class="sxs-lookup"><span data-stu-id="50a99-107">If the new range of key values is not already part of an existing mapping, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a><span data-ttu-id="50a99-108">Exemple : ajout d’une partition et de sa plage à une carte de partition existante</span><span class="sxs-lookup"><span data-stu-id="50a99-108">Example:  adding a shard and its range to an existing shard map</span></span>
<span data-ttu-id="50a99-109">Cet exemple utilise les méthodes [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx), [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx) et [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)), et crée une instance de la classe [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.).</span><span class="sxs-lookup"><span data-stu-id="50a99-109">This sample uses the [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) the [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of the [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="50a99-110">Dans l’exemple ci-dessous, une base de données nommée **sample_shard_2** et tous les objets de schéma nécessaires qu’elle contient ont été créés pour contenir la plage [300, 400).</span><span class="sxs-lookup"><span data-stu-id="50a99-110">In the sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created to hold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create the mapping and associate it with the new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="50a99-111">Comme alternative, vous pouvez utiliser PowerShell pour créer un gestionnaire de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="50a99-111">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="50a99-112">Un exemple est disponible [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="50a99-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="50a99-113">Pour ajouter une partition pour une partie vide d’une plage existante</span><span class="sxs-lookup"><span data-stu-id="50a99-113">To add a shard for an empty part of an existing range</span></span>
<span data-ttu-id="50a99-114">Il peut arriver que vous ayez déjà mappé une plage à une partition et l’ayez partiellement remplie avec des données, mais que vous souhaitiez maintenant que les données futures soient dirigées vers une autre partition.</span><span class="sxs-lookup"><span data-stu-id="50a99-114">In some circumstances, you may have already mapped a range to a shard and partially filled it with data, but you now want upcoming data to be directed to a different shard.</span></span> <span data-ttu-id="50a99-115">Par exemple, vous partitionnez par plage de jours et avez déjà alloué 50 jours à une partition, mais le jour 24, vous souhaitez que les données futures soient dirigées vers une autre partition.</span><span class="sxs-lookup"><span data-stu-id="50a99-115">For example, you shard by day range and have already allocated 50 days to a shard, but on day 24, you want future data to land in a different shard.</span></span> <span data-ttu-id="50a99-116">[L’outil de fusion et de fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) de la base de données élastique peut effectuer cette opération, mais s’il n’est pas nécessaire de déplacer des données (par exemple, les données de la plage de jours [25, 50), c’est-à-dire le jour 25 inclus et le jour 50 exclu, qui n’existe pas encore) vous pouvez effectuer cela entièrement en utilisant directement les API de gestion de carte de partition.</span><span class="sxs-lookup"><span data-stu-id="50a99-116">The elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for the range of days [25, 50), i.e., day 25 inclusive to 50 exclusive, does not yet exist) you can perform this entirely using the Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a><span data-ttu-id="50a99-117">Exemple : fractionnement d’une plage et affectation de la partie vide dans une partition nouvellement ajoutée</span><span class="sxs-lookup"><span data-stu-id="50a99-117">Example: splitting a range and assigning the empty portion to a newly-added shard</span></span>
<span data-ttu-id="50a99-118">Une base de données nommée « sample_shard_2 » et tous les objets de schéma nécessaires qu’elle contient ont été créés.</span><span class="sxs-lookup"><span data-stu-id="50a99-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split the Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) to different shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline to a different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="50a99-119">**Important** : utilisez cette technique seulement si vous êtes certain que la plage de la carte mise à jour est vide.</span><span class="sxs-lookup"><span data-stu-id="50a99-119">**Important**:  Use this technique only if you are certain that the range for the updated mapping is empty.</span></span>  <span data-ttu-id="50a99-120">Les méthodes ci-dessus ne vérifient pas les données de la plage déplacée, il est donc préférable d’inclure des vérifications dans votre code.</span><span class="sxs-lookup"><span data-stu-id="50a99-120">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>  <span data-ttu-id="50a99-121">S’il existe des lignes dans la plage déplacée, la distribution des données réelle ne correspondra pas à la carte des partitions mise à jour.</span><span class="sxs-lookup"><span data-stu-id="50a99-121">If rows exist in the range being moved, the actual data distribution will not match the updated shard map.</span></span> <span data-ttu-id="50a99-122">Utilisez [l’outil de fusion et de fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) pour effectuer cette opération, au lieu de le faire dans ces cases.</span><span class="sxs-lookup"><span data-stu-id="50a99-122">Use the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) to perform the operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

