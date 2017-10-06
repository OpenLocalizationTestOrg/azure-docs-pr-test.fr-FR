---
title: "Azure Cosmos DB : API Java DocumentDB, Kit de développement logiciel (SDK) et ressources | Microsoft Docs"
description: "Découvrez les hello API Java et le Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version du Kit de développement logiciel Azure Cosmos DB DocumentDB Java de hello."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB - Kit de développement logiciel (SDK) Java DocumentDB : notes de publication et ressources
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Flux de modification .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.JS](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [API REST Resource Provider](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Téléchargement du Kit de développement logiciel (SDK)**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**Documentation de l’API**</td><td>[Documentation de référence sur l’API Java](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**Contribuent tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**Prise en main**</td><td>[Prise en main hello Kit de développement logiciel Java](documentdb-java-get-started.md)</td></tr>

<tr><td>**Didacticiel d’application web**</td><td>[Développement d’applications web avec Azure Cosmos DB](documentdb-java-application.md)</td></tr>

<tr><td>**Runtime actuellement pris en charge**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>Notes de publication

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Fractionnements de pages toorequest de correctifs critiques du traitement au cours de la partition.
* Résolution du problème de hello fort et niveaux de cohérence BoundedStaleness.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.
* Correction d’un bogue de lecture de collection en mode de session.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Activation de la prise en charge de la collection partitionnée avec au minimum 2 500 RU/seconde et des incréments d’évolution de 100 RU/seconde.
* Correction d’un bogue dans l’assembly natif de hello qui peut provoquer des NullRef exception de certaines requêtes.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* Correction d’un bogue dans la configuration du moteur de requête hello qui peut provoquer des exceptions pour les requêtes en mode de passerelle.
* Résolu quelques bogues dans le conteneur de session hello qui peut provoquer une exception « Ressource propriétaire introuvable » pour les demandes immédiatement après la création de la collection.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG). Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).
* Ajout de la prise en charge de la modification de flux.
* Ajout de la prise en charge des informations relatives aux quotas de collections via RequestOptions.setPopulateQuotaInfo.
* Ajout de la prise en charge de l’enregistrement de script de procédure stockée via RequestOptions.setScriptLoggingEnabled.
* Correction d’un bogue dans lequel la requête en mode DirectHttps peut se bloquer lorsqu’elle rencontre des échecs de limitation.
* Correction d’un bogue dans le mode de cohérence de session.
* Correction d’un bogue susceptible d’entraîner l’exception NullReferenceException dans HttpContext lorsque le taux de demandes est élevé.
* Amélioration des performances du mode DirectHttps.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Ajout de la prise en charge simple d’un proxy basé sur les instances d’un client avec l’API ConnectionPolicy.setProxy().
* Ajouté DocumentClient.close() API tooproperly arrêter DocumentClient l’instance.
* Meilleures performances des requêtes en mode de connectivité directe en dérivant de plan de requête hello assembly natif hello au lieu de hello passerelle.
* Définissez FAIL_ON_UNKNOWN_PROPERTIES = false, les utilisateurs n’avez pas besoin toodefine JsonIgnoreProperties dans leur POJO.
* Journalisation refactorisé toouse SLF4J.
* Correction de quelques autres bogues dans un lecteur de cohérence.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Correction d’un bogue dans les pertes de connexion tooprevent hello connexion gestion en mode de connexion directe.
* Correction d’un bogue dans la requête TOP de hello où il peut lever NullReferenece exception.
* Amélioration des performances en réduisant le nombre de hello d’appel de réseau pour les caches internes hello.
* Ajout d’un code d’état, d’un ID d’activité et d’un URI de requête dans DocumentClientException pour une meilleure résolution des problèmes.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Correction d’un problème dans la gestion des connexions hello de stabilité.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* Ajout de la prise en charge du niveau de cohérence BoundedStaleness.
* Ajout de la prise en charge de la connectivité directe pour les opérations CRUD pour les collections partitionnées.
* Correction d’un bogue dans l’interrogation d’une base de données avec SQL.
* Correction d’un bogue dans le cache de session hello où le jeton de session peut-être être défini de façon incorrecte.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Ajout de la prise en charge des requêtes parallèles sur plusieurs partitions.
* Ajout de la prise en charge des requêtes TOP/ORDER BY pour les collections partitionnées.
* Ajout de la prise en charge de la cohérence forte.
* Ajout de la prise en charge des requêtes en fonction du nom lors de l’utilisation de la connectivité directe.
* Toomake fixe ActivityId maintenir une cohérence entre toutes les nouvelles tentatives de requête.
* Correction d’un bogue lié cache de session toohello lors de la recréation d’une collection de hello même nom.
* Ajout des types de données Polygone et LineString lors de la spécification de la stratégie d’indexation de collection pour les requêtes spatiales à délimitation géographique.
* Résolution des problèmes liés à Java Doc pour Java 1.8.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* Correction d’un bogue dans PartitionKeyDefinitionMap toocache les collections de partitions uniques afin de pas supplémentaire fetch partition principales demandes.
* Correction d’une nouvelle tentative de bogue toonot lorsqu’une valeur de clé de partition incorrecte est fournie.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.
* Prise en charge pour la nouvelle tentative automatique sur les demandes limitées par hello de toocustomize options max nouvelles tentatives et recommencez max de délai d’attente.  Voir RetryOptions et ConnectionPolicy.getRetryOptions().
* Propriété IPartitionResolver déconseillée basée sur un code de partitionnement personnalisé. Utilisez des collections partitionnées pour bénéficier d’un niveau de stockage et de débit supérieur.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Ajout de la prise en charge d’une stratégie de nouvelle tentative pour la limitation.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Durée toolive (TTL) prise en charge pour les documents.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* Correction d’un bogue dans les valeurs de hachage HashPartitionResolver toogenerate dans toobe little-endian cohérent avec les autres kits de développement logiciel.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Ajouter & age de hachage tooassist de programmes de résolution de partition avec des applications de partitionnement sur plusieurs partitions.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Implémentation de l’opération Upsert. Nouvelles méthodes upsertXXX a ajouté une fonctionnalité de Upsert toosupport.
* Implémenter l'ID en fonction du routage. Aucune modification d'API publique, toutes les modifications en interne.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Version a ignoré le numéro de version toobring d’alignement avec les autres kits de développement logiciel

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Prise en charge de l'index géospatial
* Validation de la propriété ID pour toutes les ressources. Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.
* Ajoute un nouveau tooResourceResponse de « cours de transformation d’index » en-tête.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implémente la stratégie d'indexation V2

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* Kit SDK GA

## <a name="release--retirement-dates"></a>Dates de lancement et de suppression
Microsoft enverra une notification au moins **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.

Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel kit de développement logiciel, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible.

N’importe quel tooCosmos demande à l’aide d’un kit de développement logiciel mis hors service de base de données seront rejetées par le service de hello.

> [!WARNING]
> Toutes les versions de hello DocumentDB SDK pour tooversion préalable de Java **1.0.0** sera retiré le **29 février 2016**.
> 
> 

<br/>

| Version | Date de lancement | Date de suppression |
| --- | --- | --- |
| [1.12.0](#1.12.0) |11 juillet 2017 |--- |
| [1.11.0](#1.11.0) |10 mai 2017 |--- |
| [1.10.0](#1.10.0) |11 mars 2017 |--- |
| [1.9.6](#1.9.6) |21 février 2017 |--- |
| [1.9.5](#1.9.5) |31 janvier 2017 |--- |
| [1.9.4](#1.9.4) |24 novembre 2016 |--- |
| [1.9.3](#1.9.3) |30 octobre 2016 |--- |
| [1.9.2](#1.9.2) |28 octobre 2016 |--- |
| [1.9.1](#1.9.1) |26 octobre 2016 |--- |
| [1.9.0](#1.9.0) |3 octobre 2016 |--- |
| [1.8.1](#1.8.1) |30 juin 2016 |--- |
| [1.8.0](#1.8.0) |14 juin 2016 |--- |
| [1.7.1](#1.7.1) |30 avril 2016 |--- |
| [1.7.0](#1.7.0) |27 avril 2016 |--- |
| [1.6.0](#1.6.0) |29 mars 2016 |--- |
| [1.5.1](#1.5.1) |31 décembre 2015 |--- |
| [1.5.0](#1.5.0) |4 décembre 2015 |--- |
| [1.4.0](#1.4.0) |5 octobre 2015 |--- |
| [1.3.0](#1.3.0) |5 octobre 2015 |--- |
| [1.2.0](#1.2.0) |5 août 2015 |--- |
| [1.1.0](#1.1.0) |9 juillet 2015 |--- |
| [1.0.1](#1.0.1) |12 mai 2015 |--- |
| [1.0.0](#1.0.0) |7 avril 2015 |--- |
| 0.9.5-prelease |9 mars 2015 |29 février 2016 |
| 0.9.4-prelease |17 février 2015 |29 février 2016 |
| 0.9.3-prelease |13 janvier 2015 |29 février 2016 |
| 0.9.2-prelease |19 décembre 2014 |29 février 2016 |
| 0.9.1-prelease |19 décembre 2014 |29 février 2016 |
| 0.9.0-prelease |10 décembre 2014 |29 février 2016 |

## <a name="faq"></a>Forum Aux Questions
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Voir aussi
toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.

