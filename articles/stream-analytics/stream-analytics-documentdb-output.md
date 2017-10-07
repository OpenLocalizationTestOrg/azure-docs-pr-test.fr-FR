---
title: "sortie d’aaaJSON pour les flux de données Analytique | Documents Microsoft"
description: "Découvrez comment Stream Analytics peut cibler Azure Cosmos DB pour la sortie JSON à des fins d’archivage des données et d’exécution de requêtes à faible latence sur des données JSON non structurées."
keywords: Sortie JSON
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Cibler Azure Cosmos DB pour la sortie JSON à partir de Stream Analytics
Stream Analytics peut cibler [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) pour la sortie JSON, ce qui permet d’archiver des données et d’exécuter des requêtes à faible latence sur des données JSON non structurées. Ce document traite certaines meilleures pratiques recommandées pour l’implémentation de cette configuration.

Pour ceux qui ne sont pas familiarisés avec la base de données Cosmos, examinons [cursus Azure Cosmos DB](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget a démarré. 

Remarque : L’API Mongo DB basée sur les collections Cosmos DB n’est pas prise en charge actuellement. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Principes de base de Cosmos DB en tant que cible de sortie
Hello sortie de base de données Azure Cosmos dans le flux de données Analytique qui permet d’écrire votre flux de traitement des résultats en tant que sortie JSON dans vos collections de base de données Cosmos. Flux de données Analytique ne crée pas de collections dans votre base de données, au lieu de cela, vous êtes obligé toocreate les dès le départ. Il s’agit des coûts de facturation hello des collections de base de données Cosmos sont tooyou transparent, et afin que vous pouvez régler les performances de hello, la cohérence et la capacité de vos collections directement à l’aide de hello [Cosmos DB API](https://msdn.microsoft.com/library/azure/dn781481.aspx). Nous recommandons d’utiliser une base de données de base de données Cosmos par travail toologically distinct de diffusion en continu vos collections pour un travail de diffusion en continu.

Certaines des options de collection Cosmos DB hello sont détaillées ci-dessous.

## <a name="tune-consistency-availability-and-latency"></a>Régler la cohérence, la disponibilité et la latence
toomatch les exigences de votre application, base de données Cosmos vous permet de base de données toofine régler hello et de regroupements et de rendre des compromis entre la latence, la disponibilité et la cohérence. Selon les niveaux de cohérence de lecture qui s’appliquent à votre scénario compte tenu de la latence de lecture et d’écriture, vous pouvez choisir un niveau de cohérence sur votre compte de base de données. Par défaut, Cosmos DB permet également l’indexation synchrone sur chaque collection de tooyour opération CRUD. Il s’agit d’un autre hello de toocontrol l’option performances dans la base de données Cosmos de lecture/écriture. Pour plus d’informations sur cette rubrique, consultez hello [modifier votre niveau de cohérence de base de données et de requête](../documentdb/documentdb-consistency-levels.md) l’article.

## <a name="upserts-from-stream-analytics"></a>Upserts à partir de Stream Analytics
Intégration Analytique de flux de données avec la base de données Cosmos vous permet de tooinsert ou mise à jour des enregistrements dans votre collection de base de données Cosmos basée sur une colonne d’ID de Document donnée. Il s’agit également tooas auxquels un *Upsert*.

Flux de données Analytique utilise une approche Upsert optimiste, où les mises à jour sont effectuées uniquement lors de l’insertion échoue en raison de conflits d’ID de Document tooa. Cette mise à jour est effectuée par flux de données Analytique comme un correctif logiciel, il permet de document toohello de mises à jour partielles, autrement dit, l’ajout de nouvelles propriétés ou de remplacement de qu'une propriété existante est effectuée de façon incrémentielle. Notez que la raison d’une modification dans les valeurs de propriétés de tableau dans votre document JSON hello dans le tableau dans son intégralité hello obtention remplacé, autrement dit, le tableau de hello n’est pas fusionnée.

## <a name="data-partitioning-in-cosmos-db"></a>Partitionnement des données dans Cosmos DB
COSMOS DB [partitionnée collections](../cosmos-db/partition-data.md) sont hello approche de partitionnement des données recommandée. 

Pour les collections de base de données Cosmos uniques, flux Analytique permet toujours toopartition vos données en fonction des modèles de requête hello et les besoins de performances de votre application. Chaque collection peut contenir des too10GB de données (maximum) et, actuellement, qu'il n’existe aucun tooscale de façon des (ou de dépassement de capacité) une collection. Pour la montée en puissance parallèle, Analytique de flux de données vous permet de collections de toomultiple toowrite avec un préfixe donné (voir les détails d’utilisation ci-dessous). Flux de données Analytique utilise hello cohérent [résolveur de Partition de hachage](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) stratégie basée sur l’utilisateur de hello fourni PartitionKey colonne toopartition ses enregistrements de sortie. Hello nombre de collections avec hello doté du préfixe à l’heure de début du travail de diffusion en continu de hello est utilisé en tant que nombre de partitions de sortie hello, tâche de hello toowhich écrit tooin parallèle (Collections de base de données Cosmos = sortie Partitions). Pour une collection unique utilisant une méthode d’indexation différée axée uniquement sur les insertions, vous pouvez vous attendre à un débit d’écriture de 0,4 Mo/s. L’utilisation de plusieurs regroupements peut permettre de vous tooachieve un débit plus élevé et une capacité supérieure.

Si vous envisagez de nombre de partitions tooincrease hello Bonjour futures, vous devrez peut-être toostop votre travail, les données de salutation repartition à partir de vos collections existantes dans les nouvelles collections, puis redémarrer hello flux Analytique travail. Nous publierons prochainement un article sur l’utilisation de PartitionResolver et sur le repartitionnement, avec des exemples de code. article de Hello [de partitionnement et de mise à l’échelle dans la base de données Cosmos](../documentdb/documentdb-partition-data.md) fournit également des détails sur ce.

## <a name="cosmos-db-settings-for-json-output"></a>Paramètres de Cosmos DB pour la sortie JSON
Lorsque vous créez une sortie Cosmos DB dans Stream Analytics, vous devez fournir des informations supplémentaires, comme indiqué ci-dessous. Cette section fournit une explication de la définition de propriétés hello.

Collection partitionnée | Collections « Partition unique » multiples
---|---
![écran de sortie documentdb stream analytics](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![écran de sortie documentdb stream analytics](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Hello **plusieurs collections de « Partition unique »** scénario nécessite une clé de partition et une configuration prise en charge. 

* **Alias de sortie** – un toorefer alias cette sortie dans votre requête ASA  
* **Nom de compte** – nom de hello ou point de terminaison de l’URI de hello Cosmos DB compte.  
* **Clé de compte** – clé d’accès partagé hello pour hello Cosmos DB compte.  
* **Base de données** – nom de base de données de base de données Cosmos hello.  
* **Modèle de nom de collection** – nom de la collection hello ou leur modèle pour hello collections toobe est utilisé. format du nom de collection Hello peut être construite à l’aide de jeton {partition} facultatif de hello, où les partitions commencent à 0. Voici des exemples d’entrées valides :  
  1\) MyCollection : il doit exister une collection nommée « MyCollection ».  
  2\) MyCollection{partition} : vous devez créer les collections « MyCollection0 », « MyCollection1 », « MyCollection2 », etc.  
* **Clé de partition** : facultative. Nécessaire uniquement si vous utilisez un jeton {partition} dans votre modèle de nom de collection. nom Hello du champ hello dans la clé de hello toospecify sortie événements utilisés pour le partitionnement de sortie entre les collections. Pour une sortie de collection unique, une colonne de sortie arbitraire peut être utilisée (par exemple, PartitionId).  
* **ID de document** : facultatif. nom de Hello du champ hello dans les événements de sortie utilisé clé primaire de toospecify hello basées sur les insert ou la mise à jour operations.  
