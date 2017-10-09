---
title: "aaaUsing toofix du Gestionnaire de récupération partition mapper des problèmes | Documents Microsoft"
description: "Utilisez hello RecoveryManager toosolve des problèmes de classe avec les cartes de partitions"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>À l’aide des problèmes du mappage de partitions hello RecoveryManager classe toofix
Hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) classe fournit des applications ADO.Net hello capacité tooeasily détecter et corriger les incohérences entre la carte de partitions globales de hello (GSM) et la carte de partitions local hello (LSM) dans un environnement de base de données partitionnée. 

Hello GSM et LSM suivi hello mappage de chaque base de données dans un environnement partitionné. Parfois, un arrêt se produit entre hello GSM et hello LSM. Dans ce cas, utilisez hello RecoveryManager classe toodetect et réparer le saut de hello.

Hello RecoveryManager classe fait partie de hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md). 

![Mappage de partition][1]

Vous trouverez les définitions des termes évoqués ici dans la page [Glossaire des outils de base de données élastique](sql-database-elastic-scale-glossary.md). toounderstand comment hello **ShardMapManager** les données toomanage utilisé dans une solution partitionnée, consultez [gestion de carte de partitions](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Pourquoi utiliser le Gestionnaire de récupération hello ?
Dans un environnement de base de données partitionnée, il existe un seul client par base de données et plusieurs bases de données par serveur. Il peut être également de nombreux serveurs dans un environnement de hello. Chaque base de données est mappé dans la carte de partitions hello, appels peuvent avoir une base de données et routé toohello correcte du serveur. Bases de données sont traitées selon tooa **clé de partitionnement**, et chaque partition est attribuée un **plage de valeurs de clé**. Par exemple, une clé de partitionnement peut-être représenter des noms de clients hello de « D » trop « f ». Hello mappage de toutes les partitions (c'est-à-dire dans les bases de données) et de leurs plages de mappage sont contenues dans hello **le carte de partitions globales (GSM)**. Chaque base de données contient également un mappage de plages hello contenue dans la partition hello appelé hello **le carte de partitions local (LSM)**. Lorsqu’une application se connecte à des partitions de tooa, mappage de hello est mis en cache avec l’application hello pour la récupération rapide. Hello LSM donnée utilisé toovalidate mis en cache. 

Hello GSM et LSM peuvent devenir désynchronisés pour hello suivant raisons :

1. suppression de Hello d’une partition dont l’étendue est considérée comme toono plu être utilisé, ou changement de nom d’une partition. La suppression d’une partition  se traduit par un **mappage de partition orphelin**. De même, une base de données renommée peut causer un mappage de partition orphelin. En fonction de la finalité de hello de modification de hello, les partitions hello peut-être toobe supprimé ou emplacement de partition hello doit toobe mis à jour. toorecover une base de données supprimée, consultez [restaurer une base de données supprimée](sql-database-recovery-using-backups.md).
2. Un événement de géo-basculement se produit. toocontinue, un doit mettre à jour hello nom du serveur et nom de la base de données du Gestionnaire de carte de partitions dans l’application hello, puis Détails de mappage de mise à jour hello partition pour toutes les partitions dans une carte de partitions. S’il existe un basculement géographique, une telle logique de récupération doit être automatisée dans le flux de travail de basculement hello. L’automatisation des actions de récupération offre des possibilités de gestion sans friction pour les bases de données géolocalisées et évite les interventions manuelles. toolearn sur toorecover options une base de données en cas de panne du centre de données, consultez [continuité](sql-database-business-continuity.md) et [la récupération d’urgence](sql-database-disaster-recovery.md).
3. Une partition ou hello ShardMapManager base de données est restaurée tooan antérieures point précis dans le temps. toolearn sur le point de récupération dans le temps à l’aide de sauvegardes, consultez [à l’aide de sauvegardes de récupération](sql-database-recovery-using-backups.md).

Pour plus d’informations sur les outils de la base de données élastique de base de données SQL Azure, géo-réplication et de restauration, voir hello : 

* [Vue d’ensemble : continuité des activités cloud et récupération d’urgence d’une base de données avec SQL Database](sql-database-business-continuity.md) 
* [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md)  
* [Gestion de ShardMap](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Récupération RecoveryManager à partir d’un ShardMapManager
première étape de Hello est toocreate une instance RecoveryManager. Hello [GetRecoveryManager méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) renvoie hello Gestionnaire de récupération pour hello actuel [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) instance. mappent de toutes les incohérences dans les partitions hello tooaddress, vous devez d’abord récupérer hello RecoveryManager pour la carte de partitions particulier de hello. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

Dans cet exemple, hello RecoveryManager hello ShardMapManager est initialisé. Hello ShardMapManager contenant un ShardMap est également déjà initialisé. 

Étant donné que ce code de l’application manipule la carte de partitions hello lui-même, hello des informations d’identification utilisées dans la méthode de fabrique hello (Bonjour précédent exemple, smmConnectionString) doivent être des informations d’identification disposant des autorisations de lecture-écriture sur base de données GSM hello référencé par hello chaîne de connexion. Ces informations d’identification sont en général différentes de connexions de tooopen d’informations d’identification utilisées pour le routage dépendant des données. Pour plus d’informations, consultez [à l’aide des informations d’identification de client de base de données élastique hello](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Suppression d’une partition à partir de hello ShardMap après la suppression d’une partition
Hello [DetachShard méthode](https://msdn.microsoft.com/library/azure/dn842083.aspx) détache hello fonction de partition à partir de la carte de partitions hello et supprime les mappages associés à des partitions de hello.  

* paramètre d’emplacement Hello est l’emplacement des partitions hello, spécifiquement le nom du serveur et nom de la base de données de partition hello détachée. 
* paramètre de shardMapName Hello est le nom de carte de partitions hello. Cela est uniquement requis lorsque plusieurs cartes de partitions sont gérés par hello même gestionnaire de carte de partitions. facultatif. 


> [!IMPORTANT]
> Utilisez cette technique uniquement si vous êtes certain que la plage hello pour le mappage de hello mis à jour est vide. méthodes Hello ci-dessus ne vérifient pas les données de la plage de hello déplacé, il est donc préférable tooinclude vérifie dans votre code.
>

Cet exemple supprime les partitions à partir de la carte de partitions hello. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

carte de partitions Hello reflète l’emplacement des partitions hello Bonjour GSM avant la suppression de hello de partition de hello. Étant donné que les partitions hello a été supprimée, il est supposé cela n’est pas intentionnel, et plage de clés de partitionnement hello n’est plus en cours d’utilisation. Sinon, vous pouvez exécuter une restauration à un moment donné. partition de hello toorecover à partir d’un plus haut dans le temps. (Dans ce cas, passez en revue hello suivant des incohérences de partitions section toodetect.) toorecover, consultez [Point de récupération dans le temps](sql-database-recovery-using-backups.md).

Dans la mesure où il est supposé hello de leur suppression n’est pas intentionnelle, hello action de nettoyage d’administration final est partition de toohello toodelete hello entrée dans le Gestionnaire de carte de partitions hello. Cela empêche l’application hello d’écrire par inadvertance des informations tooa plage qui n’est pas attendu.

## <a name="toodetect-mapping-differences"></a>différences de mappage toodetect
Hello [DetectMappingDifferences méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) sélectionne et retourne l’une des cartes de partitions hello (locales ou globales) en tant que source fiable hello et rapproche les mappages sur les deux cartes de partitions (GSM et LSM).

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Hello *emplacement* Spécifie le nom du serveur hello et le nom de la base de données. 
* Hello *shardMapName* paramètre est le nom de mappage de partitions hello. Cela est uniquement requis si plusieurs cartes de partitions sont gérés par hello même gestionnaire de carte de partitions. facultatif. 

## <a name="tooresolve-mapping-differences"></a>différences de mappage tooresolve
Hello [ResolveMappingDifferences méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) sélectionne l’une des cartes de partitions hello (locales ou globales) en tant que source de hello de vérité puis harmonise les mappages sur les deux cartes de partitions (GSM et LSM).

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Hello *RecoveryToken* paramètre énumère hello différences dans les mappages hello hello GSM et hello LSM pour les partitions spécifiques hello. 
* Hello [MappingDifferenceResolution énumération](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) est la méthode de hello tooindicate utilisé pour la résolution de différence hello entre les mappages de partition hello. 
* **MappingDifferenceResolution.KeepShardMapping** est recommandé que lorsque hello LSM qui contient les correspondances exactes hello et mappage hello dans les partitions hello doit donc être utilisé. C’est généralement hello cas s’il existe un basculement : les partitions hello résident maintenant sur un nouveau serveur. Étant donné que les partitions hello doivent tout d’abord être supprimée de hello GSM (à l’aide de la méthode de RecoveryManager.DetachShard hello), un mappage n’existe plus sur hello GSM. Hello LSM doit donc être utilisé toore-établir le mappage de partitions hello.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Attacher un toohello partition ShardMap après la restauration d’une partition
Hello [AttachShard méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) attache hello carte de partitions toohello de partition donné. Il détecte des incohérences de mappage de partition et met à jour de la partition de hello hello mappages toomatch hello au moment même de restauration de partition hello. Il est supposé que Hello base de données est également renommée tooreflect hello nom d’origine (avant la restauration de partition de hello), étant donné que la restauration de point à temps hello par défaut est la nouvelle base de données tooa ajouté avec un horodateur de hello. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Hello *emplacement* paramètre est le nom du serveur hello et nom de la base de données de partition hello en cours d’attachement. 
* Hello *shardMapName* paramètre est le nom de mappage de partitions hello. Cela est uniquement requis lorsque plusieurs cartes de partitions sont gérés par hello même gestionnaire de carte de partitions. facultatif. 

Cet exemple ajoute une carte de partitions toohello partition qui a été récemment restaurée à partir d’une heure antérieure de point. Étant donné que les partitions de hello (à savoir hello mappage de partitions hello Bonjour LSM) a été restaurée, il est potentiellement incohérent avec une entrée de partition hello Bonjour GSM. En dehors de cet exemple de code, les partitions hello a été restaurée et renommé toohello le nom d’origine de la base de données hello. Dans la mesure où il a été restaurée, il est supposé être mappage hello Bonjour LSM mappage de confiance hello. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Mise à jour des emplacements de partitions après un basculement géographique (restauration) de partitions de hello
S’il existe un basculement géographique, base de données secondaire hello est accessibles écrire et devient hello base de données primaire. nom du serveur de hello et potentiellement hello base de données (selon votre configuration) de Hello, peut être différent du serveur principal d’origine de hello. Par conséquent hello des entrées de mappage de partitions hello Bonjour GSM et LSM doit être corrigée. De même, si hello base de données est restaurée tooa autre nom ou emplacement ou tooan point antérieur dans le temps, cela peut provoquer des incohérences dans les cartes de partitions hello. Hello Gestionnaire de carte de partitions gère la distribution hello de base de données de connexions ouvertes toohello correcte. Distribution est basée sur des données dans la carte de partitions hello et valeur hello de clé de partitionnement hello cible hello de demande d’applications hello hello. Après un basculement géographique, ces informations doivent être mis à jour avec le nom du serveur précis hello, nom de la base de données et le mappage de partition de base de données récupérée hello. 

## <a name="best-practices"></a>Meilleures pratiques
Basculement géographique et restauration sont des opérations généralement gérées par un administrateur de cloud de l’application hello intentionnellement utilisant une des fonctionnalités de continuité d’activité de bases de données SQL Azure. Planification de la continuité des activités commerciales nécessite tooensure de mesures commerciales peuvent continuer sans interruption, des procédures et processus. Hello méthodes disponibles comme partie de hello RecoveryManager classe doit être utilisé dans ce hello de tooensure de flux de travail GSM et LSM sont mis à jour en fonction de l’action de récupération hello entreprise. Il existe cinq étapes de base tooproperly garantissant hello GSM et LSM reflètent des informations précises hello après un événement de basculement. Bonjour tooexecute de code d’application que ces étapes peuvent être intégrées dans les flux de travail et des outils existants. 

1. Extraire hello RecoveryManager hello ShardMapManager. 
2. Détachez la partition ancienne de hello à partir de la carte de partitions hello.
3. Attachez hello nouvelle partition toohello carte de partitions, y compris le nouvel emplacement de partition hello.
4. Détecter les incohérences Bonjour le mappage entre les hello GSM et LSM. 
5. Résoudre les différences entre hello GSM et hello LSM, approbation hello LSM. 

Cet exemple exécute hello comme suit :

1. Supprime les partitions de hello carte de partitions qui reflète les emplacements des partitions avant l’événement de basculement hello.
2. Joint des partitions toohello carte de partitions réfléchissante hello nouvelle partition emplacements (le paramètre hello « Configuration.SecondaryServer » est le nom du nouveau serveur hello mais hello même nom de base de données).
3. Récupère les jetons de récupération hello en détectant les différences de mappage entre hello GSM et hello LSM pour chaque partition. 
4. Résout les incohérences hello en approbation mappage hello de hello LSM de chaque partition. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

