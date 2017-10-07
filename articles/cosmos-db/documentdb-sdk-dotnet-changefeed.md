---
title: "aaaAzure DocumentDB modification flux processeur Kit de développement .NET et ressources | Documents Microsoft"
description: "Découvrez les hello modification flux processeur API et SDK, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version de hello DocumentDB modification de flux de processeur du SDK .NET."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="b9789-103">Kit SDK du processeur de flux de modification .NET DocumentDB : téléchargement et notes de publication</span><span class="sxs-lookup"><span data-stu-id="b9789-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9789-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b9789-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="b9789-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="b9789-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="b9789-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b9789-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="b9789-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b9789-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="b9789-108">Java</span><span class="sxs-lookup"><span data-stu-id="b9789-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="b9789-109">Python</span><span class="sxs-lookup"><span data-stu-id="b9789-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="b9789-110">REST</span><span class="sxs-lookup"><span data-stu-id="b9789-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="b9789-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="b9789-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="b9789-112">SQL</span><span class="sxs-lookup"><span data-stu-id="b9789-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="b9789-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="b9789-113">**SDK download**</span></span></td><td>[<span data-ttu-id="b9789-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="b9789-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="b9789-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="b9789-115">**API documentation**</span></span></td><td>[<span data-ttu-id="b9789-116">Documentation de référence de l’API de la bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="b9789-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="b9789-117">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="b9789-117">**Get started**</span></span></td><td>[<span data-ttu-id="b9789-118">Prise en main hello DocumentDB modification flux processeur .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b9789-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="b9789-119">**Infrastructure actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="b9789-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="b9789-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="b9789-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="b9789-121">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="b9789-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="b9789-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="b9789-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="b9789-123">Ajouter un tooobtain méthode une estimation de restantes toobe de travail traité dans hello modification de flux.</span><span class="sxs-lookup"><span data-stu-id="b9789-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="b9789-124">Compatible avec les versions 1.13.2 et supérieures du [Kit de développement logiciel (SDK) Document DB .NET](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b9789-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="b9789-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="b9789-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="b9789-126">Kit SDK GA</span><span class="sxs-lookup"><span data-stu-id="b9789-126">GA SDK</span></span>
* <span data-ttu-id="b9789-127">Compatible avec les versions 1.14.1 et les versions ci-dessous du [Kit de développement logiciel (SDK) DocumentDB .NET ](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b9789-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="b9789-128">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="b9789-128">Release & Retirement dates</span></span>
<span data-ttu-id="b9789-129">Microsoft enverra une notification au moins **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.</span><span class="sxs-lookup"><span data-stu-id="b9789-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="b9789-130">Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel SDK, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible.</span><span class="sxs-lookup"><span data-stu-id="b9789-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="b9789-131">N’importe quel tooCosmos demande à l’aide d’un kit de développement logiciel mis hors service de base de données seront rejetées par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b9789-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="b9789-132">Version</span><span class="sxs-lookup"><span data-stu-id="b9789-132">Version</span></span> | <span data-ttu-id="b9789-133">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="b9789-133">Release Date</span></span> | <span data-ttu-id="b9789-134">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="b9789-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b9789-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b9789-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="b9789-136">13 août 2017</span><span class="sxs-lookup"><span data-stu-id="b9789-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="b9789-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b9789-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="b9789-138">7 juillet 2017</span><span class="sxs-lookup"><span data-stu-id="b9789-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="b9789-139">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="b9789-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="b9789-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b9789-140">See also</span></span>
<span data-ttu-id="b9789-141">toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.</span><span class="sxs-lookup"><span data-stu-id="b9789-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

