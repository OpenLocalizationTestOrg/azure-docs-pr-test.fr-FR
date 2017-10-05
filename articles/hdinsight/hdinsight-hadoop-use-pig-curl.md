---
title: Utiliser Hadoop Pig avec REST dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment utiliser REST pour exécuter des tâches Pig Latin sur un cluster Hadoop dans HDInsight Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="768e0-103">Exécution de tâches Pig avec Hadoop sur HDInsight à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="768e0-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="768e0-104">Découvrez comment exécuter des tâches Pig Latin en effectuant des demandes REST pour un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="768e0-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="768e0-105">Curl est utilisé pour illustrer comment interagir avec HDInsight en utilisant l’API REST WebHCat.</span><span class="sxs-lookup"><span data-stu-id="768e0-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="768e0-106">Si vous connaissez déjà l’utilisation de serveurs Hadoop basés sur Linux, mais pas HDInsight, consultez la rubrique [Informations sur l’utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="768e0-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="768e0-107"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="768e0-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="768e0-108">Un cluster Azure HDInsight (Hadoop sur HDInsight) Windows ou Linux</span><span class="sxs-lookup"><span data-stu-id="768e0-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="768e0-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="768e0-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="768e0-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="768e0-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="768e0-111">Curl</span><span class="sxs-lookup"><span data-stu-id="768e0-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="768e0-112">jq</span><span class="sxs-lookup"><span data-stu-id="768e0-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="768e0-113"><a id="curl"></a>Exécution de tâches Pig à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="768e0-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="768e0-114">L’API REST est sécurisée à l’aide de l’ [authentification d’accès de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="768e0-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="768e0-115">Pour garantir l’envoi en toute sécurité de vos informations d’identification sur le serveur, procédez toujours aux requêtes via le protocole HTTP sécurisé (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="768e0-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="768e0-116">Lorsque vous utilisez les commandes de cette section, remplacez `USERNAME` par l’utilisateur à authentifier sur le cluster et `PASSWORD` par le mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="768e0-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="768e0-117">Remplacez `CLUSTERNAME` par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="768e0-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="768e0-118">À partir d’une ligne de commande, exécutez la commande suivante pour vérifier que vous pouvez vous connecter à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="768e0-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="768e0-119">La réponse JSON suivante doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="768e0-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="768e0-120">Les paramètres utilisés dans cette commande sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="768e0-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="768e0-121">**-u**: le nom d’utilisateur et le mot de passe utilisés pour authentifier la demande</span><span class="sxs-lookup"><span data-stu-id="768e0-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="768e0-122">**-G** : indique que la requête correspond à une requête GET.</span><span class="sxs-lookup"><span data-stu-id="768e0-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="768e0-123">Le début de l’URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est le même pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="768e0-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="768e0-124">Le chemin d’accès, **/status**, indique que la demande doit retourner le statut de WebHCat (également appelé Templeton) au serveur.</span><span class="sxs-lookup"><span data-stu-id="768e0-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="768e0-125">Utilisez le code suivant pour soumettre une tâche Pig Latin au cluster :</span><span class="sxs-lookup"><span data-stu-id="768e0-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="768e0-126">Les paramètres utilisés dans cette commande sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="768e0-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="768e0-127">**-d** : étant donné que `-G` n’est pas utilisé, la demande passe par défaut à la méthode POST.</span><span class="sxs-lookup"><span data-stu-id="768e0-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="768e0-128">`-d` spécifie les valeurs de données envoyées avec la demande.</span><span class="sxs-lookup"><span data-stu-id="768e0-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="768e0-129">**user.name**: l’utilisateur qui exécute la commande</span><span class="sxs-lookup"><span data-stu-id="768e0-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="768e0-130">**execute**: les instructions Pig Latin à exécuter</span><span class="sxs-lookup"><span data-stu-id="768e0-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="768e0-131">**statusdir** : le répertoire dans lequel les statuts de cette tâche sont écrits.</span><span class="sxs-lookup"><span data-stu-id="768e0-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="768e0-132">Notez que les espaces dans les instructions Pig Latin sont remplacées par le caractère `+` avec Curl.</span><span class="sxs-lookup"><span data-stu-id="768e0-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="768e0-133">Cette commande doit retourner un ID de tâche qui peut être utilisé pour vérifier le statut de la tâche, par exemple :</span><span class="sxs-lookup"><span data-stu-id="768e0-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="768e0-134">Pour vérifier le statut de la tâche, utilisez la commande suivante</span><span class="sxs-lookup"><span data-stu-id="768e0-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="768e0-135">Remplacez `JOBID` par la valeur renvoyée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="768e0-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="768e0-136">Par exemple, si la valeur de retour était `{"id":"job_1415651640909_0026"}`, alors `JOBID` est `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="768e0-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="768e0-137">Si la tâche est terminée, l’état est **TERMINÉ**.</span><span class="sxs-lookup"><span data-stu-id="768e0-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="768e0-138">Cette requête Curl retourne un document JSON (JavaScript Object Notation) avec des informations sur la tâche et jq est utilisé pour récupérer uniquement la valeur d’état.</span><span class="sxs-lookup"><span data-stu-id="768e0-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="768e0-139"><a id="results"></a>Affichage des résultats</span><span class="sxs-lookup"><span data-stu-id="768e0-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="768e0-140">Une fois que le statut de la tâche est passé à **TERMINÉ**, vous pouvez récupérer les résultats.</span><span class="sxs-lookup"><span data-stu-id="768e0-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="768e0-141">Le paramètre `statusdir` transmis avec la requête contient l’emplacement du fichier de sortie. Dans notre cas `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="768e0-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="768e0-142">HDInsight peut utiliser le stockage Azure ou Azure Data Lake Store comme magasin de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="768e0-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="768e0-143">Il existe différentes façons d’obtenir les données en fonction de celles que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="768e0-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="768e0-144">Pour plus d’informations, consultez la section relative au stockage, dans le document [Informations sur HDInsight sous Linux](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="768e0-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="768e0-145"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="768e0-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="768e0-146">Comme illustré dans ce document, vous pouvez utiliser les demandes HTTP brutes pour exécuter, surveiller et afficher les résultats de tâches Pig sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="768e0-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="768e0-147">Pour plus d’informations sur l’interface REST utilisée dans cet article, consultez la [Référence WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="768e0-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="768e0-148"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="768e0-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="768e0-149">Pour obtenir des informations générales sur Pig dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="768e0-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="768e0-150">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="768e0-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="768e0-151">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="768e0-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="768e0-152">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="768e0-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="768e0-153">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="768e0-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
