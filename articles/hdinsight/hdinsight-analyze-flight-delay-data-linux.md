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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="5de6d-103">Analyse des données sur les retards de vol avec Hive dans HDInsight basé sur Linux</span><span class="sxs-lookup"><span data-stu-id="5de6d-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="5de6d-104">Découvrez comment les données de retard de vol tooanalyze puis à l’aide de Hive dans HDInsight de basés sur Linux exporter hello tooAzure de données de la base de données SQL à l’aide de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5de6d-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5de6d-105">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="5de6d-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5de6d-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="5de6d-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5de6d-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5de6d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5de6d-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5de6d-108">Prerequisites</span></span>

* <span data-ttu-id="5de6d-109">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5de6d-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="5de6d-110">Consultez la rubrique [Prise en main de Hadoop avec Hive dans HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md) pour connaître les étapes de création d’un cluster HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="5de6d-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="5de6d-111">**Base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="5de6d-111">**Azure SQL Database**.</span></span> <span data-ttu-id="5de6d-112">Vous allez utiliser une base de données SQL Azure comme magasin de données cible.</span><span class="sxs-lookup"><span data-stu-id="5de6d-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="5de6d-113">Si vous n'avez pas déjà une base de données SQL, consultez [Didacticiel sur la base de données SQL : Créer une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5de6d-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="5de6d-114">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="5de6d-114">**Azure CLI**.</span></span> <span data-ttu-id="5de6d-115">Si vous n’avez pas installé hello CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) pour connaître la procédure.</span><span class="sxs-lookup"><span data-stu-id="5de6d-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="5de6d-116">Télécharger des données de vol hello</span><span class="sxs-lookup"><span data-stu-id="5de6d-116">Download hello flight data</span></span>

1. <span data-ttu-id="5de6d-117">Parcourir trop[recherche et l’Administration de technologie novatrice, Bureau de statistiques de transport][rita-website].</span><span class="sxs-lookup"><span data-stu-id="5de6d-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="5de6d-118">Sur la page de hello, sélectionnez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5de6d-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="5de6d-119">Nom</span><span class="sxs-lookup"><span data-stu-id="5de6d-119">Name</span></span> | <span data-ttu-id="5de6d-120">Valeur</span><span class="sxs-lookup"><span data-stu-id="5de6d-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="5de6d-121">Filtre année</span><span class="sxs-lookup"><span data-stu-id="5de6d-121">Filter Year</span></span> |<span data-ttu-id="5de6d-122">2013</span><span class="sxs-lookup"><span data-stu-id="5de6d-122">2013</span></span> |
   | <span data-ttu-id="5de6d-123">Filtre période</span><span class="sxs-lookup"><span data-stu-id="5de6d-123">Filter Period</span></span> |<span data-ttu-id="5de6d-124">Janvier</span><span class="sxs-lookup"><span data-stu-id="5de6d-124">January</span></span> |
   | <span data-ttu-id="5de6d-125">Champs</span><span class="sxs-lookup"><span data-stu-id="5de6d-125">Fields</span></span> |<span data-ttu-id="5de6d-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="5de6d-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="5de6d-127">Effacez tous les autres champs</span><span class="sxs-lookup"><span data-stu-id="5de6d-127">Clear all other fields</span></span> |

3. <span data-ttu-id="5de6d-128">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="5de6d-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="5de6d-129">Télécharger les données de salutation</span><span class="sxs-lookup"><span data-stu-id="5de6d-129">Upload hello data</span></span>

