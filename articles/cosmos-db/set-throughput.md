---
title: "Approvisionner le débit pour Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment définir un débit approvisionné pour vos conteneurs, collections, graphes et tables Azure Cosmos DB."
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="ec27c-103">Définir le débit des conteneurs Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ec27c-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="ec27c-104">Vous pouvez définir le débit de vos conteneurs Azure Cosmos DB dans le portail Azure ou à l’aide des SDK clients.</span><span class="sxs-lookup"><span data-stu-id="ec27c-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="ec27c-105">Le tableau suivant répertorie les débits disponibles pour les conteneurs :</span><span class="sxs-lookup"><span data-stu-id="ec27c-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="ec27c-106"><strong>Conteneur à partition unique</strong></span><span class="sxs-lookup"><span data-stu-id="ec27c-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ec27c-107"><strong>Conteneur partitionné</strong></span><span class="sxs-lookup"><span data-stu-id="ec27c-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ec27c-108">Débit minimal</span><span class="sxs-lookup"><span data-stu-id="ec27c-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ec27c-109">400 unités de demande par seconde</span><span class="sxs-lookup"><span data-stu-id="ec27c-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ec27c-110">2 500 unités de requête par seconde</span><span class="sxs-lookup"><span data-stu-id="ec27c-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ec27c-111">Débit maximal</span><span class="sxs-lookup"><span data-stu-id="ec27c-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ec27c-112">10 000 unités de demande par seconde</span><span class="sxs-lookup"><span data-stu-id="ec27c-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ec27c-113">Illimité</span><span class="sxs-lookup"><span data-stu-id="ec27c-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="ec27c-114">Pour définir le débit à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec27c-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="ec27c-115">Dans une nouvelle fenêtre, ouvrez le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec27c-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec27c-116">Dans la barre de gauche, cliquez sur **Azure Cosmos DB** ou sur **Plus de services** en bas, accédez à **Bases de données**, puis sélectionnez **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ec27c-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="ec27c-117">Sélectionnez votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ec27c-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="ec27c-118">Dans la nouvelle fenêtre, cliquez sur **Explorateur de données (préversion)** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="ec27c-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="ec27c-119">Dans la nouvelle fenêtre, développez la base de données et le conteneur, puis cliquez sur **Scale & Settings** (Mise à l’échelle & paramètres).</span><span class="sxs-lookup"><span data-stu-id="ec27c-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="ec27c-120">Dans la nouvelle fenêtre, tapez la nouvelle valeur de débit dans la zone **Débit**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ec27c-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="ec27c-121">Pour définir le débit à l’aide de l’API DocumentDB pour .NET</span><span class="sxs-lookup"><span data-stu-id="ec27c-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="ec27c-122">Forum Aux Questions sur le débit</span><span class="sxs-lookup"><span data-stu-id="ec27c-122">Throughput FAQ</span></span>

<span data-ttu-id="ec27c-123">**Puis-je définir mon débit sur une valeur inférieure à 400 unités de demande/s ?**</span><span class="sxs-lookup"><span data-stu-id="ec27c-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="ec27c-124">Cette valeur de 400 unités de demande/s correspond au débit minimal disponible sur les collections à partition unique Cosmos DB (une valeur de 2 500 unités de demande/s correspond à la valeur minimale pour les collections partitionnées).</span><span class="sxs-lookup"><span data-stu-id="ec27c-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="ec27c-125">Les unités de demande sont définies par intervalles de 100 unités de demande/s, mais le débit ne peut pas avoir la valeur 100 unités de demande/s ou toute valeur inférieure à 400 unités de demande/s.</span><span class="sxs-lookup"><span data-stu-id="ec27c-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="ec27c-126">Si vous recherchez une méthode économique pour développer et tester Cosmos DB, vous pouvez utiliser gratuitement l’[Émulateur Azure Cosmos DB](local-emulator.md), que vous pouvez déployer localement sans frais.</span><span class="sxs-lookup"><span data-stu-id="ec27c-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="ec27c-127">**Comment définir le débit à l’aide de l’API MongoDB ?**</span><span class="sxs-lookup"><span data-stu-id="ec27c-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="ec27c-128">Il n’existe aucune extension d’API MongoDB pour définir le débit.</span><span class="sxs-lookup"><span data-stu-id="ec27c-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="ec27c-129">Nous vous recommandons d’utiliser l’API DocumentDB, comme indiqué dans [Pour définir le débit à l’aide de l’API DocumentDB pour .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="ec27c-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec27c-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec27c-130">Next steps</span></span>

<span data-ttu-id="ec27c-131">Pour plus d’informations sur l’approvisionnement et la mise à l’échelle avec Cosmos DB, consultez [Partitioning and scaling with Cosmos DB (Partitionnement et mise à l’échelle avec Cosmos DB)](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="ec27c-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
