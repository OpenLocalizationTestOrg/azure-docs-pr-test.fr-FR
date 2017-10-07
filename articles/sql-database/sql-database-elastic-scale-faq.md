---
title: "aaaAzure Forum aux questions sur l’échelle élastique SQL | Documents Microsoft"
description: Frequently Asked Questions about Azure SQL Database Elastic Scale.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>FAQ sur les outils de bases de données élastiques
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>Si j’ai un locataire unique par partition et aucune clé de partitionnement, comment remplir clé de partitionnement hello pour plus d’informations de schéma hello ?
objet d’informations de schéma Hello est uniquement les scénarios de fusion toosplit utilisé. Si une application est fondamentalement locataire unique, puis n’exige pas l’outil de fusion de fractionnement hello et donc il n’existe aucun objet d’informations de schéma besoin toopopulate hello.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>J’ai configuré une base de données et dispose déjà d’un gestionnaire de cartes de partition, comment enregistrer cette nouvelle base de données en tant que partition ?
Consultez  **[Ajout d’une application tooan de partitions à l’aide de la bibliothèque cliente de base de données élastique hello](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Combien coûtent les outils de bases de données élastiques ?
À l’aide de la bibliothèque cliente de base de données élastique hello ne mobilise pas les coûts. Allocation des coûts uniquement pour les bases de données hello SQL Azure que vous utilisez pour les partitions et hello Gestionnaire de carte de partitions, ainsi que les rôles de web/de travail hello que vous préparer pour l’outil de fusion de fractionnement hello.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Pourquoi mes informations d’identification ne fonctionnent pas quand j’ajoute une partition d’un autre serveur ?
N’utilisez pas les informations d’identification sous forme de hello de « ID utilisateur =username@servername», à la place utiliser simplement « ID utilisateur = nom d’utilisateur ».  En outre, veillez à que ce nom de connexion « nom_utilisateur » hello dispose d’autorisations sur les partitions hello.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>Ce besoin toocreate un gestionnaire de carte de partitions et remplir les partitions chaque démarrage de mes applications ?
Ne : hello la création de hello Gestionnaire de carte de partitions (par exemple,  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) est une opération unique.  Votre application doit utiliser l’appel de hello  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  au démarrage de l’application.  Un seul appel de ce type n’est possible par domaine d’application.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>J’ai des questions sur l’utilisation des outils de bases de données élastique. Où trouver les réponses ?
Veuillez contacter toous sur hello [Forum sur la base de données SQL Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Lorsque j’obtiens une connexion de base de données à l’aide d’une clé de partitionnement, vous pouvez toujours interroger des données pour autres partitionnement clés sur hello, même partition.  Est-ce normal ?
Hello API infrastructure élastique vous donnent une base de données connexion toohello correcte pour votre clé de partitionnement, mais ne fournissent pas de filtrage clé de partitionnement.  Ajouter **où** clauses tooyour requête toorestrict hello étendue toohello fourni la clé de partitionnement, si nécessaire.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Puis-je utiliser une édition différente d’Azure SQL Database pour chaque partition de mon ensemble de partitions ?
Oui, une partition est une base de données individuelle, par conséquent, une partition peut utiliser une édition Premium alors qu’une autre utilise une édition Standard. En outre, Édition hello d’une partition peut augmenter ou diminuer plusieurs fois pendant la durée de vie hello de partition de hello.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Hello fourniture d’outil de fusion de fractionnement (ou supprimer) une base de données pendant une opération de fractionnement ou de fusion ?
Non. Pour **fractionner** opérations, la base de données cible hello doit exister avec le schéma approprié de hello et être inscrit avec hello Gestionnaire de carte de partitions.  Pour **fusion** opérations, vous devez supprimer les partitions hello à partir du Gestionnaire de carte de partitions hello et puis supprimez la base de données hello.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