1. <span data-ttu-id="5de6d-130">Utilisez hello suivant commande tooupload hello zip fichier toohello HDInsight nœud principal du cluster :</span><span class="sxs-lookup"><span data-stu-id="5de6d-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="5de6d-131">Remplacez **nom de fichier** avec le nom hello du fichier zip de hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="5de6d-132">Remplacez **nom d’utilisateur** avec la connexion SSH hello pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="5de6d-133">Remplacez CLUSTERNAME par nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5de6d-134">Si vous utilisez un tooauthenticate de mot de passe de votre connexion SSH, vous êtes invité pour un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="5de6d-135">Si vous avez utilisé une clé publique, vous devrez peut-être toouse hello `-i` paramètre et spécifiez hello toohello de chemin d’accès qui correspondent à une clé privée.</span><span class="sxs-lookup"><span data-stu-id="5de6d-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="5de6d-136">Par exemple, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="5de6d-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="5de6d-137">Une fois le téléchargement de hello terminée, connectez cluster toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="5de6d-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="5de6d-138">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5de6d-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="5de6d-139">Une fois connecté, utilisez hello toounzip hello .zip fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="5de6d-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="5de6d-140">Cette commande extrait un fichier .csv d’environ 60 Mo.</span><span class="sxs-lookup"><span data-stu-id="5de6d-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="5de6d-141">Utilisez hello suivant de commande toocreate un répertoire de stockage de HDInsight, puis copiez le répertoire du fichier de hello toohello :</span><span class="sxs-lookup"><span data-stu-id="5de6d-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="5de6d-142">Créer et exécuter hello HiveQL</span><span class="sxs-lookup"><span data-stu-id="5de6d-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="5de6d-143">Étapes suivantes de hello d’utilisation tooimport données d’un fichier CSV hello dans une table Hive nommée **retards**.</span><span class="sxs-lookup"><span data-stu-id="5de6d-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="5de6d-144">Suivant de hello utilisez commande toocreate et modifier un fichier nommé **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="5de6d-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="5de6d-145">Utilisez hello après le texte en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="5de6d-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="5de6d-146">fichier de hello toosave, utilisez **Ctrl + X**, puis **Y** .</span><span class="sxs-lookup"><span data-stu-id="5de6d-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="5de6d-147">toostart Hive et exécution hello **flightdelays.hql** , utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de6d-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="5de6d-148">Dans cet exemple, `localhost` est utilisé, car vous êtes connecté toohello le nœud principal du cluster HDInsight hello, qui est où HiveServer2 est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5de6d-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="5de6d-149">Une fois hello __flightdelays.hql__ script fin de son exécution suivante de hello utilisez commande tooopen une session interactive de Beeline :</span><span class="sxs-lookup"><span data-stu-id="5de6d-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="5de6d-150">Lorsque vous recevez hello `jdbc:hive2://localhost:10001/>` invite, utilisez hello suivant tooretrieve interroger des données à partir des données de retard de vol hello importé.</span><span class="sxs-lookup"><span data-stu-id="5de6d-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="5de6d-151">Cette requête récupère une liste des villes que des délais de météo expérimentés, ainsi que de la moyenne de hello retarder l’heure et l’enregistrement trop`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="5de6d-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="5de6d-152">Une version ultérieure, Sqoop lit les données de hello depuis cet emplacement et à les exporter tooAzure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="5de6d-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="5de6d-153">tooexit Beeline, entrez `!quit` invite hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="5de6d-154">Création d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5de6d-154">Create a SQL Database</span></span>

