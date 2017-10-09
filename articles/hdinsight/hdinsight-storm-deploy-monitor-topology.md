---
title: "aaaDeploy et gérer les topologies d’Apache Storm sur HDInsight | Documents Microsoft"
description: "Découvrez comment toodeploy, surveiller et gérer des topologies de Apache Storm à l’aide de hello du tableau de bord Storm sur HDInsight. Utilisez les outils Hadoop pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Déploiement et gestion des topologies Apache Storm sur HDInsight Windows

Hello Storm le tableau de bord vous permet de tooeasily déployer et exécuter le cluster HDInsight de Apache Storm topologies tooyour à l’aide de votre navigateur web. Vous pouvez également utiliser toomonitor du tableau de bord hello et gérer des topologies en cours d’exécution. Si vous utilisez Visual Studio, outils de HDInsight hello pour Visual Studio fournit des fonctionnalités similaires dans Visual Studio.

Hello Storm le tableau de bord et les fonctionnalités de tempête de hello Bonjour outils HDInsight s’appuient sur hello Storm REST API, qui peut être utilisé toocreate vos propres solutions de surveillance et de gestion.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent une tempête sur le cluster HDInsight qui utilise Windows comme système d’exploitation de hello. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour plus d’informations sur le déploiement et la gestion des topologies avec un cluster HDInsight utilisant Linux, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Linux](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Composants requis

* **Apache Storm sur HDInsight** : pour connaître les étapes de création d’un cluster, voir [Prise en main d’Apache Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started.md).

* Pourquoi **tableau de bord Storm**: un navigateur web moderne qui prend en charge de HTML5.

* Pour **Visual Studio** -Windows Azure SDK 2.5.1 ou plus récent et hello outils HDInsight pour Visual Studio. Consultez [prise en main à l’aide des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall et configurer les outils de hello HDInsight pour Visual Studio.

    Une des hello versions de Visual Studio suivantes :

  * Visual Studio 2012 avec Update 4

  * Visual Studio 2013 avec Update 4 ou Visual Studio 2013 Community

  * Visual Studio 2015 (toute édition)

  * Visual Studio 2017 (toute édition)

## <a name="storm-dashboard"></a>Tableau de bord Storm

Hello Storm le tableau de bord est une page web disponible sur votre cluster Storm. URL de Hello est **https://&lt;nom_cluster >.azurehdinsight.net/**, où **clustername** hello désigne votre Storm sur le cluster HDInsight.

À partir du haut hello Hello Storm le tableau de bord, sélectionnez **soumettre une topologie**. Suivez les instructions hello sur hello page toorun un exemple de topologie ou tooupload et exécuter une topologie que vous avez créé.

![Hello envoyer la page de la topologie][storm-dashboard-submit]

### <a name="storm-ui"></a>Interface utilisateur de Storm

À partir de hello Storm le tableau de bord, sélectionnez hello **Storm UI** lien. Cela affiche des informations sur le cluster de hello, dans tooany Ajout en cours d’exécution topologies.

![interface utilisateur de Hello storm][storm-dashboard-ui]

> [!NOTE]
> Avec certaines versions d’Internet Explorer, vous pouvez constater que hello que Storm UI n’actualise pas une fois que vous avez visités tout d’abord qu’il. Par exemple, il peut ne pas affiche les topologies de nouveau hello vous avez envoyé, ou il peut afficher une topologie comme active lorsque vous l’avez désactivée précédemment. Microsoft est conscient de ce problème et recherche actuellement une solution.

#### <a name="main-page"></a>Page principale

page principale de Hello Hello Storm UI fournit hello informations suivantes :

* **Résumé du cluster**: informations de base sur le cluster de Storm hello.

* **Résumé de la topologie**: une liste des topologies en cours d’exécution. Utilisez les liens hello tooview de cette section plus d’informations sur les topologies spécifiques.

* **Résumé de superviseur**: plus d’informations sur le superviseur de Storm hello.

* **Configuration de Nimbus**: configuration Nimbus pour le cluster de hello.

#### <a name="topology-summary"></a>Résumé de la topologie

Sélection d’un lien à partir de hello **récapitulatif de la topologie** section affiche hello informations sur la topologie de hello suivantes :

* **Résumé de la topologie**: informations de base sur la topologie de hello.

* **Actions de topologie**: actions de gestion que vous pouvez effectuer pour la topologie de hello.

  * **Activer**: reprend le traitement d’une topologie arrêtée.

  * **Désactiver**: suspend une topologie en cours d’exécution.

  * **Rééquilibrer**: ajuste le parallélisme hello de topologie de hello. Vous devez rééquilibrer les topologies en cours d’exécution une fois que vous avez modifié le nombre de hello de nœuds de cluster de hello. Cela permet hello topologie tooadjust parallélisme toocompensate pour hello augmenté ou diminué le nombre de nœuds de cluster de hello.

      Pour plus d’informations, consultez [présentation parallélisme hello d’une topologie de Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **KILL**: met fin à une topologie Storm après hello spécifié le délai d’attente.

* **Statistiques de topologie**: statistiques sur la topologie de hello. Utilisez les liens hello hello **fenêtre** colonne tooset hello période hello écritures de page de hello restantes.

* **Becs verseurs amovibles**: hello becs verseurs utilisés par la topologie de hello. Utilisez les liens hello tooview de cette section plus d’informations sur becs verseurs spécifiques.

* **Boulons**: hello boulons utilisés par la topologie de hello. Utilisez les liens hello tooview de cette section plus d’informations sur les boulons spécifiques.

* **Configuration de la topologie**: configuration hello de topologie de hello sélectionné.

#### <a name="spout-and-bolt-summary"></a>Résumé relatif aux spouts et aux bolts

En sélectionnant un bec de hello **becs verseurs amovibles** ou **boulons** sections affiche hello suit les informations d’élément de hello sélectionné :

* **Résumé des composants**: informations de base sur bec de hello ou éclair.

* **BEC/éclair statistiques**: statistiques sur hello bec ou boulon. Utilisez les liens hello hello **fenêtre** colonne tooset hello période hello écritures de page de hello restantes.

* **D’entrée statistiques** (boulon uniquement) : flux consommées par un éclair de hello d’entrée le plus d’informations sur hello.

* **Statistiques de sortie**: plus d’informations sur les flux hello émis par ce bec ou boulon.

* **Les exécuteurs**: informations sur les instances de hello de bec de hello ou éclair. Sélectionnez hello **Port** entrée pour un tooview spécifique de l’exécuteur un journal d’informations de diagnostic généré pour cette instance.

* **Erreurs**: les informations d’erreur pour ce spout ou ce bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>Outils HDInsight pour Visual Studio

Hello HDInsight outils peut être utilisé toosubmit c# ou hybride topologies tooyour cluster Storm. Hello suit utilisent un exemple d’application. Pour plus d’informations sur la création de vos propres topologies à l’aide des outils de HDInsight hello, consultez [C# développer des topologies à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Utilisez hello suivant les étapes toodeploy un tooyour exemple tempête de cluster HDInsight, puis afficher et gérer la topologie hello.

1. Si vous n’avez pas déjà installé hello dernière version de hello outils HDInsight pour Visual Studio, consultez [prise en main à l’aide des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau** > **Projet**.

3. Bonjour **nouveau projet** boîte de dialogue, développez **installé** > **modèles**, puis sélectionnez **HDInsight**. Dans la liste hello des modèles, sélectionnez **Storm exemple**. Bas hello de boîte de dialogue hello, tapez un nom pour l’application hello.

    ![image](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **envoyer tooStorm sur HDInsight**.

   > [!NOTE]
   > Si vous y êtes invité, entrez les informations d’identification de connexion hello pour votre abonnement Azure. Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.

5. Sélectionnez votre Storm sur le cluster HDInsight à partir de hello **Cluster Storm** liste déroulante et sélectionnez **Submit**. Vous pouvez surveiller si l’envoi de hello réussit à l’aide de hello **sortie** fenêtre.

6. Lors de la topologie de hello a été envoyé avec succès, hello **Storm Topologies** pour le cluster de hello doit apparaître. Sélectionnez la topologie de hello dans hello liste tooview informations hello topologie en cours d’exécution.

    ![Visual Studio Monitor](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs** en développant **Azure** > **HDInsight**, puis en cliquant avec le bouton droit sur le cluster HDInsight et en sélectionnant **Affichage des topologies Storm**.

    Sélectionnez la forme de hello pour hello becs verseurs amovibles ou boulons tooview d’informations sur ces composants. Une nouvelle fenêtre s’ouvre pour chaque élément sélectionné.

   > [!NOTE]
   > nom Hello de topologie de hello est le nom de classe hello de topologie de hello (dans ce cas, `HelloWord`,) avec un horodatage ajouté.

7. À partir de hello **récapitulatif de la topologie** afficher, sélectionnez **Kill** topologie de hello toostop.

   > [!NOTE]
   > Les topologies Storm poursuivre l’exécution jusqu'à ce qu’ils sont arrêtés ou cluster de hello est supprimé.


## <a name="rest-api"></a>API REST

Hello Storm UI repose sur hello API REST, afin de pouvoir effectuer similaires de gestion et de la fonctionnalité d’analyse à l’aide des API REST de hello. Vous pouvez utiliser des outils personnalisés hello API REST toocreate pour gérer et surveiller les topologies de Storm.

Pour plus d’informations, consultez la rubrique [API REST de l’interface utilisateur Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Hello informations suivantes sont spécifiques toousing hello API REST avec Apache Storm sur HDInsight.

### <a name="base-uri"></a>URI de base

Hello est de l’URI de base pour l’API REST de hello sur les clusters HDInsight **https://&lt;nom_cluster >.azurehdinsight.net/stormui/api/v1/**, où **clustername** désigne hello votre Storm sur Cluster HDInsight.

### <a name="authentication"></a>Authentification

Toohello demandes API REST doivent utiliser **l’authentification de base**, de sorte que vous utilisez le nom du cluster hello HDInsight administrateur et le mot de passe.

> [!NOTE]
> Étant donné que l’authentification de base est envoyée à l’aide de texte en clair, vous devez **toujours** utiliser les communications HTTPS toosecure avec cluster de hello.

### <a name="return-values"></a>Valeurs de retour

Informations qui sont retournées à partir de hello API REST peuvent uniquement être utilisable à partir de cluster de hello ou ordinateurs virtuels sur hello même réseau virtuel Azure en tant que cluster de hello. Par exemple, nom de domaine complet de hello (FQDN) retournée pour les serveurs soigneur ne sont pas être accessible à partir de hello Internet.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment topologies toodeploy et le moniteur à l’aide de hello Storm le tableau de bord, découvrez comment :

* [Développer les topologies c# à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Développer des topologies basées sur Java à l’aide de Maven](hdinsight-storm-develop-java-topology.md)

Pour accéder à une liste d’exemples supplémentaires de topologies, consultez la rubrique [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
