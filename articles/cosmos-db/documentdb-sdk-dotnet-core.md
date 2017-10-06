---
title: "aaaAzure Cosmos DB .NET Core API, Kit de développement logiciel et les ressources | Documents Microsoft"
description: "Découvrez les hello .NET Core API et Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version de hello Kit de développement logiciel Azure Cosmos DB .NET Core."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Kit de développement logiciel (SDK) .NET Core Azure Cosmos DB : notes de publication et ressources
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

<tr><td>**Téléchargement du Kit de développement logiciel (SDK)**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**Documentation de l’API**</td><td>[Documentation de référence sur l’API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Exemples**</td><td>[Exemples de code .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Prise en main**</td><td>[Prise en main hello Kit de développement logiciel Azure Cosmos DB .NET Core](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Didacticiel d’application web**</td><td>[Développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Infrastructure actuellement prise en charge**</td><td>[.NET Standard 1.6 et .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Notes de publication

Hello Kit de développement logiciel Azure Cosmos DB .NET Core a parité de fonctionnalités avec la version la plus récente de hello hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Bonjour Azure Cosmos DB .NET Core SDK n’est pas encore compatible avec les applications de plateforme Windows universelle (UWP). Si vous êtes intéressé par hello Kit de développement .NET Core qui ne prend pas en charge les applications UWP, envoyer un courrier électronique trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Prise en charge supplémentaire pour PartitionKeyRangeId comme une FeedOption pour étendre la valeur de plage de clés de requête résultats tooa partition spécifique. 
* Prise en charge supplémentaire pour StartTime comme un toostart ChangeFeedOption recherche de modifications de hello après cette heure. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Correction d’un problème dans hello classe JsonSerializable qui peut provoquer une exception de dépassement de capacité de pile.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Ajout de la prise en charge de la spécification des JsonSerializerSettings personnalisés lors de l’instanciation d’une instance [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Prise en charge 1,5 Standard de .NET en tant qu’une des infrastructures de cible hello.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Correction d’un problème concernant les ordinateurs x64 qui ne prennent pas en charge l’instruction SSE4 et génèrent une SEHException lors de l’exécution de requêtes Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.
*   Prise en charge ajoutée pour les mesures de requête liées aux partitions individuelles.
*   Prise en charge supplémentaire pour limiter la taille de hello hello du jeton de continuation pour les requêtes.
*   Prise en charge ajoutée pour un suivi plus détaillé des demandes ayant échoué.
*   Apporté des améliorations de performances dans le Kit de développement logiciel de hello.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Correction d’un problème qui a ignoré la valeur de PartitionKey hello fournie dans FeedOptions pour les requêtes d’agrégation.
* Résolution du problème de gestion transparente des partitions pendant l’exécution d’une requête Order By (Trier par) entre partitions intermédiaire.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Correction d’un problème qui a provoqué des blocages dans certains hello async API lorsqu’il est utilisé à l’intérieur du contexte ASP.NET.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Résout toomake SDK plus basculement tooautomatic résilient sous certaines conditions.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Corriger un problème qui provoque parfois une WebException : nom de hello distant n’a pas pu être résolu.
* Hello ajouté prend en charge pour la lecture directe d’un document typé en ajoutant la nouvelle API tooReadDocumentAsync de surcharges.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Ajout de la prise en charge LINQ des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).
* Correctif pour un problème de fuite de mémoire pour l’objet de ConnectionPolicy hello dû à l’aide de hello de gestionnaire d’événements.
* Correction d’un problème de fonctionnement d’UpsertAttachmentAsync avec l’utilisation d’ETag.
* Correction d’un problème de fonctionnement de la liaison des requêtes ORDER BY entre les partitions lors d’un tri sur un champ de chaîne.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG). Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).
* Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Kit de développement logiciel Azure Cosmos DB .NET Core vous permet de toobuild rapide, inter-plateformes [ASP.NET Core](https://www.asp.net/core) et [.NET Core](https://www.microsoft.com/net/core#windows) toorun d’applications sur Windows, Mac et Linux. Bonjour dernière version de hello Kit de développement logiciel Azure Cosmos DB .NET Core est entièrement [Xamarin](https://www.xamarin.com) compatible et être utilisés toobuild les applications qui ciblent iOS, Android et Mono (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Bonjour Azure Cosmos DB .NET Core aperçu SDK vous permet de toobuild rapide, inter-plateformes [ASP.NET Core](https://www.asp.net/core) et [.NET Core](https://www.microsoft.com/net/core#windows) toorun d’applications sur Windows, Mac et Linux.

Bonjour Azure Cosmos DB .NET Core aperçu SDK a parité de fonctionnalités avec la version la plus récente de hello hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) et prend en charge hello suivantes :
* Tous les [modes de connexion](performance-tips.md#networking) : mode passerelle, TCP Direct et HTTPs Direct. 
* Tous les [niveaux de cohérence](consistency-levels.md): Forte, Session, Obsolescence limitée et Éventuelle.
* [Collections partitionnées](partition-data.md). 
* [Comptes de base de données multirégions et géoréplication](distribute-data-globally.md).

Si vous avez des questions, toothis connexes SDK, validez trop[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), fichier ou un problème dans hello [référentiel github](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Dates de lancement et de suppression

| Version | Date de lancement | Date de suppression |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 août 2017 |--- | 
| [1.4.1](#1.4.1) |7 août 2017 |--- |
| [1.4.0](#1.4.0) |2 août 2017 |--- |
| [1.3.2](#1.3.2) |12 juin 2017 |--- |
| [1.3.1](#1.3.1) |23 mai 2017 |--- |
| [1.3.0](#1.3.0) |10 mai 2017 |--- |
| [1.2.2](#1.2.2) |19 avril 2017 |--- |
| [1.2.1](#1.2.1) |29 mars 2017 |--- |
| [1.2.0](#1.2.0) |25 mars 2017 |--- |
| [1.1.2](#1.1.2) |20 mars 2017 |--- |
| [1.1.1](#1.1.1) |14 mars 2017 |--- |
| [1.1.0](#1.1.0) |16 février 2017 |--- |
| [1.0.0](#1.0.0) |21 décembre 2016 |--- |
| [0.1.0-preview](#0.1.0-preview) |15 novembre 2016 |31 décembre 2016 |

## <a name="see-also"></a>Voir aussi
toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service. 

