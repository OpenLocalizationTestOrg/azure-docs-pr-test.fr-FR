---
title: "aaaWhat est un entrepôt de données SQL Azure ? | Microsoft Docs"
description: "Base de données distribuée dédiée aux entreprises qui prend en charge le traitement de pétaoctets de données relationnelles et non relationnelles. Il s’agit de hello première cloud entrepôt de données avec croissance, réduire et suspendre en quelques secondes."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>En quoi consiste Azure SQL Data Warehouse ?
Azure SQL Data Warehouse est une base de données relationnelle de mise à l’échelle basée sur le cloud à traitement massivement parallèle (MPP, Massively Parallel Processing) qui prend en charge le traitement de grands volumes de données. 

SQL Data Warehouse :

* Combine la base de données relationnelle hello SQL Server avec les fonctionnalités de montée en puissance parallèle de cloud Azure. 
* Découple le stockage du calcul.
* Active l’augmentation, la réduction, la suspension ou la reprise du calcul. 
* S’intègre dans hello plateforme Azure.
* Utilise SQL Server Transact-SQL (T-SQL) et les outils.
* Est conforme à différentes exigences juridiques et commerciales de sécurité telles SOC et ISO.

Cet article décrit les principales fonctionnalités de hello d’entrepôt de données SQL.

## <a name="massively-parallel-processing-architecture"></a>Architecture Massively Parallel Processing
SQL Data Warehouse est un système de base de données distribuée à traitement massivement parallèle. Coulisses de hello, entrepôt de données SQL permet de répartir vos données sur de nombreux sans partage stockage et les unités de traitement. les données de salutation sont stockées dans une couche de stockage localement redondant Premium sur lequel les nœuds de calcul liées dynamiquement exécutent des requêtes. Utilise SQL Data Warehouse qu'un toorunning approche « diviser pour mieux régner » charge et des requêtes complexes. Les demandes sont reçues par un nœud de contrôle, optimisée pour la distribution et ensuite transmis tooCompute nœuds toodo leur travail en parallèle.

Avec le stockage découplé et le calcul, SQL Data Warehouse peut :

* Agrandir ou réduire la taille du stockage indépendant de calcul.
* Augmenter ou réduire la puissance de calcul sans déplacement de données.
* Suspendre le calcul tout en conservant les données intactes, afin de ne payer que le stockage.
* Reprendre le calcul pendant les heures d’utilisation.

Hello diagramme suivant illustre hello architecture plus en détail.

![Architecture de SQL Data Warehouse][1]

**Nœud de contrôle :** nœud de contrôle hello gère et optimise les requêtes. Il est frontal hello interagit avec toutes les applications et les connexions. Dans l’entrepôt de données SQL, nœud de contrôle hello est rendue possible par la base de données SQL et la connexion tooit recherche et hello même. Sous l’aire de hello, nœud de contrôle hello coordonne tous les mouvements de données hello et calcul requis toorun des requêtes parallèles sur vos données distribuées. Lorsque vous soumettez un tooSQL de requête T-SQL Data Warehouse, nœud de contrôle hello le transforme en requêtes distinctes qui s’exécutent sur chaque nœud de calcul en parallèle.

**Nœuds de calcul :** les nœuds de calcul hello servent power hello derrière l’entrepôt de données SQL. Il s’agit de bases de données SQL qui stockent vos données et traitent votre requête. Lorsque vous ajoutez des données, SQL Data Warehouse distribue les nœuds de calcul tooyour hello lignes. les nœuds de calcul Hello sont des travailleurs hello qui exécutent des requêtes parallèles hello sur vos données. Après traitement, elles passent de nœud de contrôle hello résultats toohello précédent. requête de hello toofinish, nœud de contrôle hello regroupe les résultats de hello et retourne hello résultat final.

**Stockage :** les données sont stockées dans Azure Blob Storage. Lorsque les nœuds de calcul interagissent avec vos données, ils écrire et lire des tooand directement depuis le stockage blob. Étant donné que le stockage Azure se développe considérablement et de façon transparente, SQL Data Warehouse faire hello identiques. Étant donné que le calcul et le stockage sont indépendants, SQL Data Warehouse peut automatiquement mettre à l’échelle le stockage séparément du calcul de mise à l’échelle et inversement. Stockage d’objets Blob Azure est également entièrement à tolérance de pannes et rationalise hello sauvegarde et le processus de restauration.

**Service de déplacement de données :** Service de déplacement des données (DMS) déplace les données entre les nœuds de hello. DMS donne hello calcul nœuds accès toodata dont ils ont besoin pour les jointures et agrégations. DMS n’est pas un service Azure. Il est un service Windows qui s’exécute en même temps que la base de données SQL sur tous les nœuds hello. DMS est un processus en arrière-plan avec lequel il est impossible d’interagir directement. Toutefois, vous pouvez examiner plans de requête toosee lorsque les opérations DMS se produisent, étant donné que le déplacement des données sont nécessaire toorun chaque requête en parallèle.

