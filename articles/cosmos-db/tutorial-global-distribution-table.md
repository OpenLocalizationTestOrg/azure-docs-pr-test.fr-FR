---
title: "didacticiel de distribution globale aaaAzure Cosmos DB pour l’API de Table | Documents Microsoft"
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API de Table."
services: cosmos-db
keywords: distribution mondiale, Table
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="f3679-104">À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API de Table</span><span class="sxs-lookup"><span data-stu-id="f3679-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="f3679-105">Dans cet article, nous montrons comment toouse hello distribution globale de base de données Azure Cosmos toosetup portail Azure et connectez-vous à l’aide de hello API (version préliminaire) de la Table.</span><span class="sxs-lookup"><span data-stu-id="f3679-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="f3679-106">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3679-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f3679-107">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f3679-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="f3679-108">Configurer la distribution globale à l’aide de hello [API de Table](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f3679-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="f3679-109">Connexion tooa la région préférée à l’aide de hello API de Table</span><span class="sxs-lookup"><span data-stu-id="f3679-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="f3679-110">Dans l’avantage de tootake d’ordre de [distribution globale](distribute-data-globally.md), les applications clientes peuvent spécifier hello classés de liste de préférence des régions toobe utilisé tooperform les opérations de document.</span><span class="sxs-lookup"><span data-stu-id="f3679-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="f3679-111">Cela est possible en définissant les hello `TablePreferredLocations` valeur de configuration dans la configuration de l’application hello pour l’aperçu de hello SDK Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f3679-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="f3679-112">Selon la configuration du compte de base de données Azure Cosmos hello, disponibilité régionale actuelle hello liste de préférence spécifié, hello la plupart des point de terminaison optimale est sélectionnée par hello SDK Azure Storage tooperform écrire et opérations de lecture.</span><span class="sxs-lookup"><span data-stu-id="f3679-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="f3679-113">Hello `TablePreferredLocations` doit contenir une liste séparée par des virgules des emplacements (multihébergement) par défaut pour les lectures.</span><span class="sxs-lookup"><span data-stu-id="f3679-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="f3679-114">Chaque instance de client peut spécifier un sous-ensemble de ces régions dans l’ordre de hello préféré pour les lectures de faible latence.</span><span class="sxs-lookup"><span data-stu-id="f3679-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="f3679-115">les régions Hello doivent être nommées à l’aide de leurs [afficher les noms des](https://msdn.microsoft.com/library/azure/gg441293.aspx), par exemple, `West US`.</span><span class="sxs-lookup"><span data-stu-id="f3679-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="f3679-116">Toutes les lectures seront envoyés toohello première disponible région Bonjour `TablePreferredLocations` liste.</span><span class="sxs-lookup"><span data-stu-id="f3679-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="f3679-117">En cas de demande de hello, client de hello échouer la région de hello liste toohello suivante et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f3679-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="f3679-118">Hello SDK tente uniquement tooread de régions hello spécifié dans `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="f3679-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="f3679-119">Ainsi, par exemple, si hello compte de base de données est disponible dans trois régions, mais les clients hello spécifie uniquement deux des hello régions non-écriture pour `TablePreferredLocations`, alors aucune lecture ne sera pris en charge en dehors de la région d’écriture hello, même dans les cas de hello de basculement.</span><span class="sxs-lookup"><span data-stu-id="f3679-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="f3679-120">Hello Kit de développement logiciel enverra automatiquement région pour l’écriture de toutes les écritures toohello actuelle.</span><span class="sxs-lookup"><span data-stu-id="f3679-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="f3679-121">Si hello `TablePreferredLocations` propriété n’est pas définie, toutes les demandes seront pris en charge à partir de la zone d’écriture en cours hello.</span><span class="sxs-lookup"><span data-stu-id="f3679-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="f3679-122">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f3679-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="f3679-123">Vous pouvez apprendre comment toomanage hello la cohérence de votre compte de réplication globale en lisant [niveaux de cohérence dans la base de données Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f3679-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="f3679-124">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="f3679-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3679-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3679-125">Next steps</span></span>

<span data-ttu-id="f3679-126">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="f3679-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3679-127">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f3679-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="f3679-128">Configurer la distribution globale à l’aide de hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f3679-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="f3679-129">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodevelop localement à l’aide de hello émulateur local de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3679-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3679-130">Développer localement avec l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="f3679-130">Develop locally with hello emulator</span></span>](local-emulator.md)
