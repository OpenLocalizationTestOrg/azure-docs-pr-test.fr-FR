---
title: "Suppression d’un cluster HDInsight - Azure | Microsoft Docs"
description: "Informations sur les différentes méthodes que vous pouvez utiliser pour supprimer un cluster HDInsight."
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
ms.openlocfilehash: 65dac529df15d2dd43eec17673d82a2832f7692e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="67795-103">Suppression d’un cluster HDInsight à l’aide de votre navigateur, PowerShell ou l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="67795-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="67795-104">La facturation du cluster HDInsight démarre à la création du cluster et s’arrête à sa suppression.</span><span class="sxs-lookup"><span data-stu-id="67795-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="67795-105">La facturation est effectuée au prorata des minutes écoulées. Par conséquent, vous devez toujours supprimer votre cluster lorsqu’il n’est plus utilisé.</span><span class="sxs-lookup"><span data-stu-id="67795-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="67795-106">Dans ce document, vous découvrirez comment supprimer un cluster à l’aide du portail Azure, d’Azure PowerShell et de l’interface de ligne de commande (CLI) Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="67795-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67795-107">La suppression d’un cluster HDInsight ne supprime pas les comptes de stockage Azure ou le Data Lake Store associés au cluster.</span><span class="sxs-lookup"><span data-stu-id="67795-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="67795-108">Vous pouvez réutiliser les données stockées dans ces services à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="67795-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="67795-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="67795-109">Azure portal</span></span>

1. <span data-ttu-id="67795-110">Connectez-vous au [portail Azure](https://portal.azure.com) et sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67795-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="67795-111">Si votre cluster HDInsight n’est pas épinglé au tableau de bord, vous pouvez le rechercher par son nom dans le champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="67795-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![recherche dans le portail](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="67795-113">Lorsque le panneau s’ouvre pour le cluster, sélectionnez l’icône **Supprimer** .</span><span class="sxs-lookup"><span data-stu-id="67795-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="67795-114">Lorsque vous y êtes invité, sélectionnez **Oui** pour supprimer le cluster.</span><span class="sxs-lookup"><span data-stu-id="67795-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![icône Supprimer](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="67795-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="67795-116">Azure PowerShell</span></span>

<span data-ttu-id="67795-117">À partir d’une invite PowerShell, utilisez la commande suivante pour supprimer le cluster :</span><span class="sxs-lookup"><span data-stu-id="67795-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="67795-118">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67795-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="67795-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="67795-119">Azure CLI 1.0</span></span>

<span data-ttu-id="67795-120">À partir d’une invite, utilisez la commande suivante pour supprimer le cluster :</span><span class="sxs-lookup"><span data-stu-id="67795-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="67795-121">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67795-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="67795-122">Azure CLI 2.0 ne prend pas en charge la suppression des clusters HDInsight pour l’instant (31 juillet 2017).</span><span class="sxs-lookup"><span data-stu-id="67795-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>