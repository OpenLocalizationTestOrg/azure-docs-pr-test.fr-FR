---
title: aaaInstall Notebook localement & connecter le cluster Azure HDInsight Spark de tooan | Documents Microsoft
description: "Découvrez comment tooinstall bloc-notes jupyter localement sur votre ordinateur et le connecter le cluster d’Apache Spark tooan sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Installer un bloc-notes jupyter sur votre ordinateur et vous connecter tooApache Spark sur HDInsight

Cet article vous explique comment tooinstall bloc-notes jupyter, avec hello PySpark personnalisé (pour Python) et noyaux Spark (pour Scala) avec les nouvelles magic et connectez hello bloc-notes tooan HDInsight cluster. Il peut y avoir un certain nombre de raisons tooinstall Notebook sur votre ordinateur local, et il peut y avoir également certains défis. Pour plus d’informations, consultez la section de hello [Pourquoi dois-je installer Notebook sur mon ordinateur](#why-should-i-install-jupyter-on-my-computer) à fin hello de cet article.

Il existe trois étapes clés impliquées dans l’installation Notebook et hello magique de Spark sur votre ordinateur.

* Installation du bloc-notes Jupyter
* Installer hello PySpark et noyaux de Spark avec hello magique de Spark
* Configurer tooaccess magique de Spark cluster Spark sur HDInsight

Pour plus d’informations sur les noyaux personnalisée hello et magique de Spark hello disponible pour les ordinateurs portables Notebook avec le cluster HDInsight, consultez [clusters de noyaux disponibles pour les ordinateurs portables Notebook avec Apache Spark Linux sur HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Composants requis
conditions préalables de Hello répertoriés ici ne sont pas pour l’installation disponible. Il s’agit pour connexion hello Notebook bloc-notes tooan du cluster HDInsight une fois que l’ordinateur portable de hello est installé.

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Installer le bloc-notes Jupyter sur votre ordinateur

Vous devez installer Python avant de pouvoir installer les blocs-notes Jupyter. Python et Notebook sont disponibles dans le cadre de hello [distribution Anaconda](https://www.continuum.io/downloads). Lorsque vous installez Anaconda, vous installez une distribution de Python. Une fois que Anaconda est installé, vous ajoutez installation de Notebook hello en exécutant les commandes appropriées.

1. Télécharger hello [programme d’installation Anaconda](https://www.continuum.io/downloads) pour votre plateforme et le programme d’installation de l’exécution hello. Lors de l’exécution hello le programme d’installation de l’Assistant, assurez-vous que vous sélectionnez la variable de chemin d’accès de hello option tooadd Anaconda tooyour.
2. Exécutez hello suivant tooinstall de commande disponible.

        conda install jupyter

    Pour plus d’informations sur l’installation de Jupyter, consultez [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Installation de Jupyter à l’aide d’Anaconda).

## <a name="install-hello-kernels-and-spark-magic"></a>Installer les noyaux hello et magique de Spark

Pour plus d’informations sur comment magique de Spark tooinstall hello, hello PySpark et noyaux de Spark, suivez les instructions d’installation de hello Bonjour [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) sur GitHub. Hello première étape dans la documentation de hello Spark magie vous demande magique de Spark tooinstall. Remplacez cette première étape de lien de hello hello suivant de commandes, en fonction de la version de hello du cluster HDInsight de hello que vous vous connecterez. Après cela, suivez hello restant les étapes décrites dans la documentation de magic Spark hello. Si vous souhaitez que les noyaux différents tooinstall hello, vous devez effectuer l’étape 3 Bonjour section d’instructions Spark installation magic.

* Pour les clusters v3.4, installez sparkmagic 0.2.3 en exécutant `pip install sparkmagic==0.2.3`.

* Pour les clusters v3.5 et v3.6, installez sparkmagic 0.11.2 en exécutant `pip install sparkmagic==0.11.2`.

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Configurer le cluster Spark de Spark magic tooconnect tooHDInsight

Dans cette section, vous configurez magic Spark hello que vous avez installé antérieur cluster Apache Spark tooconnect tooan que vous devez avoir déjà créé dans Azure HDInsight.

1. Hello Notebook les informations de configuration est généralement stocké dans le répertoire de base hello. toolocate de commandes de votre répertoire de base sur n’importe quelle plateforme de système d’exploitation, hello du type suivant.

    Démarrer l’interpréteur de commandes hello Python. Dans une fenêtre de commande, tapez hello qui suit :

        python

    Sur hello shell de Python, entrez hello suivant toofind de commande out répertoire hello.

        import os
        print(os.path.expanduser('~'))

2. Accédez répertoire toohello et créez un dossier appelé **.sparkmagic** si elle n’existe pas déjà.
3. Dans le dossier de hello, créez un fichier appelé **config.json** et ajoutez hello suivant extrait de code JSON qu’il contient.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Remplacez **{USERNAME}**, **{CLUSTERDNSNAME}** et **{BASE64ENCODEDPASSWORD}** par les valeurs appropriées. Vous pouvez utiliser un certain nombre d’utilitaires dans votre langage de programmation favori ou le mot de passe codé en base64 de toogenerate en ligne pour votre mot de passe réel.

5. Configurer les paramètres de pulsation droite hello dans `config.json`. Vous devez ajouter ces paramètres au hello hello de même niveau `kernel_python_credentials` et `kernel_scala_credentials` des extraits de code votre ajouté précédemment. Pour un exemple montrant comment et où tooadd hello des paramètres de pulsation, consultez ce [exemple config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Pour `sparkmagic 0.2.3` (clusters v3.4), incluez :

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Pour `sparkmagic 0.11.2` (clusters v3.5 et v3.6), incluez :

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Tooensure que les sessions ne sont pas divulguées des pulsations sont envoyées. Lorsqu’un ordinateur passe toosleep ou est arrêté, n’est pas envoyée de pulsation de hello, ce qui en cours de session hello nettoyées. Pour les clusters v3.4, si vous le souhaitez toodisable ce comportement, vous pouvez définir hello Livy config `livy.server.interactive.heartbeat.timeout` trop`0` de hello Ambari UI. Pour les clusters v3.5, si vous ne définissez pas de configuration hello 3.5 ci-dessus, hello session ne sera pas supprimée.

6. Démarrez Jupyter. Utilisez hello de commande suivante à partir de l’invite de commandes hello.

        jupyter notebook

7. Vérifiez que vous pouvez vous connecter à cluster toohello à l’aide du bloc-notes jupyter de hello et que vous pouvez utiliser magique de Spark hello disponible avec les noyaux hello. Effectuer hello comme suit.

    a. Créer un nouveau bloc-notes. Dans l’angle supérieur droit de hello, cliquez sur **nouveau**. Vous devez voir le noyau par défaut de hello **Python2** et hello deux noyaux que vous installez, **PySpark** et **Spark**. Cliquez sur **PySpark**.

    ![Noyaux de bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Noyaux de bloc-notes Jupyter")

    b. Exécutez hello suivant extrait de code.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Si vous pouvez récupérer avec succès de sortie de hello, votre cluster HDInsight de toohello connexion est testée.

    >[!TIP]
    >Si vous souhaitez tooupdate hello bloc-notes configuration tooconnect tooa autre cluster, mettre à jour hello config.json hello nouvel ensemble de valeurs, comme indiqué dans l’étape 3 ci-dessus.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Pourquoi dois-je installer Jupyter sur mon ordinateur ?
Il peut y avoir un nombre de raisons pour lesquelles vous pouvez souhaitez tooinstall Notebook sur votre ordinateur et puis connectez-la de cluster tooa Spark sur HDInsight.

* Même si Notebook portables sont déjà disponibles sur le cluster de Spark hello dans Azure HDInsight, installation disponible sur votre ordinateur fournit hello option toocreate vos blocs-notes localement, tester votre application sur un cluster en cours d’exécution et puis télécharger hello cluster de toohello ordinateurs portables. cluster de toohello tooupload hello portables, vous pouvez soit les télécharger à l’aide du bloc-notes jupyter hello qui est en cours d’exécution ou hello de cluster, ou les enregistrer toohello /HdiNotebooks dossier hello compte de stockage associé au cluster de hello. Pour plus d’informations sur comment les ordinateurs portables sont stockées sur le cluster de hello, consultez [où sont stockés les blocs-notes Notebook](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Avec les ordinateurs portables de hello disponibles localement, vous pouvez vous connecter les clusters de Spark toodifferent en fonction de votre application.
* Vous pouvez utiliser GitHub tooimplement un système de contrôle de code source et contrôle de version pour les ordinateurs portables hello. Vous pouvez également avoir un environnement de collaboration où plusieurs utilisateurs peuvent travailler avec hello même bloc-notes.
* Vous pouvez travailler avec les blocs-notes localement sans avoir un cluster activé. Vous devez uniquement un tootest cluster vos blocs-notes contre, toomanually pas gérer vos ordinateurs portables ou un environnement de développement.
* Il est peut-être plus facile tooconfigure votre propre environnement de développement local qu’il s’agit tooconfigure hello Notebook installation sur un cluster de hello.  Vous pouvez tirer parti de tous les logiciels hello que vous avez installé localement sans configurer un ou plusieurs clusters à distance.

> [!WARNING]
> Avec Notebook installé sur votre ordinateur local, plusieurs utilisateurs peuvent exécuter hello même bloc-notes sur hello Spark même cluster au hello même temps. Dans ce cas, plusieurs sessions Livy sont créées. Si vous rencontrez un problème et que vous souhaitez toodebug, il sera un tootrack tâche complexe session Livy appartient toowhich utilisateur.
>
>

## <a name="seealso"></a>Voir aussi
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
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
