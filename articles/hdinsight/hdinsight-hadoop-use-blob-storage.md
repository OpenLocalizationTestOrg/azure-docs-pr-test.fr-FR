---
title: "aaaQuery des données à partir de HDFS compatible avec le stockage Azure - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooquery les données de stockage Azure et d’Azure Data Lake Store toostore des résultats de votre analyse."
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
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="c45a4-104">Utiliser le stockage Azure avec des clusters Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c45a4-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="c45a4-105">tooanalyze des données dans le cluster HDInsight, vous pouvez stocker des données de hello dans le stockage Azure, Azure Data Lake Store ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c45a4-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="c45a4-106">Les deux options de stockage permettent de supprimer toosafely que des clusters HDInsight qui sont utilisés pour le calcul sans perdre de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c45a4-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="c45a4-107">Hadoop prend en charge une notion hello par défaut du système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c45a4-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="c45a4-108">système de fichiers par défaut Hello implique un schéma par défaut et une autorité.</span><span class="sxs-lookup"><span data-stu-id="c45a4-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="c45a4-109">Il peut également être tooresolve utilisé des chemins d’accès relatifs.</span><span class="sxs-lookup"><span data-stu-id="c45a4-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="c45a4-110">Au cours de hello processus de création du cluster HDInsight, vous pouvez spécifier un conteneur d’objets blob dans le stockage Azure en tant que système de fichiers par défaut hello ou avec HDInsight 3.5, vous pouvez sélectionner le stockage Azure ou Azure Data Lake Store en tant que système de fichiers par défaut hello à quelques exceptions près.</span><span class="sxs-lookup"><span data-stu-id="c45a4-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="c45a4-111">Pour la prise en charge de hello de l’utilisation de Data Lake Store comme valeur par défaut hello et de stockage, consultez [disponibilités pour le cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="c45a4-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="c45a4-112">Dans cet article, vous découvrez le fonctionnement du stockage Azure avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="c45a4-113">toolearn Data Lake Store fonctionnement avec les clusters HDInsight, consultez [utilisez Azure Data Lake Store avec Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="c45a4-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="c45a4-114">Consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="c45a4-115">Le stockage Azure est une solution de stockage à la fois robuste et polyvalente qui s’intègre en toute transparence à HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="c45a4-116">HDInsight peut utiliser un conteneur d’objets blob dans le stockage Azure en tant que système de fichiers par défaut hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="c45a4-117">Via une interface (HDFS) de système de fichiers distribués Hadoop, ensemble de hello de composants dans HDInsight peut fonctionner directement sur les données structurées ou non structurées stockées en tant qu’objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="c45a4-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="c45a4-118">Plusieurs options sont disponibles lors de la création d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="c45a4-119">Hello tableau suivant fournit des informations sur les options sont prises en charge avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c45a4-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="c45a4-120">Type de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="c45a4-120">Storage account type</span></span> | <span data-ttu-id="c45a4-121">Niveau de stockage</span><span class="sxs-lookup"><span data-stu-id="c45a4-121">Storage tier</span></span> | <span data-ttu-id="c45a4-122">Pris en charge avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c45a4-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="c45a4-123">Compte de stockage à usage général</span><span class="sxs-lookup"><span data-stu-id="c45a4-123">General-purpose Storage Account</span></span> | <span data-ttu-id="c45a4-124">Standard</span><span class="sxs-lookup"><span data-stu-id="c45a4-124">Standard</span></span> | <span data-ttu-id="c45a4-125">__Oui__</span><span class="sxs-lookup"><span data-stu-id="c45a4-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="c45a4-126">Premium</span><span class="sxs-lookup"><span data-stu-id="c45a4-126">Premium</span></span> | <span data-ttu-id="c45a4-127">Non</span><span class="sxs-lookup"><span data-stu-id="c45a4-127">No</span></span> |
> | <span data-ttu-id="c45a4-128">Compte de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c45a4-128">Blob Storage Account</span></span> | <span data-ttu-id="c45a4-129">À chaud</span><span class="sxs-lookup"><span data-stu-id="c45a4-129">Hot</span></span> | <span data-ttu-id="c45a4-130">Non</span><span class="sxs-lookup"><span data-stu-id="c45a4-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="c45a4-131">À froid</span><span class="sxs-lookup"><span data-stu-id="c45a4-131">Cool</span></span> | <span data-ttu-id="c45a4-132">Non</span><span class="sxs-lookup"><span data-stu-id="c45a4-132">No</span></span> |

<span data-ttu-id="c45a4-133">Nous vous déconseillons d’utiliser le conteneur d’objets blob hello par défaut pour le stockage des données d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="c45a4-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="c45a4-134">La suppression du conteneur d’objets blob par défaut hello après chaque tooreduce utilisez coût de stockage est une bonne pratique.</span><span class="sxs-lookup"><span data-stu-id="c45a4-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="c45a4-135">Notez que le conteneur par défaut hello contient des applications et du système des journaux.</span><span class="sxs-lookup"><span data-stu-id="c45a4-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="c45a4-136">Vérifiez les journaux hello tooretrieve vraiment avant de supprimer le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="c45a4-137">Le partage d’un conteneur d’objets blob sur plusieurs clusters n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c45a4-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="c45a4-138">Architecture de stockage HDInsight</span><span class="sxs-lookup"><span data-stu-id="c45a4-138">HDInsight storage architecture</span></span>
<span data-ttu-id="c45a4-139">Hello suivant schéma fournit une vue abstraite de hello HDInsight architecture de stockage de l’utilisation du stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="c45a4-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="c45a4-140">![Clusters Hadoop utilisent hello HDFS API tooaccess et stocker des données structurées et non structurées dans le stockage Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "L’Architecture de stockage de HDInsight")</span><span class="sxs-lookup"><span data-stu-id="c45a4-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="c45a4-141">HDInsight fournit le système de fichiers accès toohello distribué est localement attaché toohello les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="c45a4-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="c45a4-142">Ce système de fichiers sont accessibles à l’aide de hello complet URI, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c45a4-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="c45a4-143">En outre, HDInsight vous permet de tooaccess les données stockées dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="c45a4-144">syntaxe de Hello est :</span><span class="sxs-lookup"><span data-stu-id="c45a4-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="c45a4-145">Voici des points à prendre en compte lorsque vous utilisez un compte de stockage Azure avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="c45a4-146">**Conteneurs dans des comptes de stockage hello qui sont connectés tooa cluster :** étant hello nom et une clé associés hello cluster lors de la création, vous avez les objets BLOB de toohello un accès complet dans ces conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c45a4-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="c45a4-147">**Conteneurs publics ou des objets BLOB publics dans les comptes de stockage qui ne sont pas connectés tooa cluster :** vous disposez des autorisations en lecture seule toohello des objets BLOB des conteneurs de hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c45a4-148">Conteneurs publics autorisent tooget une liste de tous les objets BLOB qui sont disponibles dans le conteneur et d’obtenir les métadonnées de conteneur.</span><span class="sxs-lookup"><span data-stu-id="c45a4-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="c45a4-149">Objets BLOB publics permettre de BLOB de hello tooaccess uniquement si vous connaissez l’URL exacte hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="c45a4-150">Pour plus d’informations, consultez <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">restreindre l’accès toocontainers et les objets BLOB</a>.</span><span class="sxs-lookup"><span data-stu-id="c45a4-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="c45a4-151">**Les conteneurs privés dans des comptes de stockage qui ne sont pas connectés tooa cluster :** BLOB hello dans les conteneurs hello n’est pas accessible, sauf si vous définissez le compte de stockage hello lorsque vous envoyez des travaux de WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="c45a4-152">Une explication sera fournie plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c45a4-152">This is explained later in this article.</span></span>

<span data-ttu-id="c45a4-153">les comptes de stockage Hello qui sont définies dans le processus de création de hello et leurs clés sont stockées dans %HADOOP_HOME%/conf/core-site.xml sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="c45a4-154">comportement par défaut de Hello de HDInsight est définis dans le fichier de base-site.XML hello les comptes de stockage toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="c45a4-155">Vous pouvez modifier ce paramètre avec [Ambari](./hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="c45a4-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="c45a4-156">Plusieurs tâches WebHCat, notamment Hive, MapReduce, la diffusion en continu Hadoop et Pig, peuvent véhiculer avec elles une description des comptes de stockage et des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="c45a4-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="c45a4-157">(cela fonctionne actuellement pour Pig, pour les comptes de stockage, mais pas pour les métadonnées.) Pour plus d'informations, consultez la page [Utilisation d'un cluster HDInsight avec des comptes de stockage et des metastores secondaires](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="c45a4-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="c45a4-158">Les objets blob peuvent être utilisés pour les données structurées et non structurées.</span><span class="sxs-lookup"><span data-stu-id="c45a4-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="c45a4-159">Les conteneurs d’objets blob stockent des données en tant que paires clé/valeur et sans hiérarchie de répertoires.</span><span class="sxs-lookup"><span data-stu-id="c45a4-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="c45a4-160">Toutefois, le caractère de barre oblique hello (/) peut être utilisé dans hello toomake nom de la clé il apparaît comme si un fichier est stocké dans une structure de répertoire.</span><span class="sxs-lookup"><span data-stu-id="c45a4-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="c45a4-161">Par exemple, une clé d'objet blob peut être *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="c45a4-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="c45a4-162">Ne réel *d’entrée* répertoire existe, mais en raison de la présence de toohello du caractère de barre oblique hello dans le nom de la clé hello, il semble hello un chemin d’accès de fichier.</span><span class="sxs-lookup"><span data-stu-id="c45a4-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="c45a4-163"><a id="benefits"></a>Avantages du stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c45a4-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="c45a4-164">Hello implicite de coût de performance de pas colocaliser des clusters de calcul et des ressources de stockage est atténuée par moyen hello clusters de calcul hello sont créés les ressources de compte de stockage toohello fermer à l’intérieur de hello région Azure, où le réseau à grande vitesse hello permet efficace pour les nœuds de calcul hello tooaccess hello des données dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="c45a4-165">Il existe plusieurs avantages associés au stockage des données de salutation dans le stockage Azure au lieu de HDFS :</span><span class="sxs-lookup"><span data-stu-id="c45a4-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="c45a4-166">**Partage et la réutilisation des données :** données hello dans HDFS se trouve à l’intérieur du cluster de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="c45a4-167">Seules les applications hello qui ont accès toohello compute cluster permettre utiliser des données de hello en utilisant les API de HDFS.</span><span class="sxs-lookup"><span data-stu-id="c45a4-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="c45a4-168">données de Hello dans le stockage Azure sont accessibles par le biais hello HDFS API ou hello [API REST de stockage Blob][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="c45a4-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="c45a4-169">Par conséquent, un ensemble plus important d’applications (y compris les autres clusters HDInsight) et les outils permettre être utilisé tooproduce et consommer des données de la hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="c45a4-170">**L’archivage des données :** le stockage des données dans le stockage Azure permet de clusters HDInsight de hello utilisés pour toobe calcul supprimé en toute sécurité sans perdre de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c45a4-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="c45a4-171">**Coût de stockage de données :** le stockage des données dans DFS pour hello à long terme est plus coûteuse que le stockage des données de salutation dans le stockage Azure, car le coût de hello d’un cluster de calcul est supérieur à coût hello de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="c45a4-172">En outre, étant donné que les données de salutation n’ayant pas de toobe rechargé pour chaque génération de cluster de calcul, vous enregistrez également les coûts de chargement des données.</span><span class="sxs-lookup"><span data-stu-id="c45a4-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="c45a4-173">**Montée en puissance parallèle élastique :** HDFS bien que vous fournit un système de fichiers de montée en charge, la montée en puissance hello est déterminée par le nombre de hello de nœuds que vous créez pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c45a4-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="c45a4-174">Modification de l’échelle de hello peut devenir un processus plus complexe que partie de confiance sur élastique hello mise à l’échelle les fonctionnalités que vous obtenez automatiquement dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="c45a4-175">**Géoréplication :** vous pouvez géo-répliquer votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="c45a4-176">Bien que cela vous donne la redondance des données et récupération géographique, un emplacement géorépliqué de basculement toohello affecte sérieusement les performances de vos, et il peut entraîner des frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="c45a4-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="c45a4-177">Notre recommandation est toochoose hello géo-réplication avec soin et uniquement si la valeur de données de hello hello est la valeur hello coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c45a4-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="c45a4-178">Certaines tâches MapReduce et les packages peuvent créer des résultats intermédiaires que vous ne souhaitez pas vraiment toostore dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="c45a4-179">Dans ce cas, vous pouvez choisir les données hello toostore hello HDFS local.</span><span class="sxs-lookup"><span data-stu-id="c45a4-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="c45a4-180">En fait, HDInsight utilise DFS pour plusieurs de ces résultats intermédiaires dans les tâches Hive et d'autres processus.</span><span class="sxs-lookup"><span data-stu-id="c45a4-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c45a4-181">La plupart des commandes HDFS (par exemple <b>ls</b>, <b>copyFromLocal</b> et <b>mkdir</b>) fonctionnent toujours comme prévu.</span><span class="sxs-lookup"><span data-stu-id="c45a4-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="c45a4-182">Hello uniquement les commandes qui sont spécifiques toohello HDFS implémentation native (qui est référencé tooas DFS) comme <b>fschk</b> et <b>dfsadmin</b>, afficher un comportement différent dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="c45a4-183">Création de conteneurs d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c45a4-183">Create Blob containers</span></span>
<span data-ttu-id="c45a4-184">objets BLOB toouse, tout d’abord créer un [compte de stockage Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="c45a4-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="c45a4-185">Ce cadre, vous spécifiez une région Azure où le compte de stockage hello est créé.</span><span class="sxs-lookup"><span data-stu-id="c45a4-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="c45a4-186">cluster de Hello et compte de stockage hello doivent être hébergés dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="c45a4-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="c45a4-187">Hello Hive le magasin de métadonnées SQL Server et SQL Server, base de données doit également se trouver dans le magasin de métadonnées Oozie hello même région.</span><span class="sxs-lookup"><span data-stu-id="c45a4-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="c45a4-188">Partout où il réside, chaque objet blob que vous créez appartient conteneur tooa dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="c45a4-189">Ce conteneur peut être un objet blob existant créé hors de HDInsight ou un conteneur créé pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="c45a4-190">conteneur d’objets Blob par défaut Hello stocke les informations de cluster spécifiques telles que l’historique des travaux et des journaux.</span><span class="sxs-lookup"><span data-stu-id="c45a4-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="c45a4-191">Ne partagez pas un conteneur d’objets blob par défaut avec plusieurs clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="c45a4-192">Cela est susceptible d’endommager l’historique des travaux.</span><span class="sxs-lookup"><span data-stu-id="c45a4-192">This might corrupt job history.</span></span> <span data-ttu-id="c45a4-193">Il est recommandé de toouse un conteneur différent pour chaque cluster et placer des données partagées sur un compte de stockage spécifié dans le déploiement de toutes les clusters au lieu du compte de stockage par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="c45a4-194">Pour plus d'informations sur la configuration des comptes de stockage liés, consultez la rubrique [Création de clusters HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="c45a4-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="c45a4-195">Toutefois, vous pouvez réutiliser un conteneur de stockage par défaut une fois le cluster de HDInsight hello d’origine a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="c45a4-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="c45a4-196">Pour des clusters HBase, vous pouvez réellement conserver les données et le schéma de la table HBase hello en créant un nouveau cluster HBase à l’aide du conteneur d’objets blob hello par défaut est utilisé par un cluster HBase qui a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="c45a4-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="c45a4-197">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c45a4-197">Use hello Azure portal</span></span>
<span data-ttu-id="c45a4-198">Lorsque vous créez un cluster HDInsight à partir de hello Portal, vous avez hello options (comme indiqué ci-dessous) tooprovide hello compte de stockage détails.</span><span class="sxs-lookup"><span data-stu-id="c45a4-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="c45a4-199">Vous pouvez également spécifier si vous souhaitez un compte de stockage supplémentaires associées au cluster de hello et dans ce cas, choisissez Data Lake Store ou un autre objet blob de stockage Azure en tant qu’espace de stockage supplémentaire hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![source de données de création hadoop HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="c45a4-201">À l’aide d’un compte de stockage supplémentaire dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c45a4-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="c45a4-202">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c45a4-202">Use Azure PowerShell</span></span>
<span data-ttu-id="c45a4-203">Si vous [installé et configuré Azure PowerShell][powershell-install], vous pouvez utiliser hello suivant toocreate invite de PowerShell Azure hello un compte de stockage et un conteneur :</span><span class="sxs-lookup"><span data-stu-id="c45a4-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="c45a4-204">Utiliser l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c45a4-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="c45a4-205">Si vous avez [installé et configuré hello CLI d’Azure](../cli-install-nodejs.md), suivants de hello commande peut être compte de stockage tooa utilisé et le conteneur.</span><span class="sxs-lookup"><span data-stu-id="c45a4-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="c45a4-206">Hello `--type` paramètre indique la manière dont le compte de stockage hello est répliquée.</span><span class="sxs-lookup"><span data-stu-id="c45a4-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="c45a4-207">Pour plus d'informations, consultez [Réplication Azure Storage](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="c45a4-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="c45a4-208">N’utilisez pas le stockage redondant dans une zone (ZRS), car ZRS ne prend pas en charge les objets blob de pages, les fichiers, les tables ni les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="c45a4-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="c45a4-209">Vous êtes toospecify demandées hello région que le compte de stockage hello est créé dans.</span><span class="sxs-lookup"><span data-stu-id="c45a4-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="c45a4-210">Vous devez créer le compte de stockage hello Bonjour même région que vous prévoyez sur la création de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="c45a4-211">Une fois que le compte de stockage hello est créé, utilisez hello suivant des clés de compte de stockage commande tooretrieve hello :</span><span class="sxs-lookup"><span data-stu-id="c45a4-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="c45a4-212">toocreate un conteneur, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c45a4-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="c45a4-213">Adressage des fichiers dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c45a4-213">Address files in Azure storage</span></span>
<span data-ttu-id="c45a4-214">schéma d’URI Hello pour accéder aux fichiers dans le stockage Azure à partir de HDInsight est :</span><span class="sxs-lookup"><span data-stu-id="c45a4-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="c45a4-215">schéma d’URI Hello fournit un accès non chiffrés (avec hello *wasb :* préfixe) et SSL chiffrée accès (avec *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="c45a4-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="c45a4-216">Nous vous recommandons d’utiliser *wasbs* dans la mesure du possible, même lorsque l’accès aux données qui réside à l’intérieur de hello même région dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="c45a4-217">Hello &lt;BlobStorageContainerName&gt; identifie le nom de hello du conteneur d’objets blob hello dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a4-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="c45a4-218">Hello &lt;StorageAccountName&gt; identifie le nom de compte de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c45a4-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="c45a4-219">Un nom de domaine complet (FQDN) est requis.</span><span class="sxs-lookup"><span data-stu-id="c45a4-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="c45a4-220">Si ni &lt;BlobStorageContainerName&gt; ni &lt;StorageAccountName&gt; a été spécifié, système de fichiers par défaut hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c45a4-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="c45a4-221">Pour les fichiers hello sur le système de fichiers par défaut hello, vous pouvez utiliser un chemin d’accès relatif ou un chemin d’accès absolu.</span><span class="sxs-lookup"><span data-stu-id="c45a4-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="c45a4-222">Par exemple, hello *hadoop-mapreduce-Examples.jar* fichier fourni avec les clusters HDInsight peut être tooby référencé à l’aide de valeurs hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c45a4-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="c45a4-223">nom de fichier Hello est <i>hadoop-Examples.jar</i> dans les clusters HDInsight versions 2.1 et version 1.6.</span><span class="sxs-lookup"><span data-stu-id="c45a4-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="c45a4-224">Hello &lt;chemin d’accès&gt; est hello fichier ou répertoire HDFS chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="c45a4-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="c45a4-225">Comme les conteneurs dans le stockage Azure constituent simplement un magasin de clé-valeur, il n’y a pas de système de fichiers hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="c45a4-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="c45a4-226">Une barre oblique (« / ») à l'intérieur d'une clé d'objet blob est interprétée comme un séparateur de répertoire.</span><span class="sxs-lookup"><span data-stu-id="c45a4-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="c45a4-227">Par exemple, les nom d’objet blob hello pour *hadoop-mapreduce-Examples.jar* est :</span><span class="sxs-lookup"><span data-stu-id="c45a4-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="c45a4-228">Lorsque vous travaillez avec des objets BLOB en dehors de HDInsight, la plupart des utilitaires ne pas reconnaître le format WASB hello et à la place attendent un format de chemin d’accès de base, telles que `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="c45a4-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="c45a4-229">Accéder aux objets BLOB</span><span class="sxs-lookup"><span data-stu-id="c45a4-229">Access blobs</span></span> 


### <span data-ttu-id="c45a4-230"><a name="access-blobs-using-azure-powershell"></a> Utiliser Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c45a4-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c45a4-231">commandes Hello dans cette section fournissent un exemple de base de l’utilisation de PowerShell tooaccess données est stockées dans des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="c45a4-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="c45a4-232">Pour obtenir un exemple plus complet qui est personnalisé pour travailler avec HDInsight, consultez hello [outils HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="c45a4-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="c45a4-233">Utilisez hello suivant commande toolist hello blob applets de commande :</span><span class="sxs-lookup"><span data-stu-id="c45a4-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Liste des cmdlets PowerShell relatives aux objets blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="c45a4-235">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="c45a4-235">Upload files</span></span>
<span data-ttu-id="c45a4-236">Consultez [télécharger des données tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="c45a4-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="c45a4-237">Téléchargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="c45a4-237">Download files</span></span>
<span data-ttu-id="c45a4-238">Hello script suivant télécharge un bloc blob toohello le dossier actuel.</span><span class="sxs-lookup"><span data-stu-id="c45a4-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="c45a4-239">Avant d’exécuter le script hello, modifiez hello tooa répertoire où vous disposez des autorisations en écriture.</span><span class="sxs-lookup"><span data-stu-id="c45a4-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="c45a4-240">Fournir le nom de groupe de ressources hello et nom du cluster hello, vous pouvez utiliser hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="c45a4-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="c45a4-241">Supprimer des fichiers</span><span class="sxs-lookup"><span data-stu-id="c45a4-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="c45a4-242">Énumérer des fichiers</span><span class="sxs-lookup"><span data-stu-id="c45a4-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="c45a4-243">Exécution de requêtes Hive à l'aide d'un compte de stockage non défini</span><span class="sxs-lookup"><span data-stu-id="c45a4-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="c45a4-244">Cet exemple montre comment toolist un dossier à partir du compte de stockage qui n’est pas défini au cours de hello le processus de création.</span><span class="sxs-lookup"><span data-stu-id="c45a4-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="c45a4-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="c45a4-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="c45a4-246">Utiliser l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c45a4-246">Use Azure CLI</span></span>
<span data-ttu-id="c45a4-247">Utilisez hello suivant de commandes toolist hello dépendant de l’objet blob de commandes :</span><span class="sxs-lookup"><span data-stu-id="c45a4-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="c45a4-248">**Exemple d’utilisation de le tooupload CLI d’Azure un fichier**</span><span class="sxs-lookup"><span data-stu-id="c45a4-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c45a4-249">**Exemple d’utilisation de le toodownload CLI d’Azure un fichier**</span><span class="sxs-lookup"><span data-stu-id="c45a4-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c45a4-250">**Exemple d’utilisation de Azure CLI toodelete un fichier**</span><span class="sxs-lookup"><span data-stu-id="c45a4-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c45a4-251">**Exemple d’utilisation de fichiers de toolist CLI d’Azure**</span><span class="sxs-lookup"><span data-stu-id="c45a4-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="c45a4-252">Utiliser des comptes de stockage supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c45a4-252">Use additional storage accounts</span></span>

<span data-ttu-id="c45a4-253">Lors de la création d’un cluster HDInsight, vous permet de spécifier hello Azure Storage compte tooassociate avec lui.</span><span class="sxs-lookup"><span data-stu-id="c45a4-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="c45a4-254">En outre toothis compte de stockage, vous pouvez ajouter plu les comptes de stockage à partir de hello même abonnement Azure ou différents abonnements Azure pendant le processus de création de hello ou après la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="c45a4-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="c45a4-255">Pour en savoir plus sur l'ajout de comptes de stockage supplémentaires, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c45a4-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="c45a4-256">À l’aide d’un compte de stockage supplémentaire dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c45a4-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c45a4-257">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c45a4-257">Next steps</span></span>
<span data-ttu-id="c45a4-258">Dans cet article, vous avez appris comment toouse HDFS compatible avec le stockage Azure avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c45a4-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="c45a4-259">Cela vous permet de toobuild évolutive et à long terme, l’archivage des solutions d’acquisition de données et l’utilisation de HDInsight toounlock hello plus d’informations à l’intérieur de stockée hello structurées et les données non structurées.</span><span class="sxs-lookup"><span data-stu-id="c45a4-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="c45a4-260">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="c45a4-260">For more information, see:</span></span>

* <span data-ttu-id="c45a4-261">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c45a4-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="c45a4-262">Prise en main d’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c45a4-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="c45a4-263">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c45a4-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c45a4-264">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c45a4-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c45a4-265">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c45a4-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c45a4-266">[Utiliser des Signatures d’accès partagé Azure Storage toorestrict accès toodata avec HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="c45a4-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
