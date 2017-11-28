---
title: "Analyse des données Twitter avec Hadoop dans HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser Hive pour analyser des données Twitter sur Hadoop dans HDInsight afin de déterminer la fréquence d'utilisation d'un mot particulier."
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
ms.openlocfilehash: 711d364c36c3aba699326f4a76d42891ba3219fb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="ad595-103">Analyse des données Twitter avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad595-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="ad595-104">Les sites web sociaux constituent l’un des principaux motifs de l’utilisation du modèle « Big Data ».</span><span class="sxs-lookup"><span data-stu-id="ad595-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="ad595-105">Les API publiques fournies par des sites comme Twitter représentent une source de données utile pour l'analyse et la compréhension des tendances populaires.</span><span class="sxs-lookup"><span data-stu-id="ad595-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="ad595-106">Dans ce didacticiel, vous allez recevoir des tweets à l’aide de l’API de diffusion Twitter, puis utiliser Apache Hive sur Azure HDInsight pour récupérer une liste des utilisateurs de Twitter ayant envoyé le plus de tweets contenant un mot donné.</span><span class="sxs-lookup"><span data-stu-id="ad595-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad595-107">Les étapes décrites dans ce document nécessitent un cluster HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="ad595-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="ad595-108">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="ad595-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ad595-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ad595-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="ad595-110">Pour les étapes spécifiques à un cluster basé sur Linux, consultez la rubrique [Analyse des données Twitter avec Hive dans HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ad595-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad595-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ad595-111">Prerequisites</span></span>
<span data-ttu-id="ad595-112">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ad595-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ad595-113">**poste de travail** sur lequel Azure PowerShell est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="ad595-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="ad595-114">Pour exécuter des scripts Windows PowerShell, vous devez exécuter Azure PowerShell en tant qu’administrateur et définir la stratégie d’exécution sur *RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="ad595-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="ad595-115">Consultez la page [Exécution de scripts Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="ad595-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="ad595-116">Avant d’exécuter vos scripts Windows PowerShell, assurez-vous que vous êtes connecté à votre abonnement Azure à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad595-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="ad595-117">Si vous possédez plusieurs abonnements Azure, utilisez l’applet de commande suivante pour définir l'abonnement en cours :</span><span class="sxs-lookup"><span data-stu-id="ad595-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ad595-118">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="ad595-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="ad595-119">Dans ce document, la procédure repose sur les nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ad595-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="ad595-120">Suivez les étapes indiquées dans [Installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs) pour installer la dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad595-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="ad595-121">Si vous devez modifier certains scripts pour utiliser les nouvelles applets de commande fonctionnant avec Azure Resource Manager, consultez [Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ad595-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="ad595-122">Un **cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ad595-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="ad595-123">Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="ad595-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="ad595-124">Vous en aurez besoin plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ad595-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="ad595-125">Le tableau suivant répertorie les fichiers utilisés dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="ad595-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="ad595-126">Fichiers</span><span class="sxs-lookup"><span data-stu-id="ad595-126">Files</span></span> | <span data-ttu-id="ad595-127">Description</span><span class="sxs-lookup"><span data-stu-id="ad595-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad595-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="ad595-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="ad595-129">Données source pour la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="ad595-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="ad595-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="ad595-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="ad595-131">Données de sortie pour la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="ad595-131">The output folder for the Hive job.</span></span> <span data-ttu-id="ad595-132">Par défaut, le nom du fichier de sortie de la tâche Hive est **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="ad595-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="ad595-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="ad595-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="ad595-134">Fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ad595-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="ad595-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="ad595-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="ad595-136">État de la tâche Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ad595-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="ad595-137">Obtention du flux Twitter</span><span class="sxs-lookup"><span data-stu-id="ad595-137">Get Twitter feed</span></span>
<span data-ttu-id="ad595-138">Dans ce didacticiel, vous allez utiliser les [API de diffusion Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="ad595-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="ad595-139">L’API de diffusion Twitter spécifique que vous allez utiliser est [statuses/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="ad595-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="ad595-140">Un fichier contenant 10 000 tweets et le fichier de script Hive (traité dans la section suivante) ont été téléchargés dans un conteneur d'objets blob public.</span><span class="sxs-lookup"><span data-stu-id="ad595-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="ad595-141">Vous pouvez ignorer cette section si vous souhaitez utiliser les fichiers téléchargés.</span><span class="sxs-lookup"><span data-stu-id="ad595-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="ad595-142">[données des tweets](https://dev.twitter.com/docs/platform-objects/tweets) sont stockées au format JSON (JavaScript Object Notation) qui contient une structure imbriquée complexe.</span><span class="sxs-lookup"><span data-stu-id="ad595-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="ad595-143">Au lieu d’écrire de nombreuses lignes de code à l’aide d’un langage de programmation classique, vous pouvez transformer cette structure imbriquée en une table Hive, de sorte qu’un langage de type SQL, appelé HiveQL, puisse effectuer une requête sur celle-ci.</span><span class="sxs-lookup"><span data-stu-id="ad595-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="ad595-144">Twitter utilise OAuth pour fournir un accès autorisé à son API.</span><span class="sxs-lookup"><span data-stu-id="ad595-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="ad595-145">OAuth est un protocole d’authentification qui permet aux utilisateurs d’autoriser des applications à agir à leur place sans partager leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ad595-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="ad595-146">Pour plus d'informations, consultez la page [oauth.net](http://oauth.net/) ou l'excellent [Guide du débutant sur OAuth](http://hueniverse.com/oauth/) de Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="ad595-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="ad595-147">Pour utiliser OAuth, la première étape consiste à créer une nouvelle application sur le site du développeur Twitter.</span><span class="sxs-lookup"><span data-stu-id="ad595-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="ad595-148">**Pour créer une application Twitter**</span><span class="sxs-lookup"><span data-stu-id="ad595-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="ad595-149">Connectez-vous à [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="ad595-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="ad595-150">Cliquez sur le lien **Sign up now** si vous ne possédez pas de compte Twitter.</span><span class="sxs-lookup"><span data-stu-id="ad595-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="ad595-151">Cliquez sur **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="ad595-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="ad595-152">Renseignez les champs **Name**, **Description** et **Website**.</span><span class="sxs-lookup"><span data-stu-id="ad595-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="ad595-153">Vous pouvez créer une URL pour le champ **Website** .</span><span class="sxs-lookup"><span data-stu-id="ad595-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="ad595-154">Le tableau suivant affiche quelques exemples de valeurs à utiliser :</span><span class="sxs-lookup"><span data-stu-id="ad595-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="ad595-155">Champ</span><span class="sxs-lookup"><span data-stu-id="ad595-155">Field</span></span> | <span data-ttu-id="ad595-156">Valeur</span><span class="sxs-lookup"><span data-stu-id="ad595-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="ad595-157">Nom</span><span class="sxs-lookup"><span data-stu-id="ad595-157">Name</span></span> |<span data-ttu-id="ad595-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="ad595-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="ad595-159">Description</span><span class="sxs-lookup"><span data-stu-id="ad595-159">Description</span></span> |<span data-ttu-id="ad595-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="ad595-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="ad595-161">Website</span><span class="sxs-lookup"><span data-stu-id="ad595-161">Website</span></span> |<span data-ttu-id="ad595-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="ad595-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="ad595-163">Cochez la case **Yes, I agree**, puis cliquez **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="ad595-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="ad595-164">Cliquez sur l'onglet **Permissions** .</span><span class="sxs-lookup"><span data-stu-id="ad595-164">Click the **Permissions** tab.</span></span> <span data-ttu-id="ad595-165">L'autorisation par défaut est **Read only**.</span><span class="sxs-lookup"><span data-stu-id="ad595-165">The default permission is **Read only**.</span></span> <span data-ttu-id="ad595-166">Ces étapes sont suffisantes pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ad595-166">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="ad595-167">Cliquez sur l’onglet **Keys and Access Tokens** .</span><span class="sxs-lookup"><span data-stu-id="ad595-167">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="ad595-168">Cliquez sur **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="ad595-168">Click **Create my access token**.</span></span>
8. <span data-ttu-id="ad595-169">Cliquez sur **Test OAuth** dans le coin supérieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="ad595-169">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="ad595-170">Renseignez les valeurs **consumer key**, **Consumer secret**, **Access token** et **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="ad595-170">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="ad595-171">Vous en aurez besoin plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ad595-171">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="ad595-172">Dans ce didacticiel, vous allez utiliser Windows PowerShell pour effectuer un appel de service web.</span><span class="sxs-lookup"><span data-stu-id="ad595-172">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="ad595-173">Pour obtenir un exemple .NET en C#, consultez la rubrique [Analyse des sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="ad595-173">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="ad595-174">L’autre outil connu permettant d’effectuer des appels de service Web est [*Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="ad595-174">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="ad595-175">Vous pouvez le télécharger [ici][curl-download].</span><span class="sxs-lookup"><span data-stu-id="ad595-175">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="ad595-176">Lorsque vous utilisez la commande Curl sous Windows, remplacez les guillemets simples par des guillemets doubles pour exprimer la valeur des options.</span><span class="sxs-lookup"><span data-stu-id="ad595-176">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="ad595-177">**Pour récupérer des tweets**</span><span class="sxs-lookup"><span data-stu-id="ad595-177">**To get tweets**</span></span>

1. <span data-ttu-id="ad595-178">Ouvrez l’environnement d’écriture de scripts intégré de Windows PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="ad595-178">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="ad595-179">(Sur l’écran de démarrage de Windows 8, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="ad595-179">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="ad595-180">Consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="ad595-180">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="ad595-181">Copiez le script suivant dans le volet du script :</span><span class="sxs-lookup"><span data-stu-id="ad595-181">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="ad595-182">Définissez les cinq premières variables du script :</span><span class="sxs-lookup"><span data-stu-id="ad595-182">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="ad595-183">Variable</span><span class="sxs-lookup"><span data-stu-id="ad595-183">Variable</span></span>|<span data-ttu-id="ad595-184">Description</span><span class="sxs-lookup"><span data-stu-id="ad595-184">Description</span></span>
    ---|---
    <span data-ttu-id="ad595-185">$clusterName</span><span class="sxs-lookup"><span data-stu-id="ad595-185">$clusterName</span></span>|<span data-ttu-id="ad595-186">Nom du cluster HDInsight où vous souhaitez exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="ad595-186">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="ad595-187">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="ad595-187">$oauth_consumer_key</span></span>|<span data-ttu-id="ad595-188">**Clé** que vous avez notée auparavant en créant l’application Twitter.</span><span class="sxs-lookup"><span data-stu-id="ad595-188">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="ad595-189">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="ad595-189">$oauth_consumer_secret</span></span>|<span data-ttu-id="ad595-190">**Secret** que vous avez écrit auparavant pour l'application Twitter.</span><span class="sxs-lookup"><span data-stu-id="ad595-190">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="ad595-191">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="ad595-191">$oauth_token</span></span>|<span data-ttu-id="ad595-192">**Jeton d'accès** que vous avez écrit auparavant pour l'application Twitter.</span><span class="sxs-lookup"><span data-stu-id="ad595-192">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="ad595-193">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="ad595-193">$oauth_token_secret</span></span>|<span data-ttu-id="ad595-194">**Secret de jeton d'accès** que vous avez écrit auparavant pour l'application Twitter.</span><span class="sxs-lookup"><span data-stu-id="ad595-194">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="ad595-195">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="ad595-195">$destBlobName</span></span>|<span data-ttu-id="ad595-196">Nom de l'objet blob de sortie.</span><span class="sxs-lookup"><span data-stu-id="ad595-196">This is the output blob name.</span></span> <span data-ttu-id="ad595-197">La valeur par défaut est **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="ad595-197">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="ad595-198">Si vous modifiez la valeur par défaut, vous devez mettre à jour les scripts Windows PowerShell en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ad595-198">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="ad595-199">$trackString</span><span class="sxs-lookup"><span data-stu-id="ad595-199">$trackString</span></span>|<span data-ttu-id="ad595-200">Le service Web renvoie les tweets liés à ces mots clés.</span><span class="sxs-lookup"><span data-stu-id="ad595-200">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="ad595-201">La valeur par défaut est **Azure, Cloud, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ad595-201">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="ad595-202">Si vous modifiez la valeur par défaut, vous devez mettre à jour les scripts Windows PowerShell en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ad595-202">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="ad595-203">$lineMax</span><span class="sxs-lookup"><span data-stu-id="ad595-203">$lineMax</span></span>|<span data-ttu-id="ad595-204">La valeur détermine le nombre de tweets lus par le script.</span><span class="sxs-lookup"><span data-stu-id="ad595-204">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="ad595-205">La lecture de 100 tweets prend environ trois minutes.</span><span class="sxs-lookup"><span data-stu-id="ad595-205">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="ad595-206">Vous pouvez définir un nombre plus important, mais le téléchargement prendra plus de temps.</span><span class="sxs-lookup"><span data-stu-id="ad595-206">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="ad595-207">Appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="ad595-207">Press **F5** to run the script.</span></span> <span data-ttu-id="ad595-208">Si vous êtes confronté à des problèmes, vous pouvez, pour les contourner, sélectionner toutes les lignes et appuyer ensuite sur **F8**.</span><span class="sxs-lookup"><span data-stu-id="ad595-208">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="ad595-209">Le message « Complete!</span><span class="sxs-lookup"><span data-stu-id="ad595-209">You shall see "Complete!"</span></span> <span data-ttu-id="ad595-210">» doit normalement s'afficher à la fin de la sortie.</span><span class="sxs-lookup"><span data-stu-id="ad595-210">at the end of the output.</span></span> <span data-ttu-id="ad595-211">S’il y a un message d’erreur, il s’affiche en rouge.</span><span class="sxs-lookup"><span data-stu-id="ad595-211">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="ad595-212">Dans le cadre d’une procédure de validation, vous pouvez vérifier le fichier de sortie, **/tutorials/twitter/data/tweets.txt**, sur votre stockage d’objets blob Azure à l’aide d’un explorateur de stockage Azure ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad595-212">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="ad595-213">Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="ad595-213">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="ad595-214">Créer un script HiveQL</span><span class="sxs-lookup"><span data-stu-id="ad595-214">Create HiveQL script</span></span>
<span data-ttu-id="ad595-215">À l'aide d'Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL, une par une, ou empaqueter l'instruction HiveQL dans un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="ad595-215">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="ad595-216">Dans ce didacticiel, vous allez créer un script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ad595-216">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="ad595-217">Le fichier de script doit être téléchargé dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ad595-217">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="ad595-218">Dans la section suivante, vous allez exécuter le fichier de script à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad595-218">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ad595-219">Le fichier de script Hive et un fichier contenant 10 000 tweets ont été téléchargés dans un conteneur d'objets Blob public.</span><span class="sxs-lookup"><span data-stu-id="ad595-219">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="ad595-220">Vous pouvez ignorer cette section si vous souhaitez utiliser les fichiers téléchargés.</span><span class="sxs-lookup"><span data-stu-id="ad595-220">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="ad595-221">Le script HiveQL exécutera les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ad595-221">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="ad595-222">**Suppression de la table tweets_raw** au cas où la table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="ad595-222">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="ad595-223">**Création de la table tweets_raw Hive**.</span><span class="sxs-lookup"><span data-stu-id="ad595-223">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="ad595-224">Cette table Hive structurée et temporaire conserve les données en vue d’un traitement ETL ultérieur (extraction, modification et chargement).</span><span class="sxs-lookup"><span data-stu-id="ad595-224">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="ad595-225">Pour plus d’informations sur les partitions, consultez la rubrique [Didacticiel Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ad595-225">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="ad595-226">**Chargement des données** à partir du dossier source, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="ad595-226">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="ad595-227">Le volumineux jeu de données des tweets imbriqué dans le format JSON a été transformé en une structure de table Hive temporaire.</span><span class="sxs-lookup"><span data-stu-id="ad595-227">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="ad595-228">**Suppression de la table tweets** , le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="ad595-228">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="ad595-229">**Création de la table tweets**.</span><span class="sxs-lookup"><span data-stu-id="ad595-229">**Create the tweets table**.</span></span> <span data-ttu-id="ad595-230">Avant de pouvoir effectuer une requête sur le jeu de données des tweets à l’aide de Hive, vous devez exécuter un autre processus ETL.</span><span class="sxs-lookup"><span data-stu-id="ad595-230">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="ad595-231">Ce dernier définit un schéma de table plus détaillé pour les données que vous avez stockées dans la table « twitter_raw ».</span><span class="sxs-lookup"><span data-stu-id="ad595-231">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="ad595-232">**Insertion de la table overwrite**.</span><span class="sxs-lookup"><span data-stu-id="ad595-232">**Insert overwrite table**.</span></span> <span data-ttu-id="ad595-233">Ce script Hive complexe démarre un ensemble de longues tâches MapReduce sur le cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ad595-233">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="ad595-234">Selon votre ensemble de données et la taille de votre cluster, cela peut prendre environ 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="ad595-234">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="ad595-235">**Insertion du répertoire overwrite**.</span><span class="sxs-lookup"><span data-stu-id="ad595-235">**Insert overwrite directory**.</span></span> <span data-ttu-id="ad595-236">Exécutez une requête et sortez le jeu de données dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="ad595-236">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="ad595-237">Cette requête renvoie une liste d’utilisateurs de Twitter dont la majorité des tweets envoyés contenaient le mot « Azure ».</span><span class="sxs-lookup"><span data-stu-id="ad595-237">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="ad595-238">**Pour créer un script Hive et le télécharger sur Azure**</span><span class="sxs-lookup"><span data-stu-id="ad595-238">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="ad595-239">Ouvrez Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="ad595-239">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="ad595-240">Copiez le script suivant dans le volet du script :</span><span class="sxs-lookup"><span data-stu-id="ad595-240">Copy the following script into the script pane:</span></span>

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="ad595-241">Définissez les deux premières variables du script :</span><span class="sxs-lookup"><span data-stu-id="ad595-241">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="ad595-242">Variable</span><span class="sxs-lookup"><span data-stu-id="ad595-242">Variable</span></span> | <span data-ttu-id="ad595-243">Description</span><span class="sxs-lookup"><span data-stu-id="ad595-243">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="ad595-244">$clusterName</span><span class="sxs-lookup"><span data-stu-id="ad595-244">$clusterName</span></span> |<span data-ttu-id="ad595-245">Entrez le nom du cluster HDInsight où vous souhaitez exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="ad595-245">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="ad595-246">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="ad595-246">$subscriptionID</span></span> |<span data-ttu-id="ad595-247">Entrez l’identifiant de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ad595-247">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="ad595-248">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="ad595-248">$sourceDataPath</span></span> |<span data-ttu-id="ad595-249">Emplacement de stockage d’objets blob Azure où les requêtes Hive lisent les données.</span><span class="sxs-lookup"><span data-stu-id="ad595-249">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="ad595-250">Vous n'avez pas besoin de modifier cette variable.</span><span class="sxs-lookup"><span data-stu-id="ad595-250">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="ad595-251">$outputPath</span><span class="sxs-lookup"><span data-stu-id="ad595-251">$outputPath</span></span> |<span data-ttu-id="ad595-252">Emplacement de stockage d’objets blob Azure où les requêtes Hive envoient les résultats.</span><span class="sxs-lookup"><span data-stu-id="ad595-252">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="ad595-253">Vous n'avez pas besoin de modifier cette variable.</span><span class="sxs-lookup"><span data-stu-id="ad595-253">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="ad595-254">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="ad595-254">$hqlScriptFile</span></span> |<span data-ttu-id="ad595-255">Emplacement et nom du fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ad595-255">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="ad595-256">Vous n'avez pas besoin de modifier cette variable.</span><span class="sxs-lookup"><span data-stu-id="ad595-256">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="ad595-257">Appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="ad595-257">Press **F5** to run the script.</span></span> <span data-ttu-id="ad595-258">Si vous êtes confronté à des problèmes, vous pouvez, pour les contourner, sélectionner toutes les lignes et appuyer ensuite sur **F8**.</span><span class="sxs-lookup"><span data-stu-id="ad595-258">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="ad595-259">Le message « Complete!</span><span class="sxs-lookup"><span data-stu-id="ad595-259">You shall see "Complete!"</span></span> <span data-ttu-id="ad595-260">» doit normalement s'afficher à la fin de la sortie.</span><span class="sxs-lookup"><span data-stu-id="ad595-260">at the end of the output.</span></span> <span data-ttu-id="ad595-261">S’il y a un message d’erreur, il s’affiche en rouge.</span><span class="sxs-lookup"><span data-stu-id="ad595-261">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="ad595-262">Dans le cadre d’une procédure de validation, vous pouvez vérifier le fichier de sortie, **/tutorials/twitter/twitter.hql**, sur votre stockage d’objets blob Azure à l’aide d’un explorateur de stockage Azure ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad595-262">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="ad595-263">Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="ad595-263">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="ad595-264">Traitement des données Twitter à l’aide de Hive</span><span class="sxs-lookup"><span data-stu-id="ad595-264">Process Twitter data by using Hive</span></span>
<span data-ttu-id="ad595-265">Vous avez terminé tout le travail de préparation.</span><span class="sxs-lookup"><span data-stu-id="ad595-265">You have finished all the preparation work.</span></span> <span data-ttu-id="ad595-266">Vous pouvez à présent appeler le script Hive et vérifier les résultats.</span><span class="sxs-lookup"><span data-stu-id="ad595-266">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="ad595-267">Soumettre un travail Hive</span><span class="sxs-lookup"><span data-stu-id="ad595-267">Submit a Hive job</span></span>
<span data-ttu-id="ad595-268">Utilisez le script Windows PowerShell suivant pour exécuter le script Hive.</span><span class="sxs-lookup"><span data-stu-id="ad595-268">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="ad595-269">Vous devez définir la première variable.</span><span class="sxs-lookup"><span data-stu-id="ad595-269">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="ad595-270">Pour utiliser les tweets et le script HiveQL que vous avez téléchargé dans les deux dernières sections, définissez la valeur $hqlScriptFile sur "/ tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="ad595-270">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="ad595-271">Pour utiliser ceux qui ont été chargés sur un objet blob public pour vous, définissez $hqlScriptFile sur « wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql ».</span><span class="sxs-lookup"><span data-stu-id="ad595-271">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
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

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="ad595-272">Vérification des résultats</span><span class="sxs-lookup"><span data-stu-id="ad595-272">Check the results</span></span>
<span data-ttu-id="ad595-273">Exécutez le script Windows PowerShell suivant pour vérifier la sortie de la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="ad595-273">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="ad595-274">Vous devez définir les deux premières variables.</span><span class="sxs-lookup"><span data-stu-id="ad595-274">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
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
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> La table Hive utilise \001 comme délimiteur de champ. <span data-ttu-id="ad595-276">Le délimiteur n'est pas visible dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="ad595-276">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="ad595-277">Une fois que les résultats d’analyse ont été placés dans le stockage d’objets blob Azure, vous pouvez exporter les données dans la base de données Azure SQL/le serveur SQL, exporter les données dans Excel à l’aide de Power Query ou connecter votre application aux données à l’aide du pilote ODBC Hive.</span><span class="sxs-lookup"><span data-stu-id="ad595-277">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="ad595-278">Pour plus d’informations, consultez les rubriques [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop], [Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-delay-data], [Connexion d’Excel à HDInsight à l’aide de Power Query][hdinsight-power-query] et [Connexion d’Excel à HDInsight à l’aide du pilote ODBC Microsoft Hive][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="ad595-278">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad595-279">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad595-279">Next steps</span></span>
<span data-ttu-id="ad595-280">Dans ce didacticiel, nous avons vu comment transformer le jeu de données JSON non structuré en une table Hive structurée pour effectuer une requête sur les données, les explorer et les analyser à partir de Twitter à l’aide de HDInsight sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ad595-280">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="ad595-281">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="ad595-281">To learn more, see:</span></span>

* <span data-ttu-id="ad595-282">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ad595-282">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="ad595-283">[Analyse de sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="ad595-283">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="ad595-284">[Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="ad595-284">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="ad595-285">[Connexion d’Excel à HDInsight à l’aide de Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="ad595-285">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="ad595-286">[Connexion d’Excel à HDInsight à l’aide du pilote ODBC Microsoft Hive][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="ad595-286">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="ad595-287">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="ad595-287">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
