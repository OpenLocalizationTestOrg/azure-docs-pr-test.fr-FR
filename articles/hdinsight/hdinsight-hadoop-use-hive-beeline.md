---
title: aaaUse Beeline avec Apache Hive - Azure HDInsight | Documents Microsoft
description: "Découvrez le fonctionnement des requêtes toouse hello Beeline client toorun Hive avec Hadoop dans HDInsight. Beeline est un utilitaire qui permet d’utiliser HiveServer2 sur JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive,hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Utiliser le client de Beeline hello avec Apache Hive

Découvrez comment toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun ruche interroge sur HDInsight.

Beeline est un client de la ruche qui est inclus dans les nœuds principaux d’hello de votre cluster HDInsight. Beeline utilise JDBC tooconnect tooHiveServer2, un service hébergé sur votre cluster HDInsight. Vous pouvez également utiliser Beeline tooaccess Hive dans HDInsight à distance plus hello internet. Hello tableau suivant fournit des chaînes de connexion pour une utilisation avec Beeline :

| Emplacement d’exécution de Beeline | Paramètres |
| --- | --- | --- |
| Un SSH tooa bord ou le nœud principal nœud de connexion | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Cluster en dehors de hello | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Remplacez `admin` avec un compte de connexion de cluster hello pour votre cluster.
>
> Remplacez `password` avec mot de passe hello hello cluster compte de connexion.
>
> Remplacez `clustername` par nom de hello de votre cluster HDInsight.

## <a id="prereq"></a>Configuration requise

