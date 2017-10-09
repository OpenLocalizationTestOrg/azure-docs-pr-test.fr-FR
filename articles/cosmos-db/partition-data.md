---
title: "aaaPartitioning et la mise à l’échelle horizontale dans la base de données Azure Cosmos | Documents Microsoft"
description: "En savoir plus sur le partitionnement de base de données Azure Cosmos, comment tooconfigure partitionnement et les clés de partition, et comment toopick hello droite clé de partition pour votre application."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Comment toopartition et l’échelle dans la base de données Azure Cosmos

[Base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) est un toohelp de service conçu global de base de données distribuées, comportant plusieurs modèles vous atteindre des performances rapides et prévisibles et une échelle en toute transparence avec votre application qu’elle se développe. Cet article fournit une vue d’ensemble de comment le partitionnement fonctionne pour toutes les données hello les modèles dans la base de données Azure Cosmos et décrit comment vous pouvez configurer l’échelle de base de données Azure Cosmos conteneurs tooeffectively vos applications.

Le partitionnement et les clés de partition sont également abordés dans cette vidéo Azure Friday avec Scott Hanselman et Shireesh Thota, responsable principal de l’ingénierie Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Partitionnement dans Azure Cosmos DB
Dans Azure Cosmos DB, vous pouvez stocker et interroger des données sans schéma avec des délais de réponse de l’ordre des millisecondes à n’importe quelle échelle. Azure Cosmos DB fournit des conteneurs pour le stockage des données, appelés **collections (pour les documents), graphiques ou tables**. Les conteneurs sont des ressources logiques. Ils peuvent s’étendre sur plusieurs partitions physiques ou serveurs. nombre de Hello de partitions est déterminé par DB Cosmos en fonction de la taille de stockage hello et débit approvisionné de hello du conteneur de hello. Chaque partition dans Azure Cosmos DB dispose d’une quantité fixe de stockage SSD associé. Elle est également répliquée pour offrir une haute disponibilité. Gestion des partitions est entièrement gérée par la base de données Azure Cosmos, et ne pas avoir un code complexe toowrite ou de gérer vos partitions. Les conteneurs Cosmos DB sont illimités en termes de débit et de stockage. 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

Le partitionnement est transparent tooyour application. COSMOS DB prend en charge rapides lectures et écritures, requêtes, la logique transactionnelle, niveaux de cohérence et contrôle d’accès précis via la ressource de conteneur unique tooa méthodes/API. descripteurs de service Hello distribution des données sur plusieurs partitions et le routage de partition de requête demandes toohello droite. 

Comment le partitionnement fonctionne-t-il ? Chaque élément doit avoir une clé de partition et une clé de ligne, qui l’identifient de façon. Votre clé de partition agit comme une partition logique pour vos données et fournit à Cosmos DB une frontière naturelle pour la distribution des données sur plusieurs partitions. En bref, voici comment le partitionnement fonctionne dans Azure Cosmos DB :

* Vous devez configurer un conteneur Cosmos DB avec un débit de `T` requêtes/s
* Coulisses de hello, partitions de dispositions Cosmos DB nécessaire tooserve `T` demandes/s. Si `T` est supérieur au débit maximal de hello par partition `t`, puis les dispositions Cosmos DB `N`  =  `T/t` partitions
* COSMOS DB alloue hello clé d’espace de partition hachages clés uniformément entre hello `N` partitions. Par conséquent, chaque partition (physique) héberge N-1 valeurs de clé de partition (partitions logiques)
* Lorsqu’une partition physique `p` atteint sa limite de stockage, base de données Cosmos fractionne en toute transparence `p` en deux partitions nouvelle `p1` et `p2` et distribue les valeurs correspondant tooroughly moitié hello clés tooeach de hello partitions. Cette opération de fractionnement est invisible tooyour application.
* De même, lorsque vous déployez un débit supérieur `t*N` débit, Cosmos DB fractionne un ou plusieurs de vos partitions toosupport hello plus élevé de débit

sémantique Hello pour les clés de partition est légèrement différentes toomatch la sémantique hello de chaque API, comme indiqué dans hello tableau suivant :

| API | Partition Key | Row Key |
| --- | --- | --- |
| Base de données de documents | custom partition key path | `id` (fixe) | 
| MongoDB | clé de partitionnement personnalisée  | `_id` (fixe) | 
| Graph | propriété de clé de partition personnalisée | `id` (fixe) | 
| Table | `PartitionKey` (fixe) | `RowKey` (fixe) | 

Cosmos DB utilise le partitionnement basé sur le hachage. Lorsque vous écrivez un élément, Cosmos DB hache la valeur de clé de partition hello et utilisez hello haché résultat toodetermine élément partition toostore hello dans. Tous les éléments avec hello la même clé de partition dans des magasins de COSMOS DB hello même partition physique. choix de Hello de clé de partition hello est une décision importante que vous avez toomake au moment du design. Vous devez choisir un nom de propriété qui possède une large plage de valeurs et des modèles d’accès uniformes.

> [!NOTE]
> Il s’agit d’une meilleure toohave de pratique une clé de partition avec de nombreuses valeurs distinctes (100 s-pour 1 000 au minimum).
>

