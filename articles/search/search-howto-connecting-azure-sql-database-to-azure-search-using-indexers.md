---
title: "tooAzure de base de données SQL Azure aaaConnecting les indexeurs à l’aide de la recherche | Documents Microsoft"
description: "Découvrez comment toopull des données à partir de la base de données SQL Azure tooan Azure Search index à l’aide des indexeurs."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>La connexion de base de données SQL Azure tooAzure recherche à l’aide d’indexeurs

Avant d’interroger un [index Recherche Azure](search-what-is-an-index.md), vous devez le remplir avec vos données. Si les données de salutation résident dans une base de données SQL Azure, un **indexeur Azure Search pour la base de données SQL Azure** (ou **indexeur de SQL Azure** en abrégé) pouvez automatiser des processus d’indexation hello, ce qui signifie moins de code toowrite et moins toocare infrastructure sur.

Cet article traite des mécanismes hello de l’utilisation de [indexeurs](search-indexer-overview.md), mais décrit également les fonctionnalités disponibles uniquement avec les bases de données SQL Azure (par exemple, intégrée suivi des modifications). 

En outre tooAzure bases de données SQL Azure Search fournit des indexeurs pour [base de données Azure Cosmos](search-howto-index-documentdb.md), [le stockage Blob Azure](search-howto-indexing-azure-blob-storage.md), et [le stockage de table Azure](search-howto-indexing-azure-tables.md). prise en charge de toorequest pour d’autres sources de données, entrez vos commentaires sur hello [forum de commentaires d’Azure Search](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Indexeurs et sources de données

A **source de données** spécifie quel tooindex de données, les informations d’identification pour l’accès aux données et des stratégies qui identifient efficacement les modifications apportées aux données de hello (lignes nouvelles, modifiées ou supprimées). Elle est définie comme une ressource indépendante utilisable par plusieurs indexeurs.

Un **indexeur** est une ressource qui connecte une source de données unique à un index de recherche cible. Un indexeur est utilisé dans hello suivant façons :

* Effectuer une copie ponctuelle des données de hello toopopulate un index.
* Mettre à jour un index avec des modifications dans la source de données hello selon une planification.
* Exécuter à la demande tooupdate un index en fonction des besoins.

Un indexeur peut uniquement utiliser une table ou une vue, mais vous pouvez créer plusieurs indexeurs si vous souhaitez toopopulate plusieurs index de recherche. Pour plus d’informations sur ces concepts, consultez [Opérations d’indexeur : Flux de travail classique](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).

Vous pouvez installer et configurer un indexeur SQL Azure avec les outils suivants :

* Assistant Importation de données Bonjour [portail Azure](https://portal.azure.com)
* [Kit de développement logiciel .NET (SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet) de la Recherche Azure
* [API REST](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations) de la Recherche Azure

Dans cet article, nous allons utiliser hello API REST toocreate **indexeurs** et **des sources de données**.

## <a name="when-toouse-azure-sql-indexer"></a>Lorsque toouse indexeur de SQL Azure
En fonction de plusieurs facteurs concernant les données tooyour, utilisez hello d’indexeur de SQL Azure peut ou peut ne pas convenir. Si vos données rentrent hello suivant les exigences, vous pouvez utiliser l’indexeur de SQL Azure.

| Critères | Détails |
|----------|---------|
| Les données proviennent d’une seule table ou d’une seule vue | Si les données de salutation sont dispersées dans plusieurs tables, vous pouvez créer une vue unique des données de hello. Toutefois, si vous utilisez une vue, vous ne serez en mesure de toouse intégrée de SQL Server Modification détection toorefresh un index avec des modifications incrémentielles. Pour plus d’informations, consultez la section [Capture des lignes modifiées et supprimées](#CaptureChangedRows) ci-dessous. |
| Les types de données sont compatibles | La plupart des mais pas tous les types SQL de hello sont pris en charge dans un index Azure Search. Pour obtenir une liste, consultez [Mappage des types de données](#TypeMapping). |
| La synchronisation de données en temps réel n’est pas requise | Un indexeur peut réindexer votre table toutes les cinq minutes au plus. Si vos données changent fréquemment et hello change toobe besoin reflétée dans les index hello quelques secondes ou minutes uniques, nous vous recommandons d’utiliser hello [API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) ou [.NET SDK](search-import-data-dotnet.md) toopush lignes mises à jour directement. |
| Une indexation incrémentielle est possible | Si vous avez un grand ensemble de données et l’indexeur de hello toorun plan selon une planification, Azure Search doit être en mesure de tooefficiently identifier les lignes nouvelles, modifiées ou supprimées. L’indexation non incrémentielle n’est autorisée que si vous effectuez une indexation à la demande (non planifiée) ou une indexation de moins de 100 000 lignes. Pour plus d’informations, consultez la section [Capture des lignes modifiées et supprimées](#CaptureChangedRows) ci-dessous. |

## <a name="create-an-azure-sql-indexer"></a>Créer un indexeur Azure SQL

1. Créer la source de données hello :

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Vous pouvez obtenir la chaîne de connexion hello de hello [portail Azure](https://portal.azure.com); utilisez hello `ADO.NET connection string` option.

2. Créer des index de recherche de Azure hello cible si vous n’avez pas déjà. Vous pouvez créer un index à l’aide de hello [portal](https://portal.azure.com) ou hello [créer des API Index](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Vérifiez que hello schéma de l’index cible est compatible avec le schéma hello de table de source de hello - voir [mappage de types de données entre SQL et Azure search](#TypeMapping).

3. Création d’indexeur de hello en lui donnant un nom et faisant référence à hello données source et cible les index :

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Un indexeur créé de cette façon n’a pas de planification. Il s’exécute automatiquement une fois créé. Vous pouvez le réexécuter à tout moment à l'aide d’une requête **run indexer** :

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

Vous pouvez personnaliser différents aspects du comportement des indexeurs, notamment la taille du lot et le nombre de documents pouvant être ignorés avant que l’exécution d’un indexeur n’échoue. Pour plus d’informations, consultez [Créer une API d’indexeur](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

Vous devrez peut-être de base de données tooyour de tooconnect tooallow services Azure. Consultez [la connexion à partir de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) pour obtenir des instructions sur la façon de toodo qui.

toomonitor hello statut de l’indexation et l’historique d’exécution (nombre d’éléments indexés, échecs, etc.), utilisez un **état de l’indexeur** demande :

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

réponse de Hello doit se présenter comme toohello suivant :

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

L’historique d’exécution contient des too50 d’exécutions hello terminée le plus récemment, qui sont triés dans l’ordre chronologique inverse hello (de sorte que l’exécution de la plus récente de hello en premier dans la réponse de hello).
Vous trouverez des informations supplémentaires sur la réponse de hello dans [obtenir le statut indexeur](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Exécuter des indexeurs selon une planification
Vous pouvez également organiser les toorun d’indexeur hello périodiquement selon une planification. toodo, ajouter hello **planification** propriété pendant la création ou mise à jour d’indexeur de hello. exemple Hello ci-dessous montre un indexeur de hello tooupdate PUT demande :

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Hello **intervalle** paramètre est obligatoire. intervalle de salutation fait référence à temps toohello entre début hello de deux exécutions consécutives d’indexeur. Hello plus petite autorisée intervalle est de 5 minutes. Hello plus longue est un jour. Il doit être formaté en tant que valeur « dayTimeDuration » XSD (un sous-ensemble limité d'une valeur de [durée ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). modèle Hello pour cela est : `P(nD)(T(nH)(nM))`. Exemples : `PT15M` toutes les 15 minutes, `PT2H` toutes les deux heures.

Hello facultatif **startTime** indique lorsque hello exécutions planifiées doivent commencer. S’il est omis, l’heure UTC actuelle de hello est utilisé. Cette durée peut être Bonjour au-delà, auquel cas la première exécution de hello est planifiée comme si l’indexeur de hello est exécuté en continu depuis hello startTime.  

L’indexeur ne peut s’exécuter qu’une seule fois simultanément. Si un indexeur est en cours d’exécution lors de son exécution est planifiée, l’exécution de hello est reportée hello heure planifiée suivante.

Prenons l’exemple d’un exemple toomake cela plus concret. Supposons que nous hello suivant une planification horaire configurée :

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Voici ce qui se passe :

1. exécution de l’indexeur première Hello commence à ou aux environs du 1er mars 2015 12:00 a.m. UTC.
2. Supposons que cette exécution prend 20 minutes (ou en tout cas, moins de 1 heure).
3. deuxième exécution de Hello démarre au ou aux environs de 1er mars 2015 01:00.
4. Supposons maintenant que cette exécution dure plus d’une heure, par exemple, 70 minutes, et se termine à environ 2 h 10.
5. Il est maintenant 2 h 00, heure pour hello troisième exécution toostart. Toutefois, étant donné que hello deuxième exécution à partir de 1 heure du matin est en cours d’exécution, l’exécution de la troisième de hello est ignorée. l’exécution de la troisième de Hello commence à 3 h 00.

Vous pouvez ajouter, modifier ou supprimer une planification d’indexeur en utilisant une requête **PUT indexer** .

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Capturer des lignes nouvelles, modifiées et supprimées

Azure Search utilise **indexation incrémentielle** tooavoid avoir toore-index hello la totalité de la table ou la vue chaque fois un indexeur s’exécute. Azure Search fournit que deux modifier la détection des stratégies toosupport incrémentielle l’indexation. 

### <a name="sql-integrated-change-tracking-policy"></a>Stratégie de suivi intégré des modifications SQL
Si votre base de données SQL prend en charge le [suivi des modifications](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), nous recommandons d'utiliser la **stratégie de suivi intégré des modifications SQL**. Il s’agit de stratégie la plus efficace de hello. En outre, il permet de lignes de tooidentify supprimé d’Azure Search sans que vous ayez tooadd une table de tooyour colonne explicite « suppression réversible ».

#### <a name="requirements"></a>Configuration requise 

+ Configuration requise pour la version de base de données :
  * SQL Server 2012 SP3 et versions ultérieures, si vous utilisez SQL Server sur des machines virtuelles Azure.
  * Azure SQL Database V12, si vous utilisez Azure SQL Database.
+ Tables uniquement (aucune vue). 
+ Sur la base de données hello, [activer le suivi](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) pour la table de hello. 
+ Aucune clé primaire composite (une clé primaire qui contient plus d’une colonne) sur la table de hello.  

#### <a name="usage"></a>Usage

toouse cette stratégie, créer ou mettre à jour votre source de données comme suit :

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Si vous utilisez le suivi intégré des modifications SQL, ne spécifiez pas une stratégie de détection des lignes supprimées. Elle intègre la prise en charge de l'identification des lignes supprimées. Toutefois, pour hello suppressions toobe détecté » comme par magie », clé de document hello dans votre index de recherche doit être hello même en tant que clé primaire de hello Bonjour table SQL. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Stratégie de détection des modifications de limite supérieure

Cette stratégie de détection de modification s’appuie sur une colonne « limite supérieure » capture version de hello ou temps lorsqu’une ligne a été modifiée. Si vous utilisez une vue, vous devez vous servir d’une stratégie de limite supérieure. colonne de limite supérieure Hello doit respecter hello suivant les exigences.

#### <a name="requirements"></a>Configuration requise 

* Toutes les insertions spécifient une valeur pour la colonne de hello.
* Élément de tooan toutes les mises à jour également modifier valeur hello de colonne de hello.
* valeur Hello de cette colonne augmente après chaque insertion ou la mise à jour.
* Requêtes avec hello suivant WHERE et les clauses ORDER BY peuvent être exécutées efficacement :`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Nous vous recommandons fortement de l’utilisation de hello [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) type de données pour la colonne de limite supérieure hello. Si un autre type de données est utilisé, le suivi des modifications n’est pas garanti toocapture toutes les modifications en présence de hello de transactions qui s’exécutent en même temps qu’une requête de l’indexeur. Lorsque vous utilisez **rowversion** dans une configuration avec des réplicas en lecture seule, vous devez pointer l’indexeur de hello au réplica principal de hello. Seul un réplica principal peut être utilisé dans les scénarios de synchronisation de données.

#### <a name="usage"></a>Usage

toouse une stratégie de limite supérieure, créer ou mettre à jour votre source de données comme suit :

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Si la table de source de hello n’a pas d’un index sur la colonne de la borne hello, les requêtes utilisées par l’indexeur SQL hello peuvent expirer. En particulier, hello `ORDER BY [High Water Mark Column]` clause nécessite une toorun index efficacement lors de la table de hello contient de nombreuses lignes.
>
>

Si vous rencontrez des erreurs de délai d’attente, vous pouvez utiliser hello `queryTimeout` indexeur configuration paramètre tooset hello requête tooa valeur supérieure au délai de 5 minutes par défaut hello. Par exemple, le délai d’expiration too10 minutes tooset hello, créer ou mettre à jour les indexeur hello hello configuration suivante :

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

Vous pouvez également désactiver hello `ORDER BY [High Water Mark Column]` clause. Toutefois, cela est déconseillé, car si l’exécution d’indexeur hello est interrompue par une erreur, indexeur de hello a toore-process toutes les lignes si elle s’exécute plus tard, même si l’indexeur de hello a déjà traité presque toutes les lignes de hello par heure hello qu'il a été interrompu. toodisable hello `ORDER BY` clause, utilisez hello `disableOrderByHighWaterMarkColumn` définition dans la définition d’indexeur hello :  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Stratégie de détection des colonnes à suppression réversible
Lorsque des lignes sont supprimées à partir de la table de source de hello, vous souhaiterez probablement toodelete ces lignes à partir de l’index de recherche hello également. Si vous utilisez hello SQL intégré le suivi des modifications de stratégie, cela est pris en charge pour vous. Toutefois, hello borne le suivi stratégie ne vous aide avec les lignes supprimées. Le toodo ?

Si hello lignes sont physiquement supprimées à partir de la table de hello, Azure Search n’a aucune présence de hello tooinfer moyen d’enregistrements qui n’existent plus.  Toutefois, vous pouvez utiliser supprimer des lignes hello « soft-suppression » technique toologically sans les supprimer à partir de la table de hello. Ajouter une colonne tooyour table ou vue et marquer les lignes supprimées à l’aide de cette colonne.

Lorsque vous utilisez la technique de soft-suppression hello, vous pouvez spécifier stratégie de suppression réversible hello comme suit lors de la création ou mise à jour de la source de données hello :

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Hello **softDeleteMarkerValue** doit être une chaîne – utiliser la représentation sous forme de chaîne hello votre valeur réelle. Par exemple, si vous avez une colonne d’entiers dans lequel les lignes supprimées sont marquées avec la valeur de hello 1, utilisez `"1"`. Si vous avez une colonne de bits dans laquelle les lignes supprimées sont marquées avec hello valeur booléenne true, utilisez `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Mappage entre les types de données SQL et Recherche Azure
| Type de données SQL | Types de champs d'index cible autorisés | Remarques |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.String | |
| real, float |Edm.Double, Edm.String | |
| smallmoney, money decimal numeric |Edm.String |Azure Search ne prend pas en charge la conversion de types décimaux en Edm.Double, car elle entraîne une perte de précision |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |Une chaîne SQL peut être utilisé toopopulate un champ collection (EDM.String) si la chaîne de hello représente un tableau JSON de chaînes :`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| Geography |Edm.GeographyPoint |Seules les instances de geography de type POINT avec SRID 4326 (valeur par défaut hello) sont pris en charge. |
| rowversion |N/A |Colonnes de la version de ligne ne peut pas être stockés dans l’index de recherche hello, mais elles peuvent être utilisées pour le suivi des modifications |
| time, timespan, binary, varbinary, image, xml, geometry, types CLR |N/A |Non pris en charge |

## <a name="configuration-settings"></a>Paramètres de configuration
L’indexeur SQL expose plusieurs paramètres de configuration :

| Paramètre | Type de données | Objectif | Valeur par défaut |
| --- | --- | --- | --- |
| queryTimeout |string |Jeux de hello délai d’attente pour l’exécution des requêtes SQL |5 minutes ("00:05:00") |
| disableOrderByHighWaterMarkColumn |bool |Provoque la requête SQL hello utilisée par hello borne stratégie tooomit hello clause ORDER BY. Consultez [Stratégie de limite supérieure](#HighWaterMarkPolicy) |false |

Ces paramètres sont utilisés dans hello `parameters.configuration` objet dans la définition d’indexeur hello. Par exemple, délai d’expiration too10 minutes tooset hello requête, créer ou mettre à jour les indexeur hello hello configuration suivante :

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>Forum Aux Questions

**Q. : Puis-je utiliser l’indexeur SQL Azure avec des bases de données SQL exécutées sur des machines virtuelles IaaS dans Azure ?**

Oui. Toutefois, vous devez tooallow votre base de données de recherche service tooconnect tooyour. Pour plus d’informations, consultez [configurer une connexion à partir d’un tooSQL d’indexeur Azure Search Server sur une machine virtuelle Azure](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**Q. : Puis-je utiliser l’indexeur Azure SQL avec des bases de données SQL exécutées localement ?**

Pas directement. Nous ne recommandons ni ne prend en charge une connexion directe, car cela nécessiterait vous tooopen votre trafic tooInternet de bases de données. Les clients ont réussi à l’aide de technologies de pont telles qu’Azure Data Factory. Pour plus d’informations, consultez [index Azure Search Push données tooan sont à l’aide d’Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**Q. : Puis-je utiliser l’indexeur Azure SQL avec des bases de données autres que SQL Server exécutées en IaaS sur Azure ?**

Non. Nous ne prennent pas en charge ce scénario, étant donné que nous n’avons pas testées indexeur hello avec les bases de données autre que SQL Server.  

**Q. : Puis-je créer plusieurs indexeurs qui s’exécutent selon une planification ?**

Oui. Cependant, seul un indexeur peut s'exécuter sur un nœud à la fois. Si vous avez besoin de plusieurs indexeurs qui s’exécutent simultanément, envisagez l’évolution verticale votre toomore du service de recherche à une unité de recherche.

**Q. : L’exécution d’un indexeur affecte-t-elle la charge de travail de mes requêtes ?**

Oui. Indexeur s’exécute sur l’un des nœuds hello dans votre service de recherche, et les ressources de ce nœud sont partagées entre l’indexation et desservant le trafic des requêtes et autres demandes de l’API. Si vous exécutez des charges de travail intensives d’indexation et de requête et si vous rencontrez un taux élevé d’erreurs 503 ou une augmentation des délais de réponse, [redimensionnez votre service de recherche](search-capacity-planning.md).

**Q : Puis-je utiliser un réplica secondaire dans un [cluster de basculement](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) comme source de données ?**

Cela dépend. Pour l’indexation intégrale d’une table ou d’une vue, vous pouvez utiliser un réplica secondaire. 

Pour une indexation incrémentielle, Recherche Azure prend en charge deux stratégies de détection des modifications : le suivi de modifications intégré SQL et la définition d’une limite supérieure.

Sur les réplicas en lecture seule, la base de données SQL ne prend pas en charge le suivi des modifications intégré. Par conséquent, vous devez utiliser la stratégie de limite supérieure. 

Notre recommandation standard est un type de données rowversion toouse hello pour la colonne de la borne hello. Toutefois, l’utilisation de rowversion repose sur la fonction `MIN_ACTIVE_ROWVERSION` SQL Database, qui n’est pas prise en charge sur les réplicas en lecture seule. Par conséquent, vous devez pointer le réplica principal de hello indexeur tooa si vous utilisez rowversion.

Si vous essayez de rowversion toouse sur un réplica en lecture seule, vous verrez hello l’erreur suivante : 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**Q : Puis-je utiliser une colonne autre que rowversion pour le suivi des modifications de la limite supérieure ?**

Cela n’est pas recommandé. Seule la colonne **rowversion** permet une synchronisation fiable des données. Toutefois, en fonction de votre logique d’application, cette opération peut être sécurisée si :

+ Vous pouvez vous assurer que lors de l’exécution de l’indexeur de hello, il n’existe aucune transaction en attente sur la table de hello est en cours d’indexation (par exemple, toutes les mises à jour de table se produisent en tant que lot selon un calendrier et planification de l’indexeur Azure Search hello a la valeur tooavoid qui se chevauchent avec la table de hello planification de la mise à jour).  

+ Vous effectuez régulièrement un toopick réindexation complète de toutes les lignes manquantes. 
