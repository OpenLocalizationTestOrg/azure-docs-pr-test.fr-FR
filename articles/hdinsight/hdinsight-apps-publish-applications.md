---
title: applications de HDInsight aaaPublish - Azure | Documents Microsoft
description: "Découvrez comment toocreate et publier des applications de HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Publier des applications HDInsight dans hello Azure Marketplace
Une application HDInsight est une application que les utilisateurs peuvent installer sur un cluster HDInsight sous Linux. Ces applications peuvent être développées par Microsoft, par des éditeurs de logiciels indépendants (ISV) ou par vous-même. Dans cet article, vous apprendrez comment toopublish une application HDInsight dans hello Azure Marketplace.  Pour obtenir des informations générales sur la publication dans hello Azure Marketplace, consultez [publier un toohello offre Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

Les applications HDInsight utilisent hello *mettre votre propre licence (BYOL)* modèle, le fournisseur de l’application est responsable de la licence tooend-utilisateurs de l’application hello, alors que les utilisateurs finaux sont uniquement facturé par Azure pour les ressources de hello ils Créez, telles que le cluster HDInsight de hello et ses machines virtuelles/nœuds. Actuellement, la facturation pour l’application hello elle-même n’est pas effectuée via Azure.

Autre article concernant les applications HDInsight :

* [Installer des applications de HDInsight](hdinsight-apps-install-applications.md): Découvrez comment tooinstall un tooyour d’application HDInsight clusters.
* [Installer des applications personnalisées HDInsight](hdinsight-apps-install-custom-applications.md): Découvrez comment tooinstall et test des applications HDInsight personnalisées.

## <a name="prerequisites"></a>Composants requis
toosubmit votre marketplace toohello application personnalisée, vous devez avoir créé et testé votre application personnalisée. Consultez hello suivant des articles :

* [Installer des applications personnalisées HDInsight](hdinsight-apps-install-custom-applications.md): Découvrez comment tooinstall et test des applications HDInsight personnalisées.

Vous devez également avoir inscrit votre compte de développeur. Consultez [publier un toohello offre Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) et [créer un compte Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Définir l’application
Il existe deux étapes impliquées pour la publication d’applications toohello Azure Marketplace.  Vous définissez d’abord un **createUiDef.json** tooindicate fichier dont les clusters de votre application est compatible avec ; et que vous publiez modèle hello hello portail Azure. Hello suivant la section est un exemple de fichier createUiDef.json.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Champ | Description | Valeurs possibles |
| --- | --- | --- |
| types |types de cluster de Hello application hello est compatible avec. |Hadoop, HBase, Storm, Spark (ou toute combinaison de ceux-ci) |
| tiers |niveaux de cluster Hello application hello est compatible avec. |Standard, Premium, (ou les deux) |
| versions |les types du cluster HDInsight Hello hello application est compatible avec. |3.4 |

## <a name="application-install-script"></a>Script d’installation d’application
Chaque fois qu’une application est installée sur un cluster (un existant ou un autre), un nœud est créé et le script d’installation hello application est exécutée sur celui-ci.
  > [!IMPORTANT]
  > nom Hello des noms de script installation hello application doit être unique pour un cluster particulier avec hello suivant le format.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Notez qu’il y nom du script toohello trois parties :
  > 
  > 1. Préfixe de nom de script, qui comprend le nom de l’application hello ou d’une application toohello appropriées de nom.
  > 2. Un tiret, pour une meilleure lisibilité.
  > 3. Fonction de chaîne unique avec le nom de l’application hello comme paramètre de hello.
  > 
  > Est un exemple hello ci-dessus finit devenant : teinte-install-v0-4wkahss55hlas Bonjour persistante la liste des actions de script. Pour obtenir un exemple de charge JSON, consultez [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
script d’installation Hello doit avoir hello suivant caractéristiques :
1. Assurez-vous que le script de hello est idempotente. Plusieurs appels toohello script doit produire hello même résultat.
2. script de Hello doit être gérée correctement. Utiliser un autre emplacement pour le script de hello lors de la mise à niveau ou de tester des modifications afin que les clients qui essaient d’application de hello tooinstall ne sont pas affectées. 
3. Ajouter des scripts de journalisation adéquates toohello à chaque point. Hello généralement les journaux de script est hello seule façon toodebug installation des applications.
4. Assurez-vous que les appels tooexternal services ou des ressources ont des tentatives adéquates afin que l’installation de hello n’est pas affectée par des problèmes réseau temporaires.
5. Si votre script de démarrage des services sur les nœuds de hello, vérifiez que hello sont analysés et configurer les services toostart automatiquement en cas de redémarrage à un autre nœud.

## <a name="package-application"></a>Empaqueter une application
Créez un fichier zip qui contient tous les fichiers requis pour l’installation de vos applications HDInsight. Vous devez hello fichier zip dans [publier l’application](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. Voir un exemple dans l’article [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md)(Installer des applications HDInsight personnalisées).
* Tous les scripts nécessaires.

> [!NOTE]
> Hello des fichiers d’application (y compris les fichiers d’application web le cas échéant) peut se trouver sur n’importe quel point de terminaison accessible publiquement.
> 

## <a name="publish-application"></a>Publication de l’application
Suivez hello suivant les étapes toopublish une application HDInsight :

1. Ouverture de session toohello [portail de publication Azure](https://publish.windowsazure.com/).
2. Cliquez sur **des modèles de Solution** de toocreate de gauche hello un nouveau modèle de solution.
3. Entrez un titre, puis cliquez sur **Créer un modèle de solution**.
4. Cliquez sur **compte Centre de développement de créer et jointure hello programme Azure** tooregister votre entreprise si vous n’avez pas encore fait.  Consultez les pages [Créer un compte de développeur Microsoft](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Cliquez sur **définir certains tooget Topologies démarré**. Un modèle de solution est un tooall « parent » ses topologies. Vous pouvez définir plusieurs topologies dans une offre/un modèle de solution. Lorsqu’une offre est envoyée toostaging, il est envoyé avec toutes les topologies de son. 
6. Entrez un nom de la topologie, puis cliquez sur le signe plus hello.
7. Entrez une nouvelle version, puis cliquez sur hello signe Plus.
8. Fichier zip de téléchargement hello préparé à [Package d’application](#package-application).  
9. Cliquez sur **Request Certification**(Demander la certification). équipe de certification Microsoft Hello sera passez en revue les fichiers hello et certifie la topologie de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Installer des applications de HDInsight](hdinsight-apps-install-applications.md): Découvrez comment tooinstall un tooyour d’application HDInsight clusters.
* [Installer des applications personnalisées HDInsight](hdinsight-apps-install-custom-applications.md): Découvrez comment toodeploy un tooHDInsight d’application HDInsight non publiée.
* [Personnaliser des clusters HDInsight de basés sur Linux à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md): Découvrez comment des applications supplémentaires toouse Action de Script tooinstall.
* [Créer des clusters basés sur Linux de Hadoop dans HDInsight à l’aide de modèles Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Découvrez comment toocall le Gestionnaire de ressources modèles toocreate HDInsight clusters.
* [Utiliser noeuds vide dans HDInsight](hdinsight-apps-use-edge-node.md): Découvrez comment toouse vide bord du nœud pour l’accès à cluster HDInsight, test des applications de HDInsight et l’hébergement des applications de HDInsight.

