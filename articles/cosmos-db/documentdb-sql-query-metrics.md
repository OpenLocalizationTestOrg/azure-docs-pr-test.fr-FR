---
title: "aaaSQL des métriques de requête pour l’API Azure Cosmos DB DocumentDB | Documents Microsoft"
description: "Découvrez comment tooinstrument et debug hello des performances des requêtes SQL de demandes de base de données Azure Cosmos."
keywords: "syntaxe sql, requête sql, requêtes sql, langage de requête json, concepts de bases de données, requêtes sql et fonctions agrégées"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Réglage des performances de requête avec Azure Cosmos DB
Azure Cosmos DB fournit une [API SQL pour interroger des données](documentdb-sql-query.md), sans nécessiter de schéma ou d’index secondaires. Cet article fournit hello suivant des informations destinées aux développeurs :

* Détails techniques sur le fonctionnement de l’exécution de requêtes SQL dans Azure Cosmos DB
* Développements sur les en-têtes de demande et réponse des requêtes, et sur les options du kit SDK client
* Conseils et meilleures pratiques pour les performances de requêtes
* Exemples de mode de performances des requêtes toodebug de statistiques d’exécution tooutilize SQL

## <a name="about-sql-query-execution"></a>À propos de l’exécution de requêtes SQL

Dans la base de données Azure Cosmos, vous stockez des données dans les conteneurs, qui peuvent se remplir tooany [débit de demande ou de la taille de stockage](partition-data.md). Base de données Azure Cosmos redimensionne en toute transparence des données entre les partitions physiques sous hello couvre la croissance des données toohandle ou augmenter le débit approvisionné. Vous pouvez émettre le conteneur de tooany de requêtes SQL à l’aide de hello API REST ou l’un des hello pris en charge [kits de développement logiciel DocumentDB](documentdb-sdk-dotnet.md).

Pour résumer brièvement le partitionnement : vous définissez une clé de partition, par exemple "city", qui détermine la façon dont les données sont fractionnées entre plusieurs partitions physiques. Clé de partition unique de données appartenant tooa (par exemple, « city » == « Seattle ») est stocké dans une partition physique, mais en général, une seule partition physique a plusieurs clés de partition. Lorsqu’une partition a atteint sa taille de stockage, hello service en toute transparence fractionne de partition de hello en deux nouvelles partitions et divise clé de partition hello uniformément entre ces partitions. Étant donné que les partitions sont transitoires, hello API utilisent une abstraction d’une « clé plage de partition », qui indique les plages hello des hachages de clé de partition. 

Lorsque vous émettez une requête de tooAzure Cosmos DB, hello SDK exécute les étapes logiques :

* Analyser le plan d’exécution de requête hello SQL requête toodetermine hello. 
* Si la requête de hello comprend un filtre par rapport à la clé de partition hello, tel que `SELECT * FROM c WHERE c.city = "Seattle"`, il est routé tooa une seule partition. Si la requête de hello n’a pas un filtre sur la clé de partition, puis elle est exécutée dans toutes les partitions et résultats sont fusionnés côté client.
* requête de Hello est exécuté au sein de chaque partition de série ou parallèle, en fonction de la configuration du client. Dans chaque partition, les requêtes hello risque de rendre un ou plusieurs allers-retours en fonction de la complexité de la requête hello, configuré la taille de la page et configuré le débit de la collection de hello. Chaque exécution retourne le nombre hello de [unités de requête](request-units.md) consommée par l’exécution des requêtes et éventuellement, des statistiques d’exécution de requête. 
* Hello SDK effectue une synthèse des résultats de la requête hello sur plusieurs partitions. Par exemple, si la requête de hello implique une clause ORDER BY sur plusieurs partitions, les résultats à partir des partitions individuelles sont les résultats triés de fusion de tooreturn globalement trié par ordre. Si la requête de hello est une agrégation telle que `COUNT`, hello des nombres à partir des partitions individuelles sont additionnée tooproduce hello nombre total.

