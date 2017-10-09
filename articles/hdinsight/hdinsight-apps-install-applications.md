---
title: applications de Hadoop aaaInstall tiers sur Azure HDInsight | Documents Microsoft
description: "Découvrez comment les applications Hadoop tooinstall tiers sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Installer des applications Hadoop tierces sur Azure HDInsight

Dans cet article, vous apprendrez comment tooinstall une application Hadoop déjà publiée sur Azure HDInsight. Pour des instructions d’installation de votre propre application, consultez la page [Installer des applications HDInsight personnalisées](hdinsight-apps-install-custom-applications.md).

Une application HDInsight est une application que les utilisateurs peuvent installer sur un cluster HDInsight sous Linux. Ces applications peuvent être développées par Microsoft, par des éditeurs de logiciels indépendants (ISV) ou par vous-même.  

Actuellement, il existe quatre applications publiées :

* **DDS DATAIKU sur HDInsight**: Dataiku DSS (Studio de science des données) est un logiciel qui permet aux données tooprototype de professionnels (chercheurs de données, les analystes d’entreprise, les développeurs...), générer et déployer des services très spécifiques qui transforment les données brutes dans prédictions business impact non négligeable.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) offre analystes un toodiscover de manière interactive, analyser et visualiser les résultats de hello sur les données volumineuses. Extraire dans les sources de données supplémentaires facilement toodiscover nouvelles relations et obtenir des réponses hello que vous devez rapidement.
* **Le collecteur de données Streamsets pour HDnsight** fournit un environnement complet de développement intégré (IDE) que vous permet de concevoir, tester, déployer et gérer à tout réception pipelines que les données de flux de données et de traitement par lots de maillage et inclure diverses transformations de flux de données, sans avoir toowrite un code personnalisé. 
* **Cages CDAP pour HDInsight** fournit hello unifiée tout d’abord la plateforme d’intégration pour les données volumineuses qui tooproduction de temps hello pour les applications de données et des lacs de données réduit à 80 %. Cette application prend uniquement en charge les clusters Standard HBase 3.4.
* **Intelligence artificielle de H2O pour HDInsight (bêta)** H2O mousseux eau prend en charge hello suivant des algorithmes distribués : GLM, Naïve Bayes, Distributed aléatoire forêt, dégradé Machine Boosting, réseaux neuronaux en profondeur, approfondie de formation, K-means, PCA, Modèles de classement faibles généralisés, détection d’anomalie et Autoencoders.
* **Kyligence Analytics Platform** Kyligence Analytics Platform (KAP) est un entrepôt de données d’entreprise s’appuyant sur Apache Kylin et Apache Hadoop. Il permet d’obtenir une latence de requête inférieure à une seconde sur des jeux de données extrêmement volumineux, et il simplifie l’analyse des données pour les utilisateurs professionnels et les analystes. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex en cours d’exécution sur HDInsight permet insights toobusiness à tooget de clients plus rapides en fournissant l’ingestion de données libre-service et de préparation à partir de pratiquement n’importe quel toohello source cloud Microsoft Azure plateforme.
* **Serveur de travail Spark pour l’exécuteur de Spark KNIME** Spark serveur de travail pour l’exécuteur de Spark KNIME est utilisé tooconnect hello KNIME Analytique plateforme tooHDInsight clusters.

