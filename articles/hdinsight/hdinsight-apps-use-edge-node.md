---
title: aaaUse vide les noeuds sur les clusters Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Comment tooadd un tooan de nœud vide bord HDInsight de cluster qui peut être utilisé en tant que client et vos applications HDInsight puis test/hôte."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Utiliser les nœuds de périphérie vides sur les clusters Hadoop dans HDInsight

Découvrez comment tooadd vide bord du cluster de nœud tooan HDInsight. Un nœud vide est une machine virtuelle de Linux avec hello mêmes outils client installé et configuré comme hello headnodes, mais sans aucun service Hadoop en cours d’exécution. Vous pouvez utiliser le nœud de périmètre hello pour accédant à hello cluster, le test de vos applications clientes et hébergement de vos applications clientes. 

Lorsque vous créez le cluster de hello, vous pouvez ajouter un cluster HDInsight existant de bord vide nœud tooan, le tooa nouveau cluster. L’ajout d’un nœud de périmètre vide est effectué à l’aide du modèle Azure Resource Manager.  Hello exemple suivant montre comment procéder à l’aide d’un modèle :

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Comme indiqué dans l’exemple hello, vous pouvez éventuellement appeler un [action de script](hdinsight-hadoop-customize-cluster-linux.md) tooperform une configuration supplémentaire, telle que l’installation [Apache teinte](hdinsight-hadoop-hue-linux.md) dans le nœud de périmètre hello. script d’action de script Hello doit être publiquement accessible sur le web de hello.  Par exemple, si le script de hello est stocké dans le stockage Azure, utilisez des conteneurs publics ou objets BLOB publics.

