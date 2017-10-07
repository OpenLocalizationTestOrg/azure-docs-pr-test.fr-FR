---
title: "données aaaLoad dans Azure SQL Data Warehouse | Documents Microsoft"
description: "Découvrez les scénarios courants de hello pour les données à charger dans l’entrepôt de données SQL. Ceux-ci incluent l’utilisation de PolyBase, d’Azure Blob Storage et de fichiers plats ainsi que l’envoi de disques. Vous pouvez également utiliser des outils tiers."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Chargement de données dans Azure SQL Data Warehouse
Résumé des options de scénario hello et des recommandations pour le chargement des données dans l’entrepôt de données SQL.

Hello plus difficiles le chargement des données est généralement préparation des données de hello pour la charge hello. Azure simplifie le chargement à l’aide du stockage d’objets blob Azure comme une banque de données commune pour un grand nombre de services de hello et à l’aide d’Azure Data Factory le hello tooorchestrate communication et déplacement des données entre des services Azure. Ces processus sont intégrés à la technologie PolyBase qui utilise massivement parallèle du traitement des données de tooload de (MPP) en parallèle à partir du stockage d’objets blob Azure dans SQL Data Warehouse. 

Pour accéder à des didacticiels décrivant le chargement d’exemples de bases de données, consultez l’article [Charger des exemples de données dans SQL Data Warehouse][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Chargement à partir d’Azure Blob Storage
Hello plus rapide des tooimport données dans l’entrepôt de données SQL sont toouse PolyBase les données de tooload depuis le stockage blob Azure. PolyBase utilise SQL Data Warehouse traitement hautement parallèle des données de tooload de conception (MPP) en parallèle à partir du stockage d’objets blob Azure. toouse PolyBase, vous pouvez utiliser les commandes T-SQL ou un pipeline Azure Data Factory.

### <a name="1-use-polybase-and-t-sql"></a>1. Utilisation de PolyBase et de T-SQL
Résumé du processus de chargement :

1. Déplacez la Azure Data Lake Store ou le stockage d’objets blob de données tooAzure et stockez-le dans des fichiers texte.
2. Configurer des objets externes dans l’emplacement de l’entrepôt de données SQL toodefine hello et un format de données de hello
3. Exécuter les données de salutation tooload une commande T-SQL en parallèle dans une nouvelle table de base de données.

<!-- 5. Schedule and run a loading job. --> 

Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Utilisation d’Azure Data Factory
Pour un moyen plus simple toouse PolyBase, vous pouvez créer un pipeline Azure Data Factory qui utilise des données de tooload PolyBase à partir du stockage d’objets blob Azure dans SQL Data Warehouse. Il s’agit de tooconfigure rapide, car vous n’avez pas besoin d’objets de toodefine hello T-SQL. Si vous avez besoin des données externes tooquery hello sans les importer, utilisez T-SQL. 

Résumé du processus de chargement :

1. Déplacez votre stockage d’objets blob de données tooAzure et stockez-le dans des fichiers texte. (Azure Data Factory ne prend pas en charge la connectivité ADLS avec PolyBase pour le moment.)
2. Créer une pipeline Azure Data Factory tooingest des données hello. Utilisez l’option de PolyBase hello.
4. Planifier et exécuter le pipeline de hello.

Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Chargement à partir de SQL Server
tooload tooSQL de SQL Server Data Warehouse, vous pouvez utiliser Integration Services (SSIS), transfert de fichiers plats ou expédier les disques tooMicrosoft. Lire un résumé de hello différent du chargement de processus et les liens tootutorials sur toosee.

tooplan une migration complète des données à partir de SQL Server tooSQL entrepôt de données, consultez hello [présentation de la Migration][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Utilisation d’Integration Services (SSIS)
Si vous utilisez déjà tooload de packages Integration Services (SSIS) dans SQL Server, vous pouvez mettre à jour votre toouse de packages SQL Server en tant que source de hello et l’entrepôt de données SQL en tant que destination de hello. Cela est rapide et facile toodo, et constitue un bon choix si vous n’essayez pas toomigrate votre chargement traiter les données toouse déjà dans le cloud de hello. compromis de Hello est la charge de hello sera plus lente que l’utilisation de PolyBase, car cette SSIS n’effectue pas de charge de hello en parallèle.

Résumé du processus de chargement :

1. Passez en revue votre instance de SQL Server Integration Services package toopoint toohello pour la source de hello et base de données de l’entrepôt de données SQL hello pour la destination de hello.
2. Migrez votre tooSQL schéma entrepôt de données, s’il n’y ne figure pas déjà.
3. Mappage de hello de modification dans vos packages d’utiliser uniquement les types de données de hello sont pris en charge par SQL Data Warehouse.
4. Planifier et exécuter le package de hello.

Pour obtenir un didacticiel, consultez [charger des données à partir de SQL Server tooAzure l’entrepôt de données SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>Utilisation d’AZCopy (recommandé pour des données de moins de 10 To)
Si la taille de vos données est < 10 To, vous pouvez exporter les données de salutation à partir de fichiers tooflat de SQL Server, copiez le stockage d’objets blob tooAzure hello fichiers et ensuite utiliser les données de salutation tooload PolyBase dans SQL Data Warehouse

Résumé du processus de chargement :

1. Utiliser les données de tooexport salutation bcp utilitaire de ligne de commande à partir de fichiers tooflat de SQL Server.
2. Utiliser des données de toocopy hello AZCopy utilitaire de ligne de commande de stockage d’objets blob tooAzure fichiers plats.
3. Utilisez PolyBase tooload dans SQL Data Warehouse.

Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Utilisation de bcp
Si vous avez une petite quantité de données, vous pouvez utiliser bcp tooload directement dans l’entrepôt de données SQL Azure.

Résumé du processus de chargement :

1. Utiliser les données de tooexport salutation bcp utilitaire de ligne de commande à partir de fichiers tooflat de SQL Server.
2. Utiliser les données de tooload de bcp de plat les fichiers directement tooSQL l’entrepôt de données.

Pour obtenir un didacticiel, consultez [charger des données à partir de SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Utilisation des fonctions d’importation/exportation (recommandé pour les données supérieures à 10 To)
Si la taille de vos données est de 10 To > et que vous souhaitez toomove il tooAzure, nous vous recommandons d’utiliser notre service d’expédition de disque [Import/Export][Import/Export]. 

Résumé du processus de chargement :

1. Utiliser données tooexport de hello bcp utilitaire de ligne de commande à partir de fichiers tooflat de SQL Server sur des disques transférables.
2. Expédier hello disques tooMicrosoft.
3. Microsoft charge les données de salutation dans SQL Data Warehouse

## <a name="load-from-hdinsight"></a>Charger à partir de HDInsight
SQL Data Warehouse prend en charge le chargement des données à partir de HDInsight par le biais de PolyBase. processus de Hello est hello identique à celui du chargement de données à partir du stockage d’objets Blob Azure - à l’aide de données de PolyBase tooconnect tooHDInsight tooload. 

### <a name="1-use-polybase-and-t-sql"></a>1. Utilisation de PolyBase et de T-SQL
Résumé du processus de chargement :

1. Déplacez votre tooHDInsight de données et les stocker dans des fichiers texte, format ORC ou Parquet.
2. Configurer des objets externes dans l’emplacement de l’entrepôt de données SQL toodefine hello et un format de données de hello.
3. Exécuter les données de salutation tooload une commande T-SQL en parallèle dans une nouvelle table de base de données.

Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Recommandations
La plupart de nos partenaires proposent des solutions de chargement. toofind plus d’informations, consultez une liste de nos [les partenaires de solutions][solution partners]. 

Si vos données provenant d’une source non relationnelle et que vous souhaitez tooload dans des données SQL de l’entrepôt vous devez tootransform dans les lignes et les colonnes avant de les charger. les données de salutation transformée n’a pas besoin toobe stockée dans une base de données, il peut être stocké dans des fichiers texte.

Créer des statistiques sur des données nouvellement chargées. Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.  Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important toocreate des statistiques sur toutes les colonnes de toutes les tables après hello d’abord chargement ou de toutes les modifications importantes se produisent dans les données de salutation.  Pour plus d’informations, consultez [Statistiques][Statistics].

## <a name="next-steps"></a>Étapes suivantes
Pour plus de conseils de développement, consultez hello [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
