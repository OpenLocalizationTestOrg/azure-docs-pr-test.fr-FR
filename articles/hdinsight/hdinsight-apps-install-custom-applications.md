---
title: "aaaInstall vos propres applications personnalisées de Hadoop sur Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooinstall HDInsight les applications sur les applications de HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Installer des applications personnalisées Hadoop sur Azure HDInsight

Dans cet article, vous allez apprendre comment tooinstall une application Hadoop sur Azure HDInsight, qui n’a pas été publié toohello portail Azure. application Hello vous installerez dans cet article est [teinte](http://gethue.com/).

Une application HDInsight est une application que les utilisateurs peuvent installer sur un cluster HDInsight sous Linux.  Ces applications peuvent être développées par Microsoft, par des éditeurs de logiciels indépendants (ISV) ou par vous-même.  

Autres articles associés :

* [Installer des applications de HDInsight](hdinsight-apps-install-applications.md): Découvrez comment tooinstall un tooyour d’application HDInsight clusters.
* [Publier des applications de HDInsight](hdinsight-apps-publish-applications.md): Découvrez comment toopublish votre tooAzure d’applications personnalisée HDInsight Marketplace.
* [MSDN : Installer une application de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Découvrez comment toodefine HDInsight applications.

## <a name="prerequisites"></a>Composants requis
Si vous souhaitez que les applications de HDInsight tooinstall sur un cluster HDInsight existant, vous devez disposer d’un cluster HDInsight. toocreate, consultez [créer des clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Vous pouvez également installer des applications HDInsight lorsque vous créez un cluster HDInsight.

## <a name="install-hdinsight-applications"></a>Install custom HDInsight applications
Applications de HDInsight peuvent être installées lorsque vous créez un cluster ou tooan existant HDInsight. Pour définir des modèles Azure Resource Manager, consultez [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx)(MSDN : installer une application HDInsight).

fichiers Hello nécessaires pour déployer cette application (teinte) :

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): modèle de gestionnaire de ressources hello pour l’installation d’application de HDInsight. Consultez la page [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN : installer une application HDInsight) pour développer votre propre modèle Resource Manager.
* [teinte-install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello action de Script qui est appelée par le modèle de gestionnaire de ressources hello pour la configuration de nœud de périmètre hello.
* [teinte-binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): fichier binaire de hello teinte appelée à partir d’aujourd'hui-install_v0.sh.
* [teinte-binaires-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): fichier binaire de hello teinte appelée à partir d’aujourd'hui-install_v0.sh.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz) : exemple d’application web (Tomcat) appelée à partir de hui-install_v0.sh.

**cluster HDInsight existant de tooinstall teinte tooan**

1. Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Ce bouton ouvre un modèle de gestionnaire de ressources sur hello portail Azure.  Hello modèle Resource Manager se trouve dans [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn comment toowrite ce modèle de gestionnaire de ressources, consultez [MSDN : installer une application de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. À partir de hello **paramètres** panneau, entrez hello suivante :

   * **ClusterName**: entrez le nom hello du cluster de hello application hello de tooinstall. Ce cluster doit être un cluster existant.
3. Cliquez sur **OK** toosave les paramètres hello.
4. À partir de hello **les déploiement personnalisé** panneau, entrez **groupe de ressources**.  groupe de ressources Hello est un conteneur qui regroupe le cluster de hello, compte de stockage dépendant de hello et autres ressources. Il est requis toouse hello même groupe de ressources en tant que cluster de hello.
5. Cliquez sur **Conditions juridiques**, puis cliquez sur **Créer**.
6. Vérifiez que hello **code confidentiel toodashboard** case à cocher est sélectionnée, puis cliquez sur **créer**. Vous pouvez voir l’état de l’installation hello hello vignette épinglée toohello portail du tableau de bord et de notification du portail hello (cliquez sur l’icône de cloche hello haut hello du portail de hello).  Il faut application hello de tooinstall environ 10 minutes.

**tooinstall teinte lors de la création d’un cluster**

1. Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Ce bouton ouvre un modèle de gestionnaire de ressources sur hello portail Azure.  Hello modèle Resource Manager se trouve dans [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn comment toowrite ce modèle de gestionnaire de ressources, consultez [MSDN : installer une application de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Suivez hello instruction toocreate cluster et installer la teinte. Pour plus d’informations sur la création de clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

En outre toohello portail Azure, vous pouvez également utiliser [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) et [CLI d’Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall les modèles de gestionnaire de ressources.

## <a name="validate-hello-installation"></a>Valider l’installation de hello
Vous pouvez vérifier l’état de l’application hello sur hello installation de l’application hello toovalidate portail Azure. En outre, vous pouvez également valider tous les provient de points de terminaison HTTP des comme prévu et une page Web de hello si elle existe :

**portail de teinte hello tooopen**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** dans le menu de gauche hello.  Si vous ne le voyez pas, cliquez sur **Parcourir**, puis sur **Clusters HDInsight**.
3. Cliquez sur le cluster hello où vous avez installé l’application hello.
4. À partir de hello **paramètres** panneau, cliquez sur **Applications** sous hello **général** catégorie. Vous allez voir **teinte** répertoriés dans hello **installé des applications** panneau.
5. Cliquez sur **teinte** à partir des propriétés de hello liste toolist hello.  
6. Cliquez sur le site Web hello page Web lien toovalidate hello ; Ouvrez le point de terminaison hello HTTP dans un navigateur toovalidate hello teinte interface utilisateur web, point de terminaison SSH hello ouverte à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Résoudre les problèmes d’installation de hello
Vous pouvez vérifier hello application installation état à partir de la notification du portail hello (cliquez sur l’icône de cloche hello haut hello du portail de hello).

En cas d’échec de l’installation d’une application, vous pouvez voir les messages d’erreur hello et déboguer des informations à partir de 3 emplacements :

* Applications HDInsight : informations générales relatives à l’erreur.

    Ouvrir le cluster de hello à partir du portail de hello, puis cliquez sur Applications à partir du Panneau de paramètres hello :

    ![Erreur d’installation des applications hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Action de script HDInsight : si le message d’erreur hello HDInsight Applications indique un échec d’action de script, plus de détails sur l’échec du script hello seront affiche dans le volet actions de script hello.

    Cliquez sur Action de Script à partir du Panneau de paramètres hello. Historique des actions de script affiche les messages d’erreur hello

    ![Erreur de l’action de script des applications hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web, l’interface utilisateur : Si le script d’installation hello était cause hello de défaillance de hello, utilisez journaux complets de l’interface utilisateur de Ambari Web toocheck sur les scripts d’installation hello.

    Pour plus d’informations, consultez la page [Dépannage](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Supprimer des applications HDInsight
Il existe plusieurs façons toodelete HDInsight applications.

### <a name="use-portal"></a>Utilisation du portail
**tooremove une application à l’aide du portail de hello**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** dans le menu de gauche hello.  Si vous ne le voyez pas, cliquez sur **Parcourir**, puis sur **Clusters HDInsight**.
3. Cliquez sur le cluster hello où vous avez installé l’application hello.
4. À partir de hello **paramètres** panneau, cliquez sur **Applications** sous hello **général** catégorie. Vous devriez voir une liste des applications installées. Pour ce didacticiel, **teinte** répertoriés dans hello **installé des applications** panneau.
5. Cliquez sur application hello vous souhaitez tooremove, puis cliquez sur **supprimer**.
6. Cliquez sur **Oui** tooconfirm.

À partir du portail de hello, vous pouvez également supprimer le cluster de hello ou supprimer le groupe de ressources hello qui contient l’application hello.

### <a name="use-azure-powershell"></a>Utilisation d'Azure PowerShell
À l’aide d’Azure PowerShell, vous pouvez supprimer le cluster de hello ou supprimer le groupe de ressources hello. Consultez la section [Supprimer des clusters à l’aide d’Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Utiliser l’interface de ligne de commande Microsoft Azure
À l’aide de CLI d’Azure, vous pouvez supprimer le cluster de hello ou supprimer le groupe de ressources hello. Consultez la section [Supprimer des clusters à l’aide de l’interface de ligne de commande Azure](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Étapes suivantes
* [MSDN : Installer une application de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Découvrez comment toodevelop les modèles de gestionnaire de ressources pour le déploiement d’applications de HDInsight.
* [Installer des applications de HDInsight](hdinsight-apps-install-applications.md): Découvrez comment tooinstall un tooyour d’application HDInsight clusters.
* [Publier des applications de HDInsight](hdinsight-apps-publish-applications.md): Découvrez comment toopublish votre tooAzure d’applications personnalisée HDInsight Marketplace.
* [Personnaliser des clusters HDInsight de basés sur Linux à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md): Découvrez comment des applications supplémentaires toouse Action de Script tooinstall.
* [Créer des clusters basés sur Linux de Hadoop dans HDInsight à l’aide du Gestionnaire de ressources modèles](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Découvrez comment toocall le Gestionnaire de ressources modèles toocreate HDInsight clusters.
* [Utiliser noeuds vide dans HDInsight](hdinsight-apps-use-edge-node.md): Découvrez comment toouse vide bord du nœud pour l’accès à cluster HDInsight, test des applications de HDInsight et l’hébergement des applications de HDInsight.
