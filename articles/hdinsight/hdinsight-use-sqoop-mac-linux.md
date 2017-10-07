---
title: aaaApache Sqoop avec Hadoop - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Apache Sqoop tooimport et exportation entre Hadoop dans HDInsight et d’une base de données SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Utilisez Apache Sqoop tooimport et exporter des données entre Hadoop dans HDInsight et de la base de données SQL

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Découvrez comment toouse Apache Sqoop tooimport et exportation entre un Hadoop de cluster Azure HDInsight et de la base de données de base de données SQL Azure ou Microsoft SQL Server. Hello les étapes dans cette hello d’utilisation de document `sqoop` commande directement à partir de nœud principal de hello du cluster Hadoop de hello. Vous utilisez le nœud principal de SSH tooconnect toohello et exécutez des commandes hello dans ce document.

> [!IMPORTANT]
> Hello étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight qui utilisent Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="install-freetds"></a>Installer FreeTDS

1. Utiliser SSH tooconnect toohello HDInsight cluster. Par exemple, hello commande suivante connecte toohello le nœud principal principal d’un cluster nommé `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilisez hello suivant commande tooinstall FreeTDS :

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    FreeTDS est utilisé dans plusieurs étapes de tooconnect tooSQL de base de données.

## <a name="create-hello-table-in-sql-database"></a>Créer la table de hello dans la base de données SQL

> [!IMPORTANT]
> Si vous utilisez un cluster HDInsight de hello et base de données SQL créée dans [créer le cluster et la base de données SQL](hdinsight-use-sqoop.md), ignorez les étapes hello dans cette section. Hello base de données et la table ont été créées comme partie de hello étapes Bonjour [créer le cluster et la base de données SQL](hdinsight-use-sqoop.md) document.

1. À partir de la session SSH de hello, utilisez hello suivant du serveur de base de données SQL de commande tooconnect toohello.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Vous recevez toohello similaire de sortie suivant du texte :

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. À hello `1>` invite, entrez hello suivant la requête :

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    Hello lorsque `GO` instruction est entrée, les instructions précédentes hello sont évaluées. Tout d’abord, hello **mobiledata** table est créée, puis un index cluster est ajouté tooit (requis par la base de données SQL).

    Hello utilisation suivant tooverify de requête qui hello table a été créé :

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Vous consultez toohello similaire de sortie suivant du texte :

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Entrez `exit` à hello `1>` tooexit hello tsql utilitaire d’invite.

## <a name="sqoop-export"></a>Exportation de Sqoop

1. Cluster de toohello connexion hello SSH, utilisez hello suivant tooverify commande que Sqoop peut voir votre base de données SQL :

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    Lorsque vous y êtes invité, entrez le mot de passe de hello pour la connexion de base de données SQL hello.

    Cette commande renvoie une liste des bases de données, y compris hello **sqooptest** base de données que vous avez créé précédemment.

2. données tooexport **hivesampletable** toohello **mobiledata** table, utilisez hello de commande suivante :

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Cette commande ordonne à Sqoop tooconnect toohello **sqooptest** base de données. Sqoop exporte ensuite les données à partir de **wasb : / / / hive/entrepôt/hivesampletable** toohello **mobiledata** table.

    > [!IMPORTANT]
    > Utilisez `wasb:///` si le stockage par défaut de hello pour votre cluster est un compte de stockage Azure. Utilisez `adl:///` s’il s’agit d’un Azure Data Lake Store.

3. Après la commande hello, utilisez hello suivant commande tooconnect toohello de base de données à l’aide de TSQL :

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Une fois connecté, hello utilisation suivant les instructions tooverify qui hello de données a été exporté toohello **mobiledata** table :

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Vous devez voir une liste de données de table de hello. Type `exit` utilitaire de tooexit hello tsql.

## <a name="sqoop-import"></a>Importation de Sqoop

1. Suivant de hello utilisez commande tooimport des données à partir de hello **mobiledata** table dans la base de données SQL, toohello **wasb : / / / didacticiels/usesqoop/importeddata** répertoire HDInsight :

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    champs de Hello dans les données de salutation sont séparés par un caractère de tabulation et les lignes hello sont terminent par un caractère de nouvelle ligne.

2. Une fois l’importation de hello terminée, utilisez hello suivant toolist commande données hello dans le répertoire hello :

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Utilisation de SQL Server

Vous pouvez également utiliser Sqoop tooimport et exporter des données à partir de SQL Server, dans votre centre de données ou sur une Machine virtuelle hébergée dans Azure. Hello les différences entre l’utilisation de la base de données SQL et SQL Server sont :

* HDInsight et SQL Server doit être sur hello même réseau virtuel Azure.

    Pour obtenir un exemple, consultez hello [réseau de se connecter de HDInsight tooyour local](./connect-on-premises-network.md) document.

    Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel Azure, consultez hello [HDInsight d’étendre avec un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md) document. Pour plus d’informations sur un réseau virtuel Azure, consultez hello [présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md) document.

* SQL Server doit être configuré tooallow l’authentification SQL. Pour plus d’informations, consultez hello [choisir un Mode d’authentification](https://msdn.microsoft.com/ms144284.aspx) document.

* Vous pouvez avoir des connexions à distance du tooaccept tooconfigure SQL Server. Pour plus d’informations, consultez hello [moteur de base de toohello de connexion tootroubleshoot SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.

* Créer hello **sqooptest** base de données dans SQL Server à l’aide d’un utilitaire tel que **SQL Server Management Studio** ou **tsql**. étapes de Hello pour l’utilisation de hello CLI d’Azure fonctionnent uniquement pour la base de données SQL Azure.

    Hello utilisation suivant hello de toocreate d’instructions Transact-SQL **mobiledata** table :

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* Lors de la connexion toohello SQL Server à partir de HDInsight, vous avez peut-être l’adresse IP toouse hello hello SQL Server. Par exemple :

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Limites

* L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.

* Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse Sqoop. toolearn, voir :

* [Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie] : utilisez l’action Sqoop dans un workflow Oozie.
* [Analyser des données de retard de vol avec HDInsight][hdinsight-analyze-flight-data]: utiliser la ruche de vol de tooanalyze retarder des données et ensuite utiliser la base de données Sqoop tooexport données tooan SQL Azure.
* [Télécharger des données tooHDInsight][hdinsight-upload-data]: trouver d’autres méthodes pour le téléchargement des données tooHDInsight/Azure Blob storage.

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
