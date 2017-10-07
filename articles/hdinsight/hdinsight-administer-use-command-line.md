---
title: "aaaManage Hadoop clusters à l’aide d’Azure HDInsight - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Interface de ligne de commande Azure toomanage Hadoop clusters dans Azure HDInsight. Hello CLI d’Azure fonctionne sous Windows, Mac et Linux."
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
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="c7cac-104">Gérer les clusters Hadoop dans HDInsight à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="c7cac-105">Découvrez comment toouse hello [Interface de ligne de commande Azure](../cli-install-nodejs.md) toomanage Hadoop de clusters dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7cac-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="c7cac-106">Hello CLI d’Azure est implémenté dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="c7cac-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="c7cac-107">Elle peut être utilisée sur toute plateforme prenant en charge Node.js, y compris Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="c7cac-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="c7cac-108">Cet article couvre uniquement l’utilisation hello CLI d’Azure avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7cac-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="c7cac-109">Pour obtenir un guide général sur la façon de toouse CLI d’Azure, consultez [installer et configurer Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="c7cac-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="c7cac-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c7cac-110">Prerequisites</span></span>
<span data-ttu-id="c7cac-111">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="c7cac-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="c7cac-112">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-112">**An Azure subscription**.</span></span> <span data-ttu-id="c7cac-113">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c7cac-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c7cac-114">**CLI Azure** -consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) pour plus d’informations d’installation et de configuration.</span><span class="sxs-lookup"><span data-stu-id="c7cac-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="c7cac-115">**Se connecter tooAzure**, à l’aide hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7cac-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="c7cac-116">Pour plus d’informations sur l’authentification à l’aide d’un compte professionnel ou scolaire, consultez [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c7cac-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="c7cac-117">**Passez en mode Azure Resource Manager de toohello**, à l’aide hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7cac-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="c7cac-118">tooget help, utilisez hello **-h** basculer.</span><span class="sxs-lookup"><span data-stu-id="c7cac-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="c7cac-119">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c7cac-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="c7cac-120">Créer des clusters avec hello CLI</span><span class="sxs-lookup"><span data-stu-id="c7cac-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="c7cac-121">Consultez [créer des clusters HDInsight à l’aide hello CLI d’Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c7cac-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="c7cac-122">Énumération et affichage des détails de cluster</span><span class="sxs-lookup"><span data-stu-id="c7cac-122">List and show cluster details</span></span>
<span data-ttu-id="c7cac-123">Utilisez hello suivant toolist de commandes et afficher les détails du cluster :</span><span class="sxs-lookup"><span data-stu-id="c7cac-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="c7cac-124">![Vue de ligne de commande de la liste de clusters][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="c7cac-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="c7cac-125">Suppression des clusters</span><span class="sxs-lookup"><span data-stu-id="c7cac-125">Delete clusters</span></span>
<span data-ttu-id="c7cac-126">Utilisez hello suivant commande toodelete un cluster :</span><span class="sxs-lookup"><span data-stu-id="c7cac-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="c7cac-127">Vous pouvez également supprimer un cluster par la suppression du groupe de ressources hello contient hello cluster.</span><span class="sxs-lookup"><span data-stu-id="c7cac-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="c7cac-128">Notez cette opération supprimera toutes les ressources hello groupe hello, y compris le compte de stockage par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="c7cac-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="c7cac-129">Mise à l’échelle des clusters</span><span class="sxs-lookup"><span data-stu-id="c7cac-129">Scale clusters</span></span>
<span data-ttu-id="c7cac-130">hello toochange taille de cluster Hadoop :</span><span class="sxs-lookup"><span data-stu-id="c7cac-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="c7cac-131">Activer / désactiver l’accès HTTP pour un cluster</span><span class="sxs-lookup"><span data-stu-id="c7cac-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="c7cac-132">Activer / désactiver l’accès RDP pour un cluster</span><span class="sxs-lookup"><span data-stu-id="c7cac-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="c7cac-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7cac-133">Next steps</span></span>
<span data-ttu-id="c7cac-134">Dans cet article, vous avez appris comment tooperform HDInsight cluster tâches administratives.</span><span class="sxs-lookup"><span data-stu-id="c7cac-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="c7cac-135">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="c7cac-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c7cac-136">[Administrer HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="c7cac-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="c7cac-137">[Administration de HDInsight à l'aide d'Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="c7cac-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="c7cac-138">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c7cac-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c7cac-139">[Comment toouse hello CLI d’Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="c7cac-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

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
