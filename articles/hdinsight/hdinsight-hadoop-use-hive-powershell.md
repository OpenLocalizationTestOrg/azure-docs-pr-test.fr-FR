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
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="ceaac-103">Exécution de requêtes Hive avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceaac-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ceaac-104">Ce document fournit un exemple d’utilisation d’Azure PowerShell dans hello groupe de ressources Azure mode toorun requêtes Hive dans un Hadoop sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ceaac-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ceaac-105">Ce document ne fournit pas une description détaillée de ce que font les instructions HiveQL hello qui sont utilisées dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="ceaac-106">Pour plus d’informations sur hello HiveQL qui est utilisé dans cet exemple, consultez [utilisez Hive avec Hadoop dans HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="ceaac-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="ceaac-107">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="ceaac-107">**Prerequisites**</span></span>

* <span data-ttu-id="ceaac-108">**Un cluster Azure HDInsight**: il n’a pas d’importance si le cluster de hello est Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="ceaac-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ceaac-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="ceaac-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ceaac-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ceaac-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ceaac-111">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ceaac-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="ceaac-112">Exécution de requêtes Hive avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceaac-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="ceaac-113">Azure PowerShell fournit *applets de commande* qui permettent de tooremotely exécuter des requêtes Hive dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ceaac-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="ceaac-114">En interne, les applets de commande hello appeler reste trop[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="ceaac-115">applets de commande suivantes Hello sont utilisées lors de l’exécution des requêtes Hive dans un cluster HDInsight à distance :</span><span class="sxs-lookup"><span data-stu-id="ceaac-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="ceaac-116">**AzureRmAccount ajouter**: authentifie Azure PowerShell tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="ceaac-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="ceaac-117">**Nouveau-AzureRmHDInsightHiveJobDefinition**: crée un *définition de travail* à l’aide de hello spécifié les instructions HiveQL</span><span class="sxs-lookup"><span data-stu-id="ceaac-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="ceaac-118">**Start-AzureRmHDInsightJob**: envoie tooHDInsight de définition de tâche hello, démarre le travail de hello et retourne un *travail* objet qui peut être l’état de hello toocheck utilisés du travail de hello</span><span class="sxs-lookup"><span data-stu-id="ceaac-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="ceaac-119">**Wait-AzureRmHDInsightJob**: utilise hello objet toocheck hello statut de tâche de travail de hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="ceaac-120">Il attend hello tâche se termine ou dépasse du délai d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="ceaac-121">**Get-AzureRmHDInsightJobOutput**: utilisé la sortie de hello tooretrieve du travail de hello</span><span class="sxs-lookup"><span data-stu-id="ceaac-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="ceaac-122">**Invoke-AzureRmHDInsightHiveJob**: utiliser les instructions HiveQL toorun.</span><span class="sxs-lookup"><span data-stu-id="ceaac-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="ceaac-123">Cette requête de hello blocs applet de commande se termine, puis retourne les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="ceaac-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="ceaac-124">**Utilisez-AzureRmHDInsightCluster**: jeux hello toouse de cluster actuel pour hello **Invoke-AzureRmHDInsightHiveJob** commande</span><span class="sxs-lookup"><span data-stu-id="ceaac-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="ceaac-125">Hello étapes suivantes montrent comment toouse ces applets de commande de toorun un travail dans votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="ceaac-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="ceaac-126">À l’aide d’un éditeur, enregistrer hello suivant le code en tant que **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ceaac-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="ceaac-127">Ouvrez une invite de commandes **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="ceaac-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="ceaac-128">Modifier l’emplacement de toohello répertoires de hello **hivejob.ps1** de fichier, puis utilisez hello commande toorun hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="ceaac-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="ceaac-129">Lors de l’exécution du script de hello, vous sont demandées tooenter hello cluster nom et hello HTTPS/Admin informations d’identification pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="ceaac-130">Vous pouvez également être invité à toolog dans tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ceaac-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="ceaac-131">Lors de la tâche de hello est terminée, elle retourne toohello similaire à informations suivant le texte ne :</span><span class="sxs-lookup"><span data-stu-id="ceaac-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="ceaac-132">Comme mentionné précédemment, **Invoke-Hive** peut être utilisé toorun une requête et attendre la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="ceaac-133">Utilisez hello suivant toosee script fonctionne Invoke-Hive :</span><span class="sxs-lookup"><span data-stu-id="ceaac-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="ceaac-134">sortie de Hello ressemble à hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="ceaac-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="ceaac-135">Pour les requêtes HiveQL plus, vous pouvez utiliser hello Azure PowerShell **les chaînes Here** applet de commande ou HiveQL des fichiers de script.</span><span class="sxs-lookup"><span data-stu-id="ceaac-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="ceaac-136">Hello suivant extrait de code montre comment toouse hello **Invoke-Hive** toorun de l’applet de commande un fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ceaac-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="ceaac-137">Hello HiveQL fichier de script doit être téléchargé toowasb : / /.</span><span class="sxs-lookup"><span data-stu-id="ceaac-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="ceaac-138">Pour plus d'informations sur **Here-Strings**, consultez la page <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Utilisation du fichier de script Here-Strings de PowerShell</a>.</span><span class="sxs-lookup"><span data-stu-id="ceaac-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ceaac-139">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ceaac-139">Troubleshooting</span></span>

<span data-ttu-id="ceaac-140">Si aucune information n’est retournée lorsque hello travail se termine, une erreur peut être survenu lors du traitement.</span><span class="sxs-lookup"><span data-stu-id="ceaac-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="ceaac-141">informations sur l’erreur tooview à cette tâche, ajouter hello suivant fin toohello Hello **hivejob.ps1** de fichiers, enregistrez-le et exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="ceaac-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="ceaac-142">Cette applet de commande retourne des informations de hello écrit tooSTDERR sur le serveur de hello lors de l’exécution du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="ceaac-143">Résumé</span><span class="sxs-lookup"><span data-stu-id="ceaac-143">Summary</span></span>

<span data-ttu-id="ceaac-144">Comme vous pouvez le voir, Azure PowerShell fournit un moyen simple de toorun requêtes Hive dans un cluster HDInsight, hello d’analyse état du travail et d’extraire la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="ceaac-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ceaac-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ceaac-145">Next steps</span></span>

<span data-ttu-id="ceaac-146">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="ceaac-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="ceaac-147">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceaac-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ceaac-148">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="ceaac-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ceaac-149">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceaac-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ceaac-150">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceaac-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
