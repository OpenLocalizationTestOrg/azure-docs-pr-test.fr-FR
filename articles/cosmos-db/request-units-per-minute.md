---
title: "Azure CosmosDB : Unités de requête par minute (RU/m) | Microsoft Docs"
description: "Découvrez comment tooreduce les coûts grâce à demander des unités par minute."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="94285-103">Unités de requête par minute dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="94285-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="94285-104">Base de données Azure Cosmos est conçue toohelp vous atteindre une performance rapide et prévisible et une échelle en toute transparence, ainsi que la croissance de votre application.</span><span class="sxs-lookup"><span data-stu-id="94285-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="94285-105">Vous pouvez configurer le débit sur un conteneur Cosmos DB sur les granularités par minute (RU/m), par seconde ou les deux.</span><span class="sxs-lookup"><span data-stu-id="94285-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="94285-106">Bonjour débit approvisionné par minute jusqu'à la granularité est utilisé toomanage inattendue des pics de charge de travail hello qui se produisent à un niveau de granularité par seconde.</span><span class="sxs-lookup"><span data-stu-id="94285-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="94285-107">Cet article fournit une vue d’ensemble du fonctionne de l’approvisionnement hello d’unité de demande par Minute (RU/m).</span><span class="sxs-lookup"><span data-stu-id="94285-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="94285-108">Hello vise à l’esprit l’approvisionnement ur/m tooprovide prévisibilité des performances imprévisibles besoins (surtout si vous devez toorun analytique sur vos données opérationnelles) et les charges de travail beaucoup.</span><span class="sxs-lookup"><span data-stu-id="94285-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="94285-109">Nous souhaitons toohave que nos clients consomment le plus grand débit de hello que préparation se peuvent adapter rapidement avec tranquillité d’esprit.</span><span class="sxs-lookup"><span data-stu-id="94285-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="94285-110">Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="94285-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="94285-111">Comment une unité de requête par minute fonctionne-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="94285-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="94285-112">Qu’est la différence de hello entre les unités de demande par Minute et demandes par seconde ?</span><span class="sxs-lookup"><span data-stu-id="94285-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="94285-113">Comment tooprovision ur/m ?</span><span class="sxs-lookup"><span data-stu-id="94285-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="94285-114">Dans quels cas dois-je envisager d’approvisionner des unités de demande par minute ?</span><span class="sxs-lookup"><span data-stu-id="94285-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="94285-115">Comment toouse hello métriques portail toooptimize coût et les performances ?</span><span class="sxs-lookup"><span data-stu-id="94285-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="94285-116">Définir le type de requête qui consomme le budget RU/m ?</span><span class="sxs-lookup"><span data-stu-id="94285-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="94285-117">Configuration des unités de requête par minute (RU/m)</span><span class="sxs-lookup"><span data-stu-id="94285-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="94285-118">Lorsque vous configurez la base de données Azure Cosmos granularité hello deuxième (ur/s), vous obtenez la garantie de hello que votre demande aboutit à une latence faible si le débit n’a pas dépassé capacité hello configurée au cours de cette seconde.</span><span class="sxs-lookup"><span data-stu-id="94285-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="94285-119">Granularité de hello ur/m, est à la minute hello avec garantie de hello que votre demande a réussi au cours de cette minute.</span><span class="sxs-lookup"><span data-stu-id="94285-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="94285-120">Par rapport à des systèmes toobursting, nous vous assurer que les performances hello vous obtenez sont prévisible et vous pouvez planifier cela.</span><span class="sxs-lookup"><span data-stu-id="94285-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="94285-121">moyen Hello par minute de fonctionnement de la configuration est simple :</span><span class="sxs-lookup"><span data-stu-id="94285-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="94285-122">RU/m est facturé toutes les heures et en ajout tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="94285-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="94285-123">Pour plus d’informations, consultez la [page de tarification](https://aka.ms/acdbpricing) d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94285-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="94285-124">Les RU/m peuvent être activées au niveau de la collection.</span><span class="sxs-lookup"><span data-stu-id="94285-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="94285-125">Cela peut se faire via hello kits de développement logiciel (Node.js, Java ou .net) ou via le portail de hello (incluent également les charges de travail MongoDB API)</span><span class="sxs-lookup"><span data-stu-id="94285-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="94285-126">Lorsqu’ur/m est activé, pour chaque 100 ur/s configuré, vous obtenez également les 1 000 ur/m configuré (ratio de hello est de 10 x)</span><span class="sxs-lookup"><span data-stu-id="94285-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="94285-127">À une seconde donnée, une unité de requête consomme votre configuration de RU/m uniquement si vous avez dépassé votre configuration par seconde pendant cette seconde</span><span class="sxs-lookup"><span data-stu-id="94285-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="94285-128">Une fois hello fin du délai de 60 secondes (UTC), hello par minute de l’approvisionnement est rechargée.</span><span class="sxs-lookup"><span data-stu-id="94285-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="94285-129">Les RU/m peuvent être activées uniquement pour les collections avec une configuration maximale de 5 000 RU/s par partition.</span><span class="sxs-lookup"><span data-stu-id="94285-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="94285-130">Si vous mettez à l’échelle de vos besoins de débit avec un haut niveau de configuration par partition, vous obtiendrez un message d’avertissement</span><span class="sxs-lookup"><span data-stu-id="94285-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="94285-131">Vous trouverez ci-dessous un exemple concret, dans lequel un client peut configurer 10 kRU/s avec 100 kRU/m, et économiser 73 % des coûts par rapport à la configuration pour les pointes (à 50 kRU/s) sur une période de 90 secondes sur une collection qui a une configuration de 10 000 RU/s et 100 000 RU/m :</span><span class="sxs-lookup"><span data-stu-id="94285-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="94285-132">seconde 1er : allocation de réserve hello ur/m est définie à 100 000</span><span class="sxs-lookup"><span data-stu-id="94285-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="94285-133">second 3e : au cours de cette deuxième hello la consommation de l’unité de demande a été 11,010 RUs 1,010 RUs au-dessus de l’approvisionnement de hello ur/s.</span><span class="sxs-lookup"><span data-stu-id="94285-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="94285-134">Par conséquent, 1,010 RUs sont déduits à partir de l’allocation de réserve hello ur/m.</span><span class="sxs-lookup"><span data-stu-id="94285-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="94285-135">98,990 RUs sont disponibles pour hello suivants 57 secondes dans l’allocation de réserve hello ur/m</span><span class="sxs-lookup"><span data-stu-id="94285-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="94285-136">seconde 29 : au cours de cette seconde, est devenu un pic important (> 4 x supérieure à la mise en service par seconde) et la consommation de hello d’unité de demande a été 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="94285-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="94285-137">36,920 RUs sont déduites du budget ur/m hello exclu 92,323 RUs (seconde 28) too55, 403 RUs (29 secondes)</span><span class="sxs-lookup"><span data-stu-id="94285-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="94285-138">seconde 61st : allocation de réserve ur/m est redéfinie too100, RUs 000.</span><span class="sxs-lookup"><span data-stu-id="94285-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Graphique montrant la consommation hello et la configuration de base de données Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="94285-140">Spécification de la capacité d’unités de requête avec RU/m</span><span class="sxs-lookup"><span data-stu-id="94285-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="94285-141">Lorsque vous créez une collection de base de données Azure Cosmos, vous spécifiez le nombre de hello d’unités de demande par seconde (RU par seconde) à réserver pour la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="94285-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="94285-142">Vous pouvez également décider si vous souhaitez RU tooadd par minute.</span><span class="sxs-lookup"><span data-stu-id="94285-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="94285-143">Cela est possible via hello portail ou hello SDK.</span><span class="sxs-lookup"><span data-stu-id="94285-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="94285-144">Via hello portail</span><span class="sxs-lookup"><span data-stu-id="94285-144">Through hello Portal</span></span>

<span data-ttu-id="94285-145">L’activation ou désactivation des unités de requête par minute nécessite simplement un clic lors de la configuration d’une collection.</span><span class="sxs-lookup"><span data-stu-id="94285-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Capture d’écran montrant comment tooset ur/m Bonjour portail Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="94285-147">Via le Kit de développement logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="94285-147">Through hello SDK</span></span>
<span data-ttu-id="94285-148">Tout d’abord, il s’agit de toonote important qu’ur/m est uniquement disponible pour hello suivant des kits de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="94285-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="94285-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="94285-149">.Net 1.14.0</span></span>
* <span data-ttu-id="94285-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="94285-150">Java 1.11.0</span></span>
* <span data-ttu-id="94285-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="94285-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="94285-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="94285-152">Python 2.2.0</span></span>

<span data-ttu-id="94285-153">Voici un extrait de code pour la création d’une collection avec 3 000 unités de demande par les unités de demande de deuxième et 30 000 par minute à l’aide de hello .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="94285-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="94285-154">Voici un extrait de code pour modifier le débit de hello d’une collection de too5, 000 unités de demande par seconde sans configuration RU par minute à l’aide de hello .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="94285-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="94285-155">Scénarios adaptés</span><span class="sxs-lookup"><span data-stu-id="94285-155">Good fit scenarios</span></span>

<span data-ttu-id="94285-156">Dans cette section, nous fournissons une vue d’ensemble des scénarios qui sont adaptés à l’activation des unités de demande par minute.</span><span class="sxs-lookup"><span data-stu-id="94285-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="94285-157">**Environnement de développement/test :** convient bien.</span><span class="sxs-lookup"><span data-stu-id="94285-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="94285-158">Pendant la phase de développement hello, si vous testez votre application avec différentes charges de travail, RU/m peut fournir une grande souplesse hello à ce stade.</span><span class="sxs-lookup"><span data-stu-id="94285-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="94285-159">Lors de hello [émulateur](local-emulator.md) est un excellent outil gratuit de tootest base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="94285-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="94285-160">Toutefois si vous souhaitez toostart dans un environnement cloud, vous devez une avec une grande souplesse avec ur/m à vos besoins de performances ad hoc.</span><span class="sxs-lookup"><span data-stu-id="94285-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="94285-161">Vous passerez le plus de temps à développer, et moins à vous inquiéter des exigences de performances au départ.</span><span class="sxs-lookup"><span data-stu-id="94285-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="94285-162">Nous vous recommandons de commencer avec hello minimale ur/s mise en service et activer ur/m.</span><span class="sxs-lookup"><span data-stu-id="94285-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="94285-163">**Besoins de granularité imprévisibles, à pics, par minute :** Bien adapté – Économies : 25 à 75 %.</span><span class="sxs-lookup"><span data-stu-id="94285-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="94285-164">Nous avons vu une nette amélioration des RU/m, et la plupart des scénarios de production entrent dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="94285-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="94285-165">Si vous avez une charge de travail IoT a pic plusieurs fois dans une minute, si vous avez des requêtes en cours d’exécution lorsque votre système émet s’insérez en masse à hello même temps, vous devez une capacité supplémentaire pour handeling beaucoup doit.</span><span class="sxs-lookup"><span data-stu-id="94285-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="94285-166">Nous vous recommandons d’optimiser vos besoins en ressources en appliquant notre approche étape par étape ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="94285-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Graphique indiquant la consommation de requête dans une granularité de 5 minutes](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="94285-168">*Figure - Test d’évaluation de la consommation de RU*</span><span class="sxs-lookup"><span data-stu-id="94285-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="94285-169">**Tranquillité d’esprit :** Bien adapté - Économies : 10-20 %.</span><span class="sxs-lookup"><span data-stu-id="94285-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="94285-170">Parfois, vous souhaitiez toohave la tranquillité d’esprit et ne vous inquiétez pas sur les pics et la limitation.</span><span class="sxs-lookup"><span data-stu-id="94285-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="94285-171">Cette fonctionnalité est droite hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="94285-171">This feature is hello right one for you.</span></span> <span data-ttu-id="94285-172">Dans ce cas, nous vous recommandons d’activer les RU/m et de légèrement réduire votre approvisionnement par seconde.</span><span class="sxs-lookup"><span data-stu-id="94285-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="94285-173">Ce cas est différent de hello ci-dessus comme toooptimize n’essaie pas efficacement votre configuration.</span><span class="sxs-lookup"><span data-stu-id="94285-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="94285-174">Vous êtes davantage dans une mentalité « Zéro limite ».</span><span class="sxs-lookup"><span data-stu-id="94285-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="94285-175">Les opérations critiques ayant des besoins ad hoc : nous vous recommandons parfois tooonly permettent des opérations critiques accès ur/m budget afin de l’allocation de réserve hello n’obtient pas consommer par ad hoc ou moins importantes opérations.</span><span class="sxs-lookup"><span data-stu-id="94285-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="94285-176">Qui peut être facilement définis dans la section hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="94285-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="94285-177">À l’aide de hello métriques portail toooptimize coût et les performances</span><span class="sxs-lookup"><span data-stu-id="94285-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="94285-178">**Dans les semaines à venir hello, nous développerons davantage contenu hello autour de l’analyse toooptimize de consommation minute RUs que votre débit a besoin.**</span><span class="sxs-lookup"><span data-stu-id="94285-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="94285-179">Par le biais des mesures portail hello, vous pouvez voir combien de régulières secondes RU vous consommez et RU minutes.</span><span class="sxs-lookup"><span data-stu-id="94285-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="94285-180">La surveillance de ces métriques devrait vous aider à optimiser votre configuration.</span><span class="sxs-lookup"><span data-stu-id="94285-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="94285-181">Nous vous recommandons une approche étape par étape sur la façon de toouse ur/m tooyour parti.</span><span class="sxs-lookup"><span data-stu-id="94285-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="94285-182">Pour chaque étape, vous devez avoir une vue d’ensemble de la consommation de hello RU représentant un cycle complet de votre charge de travail (il peut être heures, jours ou semaines) et obtenir des informations sur l’utilisation de hello de ce que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="94285-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="94285-183">principe Hello derrière cette approche est toomake votre configuration de débit comme proche que possible tooa approvisionnement point qui correspond à vos critères de performances ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="94285-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Graphique indiquant la consommation de requête dans une granularité de 5 minutes](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="94285-185">toounderstand hello approvisionnement point optimal pour votre charge de travail, vous devez toounderstand :</span><span class="sxs-lookup"><span data-stu-id="94285-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="94285-186">Les modèles de consommation : pics inexistants, peu fréquents ou courants ?</span><span class="sxs-lookup"><span data-stu-id="94285-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="94285-187">Pics petits (2x en moyenne), moyens ou grands en taille (>10x en moyenne) ?</span><span class="sxs-lookup"><span data-stu-id="94285-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="94285-188">Pourcentage de demandes limitées : restez-vous à l’aise même si vous avez un peu de limitation ?</span><span class="sxs-lookup"><span data-stu-id="94285-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="94285-189">Si oui, dans quelle mesure ?</span><span class="sxs-lookup"><span data-stu-id="94285-189">If so, by how much?</span></span> 

<span data-ttu-id="94285-190">Une fois que vous avez identifié quelles sont vos objectifs, vous serez en mesure de tooget proche toohello optimal de configuration.</span><span class="sxs-lookup"><span data-stu-id="94285-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="94285-191">tooassist vous, nous souhaitons tooprovide une recommandations générales sur comment toooptimize votre configuration en fonction de votre consommation ur/m.</span><span class="sxs-lookup"><span data-stu-id="94285-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="94285-192">Cette recommandation ne s’applique pas type tooall des charges de travail, mais est basée sur la base de connaissances hello aperçu privé.</span><span class="sxs-lookup"><span data-stu-id="94285-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="94285-193">Nous pourrions modifier ces lignes de base lorsque nous en apprendrons davantage :</span><span class="sxs-lookup"><span data-stu-id="94285-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="94285-194">Utilisation de % de RU/m</span><span class="sxs-lookup"><span data-stu-id="94285-194">RU/m % utilization</span></span>|<span data-ttu-id="94285-195">Degré d’utilisation des RU/m</span><span class="sxs-lookup"><span data-stu-id="94285-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="94285-196">Actions recommandées pour la configuration</span><span class="sxs-lookup"><span data-stu-id="94285-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="94285-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="94285-197">0-1%</span></span>|<span data-ttu-id="94285-198">Sous-utilisation</span><span class="sxs-lookup"><span data-stu-id="94285-198">Under utilization</span></span>|<span data-ttu-id="94285-199">Réduire les tooconsume ur/s plus ur/m</span><span class="sxs-lookup"><span data-stu-id="94285-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="94285-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="94285-200">1-10%</span></span>|<span data-ttu-id="94285-201">Utilisation normale</span><span class="sxs-lookup"><span data-stu-id="94285-201">Healthy use</span></span>|<span data-ttu-id="94285-202">Hello même configurez niveau</span><span class="sxs-lookup"><span data-stu-id="94285-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="94285-203">Supérieur à 10 %</span><span class="sxs-lookup"><span data-stu-id="94285-203">Above 10%</span></span>|<span data-ttu-id="94285-204">Utilisation excessive</span><span class="sxs-lookup"><span data-stu-id="94285-204">Over utilization</span></span>|<span data-ttu-id="94285-205">Augmenter toorely ur/s moins sur ur/m</span><span class="sxs-lookup"><span data-stu-id="94285-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="94285-206">Sélectionnez les opérations qui peuvent consommer allocation de réserve hello ur/m</span><span class="sxs-lookup"><span data-stu-id="94285-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="94285-207">Au niveau de la demande, vous pouvez également activer ou désactiver demande hello tooserve du budget ur/m quel que soit le type d’opération.</span><span class="sxs-lookup"><span data-stu-id="94285-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="94285-208">Si le budget de RUs par seconde alloué ordinaire est consommée et demande de hello ne peut pas consommer l’allocation de réserve hello ur/m, cette demande sera limitée.</span><span class="sxs-lookup"><span data-stu-id="94285-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="94285-209">Par défaut, toute requête est servie par le budget de RU/m si le budget de débit de RU/m est activé.</span><span class="sxs-lookup"><span data-stu-id="94285-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="94285-210">Voici un extrait de code pour la désactivation de budget ur/m à l’aide de hello API DocumentDB pour les opérations CRUD et de la requête.</span><span class="sxs-lookup"><span data-stu-id="94285-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="94285-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94285-211">Next steps</span></span>

<span data-ttu-id="94285-212">Dans cet article, nous avons décrit le fonctionnement du partitionnement dans Azure Cosmos DB, la création de collections partitionnées et la sélection d’une clé de partition adéquate pour votre application.</span><span class="sxs-lookup"><span data-stu-id="94285-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="94285-213">Effectuez un test des performances et de la mise à l’échelle avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94285-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="94285-214">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md) pour obtenir un exemple.</span><span class="sxs-lookup"><span data-stu-id="94285-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="94285-215">Commencer le codage par hello [kits de développement logiciel](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="94285-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="94285-216">Informez-vous sur le [débit approvisionné](request-units.md) dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="94285-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

