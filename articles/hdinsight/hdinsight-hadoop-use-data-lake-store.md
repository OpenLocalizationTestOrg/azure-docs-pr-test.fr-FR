---
title: aaaUse Data Lake Store avec Hadoop dans HDInsight de Azure | Documents Microsoft
description: "Découvrez comment tooquery des données à partir d’Azure Data Lake Store et toostore des résultats de votre analyse."
keywords: "stockage d’objets blob, hdfs, données structurées, données non structurées, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="87347-104">Utiliser Data Lake Store avec des clusters Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="87347-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="87347-105">tooanalyze des données dans le cluster HDInsight, vous pouvez stocker les données de salutation soit dans [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), ou les deux.</span><span class="sxs-lookup"><span data-stu-id="87347-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="87347-106">Les deux options de stockage permettent de supprimer toosafely que des clusters HDInsight qui sont utilisés pour le calcul sans perdre de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="87347-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="87347-107">Dans cet article, vous découvrez le fonctionnement de Data Lake Store avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87347-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="87347-108">toolearn comment le stockage Azure fonctionne avec les clusters HDInsight, consultez [utiliser le stockage Azure avec Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="87347-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="87347-109">Consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87347-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="87347-110">Data Lake Store est toujours accessible par le biais d’un canal sécurisé, donc il y a aucun nom de schéma de système de fichiers `adls`.</span><span class="sxs-lookup"><span data-stu-id="87347-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="87347-111">Vous utilisez toujours `adl`.</span><span class="sxs-lookup"><span data-stu-id="87347-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="87347-112">Disponibilités pour les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="87347-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="87347-113">Hadoop prend en charge une notion hello par défaut du système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="87347-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="87347-114">système de fichiers par défaut Hello implique un schéma par défaut et une autorité.</span><span class="sxs-lookup"><span data-stu-id="87347-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="87347-115">Il peut également être tooresolve utilisé des chemins d’accès relatifs.</span><span class="sxs-lookup"><span data-stu-id="87347-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="87347-116">Pendant le processus de création de cluster HDInsight de hello, vous pouvez spécifier un conteneur d’objets blob dans le stockage Azure en tant que système de fichiers par défaut hello ou avec HDInsight 3.5 et les versions plus récentes, vous pouvez sélectionner le stockage Azure ou Azure Data Lake Store en tant que système de fichiers par défaut hello avec un quelques exceptions près.</span><span class="sxs-lookup"><span data-stu-id="87347-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="87347-117">Les clusters HDInsight peuvent utiliser Data Lake Store de deux manières :</span><span class="sxs-lookup"><span data-stu-id="87347-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="87347-118">En tant que stockage par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="87347-118">As hello default storage</span></span>
* <span data-ttu-id="87347-119">Comme stockage supplémentaire, avec Azure Storage Blob comme stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="87347-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="87347-120">À partir de maintenant, seules certaines hello HDInsight cluster prise en charge des types/versions à l’aide de Data Lake Store comme stockage par défaut et les comptes de stockage supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="87347-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="87347-121">Type de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="87347-121">HDInsight cluster type</span></span> | <span data-ttu-id="87347-122">Data Lake Store comme stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="87347-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="87347-123">Data Lake Store comme stockage supplémentaire</span><span class="sxs-lookup"><span data-stu-id="87347-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="87347-124">Remarques</span><span class="sxs-lookup"><span data-stu-id="87347-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="87347-125">HDInsight version 3.6</span><span class="sxs-lookup"><span data-stu-id="87347-125">HDInsight version 3.6</span></span> | <span data-ttu-id="87347-126">Oui</span><span class="sxs-lookup"><span data-stu-id="87347-126">Yes</span></span> | <span data-ttu-id="87347-127">Oui</span><span class="sxs-lookup"><span data-stu-id="87347-127">Yes</span></span> | |
| <span data-ttu-id="87347-128">HDInsight version 3.5</span><span class="sxs-lookup"><span data-stu-id="87347-128">HDInsight version 3.5</span></span> | <span data-ttu-id="87347-129">Oui</span><span class="sxs-lookup"><span data-stu-id="87347-129">Yes</span></span> | <span data-ttu-id="87347-130">Oui</span><span class="sxs-lookup"><span data-stu-id="87347-130">Yes</span></span> | <span data-ttu-id="87347-131">À l’exception de hello de HBase</span><span class="sxs-lookup"><span data-stu-id="87347-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="87347-132">HDInsight version 3.4</span><span class="sxs-lookup"><span data-stu-id="87347-132">HDInsight version 3.4</span></span> | <span data-ttu-id="87347-133">Non</span><span class="sxs-lookup"><span data-stu-id="87347-133">No</span></span> | <span data-ttu-id="87347-134">Oui</span><span class="sxs-lookup"><span data-stu-id="87347-134">Yes</span></span> | |
| <span data-ttu-id="87347-135">HDInsight version 3.3</span><span class="sxs-lookup"><span data-stu-id="87347-135">HDInsight version 3.3</span></span> | <span data-ttu-id="87347-136">Non</span><span class="sxs-lookup"><span data-stu-id="87347-136">No</span></span> | <span data-ttu-id="87347-137">Non</span><span class="sxs-lookup"><span data-stu-id="87347-137">No</span></span> | |
| <span data-ttu-id="87347-138">HDInsight version 3.2</span><span class="sxs-lookup"><span data-stu-id="87347-138">HDInsight version 3.2</span></span> | <span data-ttu-id="87347-139">Non</span><span class="sxs-lookup"><span data-stu-id="87347-139">No</span></span> | <span data-ttu-id="87347-140">Oui</span><span class="sxs-lookup"><span data-stu-id="87347-140">Yes</span></span> | |
| <span data-ttu-id="87347-141">HDInsight Premium (couche)</span><span class="sxs-lookup"><span data-stu-id="87347-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="87347-142">Non</span><span class="sxs-lookup"><span data-stu-id="87347-142">No</span></span> | <span data-ttu-id="87347-143">Non</span><span class="sxs-lookup"><span data-stu-id="87347-143">No</span></span> | |
| <span data-ttu-id="87347-144">Storm</span><span class="sxs-lookup"><span data-stu-id="87347-144">Storm</span></span> | | |<span data-ttu-id="87347-145">Vous pouvez utiliser les données de toowrite Data Lake Store à partir d’une topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="87347-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="87347-146">Vous pouvez également vous en servir pour stocker des données de référence qui peuvent ensuite être lues par une topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="87347-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="87347-147">À l’aide de Data Lake Store en tant qu’un compte de stockage supplémentaires ne pas affecter les performances ou hello capacité tooread ou d’écriture tooAzure stockage de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="87347-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="87347-148">Utiliser Data Lake Store comme stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="87347-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="87347-149">Lorsque HDInsight est déployé avec Data Lake Store en tant que stockage par défaut, fichiers hello cluster sont stockés dans Data Lake Store Bonjour à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="87347-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="87347-150">où `<cluster_root_path>` hello désigne un dossier que vous créez dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="87347-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="87347-151">En spécifiant un chemin d’accès racine pour chaque cluster, vous pouvez utiliser hello même compte Data Lake Store pour plusieurs clusters.</span><span class="sxs-lookup"><span data-stu-id="87347-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="87347-152">Par conséquent, vous pouvez avoir une configuration dans laquelle :</span><span class="sxs-lookup"><span data-stu-id="87347-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="87347-153">Cluster1 peut utiliser le chemin d’accès de hello`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="87347-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="87347-154">Cluster2 peut utiliser le chemin d’accès de hello`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="87347-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="87347-155">Notez que les deux hello clusters utilisez hello même compte Data Lake Store **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="87347-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="87347-156">Chaque cluster a accès tooits propre système de fichiers racine Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="87347-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="87347-157">Hello expérience de déploiement du portail Azure en particulier vous invite toouse un nom de dossier comme **/clusters/\<nom_cluster >** pour le chemin d’accès racine de hello.</span><span class="sxs-lookup"><span data-stu-id="87347-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="87347-158">toouse en mesure de toobe un Data Lake Store en tant que stockage par défaut, vous devez accorder hello service principal l’accès toohello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="87347-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="87347-159">racine de compte Data Lake Store Hello.</span><span class="sxs-lookup"><span data-stu-id="87347-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="87347-160">Par exemple : adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="87347-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="87347-161">dossier Hello pour tous les dossiers de cluster.</span><span class="sxs-lookup"><span data-stu-id="87347-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="87347-162">Par exemple : adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="87347-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="87347-163">dossier Hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="87347-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="87347-164">Par exemple : adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="87347-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="87347-165">Pour plus d’informations sur la création du principal de service et l’octroi de l’accès, consultez [Configure Data Lake store access](#configure-data-lake-store-access) (Configurer l’accès à Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="87347-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="87347-166">Utiliser Data Lake Store comme stockage supplémentaire</span><span class="sxs-lookup"><span data-stu-id="87347-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="87347-167">Vous pouvez utiliser Data Lake Store en tant que stockage supplémentaire pour le cluster hello.</span><span class="sxs-lookup"><span data-stu-id="87347-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="87347-168">Dans ce cas, du stockage par défaut hello cluster peut être un objet Blob de stockage Azure ou un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="87347-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="87347-169">Si vous exécutez les tâches HDInsight sur des données de hello stockées dans Data Lake Store en tant que stockage supplémentaire, vous devez utiliser des fichiers de toohello hello chemin qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="87347-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="87347-170">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="87347-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="87347-171">Notez qu’il existe aucune **cluster_root_path** dans l’URL de hello maintenant.</span><span class="sxs-lookup"><span data-stu-id="87347-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="87347-172">C’est parce que Data Lake Store n’est pas un stockage par défaut dans ce cas vous devez toodo fournissent des fichiers de toohello hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="87347-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="87347-173">toouse en mesure de toobe un Data Lake Store en tant que stockage supplémentaire, vous devez uniquement toogrant hello service principal toohello chemins d’accès où sont stockés vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="87347-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="87347-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="87347-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="87347-175">Pour plus d’informations sur la création du principal de service et l’octroi de l’accès, consultez [Configurer l’accès à Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="87347-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="87347-176">Utiliser plusieurs comptes Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="87347-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="87347-177">Ajout d’un compte Data Lake Store comme supplémentaires et Data Lake Store plusieurs comptes sont effectuées en offrant une autorisation de cluster HDInsight hello sur les données de comptes Data Lake Store d’une ou plusieurs.</span><span class="sxs-lookup"><span data-stu-id="87347-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="87347-178">Consultez [Configurer l’accès à Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="87347-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="87347-179">Configurer l’accès aux données Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="87347-179">Configure Data Lake store access</span></span>

<span data-ttu-id="87347-180">tooconfigure accès au magasin de LAC de données à partir de votre cluster HDInsight, vous devez disposer d’un principal du service Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87347-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="87347-181">Vous pouvez créer un principal de service uniquement si vous être administrateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87347-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="87347-182">principal du service Hello doit être créée avec un certificat.</span><span class="sxs-lookup"><span data-stu-id="87347-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="87347-183">Pour plus d’informations, consultez [Configurer l’accès à Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), et [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate) (Créer un principal du service avec un certificat auto-signé).</span><span class="sxs-lookup"><span data-stu-id="87347-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="87347-184">Si vous vous apprêtez toouse Azure Data Lake Store en tant que stockage supplémentaire pour le cluster HDInsight, nous vous recommandons vivement de procéder ainsi lorsque vous créez le cluster de hello comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="87347-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="87347-185">Ajout d’Azure Data Lake Store en tant que stockage supplémentaire tooan cluster HDInsight existant est un processus complexe et susceptible d’engendrer des tooerrors.</span><span class="sxs-lookup"><span data-stu-id="87347-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="87347-186">Accéder aux fichiers à partir du cluster de hello</span><span class="sxs-lookup"><span data-stu-id="87347-186">Access files from hello cluster</span></span>

<span data-ttu-id="87347-187">Il existe plusieurs méthodes que vous pouvez accéder à des fichiers hello Data Lake Store à partir d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87347-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="87347-188">**À l’aide du nom qualifié complet de hello**.</span><span class="sxs-lookup"><span data-stu-id="87347-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="87347-189">Avec cette approche, vous fournissez le fichier de toohello hello chemin d’accès complet que vous souhaitez tooaccess.</span><span class="sxs-lookup"><span data-stu-id="87347-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="87347-190">**À l’aide du format de chemin d’accès raccourcie hello**.</span><span class="sxs-lookup"><span data-stu-id="87347-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="87347-191">Avec cette approche, vous remplacez le chemin d’accès de hello jusqu'à la racine du cluster toohello avec adl : / / /.</span><span class="sxs-lookup"><span data-stu-id="87347-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="87347-192">Par conséquent, dans l’exemple hello ci-dessus, vous pouvez remplacer `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` avec `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="87347-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="87347-193">**À l’aide du chemin d’accès relatif de hello**.</span><span class="sxs-lookup"><span data-stu-id="87347-193">**Using hello relative path**.</span></span> <span data-ttu-id="87347-194">Avec cette approche, vous ne fournissez hello relatif au chemin toohello fichier que vous souhaitez tooaccess.</span><span class="sxs-lookup"><span data-stu-id="87347-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="87347-195">Par exemple, si le fichier toohello hello chemin d’accès complet est :</span><span class="sxs-lookup"><span data-stu-id="87347-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="87347-196">Vous pouvez accéder à hello même fichier exemple.log à l’aide de ce chemin d’accès relatif à la place.</span><span class="sxs-lookup"><span data-stu-id="87347-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="87347-197">Créer des clusters HDInsight avec accès tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="87347-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="87347-198">Utilisez hello suivant les liens pour obtenir des instructions détaillées sur comment toocreate des clusters HDInsight avec accès tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="87347-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="87347-199">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="87347-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="87347-200">Utilisation de PowerShell (avec Data Lake Store en tant que stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="87347-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="87347-201">Utilisation de PowerShell (avec Data Lake Store en tant que stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="87347-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="87347-202">Utilisation de modèles Azure</span><span class="sxs-lookup"><span data-stu-id="87347-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="87347-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87347-203">Next steps</span></span>
<span data-ttu-id="87347-204">Dans cet article, vous avez appris comment toouse HDFS compatibles avec Azure Data Lake Store avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87347-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="87347-205">Cela vous permet de toobuild évolutive et à long terme, l’archivage des solutions d’acquisition de données et l’utilisation de HDInsight toounlock hello plus d’informations à l’intérieur de stockée hello structurées et les données non structurées.</span><span class="sxs-lookup"><span data-stu-id="87347-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="87347-206">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="87347-206">For more information, see:</span></span>

* <span data-ttu-id="87347-207">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="87347-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="87347-208">Prise en main d’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="87347-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="87347-209">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="87347-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="87347-210">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="87347-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="87347-211">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="87347-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="87347-212">[Utiliser des Signatures d’accès partagé Azure Storage toorestrict accès toodata avec HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="87347-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