## <a name="optimized-for-data-warehouse-workloads"></a>Optimisé pour les charges de l’entrepôt de données
Hello approche MPP est facilité par plusieurs données entreposage des optimisations de performances spécifiques, y compris :

* Un optimiseur de requêtes distribuées et un ensemble de statistiques complexes sur toutes les données. À l’aide des informations sur la distribution et la taille des données, le service de hello est toooptimize en mesure de requêtes en évaluant les coûts hello d’opérations de requête distribuée spécifique.
* Techniques et des algorithmes avancés intégré dans les données de salutation le déplacement des processus tooefficiently déplacement des données entre les ressources informatiques en tant que requête de hello tooperform nécessaire. Ces opérations de déplacement de données sont générées, et toutes les optimisations toohello Service de déplacement de données se produit automatiquement.
* Des index **columnstore** cluster par défaut. À l’aide de stockage basé sur une colonne, SQL Data Warehouse Obtient des gains de compression x 5 en moyenne par rapport au stockage orienté lignes traditionnel et des too10x ou des gains de performances de requête plus. Requêtes Analytique qui doivent tooscan un grand nombre de lignes fonctionne mieux avec les index columnstore.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Performances prévisibles et évolutives avec des unités DWU (Data Warehouse Units)
SQL Data Warehouse est construit avec des technologies similaires comme SQL Database, ce qui signifie que les utilisateurs peuvent attendre des performances cohérentes et prévisibles pour les requêtes analytiques. Les utilisateurs devraient faire l’échelle des performances toosee linéairement dès leur ajoutent ou soustraire des nœuds de calcul. Allocation de ressources tooyour SQL Data Warehouse est mesurée en unités de l’entrepôt de données (Dwu). Dwu est une mesure des ressources sous-jacentes comme pour processeur, mémoire, e/s, qui sont alloués tooyour SQL Data Warehouse. Nombre hello de Dwu d’augmenter les performances et les ressources. Plus précisément, les DWU sont utilisés pour :

* Vous êtes en mesure de tooscale votre entrepôt de données sans se préoccuper du matériel sous-jacent de hello ou logiciel.
* Vous pouvez prévoir l’amélioration des performances pour le niveau DWU avant de modifier le calcul hello de votre entrepôt de données.
* Hello sous-jacent matérielle et logicielle de votre instance peuvent modifier ou déplacer sans affecter les performances de votre charge de travail.
* Microsoft peut améliorer hello sous-jacent de l’architecture du service de hello sans affecter les performances de hello de votre charge de travail.
* Microsoft rapidement pour améliorer les performances SQL Data Warehouse, d’une manière qui est évolutive et uniformément effets hello système.

Les Data Warehouse Units fournissent une mesure de trois indicateurs qui sont fortement corrélés aux performances de la charge de travail d’entreposage de données. échelle de métriques de charge de travail linéaire avec hello Dwu de clé suivant de Hello.

**Analyse/agrégation :** requête d’entreposage de données standard qui analyse un grand nombre de lignes avant d’effectuer une agrégation complexe. C’est une opération très gourmande en E/S et en ressources processeur.

**Charge :** hello données tooingest de capacité en service de hello. Les charges sont mieux exécutées avec PolyBase à partir d’Azure Storage Blobs ou d’Azure Data Lake. Cette mesure est conçue toostress réseau et les aspects de l’UC du service de hello.

**Créer la Table comme Select (SACT) :** SACT mesure hello capacité toocopy une table. Cela implique la lecture des données à partir du stockage, il répartir des nœuds hello du dispositif de hello d’et de l’écriture de toostorage à nouveau. Cette opération est très gourmande en ressources processeur, E/S et réseau.

## <a name="built-on-sql-server"></a>Basé sur SQL Server
Entrepôt de données SQL est basé sur le moteur de base de données relationnelle SQL Server hello et inclut de nombreuses fonctionnalités hello souhaitées à partir d’un entrepôt de données d’entreprise. Si vous connaissez déjà le T-SQL, il est facile tootransfer votre tooSQL de la base de connaissances l’entrepôt de données. Si vous sont avancées ou simplement la prise en main, les exemples hello dans la documentation de hello peut aider à commencer. En général, vous pouvez considérer moyen hello que nous avons construit des éléments de langage hello d’entrepôt de données SQL comme suit :