Kits de développement logiciel Hello fournissent diverses options pour l’exécution des requêtes. Par exemple, dans .NET ces options sont disponibles dans hello `FeedOptions` classe. Hello tableau suivant décrit ces options et leur impact sur la durée d’exécution de requête. 

| Option | Description |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Doit être défini tootrue pour toute requête qui nécessite toobe exécutée sur plusieurs partitions. Il s’agit d’un indicateur explicite de tooenable vous compromis de performances consciente toomake au moment du développement. |
| `EnableScanInQuery` | Doit être définie tootrue si vous avez refusé d’indexation, mais requête de hello toorun via une analyse malgré tout. Uniquement applicable si l’indexation pour hello demandé chemin de filtrage est désactivé. | 
| `MaxItemCount` | nombre maximal de Hello de tooreturn d’éléments par aller-retour toohello serveur. En définissant trop-1, vous pouvez laisser les serveur hello gérer nombre hello d’éléments. Ou bien, vous pouvez réduire cette valeur de tooretrieve uniquement un petit nombre d’éléments par aller-retour. 
| `MaxBufferedItemCount` | Ceci est une option côté client et utiliser la consommation de mémoire toolimit hello lors de l’ordre de partitions croisées par. Une valeur plus élevée permet de réduire la latence hello de tri de partitions croisées. |
| `MaxDegreeOfParallelism` | Obtient ou définit le nombre de hello d’opérations simultanées exécuté côté client lors de l’exécution de requête parallèle Bonjour service de base de données Azure DocumentDB. Une valeur de propriété positif limite hello valeur du nombre d’opérations simultanées toohello ensemble. Si sa valeur est accessible sans à 0, système de hello décide automatiquement de nombre hello de toorun des opérations simultanées. |
| `PopulateQueryMetrics` | Permet une journalisation détaillée des statistiques du temps passé dans les différentes phases d’exécution de la requête, telles que le moment de la compilation, la durée de la boucle d’indexation et la durée de chargement des documents. Vous pouvez partager la sortie à partir des statistiques de requête avec les problèmes de performances de requête toodiagnose prise en charge Azure. |
| `RequestContinuation` | Vous pouvez reprendre l’exécution des requêtes en passant d’un jeton de continuation opaque hello retourné par une requête. jeton de continuation Hello encapsule tous les états requis pour l’exécution de requête. |
| `ResponseContinuationTokenLimitInKb` | Vous pouvez limiter la taille maximale de hello hello du jeton de continuation retourné par le serveur de hello. Vous devrez peut-être tooset cela si votre hôte d’application a des limites de taille d’en-tête de réponse. Définition de cette propriété peut augmenter hello RUs consommées pour les requêtes de hello et la durée globales.  |

Par exemple, prenons un exemple de requête sur la clé de partition demandé sur une collection de `/city` en tant que partition hello configurée avec 100 000 ur/s de débit et de clé. Vous demandez cette requête à l’aide `CreateDocumentQuery<T>` dans .NET hello suivante :

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Hello extrait du Kit de développement logiciel illustrée ci-dessus, correspond toohello suivant demande l’API REST :

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Chaque page de l’exécution de requête correspond tooa API REST `POST` avec hello `Accept: application/query+json` en-tête et la requête SQL dans le corps de hello hello. Chaque requête effectue un ou plusieurs arrondies serveur toohello allers-retours hello `x-ms-continuation` jeton répercutée entre hello client et serveur tooresume de l’exécution. options de configuration Hello dans FeedOptions sont passées server toohello sous forme de hello d’en-têtes de demande. Par exemple, `MaxItemCount` correspond trop`x-ms-max-item-count`. 

Hello demande retourne suivant hello (tronquées pour une meilleure lisibilité) réponse :

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

les en-têtes de réponse de la clé Hello renvoyés par la requête de hello hello suivants :

