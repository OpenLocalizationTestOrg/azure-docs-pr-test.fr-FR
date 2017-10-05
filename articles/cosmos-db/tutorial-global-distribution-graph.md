---
title: "Didacticiel de distribution mondiale Azure Cosmos DB pour l’API Graph | Microsoft Docs"
description: "Découvrez comment configurer la distribution mondiale Azure Cosmos DB à l’aide de l’API Graph."
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
ms.openlocfilehash: 3c8794fe33c2ff5aa79559ea2c323cf8d92b426a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-graph-api"></a><span data-ttu-id="d7b89-104">Comment configurer la distribution mondiale Azure Cosmos DB à l’aide de l’API Graph</span><span class="sxs-lookup"><span data-stu-id="d7b89-104">How to setup Azure Cosmos DB global distribution using the Graph API</span></span>

<span data-ttu-id="d7b89-105">Dans cet article, nous allons vous montrer comment utiliser le portail Azure pour configurer la distribution mondiale Azure Cosmos DB avant d’établir une connexion à l’aide de l’API Graph (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="d7b89-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Graph API (preview).</span></span>

<span data-ttu-id="d7b89-106">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7b89-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d7b89-107">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7b89-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="d7b89-108">Configurer la distribution mondiale à l’aide des [API Graph](graph-introduction.md) (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="d7b89-108">Configure global distribution using the [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-graph-api-using-the-net-sdk"></a><span data-ttu-id="d7b89-109">Se connecter à une région de prédilection avec l’API Graph à l’aide du SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d7b89-109">Connecting to a preferred region using the Graph API using the .NET SDK</span></span>

<span data-ttu-id="d7b89-110">L’API Graph est exposée sous forme de bibliothèque d’extension sur le SDK DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d7b89-110">The Graph API is exposed as an extension library on top of the DocumentDB SDK.</span></span>

<span data-ttu-id="d7b89-111">Pour tirer parti de la [distribution mondiale](distribute-data-globally.md), les applications clientes peuvent spécifier la liste ordonnée de préférences de régions à utiliser pour effectuer des opérations sur les documents.</span><span class="sxs-lookup"><span data-stu-id="d7b89-111">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="d7b89-112">Pour cela, vous devez configurer la stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="d7b89-112">This can be done by setting the connection policy.</span></span> <span data-ttu-id="d7b89-113">Selon la configuration du compte Azure Cosmos DB, la disponibilité régionale actuelle et la liste de préférences spécifiée, le Kit de développement logiciel (SDK) choisit le point de terminaison optimal pour les opérations de lecture et d’écriture.</span><span class="sxs-lookup"><span data-stu-id="d7b89-113">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span></span>

<span data-ttu-id="d7b89-114">Cette liste de préférences est spécifiée lors de l’initialisation d’une connexion à l’aide des SDK.</span><span class="sxs-lookup"><span data-stu-id="d7b89-114">This preference list is specified when initializing a connection using the SDKs.</span></span> <span data-ttu-id="d7b89-115">Les SDK acceptent un paramètre facultatif « PreferredLocations » qui est une liste ordonnée des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b89-115">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="d7b89-116">**Écritures** : le SDK envoie automatiquement toutes les écritures vers la région d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="d7b89-116">**Writes**: The SDK will automatically send all writes to the current write region.</span></span>
* <span data-ttu-id="d7b89-117">**Lectures** : toutes les lectures sont envoyées vers la première région disponible dans la liste PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="d7b89-117">**Reads**: All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="d7b89-118">Si la demande échoue, le client passe à la région suivante dans la liste et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="d7b89-118">If the request fails, the client will fail down the list to the next region, and so on.</span></span> <span data-ttu-id="d7b89-119">Les SDK tentent des opérations de lecture uniquement à partir des régions spécifiées dans PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="d7b89-119">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="d7b89-120">Ainsi, par exemple, si le compte Cosmos DB est disponible dans trois régions, mais que le client spécifie uniquement deux des régions sans écriture de PreferredLocations, aucune lecture n’est traitée hors de la région d’écriture, même en cas de basculement.</span><span class="sxs-lookup"><span data-stu-id="d7b89-120">So, for example, if the Cosmos DB account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="d7b89-121">L’application peut vérifier le point de terminaison d’écriture et le point de terminaison de lecture actuels choisis par le SDK en vérifiant deux propriétés, WriteEndpoint et ReadEndpoint, disponibles dans le SDK version 1.8 et ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d7b89-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="d7b89-122">Si la propriété PreferredLocations n’est pas définie, toutes les demandes seront traitées par la zone d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="d7b89-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

### <a name="using-the-sdk"></a><span data-ttu-id="d7b89-123">Utilisation du kit de développement logiciel</span><span class="sxs-lookup"><span data-stu-id="d7b89-123">Using the SDK</span></span>

<span data-ttu-id="d7b89-124">Par exemple, dans le SDK .NET, le paramètre `ConnectionPolicy` du constructeur `DocumentClient` comporte une propriété appelée `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d7b89-124">For example, in the .NET SDK, the `ConnectionPolicy` parameter for the `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="d7b89-125">Cette propriété peut être définie sur une liste de noms de région.</span><span class="sxs-lookup"><span data-stu-id="d7b89-125">This property can be set to a list of region names.</span></span> <span data-ttu-id="d7b89-126">Le noms d’affichage des [régions Azure][regions] peuvent être spécifié dans `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d7b89-126">The display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="d7b89-127">Les URL des points de terminaison ne doivent pas être considérées comme des constantes à long terme.</span><span class="sxs-lookup"><span data-stu-id="d7b89-127">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="d7b89-128">Le service peut les mettre à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="d7b89-128">The service may update these at any point.</span></span> <span data-ttu-id="d7b89-129">Le SDK gère ce changement automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d7b89-129">The SDK handles this change automatically.</span></span>
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

// connect to Azure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="d7b89-130">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d7b89-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="d7b89-131">Découvrez comment gérer la cohérence de votre compte répliqué à l’échelle mondiale en lisant l’article [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d7b89-131">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="d7b89-132">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d7b89-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7b89-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7b89-133">Next steps</span></span>

<span data-ttu-id="d7b89-134">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7b89-134">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7b89-135">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7b89-135">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="d7b89-136">Configurer la distribution mondiale à l’aide des API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d7b89-136">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="d7b89-137">Vous pouvez maintenant passer au didacticiel suivant pour apprendre à développer en local à l’aide de l’émulateur local Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d7b89-137">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7b89-138">Développer en local avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="d7b89-138">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

