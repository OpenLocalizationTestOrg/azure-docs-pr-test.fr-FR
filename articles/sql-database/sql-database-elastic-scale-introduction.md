---
title: "Montée en charge avec la base de données SQL Azure | Microsoft Docs"
description: "Les développeurs de Software as a Service (SaaS) peuvent facilement créer des bases de données élastiques et évolutives dans le cloud à l'aide de ces outils"
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
ms.openlocfilehash: 5bb6d17ffd047ae91476c52750f293414d1dfdd5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Montée en charge avec la base de données SQL Azure
Vous pouvez facilement faire évoluer les bases de données SQL Azure à l’aide des outils de **base de données élastique** . Ces outils et fonctionnalités vous permettent d’utiliser les ressources quasi illimitées de la **base de données SQL Azure** pour créer des solutions pour les charges de travail transactionnelles et notamment les applications Software as a Service (SaaS). Les fonctionnalités de base de données élastique se composent des éléments suivants :

* [Bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md): la bibliothèque cliente est une fonctionnalité qui vous permet de créer et de gérer des bases de données partitionnées.  Voir [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md).
* [Outil de fractionnement et de fusion de base de données élastique](sql-database-elastic-scale-overview-split-and-merge.md): cet outil vous permet de déplacer les données entre les différentes bases de données partitionnées. Il est particulièrement utile pour déplacer des données d’une base de données mutualisée vers une base de données à un seul locataire (ou inversement). Consultez le [Didacticiel d’outil de fusion et de fractionnement de bases de données élastiques](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Tâches de base de données élastique](sql-database-elastic-jobs-overview.md) (version préliminaire) : utilisez des tâches pour gérer un grand nombre de bases de données SQL Azure. Exécutez facilement les opérations administratives telles que les modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte télémétrique du client (customer) à l’aide des tâches.
* [Requête de base de données élastique](sql-database-elastic-query-overview.md) (version préliminaire) : vous permet d’exécuter une requête Transact-SQL qui s’étend sur plusieurs bases de données. Cela permet une connexion à des outils de création de rapports comme Excel, PowerBI, Tableau, etc.
* [Transactions élastiques](sql-database-elastic-transactions-overview.md): cette fonctionnalité vous permet d’exécuter des transactions qui s’étendent sur plusieurs bases de données dans Azure SQL Database. Ces transactions sont disponibles pour les applications .NET utilisant ADO .NET et s’intègrent à une expérience de programmation familière basée sur les [classes System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx).

L’illustration ci-dessous montre une architecture qui inclut les **fonctionnalités de base de données élastique** liées à une collection de bases de données.

Dans ce graphique, les couleurs de la base de données représentent des schémas. Les bases de données de même couleur partagent le même schéma.

1. Un ensemble de **bases de données SQL Azure** est hébergé sur Azure avec une architecture de partitionnement.
2. La **bibliothèque cliente de base de données élastique** sert à gérer un ensemble de partitions.
3. Un sous-ensemble des bases de données est placé dans un **pool élastique**. (Voir [Qu’est-ce qu’un pool ?](sql-database-elastic-pool.md)).
4. Une **tâche de base de données élastique** exécute des scripts T-SQL planifiés ou ad hoc sur toutes les bases de données.
5. L’ **outil de fusion et fractionnement** sert à déplacer des données d’une partition à l’autre.
6. La **requête de base de données élastique** vous permet d’écrire une requête qui s’étend sur toutes les bases de données de l’ensemble de partitions.
7. **Transactions élastiques** vous permet d’exécuter des transactions qui s’étendent sur plusieurs bases de données. 

![Outils de base de données élastique][1]

## <a name="why-use-the-tools"></a>Pourquoi utiliser les outils ?
Obtenir l’élasticité et l’évolutivité pour les applications cloud a été simple pour les machines virtuelles et le stockage d’objets blob. En effet, il suffit d’ajouter ou de soustraire des unités, ou d’augmenter la puissance. Mais cela reste un défi pour le traitement des informations de bases de données relationnelles. Des difficultés sont apparues dans les scénarios suivants :

* Agrandissement et réduction des capacités pour la partie base de données relationnelle de votre charge de travail.
* Gestion des zones réactives susceptibles de survenir et d’affecter un sous-ensemble de données spécifique, comme un client final très occupé (locataire).

Traditionnellement, ces types de scénarios ont été résolus en investissant dans des serveurs de base de données à plus grande échelle de manière à prendre en charge l’application. Toutefois, cette option est limitée dans le cloud où tous les traitements se produisent sur un matériel prédéfini. La distribution des données et le traitement sur plusieurs bases de données ayant la même structure (un schéma de montée en charge connu sous le terme « partitionnement ») constituent une alternative aux approches traditionnelles de montée en charge, à la fois en matière de coût et d’élasticité.

## <a name="horizontal-and-vertical-scaling"></a>Mise à l’échelle horizontale et verticale
La figure ci-dessous illustre les dimensions horizontales et verticales de la mise à l'échelle, qui représentent les méthodes de base de mise à l'échelle des bases de données élastiques.

![Comparaison entre la montée en charge horizontale et verticale][2]

La mise à l’échelle horizontale fait référence à l’ajout ou la suppression des bases de données afin d’ajuster les capacités ou les performances globales. Cette procédure est fréquemment appelée « montée en charge ». Le partitionnement est une approche courante de mise à l’échelle horizontale, dans laquelle les données sont partitionnées sur une collection de bases de données structurées de manière identique.  

La mise à l’échelle verticale fait référence à l’augmentation ou à la réduction du niveau de performance d’une base de données individuelle et est également appelée « mise à l’échelle vers le haut ».

