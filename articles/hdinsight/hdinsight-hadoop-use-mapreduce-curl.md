---
title: aaaUse MapReduce et Curl avec Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooremotely exécuter les tâches MapReduce avec Hadoop dans HDInsight à l’aide de Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="7d39b-103">Exécution des tâches MapReduce avec Hadoop sur HDInsight avec REST</span><span class="sxs-lookup"><span data-stu-id="7d39b-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="7d39b-104">Découvrez comment toouse hello WebHCat REST API toorun MapReduce travaux sur un Hadoop sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d39b-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="7d39b-105">Curl est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide de travaux de MapReduce toorun de demandes HTTP bruts.</span><span class="sxs-lookup"><span data-stu-id="7d39b-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="7d39b-106">Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont de nouveau tooHDInsight, consultez hello [ce dont vous avez besoin tooknow sur basés sur Linux de Hadoop dans HDInsight](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="7d39b-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="7d39b-107"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7d39b-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7d39b-108">Un cluster Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d39b-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="7d39b-109">Curl</span><span class="sxs-lookup"><span data-stu-id="7d39b-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="7d39b-110">jq</span><span class="sxs-lookup"><span data-stu-id="7d39b-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="7d39b-111"><a id="curl"></a>Exécution de tâches MapReduce à l'aide de Curl</span><span class="sxs-lookup"><span data-stu-id="7d39b-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="7d39b-112">Lorsque vous utilisez Curl ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le mot de passe et le nom d’utilisateur administrateur hello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7d39b-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="7d39b-113">Vous devez utiliser le nom du cluster hello dans le cadre de hello URI qui est utilisé toosend hello demandes toohello serveur.</span><span class="sxs-lookup"><span data-stu-id="7d39b-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="7d39b-114">Pour les commandes hello dans cette section, remplacez **nom d’utilisateur** avec cluster de hello utilisateur tooauthenticate toohello, et **mot de passe** avec mot de passe hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7d39b-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="7d39b-115">Remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7d39b-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="7d39b-116">API REST Hello est sécurisé à l’aide de [l’authentification d’accès de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="7d39b-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="7d39b-117">Vous devez toujours effectuer des requêtes en utilisant tooensure HTTPS que vos informations d’identification sont envoyées en toute sécurité toohello server.</span><span class="sxs-lookup"><span data-stu-id="7d39b-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="7d39b-118">À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :</span><span class="sxs-lookup"><span data-stu-id="7d39b-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="7d39b-119">Vous devez recevoir un toohello similaire de réponse suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="7d39b-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="7d39b-120">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d39b-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="7d39b-121">**-u**: indique le nom d’utilisateur hello et le mot de passe utilisé demande de hello tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="7d39b-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="7d39b-122">**-G**: indique que cette opération est une requête GET</span><span class="sxs-lookup"><span data-stu-id="7d39b-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="7d39b-123">Bonjour à partir de hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est hello identique pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="7d39b-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="7d39b-124">toosubmit une tâche MapReduce, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7d39b-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="7d39b-125">fin de Hello Hello URI/mapreduce/jar () indique WebHCat que cette demande démarre une tâche MapReduce à partir d’une classe dans un fichier jar.</span><span class="sxs-lookup"><span data-stu-id="7d39b-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="7d39b-126">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d39b-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="7d39b-127">**-d**: `-G` n’est pas utilisé, afin de la demande de hello par défaut est la méthode POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="7d39b-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="7d39b-128">`-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="7d39b-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="7d39b-129">**User.nom**: utilisateur hello qui commande hello est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="7d39b-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="7d39b-130">**JAR**: emplacement hello du fichier jar hello qui contient la classe toobe a exécuté.</span><span class="sxs-lookup"><span data-stu-id="7d39b-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="7d39b-131">**classe**: hello de classe qui contient la logique hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="7d39b-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="7d39b-132">**arg**: hello arguments toobe passé toohello MapReduce travail.</span><span class="sxs-lookup"><span data-stu-id="7d39b-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="7d39b-133">Dans ce cas, le répertoire de fichiers et de hello texte qui sont utilisés pour la sortie de hello d’entrée hello</span><span class="sxs-lookup"><span data-stu-id="7d39b-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="7d39b-134">Cette commande doit retourner un ID de tâche qui peut être l’état de hello toocheck utilisés du travail de hello :</span><span class="sxs-lookup"><span data-stu-id="7d39b-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="7d39b-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="7d39b-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="7d39b-136">état de hello toocheck du travail hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7d39b-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="7d39b-137">Remplacez hello **JOBID** avec la valeur hello retourné à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7d39b-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="7d39b-138">Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis les hello JOBID serait `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="7d39b-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="7d39b-139">Si le travail de hello est terminée, état de hello retournée est `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="7d39b-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7d39b-140">Cette demande Curl retourne un document JSON avec des informations sur la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="7d39b-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="7d39b-141">Jq sert tooretrieve hello uniquement la valeur d’état.</span><span class="sxs-lookup"><span data-stu-id="7d39b-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="7d39b-142">Lorsque état hello du travail de hello est devenue trop`SUCCEEDED`, vous pouvez récupérer les résultats de hello du travail de hello à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d39b-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="7d39b-143">Hello `statusdir` paramètre est passé avec la requête de hello contient l’emplacement hello hello du fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="7d39b-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="7d39b-144">Dans cet exemple, emplacement de hello est `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="7d39b-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="7d39b-145">Cette adresse stocke sortie hello du travail de hello dans le stockage de valeur par défaut de clusters hello à `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="7d39b-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="7d39b-146">Vous pouvez répertorier et télécharger ces fichiers à l’aide de hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7d39b-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="7d39b-147">Pour plus d’informations sur l’utilisation des objets BLOB à partir de hello CLI d’Azure, consultez hello [Using hello Azure CLI 2.0 avec le stockage Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="7d39b-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="7d39b-148"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d39b-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7d39b-149">Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7d39b-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="7d39b-150">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d39b-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7d39b-151">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7d39b-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7d39b-152">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d39b-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7d39b-153">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d39b-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="7d39b-154">Pour plus d’informations sur l’interface REST hello qui est utilisé dans cet article, consultez hello [WebHCat référence](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="7d39b-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
