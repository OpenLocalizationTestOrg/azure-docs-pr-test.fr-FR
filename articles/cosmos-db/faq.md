---
title: aaaAzure DB Cosmos Forum aux questions | Documents Microsoft
description: "Obtenir elles sonttrop des réponses aux questions sur Azure Cosmos DB, un service de base de données distribués internationalement, comportant plusieurs modèles. Découvrez la capacité, les niveaux de performances et la mise à l’échelle."
keywords: "Questions sur la base de données, Forum aux questions, documentdb, azure, Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>FAQ Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Notions fondamentales concernant Cosmos DB Azure
### <a name="what-is-azure-cosmos-db"></a>Qu’est-ce qu’Azure Cosmos DB ?
Azure Cosmos DB est un service de base de données multimodèle répliqué globalement, qui offre des requêtes enrichies sur des données sans schéma, aide à produire des performances configurables et fiables, et permet un développement rapide. Il est rendu possible par plateforme gérée qui est soutenue par une puissance de hello et la portée de Microsoft Azure. 

Base de données Azure Cosmos est hello bonne solution pour les jeux, mobile, web, et applications IoT lorsqu’un débit prévisible, une haute disponibilité, une faible latence et un modèle de données de schéma sont les exigences clés. Cette solution offre une flexibilité des schémas et une indexation riche. Elle inclut également une prise en charge transactionnelle multidocument avec JavaScript intégré. 

