---
title: "Didacticiel de distribution mondiale Azure Cosmos DB pour l’API Table | Microsoft Docs"
description: "Découvrez comment configurer la distribution mondiale Azure Cosmos DB à l’aide de l’API Table."
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="fb8f1-104">Comment configurer la distribution mondiale Azure Cosmos DB à l’aide de l’API Table</span><span class="sxs-lookup"><span data-stu-id="fb8f1-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="fb8f1-105">Dans cet article, nous allons vous montrer comment utiliser le portail Azure pour configurer la distribution mondiale Azure Cosmos DB avant d’établir une connexion à l’aide de l’API Table (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="fb8f1-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="fb8f1-106">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="fb8f1-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="fb8f1-107">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="fb8f1-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="fb8f1-108">Configurer la distribution mondiale à l’aide de [l’API Table](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="fb8f1-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="fb8f1-109">Se connecter à une région de prédilection avec l’API Table</span><span class="sxs-lookup"><span data-stu-id="fb8f1-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="fb8f1-110">Pour tirer parti de la [distribution mondiale](distribute-data-globally.md), les applications clientes peuvent spécifier la liste ordonnée de préférences de régions à utiliser pour effectuer des opérations sur les documents.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="fb8f1-111">Pour ce faire, définissez la valeur de configuration `TablePreferredLocations` dans la configuration de l’application de la version préliminaire du kit de développement logiciel Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="fb8f1-112">Selon la configuration du compte Azure Cosmos DB, la disponibilité régionale actuelle et la liste de préférences spécifiée, le Kit de développement logiciel (SDK) Azure Storage choisit le point de terminaison optimal pour les opérations de lecture et d’écriture.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="fb8f1-113">Le paramètre `TablePreferredLocations` doit contenir une liste séparée par des virgules des emplacements (de multihébergement) préférés pour les lectures.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="fb8f1-114">Chaque instance de client peut spécifier un sous-ensemble de ces régions dans l’ordre de préférence pour des lectures à faible latence.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="fb8f1-115">Les régions doivent être nommées à l’aide de leurs [noms d’affichage](https://msdn.microsoft.com/library/azure/gg441293.aspx), par exemple, `West US`.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="fb8f1-116">Toutes les lectures sont envoyées vers la première région disponible dans la liste `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="fb8f1-117">Si la demande échoue, le client passe à la région suivante dans la liste et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="fb8f1-118">Le SDK tente des opérations de lecture uniquement à partir des régions spécifiées dans `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="fb8f1-119">Ainsi, par exemple, si le compte de base de données est disponible dans trois régions, mais que le client spécifie uniquement deux des régions sans écriture de `TablePreferredLocations`, aucune lecture n’est traitée hors de la région d’écriture, même en cas de basculement.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="fb8f1-120">Le SDK envoie automatiquement toutes les écritures vers la région d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="fb8f1-121">Si la propriété `TablePreferredLocations` n’est pas définie, toutes les demandes seront traitées par la zone d’écriture en cours.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="fb8f1-122">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="fb8f1-123">Découvrez comment gérer la cohérence de votre compte répliqué à l’échelle mondiale en lisant l’article [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="fb8f1-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="fb8f1-124">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="fb8f1-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb8f1-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb8f1-125">Next steps</span></span>

<span data-ttu-id="fb8f1-126">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="fb8f1-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb8f1-127">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="fb8f1-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="fb8f1-128">Configurer la distribution mondiale à l’aide des API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="fb8f1-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="fb8f1-129">Vous pouvez maintenant passer au didacticiel suivant pour apprendre à développer en local à l’aide de l’émulateur local Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fb8f1-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb8f1-130">Développer en local avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="fb8f1-130">Develop locally with the emulator</span></span>](local-emulator.md)