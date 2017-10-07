---
title: "données de retard de vol aaaAnalyze avec Hive dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse Hive des données de vol tooanalyze sur HDInsight de basés sur Linux, puis exporter hello données tooSQL Sqoop à l’aide de la base de données."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Analyse des données sur les retards de vol avec Hive dans HDInsight basé sur Linux

Découvrez comment les données de retard de vol tooanalyze puis à l’aide de Hive dans HDInsight de basés sur Linux exporter hello tooAzure de données de la base de données SQL à l’aide de Sqoop.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="prerequisites"></a>Composants requis

* **Un cluster HDInsight**. Consultez la rubrique [Prise en main de Hadoop avec Hive dans HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md) pour connaître les étapes de création d’un cluster HDInsight Linux.

* **Base de données SQL Azure**. Vous allez utiliser une base de données SQL Azure comme magasin de données cible. Si vous n'avez pas déjà une base de données SQL, consultez [Didacticiel sur la base de données SQL : Créer une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md).

* **Interface de ligne de commande Azure**. Si vous n’avez pas installé hello CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) pour connaître la procédure.

## <a name="download-hello-flight-data"></a>Télécharger des données de vol hello

1. Parcourir trop[recherche et l’Administration de technologie novatrice, Bureau de statistiques de transport][rita-website].

2. Sur la page de hello, sélectionnez hello valeurs suivantes :

   | Nom | Valeur |
   | --- | --- |
   | Filtre année |2013 |
   | Filtre période |Janvier |
   | Champs |Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Effacez tous les autres champs |

3. Cliquez sur **Télécharger**.

## <a name="upload-hello-data"></a>Télécharger les données de salutation

1. Utilisez hello suivant commande tooupload hello zip fichier toohello HDInsight nœud principal du cluster :

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Remplacez **nom de fichier** avec le nom hello du fichier zip de hello. Remplacez **nom d’utilisateur** avec la connexion SSH hello pour le cluster HDInsight de hello. Remplacez CLUSTERNAME par nom hello du cluster HDInsight de hello.

   > [!NOTE]
   > Si vous utilisez un tooauthenticate de mot de passe de votre connexion SSH, vous êtes invité pour un mot de passe hello. Si vous avez utilisé une clé publique, vous devrez peut-être toouse hello `-i` paramètre et spécifiez hello toohello de chemin d’accès qui correspondent à une clé privée. Par exemple, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Une fois le téléchargement de hello terminée, connectez cluster toohello à l’aide de SSH :

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Une fois connecté, utilisez hello toounzip hello .zip fichier suivant :

    ```
    unzip FILENAME.zip
    ```

    Cette commande extrait un fichier .csv d’environ 60 Mo.

4. Utilisez hello suivant de commande toocreate un répertoire de stockage de HDInsight, puis copiez le répertoire du fichier de hello toohello :

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Créer et exécuter hello HiveQL

Étapes suivantes de hello d’utilisation tooimport données d’un fichier CSV hello dans une table Hive nommée **retards**.

1. Suivant de hello utilisez commande toocreate et modifier un fichier nommé **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Utilisez hello après le texte en tant que contenu hello de ce fichier :

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. fichier de hello toosave, utilisez **Ctrl + X**, puis **Y** .

3. toostart Hive et exécution hello **flightdelays.hql** , utilisez hello de commande suivante :

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > Dans cet exemple, `localhost` est utilisé, car vous êtes connecté toohello le nœud principal du cluster HDInsight hello, qui est où HiveServer2 est en cours d’exécution.

4. Une fois hello __flightdelays.hql__ script fin de son exécution suivante de hello utilisez commande tooopen une session interactive de Beeline :

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Lorsque vous recevez hello `jdbc:hive2://localhost:10001/>` invite, utilisez hello suivant tooretrieve interroger des données à partir des données de retard de vol hello importé.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Cette requête récupère une liste des villes que des délais de météo expérimentés, ainsi que de la moyenne de hello retarder l’heure et l’enregistrement trop`/tutorials/flightdelays/output`. Une version ultérieure, Sqoop lit les données de hello depuis cet emplacement et à les exporter tooAzure base de données SQL.

6. tooexit Beeline, entrez `!quit` invite hello.

## <a name="create-a-sql-database"></a>Création d’une base de données SQL

Si vous disposez déjà d’une base de données SQL, vous devez obtenir le nom du serveur hello. Vous trouverez le nom du serveur hello Bonjour [portail Azure](https://portal.azure.com) en sélectionnant **bases de données SQL**, et de la base de données puis en filtrant sur nom hello Hello vous souhaitez toouse. nom du serveur Hello est répertorié dans hello **SERVER** colonne.

Si vous n’avez pas déjà d’une base de données SQL, utilisez les informations de hello dans [didacticiel de base de données SQL : créez une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md) toocreate une. Enregistrez le nom du serveur utilisé pour la base de données hello hello.

## <a name="create-a-sql-database-table"></a>Création d’une table de base de données SQL

> [!NOTE]
> Il existe de nombreuses façons de tooconnect tooSQL de base de données et créer une table. Hello suivant l’utilisation d’étapes [FreeTDS](http://www.freetds.org/) à partir du cluster HDInsight de hello.


1. Utiliser SSH tooconnect toohello HDInsight de basés sur Linux cluster et exécution hello comme suit à partir de la session SSH hello.

2. Utilisez hello suivant commande tooinstall FreeTDS :

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Une fois hello installation terminée, utilisez hello suivant du serveur de base de données SQL de commande tooconnect toohello. Remplacez **nom_serveur** avec le nom du serveur de base de données SQL hello. Remplacez **adminLogin** et **adminPassword** avec connexion hello pour la base de données SQL. Remplacez **databaseName** avec le nom de base de données hello.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Vous recevez toohello similaire de sortie suivant du texte :

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. À hello `1>` invite, entrez hello lignes suivantes :

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Hello lorsque `GO` instruction est entrée, les instructions précédentes hello sont évaluées. Cette requête crée une table nommée **delays** avec un index cluster.

    Hello utilisation suivant tooverify de requête qui hello table a été créé :

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Hello est similaire toohello suivant texte de sortie :

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Entrez `exit` à hello `1>` tooexit hello tsql utilitaire d’invite.

## <a name="export-data-with-sqoop"></a>Exportation de données avec Sqoop

1. Utilisez hello suivant tooverify commande que Sqoop peut voir votre base de données SQL :

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Cette commande renvoie une liste des bases de données, notamment hello de base de données que vous avez créé précédemment des table de retards hello dans.

2. Utilisez hello suivant des données de tooexport de commande à partir de la table de mobiledata hivesampletable toohello :

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop se connecte toohello de base de données contenant la table de retards hello et exporte des données à partir de hello `/tutorials/flightdelays/output` table des retards toohello répertoires.

3. Après la commande hello, utilisez hello suivant toohello tooconnect de base de données à l’aide de TSQL :

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Une fois connecté, utilisez hello suivant tooverify instructions que les données de salutation a été exporté toohello mobiledata table :

    ```
    SELECT * FROM delays
    GO
    ```

    Vous devez voir une liste de données de table de hello. Type `exit` utilitaire de tooexit hello tsql.

## <a id="nextsteps"></a> Étapes suivantes

consultez de plusieurs façons toowork, avec des données dans HDInsight, toolearn hello suivants de documents :

* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie]
* [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]
* [Développement de programmes de diffusion en continu Hadoop Python pour HDInsight][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
