---
title: "Utiliser Hadoop Hive avec Curl dans HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment transmettre à distance des tâches Pig vers HDInsight à l'aide de Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="2edc5-103">Exécuter des requêtes Hive avec Hadoop dans HDInsight à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="2edc5-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2edc5-104">Découvrez comment utiliser l’API REST WebHCat pour exécuter des requêtes Hive avec Hadoop sur un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2edc5-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="2edc5-105">[Curl](http://curl.haxx.se/) est utilisé pour illustrer comment interagir avec HDInsight en utilisant des requêtes HTTP brutes.</span><span class="sxs-lookup"><span data-stu-id="2edc5-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="2edc5-106">L’utilitaire [jq](http://stedolan.github.io/jq/) est utilisé pour traiter les données JSON renvoyées à partir de demandes REST.</span><span class="sxs-lookup"><span data-stu-id="2edc5-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="2edc5-107">Si vous êtes déjà familiarisé avec l’utilisation de serveurs Hadoop sous Linux, mais que vous découvrez HDInsight, consultez le document [Informations sur l’utilisation de Hadoop sur HDInsight sous Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="2edc5-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="2edc5-108"><a id="curl"></a>Exécuter des requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="2edc5-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="2edc5-109">Lorsque vous utilisez cURL ou toute autre communication REST avec WebHCat, vous devez authentifier les requêtes en fournissant le nom d’utilisateur et le mot de passe de l’administrateur du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2edc5-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="2edc5-110">Pour les commandes de cette section, remplacez **USERNAME** par l’utilisateur à authentifier sur le cluster et **PASSWORD** par le mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2edc5-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="2edc5-111">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="2edc5-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="2edc5-112">L’API REST est sécurisée à l’aide de l’ [authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="2edc5-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="2edc5-113">Pour aider à vous assurer que vos informations d’identification sont envoyées en toute sécurité sur le serveur, procédez toujours aux requêtes via le protocole HTTP sécurisé (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="2edc5-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="2edc5-114">À partir d’une ligne de commande, exécutez la commande suivante pour vérifier que vous pouvez vous connecter à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2edc5-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="2edc5-115">La réponse reçue est similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="2edc5-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="2edc5-116">Les paramètres utilisés dans cette commande sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="2edc5-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="2edc5-117">**-u** : le nom d’utilisateur et le mot de passe utilisés pour authentifier la demande.</span><span class="sxs-lookup"><span data-stu-id="2edc5-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="2edc5-118">**-G**: indique que la requête correspond à une opération GET.</span><span class="sxs-lookup"><span data-stu-id="2edc5-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="2edc5-119">Le début de l’URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est le même pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="2edc5-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="2edc5-120">Le chemin d’accès, **/status**, indique que la demande doit renvoyer le statut de WebHCat (également appelé Templeton) au serveur.</span><span class="sxs-lookup"><span data-stu-id="2edc5-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="2edc5-121">Vous pouvez également prendre connaissance de la version de Hive à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2edc5-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="2edc5-122">Cette requête renvoie une réponse similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="2edc5-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="2edc5-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="2edc5-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="2edc5-124">Utilisez la commande suivante pour créer une table nommée **log4jLogs** :</span><span class="sxs-lookup"><span data-stu-id="2edc5-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="2edc5-125">Les paramètres suivants sont utilisés avec cette demande :</span><span class="sxs-lookup"><span data-stu-id="2edc5-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="2edc5-126">**-d** : étant donné que `-G` n’est pas utilisé, la demande passe par défaut à la méthode POST.</span><span class="sxs-lookup"><span data-stu-id="2edc5-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="2edc5-127">`-d` spécifie les valeurs de données envoyées avec la demande.</span><span class="sxs-lookup"><span data-stu-id="2edc5-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="2edc5-128">**user.name** : l’utilisateur qui exécute la commande.</span><span class="sxs-lookup"><span data-stu-id="2edc5-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="2edc5-129">**execute** : les instructions HiveQL qui doivent être exécutées.</span><span class="sxs-lookup"><span data-stu-id="2edc5-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="2edc5-130">**statusdir**: le répertoire dans lequel les statuts de cette tâche sont écrits.</span><span class="sxs-lookup"><span data-stu-id="2edc5-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="2edc5-131">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2edc5-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="2edc5-132">**DROP TABLE** : si la table existe déjà, elle est supprimée.</span><span class="sxs-lookup"><span data-stu-id="2edc5-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="2edc5-133">**CREATE EXTERNAL TABLE** : crée une table « externe » dans Hive.</span><span class="sxs-lookup"><span data-stu-id="2edc5-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="2edc5-134">Les tables externes stockent uniquement la définition de table dans Hive.</span><span class="sxs-lookup"><span data-stu-id="2edc5-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="2edc5-135">Les données restent à l'emplacement d'origine.</span><span class="sxs-lookup"><span data-stu-id="2edc5-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2edc5-136">Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe,</span><span class="sxs-lookup"><span data-stu-id="2edc5-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="2edc5-137">par exemple, par un processus de téléchargement de données automatisé ou une autre opération MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2edc5-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="2edc5-138">La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.</span><span class="sxs-lookup"><span data-stu-id="2edc5-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="2edc5-139">**ROW FORMAT** : le mode de formatage des données.</span><span class="sxs-lookup"><span data-stu-id="2edc5-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="2edc5-140">Les champs de chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="2edc5-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="2edc5-141">**STORED AS TEXTFILE LOCATION** : l’endroit où sont stockées les données (répertoire example/data) et indique qu’elles sont stockées sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="2edc5-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="2edc5-142">**SELECT** : sélectionne toutes les lignes dont la colonne **t4** contient la valeur **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="2edc5-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="2edc5-143">Cette instruction renvoie la valeur **3**, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="2edc5-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2edc5-144">Notez que les espaces entre les instructions HiveQL sont remplacés par le caractère `+` lorsqu'ils sont utilisés avec Curl.</span><span class="sxs-lookup"><span data-stu-id="2edc5-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="2edc5-145">Les valeurs citées qui contiennent un espace, tel que le séparateur, ne doivent pas être remplacées par `+`.</span><span class="sxs-lookup"><span data-stu-id="2edc5-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="2edc5-146">**INPUT__FILE__NAME LIKE ’%25.log’** : cette instruction limite la recherche aux seuls fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="2edc5-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2edc5-147">Notez que `%25` est la forme codée de l’URL de %, donc la condition réelle est `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="2edc5-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="2edc5-148">La valeur % doit être une URL encodée, car elle est traitée comme un caractère spécial dans les URL.</span><span class="sxs-lookup"><span data-stu-id="2edc5-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="2edc5-149">Cette commande doit retourner un ID de tâche qui peut être utilisé pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2edc5-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="2edc5-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="2edc5-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="2edc5-151">Pour vérifier le statut de la tâche, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2edc5-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="2edc5-152">Remplacez **JOBID** par la valeur retournée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="2edc5-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="2edc5-153">Par exemple, si la valeur de retour était `{"id":"job_1415651640909_0026"}`, le **JOBID** est `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="2edc5-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="2edc5-154">Si la tâche est terminée, l’état est **TERMINÉ**.</span><span class="sxs-lookup"><span data-stu-id="2edc5-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2edc5-155">Cette requête Curl renvoie un document JSON (JavaScript Object Notation) avec des informations sur la tâche.</span><span class="sxs-lookup"><span data-stu-id="2edc5-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="2edc5-156">Jq est utilisé pour récupérer uniquement la valeur d’état.</span><span class="sxs-lookup"><span data-stu-id="2edc5-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="2edc5-157">Une fois que le statut de la tâche est passé à **TERMINÉ**, vous pouvez récupérer les résultats depuis le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2edc5-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="2edc5-158">Le paramètre `statusdir` transmis avec la requête contient l’emplacement du fichier de sortie. Dans notre cas : **/example/curl**.</span><span class="sxs-lookup"><span data-stu-id="2edc5-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="2edc5-159">Cette adresse stocke le résultat dans le répertoire **exemple/curl** dans le stockage par défaut du cluster.</span><span class="sxs-lookup"><span data-stu-id="2edc5-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="2edc5-160">Vous pouvez répertorier et télécharger ces fichiers à l’aide de l' [interface de ligne de commande Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2edc5-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="2edc5-161">Pour plus d’informations sur l’utilisation de l’interface CLI Azure avec Stockage Azure, consultez le document [Utiliser Azure CLI 2.0 avec Stockage Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs).</span><span class="sxs-lookup"><span data-stu-id="2edc5-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="2edc5-162">Utilisez les instructions suivantes pour créer une table « interne » nommée **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="2edc5-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="2edc5-163">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2edc5-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2edc5-164">**CREATE TABLE IF NOT EXISTS** : crée une table, si elle n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="2edc5-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="2edc5-165">Une instruction crée une table interne, qui est stockée dans l’entrepôt de données Hive et gérée intégralement par Hive.</span><span class="sxs-lookup"><span data-stu-id="2edc5-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2edc5-166">Contrairement aux tables externes, la suppression d’une table interne entraîne également la suppression des données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="2edc5-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="2edc5-167">**STORED AS ORC** : stocke les données au format ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="2edc5-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="2edc5-168">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="2edc5-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="2edc5-169">**INSERT OVERWRITE ... SELECT** : sélectionne des lignes de la table **log4jLogs** qui contiennent **[ERROR]**, puis insère les données dans la table **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="2edc5-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="2edc5-170">**SELECT** : sélectionne toutes les lignes de la nouvelle table **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="2edc5-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="2edc5-171">Utilisez l'identificateur de la tâche renvoyé pour vérifier l'état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2edc5-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="2edc5-172">Une fois la tâche terminée, utilisez la CLI Azure, comme indiqué précédemment, pour télécharger et afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="2edc5-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="2edc5-173">La sortie doit comporter trois lignes, qui contiennent toutes la valeur **ERROR**.</span><span class="sxs-lookup"><span data-stu-id="2edc5-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="2edc5-174"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2edc5-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2edc5-175">Pour obtenir des informations générales sur Hive avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2edc5-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="2edc5-176">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2edc5-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2edc5-177">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2edc5-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2edc5-178">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2edc5-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2edc5-179">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2edc5-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="2edc5-180">Si vous utilisez Tez avec Hive, consultez les documents suivants pour les informations de débogage :</span><span class="sxs-lookup"><span data-stu-id="2edc5-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="2edc5-181">Utilisez la vue Tez Ambari sur HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="2edc5-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="2edc5-182">Pour plus d’informations sur l’API REST utilisée dans ce document, consultez le document [Référence WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="2edc5-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


