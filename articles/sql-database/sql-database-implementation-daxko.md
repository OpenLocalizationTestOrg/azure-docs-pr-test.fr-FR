---
title: "aaaAzure étude de cas de base de données Azure SQL - Daxko/CSI | Documents Microsoft"
description: "Découvrez Daxko/CSI utilisation tooaccelerate de la base de données SQL son cycle de développement et tooenhance ses services du client et les performances"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI utilisé tooaccelerate Azure son cycle de développement et le tooenhance ses services du client et les performances
![Logo Daxko/CSI](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Logiciel de Daxko/CSI sont confrontés à un défi : sa base de clients de centres de capacité et de recréation a été croissant, réussite de toohello Merci de sa solution complète de logiciels d’entreprise, mais reste au niveau de hello infrastructure informatique a besoin pour cette croissance base de clients a été test société hello personnel informatique. société de Hello a été contraint plus en plus du traitement opérations augmentation, en particulier pour la gestion de ses bases de données. Pire encore, cette surcharge d’opérations a été coupe en ressources de développement pour de nouvelles initiatives, telles que de nouvelles fonctionnalités de mobilité des logiciels de l’entreprise hello.

Selon les tooDavid Molina, directeur du développement de produit à Daxko/CSI, Azure logiciels CSI fournis avec modèle de (PaaS) hello platform-as-a-service qu’il devait toosimplify gestion de base de données, d’améliorer l’évolutivité et de libérer toofocus ressources sur logiciels au lieu d’ops. « Azure SQL Database a représenté une solution très intéressante pour nous. N’ayant ne pas tooworry sur la maintenance d’un serveur SQL Server, un cluster de basculement et hello tous les autres besoins de l’infrastructure est idéale pour nous. »

Étant donné que migration tooAzure, CSI logiciel a besoin d’un personnel chargé des opérations de toomanage uniquement deux sur des bases de données client 600. la société de Hello utilise des pools élastiques de base de données SQL Azure toomove bases de données client en fonction de taille et doivent.

Molina continue, « nos clients semble hello modifier immédiatement. Avant les pools élastiques, ils subissaient parfois des délais d’attente et d’autres problèmes pendant les périodes de pic de charge. Avec les pools élastiques Azure, elles peuvent croître en fonction des besoins et utilisent des logiciel hello sans problème. »

En outre tooimproving des performances pour les clients, les pools élastiques Azure libérées ressources CSI logicielles toofocus sur le développement de nouveaux services et fonctionnalités, au lieu de traitement des opérations et la gestion. Ces ressources informatiques ont aidé CSI logiciel améliorer ses logiciels d’entreprise de l’offre, SpectrumNG, toohelp prendre part aux membres de gym, améliorer l’efficacité du personnel et donner personnel et les membres de l’accès mobile pour des tâches interactives et des notifications en temps réel.

Azure a également permis de CSI logiciel accélérer et améliorer le développement de hello et cycle d’assurance qualité (AQ) en activant les options d’automatisation. Avec l’implémentation Azure de la société hello, gestionnaires de génération peuvent regrouper les composants sur un bouton hello. Comme le décrit Molina, « dans le cadre du cycle de mise en production hello, questions et réponses est désormais environnement de test en mesure de toodeploy tooa dans Azure, qui simule avec précision notre pile de production. Nous pouvons déployer des builds aussitôt tooour dev environnement toovet change. C’est une grande avancée pour nous, car nous n’avions pas de parité de test auparavant. »

## <a name="offloading-toohello-cloud"></a>Déchargement toohello cloud
Avant de déplacer toohello cloud, CSI logiciel avaient correctement créé sa propre infrastructure mutualisées dans un centre de données local à Houston. Sous forme développée de la société de hello, il sont confrontés à des difficultés de croissance croissantes d’achat, la configuration et la gestion de tous les composants matériels de hello et des logiciels nécessaires toosupport ses clients. Les opérations toohandle du personnel informatique est devenu un autre goulot d’étranglement qui a provoqué le ralentissement tooa dans de nouvelles ressources de configuration et de déploiement de nouveaux services toocustomers.

CSI Software a examiné les options offertes par le cloud pour éliminer cette surcharge et ainsi lui permettre de se concentrer sur le code et non sur les questions opérationnelles. Hello entreprise a découvert que la plupart des fournisseurs de cloud supérieur hello n’offrent les solutions infrastructure-as-a-service (IaaS) qui requièrent encore une pile de IaaS hello volumineuse informatique personnel toomanage. En fin de hello, CSI logiciel déterminé que solution de PaaS Azure hello était hello meilleures adapté à ses besoins. Molina explique, « Azure obtient hello matériels et système de logiciels en dehors de la façon de hello, donc nous pouvons nous concentrer sur nos offres de logiciels, tout en réduisant la surcharge informatique. »

## <a name="making-hello-transition-tooazure"></a>Rendre hello transition tooAzure
Après avoir sélectionné Azure pour sa solution PaaS, CSI logiciel a commencé la migration de son cloud de toohello infrastructure et les bases de données principal. TooAzure préalable, SpectrumNG clients nécessaire tooinstall une application cliente qui a communiqué avec un service Windows Communication Foundation (WCF) principal hello. En fonction de tooMolina, « bien que certains clients hébergement tous les éléments dans leurs propres centres de données, nous avons élaboré mutualisée de toobe produit hello. Nous avons tout dans un centre de données à Houston, hébergé à l’aide de SQL Server comme magasin de données hello.

« Nos offres de produits inclus également membre côté portail web (écrit en ASP.net), qui était la présence du client hello conçue toobe toomatch de blanc en partie sur le web et un API SOAP toosupport hello en ligne des pages et intégration de tiers. »

cloud de toohello Hello migration n’a pas eu long pour l’architecture de hello. Selon les tooMolina, « majorité hello d’effort de hello traité modifiant hello façon que nous lire les informations de fichier de configuration, une modification de la chaîne de connexion centralisée, et automatisation hello empaquetage, le téléchargement et le déploiement de nos versions. »

toodevelop hello créer une automatisation, ingénieurs CSI utilisé Azure PowerShell et des API REST toocreate packages Téléchargez-les tooa des environnement intermédiaire pour cette version de chaque nuit.
Hello globale transition tooan déploiement de nuage Azure a rapidement et facilement pour l’équipe informatique de logiciel CSI hello. Molina explique, «, nous avons eu un environnement bêta dans le cloud de hello dans les trois semaines toofour d’effectuer sur le projet de hello. Une telle réussite nous a surpris. »

Une fois la configuration et le test hello environnement, CSI logiciel a commencé à migrer les clients. Pour les clients déjà à l’aide de l’hébergement de logiciels de CSI, transition de hello a été presque transparente. Pour les clients de la migration à partir d’un déploiement sur site, nuage de hello migration toohello a peu de temps, mais était toujours principalement difficulté pour les clients et les logiciels CSI.

Pour les du nouveaux clients, les logiciels CSI personnel informatique utiliser hello suivant le processus tooon-carte les tooAzure :

1. Les scripts PowerShell Azure sont toospin utilisé d’une base de données pour le client de hello ; tous les clients démarrent sur un tooensure de niveau premium suffisamment de débit initiale pour la transition de hello.
2. Lorsque cela est possible, CSI logiciel utilise instance de base de données SQL Azure tooan données existant hello Assistant Migration SQL Azure toomove.
3. Enfin, Microsoft SQL Server Integration Services (SSIS) sont utilisé tooreconcile requis d’un nettoyage de données en tant que toutes les différences dans les données de salutation ou tooperform.

Aujourd’hui, environ 99 % des clients de CSI Software sont hébergés dans Azure, sur quatre centres de données régionaux (Nord-Centre, Sud, Est et Ouest). En ayant des centres de données dans la région géographique de chaque client, la latence est conservée tooa minimale.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Les pools élastiques Azure libèrent des ressources informatiques
Plusieurs fonctionnalités d’Azure ont contribué à CSI logiciel MAJ ne soient pas la fonctionnalité de focus toobeing infrastructure et les opérations et du développement axés. Peut-être l’avantage le plus important hello a été à partir de pools élastiques.

CSI Software fournit actuellement environ 550 bases de données aux clients. Avant de pools élastiques, il était difficile toomanage que de nombreuses bases de données dans une structure de couche. Gestionnaires d’OPS avaient tooassign les niveaux de performance en fonction des besoins de croissance hello de clients, nécessitant d’importantes ressources informatiques surcharge. Avec les pools élastiques, ils peuvent affecter aux locataires un pool Standard ou Premium selon les cas, puis déplacer les clients en fonction de la taille et du besoin. Clients semble effets hello de pools élastiques de hello presque immédiatement. avant de pools élastiques, clients ont rencontré des délais d’attente et d’autres problèmes pendant les périodes de l’utilisation de la croissance, mais avec les pools élastiques, clients peuvent rencontrer des pics d’activité en fonction des besoins et ils peuvent continuer toouse SpectrumNG sans problème.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>La géoréplication active Azure accélère la création de rapports
Plusieurs clients CSI Software tirent également parti de la géoréplication active Azure. Avec la géo-réplication active, les toofour des bases de données secondaires lisibles peuvent être configurés dans hello centre de données identiques ou différentes régions. CSI logiciels utilisent de géo-réplication active de deux manières : tout d’abord, les bases de données secondaires hello sont disponibles dans les cas de hello d’un centre de données hello ou une interruption incapacité tooconnect toohello base de données primaire ; et en second lieu, les bases de données secondaires hello sont lisibles et peuvent être utilisé toooffload les charges de travail en lecture seule telles que travaux de création de rapports. Certains clients de CSI logicielles utilisent ce tooaccelerate avantages des flux de travail de création de rapports.

## <a name="csi-software-application-logic-and-architecture"></a>Architecture et logique des applications de CSI Software
SpectrumNG utilise des rôles Web. Application hello étant mutualisée, un service WCF est la demande de connexion initiale hello toohandle utilisé par les clients. Comme les États Molina, « demande de hello identifie chaque client, qui vous permet de puis nous générer une chaîne de connexion à toodo de bases de données tootheir tout ce que nous devons toodo. »

Pour le niveau de web hello de son service, les logiciels CSI bénéficie de mise à l’échelle automatique Azure, en fonction de la date et l’heure. Les ressources disponibles sont tooaccommodate automatiquement augmentation d’utilisation plus élevé pendant les heures, en fonction du fuseau horaire de toohello de chaque centre de données régional. Ressources sont également définies tooscale vers le bas sur les week-ends, lorsque les besoins des clients sont inférieures.

![Architecture Daxko/CSI](./media/sql-database-implementation-daxko/figure1.png)

Figure 1. Un rôle de travail des services cloud tire des données structurées d’Azure SQL Database et des données semi-structurées du Stockage Table. Les utilisateurs de SpectrumNG interagissent avec ces données par le biais du rôle web des services cloud.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Utilisation d’applications web et d’un niveau Plan web pour les applications mobiles
À l’aide de la base de données SQL Azure libérer des ressources pour les logiciels CSI tooenable nouvelles initiatives, y compris une plateforme mobile complète basée sur une API personnalisée hébergée dans les applications web Azure. plateforme de Hello permet aux membres de gym et planifications de toocheck personnel toouse des appareils mobiles, livre de classes et recevoir des messages.

plateforme Hello utilise tootake d’architecture orientée services (SOA) un seul composant, comme un système de point de vente (PDV) ou un système de ventes, déplacez-le sur le plan web hello tooanother vol et puis accélérons un toosupport service ce composant, tout en laissant tout le reste sur plan du web d’origine Hello. Cette possibilité offre à CSI Software une flexibilité considérable et lui permet de réduire les coûts.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure permet aux développeurs de CSI Software de se concentrer sur les applications et services
Base de données SQL Azure n’est pas simplement un tooSpectrumNG boon utilisateurs, profitez de service rapide et fiable de hello, il est également une grande victoire pour du logiciel CSI personnel informatique et aux développeurs. En déchargeant tooAzure ops dans le cloud de hello, CSI logiciel réduit sa surcharge pour les ressources et d’infrastructure, considérablement accéléré ses cycles de développement et ne nécessite plus de performances de toooptimize toomicromanage bases de données pour ses clients.

## <a name="more-information"></a>Plus d’informations
* toolearn en savoir plus sur les pools élastiques Azure, consultez [pools élastiques](sql-database-elastic-pool.md).
* toolearn en savoir plus sur les outils de base de données et la mise à l’échelle élastique, consultez [mise à l’échelle élastique et les outils de base de données élastique](sql-database-elastic-scale-get-started.md).
* toolearn en savoir plus sur la migration d’une base de données SQL Server, consultez Voir [migrer un tooAzure de la base de données SQL Server](sql-database-cloud-migrate.md).
* toolearn en savoir plus sur la géo-réplication active, consultez [géo-réplication active](sql-database-geo-replication-overview.md).
* toolearn en savoir plus sur les rôles Web et worker, consultez [rôles de travail](../fundamentals-introduction-to-azure.md#compute).    
* toolearn en savoir plus sur le Bus des services Azure, consultez [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn en savoir plus sur l’échelle automatique, consultez [mise à l’échelle des services de cloud computing](../cloud-services/cloud-services-how-to-scale.md).

