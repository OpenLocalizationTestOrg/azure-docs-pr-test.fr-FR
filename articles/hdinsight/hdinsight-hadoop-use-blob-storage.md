---
title: "Interroger des données depuis un stockage Azure compatible avec HDFS - Azure HDInsight | Microsoft Docs"
description: "Apprenez à interroger des données depuis un stockage Azure et Azure Data Lake Store pour stocker les résultats de votre analyse."
keywords: "stockage blob,hdfs,données structurées,données non structurées,data lake store,entrée Hadoop,sortie Hadoop,stockage hadoop,entrée hdfs,sortie hdfs,stockage hdfs, wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: a44c2b363f7ebb593b9a9c5bd9e0d4fc3b4c31bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="c166a-104">Utiliser le stockage Azure avec des clusters Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c166a-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="c166a-105">Pour analyser des données dans un cluster HDInsight, vous pouvez stocker les données dans le stockage Azure, Azure Data Lake Store ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c166a-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="c166a-106">Les deux options de stockage vous permettent de supprimer des clusters HDInsight servant aux calculs, sans perte de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c166a-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="c166a-107">Hadoop prend en charge une notion de système de fichiers par défaut.</span><span class="sxs-lookup"><span data-stu-id="c166a-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="c166a-108">Le système de fichiers par défaut implique un schéma et une autorité par défaut.</span><span class="sxs-lookup"><span data-stu-id="c166a-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="c166a-109">Il peut également être utilisé pour résoudre les chemins d'accès relatifs.</span><span class="sxs-lookup"><span data-stu-id="c166a-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="c166a-110">Pendant le processus de création du cluster HDInsight, vous pouvez spécifier un conteneur d’objets blob dans le stockage Azure comme système de fichiers par défaut, ou, avec HDInsight 3.5, vous pouvez sélectionner le stockage Azure ou Azure Data Lake Store en tant que système de fichiers par défaut avec quelques exceptions.</span><span class="sxs-lookup"><span data-stu-id="c166a-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> <span data-ttu-id="c166a-111">Pour la prise en charge de l’utilisation de Data Lake Store en tant que stockage associé et par défaut, consultez [Disponibilités pour le cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="c166a-111">For the supportability of using Data Lake Store as both the default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="c166a-112">Dans cet article, vous découvrez le fonctionnement du stockage Azure avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="c166a-113">Pour savoir comment Data Lake Store fonctionne avec les clusters HDInsight, consultez [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md) (Utiliser Azure Data Lake Store avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-113">To learn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="c166a-114">Consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="c166a-115">Le stockage Azure est une solution de stockage à la fois robuste et polyvalente qui s’intègre en toute transparence à HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="c166a-116">HDInsight peut utiliser un conteneur d’objets blob dans le stockage Azure comme système de fichiers par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="c166a-116">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="c166a-117">Grâce à une interface HDFS (Hadoop Distributed File System), l’ensemble des composants de HDInsight peut fonctionner directement sur les données structurées ou non structurées en tant qu’objets blob.</span><span class="sxs-lookup"><span data-stu-id="c166a-117">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="c166a-118">Plusieurs options sont disponibles lors de la création d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="c166a-119">Le tableau suivant fournit des informations sur les options prises en charge avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c166a-119">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="c166a-120">Type de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="c166a-120">Storage account type</span></span> | <span data-ttu-id="c166a-121">Niveau de stockage</span><span class="sxs-lookup"><span data-stu-id="c166a-121">Storage tier</span></span> | <span data-ttu-id="c166a-122">Pris en charge avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c166a-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="c166a-123">Compte de stockage à usage général</span><span class="sxs-lookup"><span data-stu-id="c166a-123">General-purpose Storage Account</span></span> | <span data-ttu-id="c166a-124">Standard</span><span class="sxs-lookup"><span data-stu-id="c166a-124">Standard</span></span> | <span data-ttu-id="c166a-125">__Oui__</span><span class="sxs-lookup"><span data-stu-id="c166a-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="c166a-126">Premium</span><span class="sxs-lookup"><span data-stu-id="c166a-126">Premium</span></span> | <span data-ttu-id="c166a-127">Non</span><span class="sxs-lookup"><span data-stu-id="c166a-127">No</span></span> |
> | <span data-ttu-id="c166a-128">Compte de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c166a-128">Blob Storage Account</span></span> | <span data-ttu-id="c166a-129">À chaud</span><span class="sxs-lookup"><span data-stu-id="c166a-129">Hot</span></span> | <span data-ttu-id="c166a-130">Non</span><span class="sxs-lookup"><span data-stu-id="c166a-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="c166a-131">À froid</span><span class="sxs-lookup"><span data-stu-id="c166a-131">Cool</span></span> | <span data-ttu-id="c166a-132">Non</span><span class="sxs-lookup"><span data-stu-id="c166a-132">No</span></span> |

