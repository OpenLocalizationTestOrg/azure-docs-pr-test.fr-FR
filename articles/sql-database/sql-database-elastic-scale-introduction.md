---
title: "aaaScaling out avec la base de données SQL Azure | Documents Microsoft"
description: "Logiciel en tant qu’un développeurs de Service (SaaS) permettre facilement créer élastique, bases de données évolutives Bonjour cloud à l’aide de ces outils"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Montée en charge avec la base de données SQL Azure
Vous pouvez faire évoluer facilement les bases de données SQL Azure à l’aide de hello **base de données élastique** outils. Ces outils et fonctionnalités vous permettent d’utiliser hello virtuellement illimitée ressources de la base de données **base de données SQL Azure** toocreate des solutions pour les charges de travail transactionnelles et en particulier les logiciels en tant qu’une application de Service (SaaS). Les fonctionnalités de base de données élastiques sont composent des éléments suivants de hello :

* [Bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md): bibliothèque du client hello est une fonctionnalité qui vous permet de toocreate et de gérer des bases de données partitionnées.  Voir [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md).
* [Outil de fractionnement et de fusion de base de données élastique](sql-database-elastic-scale-overview-split-and-merge.md): cet outil vous permet de déplacer les données entre les différentes bases de données partitionnées. Cela est utile pour le déplacement des données à partir d’une architecture mutualisée de base de données tooa locataire unique de base de données (ou vice versa). Consultez le [Didacticiel d’outil de fusion et de fractionnement de bases de données élastiques](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Les travaux de base de données élastiques](sql-database-elastic-jobs-overview.md) (version préliminaire) : utilisez des travaux toomanage un grand nombre de bases de données SQL Azure. Exécutez facilement les opérations administratives telles que les modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte télémétrique du client (customer) à l’aide des tâches.
* [Requête de base de données élastique](sql-database-elastic-query-overview.md) (version préliminaire) : vous permet de requête toorun Transact-SQL qui s’étend sur plusieurs bases de données. Ainsi, les outils tels que Excel, Power BI, Tableau, etc. tooreporting les connexions.
* [Transactions élastiques](sql-database-elastic-transactions-overview.md): cette fonctionnalité vous permet de toorun les transactions qui s’étendent sur plusieurs bases de données dans la base de données SQL Azure. Transactions de base de données élastique sont disponibles pour les applications .NET à l’aide d’ADO .NET et s’intégrer à hello programmation vous est familier à l’aide de hello [System.Transaction classes](https://msdn.microsoft.com/library/system.transactions.aspx).

graphique de Hello ci-dessous illustre une architecture qui inclut hello **les fonctionnalités de base de données élastique** dans la collection de tooa de relation de bases de données.

Dans ce graphique, les couleurs de base de données hello représentent des schémas. Bases de données avec hello même partage de couleur hello même schéma.

1. Un ensemble de **bases de données SQL Azure** est hébergé sur Azure avec une architecture de partitionnement.
2. Hello **bibliothèque cliente de base de données élastique** toomanage utilisé une partition n’est définie.
3. Un sous-ensemble des bases de données hello sont placés dans un **pool élastique**. (Voir [Qu’est-ce qu’un pool ?](sql-database-elastic-pool.md)).
4. Une **tâche de base de données élastique** exécute des scripts T-SQL planifiés ou ad hoc sur toutes les bases de données.
5. Hello **outil de fusion et fractionnement** toomove utilisé des données à partir d’une seule partition tooanother.
6. Hello **requête de base de données élastique** vous permet de toowrite une requête qui s’étend sur toutes les bases de données dans l’ensemble de partitions hello.
7. **Transactions élastiques** vous permet de toorun les transactions qui s’étendent sur plusieurs bases de données. 

![Outils de base de données élastique][1]

## <a name="why-use-hello-tools"></a>Pourquoi utiliser les outils hello ?
Obtenir l’élasticité et l’évolutivité pour les applications cloud a été simple pour les machines virtuelles et le stockage d’objets blob. En effet, il suffit d’ajouter ou de soustraire des unités, ou d’augmenter la puissance. Mais cela reste un défi pour le traitement des informations de bases de données relationnelles. Des difficultés sont apparues dans les scénarios suivants :

* Agrandissement et réduction de la capacité pour une partie de base de données relationnelle hello de votre charge de travail.
* Gestion des zones réactives susceptibles de survenir et d’affecter un sous-ensemble de données spécifique, comme un client final très occupé (locataire).

En règle générale, les scénarios, tels que ceux-ci ont été traités en investissant dans une application de base de données de plus grande échelle serveurs toosupport hello. Toutefois, cette option est limitée dans le cloud hello où tout le traitement se produit sur du matériel standard prédéfinis. Au lieu de cela, distribution des données et de traitement sur plusieurs bases de données structurées de façon identique (modèle de montée en puissance parallèle appelé « partitionnement ») fournit une alternative tootraditional approches de montée en puissance parallèle à la fois en termes de coût et l’élasticité.

## <a name="horizontal-and-vertical-scaling"></a>Mise à l’échelle horizontale et verticale
Hello figure ci-dessous hello des dimensions horizontales et verticales de la mise à l’échelle, qui sont des bases de données élastiques hello peuvent être monté en manières hello.

![Comparaison entre la montée en charge horizontale et verticale][2]

Mise à l’échelle horizontale fait référence tooadding ou suppression de bases de données dans la capacité de tooadjust de commande ou des performances globales. Cette procédure est fréquemment appelée « montée en charge ». Un tooimplement commun de façon horizontale le partitionnement, dans lequel les données sont partitionnées sur une collection de bases de données structurées de façon identique, est mise à l’échelle.  

Mise à l’échelle verticale fait référence tooincreasing ou en diminuant le niveau de performance hello d’une base de données individuel, il est également connu sous « montée en puissance. »

La plupart des applications de base de données à l’échelle du cloud associent ces deux stratégies. Par exemple, un logiciel en tant qu’une application de Service peut utiliser horizontal mise à l’échelle tooprovision nouveaux utilisateurs finaux et évolution tooallow de chaque client base de données toogrow ou réduction ressources selon les besoins de la charge de travail hello verticale.

* Mise à l’échelle horizontale est géré à l’aide de hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md).
* Mise à l’échelle verticale s’effectue à l’aide de la couche de service Azure PowerShell cmdlets toochange hello, ou en plaçant les bases de données dans un pool élastique.

