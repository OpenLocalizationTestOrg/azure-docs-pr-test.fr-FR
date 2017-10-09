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
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Créer un cluster Hadoop à l’aide de comptes de stockage avec transfert sécurisé dans Azure HDInsight

Hello [sécuriser le transfert requis](../storage/common/storage-require-secure-transfer.md) fonctionnalité améliore la sécurité de hello de votre compte de stockage Azure en appliquant le compte de tooyour toutes les demandes via une connexion sécurisée. Cette fonctionnalité et hello wasbs schéma sont uniquement pris en charge par la version du cluster HDInsight 3.6 ou version ultérieure. 

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :

* **Abonnement Azure**: toocreate un compte d’essai un mois gratuit, parcourir trop[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Un compte de stockage Azure doté du transfert sécurisé**. Pour obtenir des instructions de hello, consultez [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) et [requièrent un transfert sécurisé](../storage/common/storage-require-secure-transfer.md).
* **Un conteneur d’objets Blob sur le compte de stockage hello**. 
## <a name="create-cluster"></a>Créer un cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


Cette section vous permet de créer un cluster Hadoop dans HDInsight à l’aide d’un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Hello modèle se trouve dans [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Aucune expérience avec le modèle Resource Manager n’est requise pour ce didacticiel. Pour d’autres méthodes de création de cluster et les propriétés hello utilisées dans ce didacticiel, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md).

1. Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Procédez comme cluster de hello hello instructions toocreate avec hello conformément aux spécifications : 

    - Indiquez HDInsight version 3.6.  version par défaut de Hello est 3.5. La version 3.6 ou une version ultérieure est requise.
    - Indiquez un compte de stockage doté du transfert sécurisé.
    - Utilisez le nom court pour le compte de stockage hello.
    - Compte de stockage hello et conteneur d’objets blob hello doivent être créés au préalable. 

    Pour obtenir des instructions de hello, consultez [créer un cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Si vous utilisez le script action tooprovide vos propres fichiers de configuration, vous devez utiliser wasbs Bonjour suivant les paramètres :

- fs.defaultFS (site principal)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Ajouter des comptes de stockage

Il existe plusieurs comptes de stockage supplémentaires transfert sécurisé activé tooadd options :

- Modifier le modèle de gestionnaire de ressources Azure hello dans la dernière section de hello.
- Créer un cluster à l’aide de hello [portail Azure](https://portal.azure.com) et spécifiez le compte de stockage lié.
- Utilisez script action tooadd supplémentaire transfert sécurisé activé cluster HDInsight existant de stockage comptes tooan.  Pour plus d’informations, consultez [ajouter tooHDInsight des comptes de stockage supplémentaire](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toocreate un cluster HDInsight et activer sécurisé de transfert toohello les comptes de stockage.

toolearn en savoir plus sur l’analyse de données avec HDInsight, consultez hello suivant des articles :

* toolearn savoir plus sur l’utilisation de la ruche avec HDInsight, y compris le fonctionnement des requêtes tooperform Hive à partir de Visual Studio, consultez [utilisez Hive hdinsight][hdinsight-use-hive].
* toolearn sur Pig, un langage tootransform données, consultez [utilisez Pig hdinsight][hdinsight-use-pig].
* toolearn sur MapReduce, une façon dont les programmes toowrite qui traitent les données sur Hadoop, consultez [MapReduce utilisation hdinsight][hdinsight-use-mapreduce].
* toolearn sur l’utilisation des outils HDInsight de hello pour les données de tooanalyze de Visual Studio sur HDInsight, consultez [prise en main des outils de Visual Studio Hadoop pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

toolearn plus en détail comment HDInsight stocke les données ou les données tooget dans HDInsight, voir hello suivant des articles :

* Pour plus d’informations sur la façon dont HDInsight utilise le stockage Azure, consultez la page [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md) (Utilisation du stockage Azure avec HDInsight).
* Pour plus d’informations sur la façon de tooupload tooHDInsight de données, consultez [télécharger des données tooHDInsight][hdinsight-upload-data].

toolearn en savoir plus sur la création ou de gestion d’un cluster HDInsight, consultez hello suivant des articles :

* toolearn sur la gestion de votre cluster HDInsight de basés sur Linux, consultez [HDInsight de gérer des clusters à l’aide de Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn savoir plus sur les options de hello vous pouvez sélectionner lors de la création d’un cluster HDInsight, consultez [création de HDInsight sur Linux à l’aide des options personnalisées](hdinsight-hadoop-provision-linux-clusters.md).
* Si vous êtes familiarisé avec Linux et Hadoop, mais tooknow spécificités Hadoop sur hello HDInsight, consultez [utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md). Cet article vous fournit les informations suivantes :
  
  * URL pour les services hébergés sur le cluster hello, telles que Ambari et WebHCat
  * emplacement des fichiers de Hadoop et des exemples sur le système de fichiers local hello de Hello
  * utilisation de Hello d’Azure Storage (WASB) au lieu de HDFS en tant que banque de données par défaut hello

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


