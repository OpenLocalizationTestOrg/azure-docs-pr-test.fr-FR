---
title: "mise en application aaaRolling - base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment toouse géo-réplication de base de données SQL Azure toosupport en ligne les mises à niveau de votre application cloud."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>Gestion des mises à niveau propagées d’applications cloud à l’aide d’une géoréplication active de SQL Database
> [!NOTE]
> La [géoréplication active](sql-database-geo-replication-overview.md) est désormais disponible pour toutes les bases de données de tous niveaux.
> 

Découvrez comment toouse [géo-réplication](sql-database-geo-replication-overview.md) dans la base de données SQL tooenable enchaînée mises à niveau de votre application dans le cloud. Une mise à niveau est une opération qui entraîne une interruption de service ; il est donc recommandé de l’intégrer à votre conception et à votre planification de la continuité des activités. Dans cet article, que nous examinons les deux méthodes de hello orchestrant ces opérations mise à niveau et présentent les avantages hello et compromis de chaque option. Pour des raisons de hello de cet article, nous allons utiliser une application simple qui se compose d’un site web tooa connectée unique de base de données en tant que sa couche données. Notre objectif est de tooupgrade version 1 de hello application tooversion 2 sans aucun impact significatif sur l’expérience utilisateur final hello. 

Lors de l’évaluation des options de mise à niveau de hello, vous devez envisager hello suivant facteurs :

* Impact sur la disponibilité de l’application au cours des mises à niveau. La durée pendant laquelle les fonction de l’application hello peut être limitée ou détériorée.
* Capacité tooroll sauvegarder en cas d’un échec de mise à niveau.
* Vulnérabilité de l’application hello si une défaillance catastrophique non liée se produit pendant la mise à niveau hello.
* Coût total du processus,  Cela inclut une redondance supplémentaire et des coûts incrémentiels des composants de hello temporaire utilisés par le processus de mise à niveau hello. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>Mise à niveau d’applications dont la récupération d’urgence repose sur des sauvegardes de base de données
Si votre application s’appuie sur les sauvegardes de base de données automatique et utilise la géo-restauration pour la récupération d’urgence, il est généralement déployé tooa une seule région Azure. Dans ce cas les processus de mise à niveau hello implique la création d’un déploiement de tous les composants d’application de sauvegarde impliqués dans la mise à niveau hello. interruption de l’utilisateur final hello toominimize vous reposera sur Azure Traffic Manager (WATM) avec le profil de basculement hello.  Hello suivant schéma illustre la mise à niveau du précédent toohello hello environnement d’exploitation. point de terminaison de Hello <i>contoso-1.azurewebsites.net</i> représente un emplacement de production de l’application hello nécessitant toobe mis à niveau. tooenable hello capacité tooroll précédent hello mise à niveau, vous devez créer un emplacement de l’étape avec une copie entièrement synchronisée de l’application hello. Hello étapes suivantes sont à l’application hello tooprepare requis pour la mise à niveau hello :

1. Créez un emplacement de la phase de mise à niveau hello. toodo qui créent une base de données secondaire (1) et de déployer un site web identique Bonjour même région Azure. Surveiller les toosee secondaire hello si hello amorçage le processus est terminé.
2. Création d’un profil de basculement dans WATM en utilisant <i>contoso-1.azurewebsites.net</i> comme point de terminaison en ligne et <i>contoso-2.azurewebsites.net</i> comme point de terminaison hors connexion. 

> [!NOTE]
> Remarque Les étapes de préparation hello n’affectera pas application hello dans l’emplacement de production hello et il peut fonctionner en mode d’accès complet.
>  