taille de machine virtuelle de nœud Hello bord requise hello HDInsight cluster travail nœud vm taille. Pour hello recommandé travail tailles de machine virtuelle de nœud, consultez [Hadoop de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Après avoir créé un nœud, vous pouvez connecter le nœud de périmètre toohello à l’aide de SSH et exécuter client cluster d’outils tooaccess hello Hadoop dans HDInsight.

> [!WARNING] 
> L’utilisation d’un nœud de périphérie vide avec HDInsight n’est actuellement disponible qu’en préversion. Les composants personnalisés qui sont installés sur le nœud de périmètre hello bénéficier du support commercialement raisonnable de Microsoft. Ainsi, cela peut aider à résoudre les problèmes rencontrés. Ou vous pouvez être toocommunity auxquels des ressources pour obtenir une assistance. Hello Voici quelques-uns des hello la plupart des sites actifs pour l’obtention d’aide à partir de la Communauté de hello :
>
> * [Forum MSDN pour HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> Si vous utilisez une technologie d’Apache, vous pouvez être assistance toofind en mesure de par Bonjour sites de projets Apache sur [http://apache.org](http://apache.org), par exemple hello [Hadoop](http://hadoop.apache.org/) site.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Ajouter un cluster existant de bord nœud tooan
Dans cette section, vous utilisez un tooadd de modèle de gestionnaire de ressources un cluster HDInsight bord nœud tooan existant.  modèle de gestionnaire de ressources de Hello peut se trouver dans [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). modèle de gestionnaire de ressources Hello appelle une action de script située à https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. script de Hello n’effectue aucune action.  Il est toodemonstrate d’appel de l’action de script à partir d’un modèle de gestionnaire de ressources.

**tooadd un cluster existant de bord vide nœud tooan**

1. Créez un cluster HDInsight si vous n’avez pas encore.  Consultez le [Didacticiel Hadoop : prise en main de Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Cliquez sur hello suivant toosign image dans tooAzure et modèle d’Azure Resource Manager hello ouvrir Bonjour portail Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configurer les propriétés suivantes de hello :
   
   * **Abonnement**: sélectionnez un abonnement Azure utilisé pour créer le cluster de hello.
   * **Groupe de ressources**: groupe de ressources hello sélectionnez utilisé pour le cluster HDInsight existant de hello.
   * **Emplacement**: sélectionnez l’emplacement hello du cluster HDInsight existant de hello.
   * **Nom du cluster**: entrez le nom hello d’un cluster HDInsight existant.
   * **Taille du nœud de bord**: sélectionnez une des tailles de machine virtuelle hello. taille de machine virtuelle Hello doit répondre aux exigences de taille de l’ordinateur virtuel hello travail nœud. Pour hello recommandé travail tailles de machine virtuelle de nœud, consultez [Hadoop de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Bord nœud préfixe**: hello la valeur par défaut est **nouveau**.  À l’aide de la valeur par défaut de hello, nom de nœud de bord de hello est **edgenode-nouvelle**.  Vous pouvez personnaliser le préfixe hello à partir du portail de hello. Vous pouvez également personnaliser le nom complet de hello dans le modèle de hello.

4. Vérifiez **J’accepte les conditions susmentionnées générales toohello**, puis cliquez sur **achat** nœud toocreate hello.

>[!IMPORTANT]
> Assurez-vous que tooselect hello Azure groupe de ressources de cluster HDInsight existant de hello.  Dans le cas contraire, vous obtenez des erreurs de hello message « Impossible d’effectuer l’opération demandée sur la ressource imbriquée. Parent resource '&lt;ClusterName>' not found » (Impossible d’effectuer l’opération demandée sur la ressource imbriquée. Ressource parente <Nom du cluster> introuvable).

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Ajouter un nœud de périmètre lors de la création d’un cluster
Dans cette section, vous utilisez un cluster HDInsight de gestionnaire de ressources du modèle toocreate avec un nœud de périmètre.  modèle de gestionnaire de ressources Hello sont accessibles dans hello [la galerie de modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). modèle de gestionnaire de ressources Hello appelle une action de script située à https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. script de Hello n’effectue aucune action.  Il est toodemonstrate d’appel de l’action de script à partir d’un modèle de gestionnaire de ressources.

**tooadd un cluster existant de bord vide nœud tooan**

1. Créez un cluster HDInsight si vous n’avez pas encore.  Consultez [Prise en main de Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Cliquez sur hello suivant toosign image dans tooAzure et modèle d’Azure Resource Manager hello ouvrir Bonjour portail Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configurer les propriétés suivantes de hello :
   
   * **Abonnement**: sélectionnez un abonnement Azure utilisé pour créer le cluster de hello.
   * **Groupe de ressources**: créer un groupe de ressources utilisé pour le cluster de hello.
   * **Emplacement**: sélectionnez un emplacement pour le groupe de ressources hello.
   * **Nom du cluster**: entrez un nom pour hello nouveau cluster toocreate.
   * **Nom d’utilisateur de cluster**: entrez le nom d’utilisateur Hadoop HTTP hello.  le nom par défaut Hello est **admin**.
   * **Mot de passe de connexion cluster**: entrez le mot de passe utilisateur hello Hadoop HTTP.
   * **SSH nom d’utilisateur**: entrez le nom d’utilisateur SSH hello. le nom par défaut Hello est **sshuser**.
   * **SSH mot de passe**: entrez le mot de passe utilisateur hello SSH.
   * **Action de Script d’installation**: conserver la valeur par défaut de hello pour traverser ce didacticiel.
     
     Certaines propriétés ont été codé en dur dans le modèle de hello : type de Cluster, nombre de nœuds de travail de Cluster, taille du nœud contour et nom de nœud de bord.
4. Vérifiez **J’accepte les conditions susmentionnées générales toohello**, puis cliquez sur **achat** cluster hello de toocreate avec un nœud de périmètre hello.

## <a name="access-an-edge-node"></a>Accéder à un nœud de périmètre
nœud de périmètre Hello ssh point de terminaison est &lt;EdgeNodeName >.&lt; Nom_cluster >-ssh.azurehdinsight.net:22.  Par exemple, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

nœud de périmètre Hello s’affiche en tant qu’application sur hello portail Azure.  permet de portail Hello vous hello hello de tooaccess informations bord du nœud à l’aide de SSH.

**point de terminaison tooverify hello bord nœud SSH**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Ouvrez le cluster HDInsight de hello avec un nœud de périmètre.
3. Cliquez sur **Applications** à partir du Panneau de cluster hello. Vous devez voir le nœud de périmètre hello.  le nom par défaut Hello est **edgenode-nouvelle**.
4. Cliquez sur le nœud de périmètre hello. Vous devez voir le point de terminaison SSH hello.

**la ruche toouse sur le nœud de périmètre hello**

1. Utilisez SSH tooconnect toohello bord nœud. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Après que vous être connecté toohello nœud de périmètre à l’aide de SSH, utilisez hello suivant la console de commande tooopen hello Hive :
   
        hive
3. Exécutez hello commande tooshow ruche tables suivantes dans le cluster de hello :
   
        show tables;

## <a name="delete-an-edge-node"></a>Supprimer un nœud de périmètre
Vous pouvez supprimer un nœud de hello portail Azure.

**tooaccess un nœud**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Ouvrez le cluster HDInsight de hello avec un nœud de périmètre.
3. Cliquez sur **Applications** à partir du Panneau de cluster hello. Vous devriez voir une liste des nœuds de périmètre.  
4. Nœud de périmètre avec le bouton hello vous souhaitez toodelete, puis cliquez sur **supprimer**.
5. Cliquez sur **Oui** tooconfirm.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment tooadd un nœud et comment tooaccess hello nœud de périmètre. toolearn, voir hello suivant des articles :

* [Installer des applications de HDInsight](hdinsight-apps-install-applications.md): Découvrez comment tooinstall un tooyour d’application HDInsight clusters.
* [Installer des applications personnalisées HDInsight](hdinsight-apps-install-custom-applications.md): Découvrez comment toodeploy un tooHDInsight d’application HDInsight non publiée.
* [Publier des applications de HDInsight](hdinsight-apps-publish-applications.md): Découvrez comment toopublish votre tooAzure d’applications personnalisée HDInsight Marketplace.
* [MSDN : Installer une application de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Découvrez comment toodefine HDInsight applications.
* [Personnaliser des clusters HDInsight de basés sur Linux à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md): Découvrez comment des applications supplémentaires toouse Action de Script tooinstall.
* [Créer des clusters basés sur Linux de Hadoop dans HDInsight à l’aide du Gestionnaire de ressources modèles](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Découvrez comment toocall le Gestionnaire de ressources modèles toocreate HDInsight clusters.

