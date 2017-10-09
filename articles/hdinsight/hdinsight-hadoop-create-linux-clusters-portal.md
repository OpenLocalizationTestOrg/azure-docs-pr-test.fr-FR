---
title: "aaaCreate Hadoop clusters à l’aide d’un navigateur web - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate Hadoop, HBase, tempête ou Spark clusters sur Linux pour HDInsight à l’aide d’un navigateur web et hello portail Azure preview."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Créer des clusters basés sur Linux dans HDInsight à l’aide de hello portail Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello portail Azure est un outil de gestion basée sur le web pour les services et ressources hébergées dans le cloud de Microsoft Azure hello. Dans cet article, vous allez apprendre comment toocreate HDInsight de basés sur Linux clusters à l’aide du portail de hello.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un navigateur Web moderne**. Hello portail Azure utilise HTML5 et Javascript et peut ne pas fonctionne correctement dans les anciens navigateurs web.

## <a name="create-clusters"></a>Créer des clusters
Hello portail Azure expose la plupart des propriétés du cluster hello. Avec le modèle Azure Resource Manager, vous pouvez masquer de nombreux détails. Pour plus d’informations, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight à l’aide de modèles Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **+**, **Données + Analyse**, puis sur **HDInsight**.
   
    ![Création d’un nouveau cluster Bonjour Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "création d’un nouveau cluster Bonjour portail Azure")

3. Bonjour **HDInsight** panneau, cliquez sur **personnalisé (taille, paramètres, applications)**, cliquez sur **notions de base**, puis entrez hello informations suivantes.

    ![Création d’un nouveau cluster Bonjour Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "création d’un nouveau cluster Bonjour portail Azure")

    * Entrez le **nom du cluster**: ce nom doit être globalement unique.

    * À partir de hello **abonnement** hello de liste déroulante, sélectionnez un abonnement Azure qui sera utilisé pour le cluster de hello.

    * Cliquez sur **Type de cluster**, puis choisissez :
   
        * **Type de cluster**: Si vous ne savez pas quel toochoose, sélectionnez **Hadoop**. Il est le type de cluster les plus populaires hello.
     
            > [!IMPORTANT]
            > HDInsight clusters sont disponibles dans une variété de types, qui correspondent toohello la charge de travail ou la technologie hello cluster est réglée pour. Il n’a aucun toocreate méthode prise en charge un cluster qui combine plusieurs types, tels que Storm et HBase sur un seul cluster. 
            > 
            > 
        
        * **Système d’exploitation** : sélectionnez **Linux**.
        
        * **Version**: utiliser la version par défaut de hello si vous ne savez pas quel toochoose. Pour plus d’informations, consultez [Versions de clusters HDInsight](hdinsight-component-versioning.md).
        * **Niveau de cluster**: Azure HDInsight fournit les offres de cloud de données volumineuses hello dans deux catégories : les niveaux Standard et Premium. Pour plus d’informations, consultez [Niveaux de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).

    * Pour **nom d’utilisateur Cluster** et **mot de passe de connexion Cluster**, fournir le nom d’utilisateur hello et le mot de passe pour l’utilisateur admin hello.

    * Entrez un **nom d’utilisateur SSH** et si vous souhaitez que le mot de passe SSH de hello toohave identique hello mot de passe administrateur vous avez spécifié précédemment, sélectionnez hello **utiliser le même mot de passe en tant que compte de connexion de cluster** case à cocher. Dans le cas contraire, fournissent une **mot de passe** ou **clé publique**, qui sera un utilisateur SSH hello tooauthenticate utilisé. À l’aide d’une clé publique est hello approche recommandée. Cliquez sur **sélectionnez** lors de la configuration de hello bas toosave hello informations d’identification.
   
        Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Pour **groupe de ressources**, spécifiez si vous voulez toocreate un groupe de ressources ou utilisez un existant.

    * Spécifiez un centre de données **emplacement** où hello cluster sera créé.

    * Cliquez sur **Suivant**.

