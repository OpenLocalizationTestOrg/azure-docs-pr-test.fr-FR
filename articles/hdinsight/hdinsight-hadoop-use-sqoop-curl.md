---
title: aaaUse Hadoop Sqoop avec Curl dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooremotely soumettre Sqoop tooHDInsight de travaux à l’aide de Curl."
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="2be08-103">Exécution de travaux Sqoop avec Hadoop dans HDInsight via Curl</span><span class="sxs-lookup"><span data-stu-id="2be08-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="2be08-104">Découvrez comment de cluster toouse Curl toorun Sqoop travaux sur un Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2be08-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="2be08-105">Curl est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide de toorun de demandes HTTP brut, analyse et récupérer les résultats de hello de Sqoop travaux.</span><span class="sxs-lookup"><span data-stu-id="2be08-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="2be08-106">Cela fonctionne à l’aide de hello WebHCat API REST (anciennement Templeton) fournie par votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2be08-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="2be08-107">Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont tooHDInsight nouvelle, consultez [plus d’informations sur l’utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="2be08-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2be08-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2be08-108">Prerequisites</span></span>
<span data-ttu-id="2be08-109">toocomplete hello étapes décrites dans cet article, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="2be08-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="2be08-110">Un cluster Hadoop sur HDInsight (Linux ou Windows)</span><span class="sxs-lookup"><span data-stu-id="2be08-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="2be08-111">Curl</span><span class="sxs-lookup"><span data-stu-id="2be08-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="2be08-112">jq</span><span class="sxs-lookup"><span data-stu-id="2be08-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="2be08-113">Envoi de travaux Sqoop avec Curl</span><span class="sxs-lookup"><span data-stu-id="2be08-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="2be08-114">Lorsque vous utilisez Curl ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le nom d’utilisateur hello et mot de passe administrateur de cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2be08-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="2be08-115">Vous devez également utiliser le nom du cluster hello comme partie d’identificateur de ressource uniforme (URI) de hello utilisé serveur toohello de toosend hello demandes.</span><span class="sxs-lookup"><span data-stu-id="2be08-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="2be08-116">Pour les commandes hello dans cette section, remplacez **nom d’utilisateur** avec cluster de toohello tooauthenticate hello utilisateur, puis remplacez **mot de passe** avec mot de passe hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2be08-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="2be08-117">Remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="2be08-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="2be08-118">API REST Hello est sécurisé via [l’authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="2be08-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="2be08-119">Vous devez toujours effectuer des requêtes en utilisant HTTP sécurisée (HTTPS) toohelp vous assurer que vos informations d’identification sont envoyées en toute sécurité toohello server.</span><span class="sxs-lookup"><span data-stu-id="2be08-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="2be08-120">À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :</span><span class="sxs-lookup"><span data-stu-id="2be08-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="2be08-121">Vous devez recevoir une suivant toohello similaire de réponse :</span><span class="sxs-lookup"><span data-stu-id="2be08-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="2be08-122">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2be08-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="2be08-123">**-u** -nom d’utilisateur hello et le mot de passe de demande de hello tooauthenticate utilisé.</span><span class="sxs-lookup"><span data-stu-id="2be08-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="2be08-124">**-G** : indique qu’il s’agit d’une demande GET.</span><span class="sxs-lookup"><span data-stu-id="2be08-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="2be08-125">Bonjour à partir de l’URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sera hello identique pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="2be08-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="2be08-126">chemin d’accès de Hello, **/Status**, indique cette demande hello est tooreturn état WebHCat (également appelé Templeton) pour le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="2be08-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="2be08-127">Utilisez hello suivant toosubmit un travail sqoop :</span><span class="sxs-lookup"><span data-stu-id="2be08-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="2be08-128">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2be08-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="2be08-129">**-d** - depuis `-G` n’est pas utilisé, demande de hello par défaut est la méthode POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="2be08-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="2be08-130">`-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="2be08-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="2be08-131">**User.nom** -utilisateur hello qui commande hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2be08-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="2be08-132">**commande** -hello Sqoop commande tooexecute.</span><span class="sxs-lookup"><span data-stu-id="2be08-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="2be08-133">**statusdir** -répertoire hello hello l’état de cette tâche sera écrit dans.</span><span class="sxs-lookup"><span data-stu-id="2be08-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="2be08-134">Cette commande doit retourner un ID de tâche qui peut être l’état de hello toocheck utilisés du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="2be08-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="2be08-135">état de hello toocheck du travail hello, hello utilisez commande suivante.</span><span class="sxs-lookup"><span data-stu-id="2be08-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="2be08-136">Remplacez **JOBID** avec la valeur hello retourné à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="2be08-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="2be08-137">Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis **JOBID** serait `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="2be08-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="2be08-138">Si le travail de hello terminée, hello état n’aura pas **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="2be08-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2be08-139">Cette demande Curl retourne un document JavaScript Objet Notation (JSON) avec des informations sur la tâche de hello ; jq sert tooretrieve hello uniquement la valeur d’état.</span><span class="sxs-lookup"><span data-stu-id="2be08-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="2be08-140">Une fois que l’état hello du travail de hello a changé trop**SUCCEEDED**, vous pouvez récupérer les résultats de hello du travail de hello à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2be08-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="2be08-141">Hello `statusdir` passés avec la requête de hello contient l’emplacement hello hello du fichier de sortie ; dans ce cas, **wasb : / / exemple/curl**.</span><span class="sxs-lookup"><span data-stu-id="2be08-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="2be08-142">Cette adresse stocke la sortie hello du travail de hello Bonjour **exemple/curl** répertoire sur le conteneur de stockage hello par défaut utilisé par votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2be08-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="2be08-143">Vous pouvez répertorier et télécharger ces fichiers à l’aide de hello [CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2be08-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="2be08-144">Par exemple, fichiers toolist **exemple/curl**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2be08-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="2be08-145">toodownload un fichier, utilisez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="2be08-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="2be08-146">Vous devez spécifier soit le nom de compte de stockage hello qui contient l’objet blob de hello à l’aide de hello `-a` et `-k` paramètres, ou ensemble hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_accès\_clé** variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="2be08-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="2be08-147">Consultez <a href="hdinsight-upload-data.md" target="_blank" pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="2be08-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="2be08-148">Limites</span><span class="sxs-lookup"><span data-stu-id="2be08-148">Limitations</span></span>
* <span data-ttu-id="2be08-149">L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="2be08-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="2be08-150">Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.</span><span class="sxs-lookup"><span data-stu-id="2be08-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="2be08-151">Résumé</span><span class="sxs-lookup"><span data-stu-id="2be08-151">Summary</span></span>
<span data-ttu-id="2be08-152">Comme illustré dans ce document, vous pouvez utiliser un toorun de demande HTTP brut, analyse et afficher les résultats des travaux de Sqoop hello sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2be08-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="2be08-153">Pour plus d’informations sur l’interface REST de hello utilisée dans cet article, consultez hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guide de l’API REST de Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="2be08-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2be08-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2be08-154">Next steps</span></span>
<span data-ttu-id="2be08-155">Pour obtenir des informations générales sur Hive avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2be08-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="2be08-156">Utilisation de Sqoop avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2be08-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="2be08-157">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2be08-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2be08-158">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2be08-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2be08-159">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2be08-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2be08-160">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2be08-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


