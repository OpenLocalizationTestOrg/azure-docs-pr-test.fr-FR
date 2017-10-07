---
title: "aaaAzure étude de cas de base de données Azure SQL - Umbraco | Documents Microsoft"
description: "Découvrez comment Umbraco utilise disposition tooquickly de base de données SQL et les services de mise à l’échelle pour des milliers de clients dans le cloud de hello"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco utilise une disposition tooquickly de base de données SQL Azure et les services de mise à l’échelle pour des milliers de clients dans le cloud de hello
![Logo Umbraco](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco est un système de gestion de contenu open source populaires (CMS) qui peut exécuter quoi que ce soit à partir de petits sites campagne ou brochure toocomplex applications pour le classement de Fortune 500 et sites Web de support global. 

> « Nous avons une grande Communauté de développeurs qui utilisent le système de hello, avec plus de 100 000 développeurs sur nos forums et plus de 350 000 sites qui sont actives, Umbraco en cours d’exécution. »
> 
> — Morten Christensen, responsable technique, Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

déploiements de clients toosimplify, Umbraco ajouté Umbraco-as-a-Service (Administered Address) : une software-as-a-service (SaaS) offre qui élimine la nécessité de hello pour les déploiements sur site, mise à l’échelle intégrées et supprime la gestion en activant la surcharge toofocus aux développeurs sur la gestion de l’innovation plutôt que des solutions de produit. Umbraco est en mesure de tooprovide tous les avantages en vous appuyant sur hello flexible modèle (PaaS) de platform-as-a-service proposé par Microsoft Azure.

Administered Address permet aux clients de SaaS toouse Umbraco CMS les fonctionnalités qui ont été précédemment en dehors de leur portée. Ces clients sont approvisionnés avec un environnement de CMS fonctionnel qui inclut une base de données de production. Les clients peuvent ajouter des bases de données supplémentaires tootwo pour le développement et les environnements, en fonction des exigences de mise en lots. Lorsqu’un nouvel environnement est demandé, un processus automatisé affecte automatiquement une base de données à ce client. nouvelle base de données Hello est prêt, en secondes, car la base de données hello a déjà été préalablement configuré par Umbraco à partir d’un pool élastique Azure des bases de données disponibles (voir Figure 1).

![Cycle de vie d’approvisionnement Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Figure 1. Approvisionnement du cycle de vie pour Umbraco-as-a-Service (UaaS)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Les pools élastiques Azure et l’automatisation simplifient les déploiements
Avec Azure SQL Database et d’autres services Azure, les clients Umbraco peuvent approvisionner eux-mêmes leurs environnements, et Umbraco peut facilement surveiller et gérer les bases de données selon un flux de travail intuitif :

1. Mise en service
   
   Umbraco maintient une capacité de 200 bases de données pré-approvisionnées et disponibles dans des pools élastiques. Quand un nouveau client s’inscrit à Administered Address, Umbraco présente hello client un nouvel environnement CMS quasiment en temps réel en leur attribuant une base de données à partir du pool de disponibilité hello.
   
   Lorsqu’un pool de disponibilité atteint son seuil, un nouveau pool élastique est créé et nouvelles bases de données sont préconfiguré toobe affecté toocustomers en fonction des besoins.
   
   L’implémentation est entièrement automatisée grâce aux bibliothèques de gestion C# et aux files d’attente Azure Service Bus.
2. Utilisation
   
   Clients utilisent une toothree environnements (pour la production, mise en lots et/ou développement), chacun avec sa propre base de données. Bases de données client sont dans les pools élastiques, ce qui permet de tooprovide Umbraco efficace de mise à l’échelle sans avoir tooover la configuration.
   
   ![Vue d’ensemble du projet Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Détails du projet Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Figure 2 : Site web client Umbraco-as-a-Service (UaaS), montrant les détails et la vue d’ensemble du projet
   
   Base de données SQL Azure utilise l’alimentation relative du hello toorepresent unités de Transaction de base de données (Udbd) requise pour les transactions de base de données réelle. Pour les clients d’Administered Address, bases de données fonctionnent au dtu environ 10, mais chacune a hello élasticité tooscale à la demande. Cela signifie que l’UaaS peut faire en sorte que les clients aient toujours les ressources nécessaires, même pendant les heures d’activité maximale. Par exemple, lors d’un événement sportif dimanche récent un client Administered Address a rencontré des pics de base de données des too100 dtu pour durée hello du jeu de hello. Les pools élastiques Azure ont permis Umbraco toosupport exigeant une haute sans dégradation des performances.
3. Surveiller
   
   Analyses d’Umbraco de base de données de l’activité à l’aide de tableaux de bord dans hello portail Azure, ainsi que des alertes par courrier électronique personnalisé.
4. Récupération d'urgence
   
   Azure propose deux options de récupération d’urgence : la géoréplication active et la géorestauration. Hello, option de récupération d’urgence une société doit sélectionner dépend de son [objectifs de continuité d’activité](sql-database-business-continuity.md).
   
   géo-réplication Active offre un niveau de plus rapide de hello de réponse dans l’événement hello du temps d’arrêt. À l’aide de géo-réplication active, vous pouvez créer des copies secondaires lisibles de toofour sur les serveurs dans des régions différentes, et vous pouvez lancer tooany de basculement de bases de données secondaires hello dans les cas hello d’échec.
   
   Umbraco ne nécessite pas la géo-réplication, mais elle ne tire pas parti de géo-restauration Azure toohelp Vérifiez minimum d’interruption en cas de hello d’une panne. La géorestauration s’appuie sur les sauvegardes des bases de données dans le stockage Azure géoredondant. Qui permet de toorestore les utilisateurs à partir d’une copie de sauvegarde lorsqu’il existe une panne dans la région principale de hello.
5. Annuler l’approvisionnement
   
   Lorsqu’un environnement de projet est supprimé, les bases de données (de développement, intermédiaires ou en ligne) associées sont supprimées au cours du nettoyage de la file d’attente Azure Service Bus. Ce processus automatisé restaurations hello pool de disponibilité de base de données élastique de bases de données inutilisées tooUmbraco, ce qui les rend disponibles pour la configuration future tout en conservant l’utilisation maximale.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Autoriser les pools élastiques Administered Address tooscale en toute simplicité
En tirant parti des pools élastiques Azure, Umbraco peut optimiser les performances de ses clients sans avoir tooover - ou Configuration incomplète. Umbraco possède actuellement des près de 3 000 bases de données dans 19 pools élastiques, hello capacité tooeasily évoluer comme nécessaire tooaccommodate un de leurs clients existants de 325 000 ou de nouveaux clients qui sont prêt toodeploy un CMS dans le cloud de hello.

En fait, en fonction de tooMorten Christensen, responsable technique chez Umbraco, « Administered Address maintenant rencontre croissance d’environ 30 nouveaux clients par jour. Nos clients sont très la commodité hello d’être en mesure de tooprovision nouveaux projets en secondes, publier des mises à jour tootheir des sites en direct à partir d’un environnement de développement à l’aide de « déploiement en un clic » instantanément et apporter des modifications plus rapidement si trouvez des erreurs . »

Si un client n’a plus besoin du deuxième ou du troisième environnement, il peut simplement les supprimer. Qui libère des ressources qui peuvent être utilisées pour d’autres clients dans le cadre de hello pool de disponibilité de base de données élastique Umbraco.

![Architecture de déploiement Umbraco](./media/sql-database-implementation-umbraco/figure4.png)

Figure 3. Architecture de déploiement UaaS sur Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>chemin d’accès de Hello à partir du centre de données toocloud
Lorsque les développeurs de hello Umbraco initialement rendue hello décision toomove tooa modèle SaaS, connaît qu’ils ont besoin d’un toobuild de façon économique et évolutive hors service de hello.

> « Les pools élastiques sont parfaitement adaptés à notre offre SaaS, car nous pouvons accroître ou diminuer la capacité en fonction des besoins. L’approvisionnement est facile et, avec notre configuration, nous pouvons maintenir une utilisation maximale. »
> 
> — Morten Christensen, responsable technique, Umbraco
> 
> 

« Nous voulions toospend nos délais de résolution des problèmes de nos clients, ne pas la gestion des infrastructures. Nous voulions toomake plus facile pour notre tooget clients hello meilleur, » indique que Niels Hartvig, créateur de Umbraco. « Nous considéré initialement comme serveurs hello nous-mêmes d’hébergement, mais la planification des capacités aurait dû cauchemar ». » Par coïncidence, Umbraco n’emploie pas d’administrateurs de bases de données, ce qui met en évidence une proposition de valeur essentielle pour l’utilisation de l’UaaS.

Un objectif important pour les développeurs de hello Umbraco a été tooprovide un moyen pour les environnements de tooprovision Administered Address clients rapidement et sans limites de capacité. Mais, en fournissant qu'un service hébergé dédié dans les centres de données Umbraco aurait un grand nombre requis de la capacité excédentaire toohandle rafales dans le traitement. Cela aurait signifié ajouter une infrastructure de calcul considérable qui aurait été régulièrement sous-utilisée.

En outre, équipe de développement hello Umbraco souhaitait une solution qui permettrait tooreuse autant de leur code existant que possible. En tant que développeur d’Umbraco Mikkel Madsen les États, « nous ont été satisfaits des outils de développement Microsoft hello que nous avons déjà familiers, comme Microsoft SQL Server, base de données SQL Microsoft Azure, ASP.net et Internet Information Services (IIS). Avant d’investir dans IaaS ou un PaaS cloud solution, nous voulions toomake assurer qu’il serait prennent en charge nos outils de Microsoft et les plateformes, donc nous n’aurions toomake modifications massives tooour base de code. »

toomeet tous ses critères de, Umbraco recherche un partenaire de nuage avec hello suivant qualifications :

* Capacité et fiabilité suffisantes
* Prise en charge des outils de développement Microsoft, afin que Umbraco ingénieurs ne serait pas forcé toocompletely réinventer leur environnement de développement
* Présence dans tous les marchés géographiques hello dans lequel Administered Address termine (tooensure entreprises nécessaire qu’ils peuvent accéder à leurs données rapidement et que leurs données sont stockées dans un emplacement qui répond à leurs exigences réglementaires régionales)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Pourquoi Umbraco a choisi Azure pour l’UaaS
En fonction de tooMorten Christensen « après prise en compte toutes les options de notre, nous avons sélectionné Azure, car il satisfait toutes les nos critères, de facilité de gestion et évolutivité toofamiliarity et la rentabilité. Nous avons défini les environnements hello sur des machines virtuelles Azure, et chaque environnement possède sa propre instance de la base de données SQL Azure, avec toutes les instances de hello dans les pools élastiques. En séparant les bases de données entre les environnements de développement, intermédiaire et en direct, nous pouvons à nos clients des performances fiables d’isolation mis en correspondance tooscale — un énorme avantage. »

Morten continue, « avant, nous avons dû tooprovision des serveurs de bases de données web manuellement. Maintenant, nous n’avons pas toothink sur elle. Tout est automatisée, de l’approvisionnement toocleanup. »

Morten est également heureux hello mise à l’échelle des fonctionnalités fournies par Azure. « Les pools élastiques sont parfaitement adaptés à notre offre SaaS, car nous pouvons accroître ou diminuer la capacité en fonction des besoins. L’approvisionnement est facile et, avec notre configuration, nous pouvons maintenir une utilisation maximale. » États Morten, « simplicité de hello de pools élastiques, ainsi que d’assurance hello de dtu basée sur la couche de service, nous obtenons hello power tooprovision nouveaux pools de ressources à la demande. Récemment, un de nos clients plus pointu dtu too100 dans son environnement d’exploitation. À l’aide d’Azure, notre pools élastiques fourni des bases de données du client hello avec des ressources hello qui en temps réel sans avoir des exigences de DTU toopredict. En bref, nos clients d’obtenir hello bouclage temps ils attendent que nous pouvons respecter nos contrats de niveau de service de performances ».

Mikkel Madsen l’additionne : « nous avons adopté hello puissant Azure algorithme qui se connecte SaaS scénario (d’intégration nouveaux clients en temps réel à grande échelle) tooour application courant (configuration anticipée des bases de données, à la fois le développement et live) par-dessus hello technologie (à l’aide de files d’attente Azure Service Bus conjointement avec la base de données SQL Azure). »

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Avec Azure, l’UaaS dépasse les attentes des clients
Depuis le choix d’Azure en tant que son partenaire de nuage, Umbraco a été en mesure de tooprovide des clients d’Administered Address avec optimisation des performances de gestion de contenu, sans investissement hello ressources informatiques nécessaire à partir d’une solution auto-hébergé. Comme Morten dit, « nous aimons commodité de développeur hello et évolutivité Azure permet, et nos clients sont ravis de fiabilité et de fonctionnalités de hello. En somme, c’est un grand pas en avant pour nous ! »

## <a name="more-information"></a>Plus d’informations
* toolearn en savoir plus sur les pools élastiques Azure, consultez [pools élastiques](sql-database-elastic-pool.md).
* toolearn en savoir plus sur le Bus des services Azure, consultez [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn en savoir plus sur les rôles Web et worker, consultez [rôles de travail](../fundamentals-introduction-to-azure.md#compute).    
* toolearn en savoir plus sur un réseau virtuel, consultez [un réseau virtuel](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn en savoir plus sur la sauvegarde et de récupération, consultez [continuité](sql-database-business-continuity.md).    
* toolearn en savoir plus sur l’analyse ppols, consultez [pools d’analyse](sql-database-elastic-pool-manage-portal.md).    
* toolearn en savoir plus sur Umbraco en tant que Service, consultez [Umbraco](https://umbraco.com/cloud).

