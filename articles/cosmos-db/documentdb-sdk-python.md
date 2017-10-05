---
title: API, SDK et ressources Python Azure Cosmos DB | Microsoft Docs
description: "Découvrez l’API et le Kit de développement logiciel (SDK) Python, y compris les dates de publication, les dates de suppression et les modifications apportées entre chaque version du Kit de développement logiciel (SDK) Python Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Kit de développement logiciel (SDK) Python Azure Cosmos DB : notes de publication et ressources
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

<tr><td>**Téléchargement du Kit de développement logiciel (SDK)**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Documentation de l’API**</td><td>[Documentation de référence sur l’API Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Instructions d’installation du Kit de développement logiciel (SDK)**</td><td>[Instructions d’installation du Kit de développement logiciel (SDK) Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribution au Kit de développement logiciel (SDK)**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Prise en main**</td><td>[Bien démarrer avec le Kit de développement logiciel (SDK) Python](documentdb-python-application.md)</td></tr>

<tr><td>**Plateforme actuellement prise en charge**</td><td>[Python 2.7](https://www.python.org/downloads/) et [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Notes de publication
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).
* Ajout d’une option permettant de désactiver la vérification SSL pendant son exécution sur l’émulateur Cosmos DB.
* Suppression de la restriction du module de demandes dépendantes qui devait correspondre exactement à la version 2.10.0.
* Débit minimal réduit sur les collections partitionnées de 10 100 unités de demande/s à 2 500 unités de demande/s.
* Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.
* Version de l’API REST passée à « 2017-01-19 » à l’occasion de cette publication.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Modifications éditoriales apportées aux commentaires de documentation.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Ajout de la prise en charge de Python 3.5.
* Ajout de la prise en charge du regroupement de connexions à l’aide d’un module de demandes.
* Ajout de la prise en charge de la cohérence de session.
* Ajout de la prise en charge des requêtes TOP/ORDERBY pour les collections partitionnées.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées. (Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, Azure Cosmos DB accepte neuf nouvelles tentatives pour chaque requête lorsque le code d’erreur 429 est renvoyé, conformément à l’heure de retryAfter spécifiée dans l’en-tête de réponse. Il est désormais possible de définir un intervalle fixe de nouvelle tentative dans la propriété RetryOptions sur l’objet ConnectionPolicy, si vous souhaitez ignorer le temps retryAfter retourné par le serveur entre chaque nouvelle tentative. Azure Cosmos DB attend maintenant au maximum 30 secondes pour chaque requête limitée (quel que soit le nombre de nouvelles tentatives) et renvoie la réponse avec un code d’erreur 429. Cette durée peut également être remplacée dans la propriété RetryOptions sur l’objet ConnectionPolicy.
* Cosmos DB renvoie maintenant x-ms-throttle-retry-count et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse dans chaque requête pour signaler le nombre limite de nouvelles tentatives et le cumul de temps d’attente observé par la requête entre les nouvelles tentatives.
* Suppression de la classe RetryPolicy et de la propriété correspondante (retry_policy) exposées sur la classe document_client, et introduction d’une classe RetryOptions qui expose la propriété RetryOptions sur la classe ConnectionPolicy pouvant être utilisée pour substituer certaines des options de nouvelle tentative par défaut.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Ajout de la prise en charge des comptes de base de données de plusieurs régions.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Ajout de la fonctionnalité de durée de vie (TTL) pour les documents.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Résolution des bogues liés au partitionnement côté serveur pour autoriser des caractères spéciaux dans le chemin d’accès à la clé de partition.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Ajoutez des programmes de résolution de partitions par hachage et par spécification de plages de valeurs pour vous aider lors du partitionnement des applications sur plusieurs partitions.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implémentation de l’opération Upsert. Nouvelles méthodes UpsertXXX ajoutées pour prendre en charge la fonctionnalité Upsert.
* Implémenter l'ID en fonction du routage. Aucune modification d'API publique, toutes les modifications en interne.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Prise en charge de l'index géospatial.
* Validation de la propriété ID pour toutes les ressources. Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.
* Ajoute le nouvel en-tête « progression de la transformation de l'index » à ResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implémente la stratégie d’indexation V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Prend en charge la connexion proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* Kit de développement logiciel (SDK) GA

## <a name="release--retirement-dates"></a>Dates de lancement et de suppression
Microsoft fournira une notification au moins **12 mois** avant le retrait d’un Kit de développement logiciel (SDK) pour faciliter la transition vers une version plus récente/prise en charge.

Les nouvelles fonctionnalités et fonctions, et les optimisations sont uniquement ajoutées au Kit de développement logiciel (SDK) actuel. Par conséquent, il est recommandé de toujours passer à la dernière version du Kit de développement logiciel (SDK) dès que possible. 

Le service rejette toute requête envoyée à Cosmos DB à l’aide d’un Kit de développement logiciel (SDK) supprimé.

> [!WARNING]
> Toutes les versions du Kit de développement logiciel (SDK) Azure DocumentDB pour Python antérieures à la version **1.0.0** seront supprimées le **29 février 2016**. 
> 
> 

<br/>

| Version | Date de lancement | Date de suppression |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 mai 2017 |--- |
| [2.1.0](#2.1.0) |1er mai 2017 |--- |
| [2.0.1](#2.0.1) |30 octobre 2016 |--- |
| [2.0.0](#2.0.0) |29 septembre 2016 |--- |
| [1.9.0](#1.9.0) |7 juillet 2016 |--- |
| [1.8.0](#1.8.0) |14 juin 2016 |--- |
| [1.7.0](#1.7.0) |26 avril 2016 |--- |
| [1.6.1](#1.6.1) |8 avril 2016 |--- |
| [1.6.0](#1.6.0) |29 mars 2016 |--- |
| [1.5.0](#1.5.0) |3 janvier 2016 |--- |
| [1.4.2](#1.4.2) |6 octobre 2015 |--- |
| [1.4.1](#1.4.1) |6 octobre 2015 |--- |
| [1.2.0](#1.2.0) |6 août 2015 |--- |
| [1.1.0](#1.1.0) |9 juillet 2015 |--- |
| [1.0.1](#1.0.1) |25 mai 2015 |--- |
| [1.0.0](#1.0.0) |7 avril 2015 |--- |
| 0.9.4-prelease |14 janvier 2015 |29 février 2016 |
| 0.9.3-prelease |9 décembre 2014 |29 février 2016 |
| 0.9.2-prelease |25 novembre 2014 |29 février 2016 |
| 0.9.1-prelease |23 septembre 2014 |29 février 2016 |
| 0.9.0-prelease |21.08.14 |29 février 2016 |

## <a name="faq"></a>Forum Aux Questions
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Voir aussi
Pour en savoir plus sur Cosmos DB, consultez la page du service [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

