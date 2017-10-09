---
title: "débit aaaProvision pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment tooset mis en service le débit de votre base de données Azure Cosmos containsers, collections, graphiques et les tables."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="7ac60-103">Définir le débit des conteneurs Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7ac60-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="7ac60-104">Vous pouvez définir le débit pour les conteneurs de votre base de données Azure Cosmos Bonjour portail Azure ou à l’aide de hello kits de développement logiciel client.</span><span class="sxs-lookup"><span data-stu-id="7ac60-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="7ac60-105">Hello tableau suivant répertorie le débit hello disponible pour les conteneurs :</span><span class="sxs-lookup"><span data-stu-id="7ac60-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="7ac60-106"><strong>Conteneur à partition unique</strong></span><span class="sxs-lookup"><span data-stu-id="7ac60-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="7ac60-107"><strong>Conteneur partitionné</strong></span><span class="sxs-lookup"><span data-stu-id="7ac60-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="7ac60-108">Débit minimal</span><span class="sxs-lookup"><span data-stu-id="7ac60-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="7ac60-109">400 unités de demande par seconde</span><span class="sxs-lookup"><span data-stu-id="7ac60-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="7ac60-110">2 500 unités de requête par seconde</span><span class="sxs-lookup"><span data-stu-id="7ac60-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="7ac60-111">Débit maximal</span><span class="sxs-lookup"><span data-stu-id="7ac60-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="7ac60-112">10 000 unités de demande par seconde</span><span class="sxs-lookup"><span data-stu-id="7ac60-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="7ac60-113">Illimité</span><span class="sxs-lookup"><span data-stu-id="7ac60-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="7ac60-114">débit de hello tooset à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ac60-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="7ac60-115">Dans une nouvelle fenêtre, ouvrez hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ac60-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7ac60-116">Dans la barre de gauche hello, cliquez sur **base de données Azure Cosmos**, ou cliquez sur **plus Services** au bas de hello, puis faites défiler trop**bases de données**, puis cliquez sur **base de données Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="7ac60-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="7ac60-117">Sélectionnez votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7ac60-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="7ac60-118">Dans la nouvelle fenêtre de hello, cliquez sur **Explorateur de données (version préliminaire)** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="7ac60-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="7ac60-119">Dans la nouvelle fenêtre de hello, votre base de données et le conteneur, puis cliquez sur **échelle & paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7ac60-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="7ac60-120">Dans la nouvelle fenêtre de hello, tapez Bonjour nouvelle valeur de débit Bonjour **débit** zone, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7ac60-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="7ac60-121">débit de hello tooset à l’aide de hello API DocumentDB pour .NET</span><span class="sxs-lookup"><span data-stu-id="7ac60-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="7ac60-122">Forum Aux Questions sur le débit</span><span class="sxs-lookup"><span data-stu-id="7ac60-122">Throughput FAQ</span></span>

<span data-ttu-id="7ac60-123">**Puis-je définir mon accessible sans de débit à 400 ur/s ?**</span><span class="sxs-lookup"><span data-stu-id="7ac60-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="7ac60-124">400 ur/s est le débit minimal de hello sont disponible sur les collections de partitions uniques Cosmos DB (2500 ur/s est hello minimale pour les collections partitionnées).</span><span class="sxs-lookup"><span data-stu-id="7ac60-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="7ac60-125">Demander des unités sont définis dans des intervalles de 100 ur/s, mais le débit ne peut pas être défini too100 ur/s ou toute valeur inférieure à 400 ur/s.</span><span class="sxs-lookup"><span data-stu-id="7ac60-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="7ac60-126">Si vous avez besoin d’une méthode économique de toodevelop et Cosmos de base de données de test, vous pouvez utiliser hello libre [Azure Cosmos DB émulateur](local-emulator.md), que vous pouvez déployer localement sans frais.</span><span class="sxs-lookup"><span data-stu-id="7ac60-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="7ac60-127">**Comment définir le débit à l’aide de hello MongoDB API ?**</span><span class="sxs-lookup"><span data-stu-id="7ac60-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="7ac60-128">Il n’existe aucun débit de tooset extension MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="7ac60-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="7ac60-129">Hello recommandation est toouse hello API DocumentDB, comme indiqué dans [débit de hello tooset à l’aide de hello API DocumentDB pour .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="7ac60-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ac60-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ac60-130">Next steps</span></span>

<span data-ttu-id="7ac60-131">toolearn en savoir plus sur la configuration et de cours planète à l’échelle avec Cosmos DB, consultez [de partitionnement et de mise à l’échelle avec Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="7ac60-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
