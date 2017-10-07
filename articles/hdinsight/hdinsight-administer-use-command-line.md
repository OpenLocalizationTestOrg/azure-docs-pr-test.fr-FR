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
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Gérer les clusters Hadoop dans HDInsight à l’aide de hello CLI d’Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Découvrez comment toouse hello [Interface de ligne de commande Azure](../cli-install-nodejs.md) toomanage Hadoop de clusters dans Azure HDInsight. Hello CLI d’Azure est implémenté dans Node.js. Elle peut être utilisée sur toute plateforme prenant en charge Node.js, y compris Windows, Mac et Linux.

Cet article couvre uniquement l’utilisation hello CLI d’Azure avec HDInsight. Pour obtenir un guide général sur la façon de toouse CLI d’Azure, consultez [installer et configurer Azure CLI][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **CLI Azure** -consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) pour plus d’informations d’installation et de configuration.
* **Se connecter tooAzure**, à l’aide hello la commande suivante :
  
        azure login
  
    Pour plus d’informations sur l’authentification à l’aide d’un compte professionnel ou scolaire, consultez [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../xplat-cli-connect.md).
* **Passez en mode Azure Resource Manager de toohello**, à l’aide hello la commande suivante :
  
        azure config mode arm

tooget help, utilisez hello **-h** basculer.  Par exemple :

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Créer des clusters avec hello CLI
Consultez [créer des clusters HDInsight à l’aide hello CLI d’Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Énumération et affichage des détails de cluster
Utilisez hello suivant toolist de commandes et afficher les détails du cluster :

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Vue de ligne de commande de la liste de clusters][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Suppression des clusters
Utilisez hello suivant commande toodelete un cluster :

    azure hdinsight cluster delete <Cluster Name>

Vous pouvez également supprimer un cluster par la suppression du groupe de ressources hello contient hello cluster. Notez cette opération supprimera toutes les ressources hello groupe hello, y compris le compte de stockage par défaut hello.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Mise à l’échelle des clusters
hello toochange taille de cluster Hadoop :

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Activer / désactiver l’accès HTTP pour un cluster
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Activer / désactiver l’accès RDP pour un cluster
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment tooperform HDInsight cluster tâches administratives. toolearn, voir hello suivant des articles :

* [Administrer HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]
* [Administration de HDInsight à l'aide d'Azure PowerShell][hdinsight-admin-powershell]
* [Prise en main d’Azure HDInsight][hdinsight-get-started]
* [Comment toouse hello CLI d’Azure][azure-command-line-tools]

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
