---
title: aaaHow toodelete un cluster HDInsight - Azure | Documents Microsoft
description: "Plus d’informations sur les différentes méthodes que vous pouvez supprimer un cluster HDInsight de hello."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="db836-103">Supprimer un cluster HDInsight à l’aide de votre navigateur, PowerShell ou hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="db836-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="db836-104">Cluster HDInsight facturation démarre une fois qu’un cluster est créé et s’arrête lorsque le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="db836-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="db836-105">La facturation est effectuée au prorata des minutes écoulées. Par conséquent, vous devez toujours supprimer votre cluster lorsqu’il n’est plus utilisé.</span><span class="sxs-lookup"><span data-stu-id="db836-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="db836-106">Dans ce document, vous découvrez comment un cluster à l’aide de toodelete hello portail Azure, Azure PowerShell et hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="db836-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db836-107">La suppression d’un cluster HDInsight ne supprime pas les comptes de stockage Azure hello ou Data Lake Store associées au cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="db836-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="db836-108">Vous pouvez réutiliser les données stockées dans ces services Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="db836-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="db836-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="db836-109">Azure portal</span></span>

1. <span data-ttu-id="db836-110">Connectez-vous à toohello [portail Azure](https://portal.azure.com) et sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="db836-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="db836-111">Si votre cluster HDInsight n’est pas épinglé toohello le tableau de bord, vous pouvez rechercher pour celle-ci par nom à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="db836-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![recherche dans le portail](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="db836-113">Une fois que le panneau de hello s’ouvre pour le cluster de hello, sélectionnez hello **supprimer** icône.</span><span class="sxs-lookup"><span data-stu-id="db836-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="db836-114">Lorsque vous y êtes invité, sélectionnez **Oui** cluster hello de toodelete.</span><span class="sxs-lookup"><span data-stu-id="db836-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![icône Supprimer](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="db836-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="db836-116">Azure PowerShell</span></span>

<span data-ttu-id="db836-117">À partir d’une invite de PowerShell, utilisez hello suivant du cluster de commande toodelete hello :</span><span class="sxs-lookup"><span data-stu-id="db836-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="db836-118">Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="db836-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="db836-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="db836-119">Azure CLI 1.0</span></span>

<span data-ttu-id="db836-120">À partir d’une invite de commandes, utilisez hello suivant du cluster de hello toodelete :</span><span class="sxs-lookup"><span data-stu-id="db836-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="db836-121">Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="db836-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="db836-122">Azure CLI 2.0 ne prend pas en charge la suppression des clusters HDInsight pour l’instant (31 juillet 2017).</span><span class="sxs-lookup"><span data-stu-id="db836-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>