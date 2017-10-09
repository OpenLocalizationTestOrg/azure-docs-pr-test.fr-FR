---
title: "stratégies d’indexation de base de données Cosmos aaaAzure | Documents Microsoft"
description: "Comprendre le fonctionnement de l’indexation dans Azure Cosmos DB. Découvrez comment tooconfigure et modification hello stratégie d’indexation pour améliorer les performances et de l’indexation automatique."
keywords: "fonctionnement de l’indexation, indexation automatique, base de données d’indexation"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Comment Azure Cosmos DB indexe-t-il les données ?

Par défaut, toutes les données d’Azure Cosmos DB sont indexées. Alors que de nombreux clients sont heureux toolet base de données Azure Cosmos gèrent automatiquement tous les aspects de l’indexation, base de données Azure Cosmos prend également en charge en spécifiant une personnalisée **stratégie d’indexation** pour les collections lors de la création. Stratégies d’indexation dans la base de données Azure Cosmos sont plus flexibles et puissants que les index secondaires proposés dans d’autres plateformes de base de données, car elles vous permettent de concevoir et personnaliser la forme hello d’index de hello sans sacrifier la flexibilité de schéma. toolearn l’indexation de fonctionne dans la base de données Azure Cosmos, vous devez comprendre en gérant la stratégie d’indexation, vous pouvez apporter affiné compromis entre les coûts de stockage des index, écriture et le débit de la requête et la cohérence de requête.  

Dans cet article, nous examinons fermer Azure Cosmos DB stratégies d’indexation, comment vous pouvez personnaliser la stratégie d’indexation et hello associés compromis. 

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :

* Comment puis-je remplacer hello propriétés tooinclude ou exclure de l’indexation ?
* Comment puis-je configurer index hello pour les mises à jour éventuelles ?
* Comment puis-je configurer les requêtes Order By ou une plage d’indexation tooperform ?
* Comment créer une stratégie d’indexation de la collection de modifications tooa ?
* Comment puis-je comparer le stockage et les performances des différentes stratégies d'indexation ?

## <a id="CustomizingIndexingPolicy"></a>Personnalisation de stratégie d’indexation hello d’une collection
Les développeurs peuvent personnaliser hello compromis entre performances d’écriture/de la requête, de stockage et de cohérence de la requête, en remplaçant la stratégie d’indexation par défaut hello sur une collection de base de données Azure Cosmos et en configurant hello suivant aspects.

* **Inclusion/Exclusion des documents et chemins d’accès vers/à partir de l’index**. Les développeurs peuvent choisir certaine toobe documents exclus ou inclus dans les index hello au moment de hello d’insertion ou de les remplacer toohello collection. Les développeurs peuvent également choisir tooinclude ou exclure certaines propriétés JSON alias chemins d’accès (y compris les séquences de caractères génériques) toobe indexée dans tous les documents qui sont inclus dans un index.
* **Configuration de plusieurs types d’index**. Pour chacun des chemins d’accès hello inclus, les développeurs peuvent également spécifier hello type d’index, qu'ils ont besoin d’une collection en fonction de leurs données et la charge de travail de requête attendu et le hello numérique/chaîne « precision » pour chaque chemin d’accès.
* **Configuration des modes de mise à jour d’index**. Base de données Azure Cosmos prend en charge trois modes d’indexation qui peuvent être configurées via la stratégie sur une collection de base de données Azure Cosmos d’indexation de hello : cohérent, Lazy et aucun. 

Hello suivant extrait de code .NET montre comment tooset une stratégie d’indexation personnalisée lors de la création de hello d’une collection. Ici, nous avons défini stratégie hello avec index de plage pour les chaînes et les nombres à la précision maximale de hello. Cette stratégie nous permet d’exécuter des requêtes Trier par sur les chaînes.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> schéma JSON Hello pour la stratégie d’indexation a été modifié avec version hello de version de l’API REST 2015-06-03 des index de plage de toosupport sur les chaînes. .NET SDK 1.2.0 et Java, Python et Node.js kits de développement logiciel 1.1.0 prend en charge le nouveau schéma de stratégie hello. Anciens kits de développement logiciel utilisent hello version 2015-04-08 de l’API REST et prend en charge hello de schéma plus ancienne de la stratégie d’indexation.
> 
> Par défaut, Azure Cosmos DB indexe toutes les propriétés de chaîne au sein des documents, de manière cohérente, avec un index de hachage et des propriétés numériques avec un index de plage.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Personnalisation de la stratégie d’indexation de hello à l’aide du portail de hello

