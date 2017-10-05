---
title: "Créer un cluster Hadoop à l’aide de comptes de stockage avec transfert sécurisé dans Azure HDInsight | Microsoft Docs"
description: "Découvrez comment créer des clusters HDInsight à l’aide de comptes de stockage Azure doté du transfert sécurisé."
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
ms.openlocfilehash: 370b2f081930fe88527436a1a127309aed6681f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="01ee2-104">Créer un cluster Hadoop à l’aide de comptes de stockage avec transfert sécurisé dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="01ee2-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="01ee2-105">La fonctionnalité [Transfert sécurisé requis](../storage/common/storage-require-secure-transfer.md) améliore la sécurité de votre compte de stockage Azure en appliquant toutes les demandes à votre compte via une connexion sécurisée.</span><span class="sxs-lookup"><span data-stu-id="01ee2-105">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span></span> <span data-ttu-id="01ee2-106">Cette fonctionnalité et le schéma wasbs sont uniquement pris en charge par les clusters HDInsight 3.6 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="01ee2-106">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="01ee2-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="01ee2-107">Prerequisites</span></span>
<span data-ttu-id="01ee2-108">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="01ee2-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="01ee2-109">**Abonnement Azure**: pour créer un compte d’essai gratuit d’une durée d’un mois, accédez à [azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="01ee2-109">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="01ee2-110">**Un compte de stockage Azure doté du transfert sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="01ee2-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="01ee2-111">Pour obtenir des instructions, consultez [Créez un compte de stockage.](../storage/common/storage-create-storage-account.md#create-a-storage-account) et [Exiger un transfert sécurisé](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-111">For the instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="01ee2-112">**Un conteneur d’objets blob dans le compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="01ee2-112">**A Blob container on the storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="01ee2-113">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="01ee2-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="01ee2-114">Cette section vous permet de créer un cluster Hadoop dans HDInsight à l’aide d’un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="01ee2-115">Ce modèle se trouve sur [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="01ee2-115">The template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="01ee2-116">Aucune expérience avec le modèle Resource Manager n’est requise pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="01ee2-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="01ee2-117">Pour obtenir d’autres méthodes de création de cluster et comprendre les propriétés utilisées dans ce didacticiel, consultez [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-117">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="01ee2-118">Cliquez sur l’image suivante pour vous connecter à Azure et ouvrir le modèle Resource Manager dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="01ee2-118">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="01ee2-119">Suivez les instructions pour créer le cluster avec les spécifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="01ee2-119">Follow the instructions to create the cluster with the following specifications:</span></span> 

    - <span data-ttu-id="01ee2-120">Indiquez HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="01ee2-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="01ee2-121">La version par défaut est 3.5.</span><span class="sxs-lookup"><span data-stu-id="01ee2-121">The default version is 3.5.</span></span> <span data-ttu-id="01ee2-122">La version 3.6 ou une version ultérieure est requise.</span><span class="sxs-lookup"><span data-stu-id="01ee2-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="01ee2-123">Indiquez un compte de stockage doté du transfert sécurisé.</span><span class="sxs-lookup"><span data-stu-id="01ee2-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="01ee2-124">Utilisez un nom court pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="01ee2-124">Use short name for the storage account.</span></span>
    - <span data-ttu-id="01ee2-125">Le compte de stockage et le conteneur d’objets blob doivent être créés au préalable.</span><span class="sxs-lookup"><span data-stu-id="01ee2-125">Both the storage account and the blob container must be created beforehand.</span></span> 

    <span data-ttu-id="01ee2-126">Pour obtenir des instructions, consultez [Créer un cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="01ee2-126">For the instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="01ee2-127">Si vous utilisez l’action de script pour fournir vos propres fichiers de configuration, vous devez utiliser wasbs dans les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="01ee2-127">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span></span>

- <span data-ttu-id="01ee2-128">fs.defaultFS (site principal)</span><span class="sxs-lookup"><span data-stu-id="01ee2-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="01ee2-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="01ee2-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="01ee2-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="01ee2-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="01ee2-131">Ajouter des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="01ee2-131">Add additional storage accounts</span></span>

<span data-ttu-id="01ee2-132">Plusieurs options vous permettent d’ajouter des comptes de stockage dotés du transfert sécurisé :</span><span class="sxs-lookup"><span data-stu-id="01ee2-132">There are several options to add additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="01ee2-133">Modifiez le modèle Azure Resource Manager dans la dernière section.</span><span class="sxs-lookup"><span data-stu-id="01ee2-133">Modify the Azure Resource Manager template in the last section.</span></span>
- <span data-ttu-id="01ee2-134">Créez un cluster à l’aide du [portail Azure](https://portal.azure.com) et indiquez le compte de stockage lié.</span><span class="sxs-lookup"><span data-stu-id="01ee2-134">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="01ee2-135">Utilisez l’action de script pour ajouter des comptes de stockage doté du transfert sécurisé à un cluster HDInsight existant.</span><span class="sxs-lookup"><span data-stu-id="01ee2-135">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span></span>  <span data-ttu-id="01ee2-136">Pour plus d’informations, consultez [Ajouter des comptes de stockage supplémentaires à HDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-136">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01ee2-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01ee2-137">Next steps</span></span>
<span data-ttu-id="01ee2-138">Dans ce didacticiel, vous avez appris à créer un cluster HDInsight et à activer le transfert sécurisé pour les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="01ee2-138">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span></span>

<span data-ttu-id="01ee2-139">Pour en savoir plus sur l’analyse des données avec HDInsight, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="01ee2-139">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="01ee2-140">Pour en savoir plus sur l’utilisation de Hive avec HDInsight, y compris comment exécuter des requêtes Hive à partir de Visual Studio, consultez la page [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="01ee2-140">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="01ee2-141">Pour en savoir plus sur Pig, un langage utilisé pour transformer les données, consultez la page [Utilisation de Pig avec HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="01ee2-141">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="01ee2-142">Pour en savoir plus sur MapReduce, un moyen d’écrire des programmes pour traiter les données sur Hadoop, consultez la page [Utilisation de MapReduce avec HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="01ee2-142">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="01ee2-143">Pour en savoir plus sur l’utilisation des outils HDInsight pour Visual Studio pour analyser les données sur HDInsight, consultez la page [Prise en main des outils Hadoop de Visual Studio pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-143">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="01ee2-144">Pour plus d’informations sur la façon dont HDInsight stocke les données ou sur la façon d’obtenir des données dans HDInsight, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="01ee2-144">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="01ee2-145">Pour plus d’informations sur la façon dont HDInsight utilise le stockage Azure, consultez la page [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md) (Utilisation du stockage Azure avec HDInsight).</span><span class="sxs-lookup"><span data-stu-id="01ee2-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="01ee2-146">Pour plus d’informations sur le téléchargement de données dans HDInsight, consultez la page [Téléchargement de données dans HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="01ee2-146">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="01ee2-147">Pour en savoir plus sur la création ou la gestion d’un cluster HDInsight, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="01ee2-147">To learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="01ee2-148">Pour en savoir plus sur la gestion de votre cluster HDInsight Linux, consultez la page [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-148">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="01ee2-149">Pour en savoir plus sur les options que vous pouvez sélectionner pendant la création d’un cluster HDInsight, consultez la page [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-149">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="01ee2-150">Si vous maîtrisez Linux et Hadoop, mais que vous souhaitez connaître les spécificités de Hadoop sur HDInsight, consultez la page [Utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="01ee2-150">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="01ee2-151">Cet article vous fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="01ee2-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="01ee2-152">les URL correspondant aux services hébergés sur le cluster, tels qu'Ambari et WebHCat</span><span class="sxs-lookup"><span data-stu-id="01ee2-152">URLs for services hosted on the cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="01ee2-153">l'emplacement des fichiers Hadoop et des exemples sur le système de fichiers local</span><span class="sxs-lookup"><span data-stu-id="01ee2-153">The location of Hadoop files and examples on the local file system</span></span>
  * <span data-ttu-id="01ee2-154">l'utilisation de stockage d'Azure Storage (WASB) au lieu de HDFS, en tant que stockage de données par défaut</span><span class="sxs-lookup"><span data-stu-id="01ee2-154">The use of Azure Storage (WASB) instead of HDFS as the default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


