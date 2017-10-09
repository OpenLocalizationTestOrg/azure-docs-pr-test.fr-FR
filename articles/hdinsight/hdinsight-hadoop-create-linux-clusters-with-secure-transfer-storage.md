---
title: "aaaCreate Hadoop de cluster avec les comptes de stockage d’un transfert sécurisé dans Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les clusters HDInsight de toocreate avec un transfert sécurisé activé les comptes de stockage Azure."
keywords: "prise en main hadoop, hadoop linux, démarrage rapide hadoop, transfert sécurisé, compte de stockage azure"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="90cdb-104">Créer un cluster Hadoop à l’aide de comptes de stockage avec transfert sécurisé dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="90cdb-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="90cdb-105">Hello [sécuriser le transfert requis](../storage/common/storage-require-secure-transfer.md) fonctionnalité améliore la sécurité de hello de votre compte de stockage Azure en appliquant le compte de tooyour toutes les demandes via une connexion sécurisée.</span><span class="sxs-lookup"><span data-stu-id="90cdb-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="90cdb-106">Cette fonctionnalité et hello wasbs schéma sont uniquement pris en charge par la version du cluster HDInsight 3.6 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="90cdb-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="90cdb-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="90cdb-107">Prerequisites</span></span>
<span data-ttu-id="90cdb-108">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="90cdb-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="90cdb-109">**Abonnement Azure**: toocreate un compte d’essai un mois gratuit, parcourir trop[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="90cdb-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="90cdb-110">**Un compte de stockage Azure doté du transfert sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="90cdb-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="90cdb-111">Pour obtenir des instructions de hello, consultez [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) et [requièrent un transfert sécurisé](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="90cdb-112">**Un conteneur d’objets Blob sur le compte de stockage hello**.</span><span class="sxs-lookup"><span data-stu-id="90cdb-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="90cdb-113">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="90cdb-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="90cdb-114">Cette section vous permet de créer un cluster Hadoop dans HDInsight à l’aide d’un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="90cdb-115">Hello modèle se trouve dans [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="90cdb-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="90cdb-116">Aucune expérience avec le modèle Resource Manager n’est requise pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="90cdb-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="90cdb-117">Pour d’autres méthodes de création de cluster et les propriétés hello utilisées dans ce didacticiel, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="90cdb-118">Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="90cdb-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="90cdb-119">Procédez comme cluster de hello hello instructions toocreate avec hello conformément aux spécifications :</span><span class="sxs-lookup"><span data-stu-id="90cdb-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="90cdb-120">Indiquez HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="90cdb-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="90cdb-121">version par défaut de Hello est 3.5.</span><span class="sxs-lookup"><span data-stu-id="90cdb-121">hello default version is 3.5.</span></span> <span data-ttu-id="90cdb-122">La version 3.6 ou une version ultérieure est requise.</span><span class="sxs-lookup"><span data-stu-id="90cdb-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="90cdb-123">Indiquez un compte de stockage doté du transfert sécurisé.</span><span class="sxs-lookup"><span data-stu-id="90cdb-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="90cdb-124">Utilisez le nom court pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="90cdb-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="90cdb-125">Compte de stockage hello et conteneur d’objets blob hello doivent être créés au préalable.</span><span class="sxs-lookup"><span data-stu-id="90cdb-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="90cdb-126">Pour obtenir des instructions de hello, consultez [créer un cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="90cdb-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="90cdb-127">Si vous utilisez le script action tooprovide vos propres fichiers de configuration, vous devez utiliser wasbs Bonjour suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="90cdb-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="90cdb-128">fs.defaultFS (site principal)</span><span class="sxs-lookup"><span data-stu-id="90cdb-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="90cdb-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="90cdb-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="90cdb-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="90cdb-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="90cdb-131">Ajouter des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="90cdb-131">Add additional storage accounts</span></span>

<span data-ttu-id="90cdb-132">Il existe plusieurs comptes de stockage supplémentaires transfert sécurisé activé tooadd options :</span><span class="sxs-lookup"><span data-stu-id="90cdb-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="90cdb-133">Modifier le modèle de gestionnaire de ressources Azure hello dans la dernière section de hello.</span><span class="sxs-lookup"><span data-stu-id="90cdb-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="90cdb-134">Créer un cluster à l’aide de hello [portail Azure](https://portal.azure.com) et spécifiez le compte de stockage lié.</span><span class="sxs-lookup"><span data-stu-id="90cdb-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="90cdb-135">Utilisez script action tooadd supplémentaire transfert sécurisé activé cluster HDInsight existant de stockage comptes tooan.</span><span class="sxs-lookup"><span data-stu-id="90cdb-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="90cdb-136">Pour plus d’informations, consultez [ajouter tooHDInsight des comptes de stockage supplémentaire](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90cdb-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90cdb-137">Next steps</span></span>
<span data-ttu-id="90cdb-138">Dans ce didacticiel, vous avez appris comment toocreate un cluster HDInsight et activer sécurisé de transfert toohello les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="90cdb-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="90cdb-139">toolearn en savoir plus sur l’analyse de données avec HDInsight, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="90cdb-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="90cdb-140">toolearn savoir plus sur l’utilisation de la ruche avec HDInsight, y compris le fonctionnement des requêtes tooperform Hive à partir de Visual Studio, consultez [utilisez Hive hdinsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="90cdb-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="90cdb-141">toolearn sur Pig, un langage tootransform données, consultez [utilisez Pig hdinsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="90cdb-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="90cdb-142">toolearn sur MapReduce, une façon dont les programmes toowrite qui traitent les données sur Hadoop, consultez [MapReduce utilisation hdinsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="90cdb-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="90cdb-143">toolearn sur l’utilisation des outils HDInsight de hello pour les données de tooanalyze de Visual Studio sur HDInsight, consultez [prise en main des outils de Visual Studio Hadoop pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="90cdb-144">toolearn plus en détail comment HDInsight stocke les données ou les données tooget dans HDInsight, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="90cdb-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="90cdb-145">Pour plus d’informations sur la façon dont HDInsight utilise le stockage Azure, consultez la page [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md) (Utilisation du stockage Azure avec HDInsight).</span><span class="sxs-lookup"><span data-stu-id="90cdb-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="90cdb-146">Pour plus d’informations sur la façon de tooupload tooHDInsight de données, consultez [télécharger des données tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="90cdb-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="90cdb-147">toolearn en savoir plus sur la création ou de gestion d’un cluster HDInsight, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="90cdb-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="90cdb-148">toolearn sur la gestion de votre cluster HDInsight de basés sur Linux, consultez [HDInsight de gérer des clusters à l’aide de Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="90cdb-149">toolearn savoir plus sur les options de hello vous pouvez sélectionner lors de la création d’un cluster HDInsight, consultez [création de HDInsight sur Linux à l’aide des options personnalisées](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="90cdb-150">Si vous êtes familiarisé avec Linux et Hadoop, mais tooknow spécificités Hadoop sur hello HDInsight, consultez [utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="90cdb-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="90cdb-151">Cet article vous fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="90cdb-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="90cdb-152">URL pour les services hébergés sur le cluster hello, telles que Ambari et WebHCat</span><span class="sxs-lookup"><span data-stu-id="90cdb-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="90cdb-153">emplacement des fichiers de Hadoop et des exemples sur le système de fichiers local hello de Hello</span><span class="sxs-lookup"><span data-stu-id="90cdb-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="90cdb-154">utilisation de Hello d’Azure Storage (WASB) au lieu de HDFS en tant que banque de données par défaut hello</span><span class="sxs-lookup"><span data-stu-id="90cdb-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


