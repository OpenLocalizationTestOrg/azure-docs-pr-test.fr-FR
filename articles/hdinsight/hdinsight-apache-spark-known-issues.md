---
title: "cluster de problèmes aaaTroubleshoot avec Apache Spark dans Azure HDInsight | Documents Microsoft"
description: "En savoir plus sur les problèmes connexes tooApache les clusters de Spark dans Azure HDInsight et comment toowork autour de ceux."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Problèmes connus du cluster Apache Spark sur Azure HDInsight

Ce document effectue le suivi de hello tous les problèmes connus relatifs hello version préliminaire publique de HDInsight Spark.  

## <a name="livy-leaks-interactive-session"></a>Livy divulgue une session interactive
Au redémarrage Livy (à partir de Ambari ou en raison du redémarrage d’ordinateur virtuel tooheadnode 0) avec une session interactive toujours active, une session interactive des tâches est inutilisables. Pour cette raison, les nouveaux travaux peut bloqué dans hello état accepté et ne peut pas être démarré.

**Atténuation :**

Utilisez hello suivant le problème de procédure tooworkaround hello :

1. SSH dans le nœud principal. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Exécution hello après application de commande toofind hello ID des tâches interactives de hello démarrée par le biais Livy. 
   
        yarn application –list
   
    Hello les noms de tâche par défaut sera Livy si les travaux hello ont été démarrées avec une session interactive Livy sans nom explicite spécifié pour hello session Livy démarrée par un bloc-notes jupyter, nom de la tâche hello démarre avec remotesparkmagics_ *. 
3. La commande suivante d’exécution hello tookill ces travaux. 
   
        yarn application –kill <Application ID>

De nouvelles tâches commencent à être exécutées. 

## <a name="spark-history-server-not-started"></a>Serveur d’historique Spark non démarré
Le serveur d’historique Spark ne démarre pas automatiquement après la création d’un cluster.  

**Atténuation :** 

Démarrer manuellement le serveur de l’historique de hello d’Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problème d’autorisation dans le répertoire des journaux Spark
Lorsque hdiuser soumet un travail avec spark-submit, est un java.io.FileNotFoundException d’erreur : /var/log/spark/sparkdriver_hdiuser.log (autorisation refusée) et hello journal du pilote n’est pas écrit. 

**Atténuation :**

1. Ajouter un groupe de hdiuser toohello Hadoop. 
2. Fournissez les autorisations 777 sur /var/log/spark après la création du cluster. 
3. Mettre à jour à l’aide de Ambari toobe un répertoire avec des 777 autorisations de l’emplacement du journal de hello spark.  
4. Exécutez spark-submit en tant que sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Le connecteur Spark-Phoenix n’est pas pris en charge.

Actuellement, connecteur Spark-Phoenix de hello n’est pas pris en charge avec un cluster HDInsight Spark.

**Atténuation :**

Vous devez plutôt utiliser connecteur Spark-HBase de hello. Pour obtenir des instructions, consultez [comment toouse Spark-HBase connecteur](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Les problèmes liés à tooJupyter portables
Voici certains ordinateurs portables tooJupyter connexes de problèmes connus.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notebooks avec des caractères non-ASCII dans les noms de fichiers
Les notebooks Jupyter qui peuvent être utilisés dans les clusters Spark HDInsight ne doivent pas contenir de caractères non-ASCII dans les noms de fichiers. Si vous essayez de tooupload un fichier via hello UI Jupyter qui a un nom de fichier non-ASCII, il échouera en mode silencieux (autrement dit, Notebook ne vous permettre de télécharger le fichier de hello, mais elle ne lève soit une erreur visible). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Erreur lors du chargement de notebooks de taille supérieure
Vous pouvez obtenir une erreur **`Error loading notebook`** lorsque vous tentez de charger un bloc-notes de taille supérieure.  

**Atténuation :**

Si vous obtenez cette erreur, cela ne signifie pas que vos données sont endommagées ou perdues.  Vos blocs-notes sont toujours sur le disque dans `/var/lib/jupyter`, et vous pouvez SSH dans hello cluster tooaccess les. Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

Une fois que vous avez connecté cluster toohello à l’aide de SSH, vous pouvez copier vos blocs-notes à partir de votre ordinateur local à cluster tooyour (à l’aide du protocole SCP ou WinSCP) en tant qu’une perte de hello tooprevent sauvegarde de toutes les données importantes dans le bloc-notes de hello. Vous pouvez ensuite tunnel SSH dans votre nœud principal au niveau du port, 8001 tooaccess Notebook sans passer par la passerelle de hello.  À partir de là, vous pouvez effacer le résultat de hello de votre ordinateur portable et enregistrez à nouveau la taille de toominimize hello ordinateur portable.

tooprevent cette erreur se produise dans hello futur, vous devez suivre quelques meilleures pratiques :

* Il est important tookeep taille du bloc-notes hello petit. Sortie à partir de vos travaux Spark renvoyées tooJupyter est conservé dans le bloc-notes de hello.  Il est recommandé avec Notebook dans tooavoid général en cours d’exécution `.collect()` on RDD volumineux ou des trames de données ; en revanche, si vous souhaitez toopeek au contenu d’un RDD, envisagez d’exécuter `.take()` ou `.sample()` afin que la sortie n’obtient pas trop grande.
* En outre, lorsque vous enregistrez un ordinateur portable, désactivez toutes les cellules tooreduce hello la taille de sortie.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Démarrage du bloc-notes plus long que prévu
La première instruction de code du bloc-notes Jupyter avec Spark Magic peut nécessiter plusieurs minutes.  

**Explication :**

Cela se produit, car lorsque la première cellule de code hello est exécuté. En arrière-plan de hello cette commande lance d’une configuration de session et Spark, SQL, et les contextes de ruche sont définies. Une fois ces contextes, hello première instruction est exécutée, et cela donne l’impression hello qu’instruction de hello a eu un toocomplete beaucoup de temps.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Délai d’attente de bloc-notes Notebook lors de la création de session de hello
Lorsque le cluster Spark manque de ressources, hello Spark et noyaux Pyspark dans Bloc-notes jupyter de hello expireront au délai d’expiration de session de hello toocreate lors de la tentative. 

**Atténuations :** 

1. Libérez certaines ressources de votre cluster Spark :
   
   * L’arrêt d’autres blocs-notes Spark par toohello de va fermer et menu d’arrêt ou en cliquant sur l’arrêt dans l’Explorateur de bloc-notes hello.
   * Arrêtez les autres applications Spark à partir de YARN.
2. Redémarrez le bloc-notes hello que vous tentiez toostart des. Suffisamment de ressources doit être disponibles pour vous toocreate maintenant une session.

## <a name="see-also"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

