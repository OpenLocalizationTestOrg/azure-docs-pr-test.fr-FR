---
title: "aaaAnalyze données Twitter avec Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse ruche tooanalyze Twitter données sur Hadoop dans HDInsight toofind hello fréquence d’utilisation d’un mot particulier."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="762f6-103">Analyse des données Twitter avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="762f6-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="762f6-104">Sites Web sociaux sont une des forces positives de hello principaux pour l’adoption des données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="762f6-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="762f6-105">Les API publiques fournies par des sites comme Twitter représentent une source de données utile pour l'analyse et la compréhension des tendances populaires.</span><span class="sxs-lookup"><span data-stu-id="762f6-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="762f6-106">Dans ce didacticiel, vous obtenir tweets à l’aide d’un API de diffusion en continu de Twitter et utilisez Apache Hive Azure HDInsight tooget une liste d’utilisateurs Twitter qui a envoyé hello la plupart des tweets contenant un mot.</span><span class="sxs-lookup"><span data-stu-id="762f6-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="762f6-107">Hello étapes décrites dans ce document nécessitent un cluster HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="762f6-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="762f6-108">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="762f6-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="762f6-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="762f6-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="762f6-110">Pour étapes tooa spécifiques basés sur Linux de cluster, consultez [analyser Twitter des données à l’aide de la ruche dans HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="762f6-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="762f6-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="762f6-111">Prerequisites</span></span>
<span data-ttu-id="762f6-112">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="762f6-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="762f6-113">**poste de travail** sur lequel Azure PowerShell est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="762f6-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="762f6-114">tooexecute scripts Windows PowerShell, vous devez exécuter Azure PowerShell en tant qu’administrateur et définir la stratégie d’exécution de hello trop*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="762f6-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="762f6-115">Consultez la page [Exécution de scripts Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="762f6-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="762f6-116">Avant d’exécuter des scripts Windows PowerShell, vérifiez que vous êtes connecté tooyour abonnement Azure à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="762f6-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="762f6-117">Si vous avez plusieurs abonnements Azure, utilisez hello suivant l’applet de commande tooset hello abonnement :</span><span class="sxs-lookup"><span data-stu-id="762f6-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="762f6-118">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="762f6-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="762f6-119">étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="762f6-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="762f6-120">Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="762f6-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="762f6-121">Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="762f6-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="762f6-122">Un **cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="762f6-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="762f6-123">Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="762f6-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="762f6-124">Vous devrez le nom du cluster hello plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="762f6-125">Hello tableau suivant répertorie les fichiers hello utilisés dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="762f6-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="762f6-126">Fichiers</span><span class="sxs-lookup"><span data-stu-id="762f6-126">Files</span></span> | <span data-ttu-id="762f6-127">Description</span><span class="sxs-lookup"><span data-stu-id="762f6-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="762f6-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="762f6-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="762f6-129">données de sources Hello pour le travail de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="762f6-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="762f6-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="762f6-131">dossier de sortie Hello pour le travail de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="762f6-132">Bonjour nom de fichier de sortie par défaut ruche de travail est **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="762f6-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="762f6-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="762f6-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="762f6-134">fichier de script HiveQL Hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="762f6-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="762f6-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="762f6-136">état du travail Hadoop de Hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="762f6-137">Obtention du flux Twitter</span><span class="sxs-lookup"><span data-stu-id="762f6-137">Get Twitter feed</span></span>
<span data-ttu-id="762f6-138">Dans ce didacticiel, vous allez utiliser hello [Twitter API de diffusion][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="762f6-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="762f6-139">Bonjour Twitter spécifique, vous allez utiliser des API de diffusion en continu est [États/filtre][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="762f6-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="762f6-140">Un fichier contenant 10 000 tweets et le fichier de script Hive hello (présenté dans la section suivante de hello) a été téléchargé dans un conteneur d’objets Blob public.</span><span class="sxs-lookup"><span data-stu-id="762f6-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="762f6-141">Vous pouvez ignorer cette section si vous souhaitez que les fichiers toouse hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="762f6-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="762f6-142">[Données de tweets](https://dev.twitter.com/docs/platform-objects/tweets) est stocké au format JavaScript Objet Notation (JSON) hello qui contient une structure imbriquée complexe.</span><span class="sxs-lookup"><span data-stu-id="762f6-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="762f6-143">Au lieu d’écrire de nombreuses lignes de code à l’aide d’un langage de programmation classique, vous pouvez transformer cette structure imbriquée en une table Hive, de sorte qu’un langage de type SQL, appelé HiveQL, puisse effectuer une requête sur celle-ci.</span><span class="sxs-lookup"><span data-stu-id="762f6-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="762f6-144">Twitter utilise l’API de tooits accès OAuth tooprovide autorisé.</span><span class="sxs-lookup"><span data-stu-id="762f6-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="762f6-145">OAuth est un protocole d’authentification qui permet aux utilisateurs tooapprove applications tooact en leur nom sans partage son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="762f6-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="762f6-146">Plus d’informations, consultez [oauth.net](http://oauth.net/) ou Bonjour excellent [tooOAuth du Guide du débutant](http://hueniverse.com/oauth/) à partir de Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="762f6-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="762f6-147">Hello première étape toouse OAuth est toocreate une nouvelle application sur site de développeur de Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="762f6-148">**toocreate une application Twitter**</span><span class="sxs-lookup"><span data-stu-id="762f6-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="762f6-149">Connectez-vous trop[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="762f6-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="762f6-150">Cliquez sur hello **s’inscrire maintenant** lien si vous n’avez pas un compte Twitter.</span><span class="sxs-lookup"><span data-stu-id="762f6-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="762f6-151">Cliquez sur **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="762f6-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="762f6-152">Renseignez les champs **Name**, **Description** et **Website**.</span><span class="sxs-lookup"><span data-stu-id="762f6-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="762f6-153">Vous pouvez apporter une URL pour hello **site Web** champ.</span><span class="sxs-lookup"><span data-stu-id="762f6-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="762f6-154">Hello tableau suivant illustre certaines toouse de valeurs d’exemple :</span><span class="sxs-lookup"><span data-stu-id="762f6-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="762f6-155">Champ</span><span class="sxs-lookup"><span data-stu-id="762f6-155">Field</span></span> | <span data-ttu-id="762f6-156">Valeur</span><span class="sxs-lookup"><span data-stu-id="762f6-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="762f6-157">Nom</span><span class="sxs-lookup"><span data-stu-id="762f6-157">Name</span></span> |<span data-ttu-id="762f6-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="762f6-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="762f6-159">Description</span><span class="sxs-lookup"><span data-stu-id="762f6-159">Description</span></span> |<span data-ttu-id="762f6-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="762f6-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="762f6-161">Website</span><span class="sxs-lookup"><span data-stu-id="762f6-161">Website</span></span> |<span data-ttu-id="762f6-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="762f6-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="762f6-163">Cochez la case **Yes, I agree**, puis cliquez **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="762f6-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="762f6-164">Cliquez sur hello **autorisations** d’autorisations par défaut onglet hello sont **en lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="762f6-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="762f6-165">Ces étapes sont suffisantes pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="762f6-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="762f6-166">Cliquez sur hello **clés et les jetons d’accès** onglet.</span><span class="sxs-lookup"><span data-stu-id="762f6-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="762f6-167">Cliquez sur **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="762f6-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="762f6-168">Cliquez sur **Test OAuth** dans hello haut à droite de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="762f6-169">Renseignez les valeurs **consumer key**, **Consumer secret**, **Access token** et **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="762f6-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="762f6-170">Vous avez besoin des valeurs de hello plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="762f6-171">Dans ce didacticiel, vous utiliserez un appel de service web de Windows PowerShell toomake hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="762f6-172">Pour obtenir un exemple .NET en C#, consultez la rubrique [Analyse des sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="762f6-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="762f6-173">Bonjour autres appels de service web toomake outil populaire est [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="762f6-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="762f6-174">Vous pouvez le télécharger [ici][curl-download].</span><span class="sxs-lookup"><span data-stu-id="762f6-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="762f6-175">Lorsque vous utilisez la commande de curl hello dans Windows, utilisez des guillemets doubles au lieu des guillemets simples pour les valeurs d’option hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="762f6-176">**tooget tweets**</span><span class="sxs-lookup"><span data-stu-id="762f6-176">**tooget tweets**</span></span>

1. <span data-ttu-id="762f6-177">Ouvrez hello Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="762f6-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="762f6-178">(Sur l’écran d’accueil de Windows 8 hello, tapez **PowerShell_ISE** puis cliquez sur **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="762f6-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="762f6-179">Consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="762f6-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="762f6-180">Copiez hello script suivant dans le volet de script hello :</span><span class="sxs-lookup"><span data-stu-id="762f6-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="762f6-181">Définir des variables de tooeight de cinq premières hello dans le script de hello :</span><span class="sxs-lookup"><span data-stu-id="762f6-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="762f6-182">Variable</span><span class="sxs-lookup"><span data-stu-id="762f6-182">Variable</span></span>|<span data-ttu-id="762f6-183">Description</span><span class="sxs-lookup"><span data-stu-id="762f6-183">Description</span></span>
    ---|---
    <span data-ttu-id="762f6-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="762f6-184">$clusterName</span></span>|<span data-ttu-id="762f6-185">Il s’agit de nom hello du cluster HDInsight de hello où vous souhaitez application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="762f6-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="762f6-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="762f6-186">$oauth_consumer_key</span></span>|<span data-ttu-id="762f6-187">Il s’agit d’application de Twitter hello **clé de consommateur** vous avez notées précédemment lorsque vous avez créé l’application de Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="762f6-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="762f6-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="762f6-189">Il s’agit d’application de Twitter hello **secret de consommateur** vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="762f6-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="762f6-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="762f6-190">$oauth_token</span></span>|<span data-ttu-id="762f6-191">Il s’agit d’application de Twitter hello **jeton d’accès** vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="762f6-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="762f6-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="762f6-192">$oauth_token_secret</span></span>|<span data-ttu-id="762f6-193">Il s’agit d’application de Twitter hello **secret du jeton d’accès** vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="762f6-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="762f6-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="762f6-194">$destBlobName</span></span>|<span data-ttu-id="762f6-195">Il s’agit de nom d’objet blob de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-195">This is hello output blob name.</span></span> <span data-ttu-id="762f6-196">la valeur par défaut Hello est **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="762f6-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="762f6-197">Si vous modifiez la valeur par défaut de hello, vous devez les scripts Windows PowerShell tooupdate hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="762f6-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="762f6-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="762f6-198">$trackString</span></span>|<span data-ttu-id="762f6-199">service web de Hello retournera les mots clés de tweets toothese connexes.</span><span class="sxs-lookup"><span data-stu-id="762f6-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="762f6-200">la valeur par défaut Hello est **HDInsight de Azure, le Cloud,**.</span><span class="sxs-lookup"><span data-stu-id="762f6-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="762f6-201">Si vous modifiez la valeur par défaut de hello, vous mettrez à jour les scripts Windows PowerShell hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="762f6-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="762f6-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="762f6-202">$lineMax</span></span>|<span data-ttu-id="762f6-203">valeur de Hello détermine combien script de hello tweet lira.</span><span class="sxs-lookup"><span data-stu-id="762f6-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="762f6-204">Il prend environ trois minutes tooread 100 Tweet.</span><span class="sxs-lookup"><span data-stu-id="762f6-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="762f6-205">Vous pouvez définir un plus grand nombre, mais prend plus toodownload de temps.</span><span class="sxs-lookup"><span data-stu-id="762f6-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="762f6-206">Appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="762f6-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="762f6-207">Si vous rencontrez des problèmes, comme une solution de contournement, sélectionnez toutes les lignes de hello, puis appuyez sur **F8**.</span><span class="sxs-lookup"><span data-stu-id="762f6-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="762f6-208">Le message « Complete!</span><span class="sxs-lookup"><span data-stu-id="762f6-208">You shall see "Complete!"</span></span> <span data-ttu-id="762f6-209">à la fin de hello de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-209">at hello end of hello output.</span></span> <span data-ttu-id="762f6-210">S’il y a un message d’erreur, il s’affiche en rouge.</span><span class="sxs-lookup"><span data-stu-id="762f6-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="762f6-211">En tant qu’une procédure de validation, vous pouvez vérifier le fichier de sortie hello, **/tutorials/twitter/data/tweets.txt**, sur votre stockage d’objets Blob Azure en utilisant un Explorateur de stockage Azure ou l’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="762f6-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="762f6-212">Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="762f6-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="762f6-213">Créer un script HiveQL</span><span class="sxs-lookup"><span data-stu-id="762f6-213">Create HiveQL script</span></span>
<span data-ttu-id="762f6-214">À l’aide d’Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL une à une heure ou package hello HiveQL instruction dans un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="762f6-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="762f6-215">Dans ce didacticiel, vous allez créer un script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="762f6-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="762f6-216">fichier de script Hello doit être téléchargé tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="762f6-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="762f6-217">Dans la section suivante de hello, vous allez exécuter le fichier de script hello à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="762f6-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="762f6-218">fichier de script Hive Hello et un fichier contenant les 10 000 tweet ont été téléchargés dans un conteneur d’objets Blob public.</span><span class="sxs-lookup"><span data-stu-id="762f6-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="762f6-219">Vous pouvez ignorer cette section si vous souhaitez que les fichiers toouse hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="762f6-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="762f6-220">Hello script HiveQL effectuera suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="762f6-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="762f6-221">**Supprimer la table de tweets_raw hello** au cas où la table hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="762f6-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="762f6-222">**Créer la table de Hive hello tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="762f6-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="762f6-223">Cette table structurée ruche temporaire conserve des données de hello pour extraire davantage, transformer et charger de traitement (ETL).</span><span class="sxs-lookup"><span data-stu-id="762f6-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="762f6-224">Pour plus d’informations sur les partitions, consultez la rubrique [Didacticiel Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="762f6-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="762f6-225">**Charger des données** à partir du dossier source hello, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="762f6-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="762f6-226">Hello tweet grand jeu de données au format JSON imbriquée a maintenant été transformé en une structure de table temporaire Hive.</span><span class="sxs-lookup"><span data-stu-id="762f6-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="762f6-227">**DROP hello tweet table** au cas où la table hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="762f6-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="762f6-228">**Créer hello tweet table**.</span><span class="sxs-lookup"><span data-stu-id="762f6-228">**Create hello tweets table**.</span></span> <span data-ttu-id="762f6-229">Vous pouvez interroger sur hello tweet jeu de données à l’aide de ruche, vous devez toorun un autre processus ETL.</span><span class="sxs-lookup"><span data-stu-id="762f6-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="762f6-230">Ce processus ETL définit un schéma de table plus détaillé pour les données hello que vous avez stocké dans la table « twitter_raw » de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="762f6-231">**Insertion de la table overwrite**.</span><span class="sxs-lookup"><span data-stu-id="762f6-231">**Insert overwrite table**.</span></span> <span data-ttu-id="762f6-232">Ce script Hive complex lancera hors tension d’un ensemble de longs travaux MapReduce par cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="762f6-233">Selon la taille de votre jeu de données et hello de votre cluster, ceci peut prendre environ 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="762f6-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="762f6-234">**Insertion du répertoire overwrite**.</span><span class="sxs-lookup"><span data-stu-id="762f6-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="762f6-235">Exécuter un fichier de requêtes et de sortie hello dataset tooa.</span><span class="sxs-lookup"><span data-stu-id="762f6-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="762f6-236">Cette requête retourne une liste d’utilisateurs Twitter qui a envoyé la plupart des tweets hello mot « Azure ».</span><span class="sxs-lookup"><span data-stu-id="762f6-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="762f6-237">**toocreate une ruche de script et le télécharger tooAzure**</span><span class="sxs-lookup"><span data-stu-id="762f6-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="762f6-238">Ouvrez Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="762f6-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="762f6-239">Copiez hello script suivant dans le volet de script hello :</span><span class="sxs-lookup"><span data-stu-id="762f6-239">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="762f6-240">Définissez tout d’abord deux variables de hello dans le script de hello :</span><span class="sxs-lookup"><span data-stu-id="762f6-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="762f6-241">Variable</span><span class="sxs-lookup"><span data-stu-id="762f6-241">Variable</span></span> | <span data-ttu-id="762f6-242">Description</span><span class="sxs-lookup"><span data-stu-id="762f6-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="762f6-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="762f6-243">$clusterName</span></span> |<span data-ttu-id="762f6-244">Entrez le nom du cluster HDInsight hello où application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="762f6-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="762f6-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="762f6-245">$subscriptionID</span></span> |<span data-ttu-id="762f6-246">Entrez l’identifiant de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="762f6-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="762f6-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="762f6-247">$sourceDataPath</span></span> |<span data-ttu-id="762f6-248">emplacement de stockage d’objets Blob Azure où les requêtes Hive hello lit hello de données à partir de Hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="762f6-249">Vous n’avez pas besoin toochange cette variable.</span><span class="sxs-lookup"><span data-stu-id="762f6-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="762f6-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="762f6-250">$outputPath</span></span> |<span data-ttu-id="762f6-251">emplacement de stockage d’objets Blob Azure où les requêtes Hive hello produira des résultats de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="762f6-252">Vous n’avez pas besoin toochange cette variable.</span><span class="sxs-lookup"><span data-stu-id="762f6-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="762f6-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="762f6-253">$hqlScriptFile</span></span> |<span data-ttu-id="762f6-254">emplacement de Hello et le nom de fichier de hello hello HiveQL du fichier de script.</span><span class="sxs-lookup"><span data-stu-id="762f6-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="762f6-255">Vous n’avez pas besoin toochange cette variable.</span><span class="sxs-lookup"><span data-stu-id="762f6-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="762f6-256">Appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="762f6-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="762f6-257">Si vous rencontrez des problèmes, comme une solution de contournement, sélectionnez toutes les lignes de hello, puis appuyez sur **F8**.</span><span class="sxs-lookup"><span data-stu-id="762f6-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="762f6-258">Le message « Complete!</span><span class="sxs-lookup"><span data-stu-id="762f6-258">You shall see "Complete!"</span></span> <span data-ttu-id="762f6-259">à la fin de hello de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-259">at hello end of hello output.</span></span> <span data-ttu-id="762f6-260">S’il y a un message d’erreur, il s’affiche en rouge.</span><span class="sxs-lookup"><span data-stu-id="762f6-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="762f6-261">En tant qu’une procédure de validation, vous pouvez vérifier le fichier de sortie hello, **/tutorials/twitter/twitter.hql**, sur votre stockage d’objets Blob Azure en utilisant un Explorateur de stockage Azure ou l’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="762f6-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="762f6-262">Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="762f6-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="762f6-263">Traitement des données Twitter à l’aide de Hive</span><span class="sxs-lookup"><span data-stu-id="762f6-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="762f6-264">Vous avez terminé tous les travaux de préparation hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="762f6-265">Maintenant, vous pouvez appeler hello ruche script et vérifier les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="762f6-266">Soumettre un travail Hive</span><span class="sxs-lookup"><span data-stu-id="762f6-266">Submit a Hive job</span></span>
<span data-ttu-id="762f6-267">Utilisez hello Windows PowerShell script toorun hello ruche du script suivant.</span><span class="sxs-lookup"><span data-stu-id="762f6-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="762f6-268">Vous devrez la première variable de tooset hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="762f6-269">toouse hello tweet et hello script HiveQL que vous avez téléchargé dans les deux dernières sections hello, jeu $hqlScriptFile too"/tutorials/twitter/twitter.hql ».</span><span class="sxs-lookup"><span data-stu-id="762f6-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="762f6-270">toouse hello ceux qui ont été téléchargés tooa des blob publics pour vous, définissez les $hqlScriptFile trop »wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql».</span><span class="sxs-lookup"><span data-stu-id="762f6-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="762f6-271">Vérifier les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="762f6-271">Check hello results</span></span>
<span data-ttu-id="762f6-272">Utilisez hello suivant hello toocheck de script Windows PowerShell sortie des tâches Hive.</span><span class="sxs-lookup"><span data-stu-id="762f6-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="762f6-273">Vous devez tout d’abord deux variables de tooset hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> table de Hive Hello utilise \001 hello séparateur de champs. <span data-ttu-id="762f6-275">délimiteur de Hello n’est pas visible dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="762f6-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="762f6-276">Une fois les résultats de l’analyse hello ont été placés dans le stockage d’objets Blob Azure, vous pouvez exporter hello données tooan SQL Azure de base de données/SQL server, exportez hello données tooExcel à l’aide de Power Query ou connecter vos données d’application toohello à l’aide de hello Hive le pilote ODBC.</span><span class="sxs-lookup"><span data-stu-id="762f6-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="762f6-277">Pour plus d’informations, consultez [Sqoop d’utilisation avec HDInsight][hdinsight-use-sqoop], [analyser des données de retard de vol avec HDInsight][hdinsight-analyze-flight-delay-data], [ Connecter Excel tooHDInsight avec Power Query][hdinsight-power-query], et [tooHDInsight Excel de se connecter avec Microsoft ODBC Driver de la ruche de hello][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="762f6-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="762f6-278">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="762f6-278">Next steps</span></span>
<span data-ttu-id="762f6-279">Dans ce didacticiel, nous avons vu comment tootransform un jeu de données JSON non structurée dans un tooquery table Hive structuré, Explorer et analyser les données de Twitter à l’aide de HDInsight sur Azure.</span><span class="sxs-lookup"><span data-stu-id="762f6-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="762f6-280">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="762f6-280">toolearn more, see:</span></span>

* <span data-ttu-id="762f6-281">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="762f6-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="762f6-282">[Analyse de sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="762f6-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="762f6-283">[Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="762f6-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="762f6-284">[Connecter Excel tooHDInsight avec Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="762f6-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="762f6-285">[Rejoignez Excel tooHDInsight hello Microsoft ODBC Driver de la ruche][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="762f6-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="762f6-286">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="762f6-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
