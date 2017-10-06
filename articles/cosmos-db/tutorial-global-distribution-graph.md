---
title: "didacticiel de distribution globale aaaAzure Cosmos DB pour l’API Graph | Documents Microsoft"
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API Graph."
services: cosmos-db
keywords: distribution globale, graph, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="7f4ef-104">À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API Graph</span><span class="sxs-lookup"><span data-stu-id="7f4ef-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="7f4ef-105">Dans cet article, nous montrons comment toouse hello distribution globale de base de données Azure Cosmos toosetup portail Azure et connectez-vous à l’aide de hello l’API Graph (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="7f4ef-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="7f4ef-106">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7f4ef-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7f4ef-107">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7f4ef-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="7f4ef-108">Configurer la distribution globale à l’aide de hello [API graphiques](graph-introduction.md) (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="7f4ef-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="7f4ef-109">Connexion à l’aide de l’API Graph hello hello .NET SDK à l’aide de la région préférée tooa</span><span class="sxs-lookup"><span data-stu-id="7f4ef-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="7f4ef-110">Hello API Graph est exposée comme une bibliothèque d’extension par-dessus hello DocumentDB SDK.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="7f4ef-111">Dans l’avantage de tootake d’ordre de [distribution globale](distribute-data-globally.md), les applications clientes peuvent spécifier hello classés de liste de préférence des régions toobe utilisé tooperform les opérations de document.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="7f4ef-112">Pour ce faire, vous pouvez définir la stratégie de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="7f4ef-113">Selon la configuration du compte de base de données Azure Cosmos hello, disponibilité régionale en cours et la liste de préférence hello spécifié, hello la plupart des point de terminaison optimale sera choisi par l’écriture de tooperform hello SDK et les opérations de lecture.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="7f4ef-114">Cette liste de préférence est spécifiée lors de l’initialisation d’une connexion à l’aide de kits de développement logiciel hello.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="7f4ef-115">Hello kits de développement logiciel accepte un paramètre facultatif « PreferredLocations » qui est une liste ordonnée des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="7f4ef-116">**Écrit**: hello Kit de développement logiciel enverra automatiquement toutes les écrit la zone d’écriture en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="7f4ef-117">**Lit**: toutes les lectures seront envoyés toohello de première région disponibles dans la liste de PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="7f4ef-118">En cas de demande de hello, client de hello échouer la région de hello liste toohello suivante et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="7f4ef-119">Hello kits de développement logiciel tente uniquement tooread de régions hello spécifié dans PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="7f4ef-120">Ainsi, par exemple, si hello Cosmos DB compte n’est disponible dans trois régions, mais le client de hello spécifie uniquement deux des régions de non-écriture hello pour PreferredLocations, puis aucune lecture ne sera utilisée en dehors de la région d’écriture hello, même dans les cas de hello de basculement.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="7f4ef-121">application Hello peut vérifier le point de terminaison hello actuel écriture et lecture de point de terminaison choisi par hello SDK par la vérification deux propriétés, WriteEndpoint et ReadEndpoint, disponible dans la version du Kit de développement logiciel 1.8 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="7f4ef-122">Si hello PreferredLocations propriété n’est pas définie, toutes les demandes seront pris en charge à partir de la zone d’écriture en cours hello.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="7f4ef-123">À l’aide du Kit de développement logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="7f4ef-123">Using hello SDK</span></span>

<span data-ttu-id="7f4ef-124">Par exemple, Bonjour .NET SDK, hello `ConnectionPolicy` paramètre hello `DocumentClient` constructeur a une propriété appelée `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="7f4ef-125">Cette propriété peut être définie tooa la liste des noms de région.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="7f4ef-126">noms d’affichage de Hello pour [régions Azure] [ regions] peut être spécifié dans le cadre de `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="7f4ef-127">URL de Hello pour les points de terminaison hello ne doivent pas être considérés comme des constantes de longue durées.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="7f4ef-128">service de Hello peut mettre à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-128">hello service may update these at any point.</span></span> <span data-ttu-id="7f4ef-129">Hello SDK gère cette modification automatiquement.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="7f4ef-130">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="7f4ef-131">Vous pouvez apprendre comment toomanage hello la cohérence de votre compte de réplication globale en lisant [niveaux de cohérence dans la base de données Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="7f4ef-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="7f4ef-132">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="7f4ef-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f4ef-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f4ef-133">Next steps</span></span>

<span data-ttu-id="7f4ef-134">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="7f4ef-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f4ef-135">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7f4ef-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="7f4ef-136">Configurer la distribution globale à l’aide de hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7f4ef-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="7f4ef-137">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodevelop localement à l’aide de hello émulateur local de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7f4ef-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f4ef-138">Développer localement avec l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="7f4ef-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

