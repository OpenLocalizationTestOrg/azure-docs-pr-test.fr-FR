---
title: "aaaAzure Cosmos DB Python API, Kit de développement logiciel et les ressources | Documents Microsoft"
description: "Découvrez les hello Python API et Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version du Kit de développement logiciel Azure Cosmos DB Python de hello."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
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

<tr><td>**Contribuent tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Prise en main**</td><td>[Prise en main hello Python SDK](documentdb-python-application.md)</td></tr>

<tr><td>**Plateforme actuellement prise en charge**</td><td>[Python 2.7](https://www.python.org/downloads/) et [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Notes de publication
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).
* Ajout d’une option permettant de désactiver la vérification SSL pendant son exécution sur l’émulateur Cosmos DB.
* Supprimé la restriction hello de demandes dépendantes module toobe 2.10.0 exactement.
* Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.
* Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.
* Version de l’API REST pour agrandir trop ' 2017-01-19 » avec cette version.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Apportées les modifications rédactionnelles toodocumentation commentaires.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Ajout de la prise en charge de Python 3.5.
* Ajout de la prise en charge du regroupement de connexions à l’aide d’un module de demandes.
* Ajout de la prise en charge de la cohérence de session.
* Ajout de la prise en charge des requêtes TOP/ORDERBY pour les collections partitionnées.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées. (Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, base de données Azure Cosmos tentatives de neuf pour chaque demande lorsque le code d’erreur 429 est rencontrée, en respectant le temps de retryAfter hello dans l’en-tête de réponse hello. Un intervalle fixe peut désormais être défini en tant que partie de hello RetryOptions propriété sur l’objet de ConnectionPolicy hello si vous souhaitez que tooignore hello retryAfter retourné par serveur entre les tentatives de hello. Base de données Azure Cosmos attend maintenant un maximum de 30 secondes pour chaque demande qui est limitée (quel que soit le nombre de tentatives) et retourne la réponse hello avec le code d’erreur 429. Cette durée peut également être remplacées Bonjour propriété RetryOptions sur ConnectionPolicy objet.
* COSMOS DB retourne x-ms-limitation de bande passante--nombre de tentatives et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse hello dans chaque limitation hello toodenote des demandes délai entre deux tentatives nombre et hello cummulative hello demander d’attente entre les tentatives de hello.
* Classe de RetryPolicy hello supprimé et la propriété correspondante, hello (retry_policy) exposées sur la classe de document_client hello et au lieu de cela introduit une classe RetryOptions exposition propriété RetryOptions hello classe ConnectionPolicy qui peut être utilisé toooverride options des par défaut de hello de nouvelle tentative.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Hello ajouté prend en charge pour la fonctionnalité tooLive(TTL) de temps pour les documents.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Correctifs de bogues liés côté tooserver partitionnement tooallow des caractères spéciaux dans le chemin d’accès de partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Ajouter & age de hachage tooassist de programmes de résolution de partition avec des applications de partitionnement sur plusieurs partitions.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implémentation de l’opération Upsert. Nouvelles méthodes UpsertXXX a ajouté une fonctionnalité de Upsert toosupport.
* Implémenter l'ID en fonction du routage. Aucune modification d'API publique, toutes les modifications en interne.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Prise en charge de l'index géospatial.
* Validation de la propriété ID pour toutes les ressources. Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.
* Ajoute un nouveau tooResourceResponse de « cours de transformation d’index » en-tête.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implémente la stratégie d’indexation V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Prend en charge la connexion proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* Kit de développement logiciel (SDK) GA

## <a name="release--retirement-dates"></a>Dates de lancement et de suppression
Microsoft enverra une notification au moins **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.

Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel kit de développement logiciel, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible. 

N’importe quel tooCosmos demande à l’aide d’un kit de développement logiciel mis hors service de base de données seront rejetées par le service de hello.

> [!WARNING]
> Toutes les versions de hello Kit de développement logiciel Azure DocumentDB pour tooversion préalable de Python **1.0.0** sera retiré le **29 février 2016**. 
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
toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service. 