Pour plusieurs questions de base de données, les réponses et les instructions de déploiement et à l’aide de ce service, consultez hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Quelles tooDocumentDB s’est produit ?
Hello API DocumentDB est un des modèles d’API et les données hello pris en charge pour la base de données Azure Cosmos. De plus, Azure Cosmos DB met à votre disposition l’API Graph (préversion), l’API Table (préversion) et l’API MongoDB. Pour plus d’informations, voir [Questions des clients de DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Comment obtenir toomy compte DocumentDB Bonjour portail Azure ?
Bonjour portail Azure, cliquez sur l’icône de base de données Azure Cosmos hello dans le volet gauche de hello. Si vous avez un compte DocumentDB avant, vous avez maintenant un compte de base de données Azure Cosmos, avec aucune facturation tooyour de modification.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Quels sont les scénarios d’utilisation classiques hello pour la base de données Azure Cosmos ?
Azure Cosmos DB est un bon choix pour le nouveau jeu mobile, web, et les applications de IoT automatique de l’échelle, des performances prévisibles, fast ordre millisecondes de temps de réponse, alors que hello tooquery de capacité sur les données de schéma est important. Base de données Azure Cosmos prête toorapid développement et la prise en charge d’itération continue de hello application des modèles de données. Les applications qui gèrent du contenu et des données générés par l’utilisateur sont [des cas d’utilisation courants pour Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Comment Azure Cosmos DB offre-t-il des performances prévisibles ?
A [unité de demande](request-units.md) (RU) est la mesure de hello du débit dans la base de données Azure Cosmos. Un débit de 1-RU correspond débit toohello Hello GET d’un document de 1 Ko. Chaque opération dans Azure Cosmos DB, y compris les lectures, écritures, les requêtes SQL et exécutions de procédure stockée, a une valeur RU déterministe est basée sur hello débit requis toocomplete hello opération. Au lieu de penser à l’UC, à l’E/S et à la mémoire, ainsi qu’à la façon dont ces éléments affectent le débit de votre application, vous pouvez penser en termes de mesure de RU unique.

Vous pouvez réserver chaque conteneur Azure Cosmos DB avec un débit approvisionné en termes de RU de débit par seconde. Pour les applications de n’importe quelle échelle, vous pouvez du banc d’essai des requêtes individuelles toomeasure leurs valeurs ur et configurer un total de hello conteneur toohandle d’unités de demande pour toutes les requêtes. Vous pouvez également monter ou à l’échelle de débit de votre conteneur en fonction des besoins de votre evolve application hello. Pour plus d’informations sur les unités de demande et d’assistance pour déterminer votre conteneur a besoin, consultez [estimation des besoins de débit](request-units.md#estimating-throughput-needs) et essayez de hello [calculatrice de débit](https://www.documentdb.com/capacityplanner). terme de Hello *conteneur* fait ici référence toorefers tooa API DocumentDB collection, le graphique de l’API Graph, MongoDB API collection et table de l’API de Table. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Comment Azure Cosmos DB prend-il en charge différents modèles de données tels que clé/valeur, en colonnes, document et graphique ?

Clé/valeur (table), en colonnes, de document et les modèles sont tous pris en charge en raison de hello ARS (atomes, enregistrements et des séquences) concevoir cette base de données Azure Cosmos un graphique des données repose sur. Atomes, les enregistrements et les séquences peuvent être facilement mappées et prévue toovarious des modèles de données. Hello API pour un sous-ensemble de modèles sont disponible actuellement (DocumentDB, MongoDB, Table et API graphiques) et d’autres modèles de données spécifique tooadditional seront disponibles dans hello futures.

Base de données Azure Cosmos a un schéma indépendant du moteur d’indexation capable d’automatiquement l’indexation de toutes les données hello qu'il résultants sans schéma ou les index secondaires du développeur de hello. moteur de Hello s’appuie sur un ensemble de dispositions d’index logique (arborescence inversée, en colonnes,) qui découpler la disposition de stockage hello de sous-systèmes de traitement des requêtes et les index de hello. COSMOS DB également hello capacité toosupport un ensemble de protocoles de transmission et d’API de manière extensible et les traduire efficacement toohello base données modèle (1) et hello index logique dispositions (2) rend unique peut prendre en charge de plusieurs modèles de données en mode natif .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure Cosmos DB est-il conforme à la loi HIPAA ?
Oui, Azure Cosmos DB est conforme à la loi HIPAA. HIPAA établit les conditions requises pour hello utiliser, divulgation d’informations et la protection des informations d’intégrité identifiables de façon individuelle. Pour plus d’informations, consultez hello [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Quelles sont les limites de stockage hello de base de données Azure Cosmos ?
Il n’existe aucun montant toohello de limite de données un conteneur peut stocker dans la base de données Azure Cosmos.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Quelles sont les limites du débit de base de données Azure Cosmos hello ?
Il n’existe aucun montant total toohello de limite de débit sur un conteneur pouvant prendre en charge dans la base de données Azure Cosmos. Hello idée clée toodistribute votre charge de travail est à peu près uniformément entre un nombre suffisant de clés de partition.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Combien coûte Azure Cosmos DB ?
Pour plus d’informations, consultez toohello [base de données Azure Cosmos tarification](https://azure.microsoft.com/pricing/details/cosmos-db/) page. Frais d’utilisation de base de données Cosmos Azure sont déterminés par nombre hello de conteneurs approvisionnés, nombre hello d’heures de conteneurs de hello étaient en ligne et hello configuré débit pour chaque conteneur. terme de Hello *conteneurs* fait ici référence toohello API DocumentDB collection, le graphique de l’API Graph, MongoDB API collection et tables de l’API de Table. 

### <a name="is-a-free-account-available"></a>Un compte gratuit est-il disponible ?
Si vous êtes tooAzure nouveau, vous pouvez inscrire un [gratuitement un compte Azure](https://azure.microsoft.com/free/), ce qui vous donne des 30 derniers jours et et un tootry de crédit tous les services Azure de hello. Si vous avez un abonnement Visual Studio, vous pouvez également bénéficier de [libre crédits Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse sur tous les services Azure. 

Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) toodevelop et tester votre application localement pour libérer, sans créer un abonnement Azure. Lorsque vous êtes satisfait de la façon dont votre application fonctionne Bonjour Azure Cosmos DB émulateur, vous pouvez basculer toousing un compte de base de données Azure Cosmos dans le cloud de hello.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Comment puis-je obtenir une aide supplémentaire avec Azure Cosmos DB ?
Si vous avez besoin d’aide, atteindre toous sur [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb) ou hello [forum MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), ou planifier une conversation individuelle avec l’équipe d’ingénierie hello base de données Azure Cosmos en envoyant un message trop[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Configurer Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Comment s’inscrire pour Azure Cosmos DB ?
Base de données Azure Cosmos est disponible dans hello portail Azure. Tout d’abord, souscrivez un abonnement Azure. Une fois que vous avez inscrit, vous pouvez ajouter une API DocumentDB, l’API Graph (version préliminaire), les API de l’API de Table (version préliminaire) ou MongoDB compte tooyour abonnement Azure.

### <a name="what-is-a-master-key"></a>Qu'est-ce qu’une clé principale ?
Une clé principale est un tooaccess de jeton de sécurité de toutes les ressources d’un compte. Les personnes avec la clé de hello dispose de ressources de tooall accès en lecture et écriture dans le compte de base de données hello. Soyez prudent lorsque vous distribuez des clés principales. Hello principal la clé principale et secondaire clé principale sont disponibles sur hello **clés** Panneau de hello [portail Azure][azure-portal]. Pour plus d’informations sur les clés, consultez la rubrique [Affichage, copie et régénération de clés d’accès](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>Quelles sont les régions hello PreferredLocations pouvant être définies à ? 
Hello PreferredLocations valeur peut être définie tooany Hello Azure régions dans lesquels Cosmos DB est disponible. Pour obtenir la liste des régions disponibles, voir [Régions Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>Existe-t-il une que je dois être conscient lors de la distribution des données entre Bonjour via hello centres de données Azure ? 
Base de données Azure Cosmos est présent dans toutes les régions Azure, en tant que hello spécifié sur [régions Azure](https://azure.microsoft.com/regions/) page. Comme il est le service principal de hello, chaque nouveau centre de données a une présence de la base de données Azure Cosmos. 

Lorsque vous définissez une région, n’oubliez pas qu’Azure Cosmos DB respecte les clouds souverains et du secteur public. Autrement dit, si vous créez un compte dans une région souveraine, vous ne pouvez pas répliquer en dehors de cette région souveraine. De même, vous ne pouvez pas activer la réplication dans d’autres emplacements souverains à partir d’un compte externe. 

## <a name="develop-against-hello-documentdb-api"></a>Développer sur hello API DocumentDB

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>Comment commencer à développer par rapport à hello API DocumentDB ?
API DocumentDB de Microsoft est disponible dans hello [portail Azure][azure-portal]. Vous devez d’abord souscrire un abonnement Microsoft Azure. Une fois que vous vous inscrivez pour un abonnement Azure, vous pouvez ajouter les API DocumentDB conteneur tooyour abonnement Azure. Pour savoir comment ajouter un compte Azure Cosmos DB, consultez [Créer un compte de base de données Azure Cosmos DB](create-documentdb-dotnet.md#create-account). Si vous avez un compte DocumentDB Bonjour précédentes, vous avez maintenant un compte de base de données Azure Cosmos. 

[Kits de développement logiciel (SDK)](documentdb-sdk-dotnet.md) sont disponibles pour .NET, Python, Node.js, JavaScript et Java. Les développeurs peuvent également utiliser hello [RESTful HTTP API](/rest/api/documentdb/) toointeract avec des ressources de base de données Azure Cosmos à partir de différentes plateformes et langues.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>Puis-je accéder à certains tooget exemples prêts à l’emploi un point de départ ?
Exemples pour hello API DocumentDB [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), et [Python](documentdb-python-samples.md) kits de développement logiciel sont disponibles sur GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Est hello données de schéma API DocumentDB de base de données prise en charge ?
Oui, hello API DocumentDB permet d’applications toostore JSON des documents arbitraires sans indicateurs ou des définitions de schéma. Données sont immédiatement disponibles pour la requête via l’interface de requête SQL de base de données Azure Cosmos hello.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Hello API DocumentDB prend en charge les transactions ACID ?
Oui, hello API DocumentDB prend en charge les transactions entre documents exprimée sous la forme de déclencheurs et procédures stockées de JavaScript. Les transactions sont portée tooa à partition unique au sein de chaque collection et exécutée avec la sémantique ACID en tant que « tout ou rien, » isolé des autres requêtes d’utilisateur et le code qui s’exécutent simultanément. Si les exceptions sont levées à l’exécution de côté serveur hello du code JavaScript de l’application, toute transaction de hello est restaurée. Pour plus d’informations sur les transactions, consultez [Transactions de programme de base de données](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Qu'est-ce qu'une collection ?
Une collection consiste en un groupe de documents et la logique d’application JavaScript associée. Une collection est une entité facturable, où hello [coût](performance-levels.md) est déterminé par le débit de hello et de stockage utilisé. Collections peuvent s’étendre sur une ou plusieurs partitions ou des serveurs et peut évoluer toohandle quasi illimitée des volumes de stockage ou de débit.

Les collections sont également des entités de facturation hello pour la base de données Azure Cosmos. Chaque collection est facturée par heure, selon le débit approvisionné de hello et l’espace de stockage utilisé. Pour plus d’informations, consultez la [Tarification Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Comment créer une base de données ?
Vous pouvez créer des bases de données à l’aide de hello [portail Azure](https://portal.azure.com), comme décrit dans [ajouter une collection](create-documentdb-dotnet.md#create-collection), un des hello [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md), ou hello [l’API REST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Comment configurer des utilisateurs et des autorisations ?
Vous pouvez créer des utilisateurs et des autorisations à l’aide d’une des hello [Cosmos DB kits de développement logiciel API](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Hello API DocumentDB prend en charge SQL ?
Hello langage de requête SQL est un sous-ensemble amélioré des fonctionnalités de requête hello sont pris en charge par SQL. Hello langage de requête SQL de base de données Azure Cosmos fournit des opérateurs relationnelles et hiérarchiques enrichis et l’extensibilité via les fonctions de base de JavaScript, défini par l’utilisateur (UDF). Permet de grammaire JSON pour la modélisation des documents JSON en tant qu’arborescences de nœuds étiqueté, qui sont utilisés par les techniques d’indexation automatique de base de données Azure Cosmos hello et langage de requête SQL hello de base de données Azure Cosmos. Pour plus d’informations sur l’utilisation de grammaire SQL, consultez hello [QueryDocumentDB] [ query] l’article.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Est hello fonctions d’agrégation SQL API DocumentDB prise en charge ?
Hello API DocumentDB prend en charge l’agrégation de faible latence à n’importe quelle échelle via des fonctions d’agrégation `COUNT`, `MIN`, `MAX`, `AVG`, et `SUM` via hello grammaire SQL. Pour plus d’informations, consultez [Fonctions d’agrégation](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>Comment hello API DocumentDB ne fournit pas d’accès concurrentiel ?
Hello API DocumentDB prend en charge le contrôle d’accès concurrentiel optimiste (OCC) via les balises d’entité HTTP ou eTag. Toutes les ressources DocumentDB API ont un ETag et hello ETag est défini sur le serveur de hello chaque fois qu’un document est mis à jour. en-tête ETag de Hello et la valeur actuelle de hello sont inclus dans tous les messages de réponse. ETag utilisable avec hello If-Match en-tête tooallow hello server toodecide si une ressource doit être mis à jour. Hello, valeur de If-Match est toobe de valeur d’ETag hello vérifié. Si hello valeur ETag correspond au serveur de hello valeur ETag, les ressources hello sont mise à jour. Si hello ETag n’est plus en cours, hello rejette opération hello avec un « HTTP 412 Échec de la précondition « code de réponse. client de Hello ré-extrait puis hello ressource tooacquire hello valeur ETag actuelle pour la ressource de hello. En outre, ETags utilisable avec toodetermine d’en-tête If-None-Match hello si un récupérez de nouveau d’une ressource est nécessaire.

accès concurrentiel optimiste de toouse dans .NET, utilisez hello [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) classe. Pour voir un exemple .NET, [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) dans l’exemple de DocumentManagement hello sur GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Comment effectuer des transactions Bonjour API DocumentDB
Hello API DocumentDB prend en charge les transactions de langage-integrated via les procédures stockées de JavaScript et des déclencheurs. Toutes les opérations de base de données à l’intérieur des scripts sont exécutées en isolement de capture instantanée. Si elle est une collection à partition unique, l’exécution de hello est étendue toohello collection. Si la collection de hello est partitionnée, l’exécution de hello est étendue toodocuments avec hello même valeur de clé de partition dans la collection de hello. Un instantané hello de versions de document (ETags) est effectuée au début de hello de transaction de hello et validé uniquement si le script de hello réussit. Si hello JavaScript lève une erreur, hello transaction est restaurée. Pour plus d’informations, consultez [Programmation en JavaScript côté serveur pour Azure Cosmos DB](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Comment insérer des documents en bloc dans Cosmos DB ?
Vous pouvez insérer en bloc des documents dans Azure Cosmos DB de deux manières :

* Hello outil de migration, comme décrit dans [outil de migration de base de données pour la base de données Azure Cosmos](import-data.md).
* Avec des procédures stockées, comme décrit dans [Programmation en JavaScript côté serveur pour Azure Cosmos DB](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Hello API DocumentDB prend en charge la mise en cache de lien de ressource ?
Oui. Azure Cosmos DB étant un service RESTful, les liens de ressource sont immuables et peuvent être mis en cache. Les clients de API DocumentDB peuvent spécifier un en-tête « If-None-Match » pour les lectures sur n’importe quel document du type de ressource ou de la collection, puis mettre à jour leurs copies locales après que la version de serveur hello a changé.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>Une instance locale de l’API DocumentDB est-elle disponible ?
Oui. Hello [Azure Cosmos DB émulateur](local-emulator.md) fournit une émulation haute fidélité de hello service Cosmos DB. Il prend en charge la fonctionnalité tooAzure identiques Cosmos DB, y compris la prise en charge pour la création et l’interrogation de documents JSON, l’approvisionnement et de mise à l’échelle des collections et l’exécution de procédures stockées et déclencheurs. Vous pouvez développer et tester des applications à l’aide de hello Azure Cosmos DB émulateur et les déployer tooAzure à une échelle globale en effectuant une seule configuration à modifier le point de terminaison de connexion toohello pour la base de données Azure Cosmos.

## <a name="develop-against-hello-api-for-mongodb"></a>Développer sur hello API pour MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>Nouveautés hello API de base de données Azure Cosmos pour MongoDB
Hello API de base de données Azure Cosmos pour MongoDB est une couche de compatibilité qui permet des applications tooeasily et en toute transparence communique avec le moteur de base de données base de données Azure Cosmos hello natif à l’aide de l’existant, pris en charge par une Communauté Apache MongoDB APIs et les pilotes. Les développeurs peuvent désormais utiliser MongoDB outil des chaînes et des compétences toobuild applications existantes qui tirent parti de la base de données Azure Cosmos. Les développeurs bénéficient de fonctionnalités unique hello de base de données Azure Cosmos, qui incluent la maintenance de l’indexation d’automatique, la sauvegarde, contrats de niveau de service assuré (SLA) et ainsi de suite.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Comment se connecter toomy API de base de données MongoDB ?
Hello toohello de tooconnect moyen le plus rapide API de base de données Azure Cosmos pour MongoDB est toohead sur toohello [portail Azure](https://portal.azure.com). Accédez tooyour compte et, dans le menu de navigation gauche hello, cliquez sur **Quick Start**. Démarrage rapide est hello meilleure manière tooget code des extraits de code tooconnect tooyour base de données. 

Azure Cosmos DB applique des normes et des exigences strictes en matière de sécurité. Comptes Cosmos DB Azure requérir l’authentification et une communication sécurisée via SSL, soyez sûr de toouse TLSv1.2.

Pour plus d’informations, consultez [connecter tooyour des API de base de données MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Existe-t-il des codes d’erreur supplémentaires pour une API de base de données MongoDB ?
En outre toohello MongoDB codes d’erreur courants, hello MongoDB API comprend ses propres codes d’erreur spécifiques :


| Error               | Code  | Description  | Solution  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | Nombre total de Hello d’unités de demande consommée a dépassé les taux d’unité de demande configuré hello pour collection de hello et a été limitée. | Envisagez de mise à l’échelle de débit hello de collection hello hello portail Azure ou réessayer. |
| ExceededMemoryLimit | 16501 | Tant que service mutualisé, opération de hello a dépassé les unités de mémoire du client hello. | Réduire la portée hello d’opération hello via les critères de requête plus restrictives ou contactez le support de hello [portail Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>*Exemple : &nbsp;&nbsp;&nbsp;&nbsp;db.getCollection(’users’).aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Développer avec hello API de Table (version préliminaire)

### <a name="terms"></a>Termes 
Bonjour Azure Cosmos DB : API de Table (version préliminaire) fait référence offre premium de toohello par base de données Azure Cosmos pour la prise en charge de table annoncé au Build 2017. 

table de standard de Hello SDK est la table de stockage Azure existant hello Kit de développement logiciel. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Comment puis-je utiliser nouvelle offre de l’API de Table (version préliminaire) hello ? 
Hello API de Table de base de données Azure Cosmos est disponible dans hello [portail Azure][azure-portal]. Vous devez d’abord souscrire un abonnement Microsoft Azure. Une fois que vous avez inscrit, vous pouvez ajouter un tooyour de compte d’API de Table de base de données Azure Cosmos abonnement Azure et puis ajoutez le compte tooyour de tables. 

Pendant la période d’évaluation hello, lorsque [kits de développement logiciel](../cosmos-db/table-sdk-dotnet.md) sont disponibles pour .NET, vous pouvez commencer en effectuant hello [Table API](../cosmos-db/create-table-dotnet.md) article de démarrage rapide.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>Ai-je besoin d’un nouveau Bonjour de toouse SDK API (version préliminaire) de la Table ? 
Oui, hello [stockage Premium Table de Windows Azure (aperçu) SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) est disponible sur NuGet. Informations supplémentaires sont disponibles sur hello [Azure Cosmos DB Table Api.net : télécharger et notes de publication](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) page. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Comment pour fournir des commentaires sur hello SDK ou des bogues ?
Vous pouvez partager vos commentaires dans un des hello suivant façons :

* [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Forum MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Quelle est la chaîne de connexion hello que vous avez besoin de toouse tooconnect toohello API (version préliminaire) de la Table ?
chaîne de connexion Hello est la suivante :
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Vous pouvez obtenir la chaîne de connexion hello à partir de la page de clés hello Bonjour portail Azure. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Comment remplacer les paramètres de configuration hello pour les options de requête hello dans hello nouvelle Table API (version préliminaire) ?
Pour plus d’informations sur les paramètres de configuration, voir [Fonctionnalités d’Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Vous pouvez modifier les paramètres de hello en les ajoutant tooapp.config dans la section appSettings hello dans l’application cliente de hello.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Existe-t-il des modifications pour les clients qui utilisent une table standard existante hello Kit de développement logiciel ?
Aucune. Il n’y a aucune modification pour les clients existants ou nouveaux qui sont à l’aide de table standard existante hello SDK. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Comment afficher les données de table qui sont stockées dans la base de données Azure Cosmos pour une utilisation avec hello API (révision) de la Table ? 
Vous pouvez utiliser les données de salutation hello toobrowse portail Azure. Vous pouvez également utiliser hello code de l’API de Table (version préliminaire) ou les outils hello mentionnés dans la réponse suivante hello. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Outils qui fonctionnent avec hello API (version préliminaire) de la Table ? 
Vous pouvez utiliser hello ancienne version de l’Explorateur Windows Azure (0.8.9).

Les outils avec hello flexibilité tootake est une chaîne de connexion dans un format hello spécifié précédemment peut prendre en charge hello nouvelle Table API (version préliminaire). Une liste des outils de table est fournie sur hello [outils clients de stockage Azure](../storage/common/storage-explorers.md) page. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell ou CLI d’Azure fonctionnent avec hello nouvelle Table API (version préliminaire) ?
Nous prévoyons de tooadd prend en charge de PowerShell et CLI d’Azure Table API (version préliminaire). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>Est de concurrence de hello sur les opérations contrôlées ?
Oui, l’accès concurrentiel optimiste est fournie via l’utilisation hello du mécanisme d’ETag hello. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>Est hello modèle de requête OData pris en charge pour les entités ? 
Oui, hello API (version préliminaire) de la Table prend en charge la requête OData et requête LINQ. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>Puis-je connecter toohello table Azure standard et premium nouvelle API de Table (version préliminaire) côte à côte dans hello hello même application ? 
Oui, vous pouvez vous connecter en créant deux instances distinctes de hello CloudTableClient, chacune pointant tooits propre URI via la chaîne de connexion hello.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Comment migrer une existant Azure Table application toothis nouvelle offre de stockage ?
avantage tootake de nouvelle offre de Table API hello sur vos données de stockage de Table existantes, contactez [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Quelle est la feuille de route hello pour ce service, et lorsque vous proposera autres fonctionnalités d’API de Table standard ?
Nous prévoyons de tooadd en charge SAS jetons, ServiceContext, statistiques, Client côté chiffrement, Analytique et autres fonctionnalités que nous progressons vers la disponibilité générale. Vous pouvez formuler des commentaires sur [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>Comment est expansion de fait pour ce service, si, par exemple, je commence par la taille de stockage hello  *n*  Go de données et mes données augmentera too1 to au fil du temps ? 
Base de données Azure Cosmos est conçue tooprovide stockage illimité via l’utilisation de hello de mise à l’échelle horizontale. service de Hello peut surveiller et efficacement augmenter le stockage. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Comment surveiller les offre des API (version préliminaire) de la Table hello ?
Vous pouvez utiliser des API (version préliminaire) de la Table de hello **métriques** volet toomonitor demandes et l’utilisation du stockage. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>Comment calculer le débit hello que j’ai besoin ?
Vous pouvez utiliser Bonjour capacité estimateur toocalculate Bonjour TableThroughput qui est requis pour les opérations de hello. Pour plus d’informations, voir [Estimer les unités de requête et le stockage de données](https://www.documentdb.com/capacityplanner). En général, vous pouvez représenter votre entité au format JSON et spécifiez des numéros de hello pour vos opérations. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>Puis-je utiliser la fonctionnalité hello nouvelle Table API (version préliminaire) SDK localement avec l’émulateur de hello ?
Oui, vous pouvez utiliser hello API (version préliminaire) de la Table avec l’émulateur local de hello lorsque vous utilisez hello nouveau SDK. émulateur de nouveau toodownload, accédez trop[hello utilisation Azure Cosmos DB émulateur pour développement local et le test](local-emulator.md). Hello valeur StorageConnectionString dans app.config doit toobe :

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>Mon application existante peut fonctionner avec hello API (version préliminaire) de la Table ? 
Hello surface d’exposition de hello nouvelle Table API (version préliminaire) est compatible avec hello existant d’une table standard Azure SDK sur hello créer, supprimer, mettre à jour et opérations de requête Bonjour API .NET. Assurez-vous que vous disposez d’une clé de ligne, car hello API de Table (version préliminaire) nécessite une clé de partition et une clé de ligne. Nous prévoyons également tooadd SDK prise en charge que nous progressons vers la disponibilité générale de cette offre de service.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>Dois-je toomigrate me toohello des applications Azure basé sur une table existante nouveau SDK si je ne souhaite pas les fonctionnalités de l’API de Table (version préliminaire) toouse hello ?
Non, vous pouvez créer et utiliser des ressources de table standard existantes sans la moindre interruption. Toutefois, si vous n’utilisez pas hello nouvelle Table API (version préliminaire), vous ne peut pas tirer parti des index automatique de hello, option supplémentaire de la cohérence de hello ou distribution globale. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Comment ajouter la réplication des données de hello dans premium hello API (version préliminaire) de la Table dans plusieurs régions Azure ?
Vous pouvez utiliser du portail de base de données Azure Cosmos hello [les paramètres de réplication globale](tutorial-global-distribution-documentdb.md#portal) tooadd les régions qui sont adaptées à votre application. toodevelop une application distribuée globalement, vous devez également ajouter votre application avec hello PreferredLocation informations ensemble toohello région permettant la faible latence de lecture. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Évolution de la région principal écriture hello compte hello dans premium de hello API de Table (version préliminaire)
Vous pouvez utiliser des hello Azure Cosmos DB global de réplication portail volet tooadd une région et basculez ensuite la région toohello requis. Pour des instructions, voir [Développement avec des comptes Azure Cosmos DB multirégions](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Comment configurer mes régions de lecture préférées pour une faible latence lors de la distribution de mes données ? 
toohelp lire à partir de l’emplacement local de hello, utilisez des clé de PreferredLocation hello dans le fichier app.config hello. Pour les applications existantes, hello API de Table (version préliminaire) génère une erreur si LocationMode est défini. Supprimez ce code, car les premium hello API de Table (version préliminaire) récupère ces informations à partir du fichier app.config de hello. Pour plus d’informations, voir [Fonctionnalités d’Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Comment dois-je réfléchir les niveaux de cohérence dans hello API (version préliminaire) de la Table ? 
Azure Cosmos DB adopte des compromis bien pensés entre cohérence, disponibilité et latence. Azure Cosmos DB propose cinq niveaux de cohérence à tooTable développeurs d’API (version préliminaire), afin de pouvoir choisir modèle de cohérence droite hello au niveau de table hello et effectuer des demandes individuelles lors de l’interrogation des données de salutation. Quand un client se connecte, il peut spécifier un niveau de cohérence. Vous pouvez modifier le niveau de hello via le paramètre de app.config hello pour hello de valeur de clé de TableConsistencyLevel hello. 

Hello API de Table (aperçu) fournit à faible latence lit avec « lire vos propres écritures, » avec la cohérence de Session en tant que valeur par défaut hello. Pour plus d’informations, consultez [Niveaux de cohérence](consistency-levels.md). 

Par défaut, le stockage Azure Table fournit une cohérence forte dans une région et cohérence Eventual dans les sites secondaires hello. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Azure Cosmos DB offre-t-il davantage de niveaux de cohérence que des tables standard ?
Oui, pour savoir comment toobenefit de hello distribuées la nature de la base de données Azure Cosmos, consultez [niveaux de cohérence](consistency-levels.md). Étant donné que les garanties sont fournies pour les niveaux de cohérence hello, vous pouvez les utiliser en toute confiance. Pour plus d’informations, voir [Fonctionnalités d’Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>Lors de la distribution globale est activée, combien de temps faut-il tooreplicate les données de salutation ?
Nous de valider les données hello durablement dans la région de hello et push hello tooother régions de données immédiatement une question de millisecondes. Cette réplication dépend uniquement délai hello aller-retour (RTT) de centre de données hello. toolearn savoir plus sur la fonctionnalité de distribution globale hello de base de données Azure Cosmos, consultez [base de données Azure Cosmos : un service de base de données distribuée globalement sur Azure](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Niveau de cohérence hello demande de lecture peut être modifié ?
Avec la base de données Azure Cosmos, vous pouvez définir le niveau de cohérence hello au niveau du conteneur hello (sur la table de hello). À l’aide de hello SDK, vous pouvez modifier le niveau de hello en fournissant la valeur de hello pour la clé TableConsistencyLevel dans le fichier app.config hello. Hello les valeurs possibles sont : Strong, Bounded Staleness, Session, le préfixe cohérent et Eventual. Pour plus d’informations, voir [Niveaux de cohérence ajustables dans Azure Cosmos DB](consistency-levels.md). idée de clé Hello est que vous ne peut pas définir la cohérence de demande hello niveau en plus de paramètre hello pour la table de hello. Par exemple, vous Impossible de définir le niveau de cohérence hello pour table hello à Eventual et niveau de cohérence hello demande à fort. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Comment compte de l’API de Table (version préliminaire) premium hello gérer basculement si une région tombe en panne ? 
premium de Hello emprunte par API (version préliminaire) de la Table à partir de la plateforme de distribués internationalement hello de base de données Azure Cosmos. tooensure que votre application peut tolérer un temps mort du centre de données, activez au moins une région plus compte hello dans le portail de base de données Azure Cosmos hello [développement avec les comptes de base de données Azure Cosmos multizone](regional-failover.md). Vous pouvez définir la priorité de hello de région de hello à l’aide du portail de hello [développement avec les comptes de base de données Azure Cosmos multizone](regional-failover.md). 

Vous pouvez ajouter des régions autant que nécessaire pour le compte de hello et contrôler où il peut basculer tooby en fournissant une priorité de basculement. Bien entendu, base de données toouse hello, vous devez trop tooprovide une application. Si vous procédez de la sorte, vos clients ne subissent aucun temps d’arrêt. le client Hello Kit de développement logiciel est automatiquement changement de site associé. Autrement dit, il peut détecter région hello qui est arrêté et un basculement automatique toohello nouvelle zone.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Premium de hello API (version préliminaire) de la Table est activée pour les sauvegardes ?
Oui, premium de hello API (version préliminaire) de la Table emprunte à partir de la plateforme hello de base de données Azure Cosmos pour les sauvegardes. Les sauvegardes sont effectuées automatiquement. Pour plus d’informations, voir [Sauvegarde et restauration en ligne automatiques avec Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hello API (version préliminaire) de la Table d’index tous les attributs d’une entité par défaut ?
Oui, tous les attributs d’une entité sont indexés par défaut. Pour plus d’informations, voir [Comment Azure Cosmos DB indexe-t-il les données ?](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Cela signifie-t-il que je n’ai pas toocreate plusieurs requêtes de hello toosatisfy index ? 
Oui, Azure Cosmos DB assure l’indexation automatique de tous les attributs sans aucune définition de schéma. Cette automatisation libère les développeurs toofocus sur application hello plutôt que sur la gestion et la création d’index. Pour plus d’informations, voir [Comment Azure Cosmos DB indexe-t-il les données ?](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>Puis-je modifier stratégie d’indexation hello ?
Oui, vous pouvez modifier la stratégie d’indexation hello en fournissant la définition d’index hello. Pour plus d’informations, voir [Fonctionnalités d’Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Vous devez tooproperly encoder et les paramètres hello de séquence d’échappement. 

Json au format de chaîne dans le fichier app.config hello :
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Base de données Azure Cosmos en tant que plateforme semble toohave de nombreuses fonctionnalités, telles que le tri, les agrégats, hiérarchie et autres fonctionnalités. Vous ajouterez ces toohello fonctions API de Table ? 
Dans l’aperçu, hello Table API fournit hello même fonctionnalité en tant que stockage de Table Azure de la requête. Azure Cosmos DB prend également en charge le tri, les agrégats, les requêtes géospatiales, les hiérarchies et un large éventail de fonctions intégrées. Nous fournirons des fonctionnalités supplémentaires dans hello API de Table dans une mise à jour future du service. Pour plus d’informations, consultez [Requêtes SQL pour l’API DocumentDB Azure Cosmos DB](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Quand dois-je modifier TableThroughput pourquoi l’API de Table (aperçu) ?
Vous devez modifier TableThroughput lorsqu’une des conditions suivantes de hello s’applique :
* Il s’agit d’une extraction, transformation et chargement (ETL) de données, ou vous souhaitez tooupload une grande quantité de données dans un laps de temps. 
* Vous avez besoin de plus de débit à partir du conteneur de hello back-end hello. Par exemple, vous voyez que le débit hello utilisée est supérieure au débit approvisionné de hello, et vous sont obtention d’accélérée. Pour plus d’informations, consultez [Définir le débit des conteneurs Azure Cosmos DB](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>Puis-je monter ou mettre à l’échelle vers le bas débit hello de mon tableau de l’API de Table (version préliminaire) ? 
Oui, vous pouvez utiliser le débit hello tooscale du portail de base de données Azure Cosmos hello échelle volet. Pour plus d’informations, voir [Définir le débit](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Un débit de table (TableThroughput) par défaut est-il défini pour les nouvelles tables approvisionnées ?
Oui, si vous ne substituez pas hello TableThroughput via app.config et que vous n’utilisez pas un conteneur créé au préalable dans la base de données Azure Cosmos, service de hello crée une table avec un débit de 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>Existe-t-il des toute modification de tarification pour les clients existants de l’API de Table standard hello ?
Aucune. Le tarif reste inchangé pour les clients existants de l’API Table standard. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Comment les prix de hello est calculé pour hello API (version préliminaire) de la Table ? 
les prix Hello dépend hello allouée TableThroughput. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Comment pour gérer toute limitation sur les tables hello dans l’API de Table (version préliminaire) offre ? 
Si les taux de demandes hello dépasse la capacité de hello de débit approvisionné de hello pour conteneur sous-jacent de hello, vous obtiendrez une erreur et hello SDK réessaiera hello appel en appliquant la stratégie de nouvelle tentative hello.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Pourquoi dois-je toochoose un débit en dehors de PartitionKey et RowKey parti tootake d’offre de l’API de Table (version préliminaire) hello premium de base de données Azure Cosmos ?
Base de données Azure Cosmos définit un débit par défaut pour votre conteneur si vous ne fournissez pas un fichier app.config de hello. 

Azure Cosmos DB fournit des garanties de performances et de latence avec des limites supérieures pour les opérations. Cette garantie n’est possible lorsque le moteur de hello peut appliquer la gouvernance sur les opérations du client hello. TableThroughput garantit que vous obtenez hello garantie de débit et la latence, étant donné que plateforme de hello réserve la capacité et garantit la réussite opérationnel. 

À l’aide de spécification de débit hello, vous pouvez façon élastique toobenefit le modifier à partir de la saisonnalité hello de votre application, répondre aux besoins de débit hello et réduire les coûts.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>SDK de stockage Azure a été très peu coûteux pour moi, car j’acquiers uniquement les données toostore hello et rarement interroger. nouvelle offre de base de données Azure Cosmos Hello semble toobe me charge même si je n'ai pas effectuée une seule transaction ou stockées quoi que ce soit. Pouvez-vous m’en expliquer la raison ?

Base de données Azure Cosmos est conçue toobe un système basé sur le contrat SLA distribué globalement les garanties de disponibilité, la latence et débit. Lorsque vous réservez un débit de base de données Azure Cosmos, il est garanti, contrairement à d’autres systèmes de débit hello. Azure Cosmos DB offre des fonctionnalités supplémentaires qui ont été demandées par les clients, telles que les index secondaires et la distribution globale. Pendant la période d’évaluation hello, nous fournissons un modèle optimisées sur le débit et, finalement, nous prévoyons tooprovide un toomeet de modèle de stockage optimisé nos clients. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Je ne reçois jamais de notification de « quota complet » (indiquant qu’une partition est pleine) lorsque j’ingère des données dans un stockage Table. Avec hello API de Table (version préliminaire), j’obtiens ce message. Cela offre de limitation me et forcer me toochange mon application existante ?

Azure Cosmos DB est un système basé sur un contrat de niveau de service (SLA) permettant une mise à l’échelle illimitée, avec des garanties en matière de latence, de débit, de disponibilité et de cohérence. tooensure garantie de performances de premium, assurez-vous que votre taille de données et les index sont gérable et évolutive. limite de 10 Go Hello nombre hello d’entités ou d’éléments par clé de partition est tooensure que nous fournir de bonnes performances de recherche et de requête. tooensure que votre application évolue bien, même pour le stockage Azure, il est recommandé que vous *pas* créer une partition à chaud à stocker toutes les informations dans une seule partition et en interrogeant ce. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>Afin de PartitionKey et RowKey sont toujours requises avec hello nouvelle Table API (version préliminaire) ? 
Oui. Hello surface d’exposition de hello API (version préliminaire) de la Table étant similaires toothat Hello SDK le stockage de Table, la clé de partition hello fournit un moyen efficace toodistribute hello de données. clé de ligne Hello est unique dans cette partition. Hello ligne toobe de clé besoins présents et ne peut pas être null, en tant que Kit de développement standard de hello. la longueur de RowKey Hello est de 255 octets et la longueur de PartitionKey hello est 100 octets (bientôt toobe augmenté too1 Ko). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Quels sont les messages d’erreur hello pour hello API (version préliminaire) de la Table ?
Étant donné que cette version d’évaluation est compatible avec la table standard de hello, la plupart des erreurs de hello mappera toohello des erreurs de table standard de hello. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Pourquoi obtenir limitation lors de lot toocreate de tables une après l’autre dans hello API (version préliminaire) de la Table ?
Azure Cosmos DB est un système basé sur un contrat de niveau de service (SLA) qui offre des garanties en matière de latence, de débit, de disponibilité et de cohérence. S’agissant d’un système configuré, il réserve ressources tooguarantee ces exigences. taux rapide Hello de création de tables est détectée et limitée. Nous vous recommandons d’examiner les taux de hello de création de tables et de réduire accessible sans à 5 par minute. N’oubliez pas que hello API (version préliminaire) de la Table est un système configuré. moment de Hello vous mettre en service, vous allez d’abord toopay pour celle-ci. 

## <a name="develop-against-hello-graph-api-preview"></a>Développer sur hello l’API Graph (version préliminaire)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Comment puis-je appliquer des fonctionnalités de l’API Graph (version préliminaire) tooAzure Cosmos DB hello ?
Vous pouvez utiliser une extension bibliothèque tooapply hello des fonctionnalités de l’API Graph (version préliminaire). Cette bibliothèque nommée Microsoft Azure AD Graph est disponible sur NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Il semble que vous prennent en charge la langue de parcours hello GREMLINE graphique. Prévoyez-vous tooadd plusieurs formes de requête ?
Oui, nous prévoyons de tooadd autres mécanismes pour la requête Bonjour futures. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Comment puis-je utiliser nouvelle offre de l’API Graph (version préliminaire) hello ? 
hello démarré, effectuez de tooget [API Graph](../cosmos-db/create-graph-dotnet.md) article de démarrage rapide.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Questions des clients de DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Raison pour laquelle vous déplacez tooAzure Cosmos DB ? 

Base de données Azure Cosmos représente hello suivant big en distribuée globalement, bases de données de cloud à grande échelle. Comme un client de DocumentDB, vous avez maintenant accès toohello révolutionnaire système et les fonctionnalités offertes par la base de données Azure Cosmos.

Base de données Azure Cosmos démarré en tant que « Projet Florence » dans les points faibles de hello 2010 tooaddress rencontrés par les développeurs à créer des applications à grande échelle à l’intérieur de Microsoft. défis Hello de création d’applications distribuées globalement n’étant pas tooMicrosoft unique, nous avons apporté hello première génération de cette technologie disponible dans 2015 tooAzure développeurs sous forme de hello d’Azure DocumentDB. 

Depuis, nous avons ajouté de nouvelles fonctionnalités et introduit de nouvelles possibilités significatives. Base de données Azure Cosmos résulte hello. Dans le cadre de cette publication, les clients DocumentDB (et leurs données) sont devenus, automatiquement et en toute fluidité, des clients Azure Cosmos DB. Ces fonctionnalités sont dans des domaines de hello de moteur de base de données principal hello, ainsi que distribution globale, l’évolutivité élastique et contrats SLA de pointe et complète. Plus précisément, nous avons évolué cartographie tooefficiently du moteur de base de données hello Azure Cosmos DB tous les modèles de données courants, les systèmes de type et les API toohello modèle de données sous-jacent de la base de données Azure Cosmos. 

Bonjour actuelle manifestation orientée développeur de ce travail est hello prise en charge de [GREMLINE](../cosmos-db/graph-introduction.md) et [API de stockage de Table](../cosmos-db/table-introduction.md). Et il s’agit simplement hello début. Nous prévoyons de tooadd autres API populaires et les modèles de données plus récentes dans le temps, avec plus avancées en matière de performances et de stockage à une échelle globale. 

Il est important toopoint out que hello DocumentDB [dialecte SQL](../documentdb/documentdb-sql-query.md) a toujours été simplement un des hello plusieurs API que hello des base de données Azure Cosmos sous-jacent peut prendre en charge. Pour les développeurs qui utilisent un service entièrement géré comme base de données Azure Cosmos hello uniquement interface toohello service est hello API qui est exposées par le service de hello. Rien ne change réellement pour les clients DocumentDB existants. Dans la base de données Azure Cosmos, vous obtenez exactement les hello que SQL même API que DocumentDB offre. Et maintenant (et Bonjour ultérieure), vous pouvez accéder à d’autres fonctionnalités précédemment inaccessibles 

Lorsqu’une autre de notre travail permanent est foundation hello étendu pour une évolutivité globale et élastique de débit et de stockage. Sous-système de distribution globale toohello, nous avons apporté plusieurs améliorations fondamentale. Hello de telles fonctionnalités orientée développeur est hello préfixe cohérent modèle de cohérence, ce qui en fait un total cinq modèles de cohérence bien définis. Nous publierons beaucoup plus de fonctionnalités intéressantes à mesure qu’elles arriveront à maturité. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>Comment dois-je tooensure toodo que mes ressources DocumentDB continueront toorun sur la base de données Azure Cosmos ?

Vous ne devez toomake aucune modification du tout. Vos ressources DocumentDB sont désormais des ressources de base de données Azure Cosmos, et aucune interruption de service de hello est produite lors de cette opération s’est produite.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>Opérations de modifications nécessaire toomake pour mon toowork application avec la base de données Azure Cosmos ?

Il n’y a aucune toomake de modifications. Les classes, les espaces de noms et les noms de package NuGet n’ont pas changé. Comme toujours, nous vous recommandons de conserver vos kits de développement logiciel des parti de tootake toodate de hello dernières fonctionnalités et améliorations. 

### <a name="whats-changed-in-hello-azure-portal"></a>Nouveautés dans hello portail Azure ?

DocumentDB n’apparaît plus dans le portail de hello comme un service Azure. À la place est une nouvelle icône de base de données Azure Cosmos, comme indiqué dans hello suivant l’image. Toutes vos collections sont disponibles comme auparavant, et vous pouvez toujours mettre à l’échelle le débit, modifier les niveaux de cohérence et analyser les contrats SLA. fonctionnalités de Hello de l’Explorateur de données (version préliminaire) ont été améliorées. Vous pouvez désormais afficher et modifier des documents, créer et exécuter des requêtes et avec des procédures stockées, des déclencheurs et des UDF de travail à partir d’une seule page, comme indiqué dans hello suivant image : 

![Panneau de Collections de base de données Azure Cosmos Hello](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Existe-t-il des modifications toopricing ?

Non, coût hello en cours d’exécution de votre application de base de données Azure Cosmos est hello même qu’avant.

### <a name="are-there-changes-toohello-slas"></a>Existe-t-il des modifications toohello SLA ?

Non, hello SLA de disponibilité, la cohérence, la latence et débit sont identiques et sont toujours affichées dans le portail de hello. Pour plus d’informations, voir [SLA pour Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![Application To-Do avec exemples de données](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
