---
title: "aaaAdding une partition à l’aide des outils de base de données élastique | Documents Microsoft"
description: "Comment toouse API infrastructure élastique tooadd nouvelle partitions tooa partition définie."
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
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="638ea-103">Ajout d’une partition à l’aide des outils de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="638ea-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="638ea-104">tooadd une partition pour une nouvelle plage ou une clé</span><span class="sxs-lookup"><span data-stu-id="638ea-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="638ea-105">Applications souvent besoin toosimply ajouter de nouvelles partitions toohandle données qui sont attendues de nouvelles clés ou des plages de clés pour une carte de partitions qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="638ea-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="638ea-106">Par exemple, une application partitionnée par ID client peut-être tooprovision une nouvelle partition pour un nouveau client, ou mensuelle partitionnée de données peut-être une nouvelle partition configurée avant le début de hello de chaque nouveau mois.</span><span class="sxs-lookup"><span data-stu-id="638ea-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="638ea-107">Si hello nouvelle plage de valeurs de clé n’est pas déjà partie d’un mappage existant, il est très simple tooadd hello nouvelle partition et associer hello nouvelle clé ou une plage toothat partition.</span><span class="sxs-lookup"><span data-stu-id="638ea-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="638ea-108">Exemple : ajout d’une partition et sa table de partition range tooan existant</span><span class="sxs-lookup"><span data-stu-id="638ea-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="638ea-109">Cet exemple utilise hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) méthodes et crée une instance de hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe.</span><span class="sxs-lookup"><span data-stu-id="638ea-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="638ea-110">Dans l’exemple hello ci-dessous, une base de données nommée **sample_shard_2** et tous les objets de schéma nécessaires à l’intérieur ont été créées toohold plage [300, 400).</span><span class="sxs-lookup"><span data-stu-id="638ea-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="638ea-111">En guise d’alternative, vous pouvez utiliser Powershell toocreate un nouveau gestionnaire de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="638ea-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="638ea-112">Un exemple est disponible [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="638ea-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="638ea-113">tooadd une partition pour une partie vide d’une plage existante</span><span class="sxs-lookup"><span data-stu-id="638ea-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="638ea-114">Dans certains cas, vous avez déjà mappée une partition tooa de plage et partiellement avec des données, mais vous souhaitez maintenant différentes partitions de données à venir toobe tooa dirigée.</span><span class="sxs-lookup"><span data-stu-id="638ea-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="638ea-115">Par exemple, vous partitions par jour de plage et avez déjà alloué partition tooa de 50 jours, mais le jour 24, que vous souhaitez tooland ultérieure de données dans une autre partition.</span><span class="sxs-lookup"><span data-stu-id="638ea-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="638ea-116">base de données élastique Hello [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) peuvent effectuer cette opération, mais si le déplacement des données n’est pas nécessaire (par exemple, les données de la plage de hello de jours [25, 50), c'est-à-dire, too50 inclusive de jour 25 exclusive, n’existe pas encore) que vous pouvez effectuer Cette exclusivement à l’aide de hello directement API de gestion de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="638ea-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="638ea-117">Exemple : fractionnement d’une plage et l’affectation de hello vide partitions de nouvellement ajouté tooa partie</span><span class="sxs-lookup"><span data-stu-id="638ea-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="638ea-118">Une base de données nommée « sample_shard_2 » et tous les objets de schéma nécessaires qu’elle contient ont été créés.</span><span class="sxs-lookup"><span data-stu-id="638ea-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="638ea-119">**Important**: utilisez cette technique uniquement si vous êtes certain qu’hello plage pour le mappage de hello mis à jour est vide.</span><span class="sxs-lookup"><span data-stu-id="638ea-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="638ea-120">méthodes Hello ci-dessus ne vérifient pas les données de la plage de hello déplacé, il est donc préférable tooinclude vérifie dans votre code.</span><span class="sxs-lookup"><span data-stu-id="638ea-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="638ea-121">S’il existe des lignes dans la plage de hello en cours de déplacement, distribution des données réelles hello ne correspondre pas de carte de partitions mis à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="638ea-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="638ea-122">Hello d’utilisation [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello opération au lieu de cela dans ces cas.</span><span class="sxs-lookup"><span data-stu-id="638ea-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

