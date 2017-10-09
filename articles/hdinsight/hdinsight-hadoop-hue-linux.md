---
title: "aaaHue avec Hadoop sur des clusters basés sur Linux de HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment les clusters de teinte tooinstall sur HDInsight et utiliser le tunneling tooroute hello demandes tooHue. Utiliser le stockage teinte toobrowse et exécutez Hive ou Pig."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Installation et utilisation de Hue sur des clusters HDInsight Hadoop

Découvrez comment les clusters de teinte tooinstall sur HDInsight et utiliser le tunneling tooroute hello demandes tooHue.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-is-hue"></a>Qu’est-ce que Hue ?
La teinte représente qu'un ensemble d’applications Web utilisé toointeract avec un cluster Hadoop. Vous pouvez utiliser le stockage de hello teinte toobrowse associé à un cluster Hadoop (WASB, dans les cas de hello des clusters HDInsight), exécuter des travaux de la ruche et scripts Pig et ainsi de suite. Hello composants suivants sont disponibles avec les installations de teinte sur un cluster HDInsight Hadoop.

* Éditeur Beeswax Hive
* Pig
* Gestionnaire de Metastore
* Oozie
* FileBrowser (qui communique avec le conteneur de tooWASB par défaut)
* Explorateur de travaux

> [!WARNING]
> Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.
>
> Les composants personnalisés de réception efforcera toohelp vous toofurther hello de dépannage. Cela peut entraîner hello de résoudre ou demandant que vous tooengage les canaux disponibles pour hello ouvrir technologies source où se trouve une grande expérience pour cette technologie. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).
>
>

## <a name="install-hue-using-script-actions"></a>Installer Hue à l’aide d’actions de script

Hello script tooinstall teinte sur un cluster HDInsight de basés sur Linux est disponible à l’adresse https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Vous pouvez utiliser cette tooinstall script teinte sur les clusters avec des objets BLOB de stockage Azure (WASB) ou d’Azure Data Lake Store comme stockage par défaut.

Cette section fournit des instructions sur la façon dont toouse hello script lors de la configuration de cluster hello hello portail Azure à l’aide de.

> [!NOTE]
> Azure PowerShell, hello CLI d’Azure, hello HDInsight .NET SDK ou modèles Azure Resource Manager peuvent également être utilisés tooapply les actions de script. Vous pouvez également appliquer tooalready d’actions de script clusters en cours d’exécution. Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Démarrer l’approvisionnement d’un cluster à l’aide des étapes hello dans [HDInsight de configurer des clusters sur Linux](hdinsight-hadoop-provision-linux-clusters.md), mais n’effectuez pas la mise en service.

   > [!NOTE]
   > clusters de teinte tooinstall sur HDInsight, hello taille du nœud principal recommandée est d’au moins A4 (8 cœurs, 14 Go de mémoire).
   >
   >
