---
title: aaaUse Hadoop Hive avec PowerShell dans HDInsight - Azure | Documents Microsoft
description: "Utiliser des requêtes Hive PowerShell toorun dans Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>Exécution de requêtes Hive avec PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Ce document fournit un exemple d’utilisation d’Azure PowerShell dans hello groupe de ressources Azure mode toorun requêtes Hive dans un Hadoop sur le cluster HDInsight.

> [!NOTE]
> Ce document ne fournit pas une description détaillée de ce que font les instructions HiveQL hello qui sont utilisées dans les exemples hello. Pour plus d’informations sur hello HiveQL qui est utilisé dans cet exemple, consultez [utilisez Hive avec Hadoop dans HDInsight](hdinsight-use-hive.md).

**Configuration requise**

* **Un cluster Azure HDInsight**: il n’a pas d’importance si le cluster de hello est Windows ou Linux.

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Un poste de travail sur lequel est installé Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Exécution de requêtes Hive avec Azure PowerShell

Azure PowerShell fournit *applets de commande* qui permettent de tooremotely exécuter des requêtes Hive dans HDInsight. En interne, les applets de commande hello appeler reste trop[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) sur le cluster HDInsight de hello.

applets de commande suivantes Hello sont utilisées lors de l’exécution des requêtes Hive dans un cluster HDInsight à distance :

* **AzureRmAccount ajouter**: authentifie Azure PowerShell tooyour abonnement Azure
* **Nouveau-AzureRmHDInsightHiveJobDefinition**: crée un *définition de travail* à l’aide de hello spécifié les instructions HiveQL
* **Start-AzureRmHDInsightJob**: envoie tooHDInsight de définition de tâche hello, démarre le travail de hello et retourne un *travail* objet qui peut être l’état de hello toocheck utilisés du travail de hello
* **Wait-AzureRmHDInsightJob**: utilise hello objet toocheck hello statut de tâche de travail de hello. Il attend hello tâche se termine ou dépasse du délai d’attente hello.
* **Get-AzureRmHDInsightJobOutput**: utilisé la sortie de hello tooretrieve du travail de hello
* **Invoke-AzureRmHDInsightHiveJob**: utiliser les instructions HiveQL toorun. Cette requête de hello blocs applet de commande se termine, puis retourne les résultats de hello
* **Utilisez-AzureRmHDInsightCluster**: jeux hello toouse de cluster actuel pour hello **Invoke-AzureRmHDInsightHiveJob** commande

Hello étapes suivantes montrent comment toouse ces applets de commande de toorun un travail dans votre cluster HDInsight :

1. À l’aide d’un éditeur, enregistrer hello suivant le code en tant que **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Ouvrez une invite de commandes **Azure PowerShell** . Modifier l’emplacement de toohello répertoires de hello **hivejob.ps1** de fichier, puis utilisez hello commande toorun hello script suivant :

        .\hivejob.ps1

    Lors de l’exécution du script de hello, vous sont demandées tooenter hello cluster nom et hello HTTPS/Admin informations d’identification pour le cluster de hello. Vous pouvez également être invité à toolog dans tooyour abonnement Azure.

3. Lors de la tâche de hello est terminée, elle retourne toohello similaire à informations suivant le texte ne :

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Comme mentionné précédemment, **Invoke-Hive** peut être utilisé toorun une requête et attendre la réponse de hello. Utilisez hello suivant toosee script fonctionne Invoke-Hive :

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    sortie de Hello ressemble à hello suivant du texte :

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Pour les requêtes HiveQL plus, vous pouvez utiliser hello Azure PowerShell **les chaînes Here** applet de commande ou HiveQL des fichiers de script. Hello suivant extrait de code montre comment toouse hello **Invoke-Hive** toorun de l’applet de commande un fichier de script HiveQL. Hello HiveQL fichier de script doit être téléchargé toowasb : / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Pour plus d'informations sur **Here-Strings**, consultez la page <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Utilisation du fichier de script Here-Strings de PowerShell</a>.

## <a name="troubleshooting"></a>Résolution des problèmes

Si aucune information n’est retournée lorsque hello travail se termine, une erreur peut être survenu lors du traitement. informations sur l’erreur tooview à cette tâche, ajouter hello suivant fin toohello Hello **hivejob.ps1** de fichiers, enregistrez-le et exécutez-le à nouveau.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Cette applet de commande retourne des informations de hello écrit tooSTDERR sur le serveur de hello lors de l’exécution du travail de hello.

## <a name="summary"></a>Résumé

Comme vous pouvez le voir, Azure PowerShell fournit un moyen simple de toorun requêtes Hive dans un cluster HDInsight, hello d’analyse état du travail et d’extraire la sortie de hello.

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des informations générales sur Hive dans HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)
