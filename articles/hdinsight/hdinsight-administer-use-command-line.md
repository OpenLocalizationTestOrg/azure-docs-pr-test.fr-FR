---
title: "Gestion des clusters Hadoop à l’aide de l’interface CLI Azure - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment utiliser l’interface de ligne de commande Azure pour gérer des clusters Hadoop dans Azure HDInsight. Azure CLI fonctionne sur Windows, Mac et Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="7dd57-104">Gestion des clusters Hadoop dans HDInsight à l'aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="7dd57-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="7dd57-105">Apprenez à utiliser [l'interface de ligne de commande Azure](../cli-install-nodejs.md) afin de gérer des clusters Hadoop dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dd57-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="7dd57-106">L’interface de ligne de commande Azure est implémentée dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="7dd57-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="7dd57-107">Elle peut être utilisée sur toute plateforme prenant en charge Node.js, y compris Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="7dd57-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="7dd57-108">Cet article aborde uniquement l’utilisation de l’interface de ligne de commande Azure dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dd57-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="7dd57-109">Pour une aide générale sur l’utilisation de l’interface Azure CLI, consultez la rubrique [Installer et configurer l’interface Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="7dd57-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="7dd57-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7dd57-110">Prerequisites</span></span>
<span data-ttu-id="7dd57-111">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7dd57-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="7dd57-112">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="7dd57-112">**An Azure subscription**.</span></span> <span data-ttu-id="7dd57-113">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7dd57-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7dd57-114">**Azure CLI** - Consultez la rubrique [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md) pour obtenir des informations sur l’installation et la configuration.</span><span class="sxs-lookup"><span data-stu-id="7dd57-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="7dd57-115">**Connectez-vous à Azure**en utilisant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7dd57-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="7dd57-116">Pour plus d’informations sur l’authentification à l’aide d’un compte professionnel ou scolaire, consultez la section [Se connecter à un abonnement Azure à partir de l’interface de ligne de commande Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7dd57-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="7dd57-117">**Passez en mode Azure Resource Manager**en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7dd57-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="7dd57-118">Pour obtenir de l’aide, utilisez le commutateur **-h** .</span><span class="sxs-lookup"><span data-stu-id="7dd57-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="7dd57-119">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7dd57-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="7dd57-120">Créer des clusters avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7dd57-120">Create clusters with the CLI</span></span>
<span data-ttu-id="7dd57-121">Voir [Créer des clusters dans HDInsight à l’aide d’Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7dd57-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="7dd57-122">Énumération et affichage des détails de cluster</span><span class="sxs-lookup"><span data-stu-id="7dd57-122">List and show cluster details</span></span>
<span data-ttu-id="7dd57-123">Utilisez les commandes suivantes pour énumérer et afficher les détails de cluster :</span><span class="sxs-lookup"><span data-stu-id="7dd57-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="7dd57-124">![Vue de ligne de commande de la liste de clusters][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="7dd57-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="7dd57-125">Suppression des clusters</span><span class="sxs-lookup"><span data-stu-id="7dd57-125">Delete clusters</span></span>
<span data-ttu-id="7dd57-126">Utilisez la commande suivante pour supprimer un cluster :</span><span class="sxs-lookup"><span data-stu-id="7dd57-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="7dd57-127">Vous pouvez également supprimer un cluster en supprimant le groupe de ressources qui le contient.</span><span class="sxs-lookup"><span data-stu-id="7dd57-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="7dd57-128">Notez que cette opération supprime toutes les ressources dans le groupe, notamment le compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="7dd57-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="7dd57-129">Mise à l’échelle des clusters</span><span class="sxs-lookup"><span data-stu-id="7dd57-129">Scale clusters</span></span>
<span data-ttu-id="7dd57-130">Pour modifier la taille du cluster Hadoop :</span><span class="sxs-lookup"><span data-stu-id="7dd57-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="7dd57-131">Activer / désactiver l’accès HTTP pour un cluster</span><span class="sxs-lookup"><span data-stu-id="7dd57-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="7dd57-132">Activer / désactiver l’accès RDP pour un cluster</span><span class="sxs-lookup"><span data-stu-id="7dd57-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="7dd57-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7dd57-133">Next steps</span></span>
<span data-ttu-id="7dd57-134">Dans cet article, vous avez appris comment effectuer différentes tâches d'administration sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dd57-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="7dd57-135">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7dd57-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="7dd57-136">[Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="7dd57-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="7dd57-137">[Administration de HDInsight à l'aide d'Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="7dd57-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="7dd57-138">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7dd57-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="7dd57-139">[Utilisation de l’interface de ligne de commande Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="7dd57-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Énumération et affichage des clusters"
