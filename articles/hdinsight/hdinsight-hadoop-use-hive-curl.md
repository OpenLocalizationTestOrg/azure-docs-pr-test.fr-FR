---
title: aaaUse Hadoop Hive avec Curl dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooremotely submit Pig travaux tooHDInsight à l’aide de Curl."
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
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="c597e-103">Exécuter des requêtes Hive avec Hadoop dans HDInsight à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="c597e-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="c597e-104">Découvrez le fonctionnement des requêtes avec Hadoop toouse hello WebHCat REST API toorun Hive sur un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c597e-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="c597e-105">[Curl](http://curl.haxx.se/) est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide des requêtes HTTP bruts.</span><span class="sxs-lookup"><span data-stu-id="c597e-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="c597e-106">Hello [jq](http://stedolan.github.io/jq/) utilitaire donnée utilisé tooprocess hello JSON retourné à partir de demandes REST.</span><span class="sxs-lookup"><span data-stu-id="c597e-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="c597e-107">Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont tooHDInsight nouvelle, consultez hello [ce dont vous avez besoin tooknow sur Hadoop dans HDInsight de basés sur Linux](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="c597e-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="c597e-108"><a id="curl"></a>Exécuter des requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="c597e-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="c597e-109">Lorsque vous utilisez cURL ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le nom d’utilisateur hello et mot de passe administrateur de cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="c597e-110">Pour les commandes hello dans cette section, remplacez **nom d’utilisateur** avec cluster de toohello tooauthenticate hello utilisateur, puis remplacez **mot de passe** avec mot de passe hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c597e-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="c597e-111">Remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c597e-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="c597e-112">API REST Hello est sécurisé via [l’authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="c597e-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="c597e-113">toohelp Assurez-vous que vos informations d’identification en toute sécurité envoyé toohello server, vérifiez systématiquement les demandes à l’aide de HTTP sécurisée (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="c597e-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="c597e-114">À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :</span><span class="sxs-lookup"><span data-stu-id="c597e-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="c597e-115">Vous recevez un toohello similaire de réponse après le texte :</span><span class="sxs-lookup"><span data-stu-id="c597e-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="c597e-116">paramètres de Hello utilisés dans cette commande sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="c597e-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="c597e-117">**-u** -nom d’utilisateur hello et le mot de passe de demande de hello tooauthenticate utilisé.</span><span class="sxs-lookup"><span data-stu-id="c597e-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="c597e-118">**-G**: indique que la requête correspond à une opération GET.</span><span class="sxs-lookup"><span data-stu-id="c597e-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="c597e-119">Bonjour à partir de l’URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est hello identique pour toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="c597e-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="c597e-120">chemin d’accès de Hello, **/Status**, indique cette demande hello est tooreturn état WebHCat (également appelé Templeton) pour le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="c597e-121">Vous pouvez également demander la version hello de ruche à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c597e-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="c597e-122">Cette requête retourne un toohello similaire de réponse après le texte :</span><span class="sxs-lookup"><span data-stu-id="c597e-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="c597e-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="c597e-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="c597e-124">Hello utilisation suivant toocreate une table nommée **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="c597e-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="c597e-125">Hello utilisés avec cette demande de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c597e-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="c597e-126">**-d** - depuis `-G` n’est pas utilisé, demande de hello par défaut est la méthode POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="c597e-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="c597e-127">`-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="c597e-128">**User.nom** -utilisateur hello qui commande hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c597e-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="c597e-129">**Exécutez** -hello tooexecute d’instructions HiveQL.</span><span class="sxs-lookup"><span data-stu-id="c597e-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="c597e-130">**statusdir** -répertoire hello hello l’état de cette tâche est écrite dans.</span><span class="sxs-lookup"><span data-stu-id="c597e-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="c597e-131">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="c597e-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="c597e-132">**DROP TABLE** -si hello table existe déjà, elle est supprimée.</span><span class="sxs-lookup"><span data-stu-id="c597e-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="c597e-133">**CREATE EXTERNAL TABLE** : crée une table « externe » dans Hive.</span><span class="sxs-lookup"><span data-stu-id="c597e-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="c597e-134">Tables externes stockent uniquement la définition de table hello dans la ruche.</span><span class="sxs-lookup"><span data-stu-id="c597e-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="c597e-135">les données de salutation reste dans l’emplacement d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c597e-136">Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe.</span><span class="sxs-lookup"><span data-stu-id="c597e-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="c597e-137">par exemple, par un processus de téléchargement de données automatisé ou une autre opération MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c597e-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="c597e-138">Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="c597e-139">**FORMAT de ligne** - mise en forme les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="c597e-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="c597e-140">champs de Hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="c597e-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="c597e-141">**EMPLACEMENT du fichier texte comme stockées** - emplacement de stockage des données de salutation (répertoire de données d’exemple hello) et qu’il est stocké sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="c597e-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="c597e-142">**Sélectionnez** -sélectionne un nombre de toutes les lignes où colonne **t4** contient la valeur de hello **[erreur]**.</span><span class="sxs-lookup"><span data-stu-id="c597e-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="c597e-143">Cette instruction renvoie la valeur **3**, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c597e-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c597e-144">Notez que les espaces hello entre les instructions HiveQL sont remplacés par hello `+` lorsqu’il est utilisé avec Curl de caractères.</span><span class="sxs-lookup"><span data-stu-id="c597e-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="c597e-145">Les valeurs entre guillemets qui contiennent un espace, comme délimiteur de hello, ne doivent pas être remplacés par `+`.</span><span class="sxs-lookup"><span data-stu-id="c597e-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="c597e-146">**INPUT__FILE__NAME comme '% 25.log'** - cette instruction limites hello recherche tooonly utilisation de fichiers se terminant par. journal.</span><span class="sxs-lookup"><span data-stu-id="c597e-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c597e-147">Hello `%25` étant formulaire codées URL de hello %, condition réelle de hello est `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="c597e-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="c597e-148">Hello % a URL toobe codée, comme il est traité comme un caractère spécial dans les URL.</span><span class="sxs-lookup"><span data-stu-id="c597e-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="c597e-149">Cette commande doit retourner un ID de tâche qui peut être l’état de hello toocheck utilisés du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="c597e-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="c597e-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="c597e-151">état de hello toocheck du travail hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c597e-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="c597e-152">Remplacez **JOBID** avec la valeur hello retourné à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="c597e-153">Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis **JOBID** serait `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="c597e-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="c597e-154">Si le travail de hello terminée, l’état hello est **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="c597e-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c597e-155">Cette demande Curl retourne un document JavaScript Objet Notation (JSON) avec des informations sur la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="c597e-156">Jq sert tooretrieve hello uniquement la valeur d’état.</span><span class="sxs-lookup"><span data-stu-id="c597e-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="c597e-157">Une fois que l’état hello du travail de hello a changé trop**SUCCEEDED**, vous pouvez récupérer les résultats de hello du travail de hello à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="c597e-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="c597e-158">Hello `statusdir` passés avec la requête de hello contient l’emplacement hello hello du fichier de sortie ; dans ce cas, **/exemple/curl**.</span><span class="sxs-lookup"><span data-stu-id="c597e-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="c597e-159">Cette adresse stocke la sortie de hello Bonjour **exemple/curl** directory Bonjour clusters de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="c597e-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="c597e-160">Vous pouvez répertorier et télécharger ces fichiers à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c597e-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="c597e-161">Pour plus d’informations sur l’utilisation de hello CLI d’Azure avec le stockage Azure, consultez hello [utiliser Azure CLI 2.0 avec le stockage Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="c597e-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="c597e-162">Hello utilisation suivant les instructions toocreate une nouvelle table « interne » nommée **journaux d’erreurs de**:</span><span class="sxs-lookup"><span data-stu-id="c597e-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="c597e-163">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="c597e-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="c597e-164">**CREATE TABLE IF NOT EXISTS** : crée une table, si elle n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="c597e-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="c597e-165">Cette instruction crée une table interne, qui est stockée dans l’entrepôt de données Hive hello et entièrement gérée par ruche.</span><span class="sxs-lookup"><span data-stu-id="c597e-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c597e-166">Contrairement aux tables externes, la suppression d’une table interne supprime également des données sous-jacentes hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="c597e-167">**ORC de AS stockées** -stocke les données de hello dans format optimisé lignes en colonnes (ORC).</span><span class="sxs-lookup"><span data-stu-id="c597e-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="c597e-168">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="c597e-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="c597e-169">**INSERT OVERWRITE ... Sélectionnez** -sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des **[erreur]**, puis insère hello des données dans hello **journaux d’erreurs de** table.</span><span class="sxs-lookup"><span data-stu-id="c597e-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="c597e-170">**Sélectionnez** -sélectionne toutes les lignes à partir de hello nouvelle **journaux d’erreurs de** table.</span><span class="sxs-lookup"><span data-stu-id="c597e-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="c597e-171">Utilisez l’ID de tâche hello a retourné l’état de hello toocheck du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="c597e-172">Une fois qu’elle a réussi, utilisez hello CLI d’Azure comme décrit précédemment toodownload et afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="c597e-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="c597e-173">sortie de Hello doit contenir trois lignes, qui contiennent toutes des **[erreur]**.</span><span class="sxs-lookup"><span data-stu-id="c597e-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="c597e-174"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c597e-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c597e-175">Pour obtenir des informations générales sur Hive avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c597e-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="c597e-176">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c597e-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="c597e-177">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c597e-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c597e-178">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c597e-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c597e-179">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c597e-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c597e-180">Si vous utilisez Tez avec Hive, consultez hello suivant des documents pour les informations de débogage :</span><span class="sxs-lookup"><span data-stu-id="c597e-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="c597e-181">Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="c597e-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="c597e-182">Pour plus d’informations sur hello API REST utilisé dans ce document, consultez hello [WebHCat référence](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span><span class="sxs-lookup"><span data-stu-id="c597e-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


