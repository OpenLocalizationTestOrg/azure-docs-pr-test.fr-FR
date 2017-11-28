---
title: "tooand de données aaaCopy de WASB dans Data Lake Store à l’aide de Distcp | Documents Microsoft"
description: "Utilisez Distcp outil toocopy données tooand à partir d’objets BLOB de stockage Azure tooData Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="2c2f6-103">Utiliser des données de toocopy Distcp entre les objets BLOB de stockage Azure et Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2c2f6-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c2f6-104">Utilisation de DistCp</span><span class="sxs-lookup"><span data-stu-id="2c2f6-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="2c2f6-105">Utilisation d’AdlCopy</span><span class="sxs-lookup"><span data-stu-id="2c2f6-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="2c2f6-106">Une fois que vous avez créé un cluster HDInsight accès tooa un compte Data Lake Store, vous pouvez utiliser les outils d’écosystème de Hadoop comme des données de toocopy Distcp **tooand de** un stockage de cluster HDInsight (WASB) dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="2c2f6-107">Cet article fournit des instructions sur la façon de tooachieve cela.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c2f6-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2c2f6-108">Prerequisites</span></span>
<span data-ttu-id="2c2f6-109">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="2c2f6-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="2c2f6-110">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-110">**An Azure subscription**.</span></span> <span data-ttu-id="2c2f6-111">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c2f6-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2c2f6-112">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2c2f6-113">Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2c2f6-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="2c2f6-114">**Cluster HDInsight Azure** avec accès tooa compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="2c2f6-115">Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c2f6-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="2c2f6-116">Assurez-vous que vous activez Bureau à distance de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="2c2f6-117">Les vidéos vous permettent-elles d’apprendre rapidement ?</span><span class="sxs-lookup"><span data-stu-id="2c2f6-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="2c2f6-118">[Regardez cette vidéo](https://mix.office.com/watch/1liuojvdx6sie) sur la façon de toocopy des données entre les objets BLOB de stockage Azure et à l’aide de DistCp Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="2c2f6-119">Utiliser Distcp à partir d’un cluster HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="2c2f6-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="2c2f6-120">Un cluster HDInsight est fourni avec l’utilitaire de Distcp hello, qui peut être utilisés toocopy des données à partir de sources différentes dans un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="2c2f6-121">Si vous avez configuré le cluster HDInsight de hello toouse Data Lake Store en tant qu’un stockage supplémentaire, hello Distcp utilitaire peut être utilisé out of box toocopy des tooand de données à partir d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="2c2f6-122">Dans cette section, nous examiner comment toouse hello Distcp utilitaire.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="2c2f6-123">À partir de votre bureau, utilisez SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="2c2f6-124">Consultez [Connect tooa HDInsight de basés sur Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2c2f6-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="2c2f6-125">Exécuter des commandes hello à partir de l’invite de commandes hello SSH.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="2c2f6-126">Vérifiez si vous avez accès hello objets BLOB de stockage Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="2c2f6-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="2c2f6-127">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2c2f6-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="2c2f6-128">Il doit fournir une liste du contenu dans l’objet blob de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="2c2f6-129">De même, vérifiez si vous pouvez accéder à hello compte Data Lake Store à partir du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="2c2f6-130">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2c2f6-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="2c2f6-131">Il doit fournir une liste de fichiers/dossiers Bonjour compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="2c2f6-132">Utilisez des données toocopy Distcp WASB tooa compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="2c2f6-133">Cette copie contenu hello Hello **/exemple données/gutenberg/** dossier dans WASB trop**/myfolder** Bonjour compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="2c2f6-134">De même, utilisez des données toocopy Distcp tooWASB du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="2c2f6-135">Cette copie contenu hello du **/myfolder** Bonjour Data Lake Store compte trop**/exempledonnées/gutenberg/** dossier dans WASB.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="2c2f6-136">Considérations de performances lors de l’utilisation de DistCp</span><span class="sxs-lookup"><span data-stu-id="2c2f6-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="2c2f6-137">DistCp's la plus faible granularité est un fichier unique, définition hello maximal du nombre de copies simultanées est hello plus importantes paramètre toooptimize sur Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="2c2f6-138">Cela est contrôlé en définissant le nombre de hello de mappeurs (am ») le paramètre de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="2c2f6-139">Ce paramètre spécifie le nombre maximal de hello de mappeurs qui sera utilisé toocopy données.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="2c2f6-140">La valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-140">Default value is 20.</span></span>

<span data-ttu-id="2c2f6-141">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="2c2f6-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="2c2f6-142">Comment déterminer le nombre de hello de mappeurs toouse ?</span><span class="sxs-lookup"><span data-stu-id="2c2f6-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="2c2f6-143">Voici quelques conseils à suivre.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="2c2f6-144">**Étape 1 : Déterminer la quantité totale de mémoire fils** -hello première étape consiste cluster toodetermine hello fils mémoire toohello disponible sur lequel vous exécutez la tâche de DistCp hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="2c2f6-145">Ces informations sont disponibles dans le portail de Ambari hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="2c2f6-146">Accédez tooYARN et afficher hello configurations onglet toosee hello fils de mémoire.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="2c2f6-147">tooget hello fils mémoire totale, multiplication hello mémoire fils par nœud en nombre hello de nœuds dont vous disposez dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="2c2f6-148">**Étape 2 : Calculer le nombre de hello de mappeurs** -hello valeur **m** est le quotient de toohello égal totale de mémoire fils divisée par la taille du conteneur fils de hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="2c2f6-149">Hello, les informations de taille de conteneur fils est disponible dans le portail de Ambari hello ainsi.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="2c2f6-150">Accédez tooYARN et vue Bonjour configurations onglet Bonjour taille du conteneur fils est affiché dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="2c2f6-151">Hello tooarrive équation au nombre de hello de mappeurs (**m**) est</span><span class="sxs-lookup"><span data-stu-id="2c2f6-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="2c2f6-152">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="2c2f6-152">**Example**</span></span>

<span data-ttu-id="2c2f6-153">Supposons que vous avez un 4 nœuds D14v2s dans un cluster de hello et que vous essayez de tootransfer 10 To de données à partir de 10 différents dossiers.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="2c2f6-154">Chacun des dossiers de hello contiennent différentes quantités de données et tailles de fichier hello dans chaque dossier sont différents.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="2c2f6-155">Mémoire totale de fils - de hello portail Ambari vous déterminez que hello mémoire des fils est 96 Go pour un nœud D14.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="2c2f6-156">Ainsi, la mémoire YARN totale pour un cluster à 4 nœuds est :</span><span class="sxs-lookup"><span data-stu-id="2c2f6-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="2c2f6-157">Nombre de mappeurs - de hello portail Ambari vous déterminez que taille de conteneur fils hello est 3072 pour un nœud de cluster D14.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="2c2f6-158">Par conséquent, le nombre de mappeurs est :</span><span class="sxs-lookup"><span data-stu-id="2c2f6-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="2c2f6-159">Si d’autres applications utilisent la mémoire, puis vous pouvez choisir tooonly utiliser une partie de la mémoire des fils de votre cluster pour DistCp.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="2c2f6-160">Copie de jeux de données volumineux</span><span class="sxs-lookup"><span data-stu-id="2c2f6-160">Copying large datasets</span></span>

<span data-ttu-id="2c2f6-161">Lorsque la taille de hello de hello dataset toobe déplacées sont très volumineux (par exemple, > 1 To) ou si vous avez de nombreux dossiers, vous devez envisager d’utiliser plusieurs travaux DistCp.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="2c2f6-162">Il n’existe probablement aucun gain de performance, mais il distribuent les tâches de hello afin que si un travail échoue, il vous suffit toorestart cette tâche spécifique plutôt que de projet hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="2c2f6-163">Limites</span><span class="sxs-lookup"><span data-stu-id="2c2f6-163">Limitations</span></span>

* <span data-ttu-id="2c2f6-164">DistCp essaie mappeurs toocreate qui ont des performances de toooptimize de taille.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="2c2f6-165">Augmenter le nombre hello de mappeurs pas toujours augmente les performances.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="2c2f6-166">DistCp est limité tooonly l’une mappeur par fichier.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="2c2f6-167">Par conséquent, vous ne devez pas avoir plus de mappeurs que de fichiers.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="2c2f6-168">Étant donné que DistCp affecter uniquement un mappeur tooa fichier, cela limite hello d’accès concurrentiel qui peut être utilisés toocopy des fichiers volumineux.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="2c2f6-169">Si vous avez un petit nombre de fichiers volumineux, vous devez fractionner les dans toogive de segments de fichier de 256 Mo vous plus de concurrence potentielle.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="2c2f6-170">Si vous copiez à partir d’un compte de stockage d’objets Blob Azure, votre travail de copie peut être limité sur le côté de stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="2c2f6-171">Cela sera dégrader les performances de hello de votre travail de copie.</span><span class="sxs-lookup"><span data-stu-id="2c2f6-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="2c2f6-172">toolearn savoir plus sur les limites de hello de stockage d’objets Blob Azure, consultez les limites de stockage Azure à [abonnement Azure et limites de service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2c2f6-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c2f6-173">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2c2f6-173">See also</span></span>
* [<span data-ttu-id="2c2f6-174">Copier des données d’objets BLOB de stockage Azure tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="2c2f6-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="2c2f6-175">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2c2f6-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2c2f6-176">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2c2f6-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2c2f6-177">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2c2f6-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
