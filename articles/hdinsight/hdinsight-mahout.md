---
title: "recommandations aaaGenerate à l’aide de Mahout HDInsight à partir de PowerShell - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Apache Mahout d’apprentissage recommandations de films bibliothèque toogenerate avec HDInsight (Hadoop) à partir d’un script PowerShell en cours d’exécution sur votre client."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="a0523-103">Génération de recommandations de films à l’aide d’Apache Mahout avec Hadoop dans HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a0523-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="a0523-104">Découvrez comment toouse hello [Apache Mahout](http://mahout.apache.org) bibliothèque d’apprentissage machine avec les recommandations de films toogenerate Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0523-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="a0523-105">exemple Hello dans ce document utilise Azure PowerShell toorun Mahout travaux.</span><span class="sxs-lookup"><span data-stu-id="a0523-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0523-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a0523-106">Prerequisites</span></span>

* <span data-ttu-id="a0523-107">Un cluster HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="a0523-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a0523-108">Pour plus d’informations sur la création de ce dernier, consultez [Prise en main de Hadoop sous Linux dans HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="a0523-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0523-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="a0523-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a0523-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a0523-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="a0523-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0523-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="a0523-112"><a name="recommendations"></a>Génération de recommandations avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0523-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="a0523-113">la tâche Hello dans cette section fonctionne à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0523-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="a0523-114">Nombre de classes hello fournis avec Mahout ne fonctionnent pas actuellement avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0523-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="a0523-115">Pour obtenir la liste des classes qui ne fonctionnent pas avec Azure PowerShell, consultez hello [dépannage](#troubleshooting) section.</span><span class="sxs-lookup"><span data-stu-id="a0523-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="a0523-116">Pour obtenir un exemple d’utilisation de SSH tooconnect tooHDInsight et exécution Mahout exemples directement sur le cluster de hello, consultez [générer des recommandations de films à l’aide de Mahout et HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="a0523-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="a0523-117">Une des fonctions hello fournie par Mahout est un moteur de recommandation.</span><span class="sxs-lookup"><span data-stu-id="a0523-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="a0523-118">Ce moteur accepte les données au format hello de `userID`, `itemId`, et `prefValue` (hello préférence aux utilisateurs pour l’élément de hello).</span><span class="sxs-lookup"><span data-stu-id="a0523-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="a0523-119">Mahout utilise hello données toodetermine utilisateurs avec les préférences de l’élément de type, qui peuvent être utilisé toomake recommandations.</span><span class="sxs-lookup"><span data-stu-id="a0523-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="a0523-120">Hello exemple suivant est une procédure simplifiée de fonctionnement du processus de recommandation hello :</span><span class="sxs-lookup"><span data-stu-id="a0523-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="a0523-121">**occurrence coadministrateurs**: Joe, Alice et Bob connexes tous les *étoile se*, *hello avertissements Empire précédent*, et *retour Hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="a0523-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="a0523-122">Mahout détermine que les utilisateurs, comme l’un de ces films également comme hello deux autres.</span><span class="sxs-lookup"><span data-stu-id="a0523-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="a0523-123">**occurrence coadministrateurs**: Bob et Alice également aimé *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="a0523-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="a0523-124">Mahout détermine que les utilisateurs qui aimé également des films de trois précédente hello, tels que ces vidéos.</span><span class="sxs-lookup"><span data-stu-id="a0523-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="a0523-125">**Recommandation de similarité**: Joe car aimé hello les trois premiers films, Mahout examine les films que d’autres personnes avec des préférences similaires plaît, mais Joe n’a pas observé (aimé/nominale).</span><span class="sxs-lookup"><span data-stu-id="a0523-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="a0523-126">Dans ce cas, vous recommande de Mahout *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="a0523-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="a0523-127">Présentation des données de salutation</span><span class="sxs-lookup"><span data-stu-id="a0523-127">Understanding hello data</span></span>

<span data-ttu-id="a0523-128">[GroupLens Research][movielens] fournit des données d’évaluation de films dans un format compatible avec Mahout.</span><span class="sxs-lookup"><span data-stu-id="a0523-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="a0523-129">Ces données sont disponibles sur le stockage par défaut hello pour votre cluster à `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="a0523-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="a0523-130">Il existe deux fichiers, `moviedb.txt` (informations sur les films hello) et `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="a0523-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="a0523-131">Hello `user-ratings.txt` fichier est utilisé lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="a0523-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="a0523-132">Hello `moviedb.txt` fichier est texte convivial de tooprovide utilisé lors de l’affichage des résultats d’analyse de hello hello.</span><span class="sxs-lookup"><span data-stu-id="a0523-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="a0523-133">les données d’utilisateur-ratings.txt Hello possède une structure de `userID`, `movieID`, `userRating`, et `timestamp`, qui indique comment recommandé de chaque utilisateur avec un film.</span><span class="sxs-lookup"><span data-stu-id="a0523-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="a0523-134">Voici un exemple de données de hello :</span><span class="sxs-lookup"><span data-stu-id="a0523-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="a0523-135">Exécuter la tâche de hello</span><span class="sxs-lookup"><span data-stu-id="a0523-135">Run hello job</span></span>

<span data-ttu-id="a0523-136">Utilisez hello suivant toorun de script Windows PowerShell une tâche qui utilise le moteur de recommandations hello Mahout avec des données de film hello :</span><span class="sxs-lookup"><span data-stu-id="a0523-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="a0523-137">Ce fichier vous demande les informations qui sont le cluster HDInsight de tooyour tooconnect utilisés et les tâches d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a0523-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="a0523-138">Il peut prendre plusieurs minutes pour hello travaux toocomplete et téléchargez le fichier de output.txt hello.</span><span class="sxs-lookup"><span data-stu-id="a0523-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="a0523-139">Mahout travaux ne supprimez pas les données temporaires qui sont créées lors du traitement du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="a0523-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="a0523-140">Hello `--tempDir` est précisé dans hello exemple travail tooisolate hello des fichiers temporaires dans un répertoire spécifique.</span><span class="sxs-lookup"><span data-stu-id="a0523-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="a0523-141">travail de Mahout Hello ne retourne pas de hello sortie tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="a0523-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="a0523-142">Au lieu de cela, elle est stockée dans le répertoire de sortie spécifié hello en tant que **partie-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="a0523-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="a0523-143">script de Hello télécharge ce fichier trop**output.txt** dans le répertoire en cours de hello sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="a0523-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="a0523-144">Hello texte suivant est un exemple de contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="a0523-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="a0523-145">première colonne de Hello est hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="a0523-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="a0523-146">Hello les valeurs contenues dans ' [' et ']' sont `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="a0523-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="a0523-147">script de Hello télécharge également hello `moviedb.txt` et `user-ratings.txt` fichiers, qui sont nécessaires tooformat hello sortie toobe plus lisible.</span><span class="sxs-lookup"><span data-stu-id="a0523-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="a0523-148">Vue hello sortie</span><span class="sxs-lookup"><span data-stu-id="a0523-148">View hello output</span></span>

<span data-ttu-id="a0523-149">Hello généré la sortie peut être OK pour une utilisation dans une application, il n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="a0523-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="a0523-150">Hello `moviedb.txt` hello server peut être utilisé tooresolve hello `movieId` tooa nom du film.</span><span class="sxs-lookup"><span data-stu-id="a0523-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="a0523-151">Utilisez hello suivant les recommandations de toodisplay de script PowerShell avec des noms de film :</span><span class="sxs-lookup"><span data-stu-id="a0523-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="a0523-152">Utilisez hello commande toodisplay hello recommandations dans un format convivial :</span><span class="sxs-lookup"><span data-stu-id="a0523-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="a0523-153">Hello est similaire toohello suivant texte de sortie :</span><span class="sxs-lookup"><span data-stu-id="a0523-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="a0523-154"><a name="troubleshooting"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a0523-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="a0523-155">Remplacement de fichiers impossible</span><span class="sxs-lookup"><span data-stu-id="a0523-155">Cannot overwrite files</span></span>

<span data-ttu-id="a0523-156">Les tâches Mahout ne suppriment pas les fichiers temporaires créés lors du traitement.</span><span class="sxs-lookup"><span data-stu-id="a0523-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="a0523-157">En outre, les travaux hello ne pas remplacement le fichier de sortie existant.</span><span class="sxs-lookup"><span data-stu-id="a0523-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="a0523-158">tooavoid erreurs lors de l’exécution des travaux de Mahout, supprimer des fichiers temporaires et de sortie entre les exécutions.</span><span class="sxs-lookup"><span data-stu-id="a0523-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="a0523-159">les fichiers de hello tooremove créés par hello scripts plus haut dans ce document, utilisez hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="a0523-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="a0523-160"><a name="nopowershell"></a>Classes ne fonctionnant pas avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0523-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="a0523-161">Mahout les travaux qui utilisent hello classes suivantes retournent différents messages d’erreur lorsqu’il est utilisé à partir de Windows PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a0523-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="a0523-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="a0523-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="a0523-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="a0523-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="a0523-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="a0523-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="a0523-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="a0523-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="a0523-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="a0523-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="a0523-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="a0523-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="a0523-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="a0523-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="a0523-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="a0523-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="a0523-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="a0523-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="a0523-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="a0523-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="a0523-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="a0523-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="a0523-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="a0523-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="a0523-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="a0523-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="a0523-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="a0523-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="a0523-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="a0523-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="a0523-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="a0523-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="a0523-178">toorun les travaux qui utilisent ces classes, connectez le cluster HDInsight de toohello à l’aide de SSH et exécuter des travaux de hello à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="a0523-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="a0523-179">Pour obtenir un exemple d’utilisation de SSH toorun Mahout travaux, consultez [générer des recommandations de films à l’aide de Mahout et HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="a0523-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0523-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0523-180">Next steps</span></span>

<span data-ttu-id="a0523-181">Maintenant que vous avez appris comment toouse Mahout, connaître les autres méthodes de travail avec des données sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="a0523-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="a0523-182">Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="a0523-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a0523-183">Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="a0523-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a0523-184">MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="a0523-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
