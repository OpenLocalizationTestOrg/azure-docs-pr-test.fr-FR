---
title: "aaaRequest unités et estimer le débit - base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toounderstand, spécifiez et estimer les besoins d’unité de demande dans la base de données Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Unités de requête dans Azure Cosmos DB
Désormais disponible : [calculatrice d’unités de requête](https://www.documentdb.com/capacityplanner) Azure Cosmos DB. Pour en savoir plus, consultez [Estimation des besoins de débit](request-units.md#estimating-throughput-needs).

![Calculatrice de débit][5]

## <a name="introduction"></a>Introduction
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) est un service de base de données multimodèle mondialement distribué de Microsoft. Avec la base de données Azure Cosmos, vous n’avez toorent des machines virtuelles, déployer des logiciels ou surveiller les bases de données. Azure Cosmos DB est traitée et en permanence contrôlé par Microsoft ingénieurs supérieur toodeliver world classe disponibilité, performances et protection des données. Vous pouvez accéder à vos données à l’aide des API de votre choix, sachant que les API [SQL DocumentDB](documentdb-sql-query.md) (document), MongoDB (document), [Stockage Table Azure](https://azure.microsoft.com/services/storage/tables/) (clé-valeur) et [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graphique) sont toutes prises en charge de manière native. Hello la devise de base de données Azure Cosmos est hello unité demande (RU). Avec RUs, vous n’avez pas besoin de capacités de lecture/écriture tooreserve ou de disposition du processeur, mémoire et e/s.

Azure Cosmos DB prend en charge un certain nombre d’API avec différentes opérations allant de simples lit et écrit toocomplex les requêtes de graphique. Pas toutes les demandes étant égales, ils sont attribués à une quantité normalisée de **unités de requête** selon la quantité hello de demande de calcul requis tooserve hello. nombre de Hello d’unités de demande pour une opération est déterministe, et vous pouvez suivre le nombre de hello d’unités de demande consommé par aucune opération dans la base de données Azure Cosmos via un en-tête de réponse. 

tooprovide des performances prévisibles, vous devez débit tooreserve en unités de 100 ur/seconde. 

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :  

* Que sont les unités de requête et les frais de requête ?
* Comment spécifier la capacité d’unités de requête pour une collection ?
* Comment estimer les besoins en unités de requête de mon application ?
* Que se passe-t-il si je dépasse la capacité d’unités de requête pour une collection ?

Azure Cosmos DB est une base de données comportant plusieurs modèle, il est important toonote que nous appelons tooa collection ou de document pour un document API, un nœud/graphique pour une API graph et/une entité de table pour l’API de table. Débit de ce document, nous allons généraliser toohello les concepts de conteneur ou cet élément.

## <a name="request-units-and-request-charges"></a>Unités de requête et frais de requête
Base de données Cosmos Azure offre des performances rapides et prévisibles par *réservation* ressources toosatisfy a besoin d’un débit de votre application.  Étant donné que l’application charge et schémas d’accès changent au fil du temps, base de données Azure Cosmos vous permet d’augmenter de tooeasily ou diminuer hello application tooyour disponible de débit réservés.

Avec Azure Cosmos DB, un débit réservé est spécifié en termes de traitement d’unités de requête par seconde. Vous pouvez considérer d’unités de demande comme devise de débit, dans laquelle vous *réserver* garantie de la quantité d’unités de demande application tooyour disponible sur par seconde.  Chaque opération dans Azure Cosmos DB (écriture d’un document, exécution d’une requête, mise à jour d’un document) consomme des ressources de processeur, de mémoire et d’E/S par seconde.  Autrement dit, chaque opération entraîne des *frais de requête*, exprimés en *unités de requête*.  Comprendre les facteurs hello qui a un impact sur les coûts d’unité de demande, ainsi que les exigences de débit de votre application, permet de vous toorun votre application en tant que coût efficacement que possible. l’Explorateur de requête Hello est également un outil merveilleux tootest hello core d’une requête.

Nous vous recommandons de mise en route en regardant hello suivant vidéo, où Aravind Ramachandran explique les unités de demande et de la prévisibilité des performances avec la base de données Azure Cosmos.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Spécification de la capacité d’unités de requête dans Azure Cosmos DB
Lorsque vous démarrez une nouvelle collection, un tableau ou un graphique, vous spécifiez le nombre de hello d’unités de demande par seconde (RU par seconde) à réserver. Selon le débit approvisionné de hello, base de données Azure Cosmos alloue toohost de partitions physiques votre collection et fractionnements/rebalances données sur plusieurs partitions qu’elle se développe.

Base de données Azure Cosmos requiert qu'un toobe de clé de partition spécifié lorsqu’une collection est configurée avec 2 500 unités de demande ou une version ultérieure. Une clé de partition est également requis tooscale débit de votre collection au-delà de 2 500 unités de demande Bonjour futures. Par conséquent, il est vivement recommandé tooconfigure un [clé de partition](partition-data.md) lors de la création d’un conteneur, quelle que soit votre débit initial. Étant donné que vos données peuvent avoir toobe divisée en plusieurs partitions, il est nécessaire toopick une clé de partition qui a une cardinalité élevée (100 toomillions de valeurs distinctes) afin que votre collection/table/graphique et les demandes peuvent être monté en uniformément par base de données Azure Cosmos. 

> [!NOTE]
> Une clé de partition est une limite logique et non physique. Par conséquent, vous n’avez pas besoin de nombre de hello toolimit partition distinctes des valeurs de clé. Il s’agit en fait une meilleure toohave plus distincte inférieure, des valeurs de clé de partition comme base de données Azure Cosmos a plus d’options d’équilibrage de charge.

Voici un extrait de code pour la création d’une collection de 3 000 demande unités par seconde en utilisant hello .NET SDK :

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB fonctionne sur un modèle de réservation du débit. Autrement dit, vous êtes facturé pour la quantité de hello de débit *réservé*, quelle que soit la quantité que le débit est activement *utilisé*. Comme charge, les données et l’utilisation de modèles modification de votre application vous pouvez facilement évoluer hello quantité réservées RUs via les kits de développement logiciel ou à l’aide de hello [Azure Portal](https://portal.azure.com).

Chaque collection/table/graphique sont mappés tooan `Offer` ressource dans Cosmos base de données Azure, qui contient les métadonnées sur le débit approvisionné de hello. Vous pouvez modifier le débit de hello allouée en recherchant la ressource offre correspondante de hello pour un conteneur, puis mettre à jour avec la nouvelle valeur de débit hello. Voici un extrait de code pour modifier le débit de hello d’une collection de too5, 000 unités de demande par seconde en utilisant hello .NET SDK :

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Il n’est pas votre conteneur de disponibilité toohello impact lorsque vous modifiez un débit hello. Débit de nouveau réservés hello est généralement efficace en quelques secondes dans l’application du débit de nouveau hello.

## <a name="request-unit-considerations"></a>Considérations relatives aux unités de requête
Lorsque vous estimez le nombre de hello de tooreserve d’unités de demande pour votre conteneur de base de données Azure Cosmos, il est hello tootake important suivant des variables en considération :

* **Taille de l’élément**. Comme la taille augmente hello unités consommées tooread ou écrire des données hello augmente également.
* **Nombre de propriétés de l’élément**. En supposant que la valeur par défaut de l’indexation de toutes les propriétés, toowrite d’unités consommées hello un document/nœud/ntity augmente à mesure que de l’augmentation du nombre de propriété hello.
* **Cohérence des données**. Lorsque vous utilisez des niveaux de cohérence des données de Strong ou Bounded Staleness, des unités supplémentaires seront consommées tooread éléments.
* **Propriétés indexées**. Une stratégie d’indexation sur chaque conteneur détermine quelles propriétés sont indexées par défaut. Vous pouvez réduire la consommation de votre unité de demande en limitant le nombre de hello des propriétés indexées ou en activant l’indexation différée.
* **Indexation des documents**. Par défaut de que chaque élément est automatiquement indexé, vous allez consommer moins d’unités de demande si vous choisissez tooindex pas certains de vos éléments.
* **Modèles de requête**. complexité Hello d’une requête a un impact sur le nombre d’unités demande sont consommé pour une opération. nombre Hello de prédicats, de la nature de hello prédicats, projections, nombre des UDF et la taille de hello du jeu de données source hello tous influencent coût hello d’opérations de requête.
* **Utilisation des scripts**.  Comme avec les requêtes, des procédures stockées et les déclencheurs consomment des unités de demande en fonction de la complexité de hello d’opérations hello en cours d’exécution. Lorsque vous développez votre application, inspecter des frais de demande hello en-tête toobetter comprendre comment chaque opération consomme la capacité des unités de demande.

## <a name="estimating-throughput-needs"></a>Estimation des besoins de débit
Une unité de requête est une mesure normalisée du coût de traitement de la requête. Une unité de demande unique représente hello traitement capacité requise tooread (via l’élément self link ou id) un 1 Ko unique élément composé de 10 valeurs de propriété unique (à l’exception des propriétés système). Une demande de toocreate (insert), remplacer ou supprimer des hello même élément consommera plus de traitement du service de hello et donc plusieurs unités de requête.   

> [!NOTE]
> ligne de base Hello d’unité de 1 demande pour une base de connaissances 1 correspond élément tooa simple obtenir par id d’élément de hello ou un élément self link.
> 
> 

Par exemple, Voici un tableau qui indique le nombre de demandes tooprovision unités à trois tailles d’élément différent (1 Ko, 4 Ko et 64 Ko) et à deux niveaux de performance différents (lectures par seconde de 500 écritures par seconde de 100 et 500 lectures par seconde + 500 écritures par seconde). la cohérence des données Hello a été configurée au niveau de la Session et hello stratégie d’indexation a été défini tooNone.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Taille de l’élément</strong></p></td>
            <td valign="top"><p><strong>Lectures par seconde</strong></p></td>
            <td valign="top"><p><strong>Écritures par seconde</strong></p></td>
            <td valign="top"><p><strong>Unités de demande</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 Ko</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1 000 UR/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 Ko</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3 000 UR/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 Ko</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1.3) + (100 * 7) = 1 350 UR/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 Ko</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1.3) + (500 * 7) = 4 150 UR/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 Ko</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9 800 UR/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 Ko</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29 000 UR/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Utiliser la calculatrice des unités hello demande
