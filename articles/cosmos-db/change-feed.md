---
title: "prise en charge de flux aaaWorking avec modification de hello dans la base de données Azure Cosmos | Documents Microsoft"
description: "Utilisez Azure Cosmos DB modifier les modifications tootrack de prise en charge des flux dans les documents et exécuter basés sur les événements de traitement tout comme les déclencheurs et la maintenance des systèmes de caches et analytique à."
keywords: change feed
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Utilisation de la prise en charge flux hello modification dans la base de données Azure Cosmos
[Azure Cosmos DB](../cosmos-db/introduction.md) est un service de base de données répliqué mondialement, rapide et flexible utilisé pour le stockage d’importants volumes de données transactionnelles et opérationnelles avec une latence prévisible en quelques millisecondes pour les lectures et les écritures. Il est ainsi parfait pour les applications d’IoT, de jeux, de vente au détail et de journalisation des compteurs. Un modèle de conception courants dans ces applications est tootrack modifications apportées tooAzure la Cosmos base de données et mettre à jour les vues matérialisées, effectuer l’analytique en temps réel, archive toocold stockage des données et des notifications de déclenchement de certains événements en fonction de ces modifications. Hello **prise en charge de flux de changement** dans la base de données Azure Cosmos vous permet de toobuild efficace et évolutive des solutions pour chacun de ces modèles.

Modification de flux de prise en charge, base de données Azure Cosmos fournit une liste triée de documents dans une collection de base de données Azure Cosmos dans l’ordre de hello dans lequel ils ont été modifiés. Ce flux peut être toolisten utilisé pour toodata des modifications au sein de la collection de hello et effectuer des actions telles que :

* Déclencher une tooan appel API lorsqu’un document est inséré ou modifié
* effectuer un traitement en temps réel (flux) sur les mises à jour ;
* synchroniser les données avec un cache, le moteur de recherche ou l’entrepôt de données.

Les modifications dans Azure Cosmos DB sont conservées et peuvent être traitées de manière asynchrone et réparties sur un ou plusieurs consommateurs pour un traitement en parallèle. Examinons hello API pour les flux de modification et comment vous pouvez les utiliser toobuild hautement évolutives en temps réel. Cet article explique comment toowork avec la base de données Azure Cosmos modifier le flux et hello API DocumentDB. 

