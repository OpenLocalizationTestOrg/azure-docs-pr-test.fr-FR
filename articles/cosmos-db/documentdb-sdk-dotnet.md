---
title: aaaAzure Cosmos DB .NET SDK & ressources | Documents Microsoft
description: "Découvrez les hello API .NET et le Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version de hello Azure Cosmos DB .NET SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Kit de développement logiciel (SDK) .NET Azure Cosmos DB : téléchargement et notes de publication
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

<tr><td>**Téléchargement du Kit de développement logiciel (SDK)**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**Documentation de l’API**</td><td>[Documentation de référence sur l’API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Exemples**</td><td>[Exemples de code .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Prise en main**</td><td>[Prise en main hello Azure Cosmos DB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Didacticiel d’application web**</td><td>[Développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Infrastructure actuellement prise en charge**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Notes de publication

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Prise en charge supplémentaire pour PartitionKeyRangeId comme une FeedOption pour étendre la valeur de plage de clés de requête résultats tooa partition spécifique. 
* Prise en charge supplémentaire pour StartTime comme un toostart ChangeFeedOption recherche de modifications de hello après cette heure.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Correction d’un problème dans hello classe JsonSerializable qui peut provoquer une exception de dépassement de capacité de pile.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Correction d’un problème nécessitant une recompilation de l’application hello en raison de l’introduction de toohello de JsonSerializerSettings comme paramètre facultatif dans le constructeur de DocumentClient hello.
* Hello marquée DocumentClient constructeur obsolète nécessitant JsonSerializerSettings comme hello dernière tooallow de paramètre pour les valeurs par défaut des paramètres ConnectionPolicy et ConsistencyLevel lors du passage de paramètres JsonSerializerSettings paramètre.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Ajout de la prise en charge de la spécification des JsonSerializerSettings personnalisés lors de l’instanciation de [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Correction d’un problème qui concernait les ordinateurs x64 qui ne prennent pas en charge l’instruction SSE4 et renvoient une SEHException lors de l’exécution de requêtes d’API Azure Cosmos DB DocumentDB.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.
*   Prise en charge ajoutée pour les mesures de requête liées aux partitions individuelles.
*   Prise en charge supplémentaire pour limiter la taille de hello hello du jeton de continuation pour les requêtes.
*   Prise en charge ajoutée pour un suivi plus détaillé des demandes ayant échoué.
*   Apporté des améliorations de performances dans le Kit de développement logiciel de hello.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Fonctionnalités identiques à 1.13.3. Plusieurs modifications internes.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Fonctionnalités identiques à 1.13.2. Plusieurs modifications internes.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Correction d’un problème qui a ignoré la valeur de PartitionKey hello fournie dans FeedOptions pour les requêtes d’agrégation.
* Résolution du problème de gestion transparente des partitions pendant l’exécution d’une requête Order By (Trier par) entre partitions intermédiaire.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Correction d’un problème qui a provoqué des blocages dans certains hello async API lorsqu’il est utilisé à l’intérieur du contexte ASP.NET.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Résout toomake SDK plus basculement tooautomatic résilient sous certaines conditions.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Corriger un problème qui provoque parfois une WebException : nom de hello distant n’a pas pu être résolu.
* Hello ajouté prend en charge pour la lecture directe d’un document typé en ajoutant la nouvelle API tooReadDocumentAsync de surcharges.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Ajout de la prise en charge LINQ des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).
* Correctif pour un problème de fuite de mémoire pour l’objet de ConnectionPolicy hello dû à l’aide de hello de gestionnaire d’événements.
* Correction d’un problème de fonctionnement d’UpsertAttachmentAsync avec l’utilisation d’ETag.
* Correction d’un problème de fonctionnement de la liaison des requêtes ORDER BY entre les partitions lors d’un tri sur un champ de chaîne.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG). Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).
* Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Correctif pour un problème dans lequel certaines des requêtes de partitions croisées hello ont échoué dans le processus d’hôte 32 bits hello.
* Correctif pour un problème dans lequel conteneur de session hello a été pas mis à jour avec le jeton hello pour les demandes ayant échouées en mode de passerelle.
* Résolution du problème causant l’échec ponctuel d’une requête avec des appels de fonctions définies par l’utilisateur en projection.
* Correctifs des performances côté client permettant d’accroître hello lecture et écriture de débit des demandes de hello.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Correctif pour un problème dans lequel conteneur de session hello a été pas mis à jour avec le jeton hello pour les demandes ayant échoué.
* Prise en charge supplémentaire pour toowork du Kit de développement logiciel hello dans un processus hôte 32 bits. Notez que si vous utilisez des requêtes entre les partitions, le processus hôte 64 bits est recommandé pour améliorer les performances.
* Amélioration des performances pour les scénarios impliquant des requêtes avec un grand nombre de valeurs de clé de partition dans une expression IN.
* Rempli différentes statistiques de quota de ressources Bonjour ResourceResponse pour la collection de documents de demandes de lecture lorsque l’option de requête PopulateQuotaInfo est définie.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Correctif de performances mineur de hello API CreateDocumentCollectionIfNotExistsAsync introduite dans 1.11.0.
* Résolution des performances dans le Kit de développement logiciel de hello pour les scénarios qui impliquent un degré élevé de demandes simultanées.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Prise en charge de hello de tooprocess nouvelles classes et méthodes [modifier le flux](change-feed.md) de documents dans une collection.
* Prise en charge de la continuité des requêtes sur plusieurs partitions et de quelques améliorations des performances pour les requêtes entre partitions.
* Ajout des méthodes CreateDatabaseIfNotExistsAsync et CreateDocumentCollectionIfNotExistsAsync.
* Prise en charge de LINQ pour les fonctions système : IsDefined, IsNull et IsPrimitive.
* Correctif de binplacing automatique du dossier bin de tooapplication suite assemblys Microsoft.Azure.Documents.ServiceInterop.dll et DocumentDB.Spatial.Sql.dll. lors de l’utilisation de package Nuget de hello aux projets qui ont des outils de project.json.
* Prise en charge de l’émission de traces ETW de côté client qui pourraient être utiles dans les scénarios de débogage.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Ajout de la prise en charge de la connectivité directe pour les collections partitionnées.
* Amélioration des performances pour hello niveau de cohérence Bounded Staleness.
* Ajout des types de données Polygone et LineString lors de la spécification de la stratégie d’indexation de collection pour les requêtes spatiales à délimitation géographique.
* Ajout de la prise en charge de LINQ pour StringEnumConverter, IsoDateTimeConverter et UnixDateTimeConverter lors de la traduction de prédicats.
* Divers correctifs de bogues de kits de développement logiciel (SDK).

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Correction d’un problème qui a causé hello suivant NotFoundException : hello lire la session n’est pas disponible pour le jeton de session d’entrée hello. Cette exception s’est produite dans certains cas lors de l’interrogation de hello en lecture-région d’un compte de géo-distribué.
* Propriété de ResponseStream hello Bonjour classe ResourceResponse, ce qui permet le flux sous-jacent de toohello un accès direct à partir d’une réponse exposée.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Hello modifié ResourceResponse, FeedResponse, StoredProcedureResponse et MediaResponse classes tooimplement hello correspondant interface publique afin qu’ils peuvent être fictive pour test piloté par déploiement (TDD).
* Résolution du problème qui provoquait la malformation d’un en-tête de clé de partition lors de l’utilisation d’un objet JsonSerializerSettings personnalisé pour la sérialisation des données.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Correction d’un problème qui a provoqué des longues requêtes toofail avec l’erreur : jeton d’autorisation n’est pas valide à hello heure actuelle.
* Fixe à un problème supprimé hello SqlParameterCollection d’origine à partir de cross-requêtes de partition haut/order by.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Prise en charge ajoutée de requêtes parallèles pour les collections partitionnées.
* Prise en charge ajoutée des requêtes ORDER BY et TOP sur plusieurs partitions pour les collections partitionnées.
* Hello fixe manquants références tooDocumentDB.Spatial.Sql.dll et Microsoft.Azure.Documents.ServiceInterop.dll qui sont nécessaires lors du référencement d’un projet de base de données Azure Cosmos avec un package Nuget de base de données Azure Cosmos de toohello référence.
* Fixe la capacité de hello toouse des paramètres de types différents lors de l’utilisation de fonctions définies par l’utilisateur dans LINQ. 
* Correction d’un bogue pour les comptes de réplication globale où Upsert appels étaient en cours d’emplacements tooread dirigée au lieu des emplacements de l’écriture.
* Ajout de méthodes toohello IDocumentClient interface qui étaient manquants : 
  * Méthode UpsertAttachmentAsync qui accepte mediaStream et les options en tant que paramètres
  * Méthode CreateAttachmentAsync qui accepte les options en tant que paramètres
  * Méthode CreateOfferQuery qui accepte querySpec en tant que paramètre.
* Classes publics non scellés qui sont exposées dans l’interface IDocumentClient hello.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.
* Ajout de la prise en charge d’une nouvelle tentative pour les requêtes limitées.  Utilisateur peut personnaliser le nombre de hello de nouvelles tentatives et temps d’attente maximale de hello en configurant la propriété de ConnectionPolicy.RetryOptions hello.
* Ajouter une nouvelle interface IDocumentClient qui définit des signatures hello de toutes les propriétés de DocumenClient et de méthodes.  Dans le cadre de cette modification, également modifié les méthodes d’extension qui créent des IQueryable et IOrderedQueryable toomethods sur hello classe DocumentClient proprement dite.
* Ajouter les hello de tooset de l’option de configuration ServicePoint.ConnectionLimit pour un point de terminaison de base de données Azure Cosmos donné Uri.  Utilisez ConnectionPolicy.MaxConnectionLimit toochange hello valeur par défaut, qui est la valeur too50.
* Propriété IPartitionResolver déconseillée et son implémentation.  La prise en charge de IPartitionResolver est désormais obsolète. Il est recommandé d’utiliser des collections partitionnées pour bénéficier d’un niveau de stockage et de débit supérieur.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Ajouter qu'un tooUri de surcharge en fonction de méthode ExecuteStoredProcedureAsync qui accepte RequestOptions en tant que paramètre.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Durée toolive (TTL) prise en charge pour les documents.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Correction d’un bogue dans l’empaquetage Nuget du Kit de développement logiciel (SDK) .NET pour son empaquetage en tant que partie d’une solution Azure Service Cloud.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Fixe]**  Lève d’interrogation de base de données Azure Cosmos le point de terminaison : « System.Net.Http.HttpRequestException : erreur lors de la copie du flux de contenu tooa'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Extension de la prise en charge de LINQ, y compris de nouveaux opérateurs pour la pagination, les expressions conditionnelles et la comparaison de plages.
  * Prendre un opérateur tooenable comportement de SELECT TOP dans LINQ
  * Comparaisons de plages CompareTo opérateur tooenable chaîne
  * Opérateurs Conditional (?) et Coalesce (??)
* **[Résolu]** ArgumentOutOfRangeException en cas de combinaison de la projection de modèle avec Where-In dans la requête LINQ. [No.81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Fixe]**  Si Select n’est pas hello expression de la dernière hello fournisseur LINQ ne supposé aucune projection et produit SELECT * incorrectement.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Mise en œuvre de l’opération Upsert, ajout des méthodes UpsertXXXAsync
* Améliorations des performances pour toutes les requêtes
* Prise en charge par le fournisseur LINQ des méthodes conditionnelles, de fusion et CompareTo pour les chaînes
* **[Fixe]**  Fournisseur LINQ--> implémentent contient la méthode sur la liste toogenerate hello SQL de même que sur IEnumerable et le tableau
* **[Fixe]**  BackoffRetryUtility utilise hello même HttpRequestMessage au lieu de créer une nouvelle tentative
* **[Obsolète]** UriFactory.CreateCollection --&gt; doit désormais utiliser UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Résolu]** Erreurs de localisation lors de l’utilisation d’autres langues que l’anglais, comme nl-NL, etc. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Ajout du routage basé sur l’ID
  * Nouvelle tooassist UriFactory d’assistance avec la conception de liens basé sur l’ID de ressource
  * Nouvelles surcharges sur tootake DocumentClient dans URI
* Ajout de IsValid() et IsValidDetailed() dans LINQ pour les données géospatiales
* Amélioration de la prise en charge du fournisseur LINQ :
  * **Mathématiques** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate
  * **Chaîne** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper
  * **Tableau** - Concat, Contains, Count
  * **IN**

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Ajout de la prise en charge de la modification des stratégies d’indexation.
  * Nouvelle méthode ReplaceDocumentCollectionAsync dans DocumentClient
  * Nouvelle propriété IndexTransformationProgress dans ResourceResponse<T> pour le suivi de l’évolution du pourcentage de modification de la stratégie d’indexation
  * DocumentCollection.IndexingPolicy est désormais mutable
* Ajout de la prise en charge de l’indexation et des requêtes spatiales.
  * Nouvel espace de noms Microsoft.Azure.Documents.Spatial pour la sérialisation/désérialisation des types de données spatiales comme Point et Polygon
  * Nouvelle classe SpatialIndex pour l’indexation des données GeoJSON stockées dans Cosmos DB
* **[Résolu]** Requête SQL incorrecte générée à partir d’une expression LINQ [#38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Ajout d’une dépendance sur Newtonsoft.Json v5.0.7.
* Toosupport les modifications apportées par la commande :
  
  * Prise en charge du fournisseur LINQ pour OrderBy() ou OrderByDescending()
  * Toosupport IndexingPolicy Order By 
    
    **Modification avec rupture possible** 
    
    Si vous avez le code existant qui collections dispositions avec une stratégie d’indexation personnalisée, votre toobe de besoins de code existante mise à jour de classe IndexingPolicy toosupport hello. Si vous n'avez pas de stratégie d'indexation personnalisée, cette modification ne vous affecte pas.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Prise en charge supplémentaire pour le partitionnement des données à l’aide de hello nouveaux HashPartitionResolver et RangePartitionResolver et classes hello IPartitionResolver.
* Ajout de la sérialisation DataContract.
* Ajout de la prise en charge de l’identificateur global unique dans le fournisseur LINQ.
* Ajout de la prise en charge d’UDF dans LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* Kit SDK GA

## <a name="release--retirement-dates"></a>Dates de lancement et de suppression
Microsoft fournit au moins une notification **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.

Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel SDK, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible. 

N’importe quel tooAzure demandes Cosmos de base de données à l’aide d’un kit de développement logiciel mis hors service sont rejetés par le service de hello.

<br/>

| Version | Date de lancement | Date de suppression |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 août 2017 |--- |
| [1.16.1](#1.16.1) |7 août 2017 |--- |
| [1.16.0](#1.16.0) |2 août 2017 |--- |
| [1.15.0](#1.15.0) |30 juin 2017 |--- |
| [1.14.1](#1.14.1) |23 mai 2017 |--- |
| [1.14.0](#1.14.0) |10 mai 2017 |--- |
| [1.13.4](#1.13.4) |09 mai 2017 |--- |
| [1.13.3](#1.13.3) |06 mai 2017 |--- |
| [1.13.2](#1.13.2) |19 avril 2017 |--- |
| [1.13.1](#1.13.1) |29 mars 2017 |--- |
| [1.13.0](#1.13.0) |24 mars 2017 |--- |
| [1.12.2](#1.12.2) |20 mars 2017 |--- |
| [1.12.1](#1.12.1) |14 mars 2017 |--- |
| [1.12.0](#1.12.0) |15 février 2017 |--- |
| [1.11.4](#1.11.4) |06 février 2017 |--- |
| [1.11.3](#1.11.3) |26 janvier 2017 |--- |
| [1.11.1](#1.11.1) |21 décembre 2016 |--- |
| [1.11.0](#1.11.0) |8 décembre 2016 |--- |
| [1.10.0](#1.10.0) |27 septembre 2016 |--- |
| [1.9.5](#1.9.5) |1er septembre 2016 |--- |
| [1.9.4](#1.9.4) |24 août 2016 |--- |
| [1.9.3](#1.9.3) |15 août 2016 |--- |
| [1.9.2](#1.9.2) |23 juillet 2016 |--- |
| [1.8.0](#1.8.0) |14 juin 2016 |--- |
| [1.7.1](#1.7.1) |6 mai 2016 |--- |
| [1.7.0](#1.7.0) |26 avril 2016 |--- |
| [1.6.3](#1.6.3) |8 avril 2016 |--- |
| [1.6.2](#1.6.2) |29 mars 2016 |--- |
| [1.5.3](#1.5.3) |19 février 2016 |--- |
| [1.5.2](#1.5.2) |14 décembre 2015 |--- |
| [1.5.1](#1.5.1) |23 novembre 2015 |--- |
| [1.5.0](#1.5.0) |5 octobre 2015 |--- |
| [1.4.1](#1.4.1) |25 août 2015 |--- |
| [1.4.0](#1.4.0) |13 août 2015 |--- |
| [1.3.0](#1.3.0) |5 août 2015 |--- |
| [1.2.0](#1.2.0) |6 juillet 2015 |--- |
| [1.1.0](#1.1.0) |30 avril 2015 |--- |
| [1.0.0](#1.0.0) |8 avril 2015 |--- |


## <a name="faq"></a>Forum Aux Questions
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Voir aussi
toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service. 