![Configuration de la géoréplication d’une base de données SQL. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Une fois les étapes de préparation hello terminés application hello est prête pour la mise à niveau réelle de hello. Hello suivant schéma illustre les étapes de hello impliqués dans le processus de mise à niveau hello. 

1. Définir la base de données primaire hello hello emplacement tooread uniquement en mode de production (3). Cela garantit que hello instance de production de l’application hello (V1) au cours de mise à niveau hello donc pas possible divergence des données hello entre hello V1 et instances de base de données V2 restera en lecture seule.  
2. Déconnecter la base de données secondaire hello à l’aide du mode d’arrêt planifié hello (4). Il créera une copie indépendante entièrement synchronisée de la base de données primaire hello. Cette base de données est alors mise à niveau.
3. Activer le mode de tooread-écriture de base de données primaire hello et exécutez le script de mise à niveau de hello dans l’emplacement de phase hello (5).     

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Si la mise à niveau hello terminée, vous êtes maintenant prêt tooswitch hello fin utilisateurs toohello intermédiaire copie hello application. Il deviendra maintenant l’emplacement de production hello de l’application hello.  Cela implique quelques étapes supplémentaires, comme illustré sur hello suivant schéma.

1. Commutateur de point de terminaison en ligne hello dans le profil WATM hello trop<i>contoso-2.azurewebsites.net</i>, version toohello V2 points du site web de hello (6). Il devient alors l’emplacement de production hello avec hello application V2 et le trafic de l’utilisateur final hello est dirigée tooit.  
2. Si vous n’avez plus besoin composants de l’application hello V1 et vous pouvez en toute sécurité les supprimer (7).   

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Si le processus de mise à niveau hello n’aboutit pas, par exemple en raison de l’erreur tooan dans le script de mise à niveau hello, emplacement de phase hello doit être considéré comme compromis. tooroll sauvegarder hello toohello pré-mise à niveau état de l’application vous restaurez simplement application hello dans access toofull de hello production emplacement. étapes Hello sont affichent sur le diagramme suivant de hello.    

1. Définissez hello de base de données copie tooread-écriture en mode (8). Cette opération restaure hello complète V1 fonctionnellement dans l’emplacement de production hello.
2. Effectuer l’analyse des causes hello et supprimer des composants de hello compromis dans l’emplacement de phase hello (9). 

À ce stade application hello est entièrement fonctionnelle et les étapes de mise à niveau hello peuvent être répétés.

> [!NOTE]
> Hello rollback ne requiert pas les modifications dans le profil WATM comme il pointe déjà trop<i>contoso-1.azurewebsites.net</i> comme hello du point de terminaison actif.
> 
> 

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

clé de Hello **parti** de cette option est que vous pouvez mettre à niveau une application dans une seule région à l’aide d’un ensemble d’étapes simples. coût global de mise à niveau hello Hello est relativement faible. Hello principal **compromis** est que si une défaillance irrémédiable se produit au cours de l’état de pré-mise à niveau la récupération toohello mise à niveau hello hello implique redéploiement de l’application hello dans une autre région et la restauration de la base de données hello de sauvegarde à l’aide de géo-restauration. Ce processus entraîne des interruptions de service importantes.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Mise à niveau d’applications dont la récupération d’urgence repose sur la géoréplication de la base de données
Si votre application utilise un géo-réplication pour la continuité d’activité, il est déployé tooat au moins deux des régions différentes avec un déploiement actif dans la région principale et un déploiement en attente dans la région de la sauvegarde. En outre les facteurs toohello mentionné précédemment, les processus de mise à niveau hello doivent garantir que :

* application Hello reste protégée contre les pannes catastrophiques à tout moment pendant le processus de mise à niveau hello
* composants de géo-redondant Hello de l’application hello sont mis à niveau en parallèle avec les composants active hello

tooachieve ces objectifs, vous allez exploiter Azure Traffic Manager (WATM) à l’aide de basculement de hello profil associé à une active et trois points de terminaison de sauvegarde.  Hello suivant schéma illustre la mise à niveau du précédent toohello hello environnement d’exploitation. Hello sites web <i>contoso-1.azurewebsites.net</i> et <i>contoso-dr.azurewebsites.net</i> représentent un emplacement de production de l’application hello avec redondance géographique complète. tooenable hello capacité tooroll précédent hello mise à niveau, vous devez créer un emplacement de l’étape avec une copie entièrement synchronisée de l’application hello. Étant donné que vous avez besoin de tooensure application hello permet de restaurer rapidement en cas d’une défaillance irrémédiable se produit pendant le processus de mise à niveau de hello, emplacement de phase hello a besoin toobe géo-redondant ainsi. Hello étapes suivantes sont à l’application hello tooprepare requis pour la mise à niveau hello :

1. Créez un emplacement de la phase de mise à niveau hello. toodo qui créent une base de données secondaire (1) et de déployer une copie identique de site web de hello Bonjour même région Azure. Surveiller les toosee secondaire hello si hello amorçage le processus est terminé.
2. Créer une base de données secondaire géo-redondant dans l’emplacement de phase hello par géo-réplication sauvegarde région hello de base de données secondaire toohello (appelée « chaînées géo-réplication »). Analyse toosee secondaire de hello sauvegarde si hello amorçage le processus est terminé (3).
3. Créer une copie de secours du site web de hello dans la région de sauvegarde hello et le lier toohello redondante base de données secondaire (4).  
4. Ajouter des points de terminaison supplémentaires hello <i>contoso-2.azurewebsites.net</i> et <i>contoso-3.azurewebsites.net</i> toohello profil de basculement dans WATM comme points de terminaison hors connexion (5). 

> [!NOTE]
> Remarque Les étapes de préparation hello n’affectera pas application hello dans l’emplacement de production hello et il peut fonctionner en mode d’accès complet.
> 
> 

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Une fois les étapes de préparation hello terminés, emplacement d’étape de hello est prêt pour la mise à niveau hello. Hello suivant schéma illustre les étapes de mise à niveau de hello.

1. Définir la base de données primaire hello hello emplacement tooread uniquement en mode de production (6). Cela garantit que hello instance de production de l’application hello (V1) au cours de mise à niveau hello donc pas possible divergence des données hello entre hello V1 et instances de base de données V2 restera en lecture seule.  
2. Déconnecter la base de données secondaire hello Bonjour même à l’aide de la région de hello mode d’arrêt planifié (7). Il créera une copie d’indépendante entièrement synchronisée de hello base de données primaire, qui deviendra automatiquement un serveur principal après l’arrêt de hello. Cette base de données est alors mise à niveau.
3. Activer la base de données primaire hello en hello étape emplacement tooread-écriture et exécuter le script de mise à niveau hello (8).    

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Si la mise à niveau hello terminée vous n’êtes désormais prêt tooswitch hello aux utilisateurs finaux toohello V2 version de l’application hello. Hello suivant schéma illustre les étapes hello.

1. Commutateur de point de terminaison actif hello dans le profil WATM hello trop<i>contoso-2.azurewebsites.net</i>, qui maintenant pointe version toohello V2 de hello web site (9). Il devient alors un emplacement de production avec hello application V2 et le trafic de l’utilisateur final est dirigé tooit. 
2. Si vous n’avez plus besoin application V1 de hello par conséquent, vous pouvez supprimer en toute sécurité (10 et 11).  

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Si le processus de mise à niveau hello n’aboutit pas, par exemple en raison de l’erreur tooan dans le script de mise à niveau hello, emplacement de phase hello doit être considéré comme compromis. tooroll sauvegarder hello toohello pré-mise à niveau état de l’application vous restaurez simplement application hello de toousing dans l’emplacement de production hello avec un accès complet. étapes Hello sont affichent sur le diagramme suivant de hello.    

1. Ensemble de la copie de base de données primaire hello hello emplacement tooread-écriture en mode de production (12). Cette opération restaure hello complète V1 fonctionnellement dans l’emplacement de production hello.
2. Effectuer l’analyse des causes hello et supprimer des composants de hello compromis dans l’emplacement de phase hello (13 et 14). 

À ce stade application hello est entièrement fonctionnelle et les étapes de mise à niveau hello peuvent être répétés.

> [!NOTE]
> Hello rollback ne requiert pas les modifications dans le profil WATM comme il pointe déjà trop <i>contoso-1.azurewebsites.net</i> comme hello du point de terminaison actif.
> 
> 

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

clé de Hello **parti** de cette option est que vous pouvez mettre à niveau application hello et sa copie géo-redondant en parallèle sans pour autant compromettre votre continuité d’activité au cours de la mise à niveau hello. Hello principal **compromis** est qu’il requiert de la redondance double de chaque composant d’application et par conséquent implique un coût plus élevé. Elle implique également un flux de travail plus complexe. 

## <a name="summary"></a>Résumé
diffère entre les méthodes de mise à niveau Hello deux décrits dans l’article hello dollar hello et de complexité de coût, mais ils sont tous deux se concentrent sur la réduction des temps hello lorsque hello utilisateur est limitées tooread les opérations de. Cette heure est définie directement par durée hello du script de mise à niveau hello. Il ne dépend pas de taille de base de données hello, hello de niveau de service vous choisissez, configuration du site web hello et vous ne pouvez pas facilement contrôler d’autres facteurs. Il s’agit, car toutes les étapes de préparation hello sont découplées à partir des étapes de mise à niveau hello et peuvent être effectuées sans affecter l’application de production hello. efficacité Hello du script de mise à niveau hello est un facteur clé hello qui détermine l’utilisateur final hello pendant les mises à niveau. Vous pouvez l’améliorer mieux hello consiste à concentrer vos efforts sur la création de script de mise à niveau hello aussi efficaces que possible.  

## <a name="next-steps"></a>Étapes suivantes
* Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).
* toolearn sur les sauvegardes de base de données SQL Azure automatisée, consultez [base de données SQL des sauvegardes automatisées](sql-database-automated-backups.md).
* toolearn sur l’utilisation des sauvegardes automatisées pour la récupération, consultez [restaurer une base de données à partir de sauvegardes automatisées](sql-database-recovery-using-backups.md).
* toolearn sur les options de récupération plus rapides, consultez [géo-réplication active](sql-database-geo-replication-overview.md).


