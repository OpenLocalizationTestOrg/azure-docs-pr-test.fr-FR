---
title: aaaIntroduction tooR Server sur Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse R Server sur les applications de toocreate HDInsight pour l’analyse de données volumineuses."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Introduction tooR serveur et des fonctionnalités de R open source sur HDInsight

Microsoft R Server est disponible en tant qu’option de déploiement lors de la création de clusters HDInsight dans Azure. Cette nouvelle fonctionnalité fournit des chercheurs de données, les statisticiens et les programmeurs R avec l’accès à la demande tooscalable, méthodes distribuées d’analytique sur HDInsight.

Clusters peuvent être dimensionnée de façon appropriée toohello projets et les tâches à effectuer et détruite puis lorsqu’ils ne sont plus nécessaires. Dans la mesure où ils font partie d’Azure HDInsight, ces clusters sont fournis avec prise en charge de niveau entreprise 24/7, un contrat SLA de 99,9 % un temps d’exécution et hello toointegrate de capacité avec d’autres composants Bonjour écosystème Azure.

R Server sur HDInsight permet hello plus récente d’analytique de R-basée sur les jeux de données de pratiquement n’importe quelle taille, chargé tooeither stockage d’objets Blob Azure ou lac de données. Étant donné que R Server repose sur R open source, applications hello basé sur R que vous créez peuvent tirer parti des packages hello 8000 + R open source. routines de Hello dans ScaleR, package d’analytique de données de Microsoft inclus avec R Server, sont également disponibles.

nœud de périmètre Hello d’un cluster fournit un emplacement pratique tooconnect toohello cluster toorun vos scripts R. Avec un nœud de périmètre, vous avez des fonctions d’option Hello en cours d’exécution parallélisée distributed hello de ScaleR entre les cœurs hello du serveur de nœud hello edge. Vous pouvez également exécuter les sur les nœuds hello du cluster de hello à l’aide de ScaleR Hadoop MapReduce ou Spark contextes de calcul.

