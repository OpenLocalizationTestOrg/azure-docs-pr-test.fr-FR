---
title: "Analyse des données sur les retards de vol avec Hive dans HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser Hive pour analyser les données sur les retards de vol à l’aide de HDInsight basé sur Linux, puis exporter les données vers une base de données SQL à l’aide de Sqoop."
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="62b53-103">Analyse des données sur les retards de vol avec Hive dans HDInsight basé sur Linux</span><span class="sxs-lookup"><span data-stu-id="62b53-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="62b53-104">Découvrez comment analyser les données sur les retards de vol à l'aide de Hive sur HDInsight Linux, puis exporter les données vers Azure SQL Database à l'aide de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="62b53-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62b53-105">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="62b53-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="62b53-106">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="62b53-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="62b53-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="62b53-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="62b53-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="62b53-108">Prerequisites</span></span>

* <span data-ttu-id="62b53-109">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="62b53-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="62b53-110">Consultez la rubrique [Prise en main de Hadoop avec Hive dans HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md) pour connaître les étapes de création d’un cluster HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="62b53-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="62b53-111">**Base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="62b53-111">**Azure SQL Database**.</span></span> <span data-ttu-id="62b53-112">Vous allez utiliser une base de données SQL Azure comme magasin de données cible.</span><span class="sxs-lookup"><span data-stu-id="62b53-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="62b53-113">Si vous n'avez pas déjà une base de données SQL, consultez [Didacticiel sur la base de données SQL : Créer une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="62b53-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="62b53-114">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="62b53-114">**Azure CLI**.</span></span> <span data-ttu-id="62b53-115">Si vous n'avez pas installé l'interface de ligne de commande Azure, consultez la rubrique [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md) pour connaître la procédure.</span><span class="sxs-lookup"><span data-stu-id="62b53-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="62b53-116">Téléchargement des données de vol</span><span class="sxs-lookup"><span data-stu-id="62b53-116">Download the flight data</span></span>