![À l’aide de la modification de la base de données Azure Cosmos flux analytique en temps réel de toopower et des scénarios de traitement pilotée par événements](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Modification de flux de prise en charge est disponible que pour hello API DocumentDB pour l’instant ; Hello API Graph et API de Table ne sont pas pris en charge actuellement.

## <a name="use-cases-and-scenarios"></a>Cas d'utilisation et scénarios
Flux de modification permet un traitement efficace de grands jeux de données avec un grand nombre d’écritures et offre une tooidentify de jeux de données entière tooquerying autre ce qui a changé. Par exemple, vous pouvez effectuer hello efficacement des tâches suivantes :

* Mettre à jour un cache, l’index de recherche ou un entrepôt de données avec les données stockées dans Azure Cosmos DB.
* Implémenter hiérarchisation et d’archivage de données de niveau application, autrement dit, stocker des données « chaudes » dans la base de données Azure Cosmos et expire trop de « données à froid »[stockage d’objets Blob Azure](../storage/common/storage-introduction.md) ou [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Implémenter une analyse en mode batch sur les données à l’aide [d’Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implémenter des [pipelines lambda sur Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) avec Azure Cosmos DB. Azure Cosmos DB fournit une solution de base de données évolutive qui peut gérer l’ingestion et l’interrogation, et implémenter des architectures lambda avec un faible coût total de possession. 
* Effectuer un zéro tooanother migrations d’inactivité du compte de base de données Azure Cosmos avec un schéma de partitionnement différent.

**Pipelines lambda avec Azure Cosmos DB pour l’ingestion et l’interrogation :**

![Pipeline lambda Azure Cosmos DB pour l’ingestion et l’interrogation](./media/change-feed/lambda.png)

Vous pouvez utiliser tooreceive de la base de données Azure Cosmos et stocker les données d’événement à partir d’appareils, capteurs, l’infrastructure et les applications et traiter ces événements en temps réel avec [Analytique de flux de données Azure](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), ou [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Au sein de votre [sans](http://azure.com/serverless) web et des applications mobiles, vous pouvez suivre les événements tels que tootrigger de profil, préférences ou l’emplacement du client de modifications tooyour certaines actions, telles que l’envoi push appareils tootheir de notifications à l’aide de [Fonctions azure](../azure-functions/functions-bindings-documentdb.md) ou [des Services d’application](https://azure.microsoft.com/services/app-service/). Si vous utilisez une base de données Azure Cosmos toobuild un jeu, vous pouvez, par exemple, utiliser ajouterons en temps réel de modification tooimplement de flux basé sur des scores à partir de jeux terminées.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Fonctionnement du flux de modification dans Azure Cosmos DB
Base de données Azure Cosmos fournit hello capacité tooincrementally lire tooan de mises à jour la collection de base de données Azure Cosmos. Ce flux du changement a hello propriétés suivantes :

* Les modifications sont persistantes dans Azure Cosmos DB et peuvent être traitées de façon asynchrone.
* Toodocuments de modifications dans une collection de sont disponibles immédiatement dans le flux de changement de hello.
* Chaque modification tooa document apparaît une seule fois dans le flux du changement hello et clients de gérer leur logique de points de contrôle. bibliothèque de flux de processeur Hello modification fournit des points de contrôle automatiques et « au moins une fois » sémantique.
* Modification la plus récente hello uniquement pour un document donné est incluse dans le journal des modifications hello. Les modifications intermédiaires peuvent ne pas être disponibles.
* flux de modification Hello est triée par ordre de modification au sein de chaque valeur de clé de partition. Il n’existe aucun ordre garanti entre les valeurs de clé de partition.
* Les modifications peuvent être synchronisées à partir de n’importe quel moment donné ; autrement dit, il n’existe aucune période de rétention de données fixes pendant laquelle les modifications sont disponibles.
* Les modifications sont disponibles dans des blocs de plages de clés de partition. Cette fonctionnalité permet des modifications à partir de toobe de grandes collections traités en parallèle par plusieurs consommateurs/serveurs.
* Les applications peuvent demander pour modifier plusieurs flux simultanément sur hello même collection.

Le flux de modification d’Azure Cosmos DB est activé par défaut pour tous les comptes. Vous pouvez utiliser votre [débit approvisionné](request-units.md) dans votre région d’écriture ou les [lire zone](distribute-data-globally.md) tooread de hello modifier le flux, comme toute autre opération de base de données Azure Cosmos. flux de changement de Hello inclut les insertions et les opérations de mise à jour apportées toodocuments au sein de la collection de hello. Vous pouvez capturer des suppressions en définissant un indicateur de « suppression réversible » dans vos documents à la place des suppressions. Vous pouvez également définir une période d’expiration de vos documents via hello [fonctionnalité de la durée de vie](time-to-live.md), pour l’exemple, 24 heures et utilisation hello la valeur de cette propriété toocapture supprime. Avec cette solution, vous avez tooprocess modifications dans un intervalle de temps inférieur à la période d’expiration de durée de vie hello. Hello modification flux n’est disponible pour chaque plage de clés de partition dans la collection de documents hello et par conséquent, peut être distribué sur un ou plusieurs consommateurs pour un traitement parallèle. 

![Traitement distribué du flux de modification d’Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

Vous avez plusieurs options pour implémenter une modification de flux dans votre code client. Hello sections qui est immédiatement suivi décrivent comment les tooimplement hello du flux de modification à l’aide de hello API REST de Azure Cosmos DB et hello kits de développement logiciel DocumentDB. Toutefois, pour les applications .NET, nous vous recommandons d’utiliser hello nouvelle [processeur bibliothèque de flux de modification](#change-feed-processor) pour le traitement des événements à partir de hello modifient le flux lorsqu’il simplifie les modifications de la lecture sur plusieurs partitions et permet à plusieurs threads en parallèle. 

## <a id="rest-apis"></a>Utilisation de hello API REST et les kits de développement logiciel DocumentDB
Azure Cosmos DB fournit des conteneurs élastiques de stockage et de débit appelés **collections**. Les données contenues dans les collections sont regroupées logiquement à l’aide de [clés de partition](partition-data.md) à des fins d’évolutivité et de performance. Azure Cosmos DB fournit diverses API pour accéder à ces données, y compris la recherche par ID (Read/Get), les requêtes et les flux de lecture (analyses). Hello modification flux peut être obtenu en remplissant les deux toohello d’en-têtes demande nouvelle DocumentDB `ReadDocumentFeed` API et peuvent être traités en parallèle sur des plages de clés de partition.

### <a name="readdocumentfeed-api"></a>API ReadDocumentFeed
Examinons brièvement comment ReadDocumentFeed fonctionne. Base de données Azure Cosmos prend en charge la lecture d’un flux de documents dans une collection via hello `ReadDocumentFeed` API. Par exemple, hello de demande suivant retourne une page de documents à l’intérieur de hello `serverlogs` collection. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Résultats peuvent être limitées à l’aide de hello `x-ms-max-item-count` en-tête et les lectures peuvent être reprise par le renvoi de la demande de hello avec un `x-ms-continuation` en-tête est retourné dans la réponse précédente de hello. Lors de l’opération à partir d’un seul client, `ReadDocumentFeed` itère dans les résultats sur les différentes partitions en série. 

**Flux de lecture de documents en série**

Vous pouvez également récupérer des flux hello de documents à l’aide d’une des hello pris en charge [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md). Par exemple, les hello suivant extrait de code montre comment toouse hello [ReadDocumentFeedAsync méthode](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) dans .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Exécution distribuée de ReadDocumentFeed
Pour les collections qui contiennent des téraoctets de données ou plus, ou qui reçoivent un grand nombre de mises à jour, l’exécution en série de flux de lecture à partir d’un seul ordinateur client n’est pas forcément pratique. Dans l’ordre toosupport ces scénarios de données volumineuses, Azure Cosmos DB fournit les API toodistribute `ReadDocumentFeed` appels en toute transparence sur plusieurs lecteurs de client/consommateurs. 

**Flux de lecture de documents distribué**

tooprovide de traitement évolutif des modifications incrémentielles, Azure Cosmos DB prend en charge un modèle de montée en puissance parallèle pour les modifications de hello flux API basée sur des plages de clés de partition.

* Vous pouvez obtenir une liste des plages de clés de partition d’une collection effectuant un appel `ReadPartitionKeyRanges`. 
* Pour chaque plage de clés de partition, vous pouvez effectuer une `ReadDocumentFeed` tooread des documents avec les clés de partition dans la plage.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Récupération des plages de clés de partition d’une collection
Vous pouvez récupérer des plages de clés de partition hello en hello demande `pkranges` ressource au sein d’une collection. Par exemple hello de demande suivant récupère hello liste de plages de clés de partition pour hello `serverlogs` collection :

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Cette requête renvoie hello suivant de réponse contenant les métadonnées sur les plages de clés de partition hello :

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Propriétés de la plage de clé de partition**: chaque plage de clés de partition inclut des propriétés de métadonnées hello Bonjour tableau suivant :

<table>
    <tr>
        <th>Nom de l’en-tête</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>ID de Hello pour la plage de clés de partition hello. Il s’agit d’un ID stable et unique dans chaque collection.</p>
            <p>Doit être utilisé par la plage de clé de partition Bonjour appel tooread modifications suivantes.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Hello partition maximale clé valeur de hachage pour la plage de clés de partition hello. À usage interne.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>Hello minimum de partition clé valeur de hachage pour la plage de clés de partition hello. À usage interne.</td>
    </tr>       
</table>

Cela à l’aide de hello pris en charge [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md). Par exemple, hello extrait de code suivant montre comment la clé de partition tooretrieve plages dans .NET à l’aide de hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) (méthode).

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Base de données Azure Cosmos prend en charge la récupération de documents par plage de clés de partition par hello de paramètre facultatif `x-ms-documentdb-partitionkeyrangeid` en-tête. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Exécution d’un ReadDocumentFeed incrémentiel
ReadDocumentFeed prend en charge hello scénarios/tâches pour le traitement incrémentiel de modifications apportées aux collections de base de données Azure Cosmos suivantes :

* Lire tous les modifie toodocuments à partir du début de hello, autrement dit, à partir de la création de la collection.
* Lire tous les modifie toofuture mises à jour toodocuments de l’heure actuelle, ou les modifications apportées depuis une durée spécifiée par l’utilisateur.
* Lire toutes les modifications toodocuments à partir d’une version de logique de collection de hello (ETag). Vous pouvez le point de contrôle vos consommateurs selon hello retourné ETag à partir des demandes de flux de lecture incrémentielle.

les changements de Hello incluent toodocuments insertions et mises à jour. Supprime de toocapture, vous devez utiliser une propriété « suppression réversible » au sein de vos documents, ou utilisez hello [propriété TTL intégrée](time-to-live.md) toosignal une suppression en attente Bonjour modifier le flux.

Hello suivants table listes hello [demande](/rest/api/documentdb/common-documentdb-rest-request-headers.md) et [les en-têtes de réponse](/rest/api/documentdb/common-documentdb-rest-response-headers.md) pour les opérations de ReadDocumentFeed.

**En-têtes de demande pour les opérations ReadDocumentFeed incrémentielles** :

<table>
    <tr>
        <th>Nom de l’en-tête</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>Doit avoir la valeur trop « Incrémentiel flux », ou est omis dans le cas contraire</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Aucun en-tête : retourne toutes les modifications à partir de hello depuis (création de la collection)</p>
            <p>« * » : retourne toutes les nouvelles modifications toodata, au sein de la collection de hello</p>         
            <p>&lt;eTag&gt;: si jeu tooa collection ETag, retourne toutes les modifications apportées depuis cette date logique</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Format d’heure RFC 1123 ; ignoré si If-None-Match est spécifié.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>ID de plage de clés Hello partition pour la lecture des données.</td>
    </tr>
</table>

**En-têtes de réponse pour les opérations ReadDocumentFeed incrémentielles** :

<table> <tr>
        <th>Nom de l’en-tête</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>numéro de séquence logique Hello (LSN) du dernier document renvoyé dans la réponse de hello.</p>
            <p>L’opération ReadDocumentFeed incrémentielle peut être reprise en resoumettant cette valeur dans If-None-Match.</p>
        </td>
    </tr>
</table>

Voici un tooreturn de demande exemple toutes les modifications incrémentielles dans la collection à partir de la logique de hello version/ETag `28535` et de la plage de clés de partition = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Modifications sont classées par temps au sein de chaque valeur de clé de partition dans la plage de clés de partition hello. Il n’existe aucun ordre garanti entre les valeurs de clé de partition. S’il y a plus de résultats peut être contenue dans une seule page, vous pouvez lire la page de résultats suivante hello à soumettre à nouveau la demande hello avec hello `If-None-Match` en-tête avec la valeur des toohello égal `etag` à partir de la réponse précédente de hello. Si plusieurs documents ont été insérées ou mises à jour au niveau transactionnel au sein d’une procédure stockée ou un déclencheur, ils seront tous renvoyés dans hello même page de réponse.

> [!NOTE]
> Avec la modification de l’alimentation, vous pouvez obtenir plus d’éléments retournés dans une page à celle spécifiée dans `x-ms-max-item-count` dans les cas de hello de plusieurs documents insérées ou mises à jour à l’intérieur des procédures stockées ou des déclencheurs. 

Lorsque vous utilisez hello .NET SDK (1.17.0), définir le champ de hello `StartTime` dans `ChangeFeedOptions` documents toodirectly retour modifié depuis `StartTime` lors de l’appel `CreateDocumentChangeFeedQuery`. En spécifiant `If-Modified-Since` à l’aide des API REST de hello, votre requête retourne pas les documents hello, mais plutôt le jeton de continuation hello ou `etag` dans l’en-tête de réponse hello. documents de hello tooreturn hello modifié spécifié, jeton de continuation hello `etag` doit ensuite être utilisée dans la demande suivante de hello avec `If-None-Match` tooreturn hello documents réels. 

Hello .NET SDK fournit hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) et [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess les modifications apportées tooa collection de classes d’assistance. Hello extrait de code suivant montre les tooretrieve toutes les modifications à partir du début hello à l’aide de hello .NET SDK à partir d’un seul client.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
Et hello extrait de code suivant montre comment tooprocess change en temps réel avec la base de données Azure Cosmos à l’aide des modifications de hello flux prise en charge et hello précédant la fonction. Hello premier appel retourne tous les documents hello dans la collection de hello et hello ensuite uniquement retourne hello deux documents créés qui ont été créés depuis le dernier point de contrôle hello.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Vous pouvez également filtrer les flux de changement de hello à l’aide d’événements de processus de tooselectively logique côté client. Par exemple, Voici un extrait de code qui utilise tooprocess LINQ côté client uniquement les événements de modification de température de capteurs de l’appareil.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Bibliothèque du processeur de flux de modification
Une autre option consiste à toouse hello [bibliothèque d’Azure Cosmos DB modifier flux processeur](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), qui peut vous aider à distribuer facilement à partir d’une modification sur plusieurs consommateurs de flux de traitement des événements. bibliothèque de Hello est idéal pour la création de lecteurs de flux sur la plateforme .NET de hello de modification. Certains flux de travail est simplifiée à l’aide de la bibliothèque du processeur de modification de flux hello sur méthodes hello inclus dans hello autres kits de développement de base de données Cosmos sont les suivantes : 

* Extraction de mises à jour à partir du flux de modification quand les données sont stockées sur plusieurs partitions
* Déplacement ou la réplication de données à partir d’une collection tooanother
* Exécution parallèle des actions déclenchées par les mises à jour toodata et modification de flux 

À l’aide des API de hello Bonjour Cosmos kits de développement logiciel fournit un accès précis toochange flux mises à jour dans chaque partition, à l’aide de la bibliothèque de processeur de modification de flux hello simplifie les modifications de lecture entre plusieurs threads en parallèle et les partitions. Au lieu de lire manuellement des modifications à partir de chaque conteneur et l’enregistrement d’un jeton de liaison pour chaque partition, hello processeur de modification de flux gère automatiquement les modifications de la lecture sur plusieurs partitions à l’aide d’un mécanisme de bail.

bibliothèque de Hello est disponible sous forme de NuGet Package : [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) et à partir de code source en tant qu’un Github [exemple](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Présentation de la bibliothèque du processeur de flux de modification 

Il existe quatre composants principaux de l’implémentation hello processeur de flux de modification : hello analysés collection, collection de bail hello, hello processeur hôte et les consommateurs hello. 

**Collecte analysé :** collection de hello analysé est données hello à partir de quels hello flux de modification est généré. N’importe quelle collection toohello analysé insertions et les modifications sont répercutées dans le flux du changement hello de collection de hello. 

**Collection de bail :** hello coordonnées de collection de bail modification hello flux entre plusieurs threads de travail de traitement. Une collection distincte est baux de hello toostore utilisé avec un bail par partition. Il est avantageux toostore cette collection de bail sur un autre compte avec hello écrire hello toowhere plus proche de la région, processeur de flux de modification est en cours d’exécution. Un objet de bail contient hello suivant d’attributs : 
* Propriétaire : Spécifie l’hôte hello qui détient le bail de hello
* Continuation : Spécifie la position d’hello (jeton de continuation) modification hello pour une partition particulière de flux
* Date et heure : Dernière bail a été mis à jour ; Hello timestamp peut être utilisé toocheck si le bail de hello est considéré comme expiré 

**Processeur hôte :** chaque hôte détermine combien tooprocess de partitions basé sur le nombre d’autres instances d’hôtes ont des baux actifs. 
1.  Lorsqu’un ordinateur hôte démarre, il acquiert la charge de travail de baux toobalance hello sur tous les hôtes. Un hôte renouvelle périodiquement les baux afin que ceux-ci restent actifs. 
2.  Un hôte des points de contrôle hello dernière continuation jeton tooits bail pour chaque lecture. la sécurité d’accès concurrentiel tooensure, un hôte vérifie hello ETag pour chaque mise à jour de bail. D’autres stratégies de point de contrôle sont également prises en charge.  
3.  En cas d’arrêt, un hôte libère tous les baux mais conserve hello les informations de liaison, afin de pouvoir reprendre la lecture à partir du point de contrôle stockée hello plus tard. 

À ce stade, nombre hello d’hôtes ne peut pas être supérieur au nombre de hello de partitions (Location).

**Consommateurs :** des traitements, ou des consommateurs sont des threads qui effectuent des modifications hello processus initié par chaque hôte de flux. Chaque hôte de processeur peut avoir plusieurs consommateurs. Chaque consommateur lit les flux de modification hello de hello partition, elle est assignée tooand informe son hôte de modifications et expiration des baux.

toofurther comprendre comment ces quatre éléments de processeur de modification de flux fonctionnent ensemble, examinons un exemple Bonjour suivant schéma. Hello analysés collection stocke les documents et utilise hello « city » en tant que clé de partition hello. Nous constatons que les partitions hello bleu contient des documents avec le champ « Ville » de hello à partir de « A-E » et ainsi de suite. Il existe deux hôtes, chacun avec deux consommateurs lors de la lecture à partir de partitions hello quatre en parallèle. les flèches de Hello indiquent les consommateurs hello lors de la lecture à partir d’un point spécifique dans hello modifier le flux. Dans la première partition de hello, bleu foncé de hello représente les modifications non lues tandis que bleu clair de hello représente hello déjà lu les modifications dans le flux du changement hello. les hôtes de Hello utilisent hello bail collection toostore une piste de tookeep de valeur « continuation » de hello en cours de la lecture de position pour chaque consommateur. 

![À l’aide de la modification de base de données Azure Cosmos hello flux processeur hôte](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Utilisation de la bibliothèque du processeur de flux de modification 
Hello suivant la section explique comment toouse hello bibliothèque processeur de modification de flux dans le contexte de hello de réplication des modifications à partir d’une collection de destination tooa collection source. Ici, hello source collection est hello analysé dans le processeur de modification de flux. 

**Installer et inclure le package NuGet de processeur de flux de changement de hello** 

Avant d’installer le package NuGet du processeur de flux de modification, vous devez d’abord installer : 
* Microsoft.Azure.DocumentDB, version 1.13.1 ou ultérieure 
* Newtonsoft.Json, version 9.0.1 ou ultérieure. Installez `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` et incluez-le comme référence.

**Créer une collection analysée, une collection de baux et une collection de destination** 

Collection de bail hello hello toouse de commande processeur bibliothèque de flux de modification, doit toobe créé avant l’exécution des hôtes de processeur hello. Là encore, nous vous recommandons de stocker une collection de bail sur un autre compte avec un hello toowhere écriture le plus proche de la région que processeur de flux de modification est en cours d’exécution. Dans cet exemple de déplacement des données, nous devons la collection de destination hello toocreate avant d’exécuter l’hôte du processeur de modification de flux hello. Dans l’exemple de code hello, nous appelons un Bonjour toocreate de méthode d’assistance surveillé, loué et des regroupements de destination s’ils n’existent pas déjà. 

> [!WARNING]
> Création d’une collection a tarification implications, que vous réservez un débit de toocommunicate d’application hello avec la base de données Azure Cosmos. Pour plus d’informations, visitez hello [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Création d’un hôte de processeur*

Hello `ChangeFeedProcessorHost` classe fournit un environnement d’exécution de thread-safe, plusieurs processus sécurisé pour les implémentations de processeur d’événements qui permet également la gestion de bail de points de contrôle et de la partition. toouse hello `ChangeFeedProcessorHost` (classe), vous pouvez implémenter `IChangeFeedObserver`. Cette interface contient trois méthodes :

* `OpenAsync` : cette fonction est appelée quand l’observateur de flux de modification est ouvert. Il peut être modifié tooperform une action spécifique lorsque le consommateur/observateur est ouvert.  
* `CloseAsync` : cette fonction est appelée quand l’observateur de flux de modification est arrêté. Il peut être modifié tooperform une action spécifique lorsque le consommateur/observateur est fermé.  
* `ProcessChangesAsync` : cette fonction est appelée quand de nouvelles modifications de document sont disponibles sur le flux de modification. Il peut être modifié tooperform une action spécifique sur chaque mise à jour de la modification de flux.  

Dans notre exemple, nous implémentons interface de hello `IChangeFeedObserver` via hello `DocumentFeedObserver` classe. Ici, hello `ProcessChangesAsync` upserts (mises à jour), un document à partir de la modification de flux dans la collection de destination hello de fonction. Cet exemple est utile pour le déplacement des données à partir d’une collection des tooanother dans la clé de partition toochange hello ordre d’un jeu de données. 

*Hello processeur hôte en cours d’exécution*

Avant de commencer le traitement des événements, vous pouvez personnaliser les options de flux de modification et les options d’hôte de flux de modification. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
champs Hello spécifiques qui peuvent être personnalisés sont résumées dans hello les tableaux suivants. 

**Options de flux de modification** :
<table>
    <tr>
        <th>Nom de la propriété</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Obtient ou définit le nombre maximal de hello de toobe d’éléments retourné dans l’opération d’énumération hello Bonjour service de base de données de base de données Azure Cosmos.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Obtient ou définit l’id de plage de clés de partition hello pour la demande en cours de hello dans le service de base de données de base de données Azure Cosmos hello.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Obtient ou définit le jeton de continuation de requête hello dans le service de base de données de base de données Azure Cosmos hello.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Obtient ou définit le jeton de session hello pour une utilisation avec la cohérence de session dans hello service de base de données de base de données Azure Cosmos.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Obtient ou définit si la modification de flux dans le service de base de données de base de données Azure Cosmos hello doit démarrer à partir de hello depuis (true) ou en cours (false). Par défaut, il démarre de la position actuelle (false).</td>
    </tr>
</table>

**Options de l’hôte de flux de modification** :
<table>
    <tr>
        <th>Nom de la propriété</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>intervalle de salutation pour tous les baux pour les partitions actuellement détenu par l’instance de ChangeFeedEventHost hello.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Bonjour tookick intervalle désactiver une tâche de toocompute si les partitions sont réparties uniformément entre les instances d’hôte connus.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>Intervalle Hello pour le hello bail est effectuée sur un bail qui représente une partition. Si le bail de hello n’est pas renouvelé dans cet intervalle, elle a expiré et la propriété de partition de hello passe tooanother ChangeFeedEventHost instance.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>délai de Hello entre l’interrogation d’une partition de nouvelles modifications sur hello flux, une fois que toutes les modifications actuelles sont purgées.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>baux de fréquence toocheckpoint Hello.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>Int</td>
        <td>nombre minimal de partitions de Hello pour l’hôte de hello.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>Int</td>
        <td>nombre maximal de Hello d’hôte hello de partitions peut traiter.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Bool</td>
        <td>Si sur hello début de l’hôte de hello, tous les baux existants doit être supprimé et l’hôte de hello doit démarrer à partir de zéro.</td>
    </tr>
</table>


traitement des événements toostart instancier `ChangeFeedProcessorHost`, en fournissant les paramètres appropriés hello pour votre collection de base de données Azure Cosmos. Ensuite, appelez `RegisterObserverAsync` tooregister votre `IChangeFeedObserver` implémentation (DocumentFeedObserver dans cet exemple) avec le runtime de hello. À ce stade, les hôtes hello tentatives tooacquire un bail sur chaque plage de clés de partition dans la collection de base de données Azure Cosmos hello à l’aide d’un algorithme « greedy ». Ces baux sont valables pour une période donnée et doivent ensuite être renouvelés. Comme les nouveaux nœuds dans ce cas, les instances de travail en ligne, ils placent des réservations de baux et au fil du temps chargement de hello déplace entre les nœuds que chaque hôte tentatives tooacquire baux supplémentaires. 

Dans l’exemple de code hello, nous utilisons un toocreate (DocumentFeedObserverFactory.cs) de classe de fabrique un observateur et le hello `RegistObserverFactoryAsync` Observateur de hello tooregister. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Au fil du temps, un équilibre est établi. Cette capacité dynamique permet de processeur mise à l’échelle toobe appliqué tooconsumers pour la montée en puissance parallèle et l’échelle vers le bas. Si les modifications sont disponibles dans la base de données Azure Cosmos à un rythme plus rapide que les consommateurs peuvent en traiter, augmentation du processeur hello consommateurs peut être utilisé toocause une à l’échelle automatique sur le nombre d’instances de processus de travail.

## <a name="next-steps"></a>Étapes suivantes
* Essayez de hello [changement de base de données Azure Cosmos flux des exemples de code sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Commencer le codage par hello [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).