<span data-ttu-id="5de6d-155">Si vous disposez déjà d’une base de données SQL, vous devez obtenir le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="5de6d-156">Vous trouverez le nom du serveur hello Bonjour [portail Azure](https://portal.azure.com) en sélectionnant **bases de données SQL**, et de la base de données puis en filtrant sur nom hello Hello vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="5de6d-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="5de6d-157">nom du serveur Hello est répertorié dans hello **SERVER** colonne.</span><span class="sxs-lookup"><span data-stu-id="5de6d-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="5de6d-158">Si vous n’avez pas déjà d’une base de données SQL, utilisez les informations de hello dans [didacticiel de base de données SQL : créez une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md) toocreate une.</span><span class="sxs-lookup"><span data-stu-id="5de6d-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="5de6d-159">Enregistrez le nom du serveur utilisé pour la base de données hello hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="5de6d-160">Création d’une table de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5de6d-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="5de6d-161">Il existe de nombreuses façons de tooconnect tooSQL de base de données et créer une table.</span><span class="sxs-lookup"><span data-stu-id="5de6d-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="5de6d-162">Hello suivant l’utilisation d’étapes [FreeTDS](http://www.freetds.org/) à partir du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="5de6d-163">Utiliser SSH tooconnect toohello HDInsight de basés sur Linux cluster et exécution hello comme suit à partir de la session SSH hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="5de6d-164">Utilisez hello suivant commande tooinstall FreeTDS :</span><span class="sxs-lookup"><span data-stu-id="5de6d-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="5de6d-165">Une fois hello installation terminée, utilisez hello suivant du serveur de base de données SQL de commande tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="5de6d-166">Remplacez **nom_serveur** avec le nom du serveur de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="5de6d-167">Remplacez **adminLogin** et **adminPassword** avec connexion hello pour la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="5de6d-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="5de6d-168">Remplacez **databaseName** avec le nom de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="5de6d-169">Vous recevez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="5de6d-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="5de6d-170">À hello `1>` invite, entrez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5de6d-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="5de6d-171">Hello lorsque `GO` instruction est entrée, les instructions précédentes hello sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="5de6d-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="5de6d-172">Cette requête crée une table nommée **delays** avec un index cluster.</span><span class="sxs-lookup"><span data-stu-id="5de6d-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="5de6d-173">Hello utilisation suivant tooverify de requête qui hello table a été créé :</span><span class="sxs-lookup"><span data-stu-id="5de6d-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="5de6d-174">Hello est similaire toohello suivant texte de sortie :</span><span class="sxs-lookup"><span data-stu-id="5de6d-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="5de6d-175">Entrez `exit` à hello `1>` tooexit hello tsql utilitaire d’invite.</span><span class="sxs-lookup"><span data-stu-id="5de6d-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="5de6d-176">Exportation de données avec Sqoop</span><span class="sxs-lookup"><span data-stu-id="5de6d-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="5de6d-177">Utilisez hello suivant tooverify commande que Sqoop peut voir votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="5de6d-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="5de6d-178">Cette commande renvoie une liste des bases de données, notamment hello de base de données que vous avez créé précédemment des table de retards hello dans.</span><span class="sxs-lookup"><span data-stu-id="5de6d-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="5de6d-179">Utilisez hello suivant des données de tooexport de commande à partir de la table de mobiledata hivesampletable toohello :</span><span class="sxs-lookup"><span data-stu-id="5de6d-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="5de6d-180">Sqoop se connecte toohello de base de données contenant la table de retards hello et exporte des données à partir de hello `/tutorials/flightdelays/output` table des retards toohello répertoires.</span><span class="sxs-lookup"><span data-stu-id="5de6d-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="5de6d-181">Après la commande hello, utilisez hello suivant toohello tooconnect de base de données à l’aide de TSQL :</span><span class="sxs-lookup"><span data-stu-id="5de6d-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="5de6d-182">Une fois connecté, utilisez hello suivant tooverify instructions que les données de salutation a été exporté toohello mobiledata table :</span><span class="sxs-lookup"><span data-stu-id="5de6d-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="5de6d-183">Vous devez voir une liste de données de table de hello.</span><span class="sxs-lookup"><span data-stu-id="5de6d-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="5de6d-184">Type `exit` utilitaire de tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="5de6d-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="5de6d-185"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5de6d-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="5de6d-186">consultez de plusieurs façons toowork, avec des données dans HDInsight, toolearn hello suivants de documents :</span><span class="sxs-lookup"><span data-stu-id="5de6d-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="5de6d-187">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="5de6d-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="5de6d-188">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="5de6d-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="5de6d-189">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5de6d-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="5de6d-190">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="5de6d-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="5de6d-191">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="5de6d-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="5de6d-192">[Développement de programmes de diffusion en continu Hadoop Python pour HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="5de6d-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