clients toohelp fines paramétrer les estimations de débit, il est basé sur le web [calculatrice des unités de demande](https://www.documentdb.com/capacityplanner) toohelp estimation hello demande unité configuration requise pour les opérations courantes, notamment :

* Créations (écritures) d’éléments
* Lectures d’éléments
* Suppressions d’éléments
* Mises à jour d’éléments

outil de Hello inclut également la prise en charge pour l’estimation des besoins de stockage de données en fonction de vous fournissez des exemples d’éléments de hello.

À l’aide d’outil de hello est simple :

1. Chargez un ou plusieurs éléments représentatifs.
   
    ![Télécharger la calculatrice des unités de demande toohello éléments][2]
2. exigences de stockage de données tooestimate, entrez le nombre total de hello d’éléments toostore prévu.
3. Entrez nombre hello d’éléments à créer, lire, mettre à jour et supprimer les opérations que vous avez besoin (sur une base par seconde). coûts d’unité de demande hello tooestimate d’opérations de mise à jour d’élément, téléchargez une copie de l’exemple d’élément hello à l’étape 1 ci-dessus qui inclut les mises à jour de champ par défaut.  Par exemple, si les mises à jour de l’élément généralement modifient deux propriétés nommées lastLogin et userVisits, puis copiez simplement exemple d’élément hello, mettre à jour les valeurs hello pour ces deux propriétés et télécharger hello copié des éléments.
   
    ![Entrez des exigences de débit de la calculatrice d’unité hello demande][3]
4. Cliquez sur Calculer et examiner les résultats de hello.
   
    ![Résultats de la calculatrice d’unités de demande][4]

> [!NOTE]
> Si vous avez des types d’éléments qui varient considérablement en termes de taille et hello nombre de propriétés indexées, puis télécharger un exemple de chaque *type* de l’élément toohello outil, puis calcule les résultats hello.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Utiliser l’en-tête de réponse des frais hello Azure Cosmos DB demande
Chaque réponse de hello service de base de données Azure Cosmos inclut un en-tête personnalisé (`x-ms-request-charge`) qui contient les unités de demande hello consommées pour la demande de hello. Cet en-tête est également accessible via hello kits de développement de base de données Azure Cosmos. Bonjour .NET SDK, RequestCharge est une propriété d’objet de ResourceResponse hello.  Pour les requêtes, hello Azure Cosmos DB requête Explorer Bonjour portail Azure fournit des informations de frais de demande pour les requêtes exécutées.

![Examen des frais RU Bonjour Explorer de requête][1]

Dans cet esprit, une méthode d’estimation de la quantité de hello de débit réservés requise par votre application est toorecord hello demande unité des frais associés avec les opérations en cours d’exécution par rapport à un élément représentatif utilisé par votre application, puis estimation du nombre de hello d’opérations vous comptez effectuer chaque seconde.  Être vraiment toomeasure et inclure des requêtes et utilisation des scripts de base de données Azure Cosmos ainsi.

> [!NOTE]
> Si vous avez des types d’éléments qui varient considérablement en termes de taille et hello nombre de propriétés indexées, puis enregistrer des frais d’unité hello opération applicable demande associées à chaque *type* d’élément.
> 
> 

Par exemple :

1. Enregistrer des frais d’unitaires hello demande de création (insertion) un élément. 
2. Enregistrement hello demande unité des frais de la lecture d’un élément.
3. Enregistrement hello demande unité des frais de mise à jour d’un élément.
4. Enregistrement hello demande unité des frais de requêtes d’élément classiques, courantes.
5. Enregistrement hello demande frais unitaires des scripts personnalisés (procédures stockées, déclencheurs, fonctions définies par l’utilisateur) exploité par l’application hello
6. Calculer les demande requis hello qu'unités indiqué le nombre estimé de hello d’opérations vous anticipez toorun chaque seconde.

### <a id="GetLastRequestStatistics"></a>Utiliser la commande GetLastRequestStatistics de l’API pour MongoDB
API pour MongoDB prend en charge une commande personnalisée, *getLastRequestStatistics*, pour récupérer des frais de demande hello pour les opérations spécifiées.

Par exemple, Bonjour Mongo Shell, exécutez opération hello tooverify hello demande frais pour.
```
> db.sample.find()
```

Ensuite, exécutez la commande hello *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

Dans cet esprit, une méthode d’estimation de la quantité de hello de débit réservés requise par votre application est toorecord hello demande unité des frais associés avec les opérations en cours d’exécution par rapport à un élément représentatif utilisé par votre application, puis estimation du nombre de hello d’opérations vous comptez effectuer chaque seconde.

> [!NOTE]
> Si vous avez des types d’éléments qui varient considérablement en termes de taille et hello nombre de propriétés indexées, puis enregistrer des frais d’unité hello opération applicable demande associées à chaque *type* d’élément.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>Utiliser les mesures du portail de l’API pour MongoDB
Hello tooget de façon la plus simple de frais une bonne estimation de l’unité de demande correspondant à votre API pour la base de données MongoDB est toouse hello [portail Azure](https://portal.azure.com) métriques. Avec hello *nombre de demandes* et *demande frais* graphiques, vous pouvez obtenir une estimation du nombre d’unités de demande chaque opération est le nombre d’unités de demande et de consommation tomberont relatif tooone un autre.

![Mesures du portail de l’API pour MongoDB][6]

## <a name="a-request-unit-estimation-example"></a>Exemple d’estimation d’unités de requête
Tenez compte des hello suivant le document de ~ 1 Ko :

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> Les documents sont réduites dans la base de données Azure Cosmos, donc calculé par le système de hello taille du document hello ci-dessus est légèrement inférieure à 1 Ko.
> 
> 

Hello tableau suivant illustre approximative demande coûts d’unité pour les opérations courantes sur cet élément (hello demande approximative unité frais part du principe que le niveau de cohérence de compte de hello est défini trop « Session » et que tous les éléments sont indexés automatiquement) :

| Opération | Frais d’unités de requête |
| --- | --- |
| Créer un élément |~15 unités de requête |
| Lire un élément |~1 unité de requête |
| Interroger un élément par id |~2,5 unités de requête |

En outre, ce tableau montre demande approximative de coûts d’unité pour les requêtes par défaut utilisés dans une application hello :

| Interroger | Frais d’unités de requête | Nombre d’éléments renvoyés |
| --- | --- | --- |
| Sélectionner un aliment par id |~2,5 unités de requête |1 |
| Sélectionner un aliment par fabricant |~7 unités de requête |7 |
| Sélectionner par groupe d’aliments et trier par poids |~70 unités de requête |100 |
| Sélectionner les 10 premiers aliments dans un groupe d’aliments |~10 unités de requête |10 |

> [!NOTE]
> Frais de RU varient en fonction nombre hello d’éléments renvoyés.
> 
> 

Avec ces informations, nous pouvons estimer les besoins en RU hello pour ce numéro hello d’application en raison d’opérations et nous pensons que par seconde de requêtes :

| Opération/Requête | Nombre estimé par seconde | Unités de requête nécessaires |
| --- | --- | --- |
| Créer un élément |10 |150 |
| Lire un élément |100 |100 |
| Sélectionner un aliment par fabricant |25 |175 |
| Sélectionner par groupe d’aliments |10 |700 |
| Sélectionner les 10 premiers |15 |150 Total |

Dans ce cas, nous estimons l’exigence de débit moyen à 1275 unités de requête par seconde.  Arrondi toohello le plus proche de 100, nous serait approvisionner 1 300 ur/s pour la collecte de cette application.

## <a id="RequestRateTooLarge"></a> Dépassement des limites de débit réservé dans Azure Cosmos DB
Rappelez-vous que la consommation d’unités de demande est évaluée comme un taux par seconde si l’allocation de réserve hello est vide. Pour les applications qui dépassent hello demande approvisionné unité pour un conteneur, demandes toothat collection vont être activée jusqu'à ce que le débit de hello devient inférieur au niveau de hello réservé. Lorsqu’une limitation se produit, le serveur de hello va se terminer manière préemptive demande hello avec RequestRateTooLargeException (code d’état HTTP 429) et en retour hello x-ms-nouvelle tentative-après-ms en-tête indiquant hello durée, en millisecondes, pendant lequel hello utilisateur doit attendre avant nouvelle tentative de demande de hello.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Si vous utilisez des requêtes de Client .NET SDK et LINQ hello, puis la plupart du temps hello jamais avoir toodeal avec cette exception, comme la version actuelle de hello Hello Client .NET SDK intercepte implicitement cette réponse, égards hello spécifiée par le serveur en-tête retry-after, et demande de hello de nouvelles tentatives. À moins que votre compte est accessible simultanément par plusieurs clients, hello suivant sera réalisée.

Si vous avez plusieurs clients cumulative fonctionne au-delà des taux de demandes hello, hello nouvelle tentative par défaut ne peut-être pas suffire, et client de hello lèvera une DocumentClientException avec application de toohello 429 état code. Dans ce cas, vous pouvez envisager de la gestion des nouvelles tentatives et logique de l’erreur de votre application des routines de gestion ou augmente le débit réservé de hello pour le conteneur de hello.

## <a id="RequestRateTooLargeAPIforMongoDB"></a> Dépassement des limites de débit réservé dans l’API pour MongoDB
Les applications qui dépassent les unités de demande hello configuré pour une collection vont être activées jusqu'à ce que le débit de hello devient inférieur au niveau de hello réservé. En cas d’une limitation de bande passante, hello principal se termine manière préemptive demande hello avec un *16500* code d’erreur - *trop grand nombre de demandes*. Par défaut, les API pour MongoDB va retenter automatiquement des heures de too10 avant de retourner un *trop grand nombre de demandes* code d’erreur. Si vous recevez plusieurs *trop grand nombre de demandes* codes d’erreur, vous pouvez envisager l’ajout comportement des nouvelles tentatives dans Gestion d’erreur de votre application routines ou [augmente le débit réservé de hello pour collection de hello](set-throughput.md).

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur le débit réservé avec les bases de données de base de données Azure Cosmos, Explorez ces ressources :

* [Tarification de Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Partitionnement, clés de partition et mise à l’échelle dans Azure Cosmos DB](partition-data.md)

toolearn savoir plus sur la base de données Azure Cosmos, consultez hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/). 

tooget en main de l’échelle et des tests de performances avec la base de données Azure Cosmos, consultez [test de performances et montée en puissance avec la base de données Azure Cosmos](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
