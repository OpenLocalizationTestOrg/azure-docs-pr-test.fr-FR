---
title: aaaUse Hadoop Pig avec PowerShell dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooa de travaux toosubmit Pig Hadoop cluster sur HDInsight à l’aide d’Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Utiliser des travaux de Azure PowerShell toorun Pig hdinsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Ce document fournit un exemple d’utilisation d’Azure PowerShell toosubmit Pig travaux tooa Hadoop sur le cluster HDInsight. Pig vous permet des tâches MapReduce toowrite à l’aide d’un langage (Pig Latin) qui modélise les transformations de données, plutôt que mapper et réduire des fonctions.

> [!NOTE]
> Ce document ne fournit pas une description détaillée de ce que font les instructions de Pig Latin hello utilisées dans les exemples hello. Pour plus d’informations sur hello Latin Pig utilisé dans cet exemple, consultez [utilisez Pig avec Hadoop dans HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Configuration requise

* **Un cluster Azure HDInsight**

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Un poste de travail sur lequel est installé Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Exécution de tâches Pig avec PowerShell

Azure PowerShell fournit *applets de commande* qui permettent de travaux de tooremotely exécution Pig dans HDInsight. En interne, PowerShell utilise des appels REST trop[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) en cours d’exécution sur le cluster HDInsight de hello.

applets de commande suivantes Hello sont utilisées lors de l’exécution des travaux de Pig sur un cluster HDInsight à distance :

* **Connexion-AzureRmAccount**: authentifie Azure PowerShell tooyour abonnement Azure
* **Nouveau-AzureRmHDInsightPigJobDefinition**: crée un *définition de travail* à l’aide de hello spécifié Pig Latin instructions
* **Start-AzureRmHDInsightJob**: envoie tooHDInsight de définition de tâche hello, démarre le travail de hello et retourne un *travail* objet qui peut être l’état de hello toocheck utilisés du travail de hello
* **Wait-AzureRmHDInsightJob**: utilise hello objet toocheck hello statut de tâche de travail de hello. Il attend hello est terminée, ou délai d’attente hello a été dépassé.
* **Get-AzureRmHDInsightJobOutput**: utilisé la sortie de hello tooretrieve du travail de hello

Hello étapes suivantes montrent comment toouse ces applets de commande de toorun une tâche sur votre cluster HDInsight.

1. À l’aide d’un éditeur, enregistrer hello suivant le code en tant que **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Ouvrez une invite de commandes Windows PowerShell. Modifier l’emplacement de toohello répertoires de hello **pigjob.ps1** de fichier, puis utilisez hello commande toorun hello script suivant :

        .\pigjob.ps1

    Vous êtes invité à toolog dans tooyour abonnement Azure. Ensuite, vous êtes invité à entrer nom du compte hello HTTPs/Admin et le mot de passe pour le cluster HDInsight de hello.

2. Lors de la tâche de hello est terminée, elle doit retourner toohello similaire à informations suivant le texte :

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Résolution des problèmes

Si aucune information n’est retournée lorsque hello travail se termine, une erreur peut être survenu lors du traitement. informations sur l’erreur tooview à cette tâche, ajouter hello suivant la fin de la commande toohello Hello **pigjob.ps1** de fichiers, enregistrez-le et exécutez-le à nouveau.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Cela retourne les informations de hello écrite tooSTDERR sur le serveur de hello lors de l’exécution du travail de hello et il peut aider à déterminer la raison pour laquelle le travail de hello échoue.

## <a id="summary"></a>Résumé
Comme vous pouvez le voir, Azure PowerShell fournit un moyen simple de toorun les travaux Pig sur un cluster HDInsight, surveiller le statut de tâche hello et récupérer hello sortie.

## <a id="nextsteps"></a>Étapes suivantes
Pour obtenir des informations générales sur Pig dans HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)