* Un cluster Hadoop Linux sur HDInsight.

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un client SSH ou un client Beeline local. La plupart des étapes hello dans ce document suppose que vous utilisez Beeline à partir d’un cluster de toohello session SSH. Pour plus d’informations sur l’exécution de Beeline à partir du cluster en dehors de hello, consultez hello [utiliser Beeline à distance](#remote) section.

    Pour plus d’informations sur l’utilisation de SSH, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Utiliser BeeLine

1. Lors du démarrage de Beeline, vous devez fournir une chaîne de connexion pour HiveServer2 sur votre cluster HDInsight. commande hello de toorun du cluster de hello externe, vous devez également fournir le nom de compte de connexion de cluster hello (valeur par défaut `admin`) et le mot de passe. Utilisez hello suivant table toofind hello connexion chaîne format et les paramètres toouse :

    | Emplacement d’exécution de Beeline | Paramètres |
    | --- | --- | --- |
    | Un SSH tooa bord ou le nœud principal nœud de connexion | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Cluster en dehors de hello | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Par exemple, hello commande suivante peut être utilisé toostart Beeline à partir d’un cluster de toohello session SSH :

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Cette commande démarre le client de Beeline hello et connecte tooHiveServer2 sur le nœud principal du cluster hello. Une fois la commande hello terminée, vous accédez à un `jdbc:hive2://headnodehost:10001/>` invite.

2. Les commandes Beeline commencent par un caractère `!`. Par exemple, `!help` affiche l’aide. Toutefois hello `!` peut être omis pour certaines commandes. Par exemple, `help` fonctionne également.

    Il existe un `!sql`, qui est utilisé tooexecute les instructions HiveQL. Toutefois, HiveQL est couramment utilisé que vous pouvez omettre hello précédent `!sql`. Hello suivant deux instructions est équivalente :

    ```hiveql
    !sql show tables;
    show tables;
    ```

    Sur un nouveau cluster, une seule table est listée : **hivesampletable**.

3. Utilisez hello suivant schéma hello hello hivesampletable commande toodisplay :

    ```hiveql
    describe hivesampletable;
    ```

    Cette commande renvoie hello informations suivantes :

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Cette section décrit les colonnes hello dans la table de hello. Pendant que nous pouvons effectuer des requêtes sur ces données, nous allons plutôt créer un tout nouveau toodemonstrate de table comment les données de tooload dans la ruche et appliquer un schéma.

4. Entrez hello suivant les instructions toocreate une table nommée **log4jLogs** à l’aide des exemples de données fournis avec le cluster HDInsight de hello :

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Ces instructions effectuent hello suivant des actions :

    * `DROP TABLE`-Si la table de hello existe, elle est supprimée.

    * `CREATE EXTERNAL TABLE` : crée une table **externe** dans Hive. Les tables externes ne stockent la définition de table hello Hive. les données de salutation reste dans l’emplacement d’origine de hello.

    * `ROW FORMAT`-Comment les données de salutation sont mis en forme. Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.

    * `STORED AS TEXTFILE LOCATION`-Emplacement de stockage des données de salutation et dans quel format de fichier.

    * `SELECT`-Sélectionne un nombre de toutes les lignes où colonne **t4** contient la valeur de hello **[erreur]**. Cette requête renvoie la valeur **3**, car trois lignes contiennent cette valeur.

    * `INPUT__FILE__NAME LIKE '%.log'`-Ruche tente de fichiers de tooall tooapply hello schéma dans le répertoire de hello. Dans ce cas, le répertoire de hello contient des fichiers qui ne correspondent pas hello schéma. données de garbage tooprevent dans les résultats de hello, cette instruction indique ruche que nous devons retourner uniquement les données à partir de fichiers se terminant par. journal.

  > [!NOTE]
  > Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe. Par exemple, un processus de chargement de données automatisé ou une opération MapReduce.
  >
  > Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.

    la sortie de cette commande est similaire toohello suivant texte Hello :

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. tooexit Beeline, utilisez `!exit`.

## <a id="file"></a>Utilisez Beeline toorun un fichier HiveQL

Utilisez hello suivant les étapes toocreate un fichier, puis l’exécuter à l’aide de Beeline.

1. Toocreate de commande suivant de hello d’utiliser un fichier nommé **query.hql**:

    ```bash
    nano query.hql
    ```

2. Utilisez hello après le texte en tant que contenu hello du fichier de hello. Cette requête crée une table « interne » nommée **errorLogs** :

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Ces instructions effectuent hello suivant des actions :

    * **CREATE TABLE IF NOT EXISTS** -si la table de hello n’existe pas déjà, il est créé. Depuis hello **externe** mot clé n’est pas utilisé, cette instruction crée une table interne. Tables internes sont stockées dans l’entrepôt de données Hive hello et sont gérées entièrement par ruche.
    * **ORC de AS stockées** -stocke les données de hello dans format optimisé lignes en colonnes (ORC). Le format ORC est particulièrement efficace et optimisé pour le stockage de données Hive.
    * **INSERT OVERWRITE ... Sélectionnez** -sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des **[erreur]**, puis insère hello des données dans hello **journaux d’erreurs de** table.

    > [!NOTE]
    > Contrairement aux tables externes, la suppression d’une table interne supprime également des données sous-jacentes hello.

3. fichier de hello toosave, utilisez **Ctrl**+**_X**, puis entrez **Y**et enfin **entrée**.

4. Utilisez hello toorun le fichier hello à l’aide de Beeline suivant :

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Hello `-i` paramètre démarre Beeline, séries hello instructions hello query.hql fichier. Une fois la requête de hello est terminée, vous arrivez à hello `jdbc:hive2://headnodehost:10001/>` invite. Vous pouvez également exécuter un fichier à l’aide de hello `-f` paramètre, qui se termine Beeline une fois hello requête terminée.

5. tooverify hello **journaux d’erreurs** table a été créée, utilisez hello suivant tooreturn instruction tous hello des lignes à partir de **journaux d’erreurs de**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Trois lignes de données doivent normalement être renvoyées. Elles contiennent toutes **[ERROR]** dans la colonne t4 :

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Utiliser Beeline à distance

Si vous avez Beeline installé localement, ou que vous l’utilisez en via une image Docker comme [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), vous devez utiliser hello paramètres suivants :

* __Chaîne de connexion__ : `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Nom de connexion du cluster__ : `-n admin`

* __Mot de passe de connexion du cluster__ : `-p 'password'`

Remplacez hello `clustername` dans la chaîne de connexion hello nom hello de votre cluster HDInsight.

Remplacez `admin` avec nom hello de votre connexion de cluster, puis remplacez `password` avec le mot de passe hello pour votre cluster.

## <a id="sparksql"></a>Utilisez Beeline avec Spark

Spark fournit sa propre implémentation de HiveServer2, qui est souvent serveur Spark Thrift d’indiqué tooas hello. Ce service utilise des requêtes de tooresolve Spark SQL au lieu de la ruche et peut offrir de meilleures performances en fonction de votre requête.

serveur Spark Thrift un Spark sur HDInsight cluster, utilisez port tooconnect toohello `10002` au lieu de `10001`. Par exemple, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> serveur de Spark Thrift Hello est pas directement accessibles sur hello internet. Vous pouvez uniquement vous connecter tooit à partir d’une session SSH ou à l’intérieur de hello même réseau virtuel Azure comme hello cluster HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Étapes suivantes

Pour des informations générales sur Hive dans HDInsight, consultez hello suivant du document :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes que vous pouvez travailler avec Hadoop dans HDInsight, consultez hello suivant des documents :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Si vous utilisez Tez avec Hive, consultez hello suivant des documents :

* [Utilisez hello Tez UI sur HDInsight de basés sur Windows](hdinsight-debug-tez-ui.md)
* [Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