1. <span data-ttu-id="62b53-117">Accédez à [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span><span class="sxs-lookup"><span data-stu-id="62b53-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="62b53-118">Sur la page, sélectionnez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="62b53-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="62b53-119">Nom</span><span class="sxs-lookup"><span data-stu-id="62b53-119">Name</span></span> | <span data-ttu-id="62b53-120">Valeur</span><span class="sxs-lookup"><span data-stu-id="62b53-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="62b53-121">Filtre année</span><span class="sxs-lookup"><span data-stu-id="62b53-121">Filter Year</span></span> |<span data-ttu-id="62b53-122">2013</span><span class="sxs-lookup"><span data-stu-id="62b53-122">2013</span></span> |
   | <span data-ttu-id="62b53-123">Filtre période</span><span class="sxs-lookup"><span data-stu-id="62b53-123">Filter Period</span></span> |<span data-ttu-id="62b53-124">Janvier</span><span class="sxs-lookup"><span data-stu-id="62b53-124">January</span></span> |
   | <span data-ttu-id="62b53-125">Champs</span><span class="sxs-lookup"><span data-stu-id="62b53-125">Fields</span></span> |<span data-ttu-id="62b53-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="62b53-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="62b53-127">Effacez tous les autres champs</span><span class="sxs-lookup"><span data-stu-id="62b53-127">Clear all other fields</span></span> |

3. <span data-ttu-id="62b53-128">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="62b53-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="62b53-129">Téléchargement des données</span><span class="sxs-lookup"><span data-stu-id="62b53-129">Upload the data</span></span>

1. <span data-ttu-id="62b53-130">Utilisez la commande suivante pour télécharger le fichier zip dans le nœud principal du cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="62b53-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="62b53-131">Remplacez **FILENAME** par le nom du fichier zip.</span><span class="sxs-lookup"><span data-stu-id="62b53-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="62b53-132">Remplacez **USERNAME** par la connexion SSH du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b53-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="62b53-133">Remplacez CLUSTERNAME par le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b53-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="62b53-134">Si vous utilisez un mot de passe pour authentifier votre connexion SSH, vous êtes invité à le saisir.</span><span class="sxs-lookup"><span data-stu-id="62b53-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="62b53-135">Si vous utilisez une clé publique, vous devrez peut-être utiliser le paramètre `-i` et spécifier le chemin d’accès de la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="62b53-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="62b53-136">Par exemple, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="62b53-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="62b53-137">Une fois le téléchargement terminé, connectez-vous au cluster à l'aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="62b53-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="62b53-138">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="62b53-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="62b53-139">Une fois connecté, procédez comme suit pour décompresser le fichier .zip :</span><span class="sxs-lookup"><span data-stu-id="62b53-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="62b53-140">Cette commande extrait un fichier .csv d’environ 60 Mo.</span><span class="sxs-lookup"><span data-stu-id="62b53-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="62b53-141">Utilisez la commande suivante pour créer un répertoire de stockage HDInsight, puis copiez le fichier dans le répertoire :</span><span class="sxs-lookup"><span data-stu-id="62b53-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="62b53-142">Création et exécution du HiveQL</span><span class="sxs-lookup"><span data-stu-id="62b53-142">Create and run the HiveQL</span></span>

<span data-ttu-id="62b53-143">Suivez la procédure suivante pour importer des données à partir du fichier CSV dans une table Hive nommée **Delays**.</span><span class="sxs-lookup"><span data-stu-id="62b53-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="62b53-144">Pour créer et modifier un fichier nommé **flightdelays.hql**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="62b53-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="62b53-145">Utilisez le texte suivant comme contenu de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="62b53-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="62b53-146">Pour enregistrer le fichier, appuyez sur **Ctrl + X**, puis sur **Y**.</span><span class="sxs-lookup"><span data-stu-id="62b53-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="62b53-147">Pour démarrer Hive et exécuter le fichier **flightdelays.hql**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="62b53-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="62b53-148">Dans cet exemple, `localhost` est utilisé, car vous êtes connecté au nœud principal du cluster HDInsight, où s’exécute HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="62b53-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="62b53-149">Une fois l’exécution du script __flightdelays.hql__ terminée, utilisez la commande suivante pour ouvrir une session Beeline interactive :</span><span class="sxs-lookup"><span data-stu-id="62b53-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="62b53-150">Lorsque vous recevrez l’invite `jdbc:hive2://localhost:10001/>`, utilisez la requête suivante pour récupérer les données à partir des données relatives aux retards de vol qui ont été importées.</span><span class="sxs-lookup"><span data-stu-id="62b53-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="62b53-151">Cette requête récupère la liste des villes qui ont enregistré des retards liés aux conditions météo, ainsi que le temps de retard moyen, qui sont enregistrés dans `/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="62b53-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="62b53-152">Sqoop lit ensuite les données à partir de cet emplacement et les exporte vers Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="62b53-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="62b53-153">Pour quitter Beeline, entrez `!quit` à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="62b53-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="62b53-154">Création d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="62b53-154">Create a SQL Database</span></span>

<span data-ttu-id="62b53-155">Si vous disposez déjà d’une base de données SQL, vous devez obtenir le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="62b53-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="62b53-156">Vous trouverez le nom du serveur sur le [portail Azure](https://portal.azure.com) en sélectionnant **Bases de données SQL**, puis en filtrant sur le nom de la base de données que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="62b53-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="62b53-157">Le nom du serveur est répertorié dans la colonne **SERVEUR** .</span><span class="sxs-lookup"><span data-stu-id="62b53-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="62b53-158">Si vous n’avez pas de base de données SQL, consultez les informations dans le [Didacticiel sur la base de données SQL : Création d’une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md) pour en créer une.</span><span class="sxs-lookup"><span data-stu-id="62b53-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="62b53-159">Enregistrer le nom du serveur utilisé pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="62b53-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="62b53-160">Création d’une table de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="62b53-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="62b53-161">Il existe de nombreuses façons de se connecter à la base de données SQL et de créer une table.</span><span class="sxs-lookup"><span data-stu-id="62b53-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="62b53-162">Les étapes suivantes utilisent [FreeTDS](http://www.freetds.org/) à partir du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b53-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="62b53-163">Utilisez le protocole SSH pour vous connecter au cluster HDInsight Linux et exécutez les étapes suivantes à partir de la session SSH.</span><span class="sxs-lookup"><span data-stu-id="62b53-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="62b53-164">Utilisez la commande suivante pour installer FreeTDS :</span><span class="sxs-lookup"><span data-stu-id="62b53-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="62b53-165">Une l’installation terminée, utilisez la commande suivante pour vous connecter au serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="62b53-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="62b53-166">Remplacez **serverName** par le nom du serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="62b53-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="62b53-167">Remplacez **adminLogin** et **adminPassword** par les informations d’identification de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="62b53-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="62b53-168">Remplacez **databaseName** par le nom de la base de données.</span><span class="sxs-lookup"><span data-stu-id="62b53-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="62b53-169">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="62b53-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="62b53-170">À l’invite de commandes `1>` , entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="62b53-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="62b53-171">Une fois l’instruction `GO` entrée, les instructions précédentes sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="62b53-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="62b53-172">Cette requête crée une table nommée **delays** avec un index cluster.</span><span class="sxs-lookup"><span data-stu-id="62b53-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="62b53-173">Utilisez la requête suivante pour vérifier que la table a été créée :</span><span class="sxs-lookup"><span data-stu-id="62b53-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="62b53-174">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="62b53-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="62b53-175">Pour quitter l’utilitaire psql, entrez `exit` at the `1>` .</span><span class="sxs-lookup"><span data-stu-id="62b53-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="62b53-176">Exportation de données avec Sqoop</span><span class="sxs-lookup"><span data-stu-id="62b53-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="62b53-177">Utilisez la commande suivante pour vérifier que Sqoop peut voir votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="62b53-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="62b53-178">Cette commande renvoie une liste des bases de données, notamment la base de données que vous avez créée précédemment dans la table des retards.</span><span class="sxs-lookup"><span data-stu-id="62b53-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="62b53-179">Utilisez la commande suivante pour exporter des données à partir de hivesampletable dans la table mobiledata :</span><span class="sxs-lookup"><span data-stu-id="62b53-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="62b53-180">Sqoop se connecte à la base de données contenant la table des retards et exporte des données du répertoire `/tutorials/flightdelays/output` vers la table des retards.</span><span class="sxs-lookup"><span data-stu-id="62b53-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="62b53-181">Une fois la commande terminée, utilisez les éléments suivants pour vous connecter à la base de données à l’aide de TSQL :</span><span class="sxs-lookup"><span data-stu-id="62b53-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="62b53-182">Une fois que vous êtes connecté, utilisez les instructions suivantes pour vérifier que les données ont été exportées dans la table mobiledata :</span><span class="sxs-lookup"><span data-stu-id="62b53-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="62b53-183">Vous devez voir une liste des données dans la table.</span><span class="sxs-lookup"><span data-stu-id="62b53-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="62b53-184">Tapez `exit` pour quitter l’utilitaire tsql.</span><span class="sxs-lookup"><span data-stu-id="62b53-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="62b53-185"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62b53-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="62b53-186">Pour découvrir d’autres façons d’utiliser les données dans HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="62b53-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="62b53-187">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="62b53-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="62b53-188">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="62b53-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="62b53-189">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="62b53-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="62b53-190">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="62b53-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="62b53-191">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="62b53-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="62b53-192">[Développement de programmes de diffusion en continu Hadoop Python pour HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="62b53-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