Vous pouvez modifier hello indexation de stratégie d’une collection à l’aide de hello portail Azure. Ouvrez votre compte de base de données Azure Cosmos Bonjour portail Azure, sélectionnez votre collection, dans le menu de navigation gauche hello, cliquez **paramètres**, puis cliquez sur **stratégie d’indexation**. Bonjour **stratégie d’indexation** panneau, modifiez votre stratégie d’indexation, puis cliquez sur **OK** toosave vos modifications. 

### <a id="indexing-modes"></a>Modes d’indexation de base de données
Base de données Azure Cosmos prend en charge trois modes d’indexation qui peuvent être configurées via hello indexation de stratégie sur une collection de base de données Azure Cosmos – cohérent, Lazy et aucun.

**Cohérence**: si la stratégie de la collection d’une base de données Azure Cosmos est désigné comme « cohérent », les requêtes sur une base de données Azure Cosmos donné, suivez collection hello hello même niveau de cohérence que celui spécifié pour hello point-lectures (c'est-à-dire fort, délimitée-péremption, session ou éventuelle). index de Hello est mise à jour de façon synchrone dans le cadre de la mise à jour du document hello (par exemple, insert, replace, mise à jour et suppression d’un document dans une collection de base de données Azure Cosmos).  Indexation cohérent prend en charge des requêtes cohérentes au coût hello de réduction possible le débit d’écriture. Cette réduction est une fonction de hello chemins d’accès uniques qui doivent toobe indexé et hello « niveau de cohérence ». Le mode d’indexation Cohérent est conçu pour les charges de travail « écrire rapidement, interroger immédiatement ».

**Lazy**: débit de réception tooallow maximal de documents, une collection de base de données Azure Cosmos peut être configurée avec une cohérence différée ; savoir les requêtes sont finalement cohérents. index de Hello est mis à jour en mode asynchrone lorsqu’une collection de base de données Azure Cosmos est inactive par exemple, lors de la capacité de débit de la collection hello n’est pas entièrement utilisé tooserve demandes de l’utilisateur. Pour les charges de travail « ingérer maintenant, interroger plus tard » nécessitant une ingestion libre des documents, le mode d'indexation « différé » peut être approprié.

**Aucun**: une collection en mode « Aucun » ne comporte aucun index associé. Ce mode est souvent employé si Azure Cosmos DB est utilisé en tant que stockage de clés-valeurs et si les documents ne sont accessibles que via leur propriété ID. 

> [!NOTE]
> Configuration hello stratégie avec « None » d’indexation a effet hello de suppression d’un index existant. Utilisez-la si vos modèles d'accès ne requièrent que l’attribut « id » et/ou « self-link » (lien réflexif).
> 
> 

Hello suivant afficher d’exemple comment créer une collection de base de données Azure Cosmos à l’aide de hello .NET SDK avec l’indexation automatique cohérente sur tous les insertions de document.

Hello tableau suivant montre la cohérence hello pour les requêtes basées sur hello mode d’indexation (cohérent et Lazy) configuré pour hello collection et hello cohérence au niveau spécifié pour la requête d’interrogation hello. Cela s’applique tooqueries apportées à l’aide des kits de développement logiciel interface - API REST, ou à partir de procédures stockées et déclencheurs. 

|Cohérence|Mode d’indexation : Cohérent|Mode d’indexation : Différé|
|---|---|---|
|Remarque|Remarque|Eventual (Éventuel)|
|Obsolescence limitée|Obsolescence limitée|Eventual (Éventuel)|
|Session|Session|Eventual (Éventuel)|
|Eventual (Éventuel)|Eventual (Éventuel)|Eventual (Éventuel)|

Azure Cosmos DB renvoie une erreur pour les requêtes effectuées sur les collections en mode d’indexation « Aucun ». Requêtes peuvent toujours être exécutées en tant qu’analyses via hello explicite `x-ms-documentdb-enable-scan` en-tête hello API REST ou hello `EnableScanInQuery` demande à l’aide de l’option hello du SDK .NET. Certaines fonctions de requêtes, telles que ORDER BY, ne sont pas prises en charge en tant qu’analyses avec `EnableScanInQuery`.

Hello tableau suivant présente la cohérence de hello pour les requêtes basées sur le mode d’indexation hello (cohérent, Lazy et aucun) lorsque EnableScanInQuery est spécifié.

|Cohérence|Mode d’indexation : Cohérent|Mode d’indexation : Différé|Mode d’indexation : Aucun|
|---|---|---|---|
|Remarque|Remarque|Eventual (Éventuel)|Remarque|
|Obsolescence limitée|Obsolescence limitée|Eventual (Éventuel)|Obsolescence limitée|
|Session|Session|Eventual (Éventuel)|Session|
|Eventual (Éventuel)|Eventual (Éventuel)|Eventual (Éventuel)|Eventual (Éventuel)|

Hello suivant afficher des exemples de code comment créer une collection de base de données Azure Cosmos à l’aide de hello .NET SDK à l’indexation de cohérence sur toutes les insertions de document.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Chemins d’accès de l’index
Base de données Azure Cosmos modélise les documents JSON et les index hello en tant qu’arborescences et vous permet de toopolicies tootune pour les chemins d’accès dans l’arborescence de hello. Dans les documents, vous pouvez choisir les chemins d'accès qui doivent être inclus ou exclus de l'indexation. Cela peut entraîner des performances d’écriture amélioré et le stockage d’index inférieure pour les scénarios de modèles de requête hello sont connues au préalable.

Chemins d’accès de l’index commencent par la racine de hello (/) et se terminent généralement par Bonjour ? opérateur de caractère générique, ce qui indique qu’il n’y a plusieurs valeurs possibles pour le préfixe de hello. Par exemple, tooserve SELECT * FROM familles F WHERE F.familyName = « Andersen », vous devez inclure un chemin d’accès de l’index pour /familyName/ ? dans la stratégie d’index de la collection hello.

Chemins d’accès de l’index permet également de hello * génériques comportement de hello toospecify l’opérateur de manière récursive les chemins d’accès sous le préfixe de hello. Par exemple, / charge utile / * peut être utilisé tooexclude tous les éléments sous la propriété de charge utile hello de l’indexation.

Voici des modèles courants hello pour la spécification des chemins d’accès de l’index :

| Chemin                | Description/cas d'utilisation                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Chemin par défaut de la collection. Récursif et s’applique toowhole arborescence du document.                                                                                                                                                                                                                                   |
| /prop/?             | Chemin d’accès de l’index requis requêtes tooserve hello suivante (Hash ou Range respectivement avec les types) :<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /prop/*             | Chemin d’accès de l’index pour tous les chemins d’accès sous hello spécifié étiquette. Fonctionne avec les requêtes suivantes de hello<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | Chemin d’accès de l’index requis tooserve itération et les requêtes de jointure sur les tableaux de valeurs scalaires comme [« a », « b », « c »] :<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[] /subprop/? | Chemin d’accès de l’index requis tooserve itération et les requêtes de jointure sur les tableaux d’objets comme [{subprop : « a »}, {subprop : « b »}] :<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | Chemin d’accès de l’index requis tooserve requêtes (Hash ou Range respectivement avec les types) :<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Lors de la définition des chemins d’accès de l’index personnalisé, vous êtes règle d’indexation par défaut hello toospecify requis pour arborescence du document entier hello désigné par le chemin d’accès spéciale de hello « / * ». 
> 
> 

Hello exemple suivant configure un chemin d’accès spécifique à l’indexation de plage et une valeur de précision personnalisé de 20 octets :

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Types de données d’index, types d’index et précisions d’index
Maintenant que nous avons observez comment toospecify chemins, nous allons examiner les options de hello, nous pouvons utiliser tooconfigure hello stratégie d’indexation pour un chemin d’accès. Vous pouvez spécifier une ou plusieurs définitions d’indexation pour chaque chemin d’accès :

* Type de données : **chaîne**, **nombre**, **point**, **polygone** ou **LineString** (ne pouvant contenir qu’une seule entrée par type de données par chemin d’accès)
* Genre d’index : **hachage** (requêtes d’égalité) ou **plage** (requêtes d’égalité, de plage ou requêtes Trier par) ou **spatial** (demandes spatiales) 
* Précision : Pour les index de hachage cela varie de 1 too8 pour les chaînes et nombres avec la valeur par défaut 3. Pour les index de plage, cette valeur peut être -1 (précision maximale) et varie entre 1 et 100 (précision maximale) pour les valeurs de chaîne ou numériques.

#### <a name="index-kind"></a>Type d’index
Azure Cosmos DB prend en charge les types d’index de hachage et de plage pour chaque chemin d’accès (qui peuvent être configurés pour les chaînes, les nombres ou les deux).

* **Hachage** prend en charge les requêtes d’égalité efficaces et JOIN. Pour la plupart des cas d’usage, les index de hachage est inutile une précision supérieure à celle de la valeur par défaut hello 3 octets. Le type de données peut être Chaîne ou Nombre.
* **Plage** prend en charge les requêtes d’égalité efficaces, les requêtes de plage (avec &gt;, &lt;, &gt;=, &lt;=, !=) et les requêtes Trier par. Par défaut, les requêtes Trier par nécessitent également une précision d’index maximale (-1). Le type de données peut être Chaîne ou Nombre.

Base de données Azure Cosmos prend également en charge le type d’index Spatial hello pour chaque chemin d’accès, qui peut être spécifié pour les types de données de Point, un polygone ou LineString hello. valeur Hello au chemin d’accès spécifié de hello doit être un fragment GeoJSON valid comme `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Spatial** prend en charge les requêtes spatiales efficaces (within et distance) Le type de données peut être Point, Polygone ou LineString.

> [!NOTE]
> Azure Cosmos DB prend en charge l’indexation automatique des points, polygones et lineStrings.
> 
> 

Voici les types d’index hello pris en charge et des exemples de requêtes qu’ils peuvent être utilisé tooserve :

| Type d’index | Description/cas d'utilisation                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hachage       | Le hachage disposant de l’élément /prop? (ou /) peut être utilisé tooserve hello requêtes suivantes efficacement :<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Le hachage disposant de l’élément /props/[]/? (ou / ou/propriétés /) peut être utilisé tooserve hello requêtes suivantes efficacement :<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| Plage      | La plage disposant de l’élément /prop/? (ou /) peut être utilisé tooserve hello requêtes suivantes efficacement :<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| spatial     | La plage disposant de l’élément /prop/? (ou /) peut être utilisé tooserve hello requêtes suivantes efficacement :<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --avec indexation sur les points activée<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --avec indexation sur les polygones activée              |

Par défaut, une erreur est renvoyée pour les requêtes avec des opérateurs de plage tel que > = s’il n’existe aucun index de plage (de n’importe quel type de précision) dans toosignal ordre qu’une analyse peut être requête de hello tooserve nécessaire. Requêtes de plage peuvent être effectuées sans un index de plage à l’aide d’en-tête x-ms-documentdb-enable-analyse de hello Bonjour API REST ou option de requête hello EnableScanInQuery à l’aide de hello du SDK .NET. S’il y a tous les autres filtres de requête hello utilisable par base de données Azure Cosmos toofilter d’index hello contre, aucune erreur ne s’affichera.

Bonjour les mêmes règles s’appliquent pour les requêtes spatiales. Par défaut, une erreur est renvoyée pour les requêtes spatiales s’il n’existe aucun index spatial, et aucun autre filtre qui peut être obtenue à partir de l’index de hello. Elles peuvent être effectuées en tant qu'analyse à l'aide de x-ms-documentdb-enable-scan/EnableScanInQuery.

#### <a name="index-precision"></a>Précision d’index
La précision d’index vous permet de trouver un compromis entre le traitement du stockage de l’index et les performances des requêtes. Pour les nombres, nous vous recommandons d’à l’aide de la configuration de précision par défaut hello-1 (« maximum »). Étant donné que les nombres sont JSON de 8 octets, il s’agit de configuration tooa équivalent de 8 octets. Sélection d’une valeur inférieure pour la précision, par exemple 1-7, signifie que les valeurs dans certaines toohello de carte de plages même entrée d’index. Par conséquent, vous réduirez espace de stockage d’index, mais l’exécution de requête peut avoir des documents plus de tooprocess et par conséquent consommer plus grand débit par exemple, les unités de requête.

La configuration de la précision d’index est plus pratique avec les plages de chaînes. Étant donné que les chaînes peuvent être n’importe quelle longueur arbitraire, choix hello de précision d’index hello peut affecter les performances de hello des requêtes de plage chaîne et montant de hello impact de l’espace de stockage d’index requis. Les index de plage de chaînes peuvent être configurés avec une valeur comprise entre 1 et 100, ou la valeur de précision maximale (-1). Si vous souhaitez que les requêtes Order By tooperform par rapport aux propriétés de chaîne, vous devez spécifier une précision de -1 pour les chemins d’accès correspondants hello.

Les index spatiaux toujours utilisent la précision d’index hello par défaut pour tous les types (Points, LineStrings et polygones) et ne peut pas être remplacée. 

Hello, l’exemple suivant montre comment précision de hello tooincrease pour la plage d’index dans une collection à l’aide de hello du SDK .NET. 

**Créer une collection avec une précision d'index personnalisée**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Base de données Azure Cosmos renvoie une erreur lorsqu’une requête utilise Order By, mais n’a pas un index de plage de chemin d’accès demandé de hello avec la précision maximale de hello. 
> 
> 

De même, des chemins d’accès peuvent être exclus complètement de l’indexation. Hello l’exemple suivant montre comment tooexclude une section complète de hello documents (aussi appelé) une sous-arborescence) de l’indexation à l’aide de hello « * » générique.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Activation ou désactivation de l’indexation
Vous pouvez choisir si vous voulez que hello collection tooautomatically index tous les documents. Par défaut, tous les documents sont indexés automatiquement, mais vous pouvez choisir tooturn désactiver. Lorsque l’indexation est désactivée, les documents sont accessibles uniquement par le biais de leurs liens réflexifs ou de requêtes avec l’ID.

Avec l’indexation automatique désactivé, vous pouvez toujours sélectivement ajouter uniquement les index toohello des documents spécifiques. À l’inverse, vous pouvez laisser automatique de l’indexation sur et choisir de façon sélective tooexclude des documents spécifiques uniquement. L’indexation ou désactiver les configurations sont utiles lorsque vous avez uniquement un sous-ensemble des documents nécessitant toobe interrogé.

Par exemple, hello exemple suivant montre comment tooinclude un document explicitement à l’aide de hello [DocumentDB API .NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) et hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) propriété.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Modification de stratégie d’indexation hello d’une collection
Base de données Cosmos Azure vous permet de toomake modifications toohello de stratégie d’indexation d’une collection volée hello. Une modification de stratégie sur une collection de base de données Azure Cosmos d’indexation peut entraîner des tooa modification de la forme hello d’index hello notamment hello chemins d’accès peuvent être indexées, leur précision, ainsi que le modèle de cohérence hello d’index hello proprement dit. Une modification de la stratégie d’indexation nécessite donc efficacement une transformation de l’ancien index de hello dans une autre. 

**Transformations d'index en ligne**

![Mécanismes de l’indexation – Transformations d’index en ligne Azure Cosmos DB](./media/indexing-policies/index-transformations.png)

Transformations de l’index sont effectuées en ligne, ce qui signifie que conversion efficacement des documents hello indexées par l’ancienne stratégie de hello par la nouvelle stratégie de hello **sans affecter la disponibilité d’écriture hello ou un débit approvisionné hello** de collection de Hello. Hello cohérence de lecture et les opérations d’écriture effectuées à l’aide de hello API REST, les kits de développement logiciel ou à partir de déclencheurs et procédures stockées n’est pas affecté au cours de la transformation de l’index. Cela signifie qu’il n’existe aucune performance des applications tooyour dégradation ou de temps mort lorsque vous modifiez une stratégie d’indexation.

Cependant, au moment de hello transformation de l’index est la progression, les requêtes sont finalement cohérentes quel que soit hello l’indexation de configuration du mode (cohérent ou Lazy). Également, cela s’applique tooqueries à partir de toutes les interfaces – API REST, kits de développement logiciel et à partir de procédures stockées et déclencheurs. Tout comme avec Lazy l’indexation, transformation de l’index est exécutée de façon asynchrone en arrière-plan hello sur les réplicas hello à l’aide des ressources de secours hello disponibles pour un réplica donné. 

Transformations d’index s’appliquent également aux **in situ** (en place), par exemple, base de données Azure Cosmos ne conserve pas les deux copies des index de hello et swap hello ancien index out avec hello nouveau. Cela signifie qu'aucun espace disque supplémentaire n’est requis ou utilisé dans vos collections lors de l'exécution des transformations d’index.

Lorsque vous modifiez la stratégie d’indexation, comment hello sont appliqué toomove à partir de hello ancien index toohello nouvelle un dépend principalement de hello indexation plus les configurations en mode afin que hello autres valeurs telles que chemins d’accès inclus/exclus, les types d’index et les précisions. Si vos anciennes et nouvelles stratégies utilisent l’indexation cohérente, Azure Cosmos DB effectue une transformation d’index en ligne. Impossible d’appliquer un autre changement de stratégie d’indexation avec mode d’indexation cohérent lors de la transformation de hello est en cours d’exécution.

Vous pouvez toutefois déplacer tooLazy ou aucun mode d’indexation lors d’une transformation est en cours d’exécution. 

* Lorsque vous déplacez tooLazy, hello index stratégie est modifiée effective immédiatement et base de données Azure Cosmos démarre la recréation des index de hello en mode asynchrone. 
* Lorsque vous déplacez tooNone, puis hello index est supprimé effective immédiatement. Déplacement tooNone est utile lorsque vous souhaitez toocancel une progression de transformation et démarrer avec une stratégie d’indexation différentes. 

Si vous utilisez hello .NET SDK, vous pouvez déclencher une modification de la stratégie d’indexation à l’aide de nouveau hello **ReplaceDocumentCollectionAsync** (méthode) et suivre la progression pourcentage hello de transformation d’index hello à l’aide de hello  **IndexTransformationProgress** à partir de la propriété response un **ReadDocumentCollectionAsync** appeler. Autres kits de développement logiciel et l’API REST de hello prend en charge les propriétés et méthodes équivalentes pour apporter des modifications de stratégie d’indexation.

Voici un extrait de code qui montre comment toomodify une collection de stratégie d’indexation à partir de la cohérence tooLazy mode d’indexation.

**Modifier l’indexation de la stratégie à partir de tooLazy cohérente**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


Vous pouvez vérifier la progression de hello d’une transformation de l’index en appelant ReadDocumentCollectionAsync, par exemple, comme indiqué ci-dessous.

**Suivre la progression de la transformation d’index**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

Vous pouvez supprimer des index de hello pour une collection en déplaçant toohello aucun mode d’indexation. Cela peut être un outil opérationnel utile si vous le souhaitez toocancel une transformation en cours et démarrez une nouvelle immédiatement.

**Suppression d’index hello pour une collection**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

Lorsque vous rendrait les modifications de stratégie d’indexation collections de base de données Azure Cosmos tooyour ? Hello Voici des scénarios d’utilisation les plus courants hello :

* Traiter des résultats cohérents de fonctionnement normal, mais revenir toolazy l’indexation au cours de l’importation de données en bloc
* Commencer à utiliser les nouvelles fonctionnalités d’indexation sur vos collections de base de données Azure Cosmos en cours, par exemple, comme geospatial interrogation qui nécessitent le type d’index Spatial hello ou Order By / chaîne de requêtes de plage requièrent hello chaîne type d’index de plage
* Main sélectionnez hello toobe propriétés indexée et les modifier au fil du temps
* Régler les performances des requêtes d’indexation précision tooimprove ou réduire le stockage utilisé

> [!NOTE]
> toomodify stratégie d’indexation à l’aide de ReplaceDocumentCollectionAsync, vous avez besoin de version > = version 1.3.0 Hello .NET SDK
> 
> Pour les index transformation toocomplete avec succès, vous devez vous assurer qu’il existe suffisamment d’espace libre disponible de collection de hello. Si la collection de hello atteint son quota de stockage, transformation d’index hello va être suspendue. La transformation d’index reprend automatiquement dès que de l’espace de stockage est disponible, par exemple, si vous supprimez certains documents.
> 
> 

## <a name="performance-tuning"></a>Réglage des performances
Hello DocumentDB APIs fournissent des informations sur les mesures de performances telles que le stockage d’index hello utilisé et un débit hello coût (unités de demande) pour chaque opération. Ces informations peut être utilisée toocompare diverses stratégies d’indexation et de réglage des performances.

quota de stockage toocheck hello et l’utilisation d’une collection, exécutez une demande HEAD ou GET par rapport à la ressource de collection hello et inspecter hello x-ms-demande-quota et les en-têtes x-ms-demande-usage hello. Bonjour .NET SDK, hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) et [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) propriétés dans [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) contiennent ces valeurs correspondantes .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


surcharge de hello toomeasure de l’indexation sur chaque opération d’écriture (créer, mettre à jour ou supprimer), inspecter l’en-tête x-ms-demande-frais de hello (ou équivalent de hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) propriété dans [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) Bonjour .NET SDK) nombre de hello toomeasure d’unités de demande utilisés par ces opérations.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Toohello modifications une spécification de la stratégie d’indexation
Une modification de schéma hello pour la stratégie d’indexation a été introduite le 7 juillet 2015 avec l’API REST version 2015-06-03. classes correspondantes de Hello dans les versions du Kit de développement logiciel hello ont un nouveau schéma de hello toomatch implémentations. 

Hello modifications suivantes ont été implémentée dans hello spécification JSON :

* La stratégie d'indexation prend en charge les index de plage pour les chaînes
* Chaque chemin d'accès peut avoir plusieurs définitions d'index, un pour chaque type de données
* L'indexation de précision prend en charge les nombres de 1 à 8, les chaînes de 1 à 100 et -1 (précision maximale)
* Les segments de chemins d’accès ne nécessitent pas un guillemet double de tooescape chaque chemin d’accès. Par exemple, vous pouvez ajouter un chemin d’accès pour /title/? au lieu de /"title"/?
* chemin d’accès racine de Hello représentant « tous les chemins d’accès » peut être représenté en tant que / * (en outre trop /)

Si vous avez un code qui configure collections avec une stratégie d’indexation personnalisée écrite avec version 1.1.0 de hello .NET SDK ou plus, vous devez toochange votre application de code toohandle ces modifications dans la version de tooSDK commande toomove 1.2.0. Si vous n’ont pas le code qui configure la stratégie d’indexation, ou planifier toocontinue à l’aide d’une ancienne version du Kit de développement logiciel, aucune modification n’est requise.

Pour une comparaison pratique, Voici un exemple de stratégie d’indexation personnalisée écrite à l’aide de hello version 2015-06-03 de l’API REST ainsi hello précédente version 2015-04-08.

**Stratégie d’indexation JSON précédente**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**Stratégie d’indexation JSON actuelle**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Étapes suivantes
Suivez les liens hello ci-dessous des exemples de gestion de stratégie d’index et toolearn plus d’informations sur le langage de requête de DB Azure Cosmos.

1. [Exemples de code de gestion d’index .NET de l’API DocumentDB](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [Opérations de collecte de l’API REST DocumentDB](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [Requête avec SQL](documentdb-sql-query.md)