les instructions Hello fournies dans cet article utilisent le portail Azure. Vous pouvez également exporter le modèle de gestionnaire de ressources Azure hello à partir du portail de hello ou obtenir une copie du modèle de gestionnaire de ressources hello auprès de fournisseurs et utiliser Azure PowerShell et le modèle de hello toodeploy CLI d’Azure.  Consultez [Création de clusters Hadoop basés sur Linux dans HDInsight à l’aide de modèles Resource Manager | Microsoft Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Composants requis
Si vous souhaitez que les applications de HDInsight tooinstall sur un cluster HDInsight existant, vous devez disposer d’un cluster HDInsight. toocreate, consultez [créer des clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Vous pouvez également installer des applications HDInsight lorsque vous créez un cluster HDInsight.

## <a name="install-applications-tooexisting-clusters"></a>Installer des clusters de tooexisting d’applications
Hello procédure suivante vous montre comment tooan-cluster de HDInsight existant tooinstall HDInsight applications.

**tooinstall une application HDInsight**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** dans le menu de gauche hello.  Si vous ne le voyez pas, cliquez sur **Autres services**, puis sur **Clusters HDInsight**.
3. Cliquez sur un cluster HDInsight.  Si vous ne disposez pas d’un tel cluster, vous devez d’abord en créer un.  Consultez la page [Créer des clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Cliquez sur **Applications** sous hello **Configurations** catégorie. Une liste des applications installées s’affiche. Si vous ne trouvez pas les Applications, cela signifie qu'il n’existe aucune application pour cette version du cluster HDInsight de hello.
   
    ![Applications HDInsight - menu du portail](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Cliquez sur **ajouter** à partir du menu du panneau hello. 
   
    ![Applications HDInsight - applications installées](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Une liste des applications HDInsight existantes s’affiche.
   
    ![Applications HDInsight - applications disponibles](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Cliquez sur une des applications de hello, acceptez les conditions juridiques hello et puis cliquez sur **sélectionnez**.

Vous pouvez voir d’état de l’installation à partir des notifications de portail hello hello (cliquez sur l’icône de cloche hello haut hello du portail de hello). Après hello application est installée avec l’application hello s’affiche dans le panneau des applications installées hello.

## <a name="install-applications-during-cluster-creation"></a>Installer des applications lors de la création du cluster
Vous avez des applications de HDInsight tooinstall hello option lorsque vous créez un cluster. Pendant le processus de hello, HDInsight applications sont installées après que la création de cluster de hello et est en état d’exécution de hello. Hello procédure suivante vous montre comment les applications de HDInsight tooinstall lorsque vous créez un cluster.

**tooinstall une application HDInsight**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **NOUVEAU**, sur **Données + analyse**, puis sur **HDInsight**.
3. Entrez le **nom du cluster**: ce nom doit être globalement unique.
4. Cliquez sur **abonnement** tooselect hello abonnement Azure qui est utilisé pour le cluster de hello.
5. Cliquez sur **Sélectionner un type de cluster**, puis choisissez :
   
   * **Type de cluster**: Si vous ne savez pas quel toochoose, sélectionnez **Hadoop**. Il est le type de cluster les plus populaires hello.
   * **Système d’exploitation** : sélectionnez **Linux**.
   * **Version**: utiliser la version par défaut de hello si vous ne savez pas quel toochoose. Pour plus d’informations, consultez [Versions de clusters HDInsight](hdinsight-component-versioning.md).
   * **Niveau de cluster**: Azure HDInsight fournit les offres de cloud de données volumineuses hello dans deux catégories : les niveaux Standard et Premium. Pour plus d’informations, consultez [Niveaux de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Cliquez sur **Applications**, cliquez sur un des hello applications publiées, puis cliquez sur **sélectionnez**.
7. Cliquez sur **informations d’identification** , puis entrez un mot de passe de l’utilisateur admin hello. Vous devez également tooenter une **nom d’utilisateur SSH** et un **mot de passe** ou **clé publique**, qui est l’utilisateur SSH hello tooauthenticate utilisé. À l’aide d’une clé publique est hello approche recommandée. Cliquez sur **sélectionnez** lors de la configuration de hello bas toosave hello informations d’identification.
8. Cliquez sur **Source de données**, sélectionnez une des hello les comptes de stockage existants ou créer un nouveau toobe de compte de stockage utilisé comme compte de stockage par défaut hello pour le cluster de hello.
9. Cliquez sur **groupe de ressources** tooselect une ressource de groupe, ou cliquez sur **nouveau** toocreate un groupe de ressources
10. Sur hello **nouveau HDInsight Cluster** panneau, vérifiez que **code confidentiel tooStartboard** est sélectionné, puis cliquez sur **créer**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Répertorier les applications HDInsight installées et les propriétés
portail de Hello affiche qu'une liste de hello installé des applications de HDInsight pour un cluster et les propriétés hello de chaque application installée.

**propriétés toolist HDInsight application et l’affichage**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** dans le menu de gauche hello.  Si vous ne le voyez pas, cliquez sur **Parcourir**, puis sur **Clusters HDInsight**.
3. Cliquez sur un cluster HDInsight.
4. À partir de hello **paramètres** panneau, cliquez sur **Applications** sous hello **général** catégorie. panneau des applications installées Hello répertorie toutes les applications hello installé. 
   
    ![Applications HDInsight - applications installées](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Cliquez sur une propriété de hello tooshow hello installé les applications. listes de panneau Propriétés Hello :
   
   * Nom de l’application : nom de l’application.
   * État : état de l’application. 
   * Page Web : hello URL d’application web de hello que vous avez déployé le nœud de périmètre toohello. informations d’identification Hello sont hello identique à celle de l’utilisateur de hello HTTP des informations d’identification que vous avez configuré pour le cluster de hello.
   * Point de terminaison HTTP : informations d’identification hello sont hello identique à celle de l’utilisateur de hello HTTP des informations d’identification que vous avez configuré pour le cluster de hello. 
   * Point de terminaison SSH : vous pouvez utiliser SSH tooconnect toohello bord nœud. informations d’identification SSH de Hello sont hello identique à celle de l’utilisateur SSH hello les informations d’identification que vous avez configuré pour le cluster de hello. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).
6. toodelete une application, cliquez sur application hello, puis cliquez sur **supprimer** à partir du menu contextuel de hello.

## <a name="connect-toohello-edge-node"></a>Connecter toohello bord nœud
Vous pouvez connecter le nœud de périmètre toohello à l’aide de HTTP et SSH. Vous trouverez des informations de point de terminaison de Hello de hello [portal](#list-installed-hdinsight-apps-and-properties). Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

informations d’identification du point de terminaison Hello HTTP sont hello HTTP informations d’identification utilisateur que vous avez configuré pour le cluster HDInsight de hello ; informations d’identification du point de terminaison Hello SSH sont des informations d’identification SSH hello que vous avez configuré pour le cluster HDInsight de hello.

## <a name="troubleshoot"></a>Résolution des problèmes
Consultez [dépanner hello installation](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Étapes suivantes
* [Installer des applications personnalisées HDInsight](hdinsight-apps-install-custom-applications.md): Découvrez comment toodeploy un tooHDInsight d’application HDInsight non publiée.
* [Publier des applications de HDInsight](hdinsight-apps-publish-applications.md): Découvrez comment toopublish votre tooAzure d’applications personnalisée HDInsight Marketplace.
* [MSDN : Installer une application de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Découvrez comment toodefine HDInsight applications.
* [Personnaliser des clusters HDInsight de basés sur Linux à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md): Découvrez comment des applications supplémentaires toouse Action de Script tooinstall.
* [Créer des clusters basés sur Linux de Hadoop dans HDInsight à l’aide du Gestionnaire de ressources modèles](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Découvrez comment toocall le Gestionnaire de ressources modèles toocreate HDInsight clusters.
* [Utiliser noeuds vide dans HDInsight](hdinsight-apps-use-edge-node.md): Découvrez comment toouse vide bord du nœud pour l’accès à cluster HDInsight, test des applications de HDInsight et l’hébergement des applications de HDInsight.

