---
title: "données aaaCopy entre Data Lake Store et de la base de données SQL Azure à l’aide de Sqoop | Documents Microsoft"
description: "Utiliser des données de toocopy Sqoop entre la base de données SQL Azure et Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Copier des données entre Data Lake Store et une base de données SQL Azure à l’aide de Sqoop
Découvrez comment Apache Sqoop toouse tooimport et exporter des données entre la base de données SQL Azure et Data Lake Store.

## <a name="what-is-sqoop"></a>Qu'est-ce que Sqoop ?
Les applications Big Data sont un choix naturel pour le traitement des données non structurées et semi-structurées, telles que les journaux et les fichiers. Toutefois, il peut également être un besoin de données tooprocess structurées stockées dans les bases de données relationnelles.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) est un outil conçu de tootransfer des données entre les bases de données relationnelles et un référentiel de données volumineuses, tels que Data Lake Store. Vous pouvez l’utiliser tooimport des données à partir d’un système de gestion de base de données relationnelle (SGBDR) comme base de données SQL Azure dans Data Lake Store. Vous pouvez transformer et analyser les données hello à l’aide de charges de travail de données volumineuses et puis exporter les données de salutation dans un SGBDR. Dans ce didacticiel, vous utilisez une base de données SQL Azure en tant que votre base de données relationnelle tooimport/exportation à partir de.

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Cluster HDInsight Azure** avec accès tooa compte Data Lake Store. Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Cet article suppose que vous disposez d’un cluster Linux HDInsight avec accès à Data Lake Store.
* **Base de données SQL Azure**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [créer une base de données SQL Azure](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Les vidéos vous permettent-elles d’apprendre rapidement ?
[Regardez cette vidéo](https://mix.office.com/watch/1butcdjxmu114) sur la façon de toocopy des données entre les objets BLOB de stockage Azure et à l’aide de DistCp Data Lake Store.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Créer des exemples de tables Bonjour base de données SQL Azure
1. toostart, créez deux exemples de tables dans hello de base de données SQL Azure. Utilisez [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello base de données SQL Azure et puis hello d’exécution des requêtes suivantes.

    **Créer Table1**

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    **Créer Table2**

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. Dans **Table1**, ajoutez des exemples de données. Laissez **Table2** vide. Nous importerons des données de **Table1** dans Data Lake Store. Ensuite, nous exporterons les données de Data Lake Store vers **Table2**. Exécutez hello suivant extrait de code.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Sqoop d’utilisation d’un cluster HDInsight avec accès tooData Lake Store
Un cluster HDInsight a déjà des packages de Sqoop hello disponibles. Si vous avez configuré le cluster HDInsight de hello toouse Data Lake Store en tant qu’un stockage supplémentaire, vous pouvez utiliser Sqoop (sans aucune modification de configuration) tooimport/exporter des données entre une base de données relationnelle (dans cet exemple, la base de données SQL Azure) et un magasin Data Lake Store compte.

1. Pour ce didacticiel, nous supposons que vous avez créé un cluster de Linux, vous devez utiliser SSH tooconnect toohello cluster. Consultez [Connect tooa HDInsight de basés sur Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Vérifiez si vous avez accès hello compte Data Lake Store à partir du cluster de hello. Exécutez hello de commande suivante à partir de l’invite de commandes hello SSH :

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Il doit fournir une liste de fichiers/dossiers Bonjour compte Data Lake Store.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Importer des données à partir d’Azure SQL Database dans Data Lake Store
1. Accédez répertoire toohello où Sqoop packages sont disponibles. En règle générale, il s’agit de `/usr/hdp/<version>/sqoop/bin`.
2. Importer les données hello **Table1** dans hello compte Data Lake Store. Utilisez hello selon la syntaxe :

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Notez que **nom-serveur-de base de données-sql** espace réservé représente le nom hello du serveur hello sur lequel la base de données SQL Azure hello s’exécute. **nom de base de données SQL** espace réservé représente le nom de base de données réelle hello.

    Par exemple,


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Vérifiez que hello données ont été transférées compte Data Lake Store de toohello. Exécutez hello de commande suivante :

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Vous devez voir hello suivant de sortie.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Chaque **partie-m -*** fichier correspond ligne tooa dans la table de source de hello, **Table1**. Vous pouvez afficher le contenu de hello partie hello - m-* tooverify de fichiers.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Exporter les données de Data Lake Store dans la base de données SQL Azure
1. Exporter les données de hello de table vide Data Lake Store compte toohello, **Table2**, Bonjour base de données SQL Azure. Utiliser la syntaxe de hello.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Par exemple,


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Vérifiez que hello données a été téléchargée table de base de données SQL toohello. Utilisez [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello base de données SQL Azure et puis hello exécution suivant la requête.

        SELECT * FROM TABLE2

    Cela doit avoir hello suivant de sortie.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Considérations de performances lors de l’utilisation de Sqoop

Pour votre Sqoop de réglage des performances de la tâche toocopy data tooData Lake Store, consultez [document de performances Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Voir aussi
* [Copier des données d’objets BLOB de stockage Azure tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