2. Sur hello **Configuration facultative** panneau, sélectionnez **Actions de Script**et fournissent des informations de hello comme indiqué ci-dessous :

    ![Fournir des paramètres d’action de script pour Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Fournir des paramètres d’action de script pour Hue")

   * **NOM**: entrez un nom convivial pour l’action de script hello.
   * **URI du script** : https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**: cochez cette option.
   * **WORKER** : laissez ce champ vide.
   * **ZOOKEEPER** : laissez ce champ vide.
   * **PARAMÈTRES** : laissez ce champ vide.
3. En bas de hello Hello **Actions de Script**, utilisez hello **sélectionnez** configuration hello toosave du bouton. Enfin, utilisez hello **sélectionnez** bouton bas hello hello **Configuration facultative** informations de configuration facultatives panneau toosave hello.
4. Continuer la mise en service de cluster de hello comme décrit dans [HDInsight de configurer des clusters sur Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Utilisez Hue avec les clusters HDInsight

Le Tunneling de SSH est tooaccess de façon uniquement hello teinte sur le cluster de hello une fois qu’il est en cours d’exécution. Le tunnel via SSH permet de hello trafic toogo directement le nœud principal de toohello Hello de cluster dans lequel la teinte est en cours d’exécution. Une fois le cluster de hello a terminé la configuration, utilisez hello suivant les étapes toouse teinte sur un cluster HDInsight Linux.

> [!NOTE]
> Nous vous recommandons d’utiliser Firefox web navigateur toofollow hello des instructions ci-dessous.
>
>

1. Utilisez les informations de hello dans [tooaccess utiliser SSH Tunneling Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie et toute autre interface web utilisateur](hdinsight-linux-ambari-ssh-tunnel.md) toocreate un SSH à partir de votre cluster HDInsight de client système toohello du tunnel, puis configurez votre tunnel Web SSH du hello navigateur toouse en tant que proxy.

2. Une fois que vous avez créé un tunnel SSH et configuré votre navigateur tooproxy passer le trafic, vous devez rechercher le nom d’hôte hello de nœud principal de hello principal. Pour cela, en vous connectant cluster toohello à l’aide de SSH sur le port 22. Par exemple, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` où **nom d’utilisateur** est votre nom d’utilisateur SSH et **CLUSTERNAME** est le nom hello de votre cluster.

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Une fois connecté, utilisez hello suivant le nom de domaine complet de commande tooobtain hello de nœud principal de principal hello :

        hostname -f

    Cette opération retourne une nom similaire toohello suivant :

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Il s’agit hello les nom d’hôte de nœud principal de principal hello où se trouve le site Web de teinte hello.
4. Utilisez le portail teinte hello hello navigateur tooopen à http://HOSTNAME:8888. Remplacez nom d’hôte par nom hello obtenu à l’étape précédente de hello.

   > [!NOTE]
   > Lors de la connexion pour hello première fois, vous serez invité à toocreate un toolog de compte dans le portail de teinte toohello. informations d’identification Hello que vous spécifiez ici seront limité toohello portail et ne sont pas associées toohello admin ou informations d’identification de l’utilisateur SSH que vous avez spécifié lors de cluster hello de disposition.
   >
   >

    ![Portail de teinte de connexion toohello](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "spécifier les informations d’identification pour le portail de teinte")

### <a name="run-a-hive-query"></a>Exécution d'une tâche Hive
1. À partir du portail de teinte hello, cliquez sur **éditeurs de requête**, puis cliquez sur **Hive** éditeur de ruche tooopen hello.

    ![Utiliser Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Utiliser Hive")
2. Sur hello **aider** sous l’onglet sous **base de données**, vous devez voir **hivesampletable**. Il s’agit d’une table d’échantillon qui est livrée avec tous les clusters Hadoop sur HDInsight. Entrez un exemple de requête dans le volet de droite hello et de voir le résultat de hello sur hello **résultats** onglet dans le volet hello ci-dessous, comme indiqué dans la capture d’écran hello.

    ![Exécuter la requête Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Exécuter la requête Hive")

    Vous pouvez également utiliser hello **graphique** onglet toosee une représentation visuelle du résultat de hello.

### <a name="browse-hello-cluster-storage"></a>Parcourir le stockage de cluster hello
1. À partir du portail de teinte hello, cliquez sur **Explorateur de fichiers** dans hello en haut à droite de la barre de menus hello.
2. Explorateur de fichiers hello s’ouvre par défaut à hello **/utilisateur/myuser** active. Cliquez sur barre oblique hello juste avant le répertoire de l’utilisateur hello dans la racine de toohello toogo hello chemin d’accès du conteneur de stockage Azure hello associé hello cluster.

    ![Utiliser l’explorateur de fichiers](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Utiliser l’explorateur de fichiers")
3. Avec le bouton droit sur un fichier ou dossier toosee hello opérations disponibles. Hello d’utilisation **télécharger** bouton dans le répertoire actuel toohello des fichiers tooupload hello à droite. Hello d’utilisation **nouveau** bouton toocreate de nouveaux fichiers ou répertoires.

> [!NOTE]
> Explorateur teinte Hello peut uniquement afficher hello contenu du conteneur par défaut de hello associé au cluster HDInsight de hello. Tous les comptes/conteneurs de stockage supplémentaire peut associée à cluster de hello ne seront pas accessibles à l’aide d’Explorateur de fichiers hello. Toutefois, les conteneurs supplémentaires hello associés hello cluster sera toujours accessibles pour les travaux de ruche hello. Par exemple, si vous entrez la commande hello `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` dans l’éditeur de ruche hello, vous pouvez voir le contenu hello de supplémentaires en matière de conteneurs. Dans cette commande, **newcontainer** n’est pas hello par défaut conteneur est associé à un cluster.
>
>

## <a name="important-considerations"></a>Points importants à prendre en compte
1. Hello script utilisé tooinstall teinte installe uniquement sur le nœud principal de principal hello du cluster de hello.

2. Pendant l’installation, plusieurs services Hadoop (HDFS, fils, RM2, Oozie) sont redémarrés de mise à jour de la configuration de hello. Script de hello après l’installation de teinte, elle peut prendre du temps pour les autres toostart de services Hadoop. Cela peut affecter dans un premier temps les performances de Hue. Une fois que tous les services ont démarré, Hue est complètement fonctionnel.
3. Teinte ne comprend pas de Tez travaux, hello la valeur par défaut en cours pour la ruche. Si vous souhaitez toouse MapReduce comme hello moteur d’exécution de ruche, mettre à jour hello de toouse script hello commande dans votre script suivante :

        set hive.execution.engine=mr;

4. Avec des clusters Linux, vous pouvez avoir un scénario où vos services exécutent sur le nœud principal de principal hello tandis que hello Gestionnaire de ressources peut s’exécuter sur hello secondaire. Un tel scénario peut entraîner des erreurs (voir ci-dessous) lors de l’utilisation des détails de tooview de teinte de travaux sur le cluster de hello. Toutefois, vous pouvez afficher les détails d’une tâche hello lorsque hello est terminée.

   ![Erreur de portail Hue](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Erreur de portail Hue")

   Il s’agit de tooa problème connu. Pour résoudre ce problème, modifiez Ambari afin qu’hello active le Gestionnaire de ressources s’exécute également sur le nœud principal de principal hello.
5. Hue connaît WebHDFS, tandis que les clusters HDInsight utilisent le stockage Azure à l’aide de `wasb://`. Par conséquent, le script personnalisé hello utilisé avec l’action de script installe WebWasb, qui est un service WebHDFS compatibles pour communiquer avec tooWASB. Par conséquent, même si le portail de teinte hello indique HDFS endroits (comme lorsque vous déplacez votre souris sur hello **Explorateur de fichiers**), il doit être interprété comme WASB.

## <a name="next-steps"></a>Étapes suivantes
* [Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilisez tooinstall de personnalisation de cluster que giraph sur HDInsight Hadoop de clusters. Giraph vous permet de graphique tooperform le traitement à l’aide de Hadoop, et il peut être utilisé avec Azure HDInsight.
* [Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilisez tooinstall de personnalisation de cluster que solr sur HDInsight Hadoop de clusters. Solr vous permet de tooperform les opérations de recherche puissante sur les données stockées.
* [Installation de R sur des clusters HDInsight](hdinsight-hadoop-r-scripts-linux.md). Utilisez cluster personnalisation tooinstall R sur des clusters HDInsight Hadoop. R se compose d'un langage et d'un environnement open source destinés au calcul de statistiques. Il intègre des centaines de fonctions statistiques et possède son propre langage de programmation qui regroupe des aspects de la programmation fonctionnelle et de la programmation orientée objet. Il offre également des fonctionnalités graphiques étendues.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