Les conteneurs Azure Cosmos DB peuvent être créés comme étant « fixes » ou « illimités ». Les conteneurs de taille fixe ont une limite maximale de 10 Go et de 10 000 RU/s de débit. Certaines API permettent toobe de clé de partition hello omis pour les conteneurs de taille fixe. toocreate un conteneur comme étant illimité, vous devez spécifier un débit minimum de 2500 ur/s.

## <a name="partitioning-and-provisioned-throughput"></a>Partitionnement et débit approvisionné
Cosmos DB est conçu pour offrir des performances prévisibles. Lorsque vous créez un conteneur, vous réservez le débit en termes de **[d’unités de requête](request-units.md) (RU) par seconde avec un ajout potentiel pour les unités de requête par minute**. Chaque requête est assignée à un coût unitaire de demande qui est le montant proportionnel toohello de ressources système telles que le processeur, mémoire et e/s consommées par opération de hello. La lecture d’un document de 1 ko avec une cohérence de session consomme une unité de demande. Une lecture est 1 RU, quelle que soit le nombre de hello d’éléments stockés ou hello du nombre de demandes simultanées en cours d’exécution à hello même temps. Les éléments plus volumineux nécessitent plus élevé d’unités de demande en fonction de la taille de hello. Si vous connaissez taille hello vos entités et hello du nombre de lectures vous devez toosupport pour votre application, vous pouvez configurer la quantité exacte de hello du débit requis pour votre application de lecture de vos besoins. 

> [!NOTE]
> tooachieve hello un débit complet du conteneur de hello, vous devez choisir une clé de partition qui vous permet de tooevenly distribuer les requêtes entre certaines valeurs de clé de partition distincte.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Utilisation des API de base de données Azure Cosmos de hello
Vous pouvez utiliser hello portail Azure ou les conteneurs de toocreate CLI d’Azure et mettre à l’échelle à tout moment. Cette section montre comment les conteneurs toocreate et spécifiez hello débit et la partition de définition de la clé dans chacune des hello les API prises en charge.

