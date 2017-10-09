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
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Unités de requête par minute dans Azure Cosmos DB

Base de données Azure Cosmos est conçue toohelp vous atteindre une performance rapide et prévisible et une échelle en toute transparence, ainsi que la croissance de votre application. Vous pouvez configurer le débit sur un conteneur Cosmos DB sur les granularités par minute (RU/m), par seconde ou les deux. Bonjour débit approvisionné par minute jusqu'à la granularité est utilisé toomanage inattendue des pics de charge de travail hello qui se produisent à un niveau de granularité par seconde. 

Cet article fournit une vue d’ensemble du fonctionne de l’approvisionnement hello d’unité de demande par Minute (RU/m). Hello vise à l’esprit l’approvisionnement ur/m tooprovide prévisibilité des performances imprévisibles besoins (surtout si vous devez toorun analytique sur vos données opérationnelles) et les charges de travail beaucoup. Nous souhaitons toohave que nos clients consomment le plus grand débit de hello que préparation se peuvent adapter rapidement avec tranquillité d’esprit.

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :

* Comment une unité de requête par minute fonctionne-t-elle ?
* Qu’est la différence de hello entre les unités de demande par Minute et demandes par seconde ?
* Comment tooprovision ur/m ?
* Dans quels cas dois-je envisager d’approvisionner des unités de demande par minute ?
* Comment toouse hello métriques portail toooptimize coût et les performances ?
* Définir le type de requête qui consomme le budget RU/m ?

## <a name="provisioning-request-units-per-minute-rum"></a>Configuration des unités de requête par minute (RU/m)

Lorsque vous configurez la base de données Azure Cosmos granularité hello deuxième (ur/s), vous obtenez la garantie de hello que votre demande aboutit à une latence faible si le débit n’a pas dépassé capacité hello configurée au cours de cette seconde. Granularité de hello ur/m, est à la minute hello avec garantie de hello que votre demande a réussi au cours de cette minute. Par rapport à des systèmes toobursting, nous vous assurer que les performances hello vous obtenez sont prévisible et vous pouvez planifier cela.

moyen Hello par minute de fonctionnement de la configuration est simple :

