---
title: aaaUse MapReduce et PowerShell avec Hadoop - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse PowerShell tooremotely exécuter les tâches MapReduce avec Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>Exécution à distance des travaux MapReduce avec Hadoop sur HDInsight à l’aide de PowerShell

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Ce document fournit un exemple d’utilisation d’Azure PowerShell toorun une tâche MapReduce dans un Hadoop sur le cluster HDInsight.

## <a id="prereq"></a>Configuration requise

* **Un cluster Azure HDInsight (Hadoop sur HDInsight)**

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Un poste de travail sur lequel est installé Azure PowerShell**.

## <a id="powershell"></a>Exécution d’une tâche MapReduce avec Azure PowerShell

Azure PowerShell fournit *applets de commande* qui permettent de tooremotely exécuter les tâches MapReduce dans HDInsight. En interne, cela est accompli en utilisant des appels REST trop[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anciennement Templeton) en cours d’exécution hello cluster HDInsight.

applets de commande suivantes Hello sont utilisées lors de l’exécution des tâches MapReduce dans un cluster HDInsight à distance.

* **Connexion-AzureRmAccount**: authentifie Azure PowerShell tooyour abonnement Azure.

* **Nouveau-AzureRmHDInsightMapReduceJobDefinition**: crée un nouveau *définition de travail* à l’aide de hello spécifié les informations MapReduce.

* **Start-AzureRmHDInsightJob**: envoie tooHDInsight de définition de tâche hello, démarre le travail de hello et retourne un *travail* objet qui peut être l’état de hello toocheck utilisés du travail de hello.

* **Wait-AzureRmHDInsightJob**: utilise hello objet toocheck hello statut de tâche de travail de hello. Il attend hello tâche se termine ou dépasse du délai d’attente hello.

* **Get-AzureRmHDInsightJobOutput**: utilisé la sortie de hello tooretrieve du travail de hello.

Hello étapes suivantes montrent comment toouse ces applets de commande de toorun un travail dans votre cluster HDInsight.

1. À l’aide d’un éditeur, enregistrer hello suivant le code en tant que **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Ouvrez une invite de commandes **Azure PowerShell** . Modifier l’emplacement de toohello répertoires de hello **mapreducejob.ps1** de fichier, puis utilisez hello commande toorun hello script suivant :

        .\mapreducejob.ps1

    Lorsque vous exécutez le script de hello, vous êtes invité pour nom hello du cluster HDInsight de hello et nom du compte hello HTTPS/Admin et mot de passe pour le cluster de hello. Vous pouvez également être invité à tooauthenticate tooyour abonnement Azure.

3. Lors de la tâche de hello est terminée, vous recevez toohello similaire de sortie suivant du texte :

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Cette sortie indique que le travail hello s’est terminée avec succès.

    > [!NOTE]
    > Si hello **ExitCode** est une valeur différente de 0, consultez [dépannage](#troubleshooting).

    Cet exemple stocke également hello téléchargé les fichiers tooan **output.txt** fichier hello dans répertoire dans lequel vous exécutez le script hello.

### <a name="view-output"></a>Affichage de la sortie

Ouvrez hello **output.txt** fichier dans un Bonjour de toosee de l’éditeur de texte les mots et le nombre obtenu par la tâche de hello.

> [!NOTE]
> Hello des fichiers de sortie d’une tâche MapReduce sont immuables. Si vous exécutez à nouveau cet exemple, vous devez donc nom de hello toochange hello du fichier de sortie.

## <a id="troubleshooting"></a>Résolution des problèmes

Si aucune information n’est retournée lorsque hello travail se termine, une erreur peut être survenu lors du traitement. informations sur l’erreur tooview à cette tâche, ajouter hello suivant la fin de la commande toohello Hello **mapreducejob.ps1** de fichiers, enregistrez-le et exécutez-le à nouveau.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Cette applet de commande retourne des informations de hello écrite tooSTDERR sur le serveur de hello lors de l’exécution du travail de hello et il peut aider à déterminer la raison pour laquelle le travail de hello échoue.

## <a id="summary"></a>Résumé

Comme vous pouvez le voir, Azure PowerShell fournit un moyen simple de toorun tâches MapReduce sur un cluster HDInsight, surveiller le statut de tâche hello et récupérer hello sortie.

## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :

* [Utilisation de MapReduce dans Hadoop HDInsight](hdinsight-use-mapreduce.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
