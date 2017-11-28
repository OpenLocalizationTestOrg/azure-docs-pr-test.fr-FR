---
title: Utiliser Hadoop Sqoop avec Curl dans HDInsight - Azure | Microsoft Docs
description: "Découvrez comment transmettre à distance des travaux Sqoop vers HDInsight à l’aide de Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="def2f-103">Exécution de travaux Sqoop avec Hadoop dans HDInsight via Curl</span><span class="sxs-lookup"><span data-stu-id="def2f-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="def2f-104">Apprenez à utiliser Curl pour exécuter des tâches Sqoop sur un cluster Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2f-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="def2f-105">Curl est utilisé pour illustrer comment interagir avec HDInsight en utilisant des demandes HTTP brutes pour exécuter, analyser et récupérer des travaux Sqoop.</span><span class="sxs-lookup"><span data-stu-id="def2f-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="def2f-106">Cela fonctionne à l’aide de l’API REST WebHCat (anciennement Templeton) fournie par votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2f-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="def2f-107">Si vous connaissez déjà l’utilisation de serveurs Hadoop basés sur Linux, mais pas HDInsight, consultez la rubrique [Informations sur l’utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="def2f-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="def2f-108">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="def2f-108">Prerequisites</span></span>
<span data-ttu-id="def2f-109">Pour effectuer les étapes présentées dans cet article, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="def2f-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="def2f-110">Un cluster Hadoop sur HDInsight (Linux ou Windows)</span><span class="sxs-lookup"><span data-stu-id="def2f-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="def2f-111">Curl</span><span class="sxs-lookup"><span data-stu-id="def2f-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="def2f-112">jq</span><span class="sxs-lookup"><span data-stu-id="def2f-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="def2f-113">Envoi de travaux Sqoop avec Curl</span><span class="sxs-lookup"><span data-stu-id="def2f-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="def2f-114">Lorsque vous utilisez Curl ou toute autre communication REST avec WebHCat, vous devez authentifier les demandes en fournissant le nom d'utilisateur et le mot de passe de l'administrateur du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2f-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="def2f-115">Vous devez également utiliser le nom du cluster dans l’URI (Uniform Resource Identifier) utilisé pour envoyer les demandes au serveur.</span><span class="sxs-lookup"><span data-stu-id="def2f-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="def2f-116">Pour les commandes de cette section, remplacez **USERNAME** par l’utilisateur à authentifier sur le cluster et **PASSWORD** par le mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="def2f-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="def2f-117">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="def2f-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="def2f-118">L’API REST est sécurisée à l’aide de l’ [authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="def2f-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="def2f-119">Vous devez toujours effectuer les demandes à l’aide du protocole Secure HTTP (HTTPS) pour aider à vous assurer que vos informations d’identification sont envoyées en toute sécurité sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="def2f-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="def2f-120">À partir d’une ligne de commande, exécutez la commande suivante pour vérifier que vous pouvez vous connecter à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2f-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="def2f-121">Vous devez recevoir une réponse ayant l'aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="def2f-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="def2f-122">Les paramètres utilisés dans cette commande sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="def2f-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="def2f-123">**-u** : le nom d’utilisateur et le mot de passe utilisés pour authentifier la demande.</span><span class="sxs-lookup"><span data-stu-id="def2f-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="def2f-124">**-G** : indique qu’il s’agit d’une demande GET.</span><span class="sxs-lookup"><span data-stu-id="def2f-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="def2f-125">Le début de l’URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sera le même pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="def2f-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="def2f-126">Le chemin d’accès, **/status**, indique que la demande doit renvoyer le statut de WebHCat (également appelé Templeton) au serveur.</span><span class="sxs-lookup"><span data-stu-id="def2f-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="def2f-127">Pour envoyer un travail Sqoop, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="def2f-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="def2f-128">Les paramètres utilisés dans cette commande sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="def2f-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="def2f-129">**-d** : étant donné que `-G` n’est pas utilisé, la demande passe par défaut à la méthode POST.</span><span class="sxs-lookup"><span data-stu-id="def2f-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="def2f-130">`-d` spécifie les valeurs de données envoyées avec la demande.</span><span class="sxs-lookup"><span data-stu-id="def2f-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="def2f-131">**user.name** : l’utilisateur qui exécute la commande.</span><span class="sxs-lookup"><span data-stu-id="def2f-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="def2f-132">**command** : commande Sqoop à exécuter.</span><span class="sxs-lookup"><span data-stu-id="def2f-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="def2f-133">**statusdir** : le répertoire où seront enregistrés les statuts de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="def2f-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="def2f-134">Cette commande doit retourner un ID de tâche qui peut être utilisé pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="def2f-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="def2f-135">Pour vérifier le statut de la tâche, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="def2f-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="def2f-136">Remplacez **JOBID** par la valeur retournée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="def2f-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="def2f-137">Par exemple, si la valeur de retour était `{"id":"job_1415651640909_0026"}`, le **JOBID** est `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="def2f-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="def2f-138">Si le travail est terminé, l’état est **TERMINÉ**.</span><span class="sxs-lookup"><span data-stu-id="def2f-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="def2f-139">Cette demande Curl retourne un document JSON (JavaScript Object Notation) avec des informations sur la tâche ; jq est utilisé pour récupérer uniquement la valeur de statut.</span><span class="sxs-lookup"><span data-stu-id="def2f-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="def2f-140">Une fois que le statut de la tâche est passé à **TERMINÉ**, vous pouvez récupérer les résultats depuis le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="def2f-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="def2f-141">Le paramètre `statusdir` transmis avec la requête contient l’emplacement du fichier de sortie ; dans notre cas, **wasb:///exemple/curl**.</span><span class="sxs-lookup"><span data-stu-id="def2f-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="def2f-142">Cette adresse stocke la sortie de la tâche dans le répertoire **exemple/curl** sur le conteneur de stockage par défaut utilisé par votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2f-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="def2f-143">Vous pouvez répertorier et télécharger ces fichiers à l’aide de l' [interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="def2f-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="def2f-144">Par exemple, pour répertorier les fichiers dans **exemple/curl**, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="def2f-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="def2f-145">Pour télécharger un fichier, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="def2f-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="def2f-146">Vous devez spécifier le nom du compte de stockage qui contient l’objet blob à l’aide des paramètres `-a` et `-k`, ou définir les variables d’environnement **AZURE\_STORAGE\_ACCOUNT** et **AZURE\_STORAGE\_ACCESS\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="def2f-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="def2f-147">Consultez <a href="hdinsight-upload-data.md" target="_blank" pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="def2f-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="def2f-148">Limitations</span><span class="sxs-lookup"><span data-stu-id="def2f-148">Limitations</span></span>
* <span data-ttu-id="def2f-149">Exportation en bloc : avec HDInsight sous Linux, le connecteur Sqoop utilisé pour exporter des données vers Microsoft SQL Server ou la base de données SQL Azure ne prend pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="def2f-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="def2f-150">Traitement par lots : avec HDInsight sous Linux, lorsque vous utilisez le commutateur `-batch` pour effectuer des insertions, Sqoop effectue plusieurs insertions plutôt qu’un traitement par lots des opérations d’insertion.</span><span class="sxs-lookup"><span data-stu-id="def2f-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="def2f-151">Résumé</span><span class="sxs-lookup"><span data-stu-id="def2f-151">Summary</span></span>
<span data-ttu-id="def2f-152">Comme illustré dans ce document, vous pouvez utiliser une demande HTTP brute pour exécuter, surveiller et afficher les résultats des travaux Sqoop sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="def2f-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="def2f-153">Pour plus d’informations sur l’interface REST utilisée dans cet article, consultez le document <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a> (Guide de l’API REST Sqoop).</span><span class="sxs-lookup"><span data-stu-id="def2f-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="def2f-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="def2f-154">Next steps</span></span>
<span data-ttu-id="def2f-155">Pour obtenir des informations générales sur Hive avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="def2f-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="def2f-156">Utilisation de Sqoop avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="def2f-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="def2f-157">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="def2f-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="def2f-158">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="def2f-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="def2f-159">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="def2f-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="def2f-160">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="def2f-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