* RU/m est facturé toutes les heures et en ajout tooRU/s. Pour plus d’informations, consultez la [page de tarification](https://aka.ms/acdbpricing) d’Azure Cosmos DB.
* Les RU/m peuvent être activées au niveau de la collection. Cela peut se faire via hello kits de développement logiciel (Node.js, Java ou .net) ou via le portail de hello (incluent également les charges de travail MongoDB API)
* Lorsqu’ur/m est activé, pour chaque 100 ur/s configuré, vous obtenez également les 1 000 ur/m configuré (ratio de hello est de 10 x)
* À une seconde donnée, une unité de requête consomme votre configuration de RU/m uniquement si vous avez dépassé votre configuration par seconde pendant cette seconde
* Une fois hello fin du délai de 60 secondes (UTC), hello par minute de l’approvisionnement est rechargée.
* Les RU/m peuvent être activées uniquement pour les collections avec une configuration maximale de 5 000 RU/s par partition. Si vous mettez à l’échelle de vos besoins de débit avec un haut niveau de configuration par partition, vous obtiendrez un message d’avertissement

Vous trouverez ci-dessous un exemple concret, dans lequel un client peut configurer 10 kRU/s avec 100 kRU/m, et économiser 73 % des coûts par rapport à la configuration pour les pointes (à 50 kRU/s) sur une période de 90 secondes sur une collection qui a une configuration de 10 000 RU/s et 100 000 RU/m :

* seconde 1er : allocation de réserve hello ur/m est définie à 100 000
* second 3e : au cours de cette deuxième hello la consommation de l’unité de demande a été 11,010 RUs 1,010 RUs au-dessus de l’approvisionnement de hello ur/s. Par conséquent, 1,010 RUs sont déduits à partir de l’allocation de réserve hello ur/m. 98,990 RUs sont disponibles pour hello suivants 57 secondes dans l’allocation de réserve hello ur/m
* seconde 29 : au cours de cette seconde, est devenu un pic important (> 4 x supérieure à la mise en service par seconde) et la consommation de hello d’unité de demande a été 46,920 RUs. 36,920 RUs sont déduites du budget ur/m hello exclu 92,323 RUs (seconde 28) too55, 403 RUs (29 secondes)
* seconde 61st : allocation de réserve ur/m est redéfinie too100, RUs 000.
 
![Graphique montrant la consommation hello et la configuration de base de données Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Spécification de la capacité d’unités de requête avec RU/m

Lorsque vous créez une collection de base de données Azure Cosmos, vous spécifiez le nombre de hello d’unités de demande par seconde (RU par seconde) à réserver pour la collection de hello. Vous pouvez également décider si vous souhaitez RU tooadd par minute. Cela est possible via hello portail ou hello SDK. 

### <a name="through-hello-portal"></a>Via hello portail

L’activation ou désactivation des unités de requête par minute nécessite simplement un clic lors de la configuration d’une collection. 

 ![Capture d’écran montrant comment tooset ur/m Bonjour portail Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Via le Kit de développement logiciel de hello
Tout d’abord, il s’agit de toonote important qu’ur/m est uniquement disponible pour hello suivant des kits de développement logiciel :

* .Net 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Voici un extrait de code pour la création d’une collection avec 3 000 unités de demande par les unités de demande de deuxième et 30 000 par minute à l’aide de hello .NET SDK :

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

Voici un extrait de code pour modifier le débit de hello d’une collection de too5, 000 unités de demande par seconde sans configuration RU par minute à l’aide de hello .NET SDK :

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

## <a name="good-fit-scenarios"></a>Scénarios adaptés

Dans cette section, nous fournissons une vue d’ensemble des scénarios qui sont adaptés à l’activation des unités de demande par minute.

**Environnement de développement/test :** convient bien. Pendant la phase de développement hello, si vous testez votre application avec différentes charges de travail, RU/m peut fournir une grande souplesse hello à ce stade. Lors de hello [émulateur](local-emulator.md) est un excellent outil gratuit de tootest base de données Azure Cosmos. Toutefois si vous souhaitez toostart dans un environnement cloud, vous devez une avec une grande souplesse avec ur/m à vos besoins de performances ad hoc. Vous passerez le plus de temps à développer, et moins à vous inquiéter des exigences de performances au départ. Nous vous recommandons de commencer avec hello minimale ur/s mise en service et activer ur/m.

**Besoins de granularité imprévisibles, à pics, par minute :** Bien adapté – Économies : 25 à 75 %. Nous avons vu une nette amélioration des RU/m, et la plupart des scénarios de production entrent dans ce groupe. Si vous avez une charge de travail IoT a pic plusieurs fois dans une minute, si vous avez des requêtes en cours d’exécution lorsque votre système émet s’insérez en masse à hello même temps, vous devez une capacité supplémentaire pour handeling beaucoup doit. Nous vous recommandons d’optimiser vos besoins en ressources en appliquant notre approche étape par étape ci-dessous.

 ![Graphique indiquant la consommation de requête dans une granularité de 5 minutes](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Figure - Test d’évaluation de la consommation de RU*

**Tranquillité d’esprit :** Bien adapté - Économies : 10-20 %. Parfois, vous souhaitiez toohave la tranquillité d’esprit et ne vous inquiétez pas sur les pics et la limitation. Cette fonctionnalité est droite hello pour vous. Dans ce cas, nous vous recommandons d’activer les RU/m et de légèrement réduire votre approvisionnement par seconde. Ce cas est différent de hello ci-dessus comme toooptimize n’essaie pas efficacement votre configuration. Vous êtes davantage dans une mentalité « Zéro limite ».

Les opérations critiques ayant des besoins ad hoc : nous vous recommandons parfois tooonly permettent des opérations critiques accès ur/m budget afin de l’allocation de réserve hello n’obtient pas consommer par ad hoc ou moins importantes opérations. Qui peut être facilement définis dans la section hello ci-dessous.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>À l’aide de hello métriques portail toooptimize coût et les performances

**Dans les semaines à venir hello, nous développerons davantage contenu hello autour de l’analyse toooptimize de consommation minute RUs que votre débit a besoin.**

Par le biais des mesures portail hello, vous pouvez voir combien de régulières secondes RU vous consommez et RU minutes. La surveillance de ces métriques devrait vous aider à optimiser votre configuration. 

Nous vous recommandons une approche étape par étape sur la façon de toouse ur/m tooyour parti. Pour chaque étape, vous devez avoir une vue d’ensemble de la consommation de hello RU représentant un cycle complet de votre charge de travail (il peut être heures, jours ou semaines) et obtenir des informations sur l’utilisation de hello de ce que vous configurez.

principe Hello derrière cette approche est toomake votre configuration de débit comme proche que possible tooa approvisionnement point qui correspond à vos critères de performances ci-dessous. 

![Graphique indiquant la consommation de requête dans une granularité de 5 minutes](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello approvisionnement point optimal pour votre charge de travail, vous devez toounderstand :

* Les modèles de consommation : pics inexistants, peu fréquents ou courants ? Pics petits (2x en moyenne), moyens ou grands en taille (>10x en moyenne) ?
* Pourcentage de demandes limitées : restez-vous à l’aise même si vous avez un peu de limitation ? Si oui, dans quelle mesure ? 

Une fois que vous avez identifié quelles sont vos objectifs, vous serez en mesure de tooget proche toohello optimal de configuration.

tooassist vous, nous souhaitons tooprovide une recommandations générales sur comment toooptimize votre configuration en fonction de votre consommation ur/m. Cette recommandation ne s’applique pas type tooall des charges de travail, mais est basée sur la base de connaissances hello aperçu privé. Nous pourrions modifier ces lignes de base lorsque nous en apprendrons davantage :

|Utilisation de % de RU/m|Degré d’utilisation des RU/m|Actions recommandées pour la configuration|
|---|---|---|
|0-1%|Sous-utilisation|Réduire les tooconsume ur/s plus ur/m|
|1-10%|Utilisation normale|Hello même configurez niveau|
|Supérieur à 10 %|Utilisation excessive|Augmenter toorely ur/s moins sur ur/m|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Sélectionnez les opérations qui peuvent consommer allocation de réserve hello ur/m

Au niveau de la demande, vous pouvez également activer ou désactiver demande hello tooserve du budget ur/m quel que soit le type d’opération. Si le budget de RUs par seconde alloué ordinaire est consommée et demande de hello ne peut pas consommer l’allocation de réserve hello ur/m, cette demande sera limitée. Par défaut, toute requête est servie par le budget de RU/m si le budget de débit de RU/m est activé. 

Voici un extrait de code pour la désactivation de budget ur/m à l’aide de hello API DocumentDB pour les opérations CRUD et de la requête.

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

## <a name="next-steps"></a>Étapes suivantes

Dans cet article, nous avons décrit le fonctionnement du partitionnement dans Azure Cosmos DB, la création de collections partitionnées et la sélection d’une clé de partition adéquate pour votre application.

* Effectuez un test des performances et de la mise à l’échelle avec Azure Cosmos DB. Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md) pour obtenir un exemple.
* Commencer le codage par hello [kits de développement logiciel](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).
* Informez-vous sur le [débit approvisionné](request-units.md) dans Azure Cosmos DB 