<span data-ttu-id="c166a-133">Nous vous déconseillons d’utiliser le conteneur d’objets blob par défaut pour stocker des données d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c166a-133">We do not recommend that you use the default blob container for storing business data.</span></span> <span data-ttu-id="c166a-134">Nous vous recommandons de supprimer le conteneur d’objets blob par défaut après chaque utilisation pour réduire les coûts de stockage.</span><span class="sxs-lookup"><span data-stu-id="c166a-134">Deleting the default blob container after each use to reduce storage cost is a good practice.</span></span> <span data-ttu-id="c166a-135">Veuillez noter que le conteneur par défaut contient les journaux des applications et du système.</span><span class="sxs-lookup"><span data-stu-id="c166a-135">Note that the default container contains application and system logs.</span></span> <span data-ttu-id="c166a-136">Assurez-vous de récupérer les journaux avant de supprimer le conteneur.</span><span class="sxs-lookup"><span data-stu-id="c166a-136">Make sure to retrieve the logs before deleting the container.</span></span>

<span data-ttu-id="c166a-137">Le partage d’un conteneur d’objets blob sur plusieurs clusters n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c166a-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="c166a-138">Architecture de stockage HDInsight</span><span class="sxs-lookup"><span data-stu-id="c166a-138">HDInsight storage architecture</span></span>
<span data-ttu-id="c166a-139">Le schéma suivant résume l’architecture de stockage HDInsight relative au Stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="c166a-139">The following diagram provides an abstract view of the HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="c166a-140">![Les clusters Hadoop utilisent l’API HDFS pour accéder aux données structurées et non structurées et les stocker dans le stockage d’objets blob.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Architecture de stockage HDInsight")</span><span class="sxs-lookup"><span data-stu-id="c166a-140">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="c166a-141">HDInsight permet d'accéder au système de fichiers distribués (DFS) connecté localement aux nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="c166a-141">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="c166a-142">Vous pouvez accéder à ce système de fichiers en utilisant l'URI complet, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c166a-142">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="c166a-143">De plus, HDInsight permet d’accéder aux données stockées dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-143">In addition, HDInsight allows you to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="c166a-144">La syntaxe est :</span><span class="sxs-lookup"><span data-stu-id="c166a-144">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="c166a-145">Voici des points à prendre en compte lorsque vous utilisez un compte de stockage Azure avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="c166a-146">**Conteneurs dans les comptes de stockage connectés à un cluster :** comme le nom et la clé du compte sont associés au cluster durant la création, vous disposez d'un accès complet aux objets blob de ces conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c166a-146">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="c166a-147">**Conteneurs publics ou objets blob publics dans les comptes de stockage qui ne sont PAS connectés à un cluster :** vous avez l’autorisation en lecture seule pour les objets blob dans les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c166a-147">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c166a-148">Des conteneurs publics vous permettent d'obtenir une liste de tous les objets blob disponibles, ainsi que ses métadonnées.</span><span class="sxs-lookup"><span data-stu-id="c166a-148">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="c166a-149">Vous pouvez accéder aux objets blob d'un objet blob public uniquement si vous connaissez leur URL exacte.</span><span class="sxs-lookup"><span data-stu-id="c166a-149">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="c166a-150">Pour plus d'informations, consultez la page <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Limiter l'accès aux conteneurs et aux objets blob</a>.</span><span class="sxs-lookup"><span data-stu-id="c166a-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="c166a-151">**Conteneurs privés dans les comptes de stockage qui ne sont PAS connectés à un cluster :** vous ne pouvez pas accéder aux objets blob se trouvant dans les conteneurs, sauf si vous définissez le compte de stockage quand vous envoyez des travaux WebHCat.</span><span class="sxs-lookup"><span data-stu-id="c166a-151">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="c166a-152">Une explication sera fournie plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c166a-152">This is explained later in this article.</span></span>

<span data-ttu-id="c166a-153">Les comptes de stockage définis durant la création et leurs clés sont stockés dans %HADOOP_HOME%/conf/core-site.xml sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="c166a-153">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="c166a-154">Le comportement par défaut de HDInsight consiste à utiliser les comptes de stockage définis dans le fichier core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="c166a-154">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="c166a-155">Vous pouvez modifier ce paramètre avec [Ambari](./hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="c166a-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="c166a-156">Plusieurs tâches WebHCat, notamment Hive, MapReduce, la diffusion en continu Hadoop et Pig, peuvent véhiculer avec elles une description des comptes de stockage et des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="c166a-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="c166a-157">(cela fonctionne actuellement pour Pig, pour les comptes de stockage, mais pas pour les métadonnées.) Pour plus d'informations, consultez la page [Utilisation d'un cluster HDInsight avec des comptes de stockage et des metastores secondaires](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="c166a-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="c166a-158">Les objets blob peuvent être utilisés pour les données structurées et non structurées.</span><span class="sxs-lookup"><span data-stu-id="c166a-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="c166a-159">Les conteneurs d’objets blob stockent des données en tant que paires clé/valeur et sans hiérarchie de répertoires.</span><span class="sxs-lookup"><span data-stu-id="c166a-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="c166a-160">Cependant, vous pouvez utiliser la barre oblique (« / ») dans le nom de la clé pour la faire apparaître comme un fichier stocké dans une structure de répertoires.</span><span class="sxs-lookup"><span data-stu-id="c166a-160">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="c166a-161">Par exemple, une clé d'objet blob peut être *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="c166a-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="c166a-162">Il n'existe pas de répertoire *input* , mais la barre oblique figurant dans le nom de la clé lui donne l'aspect d'un chemin d'accès de fichier.</span><span class="sxs-lookup"><span data-stu-id="c166a-162">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

## <span data-ttu-id="c166a-163"><a id="benefits"></a>Avantages du stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c166a-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="c166a-164">La réduction des performances entraînée par la séparation des clusters de calcul et des ressources de stockage est compensée par le fait que les clusters de calcul sont créés à proximité des ressources du compte de stockage dans la région Azure, où le réseau à haut débit permet aux nœuds de calcul d’accéder efficacement aux données dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-164">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="c166a-165">Voici les avantages offerts par le stockage de données dans un stockage Azure au lieu d’un système HDFS :</span><span class="sxs-lookup"><span data-stu-id="c166a-165">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="c166a-166">**Réutilisation et partage des données :** les données du système HDFS sont situées dans le cluster de calcul.</span><span class="sxs-lookup"><span data-stu-id="c166a-166">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="c166a-167">Seules les applications pouvant accéder au cluster de calcul peuvent utiliser les données avec l'API HDFS.</span><span class="sxs-lookup"><span data-stu-id="c166a-167">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="c166a-168">Vous pouvez accéder aux données du stockage Azure via les API HDFS ou les [API REST de stockage Blob][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="c166a-168">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="c166a-169">Vous pouvez donc utiliser un plus grand nombre d'applications (notamment d'autres clusters HDInsight) et d'outils pour produire et consommer des données.</span><span class="sxs-lookup"><span data-stu-id="c166a-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="c166a-170">**Archivage des données :** le stockage de données dans le stockage Azure permet de supprimer les clusters HDInsight ayant servi aux calculs, sans perte de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c166a-170">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="c166a-171">**Coût de stockage des données :** le stockage à long terme des données dans DFS est plus coûteux que le stockage des données dans un stockage Azure, car le coût d’un cluster de calcul est plus élevé que celui d’un stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-171">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="c166a-172">De plus, comme vous n'avez pas à recharger les données pour chaque génération de cluster de calcul, vous faites également des économies sur les chargements de données.</span><span class="sxs-lookup"><span data-stu-id="c166a-172">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="c166a-173">**Montée en charge élastique :** même si le système HDFS offre un système de fichiers monté en charge, cette capacité est déterminée par le nombre de nœuds que vous créez pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c166a-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="c166a-174">Au lieu de procéder ainsi, il est parfois plus simple de profiter des capacités d’évolution flexible que vous obtenez automatiquement dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-174">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="c166a-175">**Géoréplication :** vous pouvez géo-répliquer votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="c166a-176">Si cette fonctionnalité permet la récupération géographique et la redondance des données, un basculement vers un emplacement géo-répliqué affecte sérieusement les performances et peut entraîner des frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="c166a-176">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="c166a-177">Nous vous recommandons donc de peser sérieusement le pour et le contre avant de choisir la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="c166a-177">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="c166a-178">Certains packages et travaux MapReduce peuvent créer des résultats intermédiaires que vous ne voulez pas stocker dans un stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="c166a-179">Dans ce cas, vous pouvez choisir de stocker les données dans un système HDFS local.</span><span class="sxs-lookup"><span data-stu-id="c166a-179">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="c166a-180">En fait, HDInsight utilise DFS pour plusieurs de ces résultats intermédiaires dans les tâches Hive et d'autres processus.</span><span class="sxs-lookup"><span data-stu-id="c166a-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c166a-181">La plupart des commandes HDFS (par exemple <b>ls</b>, <b>copyFromLocal</b> et <b>mkdir</b>) fonctionnent toujours comme prévu.</span><span class="sxs-lookup"><span data-stu-id="c166a-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="c166a-182">Seules les commandes propres à l’implémentation HDFS native (nommée DFS), telles que <b>fschk</b> et <b>dfsadmin</b> se comportent différemment dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-182">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="c166a-183">Création de conteneurs d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c166a-183">Create Blob containers</span></span>
<span data-ttu-id="c166a-184">Pour utiliser des objets blob, commencez par créer un [compte de stockage Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="c166a-184">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="c166a-185">À cette étape, vous spécifiez une région Azure dans laquelle le compte de stockage est créé.</span><span class="sxs-lookup"><span data-stu-id="c166a-185">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="c166a-186">Le cluster et le compte de stockage doivent être hébergés dans la même région.</span><span class="sxs-lookup"><span data-stu-id="c166a-186">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="c166a-187">La base de données SQL Server de metastore Hive et la base de données SQL Server de metastore Oozie doivent également se trouver dans la même région.</span><span class="sxs-lookup"><span data-stu-id="c166a-187">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="c166a-188">Où qu’il réside, chaque objet blob que vous créez appartient à un conteneur de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-188">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="c166a-189">Ce conteneur peut être un objet blob existant créé hors de HDInsight ou un conteneur créé pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="c166a-190">Le conteneur d’objets blob par défaut stocke les informations spécifiques de cluster telles que l’historique et les journaux des travaux.</span><span class="sxs-lookup"><span data-stu-id="c166a-190">The default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="c166a-191">Ne partagez pas un conteneur d’objets blob par défaut avec plusieurs clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="c166a-192">Cela est susceptible d’endommager l’historique des travaux.</span><span class="sxs-lookup"><span data-stu-id="c166a-192">This might corrupt job history.</span></span> <span data-ttu-id="c166a-193">Il est recommandé d’utiliser un conteneur différent pour chaque cluster et de placer des données partagées sur un compte de stockage lié spécifié dans le déploiement de tous les clusters pertinents plutôt que d’utiliser le compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="c166a-193">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="c166a-194">Pour plus d'informations sur la configuration des comptes de stockage liés, consultez la rubrique [Création de clusters HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="c166a-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="c166a-195">Vous pouvez, toutefois, réutiliser un conteneur de stockage par défaut une fois le cluster HDInsight d'origine supprimé.</span><span class="sxs-lookup"><span data-stu-id="c166a-195">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="c166a-196">Pour les clusters HBase, vous pouvez conserver le schéma et les données de la table HBase en créant un cluster HBase à l’aide du conteneur d’objets blob par défaut utilisé par un cluster HBase ayant été supprimé.</span><span class="sxs-lookup"><span data-stu-id="c166a-196">For HBase clusters, you can actually retain the HBase table schema and data by creating a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-the-azure-portal"></a><span data-ttu-id="c166a-197">Utilisation du portail Azure</span><span class="sxs-lookup"><span data-stu-id="c166a-197">Use the Azure portal</span></span>
<span data-ttu-id="c166a-198">Lorsque vous créez un cluster HDInsight à partir du portail, vous avez la possibilité (comme indiqué ci-dessous) de fournir les détails du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c166a-198">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="c166a-199">Vous pouvez également spécifier si vous souhaitez un compte de stockage supplémentaire associé au cluster et, si c’est le cas, choisir Data Lake Store ou un autre Azure Storage Blob en tant que stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c166a-199">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![source de données de création hadoop HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="c166a-201">L’utilisation d’un compte de stockage supplémentaire dans un autre emplacement que le cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c166a-201">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="c166a-202">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c166a-202">Use Azure PowerShell</span></span>
<span data-ttu-id="c166a-203">Si vous avez [installé et configuré Azure PowerShell][powershell-install], vous pouvez utiliser la commande suivante dans l’invite Azure PowerShell pour créer un compte de stockage et un conteneur :</span><span class="sxs-lookup"><span data-stu-id="c166a-203">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="c166a-204">Utiliser l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c166a-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="c166a-205">Si vous avez [installé et configuré l’interface de ligne de commande Azure](../cli-install-nodejs.md), la commande suivante peut être utilisée sur un compte de stockage et un conteneur.</span><span class="sxs-lookup"><span data-stu-id="c166a-205">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="c166a-206">Le paramètre `--type` indique la méthode de réplication du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c166a-206">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="c166a-207">Pour plus d'informations, consultez [Réplication Azure Storage](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="c166a-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="c166a-208">N’utilisez pas le stockage redondant dans une zone (ZRS), car ZRS ne prend pas en charge les objets blob de pages, les fichiers, les tables ni les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="c166a-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="c166a-209">Vous devez spécifier la région géographique dans laquelle est créé le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c166a-209">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="c166a-210">Vous devez créer le compte de stockage dans la région où vous envisagez de créer votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-210">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="c166a-211">Une fois le compte de stockage créé, utilisez la commande suivante pour récupérer les clés du compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="c166a-211">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="c166a-212">Pour créer un conteneur, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c166a-212">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="c166a-213">Adressage des fichiers dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c166a-213">Address files in Azure storage</span></span>
<span data-ttu-id="c166a-214">Le modèle d’URI pour accéder aux fichiers du stockage Azure à partir de HDInsight est le suivant :</span><span class="sxs-lookup"><span data-stu-id="c166a-214">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="c166a-215">Le modèle d'URI offre à la fois un accès non chiffré (avec le préfixe *wasb:*) et un accès chiffré SSL (avec *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="c166a-215">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="c166a-216">Dans la mesure du possible, nous vous recommandons d’utiliser *wasbs* , même lorsqu’il s’agit d’accéder à des données qui résident dans la même région Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="c166a-217">Le &lt;BlobStorageContainerName&gt; identifie le nom du conteneur d’objets blob dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-217">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="c166a-218">Le &lt;StorageAccountName&gt; identifie le nom de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c166a-218">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="c166a-219">Un nom de domaine complet (FQDN) est requis.</span><span class="sxs-lookup"><span data-stu-id="c166a-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="c166a-220">Si ni &lt;BlobStorageContainerName&gt; ni &lt;StorageAccountName&gt; n'a été spécifié, le système de fichiers par défaut est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c166a-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="c166a-221">Pour les fichiers du système de fichiers par défaut, vous pouvez utiliser un chemin d'accès relatif ou absolu.</span><span class="sxs-lookup"><span data-stu-id="c166a-221">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="c166a-222">Par exemple, le fichier *hadoop-mapreduce-examples.jar* fourni avec les clusters HDInsight peut être désigné pour l'une des utilisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c166a-222">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="c166a-223">Le nom du fichier est <i>hadoop-examples.jar</i> sur les clusters HDInsight version 2.1 et 1.6.</span><span class="sxs-lookup"><span data-stu-id="c166a-223">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="c166a-224">Le &lt;path&gt; correspond au nom du chemin d'accès du fichier ou du répertoire HDFS.</span><span class="sxs-lookup"><span data-stu-id="c166a-224">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="c166a-225">Comme les conteneurs dans le stockage Azure constituent simplement un magasin de clé-valeur, il n’y a pas de système de fichiers hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="c166a-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="c166a-226">Une barre oblique (« / ») à l'intérieur d'une clé d'objet blob est interprétée comme un séparateur de répertoire.</span><span class="sxs-lookup"><span data-stu-id="c166a-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="c166a-227">Par exemple, le nom d'objet blob pour *hadoop-mapreduce-examples.jar* est :</span><span class="sxs-lookup"><span data-stu-id="c166a-227">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="c166a-228">Lorsque vous utilisez des objets blob hors de HDInsight, la plupart des utilitaires ne reconnaissent pas le format WASB et attendent plutôt un format de chemin d’accès basique, comme `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="c166a-228">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="c166a-229">Accéder aux objets BLOB</span><span class="sxs-lookup"><span data-stu-id="c166a-229">Access blobs</span></span> 


### <span data-ttu-id="c166a-230"><a name="access-blobs-using-azure-powershell"></a> Utiliser Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c166a-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c166a-231">Les commandes de cette section présentent des exemples basiques d’utilisation de PowerShell pour accéder aux données stockées dans des objets blob.</span><span class="sxs-lookup"><span data-stu-id="c166a-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="c166a-232">Pour un exemple plus complet personnalisé pour une utilisation avec HDInsight, consultez la section [Outils HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="c166a-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="c166a-233">Utilisez la commande suivante pour répertorier les cmdlets relatives aux objets blob :</span><span class="sxs-lookup"><span data-stu-id="c166a-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![Liste des cmdlets PowerShell relatives aux objets blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="c166a-235">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="c166a-235">Upload files</span></span>
<span data-ttu-id="c166a-236">Consultez la rubrique [Téléchargement de données vers HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="c166a-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="c166a-237">Téléchargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="c166a-237">Download files</span></span>
<span data-ttu-id="c166a-238">Le script suivant télécharge un objet blob de blocs vers le dossier actuel.</span><span class="sxs-lookup"><span data-stu-id="c166a-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="c166a-239">Avant d'exécuter le script, remplacez le répertoire par un dossier sur lequel vous disposez d'accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="c166a-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="c166a-240">Vous pouvez utiliser le code suivant pour fournir le nom de groupe de ressources et le nom du cluster :</span><span class="sxs-lookup"><span data-stu-id="c166a-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="c166a-241">Supprimer des fichiers</span><span class="sxs-lookup"><span data-stu-id="c166a-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="c166a-242">Énumérer des fichiers</span><span class="sxs-lookup"><span data-stu-id="c166a-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="c166a-243">Exécution de requêtes Hive à l'aide d'un compte de stockage non défini</span><span class="sxs-lookup"><span data-stu-id="c166a-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="c166a-244">Cet exemple montre comment répertorier le contenu d’un dossier d’un compte de stockage non défini pendant le processus de création.</span><span class="sxs-lookup"><span data-stu-id="c166a-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="c166a-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="c166a-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="c166a-246">Utiliser l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c166a-246">Use Azure CLI</span></span>
<span data-ttu-id="c166a-247">Utilisez la commande suivante pour répertorier les commandes relatives aux objets blob :</span><span class="sxs-lookup"><span data-stu-id="c166a-247">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="c166a-248">**Exemple d’utilisation de l’interface de ligne de commande Azure pour charger un fichier**</span><span class="sxs-lookup"><span data-stu-id="c166a-248">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c166a-249">**Exemple d’utilisation de l’interface de ligne de commande Azure pour télécharger un fichier**</span><span class="sxs-lookup"><span data-stu-id="c166a-249">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c166a-250">**Exemple d’utilisation de l’interface de ligne de commande Azure pour supprimer un fichier**</span><span class="sxs-lookup"><span data-stu-id="c166a-250">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c166a-251">**Exemple d’utilisation de l’interface de ligne de commande Azure pour répertorier des fichiers**</span><span class="sxs-lookup"><span data-stu-id="c166a-251">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="c166a-252">Utiliser des comptes de stockage supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c166a-252">Use additional storage accounts</span></span>

<span data-ttu-id="c166a-253">Lorsque vous créez un cluster HDInsight, vous spécifiez le compte de stockage Azure que vous souhaitez lui associer.</span><span class="sxs-lookup"><span data-stu-id="c166a-253">While creating an HDInsight cluster, you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="c166a-254">Outre ce compte de stockage, vous pouvez en ajouter d’autres à partir du même abonnement Azure ou à partir d’autres abonnements Azure pendant le processus de création ou à l’issue de la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="c166a-254">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="c166a-255">Pour en savoir plus sur l'ajout de comptes de stockage supplémentaires, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c166a-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="c166a-256">L’utilisation d’un compte de stockage supplémentaire dans un autre emplacement que le cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c166a-256">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c166a-257">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c166a-257">Next steps</span></span>
<span data-ttu-id="c166a-258">Dans cet article, vous avez appris à utiliser un stockage Azure compatible avec HDFS avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c166a-258">In this article, you learned how to use HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="c166a-259">Ceci vous permet de créer des solutions à long terme et évolutives d’acquisition et d’archivage de données et d’utiliser HDInsight pour déverrouiller les informations des données structurées et non structurées stockées.</span><span class="sxs-lookup"><span data-stu-id="c166a-259">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="c166a-260">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="c166a-260">For more information, see:</span></span>

* <span data-ttu-id="c166a-261">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c166a-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="c166a-262">Prise en main d’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c166a-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="c166a-263">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c166a-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c166a-264">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c166a-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c166a-265">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c166a-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c166a-266">[Utilisation des signatures d’accès partagé Azure Storage pour restreindre l’accès aux données avec HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="c166a-266">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