La plupart des applications de base de données à l’échelle du cloud associent ces deux stratégies. Par exemple, une application Software as a Service peut utiliser la mise à l’échelle horizontale pour approvisionner les nouveaux clients finaux et la mise à l’échelle verticale pour permettre l’augmentation ou la diminution des ressources de la base de données du client final, en fonction des besoins de la charge de travail.

* La mise à l’échelle horizontale est gérée à l’aide de la [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md).
* La mise à l’échelle verticale est effectuée à l’aide des applets de commande Azure PowerShell pour modifier le niveau de service, ou en plaçant des bases de données dans un pool élastique.

## <a name="sharding"></a>Partitionnement
*Partitionnement* est une technique permettant de distribuer de grandes quantités de données structurées de façon identique entre plusieurs bases de données indépendantes. Il est particulièrement populaire auprès des développeurs cloud qui créent des offres Software as a Service (SAAS) pour les clients finaux ou les entreprises. Ces clients finaux sont souvent appelés « locataires ». Le partitionnement peut être nécessaire pour plusieurs raisons :  

* La quantité totale de données est trop grande pour tenir dans les contraintes d'une base de données unique
* Le débit des transactions de la charge de travail globale dépasse les capacités d'une base de données unique
* Les locataires peuvent nécessiter une isolation physique l'un de l'autre, donc des bases de données distinctes sont nécessaires pour chaque locataire
* Différentes sections d’une base de données peuvent se trouver dans différentes zones géographiques pour des raisons géopolitiques, de performances ou de conformité.

Dans d'autres scénarios, telle la réception de données à partir d'appareils distribués, le partitionnement peut servir à remplir un ensemble de bases de données organisées en fonction du temps. Par exemple, une base de données distincte peut être dédiée à chaque jour ou chaque semaine. Dans ce cas, la clé de partitionnement peut être un entier représentant la date (présente dans toutes les lignes des tables partitionnées) et les requêtes qui retournent des informations pour une plage de dates doivent être acheminées par l’application vers le sous-ensemble de bases de données couvrant la plage en question.

Le partitionnement fonctionne mieux lorsque toutes les transactions d'une application peuvent être limitées à une seule valeur de clé de partitionnement. Cela permet de garantir que toutes les transactions sont locales à une base de données spécifique.

## <a name="multi-tenant-and-single-tenant"></a>Architecture mutualisée et architecture à un seul locataire
Certaines applications utilisent l'approche la plus simple consistant à créer une base de données distincte pour chaque locataire. C’est le **modèle de partitionnement par locataire unique** qui offre des fonctionnalités d’isolation, de sauvegarde/restauration et de mise à l’échelle des ressources au niveau de granularité du locataire. Avec le partitionnement par locataire unique, chaque base de données est associée à une valeur d'identifiant de locataire spécifique (ou la valeur de clé du client), mais il n'est pas nécessaire que cette clé soit toujours présente dans les données elles-mêmes. L’application est responsable de l’acheminement de chaque demande vers la base de données appropriée. Et la bibliothèque cliente peut simplifier cette procédure.

![Comparaison entre l’architecture à locataire unique et l’architecture mutualisée][4]

D'autres scénarios regroupent plusieurs locataires dans des bases de données, plutôt que de les isoler dans des bases de données distinctes. Il s’agit d’un modèle type de **partitionnement à plusieurs locataires** et il peut être nécessaire lorsqu’une application gère un grand nombre de très petits locataires. Dans un partitionnement à plusieurs locataires, les lignes des tables de base de données sont toutes conçues pour comporter une clé identifiant l'ID du locataire ou la clé de partitionnement. Là encore, la couche Application est responsable de l’acheminement de la demande d’un locataire vers la base de données appropriée et la bibliothèque cliente de base de données élastique peut prendre cette procédure en charge. En outre, le dispositif de sécurité au niveau des lignes peut servir à filtrer les lignes auxquelles chaque locataire peut accéder. Pour plus d’informations, consultez [Applications multi-locataires avec des outils de base de données élastique et la sécurité au niveau des lignes](sql-database-elastic-tools-multi-tenant-row-level-security.md). Il peut être nécessaire de redistribuer les données entre les bases de données à l’aide du modèle de partitionnement à plusieurs locataires. L’outil de fusion et de fractionnement des bases de données élastiques permet de faciliter cette procédure. Pour en savoir plus sur les modèles de conception pour les applications SaaS avec des pools élastiques, voir [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)(Modèles de conception pour les applications SaaS mutualisées avec la base de données SQL Azure).

### <a name="move-data-from-multiple-to-single-tenancy-databases"></a>Déplacement de données de bases de données à plusieurs locataires vers des bases de données à un seul locataire
Lorsque vous créez une application SaaS, il est courant d'offrir aux clients potentiels une version d'évaluation du logiciel. Dans ce cas, il est plus rentable d'utiliser une base de données à plusieurs locataires pour les données. Toutefois, lorsqu'un prospect devient un client, une base de données à un seul locataire est préférable car elle offre de meilleures performances. Si le client a créé des données pendant la période d’évaluation, utilisez l’ [outil de fusion et de fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) pour déplacer les données de la base de données à plusieurs locataires vers la nouvelle base de données à un seul locataire.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir un exemple d’application illustrant la bibliothèque cliente, voir [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).

Pour convertir des bases de données existantes afin d’utiliser les outils, voir [Migrer des bases de données existantes pour la montée en charge](sql-database-elastic-convert-to-use-elastic-tools.md).

Pour plus de détails sur le pool élastique, consultez [Considérations sur les prix et performances pour un pool élastique](sql-database-elastic-pool.md) ou créez un pool à l’aide des [pools élastiques](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

