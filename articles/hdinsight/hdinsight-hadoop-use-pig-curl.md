---
title: aaaUse Hadoop Pig reste dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment les travaux de Pig Latin toorun toouse reste sur un Hadoop cluster dans Azure HDInsight."
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
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="372d3-103">Exécution de tâches Pig avec Hadoop sur HDInsight à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="372d3-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="372d3-104">Découvrez comment des travaux en rendant le cluster Azure HDInsight REST demandes tooan toorun Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="372d3-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="372d3-105">Curl est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide de hello WebHCat REST API.</span><span class="sxs-lookup"><span data-stu-id="372d3-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="372d3-106">Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont tooHDInsight nouvelle, consultez [conseils de HDInsight basés sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="372d3-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="372d3-107"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="372d3-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="372d3-108">Un cluster Azure HDInsight (Hadoop sur HDInsight) Windows ou Linux</span><span class="sxs-lookup"><span data-stu-id="372d3-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="372d3-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="372d3-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="372d3-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="372d3-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="372d3-111">Curl</span><span class="sxs-lookup"><span data-stu-id="372d3-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="372d3-112">jq</span><span class="sxs-lookup"><span data-stu-id="372d3-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="372d3-113"><a id="curl"></a>Exécution de tâches Pig à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="372d3-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="372d3-114">API REST Hello est sécurisé via [l’authentification d’accès de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="372d3-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="372d3-115">Toujours effectuer des demandes à l’aide de tooensure HTTP sécurisée (HTTPS) que vos informations d’identification sont envoyées en toute sécurité toohello server.</span><span class="sxs-lookup"><span data-stu-id="372d3-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="372d3-116">Lorsque vous utilisez des commandes hello dans cette section, remplacez `USERNAME` avec cluster de toohello tooauthenticate hello utilisateur, puis remplacez `PASSWORD` avec mot de passe hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="372d3-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="372d3-117">Remplacez `CLUSTERNAME` avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="372d3-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="372d3-118">À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :</span><span class="sxs-lookup"><span data-stu-id="372d3-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="372d3-119">Vous devez recevoir hello suivant de réponse JSON :</span><span class="sxs-lookup"><span data-stu-id="372d3-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="372d3-120">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="372d3-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="372d3-121">**-u**: nom d’utilisateur hello et le mot de passe utilisé demande de hello tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="372d3-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="372d3-122">**-G** : indique que la requête correspond à une requête GET.</span><span class="sxs-lookup"><span data-stu-id="372d3-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="372d3-123">Bonjour à partir de l’URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est hello identique pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="372d3-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="372d3-124">chemin d’accès de Hello, **/Status**, indique cette demande hello est état hello tooreturn WebHCat (également appelé Templeton) pour le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="372d3-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="372d3-125">Utilisez hello suivant code toosubmit un cluster de toohello travail Pig Latin :</span><span class="sxs-lookup"><span data-stu-id="372d3-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="372d3-126">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="372d3-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="372d3-127">**-d**: car `-G` n’est pas utilisé, demande de hello par défaut est la méthode POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="372d3-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="372d3-128">`-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="372d3-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="372d3-129">**User.nom**: utilisateur hello qui commande hello est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="372d3-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="372d3-130">**Exécutez**: hello Pig Latin instructions tooexecute</span><span class="sxs-lookup"><span data-stu-id="372d3-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="372d3-131">**statusdir**: répertoire hello hello l’état de cette tâche est écrite dans</span><span class="sxs-lookup"><span data-stu-id="372d3-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="372d3-132">Notez que les espaces hello dans les instructions de Pig Latin sont remplacés par hello `+` lorsqu’il est utilisé avec Curl de caractères.</span><span class="sxs-lookup"><span data-stu-id="372d3-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="372d3-133">Cette commande doit retourner un ID de tâche qui peut être un état de hello toocheck utilisé hello du travail de, par exemple :</span><span class="sxs-lookup"><span data-stu-id="372d3-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="372d3-134">état de hello toocheck du travail hello, hello utilisez commande suivante</span><span class="sxs-lookup"><span data-stu-id="372d3-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="372d3-135">Remplacez `JOBID` avec la valeur hello retourné à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="372d3-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="372d3-136">Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis `JOBID` est `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="372d3-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="372d3-137">Si le travail de hello terminée, l’état hello est **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="372d3-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="372d3-138">Cette demande Curl retourne une JavaScript Object Notation (JSON) document avec plus d’informations sur la tâche de hello et jq est tooretrieve utilisé hello uniquement la valeur d’état.</span><span class="sxs-lookup"><span data-stu-id="372d3-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="372d3-139"><a id="results"></a>Affichage des résultats</span><span class="sxs-lookup"><span data-stu-id="372d3-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="372d3-140">Lorsque état hello du travail de hello est devenue trop**SUCCEEDED**, vous pouvez récupérer les résultats de hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="372d3-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="372d3-141">Hello `statusdir` passés avec la requête de hello contient l’emplacement hello hello du fichier de sortie ; dans ce cas, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="372d3-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="372d3-142">HDInsight peut utiliser le stockage Azure ou Azure Data Lake Store en tant que banque de données par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="372d3-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="372d3-143">Il existe différentes façons tooget données hello selon l’application que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="372d3-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="372d3-144">Pour plus d’informations, consultez la section de stockage hello Hello [basés sur Linux de HDInsight informations](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span><span class="sxs-lookup"><span data-stu-id="372d3-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="372d3-145"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="372d3-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="372d3-146">Comme illustré dans ce document, vous pouvez utiliser un toorun de demande HTTP brut, d’analyse et d’afficher les résultats des travaux de Pig hello sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="372d3-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="372d3-147">Pour plus d’informations sur l’interface REST de hello utilisée dans cet article, consultez hello [WebHCat référence](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="372d3-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="372d3-148"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="372d3-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="372d3-149">Pour obtenir des informations générales sur Pig dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="372d3-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="372d3-150">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="372d3-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="372d3-151">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="372d3-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="372d3-152">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="372d3-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="372d3-153">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="372d3-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