* SQL Data Warehouse utilise la syntaxe T-SQL pour de nombreuses opérations. Il prend en charge un large éventail de constructions SQL traditionnelles, telles que les procédures stockées, les fonctions définies par l’utilisateur, le partitionnement de tables, les index et les classements.
* SQL Data Warehouse contient également différentes fonctionnalités SQL Server inédites, notamment les index **columnstore** en cluster, l’intégration PolyBase et l’audit de données (complété par l’évaluation des menaces).
* Certains éléments de langage T-SQL qui sont moins courantes pour les charges de travail d’entreposage de données ou qui sont plus récent tooSQL Server, n’est peut-être pas disponibles actuellement. Pour plus d’informations, consultez hello [documentation de Migration][Migration documentation].

Avec hello Transact-SQL et le vecteur de fonctionnalité entre SQL Server, SQL Data Warehouse, base de données SQL et système de plateforme Analytique, vous pouvez développer une solution adaptée à vos besoins en données. Vous pouvez décider où tookeep vos données, basée sur les performances, sécurité et les exigences de mise à l’échelle et transférer des données selon les besoins entre différents systèmes.

## <a name="data-protection"></a>Protection des données
SQL Data Warehouse stocke l’ensemble des données dans le stockage Azure Premium localement redondant. Plusieurs copies synchrones des données de hello sont conservées hello données locales center tooguarantee transparent des données contre les défaillances localisées. En outre, SQL Data Warehouse sauvegarde automatiquement vos bases de données actives (réactivées) à intervalles réguliers à l’aide d’instantanés Azure Storage. toolearn d’informations sur la sauvegarde et la restauration fonctionne, consultez hello [vue d’ensemble de sauvegarde et de restauration][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Intégré avec les outils Microsoft
SQL Data Warehouse s’intègre également plusieurs outils de hello que les utilisateurs peuvent être familiers de SQL Server. Ces outils incluent :

**Outils SQL Server traditionnels :** SQL Data Warehouse est totalement intégré à SQL Server Analysis Services, Integration Services et Reporting Services.

**Des outils basés sur le cloud :** SQL Data Warehouse peut être intégré à différents services dans Azure, notamment Data Factory, Stream Analytics, Machine Learning et Power BI. Pour une liste plus complète, consultez [Vue d’ensemble des outils intégrés][Integrated tools overview].

**Des outils tiers :** de nombreux fournisseurs d’outils tiers ont certifié l’intégration de leurs outils avec SQL Data Warehouse. Pour obtenir une liste complète, consultez [Partenaires de solutions SQL Data Warehouse][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Scénarios de sources de données hybrides
Polybase vous permet de tooleverage vos données à partir de sources différentes à l’aide de commandes de T-SQL. Polybase vous permet de tooquery des données non relationnelles contenues dans le stockage Blob Azure comme s’il s’agit d’une table normale. Utilisez Polybase tooquery des données non relationnelles ou des données non relationnelles tooimport dans SQL Data Warehouse.

* PolyBase utilise des données non relationnelles tooaccess de tables externes. les définitions de table Hello sont stockées dans l’entrepôt de données SQL et vous pouvez y accéder à l’aide de SQL et outils comme vous accéderiez à normale des données relationnelles.
* PolyBase assure une intégration standard. Il expose hello les mêmes fonctions et fonctionnalités tooall hello sources pris en charge. les données Hello lues par Polybase peuvent être dans différents formats, y compris les fichiers délimités ou ORC.
* PolyBase peut être le stockage d’objets blob utilisé tooaccess qui est également utilisé comme espace de stockage pour un cluster HDInsight. Ce vous donne accès toohello données mêmes avec les outils relationnelles et non relationnelles.

## <a name="sla"></a>Contrat SLA
SQL Data Warehouse offre un contrat de niveau de service pour les produits dans le cadre du Contrat SLA des services en ligne Microsoft. Pour plus d’informations, consultez [SLA pour SQL Data Warehouse][SLA for SQL Data Warehouse]. Pour plus d’informations de contrat SLA sur tous les autres produits, vous pouvez visiter hello [les contrats de niveau de Service] Azure page ou de les télécharger sur hello [licence en Volume] [ Volume Licensing] page. 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous connaissez un peu SQL Data Warehouse, découvrez comment tooquickly [créer un entrepôt de données SQL] [ create a SQL Data Warehouse] et [charger les données d’exemple][load sample data]. Si vous êtes tooAzure nouveau, vous souhaiterez peut-être hello [glossaire Azure] [ Azure glossary] utile lorsque vous rencontrez de nouveaux termes. Ou bien, consultez ces autres ressources de SQL Data Warehouse.  

* [Témoignages de clients]
* [Blogs]
* [Demandes de fonctionnalités]
* [Vidéos]
* [Blogs de l’équipe de conseil clientèle]
* [Création d’un ticket de support]
* [Forum MSDN]
* [Forum Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Création d’un ticket de support]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Témoignages de clients]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogs de l’équipe de conseil clientèle]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Demandes de fonctionnalités]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Forum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vidéos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[les contrats de niveau de Service]: https://azure.microsoft.com/en-us/support/legal/sla/
