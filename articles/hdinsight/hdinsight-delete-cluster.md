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
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Supprimer un cluster HDInsight à l’aide de votre navigateur, PowerShell ou hello CLI d’Azure

Cluster HDInsight facturation démarre une fois qu’un cluster est créé et s’arrête lorsque le cluster de hello est supprimé. La facturation est effectuée au prorata des minutes écoulées. Par conséquent, vous devez toujours supprimer votre cluster lorsqu’il n’est plus utilisé. Dans ce document, vous découvrez comment un cluster à l’aide de toodelete hello portail Azure, Azure PowerShell et hello Azure CLI 1.0.

> [!IMPORTANT]
> La suppression d’un cluster HDInsight ne supprime pas les comptes de stockage Azure hello ou Data Lake Store associées au cluster de hello. Vous pouvez réutiliser les données stockées dans ces services Bonjour futures.

## <a name="azure-portal"></a>Portail Azure

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) et sélectionnez votre cluster HDInsight. Si votre cluster HDInsight n’est pas épinglé toohello le tableau de bord, vous pouvez rechercher pour celle-ci par nom à l’aide du champ de recherche hello.
   
    ![recherche dans le portail](./media/hdinsight-delete-cluster/navbar.png)

2. Une fois que le panneau de hello s’ouvre pour le cluster de hello, sélectionnez hello **supprimer** icône. Lorsque vous y êtes invité, sélectionnez **Oui** cluster hello de toodelete.
   
    ![icône Supprimer](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

À partir d’une invite de PowerShell, utilisez hello suivant du cluster de commande toodelete hello :

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.

## <a name="azure-cli-10"></a>Azure CLI 1.0

À partir d’une invite de commandes, utilisez hello suivant du cluster de hello toodelete :

    azure hdinsight cluster delete CLUSTERNAME

Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.

> [!NOTE]
> Azure CLI 2.0 ne prend pas en charge la suppression des clusters HDInsight pour l’instant (31 juillet 2017).