modèles de Hello ou les prédictions qui résultent de l’analyse peut être téléchargé pour utilisent localement. Ils peuvent également être mis en œuvre ailleurs dans Azure, en particulier par le biais du [service web](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md) [Azure Machine Learning Studio](http://studio.azureml.net).

## <a name="get-started-with-r-on-hdinsight"></a>Prise en main de R sur HDInsight
tooinclude R Server dans un cluster HDInsight, vous devez sélectionner hello type de cluster R Server lors de la création d’un cluster HDInsight à l’aide de hello portail Azure. Hello, type de cluster R Server inclut R Server sur des nœuds de données hello du cluster de hello et sur un nœud de bord, qui sert d’une zone de lancement pour l’analytique de basé sur le serveur R. Consultez [prise en main de R Server sur HDInsight](hdinsight-hadoop-r-server-get-started.md) pour une procédure pas à pas sur la façon dont toocreate hello cluster.

## <a name="learn-about-data-storage-options"></a>En savoir plus sur les options de stockage de données
Stockage par défaut pour le système de fichiers HDFS hello des clusters HDInsight peut être associé à un compte de stockage Azure ou un magasin Azure Data Lake. Cette association permet de s’assurer que les données sont téléchargées toohello stockage en cluster lors de l’analyse est rendue persistante. Il existe différents outils de gestion des hello transfert toohello option de stockage que vous sélectionnez, notamment la fonctionnalité de téléchargement basé sur le portail de hello du compte de stockage hello et hello [AzCopy](../storage/common/storage-use-azcopy.md) utilitaire.

Vous pouvez hello Ajout d’accès tooadditional Blob et lake magasins de données pendant le processus, quelle que soit l’option de stockage principal hello en cours d’utilisation de configuration de cluster de hello. Consultez [prise en main de R Server sur HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) pour plus d’informations sur l’ajout de comptes d’accès tooadditional. Consultez hello supplémentaire [des options de stockage Azure pour R Server sur HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) toolearn article plus sur l’utilisation de plusieurs comptes de stockage.

Vous pouvez également utiliser [fichiers Azure](../storage/files/storage-how-to-use-files-linux.md) comme option de stockage pour une utilisation sur le nœud de périmètre hello. Fichiers Azure vous permet de toomount un partage de fichiers qui a été créé dans le stockage Azure toohello système de fichiers Linux. Pour plus d’informations concernant ces options de stockage de données pour R Server sur un cluster HDInsight, consultez la page [Options de stockage Azure pour R Server sur des clusters HDInsight](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>Serveur d’accès R sur le cluster de hello
Vous pouvez vous connecter tooR serveur sur le nœud de périmètre hello à l’aide d’un navigateur, à condition que vous avez choisi tooinclude RStudio serveur au cours de processus d’approvisionnement de hello. Si vous n’avez pas installé il lors de la configuration de cluster de hello, vous pouvez l’ajouter ultérieurement. Pour plus d’informations sur l’installation de RStudio Server après la création d’un cluster, consultez la page [Installer RStudio Server sur des clusters HDInsight](hdinsight-hadoop-r-server-install-r-studio.md). Vous pouvez également connecter toohello R Server à l’aide de SSH/PuTTY tooaccess hello R console. 

## <a name="develop-and-run-r-scripts"></a>Développer et exécuter des scripts R
vous créez et exécutez des scripts Hello R peuvent utiliser hello 8000 + packages R open source dans Ajout toohello parallélisée et distribués routines disponibles dans la bibliothèque de ScaleR hello. En général, un script qui est exécuté sur le nœud de périmètre hello avec R Server s’exécute au sein de l’interpréteur de hello R sur ce nœud. les exceptions de Hello sont les étapes qui doivent toocall une fonction ScaleR avec un contexte de calcul qui a la valeur tooHadoop MapReduce (RxHadoopMR) ou Spark (RxSpark). Dans ce cas, fonction hello s’exécute en mode distribué entre les nœuds du cluster de hello données (tâche) qui sont associés aux données hello référencées. Pour plus d’informations sur les options de contexte de calcul différents hello, consultez [de calcul des options de contexte pour le serveur de R sur HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Faire fonctionner un modèle
Lors de la modélisation des données est terminée, vous pouvez effectuent des prédictions de toomake modèle hello pour les nouvelles données à partir d’Azure et locales. Ce processus est appelé notation. La notation est possible dans HDInsight, dans Azure Machine Learning ou en local.

### <a name="score-in-hdinsight"></a>Noter dans HDInsight
tooscore dans HDInsight, écrivez une fonction R qui appelle votre modèle toomake des prédictions pour un nouveau fichier de données que vous avez chargé de compte de stockage tooyour. Enregistrez ensuite les prédictions hello compte de stockage toohello précédent. Vous pouvez exécuter hello routine à la demande sur le nœud de hello de périmètre de votre cluster ou à l’aide d’une tâche planifiée.  

### <a name="score-in-azure-machine-learning-aml"></a>Noter dans Azure Machine Learning (AML)
tooscore à l’aide d’un service web d’agréés, l’utilisation hello ouvre le package d’Azure Machine Learning R source appelé [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish votre modèle en tant que service web Azure. Pour plus de commodité, ce package est déjà installé sur le nœud de périmètre hello. Ensuite, utiliser des fonctions de hello dans Machine Learning toocreate une interface utilisateur pour le service web de hello, puis appelez service web de hello en fonction des besoins pour calculer les scores.

Si vous choisissez cette option, vous devez tooconvert tous les objets de modèle d’open source ScaleR modèle objets tooequivalent pour utilisent avec le service web de hello. Utilisez les fonctions de forçage de ScaleR, notamment `as.randomForest()` dans le cas des modèles basés sur un ensemble, pour cette conversion.

### <a name="score-on-premises"></a>Noter localement
tooscore locale après la création de votre modèle, vous pouvez sérialiser modèle hello dans R, téléchargement, désérialiser et l’utiliser pour le score de nouvelles données. Score de nouvelles données à l’aide d’approche hello décrit précédemment dans [de calcul de score dans HDInsight](#scoring-in-hdinsight) ou à l’aide de [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Mettre à jour de cluster de hello
### <a name="install-and-maintain-r-packages"></a>Installation et maintenance des packages R
La plupart des packages hello R que vous utilisez est requises sur le nœud de périmètre hello depuis la plupart des étapes de vos scripts R exécutées. tooinstall des packages R supplémentaires sur le nœud de périmètre hello, vous pouvez utiliser hello habituel `install.packages()` méthode dans R.

Si vous utilisez uniquement des routines de bibliothèque de ScaleR hello sur le cluster de hello, il est généralement inutile tooinstall des packages R supplémentaires sur les nœuds de données hello. Toutefois, vous devrez peut-être utiliser de hello toosupport packages supplémentaires de **rxExec** ou **RxDataStep** l’exécution sur les nœuds de données hello.

Dans ces cas, les packages supplémentaires hello peuvent être installés avec une action de script après avoir créé le cluster de hello. Pour plus d’informations, consultez la section [Création d’un cluster HDInsight avec R Server](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Modifier les paramètres de mémoire de Hadoop MapReduce
Un cluster peut être le montant de hello toochange modifiée de mémoire disponible tooR serveur lorsqu’il s’exécute un travail MapReduce. toomodify un cluster, utilisez hello Apache Ambari l’interface utilisateur qui est disponible via hello Panneau de portail Azure pour votre cluster. Pour savoir comment tooaccess hello Ambari UI pour votre cluster, voir [gérer les clusters HDInsight à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).

Il est également possible toochange hello quantité de mémoire disponible tooR serveur à l’aide de commutateurs de Hadoop dans l’appel de hello trop**RxHadoopMR** comme suit :

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Mettre à l’échelle votre cluster
Un cluster existant peut être mis à l’échelle vers le haut ou vers le bas via le portail de hello. Par la mise à l’échelle, vous pouvez obtenir une capacité supplémentaire hello que vous devrez peut-être pour des tâches de traitement supérieure, ou vous pouvez diminuer un cluster lorsqu’il est inactif. Pour obtenir des instructions sur la façon tooscale un cluster, consultez [HDInsight de gérer des clusters](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Mettre à jour le système de hello
Correctifs de maintenance tooapply du système d’exploitation et d’autres mises à jour est effectuée sur hello sous-jacent des machines virtuelles Linux dans un cluster HDInsight pendant les heures creuses. En règle générale, la maintenance est effectuée à 3 h 30 (basé sur l’heure locale hello pour hello VM) chaque lundi et le jeudi. Les mises à jour sont effectuées de manière à ce qu’ils n’avoir une incidence sur plus d’un quart de cluster de hello à la fois.  

Étant donné que les nœuds principaux hello sont redondantes et tous les nœuds de données sont affectés, tous les travaux qui sont en cours d’exécution peuvent ralentir. Ils doivent toujours s’exécuter toocompletion, toutefois. L’ensemble des logiciels personnalisés ou des données locales que vous détenez sont conservés durant ces événements de maintenance, sauf si une défaillance irrémédiable se produit, nécessitant une reconstruction du cluster.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>En savoir plus sur les options IDE pour R Server sur un cluster HDInsight
nœud de périmètre Hello Linux d’un cluster HDInsight est hello lancement de zone pour l’analyse basée sur R. Les versions récentes de HDInsight qui fournissent une option par défaut pour l’installation de version de communauté hello de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) sur le nœud de bord hello comme un IDE basé sur le navigateur. Utilisation de RStudio serveur comme un bus IDE pour le développement de hello et l’exécution de scripts R peuvent être beaucoup plus productifs que simplement à l’aide de la console de hello R. Si vous avez choisi pas tooadd RStudio serveur lors de la création d’hello cluster mais souhaitez tooadd il ultérieurement, puis consultez [installation R Studio Server sur les clusters HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Une autre option IDE complet est tooinstall un IDE bureau et utiliser cluster de hello tooaccess via l’utilisation d’un contexte de calcul MapReduce ou Spark à distance. Parmi les options disponibles figurent les [Outils R pour Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS) de Microsoft, RStudio et [StatET](http://www.walware.de/goto/statet) sur Eclipse de WalWare.

Enfin, vous pouvez accéder console de R Server hello sur le nœud de périmètre hello en tapant **R** à l’invite de commande hello Linux après vous être connecté via SSH ou PuTY. Lorsque vous utilisez l’interface de la console hello, il est pratique toorun un éditeur de texte pour le développement de script R dans une autre fenêtre, coupe et coller des sections de votre script dans la console de hello R en fonction des besoins.

## <a name="learn-about-pricing"></a>En savoir plus sur la tarification
Hello frais associés à un cluster de serveur R de HDInsight structurée de la même façon toohello des frais pour les clusters HDInsight standards hello. Elles sont basées sur le dimensionnement hello Hello sous-jacent de machines virtuelles sur le nom de hello, les données et les nœuds de bord, ajout de hello d’une extension de l’heure de la base. Pour plus d’informations sur la tarification HDInsight et la disponibilité de hello d’une version d’évaluation gratuite de 30 jours, consultez [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les clusters comment toouse R Server hdinsight, consultez hello rubriques suivantes :

* [Prise en main de R Server sur HDInsight](hdinsight-hadoop-r-server-get-started.md)
* [Ajouter RStudio Server tooHDInsight (si ne pas installé lors de la création du cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Options d’Azure Storage pour R Server sur HDInsight](hdinsight-hadoop-r-server-storage.md)