### <a name="documentdb-api"></a>API DocumentDB
Hello suivant l’exemple montre comment un conteneur (collection) à l’aide de toocreate hello API DocumentDB. Vous trouverez plus de détails dans [Partitionnement avec l’API DocumentDB](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Vous pouvez lire un élément (document) à l’aide de hello `GET` méthode hello API REST ou en utilisant les `ReadDocumentAsync` dans un des kits de développement logiciel de hello.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>API MongoDB
Avec hello MongoDB API, vous pouvez créer une collection partitionnée à l’aide de votre outil préféré, le pilote ou le Kit de développement logiciel. Dans cet exemple, nous utilisons hello de commande Mongo pour la création de la collection hello.

Bonjour interpréteur de commandes Mongo :

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Résultats :

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>API de table

Avec hello API de Table, vous devez spécifier le débit pour les tables hello configuration appSettings de hello pour votre application :

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Ensuite, vous créez une table à l’aide du stockage de Table Azure hello SDK. clé de partition Hello est implicitement créé en tant que hello `PartitionKey` valeur. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Vous pouvez récupérer une entité unique à l’aide de hello suivant extrait de code :

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Consultez [développement avec hello API Table](tutorial-develop-table-dotnet.md) pour plus d’informations.

### <a name="graph-api"></a>API Graph

Avec hello API Graph, vous devez utiliser hello portail Azure ou les conteneurs de toocreate CLI. Ou bien, Azure Cosmos DB étant comportant plusieurs modèle, vous pouvez une des hello autres toocreate de modèles et mettre à l’échelle de votre conteneur graphique.

Vous pouvez lire les sommets ou un bord à l’aide de la clé de partition hello et id dans GREMLINE. Par exemple, pour un graphique avec la région (« USA ») en tant que clé de partition hello et « Seattle » en tant que clé de ligne hello, vous trouverez un sommet à l’aide de la syntaxe de hello :

```
g.V(['USA', 'Seattle'])
```

Même avec les contours, vous pouvez référencer un bord à l’aide de la clé de partition hello et clé de ligne.

```
g.E(['USA', 'I5'])
```

Consultez la page [Prise en charge de Gremlin pour Cosmos DB](gremlin-support.md) pour plus de détails.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Conception du partitionnement
tooscale efficacement avec la base de données Azure Cosmos, vous devez toopick une bonne clé de partition lorsque vous créez votre conteneur. Il existe deux considérations essentielles pour le choix d’une clé de partition :

* **Limite de requête et les transactions**: votre choix de clé de partition doit équilibrer l’utilisation des hello hello besoin tooenable de transactions par rapport à hello exigence toodistribute vos entités sur plusieurs tooensure de clés de partition d’une solution évolutive. Une des extrémités, vous pouvez définir hello même clé de partition pour tous vos éléments, mais cela peut limiter l’extensibilité du hello de votre solution. À hello inverse, vous pouvez affecter une clé de partition unique pour chaque élément, ce qui serait hautement évolutive, mais vous empêchent de l’utilisation de transactions entre des documents via des procédures stockées et les déclencheurs. Une clé de partition idéale est un qui vous permet de toouse des requêtes efficaces et qui a une cardinalité suffisamment tooensure votre solution est évolutive. 
* **Aucun goulet d’étranglement de performances et de stockage**: il est important de toopick une propriété qui permet d’écrit toobe répartis entre les différentes valeurs distinctes. Demandes toohello même clé de partition ne peut pas dépasser le débit d’une partition unique hello et sont limités. Il est donc important toopick une clé de partition qui n’entraîne pas de « zones réactives » au sein de votre application. Puisque toutes les données hello pour une clé de partition unique doit être stockée dans une partition, il est également recommandé des clés de partition tooavoid qui ont des volumes élevés de données pour hello même valeur. 

Nous allons examiner quelques scénarios réels et les bonnes clés de partition à chaque fois :
* Si vous implémentez un service de profil utilisateur principal, l’ID d’utilisateur hello est un bon choix pour la clé de partition.
* Si vous stockez des données IoT, comme l’état d’appareil, un ID d’appareil constitue un bon choix pour la clé de partition.
* Si vous utilisez une base de données Azure Cosmos pour la journalisation des données de série chronologique, puis hello nom d’hôte ou l’ID de processus est un bon choix pour la clé de partition.
* Si vous disposez d’une architecture mutualisée, ID de client hello est un bon choix pour la clé de partition.

Dans certains cas comme IoT d’utilisation et les profils utilisateur, clé de partition hello peut être hello même comme id (clé de document). Dans d’autres données de série chronologique hello, vous pouvez avoir une clé de partition qui est différente de celle des id de hello.

### <a name="partitioning-and-loggingtime-series-data"></a>Partitionnement et journalisation de données de série chronologique
Un des cas d’usage courants hello de base de données Cosmos est pour l’enregistrement et les données de télémétrie. Il est important toopick une bonne clé de partition, car vous devrez peut-être tooread/écriture d’importants volumes de données. choix de Hello dépend de votre en lecture et écriture taux et les types de requêtes que vous attendez toorun. Voici quelques conseils sur la façon de toochoose une bonne clé de partition.

* Si votre cas d’usage implique un petit taux d’écrit accumulation sur une longue période de temps et besoin tooquery par plages d’horodatages et les autres filtres, puis à l’aide d’un correctif cumulatif de timestamp hello, par exemple, date comme une clé de partition est une bonne approche. Ainsi, vous tooquery sur toutes les données hello pour une date à partir d’une seule partition. 
* Si votre charge de travail est lourde en écriture, ce qui est plus courant, vous devez utiliser une clé de partition qui n’est pas basée sur l’horodatage, afin que Cosmos DB puisse répartir uniformément les écritures sur diverses partitions. Dans ce cas, un nom d’hôte, un ID de processus, un ID d’activité ou une autre propriété présentant une cardinalité élevée constituent un bon choix. 
* Une troisième méthode est un hybride une où vous disposez de plusieurs conteneurs, une pour chaque jour/mois et de clé de partition hello est une propriété granulaire comme nom d’hôte. Cela a pour avantage hello que vous pouvez définir différents débit en fonction de la fenêtre de temps hello, par exemple, conteneur hello pour hello mois en cours est configuré avec un débit plus élevé, car il fait Office de lectures et écritures, tandis que les mois précédents à diminuer le débit depuis ils servent uniquement des lectures.

### <a name="partitioning-and-multi-tenancy"></a>Partitionnement et mutualisation
Si vous implémentez une application mutualisée à l’aide de Cosmos DB, il existe deux modèles populaires : une clé de partition par client et un conteneur par client. Avantages et inconvénients de chaque hello sont :

* Une clé de partition par client : dans ce modèle, les clients sont colocalisés au sein d’un conteneur unique. Mais les requêtes et les insertions pour les éléments avec un seul client peuvent être exécutées sur une partition unique. Vous pouvez également implémenter une logique transactionnelle sur tous les éléments avec un client. Étant donné que plusieurs clients partagent un conteneur, vous économisez des coûts de stockage et de débit en regroupant les ressources pour les clients dans un seul conteneur plutôt que d’approvisionner une marge supplémentaire pour chaque client. Hello inconvénient que vous n’avez pas l’isolation des performances par locataire. Augmentation des performances ou de débit s’appliquent toohello tout conteneur vs ciblés augmente pour les clients.
* Un conteneur par client : chaque client possède son propre conteneur. Dans ce modèle, vous pouvez réserver des performances par client. Avec le nouveau modèle de tarification du provisionnement de Cosmos DB, ce modèle est plus rentable pour les applications mutualisées avec peu de clients.

Vous pouvez également utiliser une approche hiérarchisé combinaison collocates petits locataires et migre le plus grand conteneur propre tootheir de clients.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, nous avons proposé une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB. 

* Apprenez-en davantage sur le [débit approvisionné dans Azure Cosmos DB](request-units.md)
* En savoir plus sur la [distribution globale dans Azure Cosmos DB](distribute-data-globally.md)



