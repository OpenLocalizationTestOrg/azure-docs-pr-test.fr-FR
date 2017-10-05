---
title: "Copier des données vers et depuis WASB dans Data Lake Store à l’aide de Distcp| Microsoft Docs"
description: "Utilisez l’outil Distcp pour copier des données entre des objets blob Azure Storage et Data Lake Store"
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="525fe-103">Utilisation de l’utilitaire Distcp pour copier des données entre des objets blob Azure Storage et le Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="525fe-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="525fe-104">Utilisation de DistCp</span><span class="sxs-lookup"><span data-stu-id="525fe-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="525fe-105">Utilisation d’AdlCopy</span><span class="sxs-lookup"><span data-stu-id="525fe-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="525fe-106">Une fois que vous avez créé un cluster HDInsight ayant accès à un compte Data Lake Store, vous pouvez utiliser des outils de l’écosystème Hadoop, comme Distcp, pour copier des données **vers et depuis** un stockage de cluster HDInsight (WASB) dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="525fe-107">Cet article fournit des instructions sur la procédure à suivre.</span><span class="sxs-lookup"><span data-stu-id="525fe-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="525fe-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="525fe-108">Prerequisites</span></span>
<span data-ttu-id="525fe-109">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="525fe-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="525fe-110">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="525fe-110">**An Azure subscription**.</span></span> <span data-ttu-id="525fe-111">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="525fe-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="525fe-112">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="525fe-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="525fe-113">Pour savoir comment en créer un, consultez [Prise en main d'Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="525fe-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="525fe-114">**Cluster Azure HDInsight** ayant accès à un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="525fe-115">Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="525fe-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="525fe-116">Veillez à activer le Bureau à distance pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="525fe-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="525fe-117">Les vidéos vous permettent-elles d’apprendre rapidement ?</span><span class="sxs-lookup"><span data-stu-id="525fe-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="525fe-118">[Regardez cette vidéo](https://mix.office.com/watch/1liuojvdx6sie) pour savoir comment copier des données entre des objets blob Azure Storage et Data Lake Store à l’aide de DistCp.</span><span class="sxs-lookup"><span data-stu-id="525fe-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="525fe-119">Utiliser Distcp à partir d’un cluster HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="525fe-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="525fe-120">Un cluster HDInsight est fourni avec l’utilitaire Distcp, que vous pouvez utiliser pour copier dans un cluster des données provenant de différentes sources.</span><span class="sxs-lookup"><span data-stu-id="525fe-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="525fe-121">Si vous avez configuré le cluster HDInsight pour utiliser Data Lake Store comme espace de stockage supplémentaire, l’utilitaire Distcp peut également être utilisé tel quel pour copier des données vers et depuis un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="525fe-122">Dans cette section, nous allons voir comment utiliser l’utilitaire Distcp.</span><span class="sxs-lookup"><span data-stu-id="525fe-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="525fe-123">À partir de votre Bureau, utilisez SSH pour la connexion au cluster.</span><span class="sxs-lookup"><span data-stu-id="525fe-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="525fe-124">Consultez [Connexion à un cluster HDInsight sous Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="525fe-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="525fe-125">Exécutez les commandes de l’invite SSH.</span><span class="sxs-lookup"><span data-stu-id="525fe-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="525fe-126">Vérifiez si vous pouvez accéder aux objets blob d’Azure Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="525fe-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="525fe-127">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="525fe-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="525fe-128">Vous devriez obtenir la liste du contenu de l’objet blob de stockage.</span><span class="sxs-lookup"><span data-stu-id="525fe-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="525fe-129">Là encore, vérifiez si vous pouvez accéder au compte Data Lake Store à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="525fe-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="525fe-130">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="525fe-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="525fe-131">Vous devriez accéder à une liste des fichiers/dossiers contenus dans le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="525fe-132">Utilisez Distcp pour copier des données de WASB vers un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="525fe-133">Cette commande copie le contenu du dossier **/example/data/gutenberg/** de WASB vers le répertoire **/myfolder** du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="525fe-134">De la même manière, utilisez Distcp pour copier des données d’un compte Data Lake Store vers WASB.</span><span class="sxs-lookup"><span data-stu-id="525fe-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="525fe-135">Cette commande copie le contenu du répertoire **/myfolder** du compte Data Lake Store vers le dossier **/example/data/gutenberg/** de WASB.</span><span class="sxs-lookup"><span data-stu-id="525fe-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="525fe-136">Considérations de performances lors de l’utilisation de DistCp</span><span class="sxs-lookup"><span data-stu-id="525fe-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="525fe-137">La granularité la plus basse de DistCp étant un fichier unique, la définition du nombre maximal de copies simultanées est le paramètre le plus important à optimiser par rapport à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="525fe-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="525fe-138">Vous le contrôlez en définissant le paramètre de nombre de mappeurs (‘m’) en ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="525fe-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="525fe-139">Ce paramètre spécifie le nombre maximal de mappeurs utilisés pour copier les données.</span><span class="sxs-lookup"><span data-stu-id="525fe-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="525fe-140">La valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="525fe-140">Default value is 20.</span></span>

<span data-ttu-id="525fe-141">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="525fe-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="525fe-142">Comment déterminer le nombre de mappeurs à utiliser ?</span><span class="sxs-lookup"><span data-stu-id="525fe-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="525fe-143">Voici quelques conseils à suivre.</span><span class="sxs-lookup"><span data-stu-id="525fe-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="525fe-144">**Étape 1 : Déterminer la quantité totale de mémoire YARN** : la première étape consiste à déterminer la mémoire YARN disponible pour le cluster sur lequel vous exécutez la tâche DistCp.</span><span class="sxs-lookup"><span data-stu-id="525fe-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="525fe-145">Ces informations sont disponibles dans le portail de Ambari associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="525fe-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="525fe-146">Accédez à YARN et affichez l’onglet Configurations pour voir la mémoire YARN.</span><span class="sxs-lookup"><span data-stu-id="525fe-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="525fe-147">Pour obtenir la mémoire YARN totale, multipliez la mémoire YARN par nœud par le nombre de nœuds dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="525fe-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="525fe-148">**Étape 2 : Calculer le nombre de mappeurs** : la valeur de **m** est égale au quotient de la mémoire de YARN totale divisée par la taille du conteneur YARN.</span><span class="sxs-lookup"><span data-stu-id="525fe-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="525fe-149">Les informations sur la taille du conteneur YARN sont également disponibles dans le portail Ambari.</span><span class="sxs-lookup"><span data-stu-id="525fe-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="525fe-150">Accédez à YARN et affichez l’onglet Configurations.</span><span class="sxs-lookup"><span data-stu-id="525fe-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="525fe-151">La taille du conteneur YARN s’affiche dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="525fe-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="525fe-152">L’équation pour obtenir le nombre de mappeurs (**m**) est</span><span class="sxs-lookup"><span data-stu-id="525fe-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="525fe-153">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="525fe-153">**Example**</span></span>

<span data-ttu-id="525fe-154">Supposons que vous avez un 4 nœuds D14v2s dans le cluster et que vous essayez de transférer 10 To de données à partir de 10 différents dossiers.</span><span class="sxs-lookup"><span data-stu-id="525fe-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="525fe-155">Chaque dossier contient différentes quantités de données, et la taille des fichiers dans chaque dossier est différente.</span><span class="sxs-lookup"><span data-stu-id="525fe-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="525fe-156">Total de mémoire YARN : à partir du portail Ambari, vous déterminez que la mémoire YARN est de 96 Go pour un nœud D14.</span><span class="sxs-lookup"><span data-stu-id="525fe-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="525fe-157">Ainsi, la mémoire YARN totale pour un cluster à 4 nœuds est :</span><span class="sxs-lookup"><span data-stu-id="525fe-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="525fe-158">Nombre de mappeurs : à partir du portail Ambari, vous déterminez que la taille du conteneur YARN est de 3072 pour un nœud de cluster D14.</span><span class="sxs-lookup"><span data-stu-id="525fe-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="525fe-159">Par conséquent, le nombre de mappeurs est :</span><span class="sxs-lookup"><span data-stu-id="525fe-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="525fe-160">Si d’autres applications utilisent de la mémoire, vous pouvez choisir d’utiliser uniquement une partie de la mémoire de YARN de votre cluster pour DistCp.</span><span class="sxs-lookup"><span data-stu-id="525fe-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="525fe-161">Copie de jeux de données volumineux</span><span class="sxs-lookup"><span data-stu-id="525fe-161">Copying large datasets</span></span>

<span data-ttu-id="525fe-162">Lorsque la taille du jeu de données à déplacer est très volumineuse (par exemple > 1 To) ou si vous avez de nombreux dossiers, vous devez envisager d’utiliser plusieurs tâches DistCp.</span><span class="sxs-lookup"><span data-stu-id="525fe-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="525fe-163">Il n’y a probablement aucun gain de performance, mais cela répartira les tâches. Ainsi, si une tâche échoue, il vous suffit de redémarrer la tâche en question plutôt que l’ensemble complet.</span><span class="sxs-lookup"><span data-stu-id="525fe-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="525fe-164">Limitations</span><span class="sxs-lookup"><span data-stu-id="525fe-164">Limitations</span></span>

* <span data-ttu-id="525fe-165">DistCp tente de créer des mappeurs similaires en taille pour optimiser les performances.</span><span class="sxs-lookup"><span data-stu-id="525fe-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="525fe-166">L’augmentation du nombre de mappeurs n’améliore pas nécessairement les performances.</span><span class="sxs-lookup"><span data-stu-id="525fe-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="525fe-167">DistCp est limité à un seul mappeur par fichier.</span><span class="sxs-lookup"><span data-stu-id="525fe-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="525fe-168">Par conséquent, vous ne devez pas avoir plus de mappeurs que de fichiers.</span><span class="sxs-lookup"><span data-stu-id="525fe-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="525fe-169">Étant donné que DistCp peut affecter un seul mappeur par fichier, cela limite la quantité d’exécutions simultanées utilisables pour copier des fichiers volumineux.</span><span class="sxs-lookup"><span data-stu-id="525fe-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="525fe-170">Si vous avez un petit nombre de fichiers volumineux, vous devez les fractionner en plusieurs segments de fichier de 256 Mo pour avoir un meilleur potentiel de simultanéité.</span><span class="sxs-lookup"><span data-stu-id="525fe-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="525fe-171">Si vous copiez à partir d’un compte de stockage d’objets Blob Azure, votre tâche de copie peut être limitée sur le côté du stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="525fe-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="525fe-172">Cela dégradera les performances de votre tâche de copie.</span><span class="sxs-lookup"><span data-stu-id="525fe-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="525fe-173">Pour en savoir plus sur les limites du stockage Blob Azure, consultez les limites du stockage Azure sur [Abonnement Azure et limites du service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="525fe-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="525fe-174">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="525fe-174">See also</span></span>
* [<span data-ttu-id="525fe-175">Copier des données d’objets blob Azure Storage vers Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="525fe-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="525fe-176">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="525fe-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="525fe-177">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="525fe-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="525fe-178">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="525fe-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
