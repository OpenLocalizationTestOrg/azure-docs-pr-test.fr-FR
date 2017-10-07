---
title: "aaaAzure Cosmos DB Node.js API, Kit de développement logiciel et les ressources | Documents Microsoft"
description: "Découvrez les hello Node.js API et Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version de hello Azure Cosmos DB Node.js SDK."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Kit de développement logiciel (SDK) Azure Cosmos DB Node.js : notes de publication et ressources
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

<tr><td>**Téléchargement du Kit de développement logiciel (SDK)**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Documentation de l’API**</td><td>[Documentation de référence de l’API Node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Instructions d’installation du Kit de développement logiciel (SDK)**</td><td>[Instructions d’installation](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Contribuent tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Exemples**</td><td>[Exemples de code Node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Didacticiel de prise en main**</td><td>[Prise en main hello Node.js SDK](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Didacticiel d’application web**</td><td>[Générer une application web Node.js à l’aide d’Azure Cosmos DB](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Plateforme actuellement prise en charge**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Notes de publication

### <a name="1.12.2"/>1.12.2</a>
*   Documentation npm mise à jour.

### <a name="1.12.1"/>1.12.1</a>
* Correction d’un bogue dans executeStoredProcedure où les documents impliqués disposaient de caractères Unicode spéciaux (LS, PS).
* Correction d’un bogue dans la gestion des documents avec des caractères Unicode dans la clé de partition hello.
* Prise en charge fixe pour la création de regroupements avec un support nom hello. Problème GitHub n° 114.
* Prise en charge rétablie du jeton d’autorisation. Problème GitHub n° 178.

### <a name="1.12.0"/>1.12.0</a>
* Ajout de la prise en charge d’un nouveau [niveau de cohérence](consistency-levels.md) nommé ConsistentPrefix.
* Ajout de la prise en charge de UriFactory.
* Correction d’un bogue de prise en charge des caractères Unicode. Problème GitHub n° 171.

### <a name="1.11.0"/>1.11.0</a>
* Prise en charge de hello ajouté pour les requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).
* Option hello ajoutée pour contrôler le degré de parallélisme pour entre les requêtes de partition.
* Option hello ajouté pour désactiver la vérification SSL lors de l’exécution par rapport à l’émulateur de base de données Azure Cosmos.
* Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.
* Bogue de jeton continuation hello fixe pour une collection de partition unique. Problème GitHub n° 107.
* Bogue d’executeStoredProcedure hello fixe de gestion de 0 en tant que param unique. Problème GitHub n° 155.

### <a name="1.10.2"/>1.10.2</a>
* Agent utilisateur fixe en-tête tooinclude hello SDK version.
* Nettoyage de code mineur.

### <a name="1.10.1"/>1.10.1</a>
* La désactivation de vérification SSL lors de l’utilisation de hello SDK tootarget hello emulator(hostname=localhost).
* Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.

### <a name="1.10.0"/>1.10.0</a>
* Ajout de la prise en charge des requêtes parallèles sur plusieurs partitions.
* Ajout de la prise en charge des requêtes TOP/ORDER BY pour les collections partitionnées.

### <a name="1.9.0"/>1.9.0</a>
* Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées. (Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, base de données Azure Cosmos tentatives de neuf pour chaque demande lorsque le code d’erreur 429 est rencontrée, en respectant le temps de retryAfter hello dans l’en-tête de réponse hello. Un intervalle fixe peut désormais être défini en tant que partie de hello RetryOptions propriété sur l’objet de ConnectionPolicy hello si vous souhaitez que tooignore hello retryAfter retourné par serveur entre les tentatives de hello. Base de données Azure Cosmos attend maintenant un maximum de 30 secondes pour chaque demande qui est limitée (quel que soit le nombre de tentatives) et retourne la réponse hello avec le code d’erreur 429. Cette durée peut également être substituée dans hello propriété RetryOptions sur ConnectionPolicy objet.
* COSMOS DB retourne x-ms-limitation de bande passante--nombre de tentatives et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse hello dans chaque limitation hello toodenote des demandes délai entre deux tentatives nombre et hello cumulative hello demander d’attente entre les tentatives de hello.
* Hello RetryOptions classe a été ajouté, exposant hello RetryOptions propriété sur une classe ConnectionPolicy hello qui peut être utilisé toooverride certains de valeur par défaut hello options de nouvelle tentative.

### <a name="1.8.0"/>1.8.0</a>
* Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.

### <a name="1.7.0"/>1.7.0</a>
* Hello ajouté prend en charge pour la fonctionnalité tooLive(TTL) de temps pour les documents.

### <a name="1.6.0"/>1.6.0</a>
* Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Bogue RangePartitionResolver.resolveForRead où il a été ne retourne pas des liens en raison de concat incorrecte de tooa des résultats.

### <a name="1.5.5"/>1.5.5</a>
* Résout hashParitionResolver resolveForRead() : levait une exception si aucune clé de partition n’était fournie, au lieu de renvoyer une liste de tous les liens enregistrés.

### <a name="1.5.4"/>1.5.4</a>
* Résout le problème [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -dédié de l’Agent HTTPS : la modification de l’agent global de hello pour des raisons de base de données Azure Cosmos. Utiliser un agent dédié pour toutes les demandes de lib hello.

### <a name="1.5.3"/>1.5.3</a>
* Résolution du problème [n° 81](https://github.com/Azure/azure-documentdb-node/issues/81) : gestion correcte des tirets dans les ID de média.

### <a name="1.5.2"/>1.5.2</a>
* Résolution du problème [n° 95](https://github.com/Azure/azure-documentdb-node/issues/95) : avertissement de fuite de l’écouteur EventEmitter.

### <a name="1.5.1"/>1.5.1</a>
* Résout le problème [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -renommer toohash de hachage de dossier pour les systèmes qui respecte la casse.

### <a name="1.5.0"/>1.5.0</a>
* Implémentation de la prise en charge du partitionnement via l’ajout de programmes de résolution de partitions de hachage et de plage.

### <a name="1.4.0"/>1.4.0</a>
* Implémentation de l’opération Upsert. Nouvelles méthodes upsertXXX sur documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Numéros de version ignorée toobring en alignement avec les autres kits de développement logiciel.

### <a name="1.2.2"/>1.2.2</a>
* Fractionnement Q promet référentiel toonew de wrapper.
* Fichier toopackage de mise à jour pour le Registre npm.

### <a name="1.2.1"/>1.2.1</a>
* Implémentation du routage basé sur l’ID.
* Résolution du problème [n° 49](https://github.com/Azure/azure-documentdb-node/issues/49) - propriété actuelle en conflit avec la méthode current().

### <a name="1.2.0"/>1.2.0</a>
* Ajout de la prise en charge de l’index géospatial.
* Validation de la propriété ID pour toutes les ressources. Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, &#47;&#47; ou se terminer par un espace.
* Ajoute un nouveau tooResourceResponse de « cours de transformation d’index » en-tête.

### <a name="1.1.0"/>1.1.0</a>
* Implémente la stratégie d’indexation V2.

### <a name="1.0.3"/>1.0.3</a>
* Problème [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - implémentée eslint des grunt des configurations de base de hello et assurons le Kit de développement logiciel.

### <a name="1.0.2"/>1.0.2</a>
* Problème [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Le wrapper de promesses n’inclut pas d’en-tête avec erreur.

### <a name="1.0.1"/>1.0.1</a>
* Implémenté tooquery possibilité de conflits en ajoutant readConflicts, readConflictAsync et queryConflicts.
* Mise à jour de la documentation de l’API.
* Problème [n° 41](https://github.com/Azure/azure-documentdb-node/issues/41) : Erreur client.createDocumentAsync.

### <a name="1.0.0"/>1.0.0</a>
* Kit de développement logiciel (SDK) GA

## <a name="release--retirement-dates"></a>Dates de lancement et de suppression
Microsoft fournit au moins une notification **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.

Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel SDK, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible.

Toute demande tooCosmos DB à l’aide d’un kit de développement logiciel mis hors service est rejetée par le service de hello.

<br/>

| Version | Date de lancement | Date de suppression |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 août 2017 |--- |
| [1.12.1](#1.12.1) |10 août 2017 |--- |
| [1.12.0](#1.12.0) |10 mai 2017 |--- |
| [1.11.0](#1.11.0) |16 mars 2017 |--- |
| [1.10.2](#1.10.2) |27 janvier 2017 |--- |
| [1.10.1](#1.10.1) |22 décembre 2016 |--- |
| [1.10.0](#1.10.0) |3 octobre 2016 |--- |
| [1.9.0](#1.9.0) |7 juillet 2016 |--- |
| [1.8.0](#1.8.0) |14 juin 2016 |--- |
| [1.7.0](#1.7.0) |26 avril 2016 |--- |
| [1.6.0](#1.6.0) |29 mars 2016 |--- |
| [1.5.6](#1.5.6) |8 mars 2016 |--- |
| [1.5.5](#1.5.5) |2 février 2016 |--- |
| [1.5.4](#1.5.4) |1er février 2016 |--- |
| [1.5.2](#1.5.2) |26 janvier 2016 |--- |
| [1.5.2](#1.5.2) |22 janvier 2016 |--- |
| [1.5.1](#1.5.1) |4 janvier 2016 |--- |
| [1.5.0](#1.5.0) |31 décembre 2015 |--- |
| [1.4.0](#1.4.0) |6 octobre 2015 |--- |
| [1.3.0](#1.3.0) |6 octobre 2015 |--- |
| [1.2.2](#1.2.2) |10 septembre 2015 |--- |
| [1.2.1](#1.2.1) |15 août 2015 |--- |
| [1.2.0](#1.2.0) |5 août 2015 |--- |
| [1.1.0](#1.1.0) |9 juillet 2015 |--- |
| [1.0.3](#1.0.3) |4 juin 2015 |--- |
| [1.0.2](#1.0.2) |23 mai 2015 |--- |
| [1.0.1](#1.0.1) |15 mai 2015 |--- |
| [1.0.0](#1.0.0) |8 avril 2015 |--- |

## <a name="faq"></a>Forum Aux Questions
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Voir aussi
toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.