## <a name="sharding"></a>Partitionnement
*Partitionnement* est une technique toodistribute grandes quantités de données de structure identique sur un nombre de bases de données indépendantes. Il est particulièrement populaire auprès des développeurs cloud qui créent des offres Software as a Service (SAAS) pour les clients finaux ou les entreprises. Ces clients sont souvent tooas référencé « clients ». Le partitionnement peut être nécessaire pour plusieurs raisons :  

* quantité totale de Hello de données est trop grande toofit aux contraintes de hello d’une base de données
* débit des transactions Hello Hello charge de travail globale dépasse les capacités de hello d’une base de données
* Les locataires peuvent nécessiter une isolation physique l'un de l'autre, donc des bases de données distinctes sont nécessaires pour chaque locataire
* Différentes sections d’une base de données peut-être tooreside dans des zones géographiques différentes pour des raisons géopolitiques, de performances ou de conformité.

Dans d’autres scénarios, tels que la réception de données à partir des appareils distribués, partitionnement peut être utilisé toofill un ensemble de bases de données qui sont organisées rapprochée. Par exemple, une base de données distincte peut être dédié tooeach jour ou semaine. Dans ce cas, clé de partitionnement hello peut être une date hello représentant entier et (présente dans toutes les lignes des tables partitionnées de hello) et les requêtes qui retournent des informations pour une plage de dates doivent être acheminés par un sous-ensemble de toohello application hello des bases de données couvrant la plage hello dans question.

Partitionnement fonctionne mieux lorsque toutes les transactions dans une application peuvent être restreint tooa valeur d’une clé de partitionnement unique. Cela garantit que toutes les transactions seront tooa local de base de données spécifique.

## <a name="multi-tenant-and-single-tenant"></a>Architecture mutualisée et architecture à un seul locataire
Certaines applications utilisent l’approche la plus simple de hello de création d’une base de données distincte pour chaque client. Il s’agit de hello **modèle de partitionnement d’un seul locataire** qui offre une isolation, possibilité de sauvegarde/restauration et mise à l’échelle au niveau de granularité hello du client de hello de ressource. Avec le partitionnement par locataire unique, chaque base de données est associé à une valeur d’ID client spécifique (ou la valeur de clé de client), mais cette clé ne sont pas toujours nécessairement présente dans les données hello lui-même. Il est hello tooroute de responsabilité de l’application de chaque demande toohello appropriés de base de données - et bibliothèque cliente de hello peut simplifier cet affichage.

![Comparaison entre l’architecture à locataire unique et l’architecture mutualisée][4]

D'autres scénarios regroupent plusieurs locataires dans des bases de données, plutôt que de les isoler dans des bases de données distinctes. Il s’agit d’un type **modèle de partitionnement de l’architecture mutualisée** - et il peut piloté par le fait de hello qu’une application gère le grand nombre de clients très faible. Dans le partitionnement de l’architecture mutualisée, lignes hello dans les tables de base de données hello sont que tous conçus toocarry une clé identifiant la clé ID ou le partitionnement du locataire hello. Là encore, couche d’application hello est responsable du routage de base de données d’un client demande toohello appropriée, et cela peut être pris en charge par la bibliothèque cliente de base de données élastique hello. En outre, sécurité de niveau ligne peut être utilisé toofilter quelles lignes de chaque client puisse accéder aux - pour plus d’informations, consultez [applications mutualisées avec les outils de base de données élastique et de sécurité de niveau ligne](sql-database-elastic-tools-multi-tenant-row-level-security.md). Redistribution des données entre les bases de données peut être nécessaire avec le modèle de partitionnement de l’architecture mutualisée hello, et cette opération est facilitée par l’outil de fusion et fractionnement de base de données élastique hello. toolearn savoir plus sur les modèles de conception pour les applications SaaS à l’aide de pools élastiques, consultez [des modèles de conception pour les Applications SaaS mutualisée avec la base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Déplacement des données à partir de plusieurs bases de données toosingle-location
Lorsque vous créez une application SaaS, il est prospects toooffer classique une version d’évaluation du logiciel de hello. Dans ce cas, il est économique toouse une base de données de plusieurs locataire pour les données de salutation. Toutefois, lorsqu'un prospect devient un client, une base de données à un seul locataire est préférable car elle offre de meilleures performances. Si le client de hello a créé les données pendant la période d’évaluation de hello, utilisez hello [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) données hello toomove hello mutualisée toohello nouveau locataire unique de base de données.

## <a name="next-steps"></a>Étapes suivantes
Pour un exemple d’application qui illustre la bibliothèque cliente de hello, consultez [prise en main des outils de base de données TSO élastique](sql-database-elastic-scale-get-started.md).

tooconvert existant outils de hello toouse des bases de données, consultez [existant de la migration des bases de données montée tooscale](sql-database-elastic-convert-to-use-elastic-tools.md).

caractéristiques de hello toosee du pool élastique de hello, consultez [considérations de prix et de performances pour un pool élastique](sql-database-elastic-pool.md), ou créer un nouveau pool avec [pools élastiques](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