| Option | Description |
| ------ | ----------- |
| `x-ms-item-count` | nombre de Hello d’éléments retournés dans la réponse de hello. Cela dépend de hello fourni `x-ms-max-item-count`, hello le nombre d’éléments qui peuvent être contenues au sein de la taille de charge utile de réponse maximal hello, débit approvisionné de hello et exécution des requêtes. |  
| `x-ms-continuation:` | Hello continuation jeton tooresume l’exécution de requête hello, si des résultats supplémentaires sont disponibles. | 
| `x-ms-documentdb-query-metrics` | statistiques de requête Hello pour l’exécution de hello. Il s’agit d’une chaîne délimitée qui contient des statistiques de temps passé dans hello différentes phases d’exécution de la requête. Retourné si `x-ms-documentdb-populatequerymetrics` est défini trop`True`. | 
| `x-ms-request-charge` | Hello nombre de [unités de requête](request-units.md) consommés par requête de hello. | 

Pour plus d’informations sur les en-têtes de demande d’API REST hello et les options, consultez [interrogation des ressources à l’aide de hello API REST de DocumentDB](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Meilleures pratiques pour les performances de requêtes
Hello Voici les facteurs courants hello ayant un impact sur les performances des requêtes de base de données Azure Cosmos. Nous approfondissons chacune de ces rubriques dans cet article.

| Facteur | Conseil | 
| ------ | -----| 
| Débit approvisionné | RU de mesures par requête et assurez-vous d’avoir un débit approvisionné hello requis pour vos requêtes. | 
| Partitionnement et clés de partition | Favoriser les requêtes avec la valeur de clé de partition hello dans la clause de filtre de hello pour une latence faible. |
| Options de requête et de kit SDK | Suivez les meilleures pratiques du kit SDK, comme la connectivité directe, et paramétrez les options d’exécution de requêtes du côté client. |
| Latence du réseau | Prendre en compte réseau temps de mesure et utiliser multihébergement tooread API à partir de hello plus proche de la région. |
| Stratégie d'indexation | Assurez-vous que vous avez hello requis chemins d’accès/stratégie d’indexation pour la requête de hello. |
| Mesures d’exécution des requêtes | Analyser hello requête d’exécution métriques tooidentify potentielle réécritures des formes de requêtes et de données.  |

### <a name="provisioned-throughput"></a>Débit approvisionné
Cosmos DB vous permet de créer des conteneurs de données, chacun avec un débit réservé qui est exprimé en RU (unité de requête) par seconde. Une lecture d’un document de 1 Ko est 1 ur et chaque opération (y compris les requêtes) est normalisé tooa nombre fixe d’unités réservées en fonction de sa complexité. Par exemple, si vous avez 1000 RU/s configurées pour votre conteneur, et que vous avez une requête, telle que `SELECT * FROM c WHERE c.city = 'Seattle'` qui consomme 5 RU, vous pouvez alors effectuer (1000 RU/s) / (5 RU/requête) = 200 requêtes/s de ce genre de requête par seconde. 

Si vous envoyez de plus de 200 requêtes/s, service de hello démarre débit maximal de demandes entrantes ci-dessus 200/s. Hello kits de développement logiciel gèrent automatiquement cet incident en effectuant une interruption/nouvelle tentative, par conséquent, vous pouvez remarquer une latence plus élevée pour ces requêtes. Augmentation hello configuré débit toohello requis valeur améliore le débit et la latence de la requête. 

toolearn en savoir plus sur les unités de demande, consultez [unités de requête](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Partitionnement et clés de partition
Avec la base de données Azure Cosmos, en général, les requêtes effectuent dans hello suivant l’ordre, de la plus rapide/plus efficace tooslower/moins efficace. 

* GET sur une clé de partition unique et une clé d’élément
* Requête avec une clause de filtre sur une clé de partition unique
* Requête sans clause de filtre d’égalité ou de plage sur une propriété
* Requête sans filtre

Interroge ce tooconsult besoin une latence plus élevée toutes les partitions nécessaire et peut consommer RUs plus élevées. Étant donné que chaque partition a l’indexation automatique contre toutes les propriétés, les requêtes hello peuvent être utilisée efficacement à partir de l’index de hello dans ce cas. Vous pouvez effectuer des requêtes qui s’étendent sur des partitions plus rapides à l’aide des options de parallélisme hello.

toolearn en savoir plus sur le partitionnement et les clés de partition, consultez [partitionnement dans la base de données Azure Cosmos](partition-data.md).

### <a name="sdk-and-query-options"></a>Options de requête et de kit SDK
Consultez [conseils relatifs aux performances](performance-tips.md) et [les tests de performances](performance-testing.md) pour comment tooget hello mieux les performances côté client à partir de la base de données Azure Cosmos. Cela inclut l’utilisation hello dernière kits de développement logiciel, configuration des configurations spécifiques à une plateforme comme nombre de connexions, la fréquence de garbage collection, par défaut et à l’aide des options de connectivité léger comme Direct/TCP. 


#### <a name="max-item-count"></a>Nombre maximum d’éléments
Pour les requêtes, hello valeur `MaxItemCount` peut avoir un impact significatif sur le moment de la requête de bout en bout. Chaque aller-retour toohello server renvoie pas plus de nombre hello d’éléments de `MaxItemCount` (valeur par défaut de 100 éléments). Une valeur plus élevée tooa (-1 est maximale et recommandée) améliore votre durée de requête globale en limitant hello nombre d’allers-retours entre le serveur et le client, en particulier pour les requêtes avec des jeux de résultats volumineux.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Degré maximal de parallélisme
Pour les requêtes, paramétrer hello `MaxDegreeOfParallelism` tooidentify hello les configurations pour votre application, en particulier si vous effectuez des requêtes entre partitions (sans un filtre sur la valeur de clé de partition hello). `MaxDegreeOfParallelism`contrôle le nombre maximal hello de tâches en parallèle, c'est-à-dire hello maximum toobe partitions visité en parallèle. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Supposons que
* D = nombre par défaut maximal de tâches parallèles (= nombre total de processeur d’ordinateur du client hello)
* P = nombre maximal de tâches parallèles spécifié par l’utilisateur
* N = nombre de partitions doit toobe visité pour répondre à une requête

Voici les implications en matière de comportement des requêtes parallèles hello pour différentes valeurs de P.
* (P == 0) = > Mode série
* (P == 1) => Une tâche maximum
* (P > 1) => Nombre minimum de tâches parallèles (P, N) 
* (P < 1) => Nombre minimum de tâches parallèles (N, D)

Pour obtenir les notes de publication des kits SDK et des renseignements complémentaires sur les classes et les méthodes implémentées, consultez [Kits SDK DocumentDB](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Latence du réseau
Consultez [distribution globale de base de données Azure Cosmos](tutorial-global-distribution-documentdb.md) de tooset jusqu'à la distribution globale, puis se connecter à la région toohello le plus proche. Latence du réseau a un impact significatif sur les performances des requêtes lorsque vous devez toomake plusieurs allers-retours ou récupérer un grand jeu de résultats de requête de hello. 

Hello section sur les métriques d’exécution de requête explique comment tooretrieve hello heure d’exécution du serveur de requêtes ( `totalExecutionTimeInMs`), vous pouvez faire la différence entre le temps passé dans l’exécution des requêtes et des temps de transit du réseau.

### <a name="indexing-policy"></a>Stratégie d’indexation
Consultez [Configuration de la stratégie d’indexation](indexing-policies.md) pour l’indexation de chemins, de types et de modes, ainsi que leur impact sur l’exécution des requêtes. Par défaut, hello stratégie d’indexation utilise une indexation de hachage pour les chaînes, ce qui est efficace pour les requêtes d’égalité, mais pas pour les requêtes de plage/order par les requêtes. Si vous avez besoin des requêtes de plage pour les chaînes, nous recommandons de spécifier hello type d’index de plage pour toutes les chaînes. 

## <a name="query-execution-metrics"></a>Mesures d’exécution des requêtes
Vous pouvez obtenir les métriques détaillées sur l’exécution des requêtes en passant hello facultatif `x-ms-documentdb-populatequerymetrics` en-tête (`FeedOptions.PopulateQueryMetrics` Bonjour .NET SDK). Hello la valeur retournée dans `x-ms-documentdb-query-metrics` a hello suivant des paires clé-valeur destinés à un dépannage de l’exécution de requêtes avancé. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Mesure | Unité | Description | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | millisecondes | Durée d’exécution de la requête | 
| `queryCompileTimeInMs` | millisecondes | Durée de compilation de la requête  | 
| `queryLogicalPlanBuildTimeInMs` | millisecondes | Plan de requête logique toobuild de temps | 
| `queryPhysicalPlanBuildTimeInMs` | millisecondes | Plan de requête physique toobuild de temps | 
| `queryOptimizationTimeInMs` | millisecondes | Temps consacré à l’optimisation de la requête | 
| `VMExecutionTimeInMs` | millisecondes | Temps passé dans l’exécution de la requête | 
| `indexLookupTimeInMs` | millisecondes | Temps passé dans la couche de l’index physique | 
| `documentLoadTimeInMs` | millisecondes | Temps de chargement de documents  | 
| `systemFunctionExecuteTimeInMs` | millisecondes | Temps total consacré à l’exécution de fonctions (intégrées) système, en millisecondes  | 
| `userFunctionExecuteTimeInMs` | millisecondes | Temps total consacré à l’exécution de fonctions définies par l’utilisateur, en millisecondes | 
| `retrievedDocumentCount` | millisecondes | Nombre total de documents récupérés  | 
| `retrievedDocumentSize` | octets | Taille totale des documents récupérés, en octets  | 
| `outputDocumentCount` | count | Nombre de documents sortants | 
| `writeOutputTimeInMs` | millisecondes | Durée moyenne d’exécution de la requête, en millisecondes | 
| `indexUtilizationRatio` | ratio (< = 1) | Ratio du nombre de documents mis en correspondance par le nombre de toohello hello filtre des documents chargés  | 

Hello client SDK peut en interne rendre plusieurs requêtes opérations tooserve hello requête dans chaque partition. client de Hello effectue plusieurs appels par partition si les résultats total hello dépassent `x-ms-max-item-count`, si la requête de hello dépasse le débit approvisionné de hello pour les partitions hello, ou si hello charge utile de requête atteint la taille maximale de hello par page si hello requête atteint hello système allouée limite de délai d’attente. Chaque exécution de requête partielle retourne un `x-ms-documentdb-query-metrics` pour cette page. 

Voici quelques exemples de requêtes et comment toointerpret des métriques de hello retournés à partir de l’exécution de la requête : 

| Interroger | Exemples de mesures | Description | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Hello nombre de documents récupérés est 100 + 1 toomatch hello mot clé TOP. Le temps de la requête est essentiellement consacré à `WriteOutputTime` et `DocumentLoadTime` puisqu’il s’agit d’une analyse. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount est désormais plus élevé (500 + 1 toomatch hello clause TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Environ 0,9 ms est passé dans IndexLookupTime pour une recherche de clé, car c’est une recherche d’index sur `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Légèrement plus de temps (1,7 ms) est passé dans IndexLookupTime sur une analyse de plage, car c’est une recherche d’index sur `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | Même temps passé sur `DocumentLoadTime` que sur les requêtes précédentes, mais `WriteOutputTime` est inférieur, car nous ne projetons qu’une seule propriété. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Environ 213 ms est consacré à `UserDefinedFunctionExecutionTime` l’exécution de hello UDF sur chaque valeur de `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Environ 0,6 ms est consacré à `IndexLookupTime` sur `/Name/?`. La plupart des hello interroger le temps d’exécution (ms ~ 7) dans `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | La requête est exécutée en tant qu’analyse, car elle utilise `LOWER`, et 500 documents sur les 2491 récupérés sont retournés. |


## <a name="next-steps"></a>Étapes suivantes
* toolearn sur hello pris en charge les opérateurs de requête SQL et les mots clés, consultez [requête SQL](documentdb-sql-query.md). 
* toolearn sur les unités de demande, consultez [unités de requête](request-units.md).
* toolearn sur la stratégie d’indexation, consultez [stratégie d’indexation](indexing-policies.md) 