4. Sur hello **stockage** panneau, spécifier si vous souhaitez Data Lake Store ou stockage Azure (WASB) en tant que votre espace de stockage par défaut. Examinez la table hello ci-dessous pour plus d’informations.

    ![Création d’un nouveau cluster Bonjour Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "création d’un nouveau cluster Bonjour portail Azure")

    | Storage                                      | Description |
    |----------------------------------------------|-------------|
    | **Objets blob de stockage Azure comme stockage par défaut**   | <ul><li>Pour **Type de stockage principal**, sélectionnez **Stockage Azure**. Après cela, pour **méthode de sélection**, vous pouvez choisir **Mes abonnements** si vous souhaitez toospecify un compte de stockage qui fait partie de votre abonnement Azure et compte de stockage puis hello. Sinon, cliquez sur **clé d’accès** et fournissent des informations de hello hello compte de stockage que vous souhaitez toochoose à partir d’à l’extérieur de votre abonnement Azure.</li><li>Pour **conteneur par défaut**, vous pouvez choisir toogo avec hello nom de conteneur par défaut suggérée par le portail de hello ou spécifier votre propre.</li><li>Si vous utilisez WASB comme stockage par défaut, vous pouvez (facultatif) cliquez sur **des comptes de stockage supplémentaires** tooassociate avec cluster de hello les comptes de stockage supplémentaires de toospecify. Bonjour **clés de stockage Azure** panneau, cliquez sur **ajouter une clé de stockage**, et puis vous pouvez fournir un compte de stockage à partir de vos abonnements Azure ou d’autres abonnements (en fournissant le compte de stockage hello clé d’accès).</li><li>Si vous utilisez WASB comme stockage par défaut, vous pouvez (facultatif) cliquez sur **l’accès Data Lake Store** toospecify Azure Data Lake Store en tant qu’espace de stockage supplémentaire. Pour plus d’informations, consultez [Créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store en tant que stockage par défaut** | Pour **type de stockage principal**, sélectionnez **Data Lake Store** puis consultez l’article de toohello [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) pour obtenir des instructions. |
    | **Metastores externes**                      | Si vous le souhaitez, vous pouvez spécifier une base de données toosave Hive et Oozie métadonnées SQL associée hello cluster. Pour **sélectionner une base de données SQL pour la ruche** sélectionner une base de données SQL, puis indiquez hello nom d’utilisateur/mot de passe pour la base de données hello. Répétez ces étapes pour les métadonnées d’Oozie.<br><br>Des points à prendre en compte lors de l’utilisation d’une base de données Azure SQL pour les metastores. <ul><li>base de données SQL Azure Hello utilisé pour le magasin de métadonnées hello doit autoriser tooother de connectivité des services Azure, y compris Azure HDInsight. Tableau de bord de base de données SQL Azure hello, sur le côté droit de hello, cliquez sur le nom du serveur hello. Il s’agit de serveur hello sur quel hello SQL instance de base de données est en cours d’exécution. Une fois que vous êtes dans la vue du serveur hello, cliquez sur **configurer**, puis **Services Azure**, cliquez sur **Oui**, puis cliquez sur **enregistrer**.</li><li>Lors de la création d’un magasin de métadonnées, n’utilisez pas un nom de base de données qui contient des tirets ou des traits d’union, cela peut entraîner des toofail de processus de création de cluster hello.</li></ul>                                                                                                                                                                       |

    Cliquez sur **Suivant**. 

    > [!WARNING]
    > À l’aide d’un compte de stockage supplémentaire dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.

5. Si vous le souhaitez, cliquez sur **Applications** tooinstall les applications qui fonctionnent avec des clusters HDInsight. Ces applications peuvent être développées par Microsoft, par des éditeurs de logiciels indépendants (ISV) ou par vous-même. Pour plus d’informations, consultez [Installer des applications HDInsight](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Cliquez sur **taille de Cluster** toodisplay plus d’informations sur les nœuds hello qui sera créé pour ce cluster. Définir le nombre hello de nœuds de travail dont vous avez besoin pour le cluster de hello. Hello estimation de coût de cluster de hello s’affichera dans le panneau de hello.
   
    ![Panneau des niveaux de tarification du nœud](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Spécifier le nombre de nœuds de cluster")
   
   > [!IMPORTANT]
   > Si vous prévoyez plus de 32 nœuds de travail, à la création du cluster ou par mise à l’échelle les cluster hello après sa création, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de ram.
   > 
   > Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Cliquez sur **suivant** nœud de hello toosave configuration de la tarification.

7. Cliquez sur **paramètres avancés** tooconfigure autres paramètres facultatifs, telles que l’utilisation **Actions de Script** toocustomize un tooinstall cluster des composants personnalisés ou joindre un **deréseauvirtuel**. Examinez la table hello ci-dessous pour plus d’informations.

    ![Panneau des niveaux de tarification du nœud](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Spécifier le nombre de nœuds de cluster")

    | Option | Description |
    |--------|-------------|
    | **Actions de script** | Utilisez cette option si vous voulez toouse un script personnalisé de toocustomize un cluster, lors de la création de cluster de hello. Pour plus d’informations sur les actions de script, consultez l’article [Personnaliser des clusters HDInsight à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Réseau virtuel** | Sélectionnez un sous-réseau hello et de réseau virtuel Azure si vous souhaitez que le cluster de hello tooplace dans un réseau virtuel. Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel, y compris la configuration spécifique requise pour hello réseau virtuel, consultez [HDInsight d’étendre les fonctionnalités à l’aide d’un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md). |

    Cliquez sur **Suivant**.

8. Sur hello **Résumé** panneau, vérifiez les informations de hello que vous avez entrées précédemment, puis **créer**.

    ![Panneau des niveaux de tarification du nœud](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Spécifier le nombre de nœuds de cluster")
    
    > [!NOTE]
    > Il prend un certain temps pour hello toobe de cluster créé, généralement environ 15 minutes. Utilisez hello vignette sur hello tableau d’accueil ou hello **Notifications** entrée sur hello restant de hello page toocheck sur hello processus de configuration.
    > 
    > 
12. Une fois que le processus de création de hello terminée, cliquez sur mosaïque hello pour cluster hello à partir du Panneau de cluster hello tableau d’accueil toolaunch hello. Panneau de cluster Hello fournit hello informations suivantes.
    
    ![Panneau de cluster](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Propriétés du Cluster")
    
    Utilisez hello suivant des icônes de hello toounderstand haut hello de ce panneau.
    
    * **Vue d’ensemble** onglet fournit toutes les informations essentielles hello sur cluster hello telles que nom hello, groupe de ressources hello il appartient, emplacement hello, système d’exploitation de hello, URL de tableau de bord de cluster hello, etc..
    * **Tableau de bord** vous dirige le portail de Ambari toohello associé hello cluster.
    * **Secure Shell**: informations requises de cluster de hello tooaccess à l’aide de SSH.
    * **Cluster de la mise à l’échelle** vous permet de vous augmentez le nombre hello de nœuds de travail associé hello cluster.
    * **Supprimer**: cluster de suppressions hello HDInsight.
    

## <a name="customize-clusters"></a>Personnalisation des clusters
* Consultez [Personnalisation de clusters HDInsight à l’aide de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé un cluster HDInsight, utilisez hello suivant toolearn comment toowork avec votre cluster :

### <a name="hadoop-clusters"></a>Clusters Hadoop
* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clusters HBase
* [Prise en main de HBase sur HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Développement d’applications Java pour HBase sur HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clusters Storm
* [Développement de topologies Java pour Storm sur HDInsight](hdinsight-storm-develop-java-topology.md)
* [Utilisation de composants Python dans Storm sur HDInsight](hdinsight-storm-develop-python-topology.md)
* [Déploiement et analyse des topologies avec Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Clusters Spark
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécution de travaux à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)

