---
title: "aaaAzure Cosmos DB échelle et les tests de performances | Documents Microsoft"
description: "Découvrez comment tooperform l’échelle et test des performances avec la base de données Azure Cosmos"
keywords: Tester les performances
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Test des performances et de la mise à l’échelle avec Azure Cosmos DB
Le test des performances et de la mise à l’échelle est une étape essentielle du développement d’applications. Pour de nombreuses applications, couche de base de données hello a un impact significatif hello les performances globales et l’évolutivité, et est par conséquent, un composant essentiel de performances de test. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) a été spécialement conçu pour une mise à l’échelle élastique et des performances prévisibles et, par conséquent, convient parfaitement aux applications nécessitant un niveau de base de données hautes performances. 

Cet article est une référence pour les développeurs implémentant des suites de tests de performances pour leurs charges de travail Cosmos DB ou évaluant Cosmos DB pour des scénarios d’applications hautes performances. Il se concentre essentiellement sur les tests de performances isolé de base de données hello, mais il inclut également les meilleures pratiques pour les applications de production.

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :   

* Où puis-je trouver un exemple d’application cliente .NET pour le test des performances de Cosmos DB ? 
* Comment atteindre des niveaux de débit élevés avec Cosmos DB à partir de mon application cliente ?

tooget a démarré avec le code, téléchargez projet à partir de hello [exemple de test de Performance Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> Hello cette application vise toodemonstrate meilleures pratiques pour l’extraction de meilleures performances en dehors de la base de données Cosmos avec un petit nombre d’ordinateurs clients. Cela a été pas de capacité de pointe hello toodemonstrate du service de hello, qui peut mettre à l’échelle limitlessly.
> 
> 

Si vous recherchez des options de configuration côté client tooimprove Cosmos DB performances, consultez [conseils relatifs aux performances de base de données Azure Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Exécuter l’application de test de performance de hello
Hello tooget de manière plus rapide démarré est toocompile et exécution hello, exemple .NET ci-dessous, comme décrit dans les étapes de hello ci-dessous. Vous pouvez également consulter le code source de hello et implémenter des applications client propre tooyour configurations similaires.

**Étape 1 :** projet hello de téléchargement à partir de [exemple de test de Performance Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), ou le référentiel GitHub branchement hello.

**Étape 2 :** modifier les paramètres de hello pour EndpointUrl, AuthorizationKey, CollectionThroughput et DocumentTemplate (facultatif) dans le fichier App.config.

> [!NOTE]
> Avant de configurer des regroupements avec un débit élevé, reportez-vous à toohello [Page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate les coûts de hello par collection. Base de données Azure Cosmos facture débit indépendamment de toutes les heures et de stockage afin de conserver les coûts en supprimant ou en diminuant le débit de vos collections de base de données Azure Cosmos hello après le test.
> 
> 

**Étape 3 :** compiler et exécuter l’application de console hello à partir de la ligne de commande hello. Sortie hello suivante doit s’afficher :

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Étape 4 (si nécessaire) :** hello débit signalé (ur/s) à partir de l’outil de hello doit être hello identique ou supérieur à débit approvisionné de hello de collection de hello. Si ce n’est pas le cas, croissant hello DegreeOfParallelism par petits incréments peut-être vous aider à atteindre la limite de hello. Si des plateaux débit hello à partir de votre application cliente, lancer plusieurs instances de l’application hello sur hello identiques ou différents ordinateurs vous aideront à atteindre la limite de hello configuré sur hello différentes instances. Si vous avez besoin d’aide pour cette étape, veuillez écrire un message électronique tooaskcosmosdb@microsoft.com ou le fichier d’un ticket de support à partir de hello [Azure Portal](https://portal.azure.com).

Une fois que vous avez application hello en cours d’exécution, vous pouvez essayer différents [stratégies d’indexation](indexing-policies.md) et [niveaux de cohérence](consistency-levels.md) toounderstand leur impact sur le débit et la latence. Vous pouvez également consulter le code source de hello et implémenter similaire configurations tooyour propre des suites de tests ou les applications de production.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, nous avons vu comment effectuer des tests de performances et d’évolutivité avec Cosmos DB à l’aide d’une application console .NET. Consultez les liens toohello ci-dessous pour plus d’informations sur l’utilisation de base de données Azure Cosmos.

* [Exemple de test des performances Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Client configuration options tooimprove les performances de base de données Azure Cosmos](performance-tips.md)
* [Guide de partitionnement et de mise à l’échelle dans Azure Cosmos DB](partition-data.md)


