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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Génération de recommandations de films à l’aide d’Apache Mahout avec Hadoop dans HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Découvrez comment toouse hello [Apache Mahout](http://mahout.apache.org) bibliothèque d’apprentissage machine avec les recommandations de films toogenerate Azure HDInsight. exemple Hello dans ce document utilise Azure PowerShell toorun Mahout travaux.

## <a name="prerequisites"></a>Composants requis

* Un cluster HDInsight sous Linux Pour plus d’informations sur la création de ce dernier, consultez [Prise en main de Hadoop sous Linux dans HDInsight][getstarted].

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Génération de recommandations avec Azure PowerShell

> [!WARNING]
> la tâche Hello dans cette section fonctionne à l’aide d’Azure PowerShell. Nombre de classes hello fournis avec Mahout ne fonctionnent pas actuellement avec Azure PowerShell. Pour obtenir la liste des classes qui ne fonctionnent pas avec Azure PowerShell, consultez hello [dépannage](#troubleshooting) section.
>
> Pour obtenir un exemple d’utilisation de SSH tooconnect tooHDInsight et exécution Mahout exemples directement sur le cluster de hello, consultez [générer des recommandations de films à l’aide de Mahout et HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Une des fonctions hello fournie par Mahout est un moteur de recommandation. Ce moteur accepte les données au format hello de `userID`, `itemId`, et `prefValue` (hello préférence aux utilisateurs pour l’élément de hello). Mahout utilise hello données toodetermine utilisateurs avec les préférences de l’élément de type, qui peuvent être utilisé toomake recommandations.

Hello exemple suivant est une procédure simplifiée de fonctionnement du processus de recommandation hello :

* **occurrence coadministrateurs**: Joe, Alice et Bob connexes tous les *étoile se*, *hello avertissements Empire précédent*, et *retour Hello Jedi*. Mahout détermine que les utilisateurs, comme l’un de ces films également comme hello deux autres.

* **occurrence coadministrateurs**: Bob et Alice également aimé *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*. Mahout détermine que les utilisateurs qui aimé également des films de trois précédente hello, tels que ces vidéos.

* **Recommandation de similarité**: Joe car aimé hello les trois premiers films, Mahout examine les films que d’autres personnes avec des préférences similaires plaît, mais Joe n’a pas observé (aimé/nominale). Dans ce cas, vous recommande de Mahout *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*.

### <a name="understanding-hello-data"></a>Présentation des données de salutation

[GroupLens Research][movielens] fournit des données d’évaluation de films dans un format compatible avec Mahout. Ces données sont disponibles sur le stockage par défaut hello pour votre cluster à `/HdiSamples//HdiSamples/MahoutMovieData`.

Il existe deux fichiers, `moviedb.txt` (informations sur les films hello) et `user-ratings.txt`. Hello `user-ratings.txt` fichier est utilisé lors de l’analyse. Hello `moviedb.txt` fichier est texte convivial de tooprovide utilisé lors de l’affichage des résultats d’analyse de hello hello.

les données d’utilisateur-ratings.txt Hello possède une structure de `userID`, `movieID`, `userRating`, et `timestamp`, qui indique comment recommandé de chaque utilisateur avec un film. Voici un exemple de données de hello :

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Exécuter la tâche de hello

Utilisez hello suivant toorun de script Windows PowerShell une tâche qui utilise le moteur de recommandations hello Mahout avec des données de film hello :

> [!NOTE]
> Ce fichier vous demande les informations qui sont le cluster HDInsight de tooyour tooconnect utilisés et les tâches d’exécution. Il peut prendre plusieurs minutes pour hello travaux toocomplete et téléchargez le fichier de output.txt hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Mahout travaux ne supprimez pas les données temporaires qui sont créées lors du traitement du travail de hello. Hello `--tempDir` est précisé dans hello exemple travail tooisolate hello des fichiers temporaires dans un répertoire spécifique.

travail de Mahout Hello ne retourne pas de hello sortie tooSTDOUT. Au lieu de cela, elle est stockée dans le répertoire de sortie spécifié hello en tant que **partie-r-00000**. script de Hello télécharge ce fichier trop**output.txt** dans le répertoire en cours de hello sur votre station de travail.

Hello texte suivant est un exemple de contenu hello de ce fichier :

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

première colonne de Hello est hello `userID`. Hello les valeurs contenues dans ' [' et ']' sont `movieId`:`recommendationScore`.

script de Hello télécharge également hello `moviedb.txt` et `user-ratings.txt` fichiers, qui sont nécessaires tooformat hello sortie toobe plus lisible.

### <a name="view-hello-output"></a>Vue hello sortie

Hello généré la sortie peut être OK pour une utilisation dans une application, il n’est pas convivial. Hello `moviedb.txt` hello server peut être utilisé tooresolve hello `movieId` tooa nom du film. Utilisez hello suivant les recommandations de toodisplay de script PowerShell avec des noms de film :

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Utilisez hello commande toodisplay hello recommandations dans un format convivial : 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Hello est similaire toohello suivant texte de sortie :

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

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="cannot-overwrite-files"></a>Remplacement de fichiers impossible

Les tâches Mahout ne suppriment pas les fichiers temporaires créés lors du traitement. En outre, les travaux hello ne pas remplacement le fichier de sortie existant.

tooavoid erreurs lors de l’exécution des travaux de Mahout, supprimer des fichiers temporaires et de sortie entre les exécutions. les fichiers de hello tooremove créés par hello scripts plus haut dans ce document, utilisez hello PowerShell script suivant :

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

### <a name="nopowershell"></a>Classes ne fonctionnant pas avec Azure PowerShell

Mahout les travaux qui utilisent hello classes suivantes retournent différents messages d’erreur lorsqu’il est utilisé à partir de Windows PowerShell :

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

toorun les travaux qui utilisent ces classes, connectez le cluster HDInsight de toohello à l’aide de SSH et exécuter des travaux de hello à partir de la ligne de commande hello. Pour obtenir un exemple d’utilisation de SSH toorun Mahout travaux, consultez [générer des recommandations de films à l’aide de Mahout et HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse Mahout, connaître les autres méthodes de travail avec des données sur HDInsight :

* [Hive avec HDInsight](hdinsight-use-hive.md)
* [Pig avec HDInsight](hdinsight-use-pig.md)
* [MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

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
