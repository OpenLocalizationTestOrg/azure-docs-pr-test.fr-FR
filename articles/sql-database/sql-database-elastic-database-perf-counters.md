---
title: aaaPerformance les compteurs pour le Gestionnaire de carte de partitions
description: "Classe ShardMapManager et compteurs de performances pour le routage dépendant des données"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Compteurs de performance pour le Gestionnaire de cartes de partitions
Vous pouvez capturer des performances hello d’un [Gestionnaire de carte de partitions](sql-database-elastic-scale-shard-map-management.md), surtout lorsque vous utilisez [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md). Les compteurs sont créés avec des méthodes de hello Microsoft.Azure.SqlDatabase.ElasticScale.Client classe.  

Les compteurs sont utilisés tootrack les performances de hello de [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) operations. Ces compteurs sont accessibles dans hello Analyseur de performances, sous la catégorie de « Élastique de base de données : partition gestion » hello.

**Pour la version la plus récente hello :** accédez trop[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Voir aussi [mise à niveau d’une bibliothèque cliente de base de données élastique plus récente d’application toouse hello](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Composants requis
* catégorie de performance toocreate hello et des compteurs hello utilisateur doit faire partie de hello local **administrateurs** groupe sur l’ordinateur hello hébergeant l’application hello.  
* toocreate performances instance de compteur et mettre à jour les compteurs de hello, utilisateur de hello doit être un membre de deux hello **administrateurs** ou **utilisateurs de l’Analyseur de performances** groupe. 

## <a name="create-performance-category-and-counters"></a>Création de catégories et de compteurs de performances
les compteurs de hello toocreate, appelez la méthode de CreatePeformanceCategoryAndCounters de hello Hello [ShardMapManagmentFactory classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Seul un administrateur peut exécuter la méthode hello : 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

Vous pouvez également utiliser [cela](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) méthode hello de PowerShell script tooexecute. méthode Hello crée hello suivant des compteurs de performances :  

* **Mise en cache des mappages**: nombre de mappages mis en cache pour la carte de partitions hello.
* **DDR opérations/s**: taux d’opérations routage dépendant des données pour la carte de partitions hello. Ce compteur est mis à jour lorsqu’un appel trop[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) entraîne une partition de destination toohello connexion réussie. 
* **Mappage des présences dans le cache de recherche/s**: taux d’opérations de recherche du cache réussi pour les mappages dans la carte de partitions hello. 
* **Mappage des absences dans le cache de recherche/s**: taux d’opérations de recherche de cache ayant échoué pour les mappages dans la carte de partitions hello.
* **Mappages ajoutés ou mis à jour dans le cache/s**: taux lesquelles mappages sont ajoutés ou mis à jour de cache pour la carte de partitions hello. 
* **Les mappages supprimés du cache/s**: vitesse à laquelle les mappages sont supprimés du cache pour la carte de partitions hello. 

Les compteurs de performances sont créés pour chaque carte de partitions mises en cache par processus.  

## <a name="notes"></a>Remarques
Hello événements suivants déclenchent la création de hello hello des compteurs de performances :  

* L’initialisation de hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) avec [chargement hâtif](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), si hello ShardMapManager contient toutes les cartes de partitions. Ceux-ci incluent hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) et hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) méthodes.
* Recherche réussie d’une carte de partitions (à l’aide de [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) ou [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Création réussie de la carte de partitions à l’aide de CreateShardMap().

les compteurs de performance Hello mettra à jour toutes les opérations de cache effectuées sur les mappages et de carte de partitions hello. Suppression réussie de la carte de partitions hello à l’aide de DeleteShardMap () reults à la suppression de l’instance des compteurs de performance hello.  

## <a name="best-practices"></a>Meilleures pratiques
* La création de compteurs et de la catégorie de performance hello doit être effectuée qu’une seule fois avant la création de hello de ShardMapManager objet. Chaque exécution de la commande hello CreatePerformanceCategoryAndCounters() efface les compteurs précédents hello (perte de données signalées par toutes les instances) et crée de nouvelles.  
* Des instances de compteurs de performances sont créées pour chaque processus. Tout blocage d’application ou la suppression d’une carte de partitions à partir du cache de hello entraîne la suppression des instances de compteurs de performances hello.  

### <a name="see-also"></a>Voir aussi
[Vue d’ensemble des fonctionnalités de base de données élastique](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

